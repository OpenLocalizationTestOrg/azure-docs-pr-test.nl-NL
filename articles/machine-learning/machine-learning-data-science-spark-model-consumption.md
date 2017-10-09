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
# <a name="operationalize-spark-built-machine-learning-models"></a><span data-ttu-id="3c6ab-103">Spark is gebouwd machine learning-modellen operationeel maken</span><span class="sxs-lookup"><span data-stu-id="3c6ab-103">Operationalize Spark-built machine learning models</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="3c6ab-104">Dit onderwerp leest hoe toooperationalize een opgeslagen machine learning-model (ML) met behulp van Python op HDInsight Spark-clusters.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-104">This topic shows how toooperationalize a saved machine learning model (ML) using Python on HDInsight Spark clusters.</span></span> <span data-ttu-id="3c6ab-105">Hierin wordt beschreven hoe tooload machine learning-modellen die zijn gebouwd met behulp van Spark MLlib en opgeslagen in Azure Blob Storage (WASB) en hoe tooscore ze met gegevenssets die ook in WASB zijn opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-105">It describes how tooload machine learning models that have been built using Spark MLlib and stored in Azure Blob Storage (WASB), and how tooscore them with datasets that have also been stored in WASB.</span></span> <span data-ttu-id="3c6ab-106">Er wordt weergegeven hoe toopre proces Hallo invoergegevens, transformatie-onderdelen met de functies voor indexering en codering in Hallo MLlib toolkit en hoe toocreate een gelabelde punt gegevensobject die kan worden gebruikt als invoer voor batchscoreberekening met Hallo ML modellen Hallo.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-106">It shows how toopre-process hello input data, transform features using hello indexing and encoding functions in hello MLlib toolkit, and how toocreate a labeled point data object that can be used as input for scoring with hello ML models.</span></span> <span data-ttu-id="3c6ab-107">Hallo-modellen gebruikt voor score berekenen bevatten lineaire regressie, Logistic Regression willekeurige Forest modellen en kleurovergang versterking structuur modellen.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-107">hello models used for scoring include Linear Regression, Logistic Regression, Random Forest Models, and Gradient Boosting Tree Models.</span></span>

## <a name="spark-clusters-and-jupyter-notebooks"></a><span data-ttu-id="3c6ab-108">Spark-clusters en Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="3c6ab-108">Spark clusters and Jupyter notebooks</span></span>
<span data-ttu-id="3c6ab-109">Instellingsstappen en Hallo code toooperationalize ML-model beschikbaar zijn in dit scenario voor het gebruik van een HDInsight Spark 1.6-cluster, evenals een 2.0 Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-109">Setup steps and hello code toooperationalize an ML model are provided in this walkthrough for using an HDInsight Spark 1.6 cluster as well as a Spark 2.0 cluster.</span></span> <span data-ttu-id="3c6ab-110">Hallo-code voor deze procedures is ook beschikbaar in Jupyter-notebooks.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-110">hello code for these procedures is also provided in Jupyter notebooks.</span></span>

### <a name="notebook-for-spark-16"></a><span data-ttu-id="3c6ab-111">Laptop voor Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="3c6ab-111">Notebook for Spark 1.6</span></span>
<span data-ttu-id="3c6ab-112">Hallo [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) Jupyter-notebook ziet u hoe toooperationalize een opgeslagen model met behulp van Python op HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-112">hello [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) Jupyter notebook shows how toooperationalize a saved model using Python on HDInsight clusters.</span></span> 

### <a name="notebook-for-spark-20"></a><span data-ttu-id="3c6ab-113">Laptop voor Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="3c6ab-113">Notebook for Spark 2.0</span></span>
<span data-ttu-id="3c6ab-114">toomodify hello Jupyter-notebook voor Spark 1.6 toouse met een cluster HDInsight Spark 2.0 vervangen Hallo Python code-bestand met [dit bestand](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span><span class="sxs-lookup"><span data-stu-id="3c6ab-114">toomodify hello Jupyter notebook for Spark 1.6 toouse with an HDInsight Spark 2.0 cluster, replace hello Python code file with [this file](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span></span> <span data-ttu-id="3c6ab-115">Deze code laat zien hoe tooconsume Hallo modellen gemaakt in Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-115">This code shows how tooconsume hello models created in Spark 2.0.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="3c6ab-116">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3c6ab-116">Prerequisites</span></span>

1. <span data-ttu-id="3c6ab-117">U moet een Azure-account en een 1.6 Spark (of Spark 2.0) HDInsight-cluster toocomplete in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-117">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster toocomplete this walkthrough.</span></span> <span data-ttu-id="3c6ab-118">Zie Hallo [overzicht van Gegevenswetenschap met Spark op Azure HDInsight](machine-learning-data-science-spark-overview.md) voor instructies over het toosatisfy deze vereisten.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-118">See hello [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how toosatisfy these requirements.</span></span> <span data-ttu-id="3c6ab-119">Dit onderwerp bevat ook een beschrijving van Hallo NYC 2013 Taxi gegevens hier gebruikt en instructies over hoe tooexecute code van een Jupyter-notebook in Spark-cluster Hallo.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-119">That topic also contains a description of hello NYC 2013 Taxi data used here and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster.</span></span> 
2. <span data-ttu-id="3c6ab-120">Moet u ook maken Hallo machine learning-modellen toobe berekend hier doorloopt Hallo [gegevensverkenning en modellering met Spark](machine-learning-data-science-spark-data-exploration-modeling.md) onderwerp voor Hallo 1.6 Spark-cluster of Hallo Spark 2.0-laptops.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-120">You must also create hello machine learning models toobe scored here by working through hello [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic for hello Spark 1.6 cluster or hello Spark 2.0 notebooks.</span></span> 
3. <span data-ttu-id="3c6ab-121">Hallo Spark 2.0-notebooks gebruiken een aanvullende gegevensset voor Hallo classificatietaak Hallo bekende luchtvaartmaatschappij tijdige vertrek gegevensset van 2011 en 2012.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-121">hello Spark 2.0 notebooks use an additional data set for hello classification task, hello well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="3c6ab-122">Een beschrijving van het Hallo-notitieblokken en -koppelingen toothem vindt u in Hallo [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) voor Hallo GitHub-opslagplaats met ze.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-122">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="3c6ab-123">Bovendien Hallo code hier en in notitieblokken Hallo gekoppeld is algemeen en moet werken op een Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-123">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="3c6ab-124">Als u geen van HDInsight Spark, Hallo clusterinstallatie gebruikmaakt en management stappen mogelijk enigszins afwijken van wat hier moet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-124">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> 

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="3c6ab-125">Setup: opslaglocaties, bibliotheken en Hallo voorinstelling Spark-context</span><span class="sxs-lookup"><span data-stu-id="3c6ab-125">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="3c6ab-126">Spark is kunnen tooread en write tooan Azure Storage-Blob (WASB).</span><span class="sxs-lookup"><span data-stu-id="3c6ab-126">Spark is able tooread and write tooan Azure Storage Blob (WASB).</span></span> <span data-ttu-id="3c6ab-127">Dus een van uw bestaande gegevens opgeslagen kunnen worden verwerkt met Spark en Hallo resultaten WASB opgeslagen opnieuw in.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-127">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="3c6ab-128">toosave modellen of bestanden in WASB moet Hallo pad toobe juist opgegeven.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-128">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="3c6ab-129">Hallo standaard verbonden container toohello Spark-cluster kan worden verwezen met behulp van een pad die begint met: *' wasb / / '*.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-129">hello default container attached toohello Spark cluster can be referenced using a path beginning with: *"wasb//"*.</span></span> <span data-ttu-id="3c6ab-130">Hallo volgende codevoorbeeld geeft Hallo locatie van Hallo gegevens toobe lezen en Hallo pad voor Hallo model opslag directory toowhich Hallo model uitvoer wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-130">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved.</span></span> 

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="3c6ab-131">Directory-paden voor opslaglocaties in WASB instellen</span><span class="sxs-lookup"><span data-stu-id="3c6ab-131">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="3c6ab-132">Modellen worden opgeslagen in: "wasb: / / / gebruiker/remoteuser/NYCTaxi/modellen '.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-132">Models are saved in: "wasb:///user/remoteuser/NYCTaxi/Models".</span></span> <span data-ttu-id="3c6ab-133">Als dit pad is niet correct ingesteld, worden de modellen niet voor score berekenen geladen.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-133">If this path is not set properly, models are not loaded for scoring.</span></span>

<span data-ttu-id="3c6ab-134">Hallo scored resultaten zijn opgeslagen: "wasb: / / / gebruiker/remoteuser/NYCTaxi/ScoredResults '.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-134">hello scored results have been saved in: "wasb:///user/remoteuser/NYCTaxi/ScoredResults".</span></span> <span data-ttu-id="3c6ab-135">Als Hallo pad toofolder onjuist is, worden resultaten niet opgeslagen in de map.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-135">If hello path toofolder is incorrect, results are not saved in that folder.</span></span>   

> [!NOTE]
> <span data-ttu-id="3c6ab-136">Hallo-bestandslocaties pad kunnen worden gekopieerd en geplakt Hallo tijdelijke aanduidingen in deze code uit de uitvoer van de laatste cel Hallo HALLO hallo **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notebook.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-136">hello file path locations can be copied and pasted into hello placeholders in this code from hello output of hello last cell of hello **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notebook.</span></span>   
> 
> 

<span data-ttu-id="3c6ab-137">Hier volgt tooset Hallo-directory codepaden:</span><span class="sxs-lookup"><span data-stu-id="3c6ab-137">Here is hello code tooset directory paths:</span></span> 

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

<span data-ttu-id="3c6ab-138">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="3c6ab-138">**OUTPUT:**</span></span>

<span data-ttu-id="3c6ab-139">DateTime.DateTime (2016, 4, 25, 23, 56, 19, 229403)</span><span class="sxs-lookup"><span data-stu-id="3c6ab-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="3c6ab-140">Bibliotheken importeren</span><span class="sxs-lookup"><span data-stu-id="3c6ab-140">Import libraries</span></span>
<span data-ttu-id="3c6ab-141">Context voor spark instellen en benodigde bibliotheken importeren met de volgende code Hallo</span><span class="sxs-lookup"><span data-stu-id="3c6ab-141">Set spark context and import necessary libraries with hello following code</span></span>

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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="3c6ab-142">Vooraf context voor Spark en PySpark magics</span><span class="sxs-lookup"><span data-stu-id="3c6ab-142">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="3c6ab-143">Hallo PySpark kernels die worden geleverd met Jupyter-notebooks hebben een vooraf ingestelde context.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-143">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="3c6ab-144">Dus hoeft u niet tooset Hallo Spark of Hive-contexten expliciet voordat u begint te werken met Hallo-toepassing die u ontwikkelt.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-144">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="3c6ab-145">Dit zijn standaard beschikbaar voor u.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-145">These are available for you by default.</span></span> <span data-ttu-id="3c6ab-146">Deze contexten zijn:</span><span class="sxs-lookup"><span data-stu-id="3c6ab-146">These contexts are:</span></span>

* <span data-ttu-id="3c6ab-147">SC - voor Spark</span><span class="sxs-lookup"><span data-stu-id="3c6ab-147">sc - for Spark</span></span> 
* <span data-ttu-id="3c6ab-148">sqlContext - voor Hive</span><span class="sxs-lookup"><span data-stu-id="3c6ab-148">sqlContext - for Hive</span></span>

<span data-ttu-id="3c6ab-149">Hallo PySpark-kernel biedt een aantal vooraf gedefinieerde 'magics', die zijn speciale opdrachten die u met aanroepen kunt %%.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-149">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="3c6ab-150">Er zijn twee dergelijke opdrachten die worden gebruikt in deze codevoorbeelden.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-150">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="3c6ab-151">**%% lokale** opgegeven Hallo-code in de volgende regels lokaal wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-151">**%%local** Specified that hello code in subsequent lines is executed locally.</span></span> <span data-ttu-id="3c6ab-152">De sitecode moet geldige Python-code.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-152">Code must be valid Python code.</span></span>
* <span data-ttu-id="3c6ab-153">**%% sql -o<variable name>**</span><span class="sxs-lookup"><span data-stu-id="3c6ab-153">**%%sql -o <variable name>**</span></span> 
* <span data-ttu-id="3c6ab-154">Een Hive-query op Hallo sqlContext worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-154">Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="3c6ab-155">Als het Hallo -o parameter is doorgegeven, Hallo resultaat van Hallo query blijft behouden in Hallo %% lokale Python context als een dataframe Pandas.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-155">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas dataframe.</span></span>

<span data-ttu-id="3c6ab-156">Voor meer informatie over het Hallo kernels voor Jupyter-notebooks en vooraf gedefinieerde Hallo 'magics' die ze bieden, Zie [beschikbare Kernels voor Jupyter-notebooks met HDInsight Spark Linux-clusters in HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="3c6ab-156">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="ingest-data-and-create-a-cleaned-data-frame"></a><span data-ttu-id="3c6ab-157">Voor het opnemen van gegevens en een kader opgeschoonde gegevens maken</span><span class="sxs-lookup"><span data-stu-id="3c6ab-157">Ingest data and create a cleaned data frame</span></span>
<span data-ttu-id="3c6ab-158">Deze sectie bevat Hallo-code voor een reeks van taken vereist tooingest Hallo gegevens toobe berekend.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-158">This section contains hello code for a series of tasks required tooingest hello data toobe scored.</span></span> <span data-ttu-id="3c6ab-159">In een gekoppelde 0,1% voorbeeld van Hallo taxi reis en tarief bestand (opgeslagen als een bestand .tsv), indeling Hallo gegevens te kunnen lezen en maakt vervolgens een frame gegevens wissen.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-159">Read in a joined 0.1% sample of hello taxi trip and fare file (stored as a .tsv file), format hello data, and then creates a clean data frame.</span></span>

<span data-ttu-id="3c6ab-160">Hallo taxi reis en tarief dat bestanden op basis zijn gekoppeld op Hallo procedure die is opgegeven de: [Hallo Team gegevens wetenschappelijke processen in actie: met behulp van HDInsight Hadoop-clusters](machine-learning-data-science-process-hive-walkthrough.md) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-160">hello taxi trip and fare files were joined based on hello procedure provided in the: [hello Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) topic.</span></span>

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

<span data-ttu-id="3c6ab-161">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="3c6ab-161">**OUTPUT:**</span></span>

<span data-ttu-id="3c6ab-162">Tijd tooexecute boven cel: 46.37 seconden</span><span class="sxs-lookup"><span data-stu-id="3c6ab-162">Time taken tooexecute above cell: 46.37 seconds</span></span>

## <a name="prepare-data-for-scoring-in-spark"></a><span data-ttu-id="3c6ab-163">Gegevens voorbereiden voor score berekenen in Spark</span><span class="sxs-lookup"><span data-stu-id="3c6ab-163">Prepare data for scoring in Spark</span></span>
<span data-ttu-id="3c6ab-164">Deze sectie wordt beschreven hoe u tooindex, coderen en categorische functies tooprepare ze voor gebruik in MLlib onder supervisie learning-algoritmen voor classificatie en regressie schalen.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-164">This section shows how tooindex, encode, and scale categorical features tooprepare them for use in MLlib supervised learning algorithms for classification and regression.</span></span>

### <a name="feature-transformation-index-and-encode-categorical-features-for-input-into-models-for-scoring"></a><span data-ttu-id="3c6ab-165">Functie transformatie: te indexeren en coderen categorische functies voor invoer in modellen voor score berekenen</span><span class="sxs-lookup"><span data-stu-id="3c6ab-165">Feature transformation: index and encode categorical features for input into models for scoring</span></span>
<span data-ttu-id="3c6ab-166">Deze sectie wordt beschreven hoe tooindex categorische gegevens met een `StringIndexer` en het coderen van functies met `OneHotEncoder` invoer voor Hallo-modellen.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-166">This section shows how tooindex categorical data using a `StringIndexer` and encode features with `OneHotEncoder` input into hello models.</span></span>

<span data-ttu-id="3c6ab-167">Hallo [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) coderen van een kolom met tekenreeksen van labels tooa kolom van de label-indexen.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-167">hello [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) encodes a string column of labels tooa column of label indices.</span></span> <span data-ttu-id="3c6ab-168">Hallo-indexen zijn geordend op label frequenties.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-168">hello indices are ordered by label frequencies.</span></span> 

<span data-ttu-id="3c6ab-169">Hallo [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) een kolom van een label indexen tooa kolom van de binaire aanvalsvectoren, met maximaal één one-waarde wordt toegewezen.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-169">hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="3c6ab-170">Met deze codering kunt algoritmen die continue belangrijke functies, zoals logistic regression verwacht toobe toegepast toocategorical functies.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-170">This encoding allows algorithms that expect continuous valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

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

<span data-ttu-id="3c6ab-171">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="3c6ab-171">**OUTPUT:**</span></span>

<span data-ttu-id="3c6ab-172">Tijd tooexecute boven cel: 5,37 seconden</span><span class="sxs-lookup"><span data-stu-id="3c6ab-172">Time taken tooexecute above cell: 5.37 seconds</span></span>

### <a name="create-rdd-objects-with-feature-arrays-for-input-into-models"></a><span data-ttu-id="3c6ab-173">RDD objecten met de functie matrices voor invoer in modellen maken</span><span class="sxs-lookup"><span data-stu-id="3c6ab-173">Create RDD objects with feature arrays for input into models</span></span>
<span data-ttu-id="3c6ab-174">Deze sectie bevat de code die laat zien hoe tooindex categorische gegevens als een RDD object en deze een hot coderen zodat deze gebruikt tootrain en test MLlib logistic regression en modellen op basis van een structuur worden kan.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-174">This section contains code that shows how tooindex categorical text data as an RDD object and one-hot encode it so it can be used tootrain and test MLlib logistic regression and tree-based models.</span></span> <span data-ttu-id="3c6ab-175">Hallo geïndexeerde gegevens worden opgeslagen in [robuuste gedistribueerd gegevensset (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) objecten.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-175">hello indexed data is stored in [Resilient Distributed Dataset (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) objects.</span></span> <span data-ttu-id="3c6ab-176">Dit zijn eenvoudige abstractie Hallo in Spark.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-176">These are hello basic abstraction in Spark.</span></span> <span data-ttu-id="3c6ab-177">Een object RDD vertegenwoordigt een niet-wijzigbaar, gepartitioneerde verzameling van elementen die kunnen worden bediend op, in combinatie met Spark.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-177">An RDD object represents an immutable, partitioned collection of elements that can be operated on in parallel with Spark.</span></span>

<span data-ttu-id="3c6ab-178">Bevat ook code die laat zien hoe de gegevens met tooscale Hallo `StandardScalar` geleverd door MLlib voor gebruik in lineaire regressie met stochastische kleurovergang Daalgradiënt (SGD), een populaire algoritme voor het trainen van een breed scala aan machine learning-modellen.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-178">It also contains code that shows how tooscale data with hello `StandardScalar` provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of machine learning models.</span></span> <span data-ttu-id="3c6ab-179">Hallo [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) gebruikte tooscale Hallo functies toounit variantie is.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-179">hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) is used tooscale hello features toounit variance.</span></span> <span data-ttu-id="3c6ab-180">Functie schaal, ook wel bekend als gegevensnormalisatie, weet u zeker dat functies met veel betaald waarden zijn niet opgegeven overmatige afwegen in objective Hallo-functie.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-180">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> 

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

<span data-ttu-id="3c6ab-181">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="3c6ab-181">**OUTPUT:**</span></span>

<span data-ttu-id="3c6ab-182">Tijd tooexecute boven cel: 11.72 seconden</span><span class="sxs-lookup"><span data-stu-id="3c6ab-182">Time taken tooexecute above cell: 11.72 seconds</span></span>

## <a name="score-with-hello-logistic-regression-model-and-save-output-tooblob"></a><span data-ttu-id="3c6ab-183">Hello Logistic Regression-Model beoordelen en uitvoer tooblob opslaan</span><span class="sxs-lookup"><span data-stu-id="3c6ab-183">Score with hello Logistic Regression Model and save output tooblob</span></span>
<span data-ttu-id="3c6ab-184">Hallo-code in deze sectie ziet u hoe tooload een Logistic regressiemodel dat is opgeslagen in Azure blob-opslag en toopredict al dan niet een tip wordt betaald op reis taxi gebruiken, deze met standaard classificatie metrische gegevens te beoordelen en vervolgens opslaan en Hallo resultaten tooblob tekenen opslag.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-184">hello code in this section shows how tooload a Logistic Regression Model that has been saved in Azure blob storage and use it toopredict whether or not a tip is paid on a taxi trip, score it with standard classification metrics, and then save and plot hello results tooblob storage.</span></span> <span data-ttu-id="3c6ab-185">Hallo berekend resultaten worden opgeslagen in RDD objecten.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-185">hello scored results are stored in RDD objects.</span></span> 

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

<span data-ttu-id="3c6ab-186">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="3c6ab-186">**OUTPUT:**</span></span>

<span data-ttu-id="3c6ab-187">Tijd tooexecute boven cel: 19.22 seconden</span><span class="sxs-lookup"><span data-stu-id="3c6ab-187">Time taken tooexecute above cell: 19.22 seconds</span></span>

## <a name="score-a-linear-regression-model"></a><span data-ttu-id="3c6ab-188">Een lineair regressiemodel beoordelen</span><span class="sxs-lookup"><span data-stu-id="3c6ab-188">Score a Linear Regression Model</span></span>
<span data-ttu-id="3c6ab-189">We hebben gebruikt [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) tootrain een lineair regressiemodel met stochastische kleurovergang Daalgradiënt (SGD) voor optimalisatie toopredict Hallo hoeveelheid tip betaald.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-189">We used [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) tootrain a linear regression model using Stochastic Gradient Descent (SGD) for optimization toopredict hello amount of tip paid.</span></span> 

<span data-ttu-id="3c6ab-190">Hallo-code in deze sectie ziet u hoe tooload een lineair regressiemodel uit Azure blob storage, beoordelen geschaalde variabelen gebruiken en sla Hallo resultaten back toohello blob.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-190">hello code in this section shows how tooload a Linear Regression Model from Azure blob storage, score using scaled variables, and then save hello results back toohello blob.</span></span>

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


<span data-ttu-id="3c6ab-191">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="3c6ab-191">**OUTPUT:**</span></span>

<span data-ttu-id="3c6ab-192">Tijd tooexecute boven cel: 16.63 seconden</span><span class="sxs-lookup"><span data-stu-id="3c6ab-192">Time taken tooexecute above cell: 16.63 seconds</span></span>

## <a name="score-classification-and-regression-random-forest-models"></a><span data-ttu-id="3c6ab-193">Classificatie en regressie willekeurige Forest modellen beoordelen</span><span class="sxs-lookup"><span data-stu-id="3c6ab-193">Score classification and regression Random Forest Models</span></span>
<span data-ttu-id="3c6ab-194">Hallo-code in deze sectie toont hoe tooload Hallo classificatie opgeslagen en regressie willekeurige Forest modellen opgeslagen in Azure blob-opslag score van de prestaties met standaard classificatie en regressie metingen en sla Hallo resultaten back tooblob opslag.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-194">hello code in this section shows how tooload hello saved classification and regression Random Forest Models saved in Azure blob storage, score their performance with standard classifier and regression measures, and then save hello results back tooblob storage.</span></span>

<span data-ttu-id="3c6ab-195">[Willekeurige forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) ensembles van beslissingsstructuren zijn.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-195">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="3c6ab-196">Ze combineren veel decision trees tooreduce Hallo risico te.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-196">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="3c6ab-197">Willekeurige forests kunnen verwerken categorische functies toohello multiklassen classificatie instelling uitbreiden, hoeven niet functie schalen en kunnen toocapture niet-mogelijkheid tot zijn en interacties functies.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-197">Random forests can handle categorical features, extend toohello multiclass classification setting, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="3c6ab-198">Willekeurige forests zijn een van de meest succesvolle Hallo-machine learning-modellen voor de indeling en regressie.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-198">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>

<span data-ttu-id="3c6ab-199">[Spark.mllib](http://spark.apache.org/mllib/) willekeurige forests ondersteunt voor binaire en multiklassen classificatie en voor regressie, continue en categorische functies gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-199">[spark.mllib](http://spark.apache.org/mllib/) supports random forests for binary and multiclass classification and for regression, using both continuous and categorical features.</span></span> 

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

<span data-ttu-id="3c6ab-200">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="3c6ab-200">**OUTPUT:**</span></span>

<span data-ttu-id="3c6ab-201">Tijd tooexecute boven cel: 31.07 seconden</span><span class="sxs-lookup"><span data-stu-id="3c6ab-201">Time taken tooexecute above cell: 31.07 seconds</span></span>

## <a name="score-classification-and-regression-gradient-boosting-tree-models"></a><span data-ttu-id="3c6ab-202">Classificatie en regressie kleurovergang versterking structuur modellen beoordelen</span><span class="sxs-lookup"><span data-stu-id="3c6ab-202">Score classification and regression Gradient Boosting Tree Models</span></span>
<span data-ttu-id="3c6ab-203">Hallo-code in deze sectie ziet u hoe tooload classificatie en regressie kleurovergang versterking structuur modellen uit Azure blob-opslag score van de prestaties met standaard classificatie en regressie metingen en sla Hallo resultaten back tooblob opslag.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-203">hello code in this section shows how tooload classification and regression Gradient Boosting Tree Models from Azure blob storage, score their performance with standard classifier and regression measures, and then save hello results back tooblob storage.</span></span> 

<span data-ttu-id="3c6ab-204">**Spark.mllib** GBTs voor binaire classificatie en voor regressie, met behulp van de functies voor continue en categorische ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-204">**spark.mllib** supports GBTs for binary classification and for regression, using both continuous and categorical features.</span></span> 

<span data-ttu-id="3c6ab-205">[Kleurovergang versterking structuren](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) ensembles van beslissingsstructuren zijn.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-205">[Gradient Boosting Trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="3c6ab-206">GBTs train besluit structuren iteratief toominimize een verlies-functie.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-206">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="3c6ab-207">GBTs categorische functies kan verwerken, hoeven niet functie schalen en kunnen toocapture niet-mogelijkheid tot zijn en interacties functies.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-207">GBTs can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="3c6ab-208">Ze kunnen ook worden gebruikt in een setting multiklasse classificatie.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-208">They can also be used in a multiclass-classification setting.</span></span>

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

<span data-ttu-id="3c6ab-209">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="3c6ab-209">**OUTPUT:**</span></span>

<span data-ttu-id="3c6ab-210">Tijd tooexecute boven cel: 14.6 seconden</span><span class="sxs-lookup"><span data-stu-id="3c6ab-210">Time taken tooexecute above cell: 14.6 seconds</span></span>

## <a name="clean-up-objects-from-memory-and-print-scored-file-locations"></a><span data-ttu-id="3c6ab-211">Opschonen van objecten uit het geheugen en scored bestandslocaties afdrukken</span><span class="sxs-lookup"><span data-stu-id="3c6ab-211">Clean up objects from memory and print scored file locations</span></span>
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


<span data-ttu-id="3c6ab-212">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="3c6ab-212">**OUTPUT:**</span></span>

<span data-ttu-id="3c6ab-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span><span class="sxs-lookup"><span data-stu-id="3c6ab-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span></span>

<span data-ttu-id="3c6ab-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span><span class="sxs-lookup"><span data-stu-id="3c6ab-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span></span>

<span data-ttu-id="3c6ab-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span><span class="sxs-lookup"><span data-stu-id="3c6ab-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span></span>

<span data-ttu-id="3c6ab-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span><span class="sxs-lookup"><span data-stu-id="3c6ab-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span></span>

<span data-ttu-id="3c6ab-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span><span class="sxs-lookup"><span data-stu-id="3c6ab-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span></span>

<span data-ttu-id="3c6ab-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span><span class="sxs-lookup"><span data-stu-id="3c6ab-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span></span>

## <a name="consume-spark-models-through-a-web-interface"></a><span data-ttu-id="3c6ab-219">Spark modellen gebruiken via een webinterface</span><span class="sxs-lookup"><span data-stu-id="3c6ab-219">Consume Spark Models through a web interface</span></span>
<span data-ttu-id="3c6ab-220">Spark biedt een mechanisme tooremotely indienen batchtaken of interactieve query's via een REST-interface met een component Livy genoemd.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-220">Spark provides a mechanism tooremotely submit batch jobs or interactive queries through a REST interface with a component called Livy.</span></span> <span data-ttu-id="3c6ab-221">Livy is standaard ingeschakeld op uw HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-221">Livy is enabled by default on your HDInsight Spark cluster.</span></span> <span data-ttu-id="3c6ab-222">Zie voor meer informatie over Livy: [Spark verzenden van taken op afstand met behulp van Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="3c6ab-222">For more information on Livy, see: [Submit Spark jobs remotely using Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span></span> 

<span data-ttu-id="3c6ab-223">U kunt Livy tooremotely verzenden van een taak die door de batch scores een bestand dat is opgeslagen in een Azure-blob en hierna schrijft Hallo resultaten tooanother blob.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-223">You can use Livy tooremotely submit a job that batch scores a file that is stored in an Azure blob and then writes hello results tooanother blob.</span></span> <span data-ttu-id="3c6ab-224">toodo dit u Python-script op Hallo van uploaden</span><span class="sxs-lookup"><span data-stu-id="3c6ab-224">toodo this, you upload hello Python script from</span></span>  
<span data-ttu-id="3c6ab-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) toohello blob van Hallo Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) toohello blob of hello Spark cluster.</span></span> <span data-ttu-id="3c6ab-226">U kunt een hulpprogramma zoals **Microsoft Azure Storage Explorer** of **AzCopy** toocopy Hallo script toohello cluster blob.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-226">You can use a tool like **Microsoft Azure Storage Explorer** or **AzCopy** toocopy hello script toohello cluster blob.</span></span> <span data-ttu-id="3c6ab-227">In ons geval geüpload we Hallo script te***wasb:///example/python/ConsumeGBNYCReg.py***.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-227">In our case we uploaded hello script too***wasb:///example/python/ConsumeGBNYCReg.py***.</span></span>   

> [!NOTE]
> <span data-ttu-id="3c6ab-228">Hallo toegangstoetsen die u kunt u op Hallo-portal voor Hallo storage-account gekoppeld Hallo Spark-cluster vinden nodig.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-228">hello access keys that you need can be found on hello portal for hello storage account associated with hello Spark cluster.</span></span> 
> 
> 

<span data-ttu-id="3c6ab-229">Na het uploaden van toothis locatie dit script wordt uitgevoerd binnen een Spark-cluster Hallo in een gedistribueerde context.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-229">Once uploaded toothis location, this script runs within hello Spark cluster in a distributed context.</span></span> <span data-ttu-id="3c6ab-230">Hallo-model geladen en voorspellingen op op basis van model Hallo invoerbestanden wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-230">It loads hello model and runs predictions on input files based on hello model.</span></span>  

<span data-ttu-id="3c6ab-231">U kunt dit script extern aanroepen door een eenvoudige HTTPS/REST-aanvraag op Livy.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-231">You can invoke this script remotely by making a simple HTTPS/REST request on Livy.</span></span>  <span data-ttu-id="3c6ab-232">Hier volgt een curl-opdracht tooconstruct Hallo HTTP-aanvraag tooinvoke hello pythonscript op afstand.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-232">Here is a curl command tooconstruct hello HTTP request tooinvoke hello Python script remotely.</span></span> <span data-ttu-id="3c6ab-233">Vervangen door CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME Hallo juiste waarden voor uw Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-233">Replace CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME with hello appropriate values for your Spark cluster.</span></span>

    # CURL COMMAND tooINVOKE PYTHON SCRIPT WITH HTTP REQUEST

    curl -k --user "CLUSTERLOGIN:CLUSTERPASSWORD" -X POST --data "{\"file\": \"wasb:///example/python/ConsumeGBNYCReg.py\"}" -H "Content-Type: application/json" https://CLUSTERNAME.azurehdinsight.net/livy/batches

<span data-ttu-id="3c6ab-234">U kunt een andere taal op Hallo extern systeem tooinvoke Hallo Spark taak via Livy door het maken van een eenvoudige HTTPS-aanroep met basisverificatie.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-234">You can use any language on hello remote system tooinvoke hello Spark job through Livy by making a simple HTTPS call with Basic Authentication.</span></span>   

> [!NOTE]
> <span data-ttu-id="3c6ab-235">Het handige toouse Hallo Python aanvragen bibliotheek normaal zou zijn bij het maken van deze aanroep HTTP, maar dit momenteel niet standaard ingeschakeld in Azure Functions is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-235">It would be convenient toouse hello Python Requests library when making this HTTP call, but it is not currently installed by default in Azure Functions.</span></span> <span data-ttu-id="3c6ab-236">Zodat oudere HTTP-bibliotheken in plaats daarvan worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-236">So older HTTP libraries are used instead.</span></span>   
> 
> 

<span data-ttu-id="3c6ab-237">Dit is Hallo Python-code voor Hallo HTTP-aanroep:</span><span class="sxs-lookup"><span data-stu-id="3c6ab-237">Here is hello Python code for hello HTTP call:</span></span>

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


<span data-ttu-id="3c6ab-238">U kunt ook deze Python-code te toevoegen[Azure Functions](https://azure.microsoft.com/documentation/services/functions/) tootrigger de verzending van een Spark-taak die een blob scores op basis van verschillende gebeurtenissen, zoals een timer, maken of bijwerken van een blob.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-238">You can also add this Python code too[Azure Functions](https://azure.microsoft.com/documentation/services/functions/) tootrigger a Spark job submission that scores a blob based on various events like a timer, creation, or update of a blob.</span></span> 

<span data-ttu-id="3c6ab-239">Als u liever een code gratis Clientervaring, gebruik Hallo [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) tooinvoke Hallo Spark batchscoreberekening met het definiëren van een HTTP-actie op Hallo **Logic Apps Designer** en het instellen van de parameters.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-239">If you prefer a code free client experience, use hello [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) tooinvoke hello Spark batch scoring by defining an HTTP action on hello **Logic Apps Designer** and setting its parameters.</span></span> 

* <span data-ttu-id="3c6ab-240">Maken vanuit Azure-portal een nieuwe logische App door te selecteren **+ nieuw** -> **Web en mobiel** -> **logische App**.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-240">From Azure portal, create a new Logic App by selecting **+New** -> **Web + Mobile** -> **Logic App**.</span></span> 
* <span data-ttu-id="3c6ab-241">toobring up Hallo **Logic Apps Designer**, voer de naam Hallo Hallo logische App en de App Service-Plan.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-241">toobring up hello **Logic Apps Designer**, enter hello name of hello Logic App and App Service Plan.</span></span>
* <span data-ttu-id="3c6ab-242">Selecteer een HTTP-actie en Voer Hallo parameters die worden weergegeven in de volgende afbeelding Hallo:</span><span class="sxs-lookup"><span data-stu-id="3c6ab-242">Select an HTTP action and enter hello parameters shown in hello following figure:</span></span>

![Logic Apps Designer](./media/machine-learning-data-science-spark-model-consumption/spark-logica-app-client.png)

## <a name="whats-next"></a><span data-ttu-id="3c6ab-244">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3c6ab-244">What's next?</span></span>
<span data-ttu-id="3c6ab-245">**Kruisvalidatie en hyperparameter sweeping**: Zie [geavanceerde gegevensverkenning en modellering met Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) over de manier waarop modellen kunnen getraind met sweeping kruisvalidatie en hyper-parameter.</span><span class="sxs-lookup"><span data-stu-id="3c6ab-245">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping.</span></span>

