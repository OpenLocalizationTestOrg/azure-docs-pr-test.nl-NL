---
title: Voorbeeld van de machine learning met MLlib Spark in HDInsight - Azure | Microsoft Docs
description: Informatie over het Spark MLlib gebruiken voor het maken van een machine learning-app die een gegevensset met behulp van classificatie via logistic regression analyseert.
keywords: Spark machine learning spark machine learning-voorbeeld
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c0fd4baa-946d-4e03-ad2c-a03491bd90c8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: e563d4f51c9e27b20df47eca6d3eb00ac79e854f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="use-spark-mllib-to-build-a-machine-learning-application-and-analyze-a-dataset"></a><span data-ttu-id="63cc4-104">Spark MLlib gebruiken voor het bouwen van een machine learning-toepassing en analyseren van een gegevensset</span><span class="sxs-lookup"><span data-stu-id="63cc4-104">Use Spark MLlib to build a machine learning application and analyze a dataset</span></span>

<span data-ttu-id="63cc4-105">Informatie over het gebruik van Spark **MLlib** voor het maken van een machine learning-toepassing te doen eenvoudige predictive Analytics op een open gegevensset.</span><span class="sxs-lookup"><span data-stu-id="63cc4-105">Learn how to use Spark **MLlib** to create a machine learning application to do simple predictive analysis on an open dataset.</span></span> <span data-ttu-id="63cc4-106">Van Spark van ingebouwde machine learning-bibliotheken, in dit voorbeeld wordt *classificatie* via logistic regression.</span><span class="sxs-lookup"><span data-stu-id="63cc4-106">From Spark's built-in machine learning libraries, this example uses *classification* through logistic regression.</span></span> 

> [!TIP]
> <span data-ttu-id="63cc4-107">In dit voorbeeld is ook beschikbaar als een Jupyter-notebook op een cluster Spark (Linux) die u in HDInsight maakt.</span><span class="sxs-lookup"><span data-stu-id="63cc4-107">This example is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="63cc4-108">De ervaring voor de notebook kunt u de Python-codefragmenten uitvoeren vanaf de notebook zelf.</span><span class="sxs-lookup"><span data-stu-id="63cc4-108">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="63cc4-109">Wilt u de zelfstudie uit binnen een laptop, een Spark-cluster maken en starten van een Jupyter-notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span><span class="sxs-lookup"><span data-stu-id="63cc4-109">To follow the tutorial from within a notebook, create a Spark cluster and launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span></span> <span data-ttu-id="63cc4-110">Voer vervolgens de notebook **Spark Machine Learning - Predictive Analytics op voeding inspectie gegevens met behulp van MLlib.ipynb** onder de **Python** map.</span><span class="sxs-lookup"><span data-stu-id="63cc4-110">Then, run the notebook **Spark Machine Learning - Predictive analysis on food inspection data using MLlib.ipynb** under the **Python** folder.</span></span>
>
>

<span data-ttu-id="63cc4-111">MLlib is een core Spark-bibliotheek met veel nuttige hulpprogramma's voor machine learning taken, waaronder hulpprogramma's die geschikt zijn voor:</span><span class="sxs-lookup"><span data-stu-id="63cc4-111">MLlib is a core Spark library that provides many utilities useful for machine learning tasks, including utilities that are suitable for:</span></span>

* <span data-ttu-id="63cc4-112">Classificatie</span><span class="sxs-lookup"><span data-stu-id="63cc4-112">Classification</span></span>
* <span data-ttu-id="63cc4-113">Regressie</span><span class="sxs-lookup"><span data-stu-id="63cc4-113">Regression</span></span>
* <span data-ttu-id="63cc4-114">Clustering</span><span class="sxs-lookup"><span data-stu-id="63cc4-114">Clustering</span></span>
* <span data-ttu-id="63cc4-115">Onderwerp-model</span><span class="sxs-lookup"><span data-stu-id="63cc4-115">Topic modeling</span></span>
* <span data-ttu-id="63cc4-116">Enkelvoudige waarde afbreken (SVD) en analyse van de principal-onderdeel (Pso)</span><span class="sxs-lookup"><span data-stu-id="63cc4-116">Singular value decomposition (SVD) and principal component analysis (PCA)</span></span>
* <span data-ttu-id="63cc4-117">Hypothese testen en het berekenen van de voorbeeld-statistieken</span><span class="sxs-lookup"><span data-stu-id="63cc4-117">Hypothesis testing and calculating sample statistics</span></span>

## <a name="what-are-classification-and-logistic-regression"></a><span data-ttu-id="63cc4-118">Wat zijn de classificatie en logistic regression?</span><span class="sxs-lookup"><span data-stu-id="63cc4-118">What are classification and logistic regression?</span></span>
<span data-ttu-id="63cc4-119">*Classificatie*, een populaire machine learning-taak is het proces voor het sorteren van invoergegevens in categorieën.</span><span class="sxs-lookup"><span data-stu-id="63cc4-119">*Classification*, a popular machine learning task, is the process of sorting input data into categories.</span></span> <span data-ttu-id="63cc4-120">Het is de taak van een classificatie-algoritme om te achterhalen toewijzen 'labels' voor het invoeren van gegevens die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="63cc4-120">It is the job of a classification algorithm to figure out how to assign "labels" to input data that you provide.</span></span> <span data-ttu-id="63cc4-121">Bijvoorbeeld, u een machine learning-algoritme dat vooraf gedefinieerde gegevens als invoer accepteert en wordt de stock verdeeld in twee categorieën kan zien: bestanden die u moet verkoopt en bestanden die u dient te houden.</span><span class="sxs-lookup"><span data-stu-id="63cc4-121">For example, you could think of a machine learning algorithm that accepts stock information as input and divides the stock into two categories: stocks that you should sell and stocks that you should keep.</span></span>

<span data-ttu-id="63cc4-122">Logistic regression is de algoritme die u voor classificatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="63cc4-122">Logistic regression is the algorithm that you use for classification.</span></span> <span data-ttu-id="63cc4-123">De Spark logistic regression API is nuttig voor *binaire classificatie*, of de ingevoerde gegevens classificeren in een van twee groepen.</span><span class="sxs-lookup"><span data-stu-id="63cc4-123">Spark's logistic regression API is useful for *binary classification*, or classifying input data into one of two groups.</span></span> <span data-ttu-id="63cc4-124">Zie voor meer informatie over logistic regressies [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span><span class="sxs-lookup"><span data-stu-id="63cc4-124">For more information about logistic regressions, see [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span></span>

<span data-ttu-id="63cc4-125">Kortom, het proces van het logistic regression produceert een *logistic functie* kunnen worden gebruikt voor het voorspellen van de kans dat een invoer-vector in één groep of de andere behoort.</span><span class="sxs-lookup"><span data-stu-id="63cc4-125">In summary, the process of logistic regression produces a *logistic function* that can be used to predict the probability that an input vector belongs in one group or the other.</span></span>  

## <a name="predictive-analysis-example-on-food-inspection-data"></a><span data-ttu-id="63cc4-126">Predictive Analytics-voorbeeld op voeding inspectie gegevens</span><span class="sxs-lookup"><span data-stu-id="63cc4-126">Predictive analysis example on food inspection data</span></span>
<span data-ttu-id="63cc4-127">In dit voorbeeld gebruikt u Spark sommige voorspellende analyses uitvoeren op voeding inspectie gegevens (**Food_Inspections1.csv**) die is verkregen via de [Den Haag gegevensportal](https://data.cityofchicago.org/).</span><span class="sxs-lookup"><span data-stu-id="63cc4-127">In this example, you use Spark to perform some predictive analysis on food inspection data (**Food_Inspections1.csv**) that was acquired through the [City of Chicago data portal](https://data.cityofchicago.org/).</span></span> <span data-ttu-id="63cc4-128">Deze gegevensset bevat informatie over voeding inrichting controles zijn uitgevoerd in Chicago, inclusief informatie over elke inrichting, de schendingen gevonden (indien aanwezig) en de resultaten van de controle.</span><span class="sxs-lookup"><span data-stu-id="63cc4-128">This dataset contains information about food establishment inspections that were conducted in Chicago, including information about each establishment, the violations found (if any), and the results of the inspection.</span></span> <span data-ttu-id="63cc4-129">Het CSV-bestand is al beschikbaar in het opslagaccount dat is gekoppeld aan het cluster **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="63cc4-129">The CSV data file is already available in the storage account associated with the cluster at **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span></span>

<span data-ttu-id="63cc4-130">In de onderstaande stappen kunt u een model om te zien wat er nodig is om te geven of mislukken van een voeding inspectie ontwikkelen.</span><span class="sxs-lookup"><span data-stu-id="63cc4-130">In the steps below, you develop a model to see what it takes to pass or fail a food inspection.</span></span>

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a><span data-ttu-id="63cc4-131">Beginnen met het samenstellen van een Spark-MMLib machine learning-app</span><span class="sxs-lookup"><span data-stu-id="63cc4-131">Start building a Spark MMLib machine learning app</span></span>
1. <span data-ttu-id="63cc4-132">Klik vanaf het Startboard in [Azure Portal](https://portal.azure.com/) op de tegel voor uw Spark-cluster (als u deze aan het Startboard hebt vastgemaakt).</span><span class="sxs-lookup"><span data-stu-id="63cc4-132">From the [Azure portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="63cc4-133">U kunt ook naar uw cluster navigeren onder **Bladeren** > **HDInsight-clusters**.</span><span class="sxs-lookup"><span data-stu-id="63cc4-133">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
1. <span data-ttu-id="63cc4-134">Klik vanuit de blade Spark-cluster op **Cluster-dashboard** en vervolgens op **Jupyter Notebook**.</span><span class="sxs-lookup"><span data-stu-id="63cc4-134">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="63cc4-135">Voer de beheerdersreferenties voor het cluster in als u daarom wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="63cc4-135">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="63cc4-136">Mogelijk bereikt u de Jupyter-notebook voor uw cluster ook door de volgende URL in uw browser te openen.</span><span class="sxs-lookup"><span data-stu-id="63cc4-136">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="63cc4-137">Vervang **CLUSTERNAME** door de naam van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="63cc4-137">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. <span data-ttu-id="63cc4-138">Maak een notebook.</span><span class="sxs-lookup"><span data-stu-id="63cc4-138">Create a notebook.</span></span> <span data-ttu-id="63cc4-139">Klik op **Nieuw** en klik vervolgens op **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="63cc4-139">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="63cc4-140">![Maken van een Jupyter-notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "een nieuwe Jupyter-notebook maken")</span><span class="sxs-lookup"><span data-stu-id="63cc4-140">![Create a Jupyter notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Create a new Jupyter notebook")</span></span>
1. <span data-ttu-id="63cc4-141">Er wordt een nieuwe notebook gemaakt en geopend met de naam Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="63cc4-141">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="63cc4-142">Klik bovenaan op de naam van de notebook en wijzig deze in een beschrijvende naam.</span><span class="sxs-lookup"><span data-stu-id="63cc4-142">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="63cc4-143">![Een naam opgeven voor de notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Een naam opgeven voor de notebook")</span><span class="sxs-lookup"><span data-stu-id="63cc4-143">![Provide a name for the notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Provide a name for the notebook")</span></span>
1. <span data-ttu-id="63cc4-144">Omdat u de notebook met behulp van de PySpark-kernel hebt gemaakt, hoeft u niet expliciet contexten te maken.</span><span class="sxs-lookup"><span data-stu-id="63cc4-144">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="63cc4-145">De Spark- en Hive-contexten worden automatisch voor u gemaakt wanneer u de eerste codecel uitvoert.</span><span class="sxs-lookup"><span data-stu-id="63cc4-145">The Spark and Hive contexts are automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="63cc4-146">U kunt beginnen met het bouwen van uw machine learning-toepassingen door het importeren van de typen die nodig zijn voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="63cc4-146">You can start building your machine learning application by importing the types required for this scenario.</span></span> <span data-ttu-id="63cc4-147">Om dit te doen, plaatst u de cursor in de cel en druk op **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="63cc4-147">To do so, place the cursor in the cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a><span data-ttu-id="63cc4-148">Maken van een invoer dataframe</span><span class="sxs-lookup"><span data-stu-id="63cc4-148">Construct an input dataframe</span></span>
<span data-ttu-id="63cc4-149">We kunnen gebruiken `sqlContext` transformaties uitvoeren op gestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="63cc4-149">We can use `sqlContext` to perform transformations on structured data.</span></span> <span data-ttu-id="63cc4-150">De eerste taak is de voorbeeldgegevens laden ((**Food_Inspections1.csv**)) in een Spark SQL *dataframe*.</span><span class="sxs-lookup"><span data-stu-id="63cc4-150">The first task is to load the sample data ((**Food_Inspections1.csv**)) into a Spark SQL *dataframe*.</span></span>

1. <span data-ttu-id="63cc4-151">Omdat de onbewerkte gegevens zich in een CSV-indeling, moeten we de Spark-context gebruiken voor het ophalen van elke regel van het bestand in het geheugen als niet-gestructureerde tekst; vervolgens gebruikt u de CSV-bibliotheek van Python elke regel afzonderlijk parseren.</span><span class="sxs-lookup"><span data-stu-id="63cc4-151">Because the raw data is in a CSV format, we need to use the Spark context to pull every line of the file into memory as unstructured text; then, you use Python's CSV library to parse each line individually.</span></span>

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. <span data-ttu-id="63cc4-152">We nu hebben het CSV-bestand als een RDD.</span><span class="sxs-lookup"><span data-stu-id="63cc4-152">We now have the CSV file as an RDD.</span></span>  <span data-ttu-id="63cc4-153">Om het schema van de gegevens te begrijpen, ophalen we één rij uit de RDD.</span><span class="sxs-lookup"><span data-stu-id="63cc4-153">To understand the schema of the data, we retrieve one row from the RDD.</span></span>

        inspections.take(1)

    <span data-ttu-id="63cc4-154">Als het goed is, wordt ongeveer de volgende uitvoer weergegeven:</span><span class="sxs-lookup"><span data-stu-id="63cc4-154">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [['413707',
          'LUNA PARK INC',
          'LUNA PARK  DAY CARE',
          '2049789',
          "Children's Services Facility",
          'Risk 1 (High)',
          '3250 W FOSTER AVE ',
          'CHICAGO',
          'IL',
          '60625',
          '09/21/2010',
          'License-Task Force',
          'Fail',
          '24. DISH WASHING FACILITIES: PROPERLY DESIGNED, CONSTRUCTED, MAINTAINED, INSTALLED, LOCATED AND OPERATED - Comments: All dishwashing machines must be of a type that complies with all requirements of the plumbing section of the Municipal Code of Chicago and Rules and Regulation of the Board of Health. OBSEVERD THE 3 COMPARTMENT SINK BACKING UP INTO THE 1ST AND 2ND COMPARTMENT WITH CLEAR WATER AND SLOWLY DRAINING OUT. INST NEED HAVE IT REPAIR. CITATION ISSUED, SERIOUS VIOLATION 7-38-030 H000062369-10 COURT DATE 10-28-10 TIME 1 P.M. ROOM 107 400 W. SURPERIOR. | 36. LIGHTING: REQUIRED MINIMUM FOOT-CANDLES OF LIGHT PROVIDED, FIXTURES SHIELDED - Comments: Shielding to protect against broken glass falling into food shall be provided for all artificial lighting sources in preparation, service, and display facilities. LIGHT SHIELD ARE MISSING UNDER HOOD OF  COOKING EQUIPMENT AND NEED TO REPLACE LIGHT UNDER UNIT. 4 LIGHTS ARE OUT IN THE REAR CHILDREN AREA,IN THE KINDERGARDEN CLASS ROOM. 2 LIGHT ARE OUT EAST REAR, LIGHT FRONT WEST ROOM. NEED TO REPLACE ALL LIGHT THAT ARE NOT WORKING. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: The walls and ceilings shall be in good repair and easily cleaned. MISSING CEILING TILES WITH STAINS IN WEST,EAST, IN FRONT AREA WEST, AND BY THE 15MOS AREA. NEED TO BE REPLACED. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair. SPLASH GUARDED ARE NEEDED BY THE EXPOSED HAND SINK IN THE KITCHEN AREA | 34. FLOORS: CONSTRUCTED PER CODE, CLEANED, GOOD REPAIR, COVING INSTALLED, DUST-LESS CLEANING METHODS USED - Comments: The floors shall be constructed per code, be smooth and easily cleaned, and be kept clean and in good repair. INST NEED TO ELEVATE ALL FOOD ITEMS 6INCH OFF THE FLOOR 6 INCH AWAY FORM WALL.  ',
          '41.97583445690982',
          '-87.7107455232781',
          '(41.97583445690982, -87.7107455232781)']]
1. <span data-ttu-id="63cc4-155">De voorgaande uitvoer geeft ons een idee van het schema van het invoerbestand.</span><span class="sxs-lookup"><span data-stu-id="63cc4-155">The preceding output gives us an idea of the schema of the input file.</span></span> <span data-ttu-id="63cc4-156">Het bevat de naam van elke instelling, het type van de inrichting, het adres, de gegevens van de controles en de locatie, onder andere.</span><span class="sxs-lookup"><span data-stu-id="63cc4-156">It includes the name of every establishment, the type of establishment, the address, the data of the inspections, and the location, among other things.</span></span> <span data-ttu-id="63cc4-157">Laten we enkele kolommen selecteren die zijn handig voor onze predictive Analytics en de resultaten groeperen als een dataframe dat we vervolgens gebruiken om een tijdelijke tabel te maken.</span><span class="sxs-lookup"><span data-stu-id="63cc4-157">Let's select a few columns that are useful for our predictive analysis and group the results as a dataframe, which we then use to create a temporary table.</span></span>

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. <span data-ttu-id="63cc4-158">Nu een *dataframe*, `df` waarop we onze analyse kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="63cc4-158">We now have a *dataframe*, `df` on which we can perform our analysis.</span></span> <span data-ttu-id="63cc4-159">We hebben ook een aanroep van de tijdelijke tabel **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="63cc4-159">We also have a temporary table call **CountResults**.</span></span> <span data-ttu-id="63cc4-160">Vindt u vier kolommen in de dataframe van belang: **id**, **naam**, **resultaten**, en **schendingen**.</span><span class="sxs-lookup"><span data-stu-id="63cc4-160">We've included four columns of interest in the dataframe: **id**, **name**, **results**, and **violations**.</span></span>

    <span data-ttu-id="63cc4-161">We gaan een kort voorbeeld van de gegevens ophalen:</span><span class="sxs-lookup"><span data-stu-id="63cc4-161">Let's get a small sample of the data:</span></span>

        df.show(5)

    <span data-ttu-id="63cc4-162">Als het goed is, wordt ongeveer de volgende uitvoer weergegeven:</span><span class="sxs-lookup"><span data-stu-id="63cc4-162">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +------+--------------------+-------+--------------------+
        |    id|                name|results|          violations|
        +------+--------------------+-------+--------------------+
        |413707|       LUNA PARK INC|   Fail|24. DISH WASHING ...|
        |391234|       CAFE SELMARIE|   Fail|2. FACILITIES TO ...|
        |413751|          MANCHU WOK|   Pass|33. FOOD AND NON-...|
        |413708|BENCHMARK HOSPITA...|   Pass|                    |
        |413722|           JJ BURGER|   Pass|                    |
        +------+--------------------+-------+--------------------+

## <a name="understand-the-data"></a><span data-ttu-id="63cc4-163">De gegevens begrijpen</span><span class="sxs-lookup"><span data-stu-id="63cc4-163">Understand the data</span></span>
1. <span data-ttu-id="63cc4-164">Laten we beginnen met een idee van wat onze gegevensset bevat.</span><span class="sxs-lookup"><span data-stu-id="63cc4-164">Let's start to get a sense of what our dataset contains.</span></span> <span data-ttu-id="63cc4-165">Bijvoorbeeld, wat zijn de verschillende waarden in de **resultaten** kolom?</span><span class="sxs-lookup"><span data-stu-id="63cc4-165">For example, what are the different values in the **results** column?</span></span>

        df.select('results').distinct().show()

    <span data-ttu-id="63cc4-166">Als het goed is, wordt ongeveer de volgende uitvoer weergegeven:</span><span class="sxs-lookup"><span data-stu-id="63cc4-166">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +--------------------+
        |             results|
        +--------------------+
        |                Fail|
        |Business Not Located|
        |                Pass|
        |  Pass w/ Conditions|
        |     Out of Business|
        +--------------------+
1. <span data-ttu-id="63cc4-167">Een snelle visualisatie kan we beter reden over de distributie van deze resultaten.</span><span class="sxs-lookup"><span data-stu-id="63cc4-167">A quick visualization can help us reason about the distribution of these outcomes.</span></span> <span data-ttu-id="63cc4-168">We hebben al de gegevens in een tijdelijke tabel **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="63cc4-168">We already have the data in a temporary table **CountResults**.</span></span> <span data-ttu-id="63cc4-169">U kunt de volgende SQL-query uitvoeren op de tabel voor een beter inzicht te krijgen van hoe de resultaten worden gedistribueerd.</span><span class="sxs-lookup"><span data-stu-id="63cc4-169">You can run the following SQL query against the table to get a better understanding of how the results are distributed.</span></span>

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    <span data-ttu-id="63cc4-170">De `%%sql` magic gevolgd door `-o countResultsdf` zorgt ervoor dat de uitvoer van de query lokaal worden bewaard op de Jupyter-server (meestal de headnode van het cluster).</span><span class="sxs-lookup"><span data-stu-id="63cc4-170">The `%%sql` magic followed by `-o countResultsdf` ensures that the output of the query is persisted locally on the Jupyter server (typically the headnode of the cluster).</span></span> <span data-ttu-id="63cc4-171">De uitvoer is doorgevoerd als een [Pandas](http://pandas.pydata.org/) dataframe met de opgegeven naam **countResultsdf**.</span><span class="sxs-lookup"><span data-stu-id="63cc4-171">The output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with the specified name **countResultsdf**.</span></span>

    <span data-ttu-id="63cc4-172">Als het goed is, wordt ongeveer de volgende uitvoer weergegeven:</span><span class="sxs-lookup"><span data-stu-id="63cc4-172">You should see an output like the following:</span></span>

    <span data-ttu-id="63cc4-173">![Uitvoer van de SQL-query](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "uitvoer van de SQL-query")</span><span class="sxs-lookup"><span data-stu-id="63cc4-173">![SQL query output](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "SQL query output")</span></span>

    <span data-ttu-id="63cc4-174">Voor meer informatie over de `%%sql`-magic, en andere magics die voor de PySpark-kernel beschikbaar zijn, raadpleegt u [Beschikbare kernels op Jupyter-notebooks met HDInsight Spark-clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="63cc4-174">For more information about the `%%sql` magic, and other magics available with the PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
1. <span data-ttu-id="63cc4-175">U kunt ook Matplotlib, een bibliotheek gebruikt voor het opstellen van visualisatie van gegevens, tekent maken.</span><span class="sxs-lookup"><span data-stu-id="63cc4-175">You can also use Matplotlib, a library used to construct visualization of data, to create a plot.</span></span> <span data-ttu-id="63cc4-176">Omdat de grafiek moet worden gemaakt van de lokaal persistente **countResultsdf** dataframe, het codefragment moet beginnen met de `%%local` verwerkt Magic-pakket.</span><span class="sxs-lookup"><span data-stu-id="63cc4-176">Because the plot must be created from the locally persisted **countResultsdf** dataframe, the code snippet must begin with the `%%local` magic.</span></span> <span data-ttu-id="63cc4-177">Dit zorgt ervoor dat de code op de Jupyter-server lokaal wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="63cc4-177">This ensures that the code is run locally on the Jupyter server.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="63cc4-178">Als het goed is, wordt ongeveer de volgende uitvoer weergegeven:</span><span class="sxs-lookup"><span data-stu-id="63cc4-178">You should see an output like the following:</span></span>

    <span data-ttu-id="63cc4-179">![Spark machine learning-toepassing output - cirkeldiagram met vijf verschillende controleresultaten](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark machine learning-resultaat-uitvoer")</span><span class="sxs-lookup"><span data-stu-id="63cc4-179">![Spark machine learning application output - pie chart with five distinct inspection results](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark machine learning result output")</span></span>
1. <span data-ttu-id="63cc4-180">U kunt zien dat er 5 verschillende resultaten, waarvoor een inspectie kan zijn:</span><span class="sxs-lookup"><span data-stu-id="63cc4-180">You can see that there are 5 distinct results that an inspection can have:</span></span>

   * <span data-ttu-id="63cc4-181">Bedrijven niet vinden</span><span class="sxs-lookup"><span data-stu-id="63cc4-181">Business not located</span></span>
   * <span data-ttu-id="63cc4-182">Mislukt</span><span class="sxs-lookup"><span data-stu-id="63cc4-182">Fail</span></span>
   * <span data-ttu-id="63cc4-183">Doorgeven</span><span class="sxs-lookup"><span data-stu-id="63cc4-183">Pass</span></span>
   * <span data-ttu-id="63cc4-184">PSS met voorwaarden</span><span class="sxs-lookup"><span data-stu-id="63cc4-184">Pss w/ conditions</span></span>
   * <span data-ttu-id="63cc4-185">Buiten bedrijf</span><span class="sxs-lookup"><span data-stu-id="63cc4-185">Out of Business</span></span>

     <span data-ttu-id="63cc4-186">Laat het ons ontwikkel een model waarmee de uitkomst van een inspectie voeding kan raden schendingen van het gegeven.</span><span class="sxs-lookup"><span data-stu-id="63cc4-186">Let us develop a model that can guess the outcome of a food inspection, given the violations.</span></span> <span data-ttu-id="63cc4-187">Aangezien logistic regression een classificatiemethode binaire is, is het verstandig om onze gegevens in twee categorieën: **mislukken** en **doorgeven**.</span><span class="sxs-lookup"><span data-stu-id="63cc4-187">Since logistic regression is a binary classification method, it makes sense to group our data into two categories: **Fail** and **Pass**.</span></span> <span data-ttu-id="63cc4-188">Een 'doorgeven met voorwaarden' nog steeds een op te geven, zodat wanneer we het model trainen, we beide resultaten als gelijkwaardig beschouwt.</span><span class="sxs-lookup"><span data-stu-id="63cc4-188">A "Pass w/ Conditions" is still a Pass, so when we train the model, we consider the two results equivalent.</span></span> <span data-ttu-id="63cc4-189">Gegevens met de andere resultaten ('Bedrijven niet vinden' of 'Out of Business') zijn niet handig zodat we uit onze trainingset verwijderen.</span><span class="sxs-lookup"><span data-stu-id="63cc4-189">Data with the other results ("Business Not Located" or "Out of Business") are not useful so we remove them from our training set.</span></span> <span data-ttu-id="63cc4-190">Dit mag geen probleem omdat deze twee categorieën gezamenlijk een kleine hoeveelheid van de resultaten toch.</span><span class="sxs-lookup"><span data-stu-id="63cc4-190">This should be okay since these two categories make up a very small percentage of the results anyway.</span></span>
1. <span data-ttu-id="63cc4-191">Laat het ons opwekken en onze bestaande dataframe converteren (`df`) in een nieuwe dataframe waar elke inspectie wordt weergegeven als een combinatie van schendingen van het label.</span><span class="sxs-lookup"><span data-stu-id="63cc4-191">Let us go ahead and convert our existing dataframe(`df`) into a new dataframe where each inspection is represented as a label-violations pair.</span></span> <span data-ttu-id="63cc4-192">In ons geval een label van `0.0` vertegenwoordigt een fout optreedt, wordt een label van `1.0` vertegenwoordigt een is voltooid en een label van `-1.0` bepaalde resultaten naast deze twee vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="63cc4-192">In our case, a label of `0.0` represents a failure, a label of `1.0` represents a success, and a label of `-1.0` represents some results besides those two.</span></span> <span data-ttu-id="63cc4-193">We uitfilteren die andere resultaten bij het berekenen van de nieuwe gegevensframe.</span><span class="sxs-lookup"><span data-stu-id="63cc4-193">We filter those other results out when computing the new data frame.</span></span>

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    <span data-ttu-id="63cc4-194">Als u wilt zien welke lijkt gelabelde gegevens erop, gaan we u één rij ophalen.</span><span class="sxs-lookup"><span data-stu-id="63cc4-194">To see what the labeled data looks like, let's retrieve one row.</span></span>

        labeledData.take(1)

    <span data-ttu-id="63cc4-195">Als het goed is, wordt ongeveer de volgende uitvoer weergegeven:</span><span class="sxs-lookup"><span data-stu-id="63cc4-195">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of the food establishment and all parts of the property used in connection with the operation of the establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: The walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF THE FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: The flow of air discharged from kitchen fans shall always be through a duct to a point above the roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT TO DINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT TO OFFICE.")]

## <a name="create-a-logistic-regression-model-from-the-input-dataframe"></a><span data-ttu-id="63cc4-196">Een logistic regressiemodel maken van de invoer dataframe</span><span class="sxs-lookup"><span data-stu-id="63cc4-196">Create a logistic regression model from the input dataframe</span></span>
<span data-ttu-id="63cc4-197">De laatste taak is de gelabelde gegevens te converteren naar een indeling die kan worden geanalyseerd door logistic regression.</span><span class="sxs-lookup"><span data-stu-id="63cc4-197">Our final task is to convert the labeled data into a format that can be analyzed by logistic regression.</span></span> <span data-ttu-id="63cc4-198">De invoer voor een logistic regression-algoritme moet een reeks *label-functie vector paren*, waarbij 'functie vector' een vector van getallen die de invoer punt.</span><span class="sxs-lookup"><span data-stu-id="63cc4-198">The input to a logistic regression algorithm should be a set of *label-feature vector pairs*, where the "feature vector" is a vector of numbers representing the input point.</span></span> <span data-ttu-id="63cc4-199">Dus moeten we de kolom 'schendingen', die wordt semi-gestructureerde en bevat veel opmerkingen in vrije tekst, naar een matrix van real-getallen die met een machine gemakkelijk kan begrijpen converteren.</span><span class="sxs-lookup"><span data-stu-id="63cc4-199">So, we need to convert the "violations" column, which is semi-structured and contains many comments in free-text, to an array of real numbers that a machine could easily understand.</span></span>

<span data-ttu-id="63cc4-200">Een standaard machine learning-benadering voor het verwerken van natuurlijke taal is een 'index' van elk woord distinct toewijzen en vervolgens een vector doorgeven aan de machine learning-algoritme dat de waarde voor elke index de relatieve frequentie van dat woord in de tekenreeks bevat.</span><span class="sxs-lookup"><span data-stu-id="63cc4-200">One standard machine learning approach for processing natural language is to assign each distinct word an "index", and then pass a vector to the machine learning algorithm such that each index's value contains the relative frequency of that word in the text string.</span></span>

<span data-ttu-id="63cc4-201">MLlib biedt een eenvoudige manier om deze bewerking niet uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="63cc4-201">MLlib provides an easy way to perform this operation.</span></span> <span data-ttu-id="63cc4-202">Eerst 'basisvormen' elke tekenreeks schendingen om op te halen van de afzonderlijke woorden in elke tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="63cc4-202">First, "tokenize" each violations string to get the individual words in each string.</span></span> <span data-ttu-id="63cc4-203">Vervolgens gebruikt u een `HashingTF` elke set van tokens omzetten in een functie-vector die vervolgens kan worden doorgegeven aan de logistic regression-algoritme om te maken van een model.</span><span class="sxs-lookup"><span data-stu-id="63cc4-203">Then, use a `HashingTF` to convert each set of tokens into a feature vector that can then be passed to the logistic regression algorithm to construct a model.</span></span> <span data-ttu-id="63cc4-204">We uitvoeren alle deze stappen in de reeks met behulp van een "pipeline".</span><span class="sxs-lookup"><span data-stu-id="63cc4-204">We conduct all of these steps in sequence using a "pipeline".</span></span>

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-the-model-on-a-separate-test-dataset"></a><span data-ttu-id="63cc4-205">Evalueren van het model op een afzonderlijke testgegevensset</span><span class="sxs-lookup"><span data-stu-id="63cc4-205">Evaluate the model on a separate test dataset</span></span>
<span data-ttu-id="63cc4-206">Gebruiken we het model dat we eerder tot gemaakt *voorspellen* wat de resultaten van nieuwe controles worden, op basis van de schendingen die zijn waargenomen.</span><span class="sxs-lookup"><span data-stu-id="63cc4-206">We can use the model we created earlier to *predict* what the results of new inspections will be, based on the violations that were observed.</span></span> <span data-ttu-id="63cc4-207">We dit model op de gegevensset getraind **Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="63cc4-207">We trained this model on the dataset **Food_Inspections1.csv**.</span></span> <span data-ttu-id="63cc4-208">Laat het ons gebruik van een tweede gegevensset **Food_Inspections2.csv**, naar *evalueren* de sterkte van dit model op nieuwe gegevens.</span><span class="sxs-lookup"><span data-stu-id="63cc4-208">Let us use a second dataset, **Food_Inspections2.csv**, to *evaluate* the strength of this model on new data.</span></span> <span data-ttu-id="63cc4-209">Deze tweede gegevensverzameling (**Food_Inspections2.csv**) moet al zijn in de standaard storage-container die is gekoppeld aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="63cc4-209">This second data set (**Food_Inspections2.csv**) should already be in the default storage container associated with the cluster.</span></span>

1. <span data-ttu-id="63cc4-210">Het volgende codefragment maakt u een nieuwe dataframe **predictionsDf** die de voorspelling gegenereerd door het model bevat.</span><span class="sxs-lookup"><span data-stu-id="63cc4-210">The following snippet creates a new dataframe, **predictionsDf** that contains the prediction generated by the model.</span></span> <span data-ttu-id="63cc4-211">Het codefragment maakt ook een tijdelijke tabel genaamd **voorspellingen** op basis van de dataframe.</span><span class="sxs-lookup"><span data-stu-id="63cc4-211">The snippet also creates a temporary table called **Predictions** based on the dataframe.</span></span>

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    <span data-ttu-id="63cc4-212">Als het goed is, wordt ongeveer de volgende uitvoer weergegeven:</span><span class="sxs-lookup"><span data-stu-id="63cc4-212">You should see an output like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        ['id',
         'name',
         'results',
         'violations',
         'words',
         'features',
         'rawPrediction',
         'probability',
         'prediction']
1. <span data-ttu-id="63cc4-213">Bekijk een van de voorspellingen.</span><span class="sxs-lookup"><span data-stu-id="63cc4-213">Look at one of the predictions.</span></span> <span data-ttu-id="63cc4-214">In dit fragment uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="63cc4-214">Run this snippet:</span></span>

        predictionsDf.take(1)

   <span data-ttu-id="63cc4-215">Er is een voorspelling voor het eerste item in de testgegevensset.</span><span class="sxs-lookup"><span data-stu-id="63cc4-215">There is a prediction for the first entry in the test data set.</span></span>
1. <span data-ttu-id="63cc4-216">De `model.transform()` methode past de dezelfde transformatie uit op nieuwe gegevens die met hetzelfde schema en een voorspelling van het classificeren van de gegevens aankomen.</span><span class="sxs-lookup"><span data-stu-id="63cc4-216">The `model.transform()` method applies the same transformation to any new data with the same schema, and arrive at a prediction of how to classify the data.</span></span> <span data-ttu-id="63cc4-217">We kunt enkele eenvoudige statistieken om een beeld van hoe nauwkeurig zijn van onze voorspellingen doen:</span><span class="sxs-lookup"><span data-stu-id="63cc4-217">We can do some simple statistics to get a sense of how accurate our predictions were:</span></span>

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    <span data-ttu-id="63cc4-218">De uitvoer ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="63cc4-218">The output looks like the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    <span data-ttu-id="63cc4-219">Met behulp van logistic regression met Spark biedt ons een nauwkeurige model van de relatie tussen schendingen beschrijvingen in het Engels en een opgegeven bedrijf zou doorgeven of afbreken van een voeding inspectie.</span><span class="sxs-lookup"><span data-stu-id="63cc4-219">Using logistic regression with Spark gives us an accurate model of the relationship between violations descriptions in English and whether a given business would pass or fail a food inspection.</span></span>

## <a name="create-a-visual-representation-of-the-prediction"></a><span data-ttu-id="63cc4-220">Een visuele representatie van de voorspelling te maken</span><span class="sxs-lookup"><span data-stu-id="63cc4-220">Create a visual representation of the prediction</span></span>
<span data-ttu-id="63cc4-221">We kunnen een definitieve visualisatie om ons te helpen nu reden over de resultaten van deze test maken.</span><span class="sxs-lookup"><span data-stu-id="63cc4-221">We can now construct a final visualization to help us reason about the results of this test.</span></span>

1. <span data-ttu-id="63cc4-222">Begin met het uitpakken van de verschillende voorspellingen en de resultaten van de **voorspellingen** tijdelijke tabel die eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="63cc4-222">We start by extracting the different predictions and results from the **Predictions** temporary table created earlier.</span></span> <span data-ttu-id="63cc4-223">De volgende query's scheiden de uitvoer als *true_positive*, *false_positive*, *true_negative*, en *false_negative*.</span><span class="sxs-lookup"><span data-stu-id="63cc4-223">The following queries separate the output as *true_positive*, *false_positive*, *true_negative*, and *false_negative*.</span></span> <span data-ttu-id="63cc4-224">In de onderstaande query's we uitschakelen visualisatie met `-q` en ook de uitvoer op te slaan (met behulp van `-o`) als dataframes die vervolgens kunnen worden gebruikt met de `%%local` verwerkt Magic-pakket.</span><span class="sxs-lookup"><span data-stu-id="63cc4-224">In the queries below, we turn off visualization by using `-q` and also save the output (by using `-o`) as dataframes that can be then used with the `%%local` magic.</span></span>

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. <span data-ttu-id="63cc4-225">Ten slotte het volgende fragment gebruiken voor het genereren van het tekengebied via **Matplotlib**.</span><span class="sxs-lookup"><span data-stu-id="63cc4-225">Finally, use the following snippet to generate the plot using **Matplotlib**.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="63cc4-226">U ziet de volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="63cc4-226">You should see the following output:</span></span>

    <span data-ttu-id="63cc4-227">![Spark machine learning-uitvoer van de toepassing - cirkeldiagram percentages van mislukte voeding controles. ] (./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark machine learning-resultaat-uitvoer")</span><span class="sxs-lookup"><span data-stu-id="63cc4-227">![Spark machine learning application output - pie chart percentages of failed food inspections.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark machine learning result output")</span></span>

    <span data-ttu-id="63cc4-228">In deze grafiek verwijst ' ' positief naar de inspectie mislukte voeding, terwijl een negatief resultaat naar een doorgegeven inspectie verwijst.</span><span class="sxs-lookup"><span data-stu-id="63cc4-228">In this chart, a "positive" result refers to the failed food inspection, while a negative result refers to a passed inspection.</span></span>

## <a name="shut-down-the-notebook"></a><span data-ttu-id="63cc4-229">De notebook afsluiten</span><span class="sxs-lookup"><span data-stu-id="63cc4-229">Shut down the notebook</span></span>
<span data-ttu-id="63cc4-230">Nadat u klaar bent met het uitvoeren van de toepassing, moet u de notebook om resources vrij te geven afgesloten.</span><span class="sxs-lookup"><span data-stu-id="63cc4-230">After you have finished running the application, you should shut down the notebook to release the resources.</span></span> <span data-ttu-id="63cc4-231">Dit doet u door in het menu **Bestand** in de notebook te klikken op **Sluiten en stoppen**.</span><span class="sxs-lookup"><span data-stu-id="63cc4-231">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="63cc4-232">Dit wordt afgesloten en wordt de notebook gesloten.</span><span class="sxs-lookup"><span data-stu-id="63cc4-232">This shuts down and closes the notebook.</span></span>

## <span data-ttu-id="63cc4-233"><a name="seealso"></a>Zie ook</span><span class="sxs-lookup"><span data-stu-id="63cc4-233"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="63cc4-234">Overzicht: Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="63cc4-234">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="63cc4-235">Scenario's</span><span class="sxs-lookup"><span data-stu-id="63cc4-235">Scenarios</span></span>
* [<span data-ttu-id="63cc4-236">Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools</span><span class="sxs-lookup"><span data-stu-id="63cc4-236">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="63cc4-237">Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens</span><span class="sxs-lookup"><span data-stu-id="63cc4-237">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="63cc4-238">Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen</span><span class="sxs-lookup"><span data-stu-id="63cc4-238">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="63cc4-239">Websitelogboekanalyse met Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="63cc4-239">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="63cc4-240">Toepassingen maken en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="63cc4-240">Create and run applications</span></span>
* [<span data-ttu-id="63cc4-241">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="63cc4-241">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="63cc4-242">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="63cc4-242">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="63cc4-243">Tools en uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="63cc4-243">Tools and extensions</span></span>
* [<span data-ttu-id="63cc4-244">De invoegtoepassing HDInsight Tools for IntelliJ IDEA gebruiken om Spark Scala-toepassingen te maken en in te dienen</span><span class="sxs-lookup"><span data-stu-id="63cc4-244">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="63cc4-245">De invoegtoepassing HDInsight Tools for IntelliJ IDEA gebruiken om op afstand fouten in Spark Scala-toepassingen op te lossen</span><span class="sxs-lookup"><span data-stu-id="63cc4-245">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="63cc4-246">Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="63cc4-246">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="63cc4-247">Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="63cc4-247">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="63cc4-248">Externe pakketten gebruiken met Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="63cc4-248">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="63cc4-249">Jupyter op uw computer installeren en verbinding maken met een HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="63cc4-249">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="63cc4-250">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="63cc4-250">Manage resources</span></span>
* [<span data-ttu-id="63cc4-251">Resources beheren voor het Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="63cc4-251">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="63cc4-252">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="63cc4-252">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
