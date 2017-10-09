---
title: Voorbeeld met MLlib Spark in HDInsight - Azure learning aaaMachine | Microsoft Docs
description: Meer informatie over hoe toouse Spark MLlib toocreate een machine learning-app die een gegevensset met behulp van classificatie via logistic regression analyseert.
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
ms.openlocfilehash: 5c3b83482de5d8fba224398aaafe07fa67ec1fb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-spark-mllib-toobuild-a-machine-learning-application-and-analyze-a-dataset"></a><span data-ttu-id="5e0a0-104">Een machine learning-toepassing voor Spark MLlib toobuild gebruiken en analyseren van een gegevensset</span><span class="sxs-lookup"><span data-stu-id="5e0a0-104">Use Spark MLlib toobuild a machine learning application and analyze a dataset</span></span>

<span data-ttu-id="5e0a0-105">Meer informatie over hoe toouse Spark **MLlib** toocreate een machine learning-toepassing toodo eenvoudige predictive Analytics op een open gegevensset.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-105">Learn how toouse Spark **MLlib** toocreate a machine learning application toodo simple predictive analysis on an open dataset.</span></span> <span data-ttu-id="5e0a0-106">Van Spark van ingebouwde machine learning-bibliotheken, in dit voorbeeld wordt *classificatie* via logistic regression.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-106">From Spark's built-in machine learning libraries, this example uses *classification* through logistic regression.</span></span> 

> [!TIP]
> <span data-ttu-id="5e0a0-107">In dit voorbeeld is ook beschikbaar als een Jupyter-notebook op een cluster Spark (Linux) die u in HDInsight maakt.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-107">This example is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="5e0a0-108">Hallo-notebook ervaring kunt u Hallo Python codefragmenten uit Hallo laptop zelf uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-108">hello notebook experience lets you run hello Python snippets from hello notebook itself.</span></span> <span data-ttu-id="5e0a0-109">toofollow hello zelfstudie uit binnen een laptop een Spark-cluster en start een Jupyter-notebook maken (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span><span class="sxs-lookup"><span data-stu-id="5e0a0-109">toofollow hello tutorial from within a notebook, create a Spark cluster and launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`).</span></span> <span data-ttu-id="5e0a0-110">Voer vervolgens de notebook Hallo **Spark Machine Learning - Predictive Analytics op voeding inspectie gegevens met behulp van MLlib.ipynb** onder Hallo **Python** map.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-110">Then, run hello notebook **Spark Machine Learning - Predictive analysis on food inspection data using MLlib.ipynb** under hello **Python** folder.</span></span>
>
>

<span data-ttu-id="5e0a0-111">MLlib is een core Spark-bibliotheek met veel nuttige hulpprogramma's voor machine learning taken, waaronder hulpprogramma's die geschikt zijn voor:</span><span class="sxs-lookup"><span data-stu-id="5e0a0-111">MLlib is a core Spark library that provides many utilities useful for machine learning tasks, including utilities that are suitable for:</span></span>

* <span data-ttu-id="5e0a0-112">Classificatie</span><span class="sxs-lookup"><span data-stu-id="5e0a0-112">Classification</span></span>
* <span data-ttu-id="5e0a0-113">Regressie</span><span class="sxs-lookup"><span data-stu-id="5e0a0-113">Regression</span></span>
* <span data-ttu-id="5e0a0-114">Clustering</span><span class="sxs-lookup"><span data-stu-id="5e0a0-114">Clustering</span></span>
* <span data-ttu-id="5e0a0-115">Onderwerp-model</span><span class="sxs-lookup"><span data-stu-id="5e0a0-115">Topic modeling</span></span>
* <span data-ttu-id="5e0a0-116">Enkelvoudige waarde afbreken (SVD) en analyse van de principal-onderdeel (Pso)</span><span class="sxs-lookup"><span data-stu-id="5e0a0-116">Singular value decomposition (SVD) and principal component analysis (PCA)</span></span>
* <span data-ttu-id="5e0a0-117">Hypothese testen en het berekenen van de voorbeeld-statistieken</span><span class="sxs-lookup"><span data-stu-id="5e0a0-117">Hypothesis testing and calculating sample statistics</span></span>

## <a name="what-are-classification-and-logistic-regression"></a><span data-ttu-id="5e0a0-118">Wat zijn de classificatie en logistic regression?</span><span class="sxs-lookup"><span data-stu-id="5e0a0-118">What are classification and logistic regression?</span></span>
<span data-ttu-id="5e0a0-119">*Classificatie*, een populaire machine learning-taak is Hallo-proces voor het sorteren van invoergegevens in categorieën.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-119">*Classification*, a popular machine learning task, is hello process of sorting input data into categories.</span></span> <span data-ttu-id="5e0a0-120">Is het Hallo-taak van een classificatie algoritme toofigure hoe tooassign 'labels' tooinput gegevens die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-120">It is hello job of a classification algorithm toofigure out how tooassign "labels" tooinput data that you provide.</span></span> <span data-ttu-id="5e0a0-121">Bijvoorbeeld, u een machine learning-algoritme dat vooraf gedefinieerde gegevens als invoer accepteert kan zien en delen Hallo stock in twee categorieën: bestanden die u moet verkoopt en bestanden die u dient te houden.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-121">For example, you could think of a machine learning algorithm that accepts stock information as input and divides hello stock into two categories: stocks that you should sell and stocks that you should keep.</span></span>

<span data-ttu-id="5e0a0-122">Logistic regression is Hallo-algoritme dat u voor classificatie gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-122">Logistic regression is hello algorithm that you use for classification.</span></span> <span data-ttu-id="5e0a0-123">De Spark logistic regression API is nuttig voor *binaire classificatie*, of de ingevoerde gegevens classificeren in een van twee groepen.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-123">Spark's logistic regression API is useful for *binary classification*, or classifying input data into one of two groups.</span></span> <span data-ttu-id="5e0a0-124">Zie voor meer informatie over logistic regressies [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span><span class="sxs-lookup"><span data-stu-id="5e0a0-124">For more information about logistic regressions, see [Wikipedia](https://en.wikipedia.org/wiki/Logistic_regression).</span></span>

<span data-ttu-id="5e0a0-125">Kortom, Hallo proces logistic regression produceert een *logistic functie* die kunnen worden gebruikt toopredict Hallo kans dat een invoer-vector in een groep of andere Hallo behoort.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-125">In summary, hello process of logistic regression produces a *logistic function* that can be used toopredict hello probability that an input vector belongs in one group or hello other.</span></span>  

## <a name="predictive-analysis-example-on-food-inspection-data"></a><span data-ttu-id="5e0a0-126">Predictive Analytics-voorbeeld op voeding inspectie gegevens</span><span class="sxs-lookup"><span data-stu-id="5e0a0-126">Predictive analysis example on food inspection data</span></span>
<span data-ttu-id="5e0a0-127">In dit voorbeeld u Spark tooperform sommige predictive Analytics op voeding inspectie gegevens gebruiken (**Food_Inspections1.csv**) die is verkregen via Hallo [Den Haag gegevensportal](https://data.cityofchicago.org/).</span><span class="sxs-lookup"><span data-stu-id="5e0a0-127">In this example, you use Spark tooperform some predictive analysis on food inspection data (**Food_Inspections1.csv**) that was acquired through hello [City of Chicago data portal](https://data.cityofchicago.org/).</span></span> <span data-ttu-id="5e0a0-128">Deze gegevensset bevat informatie over voeding inrichting controles zijn uitgevoerd in Chicago, inclusief informatie over elke inrichting, Hallo schendingen gevonden (indien aanwezig) en resultaten van Hallo inspectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-128">This dataset contains information about food establishment inspections that were conducted in Chicago, including information about each establishment, hello violations found (if any), and hello results of hello inspection.</span></span> <span data-ttu-id="5e0a0-129">Hallo CSV-bestand is al beschikbaar in Hallo storage-account is gekoppeld aan het cluster op Hallo **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-129">hello CSV data file is already available in hello storage account associated with hello cluster at **/HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv**.</span></span>

<span data-ttu-id="5e0a0-130">In onderstaande Hallo stappen, ontwikkelen van een model toosee wat er toopass nodig is of een voeding inspectie mislukken.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-130">In hello steps below, you develop a model toosee what it takes toopass or fail a food inspection.</span></span>

## <a name="start-building-a-spark-mmlib-machine-learning-app"></a><span data-ttu-id="5e0a0-131">Beginnen met het samenstellen van een Spark-MMLib machine learning-app</span><span class="sxs-lookup"><span data-stu-id="5e0a0-131">Start building a Spark MMLib machine learning app</span></span>
1. <span data-ttu-id="5e0a0-132">Van Hallo [Azure-portal](https://portal.azure.com/), vanaf Hallo startboard, klikt u op Hallo tegel voor uw Spark-cluster (als u toohello startboard vastgemaakt).</span><span class="sxs-lookup"><span data-stu-id="5e0a0-132">From hello [Azure portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="5e0a0-133">U kunt ook tooyour cluster onder navigeren **door alles bladeren** > **HDInsight-Clusters**.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-133">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
1. <span data-ttu-id="5e0a0-134">Klik op Hallo blade Spark-cluster **Cluster-Dashboard**, en klik vervolgens op **Jupyter-Notebook**.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-134">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="5e0a0-135">Voer desgevraagd Hallo beheerdersreferenties voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-135">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5e0a0-136">U mogelijk ook Hallo Jupyter-Notebook voor uw cluster door de volgende URL in uw browser openen-Hallo bereiken.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-136">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="5e0a0-137">Vervang **CLUSTERNAME** met Hallo-naam van het cluster:</span><span class="sxs-lookup"><span data-stu-id="5e0a0-137">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
1. <span data-ttu-id="5e0a0-138">Maak een notebook.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-138">Create a notebook.</span></span> <span data-ttu-id="5e0a0-139">Klik op **Nieuw** en klik vervolgens op **PySpark**.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-139">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="5e0a0-140">![Maken van een Jupyter-notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "een nieuwe Jupyter-notebook maken")</span><span class="sxs-lookup"><span data-stu-id="5e0a0-140">![Create a Jupyter notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-create-jupyter.png "Create a new Jupyter notebook")</span></span>
1. <span data-ttu-id="5e0a0-141">Een nieuwe notebook gemaakt en geopend met de Hallo naam Untitled.pynb.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-141">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="5e0a0-142">Klik op Hallo notebook naam Hallo boven en een beschrijvende naam.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-142">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="5e0a0-143">![Geef een naam voor de notebook Hallo](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Geef een naam voor de notebook Hallo")</span><span class="sxs-lookup"><span data-stu-id="5e0a0-143">![Provide a name for hello notebook](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-name-jupyter.png "Provide a name for hello notebook")</span></span>
1. <span data-ttu-id="5e0a0-144">Omdat u de notebook met behulp van Hallo PySpark-kernel hebt gemaakt, hoeft u geen toocreate contexten expliciet.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-144">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="5e0a0-145">Hallo Spark en Hive-contexten worden automatisch voor u gemaakt wanneer u de eerste codecel Hallo uitvoert.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-145">hello Spark and Hive contexts are automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="5e0a0-146">U kunt beginnen met het bouwen van uw machine learning-toepassing hello typen die nodig zijn voor dit scenario te importeren.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-146">You can start building your machine learning application by importing hello types required for this scenario.</span></span> <span data-ttu-id="5e0a0-147">Hallo cursor toodo dus plaats in Hallo cel en druk op **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-147">toodo so, place hello cursor in hello cell and press **SHIFT + ENTER**.</span></span>

        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
        from pyspark.sql.functions import UserDefinedFunction
        from pyspark.sql.types import *

## <a name="construct-an-input-dataframe"></a><span data-ttu-id="5e0a0-148">Maken van een invoer dataframe</span><span class="sxs-lookup"><span data-stu-id="5e0a0-148">Construct an input dataframe</span></span>
<span data-ttu-id="5e0a0-149">We kunnen gebruiken `sqlContext` tooperform transformaties voor gestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-149">We can use `sqlContext` tooperform transformations on structured data.</span></span> <span data-ttu-id="5e0a0-150">de eerste taak Hallo is tooload Hallo voorbeeldgegevens ((**Food_Inspections1.csv**)) in een Spark SQL *dataframe*.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-150">hello first task is tooload hello sample data ((**Food_Inspections1.csv**)) into a Spark SQL *dataframe*.</span></span>

1. <span data-ttu-id="5e0a0-151">Omdat de onbewerkte gegevens Hallo zich in een CSV-indeling, moeten we toouse Hallo Spark context toopull elke regel van het Hallo-bestand in het geheugen als niet-gestructureerde tekst; vervolgens gebruikt u Python van CSV-bibliotheek tooparse elke regel afzonderlijk.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-151">Because hello raw data is in a CSV format, we need toouse hello Spark context toopull every line of hello file into memory as unstructured text; then, you use Python's CSV library tooparse each line individually.</span></span>

        def csvParse(s):
            import csv
            from StringIO import StringIO
            sio = StringIO(s)
            value = csv.reader(sio).next()
            sio.close()
            return value

        inspections = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections1.csv')\
                        .map(csvParse)
1. <span data-ttu-id="5e0a0-152">We nu hebben Hallo CSV-bestand als een RDD.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-152">We now have hello CSV file as an RDD.</span></span>  <span data-ttu-id="5e0a0-153">toounderstand hello schema van Hallo gegevens, we één rij ophalen vanuit Hallo RDD.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-153">toounderstand hello schema of hello data, we retrieve one row from hello RDD.</span></span>

        inspections.take(1)

    <span data-ttu-id="5e0a0-154">Hier ziet u uitvoer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="5e0a0-154">You should see an output like hello following:</span></span>

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
          '24. DISH WASHING FACILITIES: PROPERLY DESIGNED, CONSTRUCTED, MAINTAINED, INSTALLED, LOCATED AND OPERATED - Comments: All dishwashing machines must be of a type that complies with all requirements of hello plumbing section of hello Municipal Code of Chicago and Rules and Regulation of hello Board of Health. OBSEVERD hello 3 COMPARTMENT SINK BACKING UP INTO hello 1ST AND 2ND COMPARTMENT WITH CLEAR WATER AND SLOWLY DRAINING OUT. INST NEED HAVE IT REPAIR. CITATION ISSUED, SERIOUS VIOLATION 7-38-030 H000062369-10 COURT DATE 10-28-10 TIME 1 P.M. ROOM 107 400 W. SURPERIOR. | 36. LIGHTING: REQUIRED MINIMUM FOOT-CANDLES OF LIGHT PROVIDED, FIXTURES SHIELDED - Comments: Shielding tooprotect against broken glass falling into food shall be provided for all artificial lighting sources in preparation, service, and display facilities. LIGHT SHIELD ARE MISSING UNDER HOOD OF  COOKING EQUIPMENT AND NEED tooREPLACE LIGHT UNDER UNIT. 4 LIGHTS ARE OUT IN hello REAR CHILDREN AREA,IN hello KINDERGARDEN CLASS ROOM. 2 LIGHT ARE OUT EAST REAR, LIGHT FRONT WEST ROOM. NEED tooREPLACE ALL LIGHT THAT ARE NOT WORKING. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned. MISSING CEILING TILES WITH STAINS IN WEST,EAST, IN FRONT AREA WEST, AND BY hello 15MOS AREA. NEED tooBE REPLACED. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair. SPLASH GUARDED ARE NEEDED BY hello EXPOSED HAND SINK IN hello KITCHEN AREA | 34. FLOORS: CONSTRUCTED PER CODE, CLEANED, GOOD REPAIR, COVING INSTALLED, DUST-LESS CLEANING METHODS USED - Comments: hello floors shall be constructed per code, be smooth and easily cleaned, and be kept clean and in good repair. INST NEED tooELEVATE ALL FOOD ITEMS 6INCH OFF hello FLOOR 6 INCH AWAY FORM WALL.  ',
          '41.97583445690982',
          '-87.7107455232781',
          '(41.97583445690982, -87.7107455232781)']]
1. <span data-ttu-id="5e0a0-155">Hallo geeft voorgaande uitvoer ons een idee van schema van het invoerbestand Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-155">hello preceding output gives us an idea of hello schema of hello input file.</span></span> <span data-ttu-id="5e0a0-156">Het bevat Hallo-naam van elke tot stand brengen, Hallo type tot stand brengen, Hallo-adres, Hallo gegevens van Hallo inspecties en Hallo locatie, onder andere.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-156">It includes hello name of every establishment, hello type of establishment, hello address, hello data of hello inspections, and hello location, among other things.</span></span> <span data-ttu-id="5e0a0-157">Laten we enkele kolommen selecteren die zijn handig voor onze predictive Analytics en Hallo resultaten groeperen als een dataframe welke we vervolgens toocreate een tijdelijke tabel gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-157">Let's select a few columns that are useful for our predictive analysis and group hello results as a dataframe, which we then use toocreate a temporary table.</span></span>

        schema = StructType([
        StructField("id", IntegerType(), False),
        StructField("name", StringType(), False),
        StructField("results", StringType(), False),
        StructField("violations", StringType(), True)])

        df = sqlContext.createDataFrame(inspections.map(lambda l: (int(l[0]), l[1], l[12], l[13])) , schema)
        df.registerTempTable('CountResults')
1. <span data-ttu-id="5e0a0-158">Nu een *dataframe*, `df` waarop we onze analyse kunt uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-158">We now have a *dataframe*, `df` on which we can perform our analysis.</span></span> <span data-ttu-id="5e0a0-159">We hebben ook een aanroep van de tijdelijke tabel **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-159">We also have a temporary table call **CountResults**.</span></span> <span data-ttu-id="5e0a0-160">Vindt u vier kolommen in Hallo dataframe van belang: **id**, **naam**, **resultaten**, en **schendingen**.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-160">We've included four columns of interest in hello dataframe: **id**, **name**, **results**, and **violations**.</span></span>

    <span data-ttu-id="5e0a0-161">We gaan een klein aantal Hallo-gegevens ophalen:</span><span class="sxs-lookup"><span data-stu-id="5e0a0-161">Let's get a small sample of hello data:</span></span>

        df.show(5)

    <span data-ttu-id="5e0a0-162">Hier ziet u uitvoer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="5e0a0-162">You should see an output like hello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        +------+--------------------+-------+--------------------+
        |    id|                name|results|          violations|
        +------+--------------------+-------+--------------------+
        |413707|       LUNA PARK INC|   Fail|24. DISH WASHING ...|
        |391234|       CAFE SELMARIE|   Fail|2. FACILITIES too...|
        |413751|          MANCHU WOK|   Pass|33. FOOD AND NON-...|
        |413708|BENCHMARK HOSPITA...|   Pass|                    |
        |413722|           JJ BURGER|   Pass|                    |
        +------+--------------------+-------+--------------------+

## <a name="understand-hello-data"></a><span data-ttu-id="5e0a0-163">Hallo gegevens begrijpen</span><span class="sxs-lookup"><span data-stu-id="5e0a0-163">Understand hello data</span></span>
1. <span data-ttu-id="5e0a0-164">Laten we beginnen tooget een beeld krijgt van wat onze gegevensset bevat.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-164">Let's start tooget a sense of what our dataset contains.</span></span> <span data-ttu-id="5e0a0-165">Wat zijn bijvoorbeeld verschillende waarden in Hallo Hallo **resultaten** kolom?</span><span class="sxs-lookup"><span data-stu-id="5e0a0-165">For example, what are hello different values in hello **results** column?</span></span>

        df.select('results').distinct().show()

    <span data-ttu-id="5e0a0-166">Hier ziet u uitvoer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="5e0a0-166">You should see an output like hello following:</span></span>

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
1. <span data-ttu-id="5e0a0-167">Een snelle visualisatie kan we beter reden over Hallo verdeling van deze resultaten.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-167">A quick visualization can help us reason about hello distribution of these outcomes.</span></span> <span data-ttu-id="5e0a0-168">Er bestaat reeds Hallo gegevens in een tijdelijke tabel **CountResults**.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-168">We already have hello data in a temporary table **CountResults**.</span></span> <span data-ttu-id="5e0a0-169">U kunt volgende SQL-query op Hallo tabel tooget Hallo uitvoeren een beter inzicht in hoe Hallo resultaten worden gedistribueerd.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-169">You can run hello following SQL query against hello table tooget a better understanding of how hello results are distributed.</span></span>

        %%sql -o countResultsdf
        SELECT results, COUNT(results) AS cnt FROM CountResults GROUP BY results

    <span data-ttu-id="5e0a0-170">Hallo `%%sql` magic gevolgd door `-o countResultsdf` zorgt ervoor dat Hallo-uitvoer van Hallo query lokaal worden bewaard op Hallo Jupyter-server (meestal Hallo headnode van Hallo cluster).</span><span class="sxs-lookup"><span data-stu-id="5e0a0-170">hello `%%sql` magic followed by `-o countResultsdf` ensures that hello output of hello query is persisted locally on hello Jupyter server (typically hello headnode of hello cluster).</span></span> <span data-ttu-id="5e0a0-171">Hallo-uitvoer is doorgevoerd als een [Pandas](http://pandas.pydata.org/) dataframe Hello naam opgegeven **countResultsdf**.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-171">hello output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with hello specified name **countResultsdf**.</span></span>

    <span data-ttu-id="5e0a0-172">Hier ziet u uitvoer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="5e0a0-172">You should see an output like hello following:</span></span>

    <span data-ttu-id="5e0a0-173">![Uitvoer van de SQL-query](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "uitvoer van de SQL-query")</span><span class="sxs-lookup"><span data-stu-id="5e0a0-173">![SQL query output](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-query-output.png "SQL query output")</span></span>

    <span data-ttu-id="5e0a0-174">Voor meer informatie over Hallo `%%sql` magic en andere magics die beschikbaar zijn met de PySpark-kernel hello, Zie [beschikbare Kernels op Jupyter-notebooks met HDInsight Spark-clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span><span class="sxs-lookup"><span data-stu-id="5e0a0-174">For more information about hello `%%sql` magic, and other magics available with hello PySpark kernel, see [Kernels available on Jupyter notebooks with Spark HDInsight clusters](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
1. <span data-ttu-id="5e0a0-175">U kunt ook Matplotlib gebruiken, een bibliotheek tooconstruct visualisatie van gegevens, toocreate tekent gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-175">You can also use Matplotlib, a library used tooconstruct visualization of data, toocreate a plot.</span></span> <span data-ttu-id="5e0a0-176">Omdat Hallo grafiek moet worden gemaakt van Hallo lokaal persistent **countResultsdf** dataframe, Hallo codefragment moet beginnen met Hallo `%%local` verwerkt Magic-pakket.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-176">Because hello plot must be created from hello locally persisted **countResultsdf** dataframe, hello code snippet must begin with hello `%%local` magic.</span></span> <span data-ttu-id="5e0a0-177">Dit zorgt ervoor dat Hallo-code op Hallo Jupyter server lokaal wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-177">This ensures that hello code is run locally on hello Jupyter server.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = countResultsdf['results']
        sizes = countResultsdf['cnt']
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="5e0a0-178">Hier ziet u uitvoer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="5e0a0-178">You should see an output like hello following:</span></span>

    <span data-ttu-id="5e0a0-179">![Spark machine learning-toepassing output - cirkeldiagram met vijf verschillende controleresultaten](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark machine learning-resultaat-uitvoer")</span><span class="sxs-lookup"><span data-stu-id="5e0a0-179">![Spark machine learning application output - pie chart with five distinct inspection results](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-1.png "Spark machine learning result output")</span></span>
1. <span data-ttu-id="5e0a0-180">U kunt zien dat er 5 verschillende resultaten, waarvoor een inspectie kan zijn:</span><span class="sxs-lookup"><span data-stu-id="5e0a0-180">You can see that there are 5 distinct results that an inspection can have:</span></span>

   * <span data-ttu-id="5e0a0-181">Bedrijven niet vinden</span><span class="sxs-lookup"><span data-stu-id="5e0a0-181">Business not located</span></span>
   * <span data-ttu-id="5e0a0-182">Mislukt</span><span class="sxs-lookup"><span data-stu-id="5e0a0-182">Fail</span></span>
   * <span data-ttu-id="5e0a0-183">Doorgeven</span><span class="sxs-lookup"><span data-stu-id="5e0a0-183">Pass</span></span>
   * <span data-ttu-id="5e0a0-184">PSS met voorwaarden</span><span class="sxs-lookup"><span data-stu-id="5e0a0-184">Pss w/ conditions</span></span>
   * <span data-ttu-id="5e0a0-185">Buiten bedrijf</span><span class="sxs-lookup"><span data-stu-id="5e0a0-185">Out of Business</span></span>

     <span data-ttu-id="5e0a0-186">Laat het ons een model voor het resultaat van een opgegeven Hallo schendingen van het inspectie voeding Hallo kan raden ontwikkelen.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-186">Let us develop a model that can guess hello outcome of a food inspection, given hello violations.</span></span> <span data-ttu-id="5e0a0-187">Aangezien logistic regression een classificatiemethode binaire is, maakt zin toogroup onze gegevens in twee categorieën: **mislukken** en **doorgeven**.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-187">Since logistic regression is a binary classification method, it makes sense toogroup our data into two categories: **Fail** and **Pass**.</span></span> <span data-ttu-id="5e0a0-188">Een 'doorgeven met voorwaarden"is nog steeds een Pass, zodat wanneer we Hallo model trainen, we beschouwen Hallo twee equivalent resulteert.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-188">A "Pass w/ Conditions" is still a Pass, so when we train hello model, we consider hello two results equivalent.</span></span> <span data-ttu-id="5e0a0-189">Gegevens met Hallo andere resultaten ('Bedrijven niet vinden' of 'Out of Business') zijn niet handig zodat we uit onze trainingset verwijderen.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-189">Data with hello other results ("Business Not Located" or "Out of Business") are not useful so we remove them from our training set.</span></span> <span data-ttu-id="5e0a0-190">Dit mag geen probleem omdat deze twee categorieën gezamenlijk een kleine hoeveelheid van Hallo resultaten toch.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-190">This should be okay since these two categories make up a very small percentage of hello results anyway.</span></span>
1. <span data-ttu-id="5e0a0-191">Laat het ons opwekken en onze bestaande dataframe converteren (`df`) in een nieuwe dataframe waar elke inspectie wordt weergegeven als een combinatie van schendingen van het label.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-191">Let us go ahead and convert our existing dataframe(`df`) into a new dataframe where each inspection is represented as a label-violations pair.</span></span> <span data-ttu-id="5e0a0-192">In ons geval een label van `0.0` vertegenwoordigt een fout optreedt, wordt een label van `1.0` vertegenwoordigt een is voltooid en een label van `-1.0` bepaalde resultaten naast deze twee vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-192">In our case, a label of `0.0` represents a failure, a label of `1.0` represents a success, and a label of `-1.0` represents some results besides those two.</span></span> <span data-ttu-id="5e0a0-193">We uitfilteren die andere resultaten bij het berekenen van de nieuwe gegevensframe Hallo.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-193">We filter those other results out when computing hello new data frame.</span></span>

        def labelForResults(s):
            if s == 'Fail':
                return 0.0
            elif s == 'Pass w/ Conditions' or s == 'Pass':
                return 1.0
            else:
                return -1.0
        label = UserDefinedFunction(labelForResults, DoubleType())
        labeledData = df.select(label(df.results).alias('label'), df.violations).where('label >= 0')

    <span data-ttu-id="5e0a0-194">toosee welke Hallo gelabeld gegevens lijkt, gaan we één rij ophalen.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-194">toosee what hello labeled data looks like, let's retrieve one row.</span></span>

        labeledData.take(1)

    <span data-ttu-id="5e0a0-195">Hier ziet u uitvoer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="5e0a0-195">You should see an output like hello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [Row(label=0.0, violations=u"41. PREMISES MAINTAINED FREE OF LITTER, UNNECESSARY ARTICLES, CLEANING  EQUIPMENT PROPERLY STORED - Comments: All parts of hello food establishment and all parts of hello property used in connection with hello operation of hello establishment shall be kept neat and clean and should not produce any offensive odors.  REMOVE MATTRESS FROM SMALL DUMPSTER. | 35. WALLS, CEILINGS, ATTACHED EQUIPMENT CONSTRUCTED PER CODE: GOOD REPAIR, SURFACES CLEAN AND DUST-LESS CLEANING METHODS - Comments: hello walls and ceilings shall be in good repair and easily cleaned.  REPAIR MISALIGNED DOORS AND DOOR NEAR ELEVATOR.  DETAIL CLEAN BLACK MOLD LIKE SUBSTANCE FROM WALLS BY BOTH DISH MACHINES.  REPAIR OR REMOVE BASEBOARD UNDER DISH MACHINE (LEFT REAR KITCHEN). SEAL ALL GAPS.  REPLACE MILK CRATES USED IN WALK IN COOLERS AND STORAGE AREAS WITH PROPER SHELVING AT LEAST 6' OFF hello FLOOR.  | 38. VENTILATION: ROOMS AND EQUIPMENT VENTED AS REQUIRED: PLUMBING: INSTALLED AND MAINTAINED - Comments: hello flow of air discharged from kitchen fans shall always be through a duct tooa point above hello roofline.  REPAIR BROKEN VENTILATION IN MEN'S AND WOMEN'S WASHROOMS NEXT tooDINING AREA. | 32. FOOD AND NON-FOOD CONTACT SURFACES PROPERLY DESIGNED, CONSTRUCTED AND MAINTAINED - Comments: All food and non-food contact equipment and utensils shall be smooth, easily cleanable, and durable, and shall be in good repair.  REPAIR DAMAGED PLUG ON LEFT SIDE OF 2 COMPARTMENT SINK.  REPAIR SELF CLOSER ON BOTTOM LEFT DOOR OF 4 DOOR PREP UNIT NEXT tooOFFICE.")]

## <a name="create-a-logistic-regression-model-from-hello-input-dataframe"></a><span data-ttu-id="5e0a0-196">Een logistic regressiemodel maken van de invoer dataframe Hallo</span><span class="sxs-lookup"><span data-stu-id="5e0a0-196">Create a logistic regression model from hello input dataframe</span></span>
<span data-ttu-id="5e0a0-197">De laatste taak is tooconvert Hallo gegevens naar een indeling die kan worden geanalyseerd door logistic regression gelabeld.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-197">Our final task is tooconvert hello labeled data into a format that can be analyzed by logistic regression.</span></span> <span data-ttu-id="5e0a0-198">Hallo invoer tooa logistic regression-algoritme moet een reeks *label-functie vector paren*, waarbij 'functie vector' hello vector van de getallen die invoer Hallo-punt.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-198">hello input tooa logistic regression algorithm should be a set of *label-feature vector pairs*, where hello "feature vector" is a vector of numbers representing hello input point.</span></span> <span data-ttu-id="5e0a0-199">Dus moeten we tooconvert Hallo 'schendingen' kolom, die is semi-gestructureerde en bevat veel opmerkingen in vrije tekst tooan matrix van real-getallen die met een machine gemakkelijk kan begrijpen.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-199">So, we need tooconvert hello "violations" column, which is semi-structured and contains many comments in free-text, tooan array of real numbers that a machine could easily understand.</span></span>

<span data-ttu-id="5e0a0-200">Een standaard machine learning-benadering voor de verwerking van natuurlijke taal is tooassign elk woord distinct 'index' en geeft u een vector toohello machine learning-algoritme dat de waarde voor elke index Hallo relatieve frequentie van dat woord in de tekst hello bevat tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-200">One standard machine learning approach for processing natural language is tooassign each distinct word an "index", and then pass a vector toohello machine learning algorithm such that each index's value contains hello relative frequency of that word in hello text string.</span></span>

<span data-ttu-id="5e0a0-201">MLlib biedt een eenvoudige manier tooperform deze bewerking.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-201">MLlib provides an easy way tooperform this operation.</span></span> <span data-ttu-id="5e0a0-202">Eerst 'basisvormen' elke schendingen tekenreeks tooget Hallo afzonderlijke woorden in elke tekenreeks.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-202">First, "tokenize" each violations string tooget hello individual words in each string.</span></span> <span data-ttu-id="5e0a0-203">Vervolgens gebruikt u een `HashingTF` tooconvert elke set tokens in een functie-vector vervolgens doorgegeven toohello logistic regression-algoritme tooconstruct worden kan een model.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-203">Then, use a `HashingTF` tooconvert each set of tokens into a feature vector that can then be passed toohello logistic regression algorithm tooconstruct a model.</span></span> <span data-ttu-id="5e0a0-204">We uitvoeren alle deze stappen in de reeks met behulp van een "pipeline".</span><span class="sxs-lookup"><span data-stu-id="5e0a0-204">We conduct all of these steps in sequence using a "pipeline".</span></span>

    tokenizer = Tokenizer(inputCol="violations", outputCol="words")
    hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
    lr = LogisticRegression(maxIter=10, regParam=0.01)
    pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])

    model = pipeline.fit(labeledData)

## <a name="evaluate-hello-model-on-a-separate-test-dataset"></a><span data-ttu-id="5e0a0-205">Hallo-model op een afzonderlijke testgegevensset evalueren</span><span class="sxs-lookup"><span data-stu-id="5e0a0-205">Evaluate hello model on a separate test dataset</span></span>
<span data-ttu-id="5e0a0-206">We kunnen gebruiken we eerder hebben gemaakt Hallo-model te*voorspellen* welke Hallo resultaten van de nieuwe inspecties zijn zal, op basis van Hallo schendingen die zijn waargenomen.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-206">We can use hello model we created earlier too*predict* what hello results of new inspections will be, based on hello violations that were observed.</span></span> <span data-ttu-id="5e0a0-207">We dit model op Hallo gegevensset getraind **Food_Inspections1.csv**.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-207">We trained this model on hello dataset **Food_Inspections1.csv**.</span></span> <span data-ttu-id="5e0a0-208">Laat het ons gebruik van een tweede gegevensset **Food_Inspections2.csv**, te*evalueren* Hallo sterkte van dit model op nieuwe gegevens.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-208">Let us use a second dataset, **Food_Inspections2.csv**, too*evaluate* hello strength of this model on new data.</span></span> <span data-ttu-id="5e0a0-209">Deze tweede gegevensverzameling (**Food_Inspections2.csv**) moet al Hallo standaardopslagcontainer die zijn gekoppeld aan het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-209">This second data set (**Food_Inspections2.csv**) should already be in hello default storage container associated with hello cluster.</span></span>

1. <span data-ttu-id="5e0a0-210">Hallo volgende codefragment maakt een nieuwe dataframe **predictionsDf** die Hallo voorspelling gegenereerd door Hallo model bevat.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-210">hello following snippet creates a new dataframe, **predictionsDf** that contains hello prediction generated by hello model.</span></span> <span data-ttu-id="5e0a0-211">Hallo-codefragment maakt ook een tijdelijke tabel genaamd **voorspellingen** op basis van Hallo dataframe.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-211">hello snippet also creates a temporary table called **Predictions** based on hello dataframe.</span></span>

        testData = sc.textFile('wasb:///HdiSamples/HdiSamples/FoodInspectionData/Food_Inspections2.csv')\
                 .map(csvParse) \
                 .map(lambda l: (int(l[0]), l[1], l[12], l[13]))
        testDf = sqlContext.createDataFrame(testData, schema).where("results = 'Fail' OR results = 'Pass' OR results = 'Pass w/ Conditions'")
        predictionsDf = model.transform(testDf)
        predictionsDf.registerTempTable('Predictions')
        predictionsDf.columns

    <span data-ttu-id="5e0a0-212">Hier ziet u uitvoer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="5e0a0-212">You should see an output like hello following:</span></span>

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
1. <span data-ttu-id="5e0a0-213">Bekijk een Hallo voorspellingen.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-213">Look at one of hello predictions.</span></span> <span data-ttu-id="5e0a0-214">In dit fragment uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5e0a0-214">Run this snippet:</span></span>

        predictionsDf.take(1)

   <span data-ttu-id="5e0a0-215">Er is een voorspelling voor Hallo eerste item in de gegevensset Hallo-test.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-215">There is a prediction for hello first entry in hello test data set.</span></span>
1. <span data-ttu-id="5e0a0-216">Hallo `model.transform()` methode toepassing hello dezelfde transformatie tooany nieuwe gegevens met Hallo van hetzelfde schema en een voorspelling van hoe tooclassify Hallo gegevens aankomen.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-216">hello `model.transform()` method applies hello same transformation tooany new data with hello same schema, and arrive at a prediction of how tooclassify hello data.</span></span> <span data-ttu-id="5e0a0-217">Wij kunnen enkele eenvoudige statistieken tooget nu een beeld van hoe nauwkeurig onze voorspellingen zijn:</span><span class="sxs-lookup"><span data-stu-id="5e0a0-217">We can do some simple statistics tooget a sense of how accurate our predictions were:</span></span>

        numSuccesses = predictionsDf.where("""(prediction = 0 AND results = 'Fail') OR
                                              (prediction = 1 AND (results = 'Pass' OR
                                                                   results = 'Pass w/ Conditions'))""").count()
        numInspections = predictionsDf.count()

        print "There were", numInspections, "inspections and there were", numSuccesses, "successful predictions"
        print "This is a", str((float(numSuccesses) / float(numInspections)) * 100) + "%", "success rate"

    <span data-ttu-id="5e0a0-218">Hallo-uitvoer ziet er Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="5e0a0-218">hello output looks like hello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        There were 9315 inspections and there were 8087 successful predictions
        This is a 86.8169618894% success rate

    <span data-ttu-id="5e0a0-219">Met behulp van logistic regression met Spark biedt ons een nauwkeurige model van Hallo relatie tussen schendingen beschrijvingen in het Engels en een opgegeven bedrijf zou doorgeven of afbreken van een voeding inspectie.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-219">Using logistic regression with Spark gives us an accurate model of hello relationship between violations descriptions in English and whether a given business would pass or fail a food inspection.</span></span>

## <a name="create-a-visual-representation-of-hello-prediction"></a><span data-ttu-id="5e0a0-220">Een visuele representatie van Hallo voorspelling maken</span><span class="sxs-lookup"><span data-stu-id="5e0a0-220">Create a visual representation of hello prediction</span></span>
<span data-ttu-id="5e0a0-221">We kunt nu een definitieve visualisatie toohelp die ons over Hallo resultaten van deze test reden opstellen.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-221">We can now construct a final visualization toohelp us reason about hello results of this test.</span></span>

1. <span data-ttu-id="5e0a0-222">Begin met het uitpakken van de verschillende voorspellingen Hallo en resultaten van Hallo **voorspellingen** tijdelijke tabel die eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-222">We start by extracting hello different predictions and results from hello **Predictions** temporary table created earlier.</span></span> <span data-ttu-id="5e0a0-223">Hallo volgende query's scheiden Hallo uitvoer als *true_positive*, *false_positive*, *true_negative*, en *false_negative*.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-223">hello following queries separate hello output as *true_positive*, *false_positive*, *true_negative*, and *false_negative*.</span></span> <span data-ttu-id="5e0a0-224">Hallo-query's hieronder, we uitschakelen visualisatie met `-q` en Hallo uitvoer ook op te slaan (met behulp van `-o`) als dataframes die vervolgens kunnen worden gebruikt met Hallo `%%local` verwerkt Magic-pakket.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-224">In hello queries below, we turn off visualization by using `-q` and also save hello output (by using `-o`) as dataframes that can be then used with hello `%%local` magic.</span></span>

        %%sql -q -o true_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND results = 'Fail'

        %%sql -q -o false_positive
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 0 AND (results = 'Pass' OR results = 'Pass w/ Conditions')

        %%sql -q -o true_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND results = 'Fail'

        %%sql -q -o false_negative
        SELECT count(*) AS cnt FROM Predictions WHERE prediction = 1 AND (results = 'Pass' OR results = 'Pass w/ Conditions')
1. <span data-ttu-id="5e0a0-225">Gebruik tot slot Hallo volgende codefragment toogenerate Hallo tekent met behulp van **Matplotlib**.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-225">Finally, use hello following snippet toogenerate hello plot using **Matplotlib**.</span></span>

        %%local
        %matplotlib inline
        import matplotlib.pyplot as plt

        labels = ['True positive', 'False positive', 'True negative', 'False negative']
        sizes = [true_positive['cnt'], false_positive['cnt'], false_negative['cnt'], true_negative['cnt']]
        colors = ['turquoise', 'seagreen', 'mediumslateblue', 'palegreen', 'coral']
        plt.pie(sizes, labels=labels, autopct='%1.1f%%', colors=colors)
        plt.axis('equal')

    <span data-ttu-id="5e0a0-226">Hallo volgende uitvoer weergegeven:</span><span class="sxs-lookup"><span data-stu-id="5e0a0-226">You should see hello following output:</span></span>

    <span data-ttu-id="5e0a0-227">![Spark machine learning-uitvoer van de toepassing - cirkeldiagram percentages van mislukte voeding controles. ] (./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark machine learning-resultaat-uitvoer")</span><span class="sxs-lookup"><span data-stu-id="5e0a0-227">![Spark machine learning application output - pie chart percentages of failed food inspections.](./media/hdinsight-apache-spark-machine-learning-mllib-ipython/spark-machine-learning-result-output-2.png "Spark machine learning result output")</span></span>

    <span data-ttu-id="5e0a0-228">In deze grafiek verwijst ' ' positief voeding inspectie van toohello is mislukt, terwijl een negatief resultaat tooa inspectie doorgegeven verwijst.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-228">In this chart, a "positive" result refers toohello failed food inspection, while a negative result refers tooa passed inspection.</span></span>

## <a name="shut-down-hello-notebook"></a><span data-ttu-id="5e0a0-229">Hallo-notebook afsluiten</span><span class="sxs-lookup"><span data-stu-id="5e0a0-229">Shut down hello notebook</span></span>
<span data-ttu-id="5e0a0-230">Nadat u klaar bent met het uitvoeren van de toepassing hello, moet u Hallo notebook toorelease Hallo resources afgesloten.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-230">After you have finished running hello application, you should shut down hello notebook toorelease hello resources.</span></span> <span data-ttu-id="5e0a0-231">toodo geval is, uit Hallo **bestand** menu op Hallo laptop, klikt u op **sluiten en stoppen**.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-231">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="5e0a0-232">Dit wordt afgesloten en wordt gesloten Hallo notebook.</span><span class="sxs-lookup"><span data-stu-id="5e0a0-232">This shuts down and closes hello notebook.</span></span>

## <span data-ttu-id="5e0a0-233"><a name="seealso"></a>Zie ook</span><span class="sxs-lookup"><span data-stu-id="5e0a0-233"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="5e0a0-234">Overzicht: Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5e0a0-234">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="5e0a0-235">Scenario's</span><span class="sxs-lookup"><span data-stu-id="5e0a0-235">Scenarios</span></span>
* [<span data-ttu-id="5e0a0-236">Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools</span><span class="sxs-lookup"><span data-stu-id="5e0a0-236">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="5e0a0-237">Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens</span><span class="sxs-lookup"><span data-stu-id="5e0a0-237">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="5e0a0-238">Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen</span><span class="sxs-lookup"><span data-stu-id="5e0a0-238">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="5e0a0-239">Websitelogboekanalyse met Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5e0a0-239">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="5e0a0-240">Toepassingen maken en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="5e0a0-240">Create and run applications</span></span>
* [<span data-ttu-id="5e0a0-241">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="5e0a0-241">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="5e0a0-242">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="5e0a0-242">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="5e0a0-243">Tools en uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="5e0a0-243">Tools and extensions</span></span>
* [<span data-ttu-id="5e0a0-244">De invoegtoepassing HDInsight Tools voor IntelliJ IDEA toocreate en verzenden van Spark Scala-toepassingen</span><span class="sxs-lookup"><span data-stu-id="5e0a0-244">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="5e0a0-245">De invoegtoepassing HDInsight Tools for IntelliJ IDEA toodebug Spark applications op afstand gebruiken</span><span class="sxs-lookup"><span data-stu-id="5e0a0-245">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="5e0a0-246">Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5e0a0-246">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="5e0a0-247">Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="5e0a0-247">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="5e0a0-248">Externe pakketten gebruiken met Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="5e0a0-248">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="5e0a0-249">Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="5e0a0-249">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="5e0a0-250">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="5e0a0-250">Manage resources</span></span>
* [<span data-ttu-id="5e0a0-251">Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5e0a0-251">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="5e0a0-252">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="5e0a0-252">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
