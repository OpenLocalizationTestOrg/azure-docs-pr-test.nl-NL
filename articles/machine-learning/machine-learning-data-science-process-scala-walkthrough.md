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
# <a name="data-science-using-scala-and-spark-on-azure"></a><span data-ttu-id="d3e4a-103">Gegevenswetenschap met Scala en Spark op Azure</span><span class="sxs-lookup"><span data-stu-id="d3e4a-103">Data Science using Scala and Spark on Azure</span></span>
<span data-ttu-id="d3e4a-104">Dit artikel laat zien hoe toouse Scala voor bewaakte machine learning taken met Hallo Spark schaalbare MLlib en Spark ML-pakketten in een Azure HDInsight Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-104">This article shows you how toouse Scala for supervised machine learning tasks with hello Spark scalable MLlib and Spark ML packages on an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="d3e4a-105">Het wordt u begeleid bij Hallo-taken die deel uitmaken van Hallo [proces voor Gegevenswetenschap](http://aka.ms/datascienceprocess): gegevensopname en verkennen, visualisatie, functie-engineering, modellering en model verbruik.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-105">It walks you through hello tasks that constitute hello [Data Science process](http://aka.ms/datascienceprocess): data ingestion and exploration, visualization, feature engineering, modeling, and model consumption.</span></span> <span data-ttu-id="d3e4a-106">Hallo-modellen in Hallo artikel logistic en lineaire regressie, willekeurige forests en verloop boosted structuren (GBTs) omvatten, maar daarnaast tootwo gemeenschappelijke onder supervisie machine learning taken:</span><span class="sxs-lookup"><span data-stu-id="d3e4a-106">hello models in hello article include logistic and linear regression, random forests, and gradient-boosted trees (GBTs), in addition tootwo common supervised machine learning tasks:</span></span>

* <span data-ttu-id="d3e4a-107">Regressie probleem: voorspelling van Hallo tip bedrag ($) voor een reis taxi</span><span class="sxs-lookup"><span data-stu-id="d3e4a-107">Regression problem: Prediction of hello tip amount ($) for a taxi trip</span></span>
* <span data-ttu-id="d3e4a-108">Binaire classificatie: voorspelling van tip of geen tip (1/0) voor een reis taxi</span><span class="sxs-lookup"><span data-stu-id="d3e4a-108">Binary classification: Prediction of tip or no tip (1/0) for a taxi trip</span></span>

<span data-ttu-id="d3e4a-109">Hallo modelleren proces is vereist voor trainings- en evaluatie van een testgegevensset en relevante nauwkeurigheid metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-109">hello modeling process requires training and evaluation on a test data set and relevant accuracy metrics.</span></span> <span data-ttu-id="d3e4a-110">In dit artikel leert u hoe toostore deze modellen Azure Blob storage en hoe tooscore en evalueren hun voorspellende prestaties.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-110">In this article, you can learn how toostore these models in Azure Blob storage and how tooscore and evaluate their predictive performance.</span></span> <span data-ttu-id="d3e4a-111">In dit artikel omvat tevens Hallo geavanceerdere onderwerpen van hoe toooptimize modellen met behulp van sweeping kruisvalidatie en hyper-parameter.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-111">This article also covers hello more advanced topics of how toooptimize models by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="d3e4a-112">Hallo-gegevens die worden gebruikt, is een voorbeeld van Hallo 2013 NYC taxi reis en tarief gegevensset beschikbaar op GitHub.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-112">hello data used is a sample of hello 2013 NYC taxi trip and fare data set available on GitHub.</span></span>

<span data-ttu-id="d3e4a-113">[Scala](http://www.scala-lang.org/), een taal die op basis van Hallo virtuele Java-machine, objectgeoriënteerd en functionele Taalconcepten integreert.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-113">[Scala](http://www.scala-lang.org/), a language based on hello Java virtual machine, integrates object-oriented and functional language concepts.</span></span> <span data-ttu-id="d3e4a-114">Het is een schaalbare taal die geschikt toodistributed worden verwerkt in de cloud Hallo en wordt uitgevoerd op Azure Spark-clusters.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-114">It's a scalable language that is well suited toodistributed processing in hello cloud, and runs on Azure Spark clusters.</span></span>

<span data-ttu-id="d3e4a-115">[Spark](http://spark.apache.org/) is een open source parallelle verwerking framework die ondersteuning biedt voor in-memory verwerking tooboost Hallo prestaties van toepassingen voor big data-analyses.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-115">[Spark](http://spark.apache.org/) is an open-source parallel-processing framework that supports in-memory processing tooboost hello performance of big data analytics applications.</span></span> <span data-ttu-id="d3e4a-116">Hallo Spark-verwerkingsengine is gebouwd voor snelheid, gebruiksgemak en geavanceerde analyses.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-116">hello Spark processing engine is built for speed, ease of use, and sophisticated analytics.</span></span> <span data-ttu-id="d3e4a-117">De Spark in-memory gedistribueerde rekencapaciteiten kunnen u een goede keuze voor zich herhalende algoritmen in machine learning- en grafiekberekeningen.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-117">Spark's in-memory distributed computation capabilities make it a good choice for iterative algorithms in machine learning and graph computations.</span></span> <span data-ttu-id="d3e4a-118">Hallo [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) pakket biedt een uniforme set op hoog niveau API's die zijn gebouwd op gegevens frames waarmee u kunnen maken en praktische machine learning-pijplijnen afstemmen.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-118">hello [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) package provides a uniform set of high-level APIs built on top of data frames that can help you create and tune practical machine learning pipelines.</span></span> <span data-ttu-id="d3e4a-119">[MLlib](http://spark.apache.org/mllib/) is Spark van schaalbare machine learning-bibliotheek, dat het modellering mogelijkheden toothis gedistribueerde omgeving.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-119">[MLlib](http://spark.apache.org/mllib/) is Spark's scalable machine learning library, which brings modeling capabilities toothis distributed environment.</span></span>

<span data-ttu-id="d3e4a-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) hello Azure gehoste aanbod van open-source Spark is.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) is hello Azure-hosted offering of open-source Spark.</span></span> <span data-ttu-id="d3e4a-121">Dit omvat ook ondersteuning voor Jupyter Scala notitieblokken op Hallo Spark-cluster, en kunt uitvoeren Spark SQL-tootransform in interactieve query's filteren en opgeslagen in Azure Blob storage-gegevens visualiseren.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-121">It also includes support for Jupyter Scala notebooks on hello Spark cluster, and can run Spark SQL interactive queries tootransform, filter, and visualize data stored in Azure Blob storage.</span></span> <span data-ttu-id="d3e4a-122">Hallo Scala codefragmenten in dit artikel die Hallo-oplossingen bieden en de relevante waarnemingspunten Hallo toovisualize Hallo gegevens weergeven in Jupyter-notebooks geïnstalleerd op Hallo Spark-clusters worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-122">hello Scala code snippets in this article that provide hello solutions and show hello relevant plots toovisualize hello data run in Jupyter notebooks installed on hello Spark clusters.</span></span> <span data-ttu-id="d3e4a-123">Hallo modellering stappen in deze onderwerpen hebben die toont u hoe tootrain, evalueren, opslaan en gebruiken ieder soort model code.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-123">hello modeling steps in these topics have code that shows you how tootrain, evaluate, save, and consume each type of model.</span></span>

<span data-ttu-id="d3e4a-124">Hallo installatiestappen en code in dit artikel zijn voor Azure HDInsight 3.4 Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-124">hello setup steps and code in this article are for Azure HDInsight 3.4 Spark 1.6.</span></span> <span data-ttu-id="d3e4a-125">Hallo echter code in dit artikel en Hallo [Scala Jupyter-Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) algemeen zijn en moet werken op een Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-125">However, hello code in this article and in hello [Scala Jupyter Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) are generic and should work on any Spark cluster.</span></span> <span data-ttu-id="d3e4a-126">Hallo clusterinstallatie en management stappen mogelijk enigszins afwijken van wat wordt weergegeven in dit artikel als u geen van HDInsight Spark gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-126">hello cluster setup and management steps might be slightly different from what is shown in this article if you are not using HDInsight Spark.</span></span>

> [!NOTE]
> <span data-ttu-id="d3e4a-127">Zie voor een onderwerp dat toont hoe toouse Python in plaats van Scala toocomplete taken voor een end-to-end-proces voor Gegevenswetenschap [Gegevenswetenschap met Spark op Azure HDInsight](machine-learning-data-science-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d3e4a-127">For a topic that shows you how toouse Python rather than Scala toocomplete tasks for an end-to-end Data Science process, see [Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="d3e4a-128">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d3e4a-128">Prerequisites</span></span>
* <span data-ttu-id="d3e4a-129">U moet een Azure-abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-129">You must have an Azure subscription.</span></span> <span data-ttu-id="d3e4a-130">Als u geen hebt nog, [ophalen van een gratis proefversie van Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="d3e4a-130">If you do not already have one, [get an Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="d3e4a-131">U moet een Azure HDInsight 3.4 Spark 1.6 cluster toocomplete Hallo procedures te volgen.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-131">You need an Azure HDInsight 3.4 Spark 1.6 cluster toocomplete hello following procedures.</span></span> <span data-ttu-id="d3e4a-132">toocreate een cluster, Zie de instructies Hallo in [aan de slag: Apache Spark maken in Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="d3e4a-132">toocreate a cluster, see hello instructions in [Get started: Create Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="d3e4a-133">Hallo-clustertype en -versie instellen op Hallo **clustertype Selecteer** menu.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-133">Set hello cluster type and version on hello **Select Cluster Type** menu.</span></span>

![Configuratie van het HDInsight-cluster](./media/machine-learning-data-science-process-scala-walkthrough/spark-cluster-on-portal.png)

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

<span data-ttu-id="d3e4a-135">Zie voor een beschrijving van Hallo NYC taxi reis gegevens en instructies over hoe tooexecute code van een Jupyter-notebook in Spark-cluster Hallo Hallo relevante secties in [overzicht van Gegevenswetenschap met Spark op Azure HDInsight](machine-learning-data-science-spark-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d3e4a-135">For a description of hello NYC taxi trip data and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster, see hello relevant sections in [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>  

## <a name="execute-scala-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a><span data-ttu-id="d3e4a-136">Scala code uitvoeren van een Jupyter-notebook in Spark-cluster Hallo</span><span class="sxs-lookup"><span data-stu-id="d3e4a-136">Execute Scala code from a Jupyter notebook on hello Spark cluster</span></span>
<span data-ttu-id="d3e4a-137">U kunt een Jupyter-notebook van hello Azure-portal op te starten.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-137">You can launch a Jupyter notebook from hello Azure portal.</span></span> <span data-ttu-id="d3e4a-138">Hallo Spark-cluster op uw dashboard zoeken en klik vervolgens op het tooenter Hallo management-pagina voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-138">Find hello Spark cluster on your dashboard, and then click it tooenter hello management page for your cluster.</span></span> <span data-ttu-id="d3e4a-139">Klik vervolgens op **Clusterdashboards**, en klik vervolgens op **Jupyter-Notebook** tooopen Hallo laptop die is gekoppeld aan Hallo Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-139">Next, click **Cluster Dashboards**, and then click **Jupyter Notebook** tooopen hello notebook associated with hello Spark cluster.</span></span>

![Cluster-dashboard en de Jupyter-notebooks](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-on-portal.png)

<span data-ttu-id="d3e4a-141">U ook toegang tot Jupyter-notebooks op https://&lt;clustername&gt;.azurehdinsight.net/jupyter.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-141">You also can access Jupyter notebooks at https://&lt;clustername&gt;.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="d3e4a-142">Vervang *clustername* met Hallo-naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-142">Replace *clustername* with hello name of your cluster.</span></span> <span data-ttu-id="d3e4a-143">Hallo-wachtwoord moet u voor uw administrator-account tooaccess hello Jupyter-notebooks.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-143">You need hello password for your administrator account tooaccess hello Jupyter notebooks.</span></span>

![Ga tooJupyter laptops met behulp van de clusternaam Hallo](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-notebook.png)

<span data-ttu-id="d3e4a-145">Selecteer **Scala** toosee een map met een paar voorbeelden van voorverpakte laptops die gebruik Hallo PySpark-API.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-145">Select **Scala** toosee a directory that has a few examples of prepackaged notebooks that use hello PySpark API.</span></span> <span data-ttu-id="d3e4a-146">Hallo exploratie modelleren en score Scala.ipynb laptop die Hallo-codevoorbeelden bevat voor dit pakket van Spark onderwerpen vindt u op met [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span><span class="sxs-lookup"><span data-stu-id="d3e4a-146">hello Exploration Modeling and Scoring using Scala.ipynb notebook that contains hello code samples for this suite of Spark topics is available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span></span>

<span data-ttu-id="d3e4a-147">U kunt Hallo notebook rechtstreeks vanuit GitHub toohello Jupyter-Notebook server uploaden in uw Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-147">You can upload hello notebook directly from GitHub toohello Jupyter Notebook server on your Spark cluster.</span></span> <span data-ttu-id="d3e4a-148">Klik op uw startpagina Jupyter hello **uploaden** knop.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-148">On your Jupyter home page, click hello **Upload** button.</span></span> <span data-ttu-id="d3e4a-149">Plak de URL van GitHub (onbewerkte inhoud) Hallo van Hallo Scala laptop in Verkenner hello, en klik vervolgens op **Open**.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-149">In hello file explorer, paste hello GitHub (raw content) URL of hello Scala notebook, and then click **Open**.</span></span> <span data-ttu-id="d3e4a-150">Hallo Scala notebook is beschikbaar op Hallo URL te volgen:</span><span class="sxs-lookup"><span data-stu-id="d3e4a-150">hello Scala notebook is available at hello following URL:</span></span>

[<span data-ttu-id="d3e4a-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span><span class="sxs-lookup"><span data-stu-id="d3e4a-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span></span>](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration-Modeling-and-Scoring-using-Scala.ipynb)

## <a name="setup-preset-spark-and-hive-contexts-spark-magics-and-spark-libraries"></a><span data-ttu-id="d3e4a-152">Instellen: Voorinstelling Spark en Hive-contexten, Spark magics en Spark bibliotheken</span><span class="sxs-lookup"><span data-stu-id="d3e4a-152">Setup: Preset Spark and Hive contexts, Spark magics, and Spark libraries</span></span>
### <a name="preset-spark-and-hive-contexts"></a><span data-ttu-id="d3e4a-153">Vooraf ingestelde Spark en Hive-contexten</span><span class="sxs-lookup"><span data-stu-id="d3e4a-153">Preset Spark and Hive contexts</span></span>
    # SET hello START TIME
    import java.util.Calendar
    val beginningTime = Calendar.getInstance().getTime()


<span data-ttu-id="d3e4a-154">Hallo Spark kernels die worden geleverd met Jupyter-notebooks hebben vooraf ingestelde contexten.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-154">hello Spark kernels that are provided with Jupyter notebooks have preset contexts.</span></span> <span data-ttu-id="d3e4a-155">U hoeft niet tooexplicitly set Hallo Spark of Hive-contexten voordat u begint te werken met Hallo-toepassing die u ontwikkelt.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-155">You don't need tooexplicitly set hello Spark or Hive contexts before you start working with hello application you are developing.</span></span> <span data-ttu-id="d3e4a-156">Hallo vooraf ingestelde contexten is zijn:</span><span class="sxs-lookup"><span data-stu-id="d3e4a-156">hello preset contexts are:</span></span>

* <span data-ttu-id="d3e4a-157">`sc`voor SparkContext</span><span class="sxs-lookup"><span data-stu-id="d3e4a-157">`sc` for SparkContext</span></span>
* <span data-ttu-id="d3e4a-158">`sqlContext`voor HiveContext</span><span class="sxs-lookup"><span data-stu-id="d3e4a-158">`sqlContext` for HiveContext</span></span>

### <a name="spark-magics"></a><span data-ttu-id="d3e4a-159">Spark magics</span><span class="sxs-lookup"><span data-stu-id="d3e4a-159">Spark magics</span></span>
<span data-ttu-id="d3e4a-160">Hallo Spark kernel biedt een aantal vooraf gedefinieerde 'magics', die zijn speciale opdrachten die u met aanroepen kunt `%%`.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-160">hello Spark kernel provides some predefined “magics,” which are special commands that you can call with `%%`.</span></span> <span data-ttu-id="d3e4a-161">Twee van deze opdrachten worden gebruikt in de volgende codevoorbeelden Hallo.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-161">Two of these commands are used in hello following code samples.</span></span>

* <span data-ttu-id="d3e4a-162">`%%local`Hiermee geeft u op dat Hallo-code in de volgende regels lokaal worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-162">`%%local` specifies that hello code in subsequent lines will be executed locally.</span></span> <span data-ttu-id="d3e4a-163">Hallo-code moet geldige Scala-code.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-163">hello code must be valid Scala code.</span></span>
* <span data-ttu-id="d3e4a-164">`%%sql -o <variable name>`voert een Hive-query op `sqlContext`.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-164">`%%sql -o <variable name>` executes a Hive query against `sqlContext`.</span></span> <span data-ttu-id="d3e4a-165">Als hello `-o` parameter is doorgegeven, Hallo resultaat van Hallo query wordt bewaard in Hallo `%%local` Scala context als een tijdskader Spark-gegevens.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-165">If hello `-o` parameter is passed, hello result of hello query is persisted in hello `%%local` Scala context as a Spark data frame.</span></span>

<span data-ttu-id="d3e4a-166">Voor meer informatie over Hallo kernels voor Jupyter-notebooks en hun vooraf gedefinieerde 'magics' die u aanroept met `%%` (bijvoorbeeld `%%local`), Zie [beschikbare Kernels voor Jupyter-notebooks met HDInsight Spark Linux-clusters op HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="d3e4a-166">For more information about hello kernels for Jupyter notebooks and their predefined "magics" that you call with `%%` (for example, `%%local`), see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

### <a name="import-libraries"></a><span data-ttu-id="d3e4a-167">Bibliotheken importeren</span><span class="sxs-lookup"><span data-stu-id="d3e4a-167">Import libraries</span></span>
<span data-ttu-id="d3e4a-168">Hallo Spark, MLlib en andere bibliotheken die u met behulp van de volgende code Hallo moet importeren.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-168">Import hello Spark, MLlib, and other libraries you'll need by using hello following code.</span></span>

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


## <a name="data-ingestion"></a><span data-ttu-id="d3e4a-169">Gegevensopname</span><span class="sxs-lookup"><span data-stu-id="d3e4a-169">Data ingestion</span></span>
<span data-ttu-id="d3e4a-170">Hallo eerste stap bij het proces voor Gegevenswetenschap hello is tooingest Hallo gegevens die u wilt dat tooanalyze.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-170">hello first step in hello Data Science process is tooingest hello data that you want tooanalyze.</span></span> <span data-ttu-id="d3e4a-171">U brengt Hallo gegevens van externe bronnen of systemen waarin deze zich bevindt in uw gegevens te verkennen en modellering omgeving.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-171">You bring hello data from external sources or systems where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="d3e4a-172">In dit artikel is Hallo-gegevens die u wilt opnemen een gekoppelde 0,1% voorbeeld van Hallo taxi reis en tarief bestand (opgeslagen als een bestand .tsv).</span><span class="sxs-lookup"><span data-stu-id="d3e4a-172">In this article, hello data you ingest is a joined 0.1% sample of hello taxi trip and fare file (stored as a .tsv file).</span></span> <span data-ttu-id="d3e4a-173">Hallo-gegevens te verkennen en modellering-omgeving is Spark.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-173">hello data exploration and modeling environment is Spark.</span></span> <span data-ttu-id="d3e4a-174">Deze sectie bevat Hallo code toocomplete Hallo reeks taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="d3e4a-174">This section contains hello code toocomplete hello following series of tasks:</span></span>

1. <span data-ttu-id="d3e4a-175">Instellen van directory-paden voor opslag van gegevens en het model.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-175">Set directory paths for data and model storage.</span></span>
2. <span data-ttu-id="d3e4a-176">Lees in Hallo invoer gegevensset (opgeslagen als een bestand .tsv).</span><span class="sxs-lookup"><span data-stu-id="d3e4a-176">Read in hello input data set (stored as a .tsv file).</span></span>
3. <span data-ttu-id="d3e4a-177">Een schema voor Hallo en schone Hallo gegevens definiëren.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-177">Define a schema for hello data and clean hello data.</span></span>
4. <span data-ttu-id="d3e4a-178">Een kader opgeschoonde gegevens maken en deze in de cache in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-178">Create a cleaned data frame and cache it in memory.</span></span>
5. <span data-ttu-id="d3e4a-179">Hallo-gegevens als een tijdelijke tabel in SQLContext registreren.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-179">Register hello data as a temporary table in SQLContext.</span></span>
6. <span data-ttu-id="d3e4a-180">Hallo querytabel en Hallo resultaten in een gegevensframe importeren.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-180">Query hello table and import hello results into a data frame.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-azure-blob-storage"></a><span data-ttu-id="d3e4a-181">Directory-paden voor opslaglocaties in Azure Blob-opslag instellen</span><span class="sxs-lookup"><span data-stu-id="d3e4a-181">Set directory paths for storage locations in Azure Blob storage</span></span>
<span data-ttu-id="d3e4a-182">Spark kunt lezen en schrijven tooAzure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-182">Spark can read and write tooAzure Blob storage.</span></span> <span data-ttu-id="d3e4a-183">U kunt een van uw bestaande gegevens Spark tooprocess gebruiken en resultaten op te slaan Hallo opnieuw in de Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-183">You can use Spark tooprocess any of your existing data, and then store hello results again in Blob storage.</span></span>

<span data-ttu-id="d3e4a-184">toosave modellen of bestanden in Blob storage, moet u tooproperly Hallo pad opgeven.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-184">toosave models or files in Blob storage, you need tooproperly specify hello path.</span></span> <span data-ttu-id="d3e4a-185">Verwijzing Hallo standaardcontainer toohello Spark-cluster aangesloten via een pad dat met begint `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-185">Reference hello default container attached toohello Spark cluster by using a path that begins with `wasb:///`.</span></span> <span data-ttu-id="d3e4a-186">Verwijzen naar andere locaties met behulp van `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-186">Reference other locations by using `wasb://`.</span></span>

<span data-ttu-id="d3e4a-187">Hallo geeft volgende codevoorbeeld locatie van de Hallo Hallo invoergegevens toobe lezen en Hallo pad tooBlob opslag die is aangesloten toohello Spark-cluster waarin Hallo model moet worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-187">hello following code sample specifies hello location of hello input data toobe read and hello path tooBlob storage that is attached toohello Spark cluster where hello model will be saved.</span></span>

    # SET PATHS tooDATA AND MODEL FILE LOCATIONS
    # INGEST DATA AND SPECIFY HEADERS FOR COLUMNS
    val taxi_train_file = sc.textFile("wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv")
    val header = taxi_train_file.first;

    # SET hello MODEL STORAGE DIRECTORY PATH
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS REQUIRED.
    val modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";


### <a name="import-data-create-an-rdd-and-define-a-data-frame-according-toohello-schema"></a><span data-ttu-id="d3e4a-188">Gegevens importeren, maakt u een RDD en een gegevensframe volgens toohello schema definiëren</span><span class="sxs-lookup"><span data-stu-id="d3e4a-188">Import data, create an RDD, and define a data frame according toohello schema</span></span>
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


<span data-ttu-id="d3e4a-189">**Uitvoer:**</span><span class="sxs-lookup"><span data-stu-id="d3e4a-189">**Output:**</span></span>

<span data-ttu-id="d3e4a-190">Tijd toorun Hallo cel: 8 seconden.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-190">Time toorun hello cell: 8 seconds.</span></span>

### <a name="query-hello-table-and-import-results-in-a-data-frame"></a><span data-ttu-id="d3e4a-191">Hallo querytabel en resulteert in een gegevensframe importeren</span><span class="sxs-lookup"><span data-stu-id="d3e4a-191">Query hello table and import results in a data frame</span></span>
<span data-ttu-id="d3e4a-192">Vervolgens Hallo querytabel voor tarief, passagiers en tip gegevens; de gegevens beschadigd en afgelegen; uitfilteren en afdrukken van meerdere rijen.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-192">Next, query hello table for fare, passenger, and tip data; filter out corrupt and outlying data; and print several rows.</span></span>

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

<span data-ttu-id="d3e4a-193">**Uitvoer:**</span><span class="sxs-lookup"><span data-stu-id="d3e4a-193">**Output:**</span></span>

| <span data-ttu-id="d3e4a-194">fare_amount</span><span class="sxs-lookup"><span data-stu-id="d3e4a-194">fare_amount</span></span> | <span data-ttu-id="d3e4a-195">passenger_count</span><span class="sxs-lookup"><span data-stu-id="d3e4a-195">passenger_count</span></span> | <span data-ttu-id="d3e4a-196">tip_amount</span><span class="sxs-lookup"><span data-stu-id="d3e4a-196">tip_amount</span></span> | <span data-ttu-id="d3e4a-197">punt</span><span class="sxs-lookup"><span data-stu-id="d3e4a-197">tipped</span></span> |
| --- | --- | --- | --- |
|        <span data-ttu-id="d3e4a-198">13.5</span><span class="sxs-lookup"><span data-stu-id="d3e4a-198">13.5</span></span> |<span data-ttu-id="d3e4a-199">1.0</span><span class="sxs-lookup"><span data-stu-id="d3e4a-199">1.0</span></span> |<span data-ttu-id="d3e4a-200">2.9</span><span class="sxs-lookup"><span data-stu-id="d3e4a-200">2.9</span></span> |<span data-ttu-id="d3e4a-201">1.0</span><span class="sxs-lookup"><span data-stu-id="d3e4a-201">1.0</span></span> |
|        <span data-ttu-id="d3e4a-202">16.0</span><span class="sxs-lookup"><span data-stu-id="d3e4a-202">16.0</span></span> |<span data-ttu-id="d3e4a-203">2.0</span><span class="sxs-lookup"><span data-stu-id="d3e4a-203">2.0</span></span> |<span data-ttu-id="d3e4a-204">3.4</span><span class="sxs-lookup"><span data-stu-id="d3e4a-204">3.4</span></span> |<span data-ttu-id="d3e4a-205">1.0</span><span class="sxs-lookup"><span data-stu-id="d3e4a-205">1.0</span></span> |
|        <span data-ttu-id="d3e4a-206">10.5</span><span class="sxs-lookup"><span data-stu-id="d3e4a-206">10.5</span></span> |<span data-ttu-id="d3e4a-207">2.0</span><span class="sxs-lookup"><span data-stu-id="d3e4a-207">2.0</span></span> |<span data-ttu-id="d3e4a-208">1.0</span><span class="sxs-lookup"><span data-stu-id="d3e4a-208">1.0</span></span> |<span data-ttu-id="d3e4a-209">1.0</span><span class="sxs-lookup"><span data-stu-id="d3e4a-209">1.0</span></span> |

## <a name="data-exploration-and-visualization"></a><span data-ttu-id="d3e4a-210">Gegevensverkenning en visualisatie</span><span class="sxs-lookup"><span data-stu-id="d3e4a-210">Data exploration and visualization</span></span>
<span data-ttu-id="d3e4a-211">Nadat u Hallo gegevens naar Spark overbrengen, is de volgende stap Hallo in Hallo proces voor Gegevenswetenschap toogain een beter begrip van gegevens via de exploratie en visualisatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-211">After you bring hello data into Spark, hello next step in hello Data Science process is toogain a deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="d3e4a-212">In deze sectie kunt u Hallo taxi gegevens controleren met behulp van SQL-query's.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-212">In this section, you examine hello taxi data by using SQL queries.</span></span> <span data-ttu-id="d3e4a-213">Resultaten van importbewerking Hallo in een frame gegevens tooplot Hallo vervolgens target-variabelen en potentiële functies voor visuele inspectie met Hallo automatisch visualisatie functie van Jupyter.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-213">Then, import hello results into a data frame tooplot hello target variables and prospective features for visual inspection by using hello auto-visualization feature of Jupyter.</span></span>

### <a name="use-local-and-sql-magic-tooplot-data"></a><span data-ttu-id="d3e4a-214">Lokale en SQL-magic tooplot gegevens gebruiken</span><span class="sxs-lookup"><span data-stu-id="d3e4a-214">Use local and SQL magic tooplot data</span></span>
<span data-ttu-id="d3e4a-215">Hallo-uitvoer van een codefragment die u vanaf een Jupyter-notebook uitvoert is standaard beschikbaar in de context Hallo van Hallo-sessie die is opgeslagen op Hallo worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-215">By default, hello output of any code snippet that you run from a Jupyter notebook is available within hello context of hello session that is persisted on hello worker nodes.</span></span> <span data-ttu-id="d3e4a-216">Als u toosave een reis toohello worker-knooppunten voor elke berekeningen wilt, en als alle gegevens die u nodig hebt voor de berekening lokaal beschikbaar op Hallo Jupyter-knooppunt is (dit is het hoofdknooppunt Hallo) hello, kunt u Hallo `%%local` magic toorun Hallo code codefragment op Hallo Jupyter-server.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-216">If you want toosave a trip toohello worker nodes for every computation, and if all hello data that you need for your computation is available locally on hello Jupyter server node (which is hello head node), you can use hello `%%local` magic toorun hello code snippet on hello Jupyter server.</span></span>

* <span data-ttu-id="d3e4a-217">**SQL-magic** (`%%sql`).</span><span class="sxs-lookup"><span data-stu-id="d3e4a-217">**SQL magic** (`%%sql`).</span></span> <span data-ttu-id="d3e4a-218">Hallo HDInsight Spark kernel ondersteunt eenvoudig inline HiveQL query's op SQLContext.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-218">hello HDInsight Spark kernel supports easy inline HiveQL queries against SQLContext.</span></span> <span data-ttu-id="d3e4a-219">Hallo (`-o VARIABLE_NAME`) argument als een frame Pandas gegevens op Hallo Jupyter server Hallo-uitvoer van de SQL-query Hallo zich blijft voordoen.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-219">hello (`-o VARIABLE_NAME`) argument persists hello output of hello SQL query as a Pandas data frame on hello Jupyter server.</span></span> <span data-ttu-id="d3e4a-220">Dit betekent waarschijnlijk in de lokale modus Hallo beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-220">This means it'll be available in hello local mode.</span></span>
* <span data-ttu-id="d3e4a-221">`%%local`**magic**.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-221">`%%local` **magic**.</span></span> <span data-ttu-id="d3e4a-222">Hallo `%%local` magic Hallo code wordt lokaal uitgevoerd op Hallo Jupyter-server, waarop Hallo hoofdknooppunt van Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-222">hello `%%local` magic runs hello code locally on hello Jupyter server, which is hello head node of hello HDInsight cluster.</span></span> <span data-ttu-id="d3e4a-223">Normaal gesproken gebruikt u `%%local` magische in combinatie met Hallo `%%sql` magische Hello `-o` parameter.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-223">Typically, you use `%%local` magic in conjunction with hello `%%sql` magic with hello `-o` parameter.</span></span> <span data-ttu-id="d3e4a-224">Hallo `-o` parameter Hallo-uitvoer van lokaal Hallo SQL-query wilt behouden en vervolgens `%%local` magic zou de volgende set Hallo van code codefragment toorun lokaal tegen Hallo uitvoer Hallo SQL-query's die lokaal wordt bewaard.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-224">hello `-o` parameter would persist hello output of hello SQL query locally, and then `%%local` magic would trigger hello next set of code snippet toorun locally against hello output of hello SQL queries that is persisted locally.</span></span>

### <a name="query-hello-data-by-using-sql"></a><span data-ttu-id="d3e4a-225">Hallo gegevens opvragen met behulp van SQL</span><span class="sxs-lookup"><span data-stu-id="d3e4a-225">Query hello data by using SQL</span></span>
<span data-ttu-id="d3e4a-226">Deze query haalt Hallo taxi reizen door tarief, passagiers aantal, en de tip.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-226">This query retrieves hello taxi trips by fare amount, passenger count, and tip amount.</span></span>

    # RUN hello SQL QUERY
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped FROM taxi_train WHERE passenger_count > 0 AND passenger_count < 7 AND fare_amount > 0 AND fare_amount < 200 AND payment_type in ('CSH', 'CRD') AND tip_amount > 0 AND tip_amount < 25

<span data-ttu-id="d3e4a-227">Hallo in Hallo code te volgen, `%%local` magic lokale gegevensframe sqlResults maakt.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-227">In hello following code, hello `%%local` magic creates a local data frame, sqlResults.</span></span> <span data-ttu-id="d3e4a-228">U kunt sqlResults tooplot gebruiken met behulp van matplotlib.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-228">You can use sqlResults tooplot by using matplotlib.</span></span>

> [!TIP]
> <span data-ttu-id="d3e4a-229">Lokale magic wordt meerdere malen gebruikt in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-229">Local magic is used multiple times in this article.</span></span> <span data-ttu-id="d3e4a-230">Als uw gegevensset te groot is, Geef een steekproef nemen uit toocreate een gegevensframe dat in het lokale geheugen past.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-230">If your data set is large, please sample toocreate a data frame that can fit in local memory.</span></span>
> 
> 

### <a name="plot-hello-data"></a><span data-ttu-id="d3e4a-231">Hallo gegevens uitzetten</span><span class="sxs-lookup"><span data-stu-id="d3e4a-231">Plot hello data</span></span>
<span data-ttu-id="d3e4a-232">U kunt met behulp van Python code nadat Hallo gegevensframe in de lokale context als een Pandas gegevensframe is uitzetten.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-232">You can plot by using Python code after hello data frame is in local context as a Pandas data frame.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES.
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, ETC.)
    sqlResults


 <span data-ttu-id="d3e4a-233">Hallo-uitvoer van SQL (HiveQL)-query's visualiseren Hallo Spark kernel automatisch nadat u Hallo code uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-233">hello Spark kernel automatically visualizes hello output of SQL (HiveQL) queries after you run hello code.</span></span> <span data-ttu-id="d3e4a-234">U kunt kiezen tussen verschillende soorten visualisaties:</span><span class="sxs-lookup"><span data-stu-id="d3e4a-234">You can choose between several types of visualizations:</span></span>

* <span data-ttu-id="d3e4a-235">Tabel</span><span class="sxs-lookup"><span data-stu-id="d3e4a-235">Table</span></span>
* <span data-ttu-id="d3e4a-236">Pie</span><span class="sxs-lookup"><span data-stu-id="d3e4a-236">Pie</span></span>
* <span data-ttu-id="d3e4a-237">Regel</span><span class="sxs-lookup"><span data-stu-id="d3e4a-237">Line</span></span>
* <span data-ttu-id="d3e4a-238">Onderwerp</span><span class="sxs-lookup"><span data-stu-id="d3e4a-238">Area</span></span>
* <span data-ttu-id="d3e4a-239">Balk</span><span class="sxs-lookup"><span data-stu-id="d3e4a-239">Bar</span></span>

<span data-ttu-id="d3e4a-240">Hier volgt Hallo code tooplot Hallo gegevens:</span><span class="sxs-lookup"><span data-stu-id="d3e4a-240">Here's hello code tooplot hello data:</span></span>

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


<span data-ttu-id="d3e4a-241">**Uitvoer:**</span><span class="sxs-lookup"><span data-stu-id="d3e4a-241">**Output:**</span></span>

![Tip bedrag histogram](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-histogram.png)

![Hoeveelheid op het aantal passagiers Tip](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-passenger-count.png)

![Tip bedrag door tarief bedrag](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-fare-amount.png)

## <a name="create-features-and-transform-features-and-then-prep-data-for-input-into-modeling-functions"></a><span data-ttu-id="d3e4a-245">Functies maken en functies transformeren en vervolgens voorbereiding-gegevens voor de invoer in het modelleren van functies</span><span class="sxs-lookup"><span data-stu-id="d3e4a-245">Create features and transform features, and then prep data for input into modeling functions</span></span>
<span data-ttu-id="d3e4a-246">Voor functies op basis van een structuur modellering van Spark ML en MLlib hebt u tooprepare doel en functies met behulp van tal van technieken zoals binning indexeren, één hot codering en vectorization.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-246">For tree-based modeling functions from Spark ML and MLlib, you have tooprepare target and features by using a variety of techniques, such as binning, indexing, one-hot encoding, and vectorization.</span></span> <span data-ttu-id="d3e4a-247">Hier volgen Hallo procedures toofollow in deze sectie:</span><span class="sxs-lookup"><span data-stu-id="d3e4a-247">Here are hello procedures toofollow in this section:</span></span>

1. <span data-ttu-id="d3e4a-248">Maak een nieuwe functie door **binning** uren in verkeer tijd buckets.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-248">Create a new feature by **binning** hours into traffic time buckets.</span></span>
2. <span data-ttu-id="d3e4a-249">Van toepassing **indexeren en één hot codering** toocategorical functies.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-249">Apply **indexing and one-hot encoding** toocategorical features.</span></span>
3. <span data-ttu-id="d3e4a-250">**Gesplitste en voorbeelden Hallo gegevensset** in trainings- en testset breuken.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-250">**Sample and split hello data set** into training and test fractions.</span></span>
4. <span data-ttu-id="d3e4a-251">**Geef variabele training en functies**, en vervolgens maken geïndexeerde of op één hot gecodeerd training en testen invoer gelabelde punt flexibele gegevenssets (RDDs) of gegevensframes gedistribueerd.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-251">**Specify training variable and features**, and then create indexed or one-hot encoded training and testing input labeled point resilient distributed datasets (RDDs) or data frames.</span></span>
5. <span data-ttu-id="d3e4a-252">Automatisch **categoriseren en aan functies en doelen vectorize** toouse als invoer voor machine learning-modellen.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-252">Automatically **categorize and vectorize features and targets** toouse as inputs for machine learning models.</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="d3e4a-253">Maakt een nieuwe functie met binning uur in verkeer tijd buckets</span><span class="sxs-lookup"><span data-stu-id="d3e4a-253">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="d3e4a-254">Deze code leest u hoe een nieuwe functie door uren in verkeer tijd binning toocreate tijdsintervallen en hoe toocache Hallo resulterende gegevensframe in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-254">This code shows you how toocreate a new feature by binning hours into traffic time buckets and how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="d3e4a-255">Wanneer gegevens en RDDs frames herhaaldelijk worden gebruikt, leidt opslaan in cache tooimproved uitvoeringstijden.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-255">Where RDDs and data frames are used repeatedly, caching leads tooimproved execution times.</span></span> <span data-ttu-id="d3e4a-256">Dienovereenkomstig, zult u RDDs en gegevens frames cache in verschillende stadia in Hallo procedures te volgen.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-256">Accordingly, you'll cache RDDs and data frames at several stages in hello following procedures.</span></span>

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


### <a name="indexing-and-one-hot-encoding-of-categorical-features"></a><span data-ttu-id="d3e4a-257">Indexeren en één hot codering van categorische functies</span><span class="sxs-lookup"><span data-stu-id="d3e4a-257">Indexing and one-hot encoding of categorical features</span></span>
<span data-ttu-id="d3e4a-258">Hallo modelleren en functies van MLlib hebben functies met categorische invoergegevens toobe geïndexeerd of eerdere toouse gecodeerd voorspellen.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-258">hello modeling and predict functions of MLlib require features with categorical input data toobe indexed or encoded prior toouse.</span></span> <span data-ttu-id="d3e4a-259">Deze sectie leest u hoe tooindex of categorische functies voor invoer in Hallo modelleren functies coderen.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-259">This section shows you how tooindex or encode categorical features for input into hello modeling functions.</span></span>

<span data-ttu-id="d3e4a-260">U moet tooindex of uw modellen coderen op verschillende manieren, afhankelijk van het Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-260">You need tooindex or encode your models in different ways, depending on hello model.</span></span> <span data-ttu-id="d3e4a-261">Logistic en lineaire regressie modellen vereisen bijvoorbeeld dat een hot codering.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-261">For example, logistic and linear regression models require one-hot encoding.</span></span> <span data-ttu-id="d3e4a-262">Bijvoorbeeld, kan een onderdeel met drie categorieën worden uitgebreid naar drie kolommen van de functie.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-262">For example, a feature with three categories can be expanded into three feature columns.</span></span> <span data-ttu-id="d3e4a-263">0 of 1, afhankelijk van de categorie van een observatie Hallo bevat elke kolom.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-263">Each column would contain 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="d3e4a-264">MLlib biedt Hallo [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) functie voor het coderen van één hot.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-264">MLlib provides hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function for one-hot encoding.</span></span> <span data-ttu-id="d3e4a-265">Deze encoder wijst een kolom van een label indexen tooa kolom van de binaire vectoren met maximaal één one-waarde.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-265">This encoder maps a column of label indices tooa column of binary vectors with at most a single one-value.</span></span> <span data-ttu-id="d3e4a-266">Met deze codering kunnen algoritmen die verwacht dat de numerieke waarden functies, zoals logistic regression toegepaste toocategorical functies zijn.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-266">With this encoding, algorithms that expect numerical valued features, such as logistic regression, can be applied toocategorical features.</span></span>

<span data-ttu-id="d3e4a-267">Hier kunt u tekenreeksen voor tooshow-voorbeelden van het slechts vier variabelen transformeren.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-267">Here you transform only four variables tooshow examples, which are character strings.</span></span> <span data-ttu-id="d3e4a-268">U kunt ook andere variabelen, zoals weekdag, vertegenwoordigd door numerieke waarden als categorische variabelen index.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-268">You also can index other variables, such as weekday, represented by numerical values, as categorical variables.</span></span>

<span data-ttu-id="d3e4a-269">Gebruik voor het indexeren, `StringIndexer()`, en gebruiken voor het coderen van één hot, `OneHotEncoder()` functies van MLlib.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-269">For indexing, use `StringIndexer()`, and for one-hot encoding, use `OneHotEncoder()` functions from MLlib.</span></span> <span data-ttu-id="d3e4a-270">Hier volgt Hallo code tooindex en coderen categorische functies:</span><span class="sxs-lookup"><span data-stu-id="d3e4a-270">Here is hello code tooindex and encode categorical features:</span></span>

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


<span data-ttu-id="d3e4a-271">**Uitvoer:**</span><span class="sxs-lookup"><span data-stu-id="d3e4a-271">**Output:**</span></span>

<span data-ttu-id="d3e4a-272">Tijd toorun Hallo cel: 4 seconden.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-272">Time toorun hello cell: 4 seconds.</span></span>

### <a name="sample-and-split-hello-data-set-into-training-and-test-fractions"></a><span data-ttu-id="d3e4a-273">Gesplitste en voorbeelden Hallo gegevensset in trainings- en testset breuken</span><span class="sxs-lookup"><span data-stu-id="d3e4a-273">Sample and split hello data set into training and test fractions</span></span>
<span data-ttu-id="d3e4a-274">Deze code maakt een willekeurige steekproeven van het Hallo-gegevens (in dit voorbeeld 25%).</span><span class="sxs-lookup"><span data-stu-id="d3e4a-274">This code creates a random sampling of hello data (25%, in this example).</span></span> <span data-ttu-id="d3e4a-275">Hoewel steekproeven niet vereist voor dit voorbeeld vanwege toohello grootte van de gegevensset hello is, Hallo artikel ziet u hoe u kunt een steekproef nemen zodat u weet hoe toouse voor uw eigen problemen wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-275">Although sampling is not required for this example due toohello size of hello data set, hello article shows you how you can sample so that you know how toouse it for your own problems when needed.</span></span> <span data-ttu-id="d3e4a-276">Als voorbeelden groot zijn, kan dit aanzienlijke tijd besparen tijdens het trainen van modellen.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-276">When samples are large, this can save significant time while you train models.</span></span> <span data-ttu-id="d3e4a-277">Vervolgens Hallo voorbeeld splitsen in trainings-onderdeel (in dit voorbeeld 75%) en een testen deel toouse in classificatie en regressie modellering (in dit voorbeeld 25%).</span><span class="sxs-lookup"><span data-stu-id="d3e4a-277">Next, split hello sample into a training part (75%, in this example) and a testing part (25%, in this example) toouse in classification and regression modeling.</span></span>

<span data-ttu-id="d3e4a-278">Een willekeurig getal (tussen 0 en 1) tooeach rij (in een kolom 'RNG') die gebruikte tooselect kruisvalidatie vouwen tijdens de training kan worden toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-278">Add a random number (between 0 and 1) tooeach row (in a "rand" column) that can be used tooselect cross-validation folds during training.</span></span>

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


<span data-ttu-id="d3e4a-279">**Uitvoer:**</span><span class="sxs-lookup"><span data-stu-id="d3e4a-279">**Output:**</span></span>

<span data-ttu-id="d3e4a-280">Tijd toorun Hallo cel: 2 seconden.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-280">Time toorun hello cell: 2 seconds.</span></span>

### <a name="specify-training-variable-and-features-and-then-create-indexed-or-one-hot-encoded-training-and-testing-input-labeled-point-rdds-or-data-frames"></a><span data-ttu-id="d3e4a-281">Geef variabele training en onderdelen, en maak vervolgens geïndexeerde of op één hot gecodeerd trainings- en testdoeleinden invoer met het label punt RDDs of gegevens frames</span><span class="sxs-lookup"><span data-stu-id="d3e4a-281">Specify training variable and features, and then create indexed or one-hot encoded training and testing input labeled point RDDs or data frames</span></span>
<span data-ttu-id="d3e4a-282">Deze sectie bevat de code die u ziet hoe tooindex categorische gegevens als een gelabelde wijst gegevenstype en deze te coderen zodat u kunt deze tootrain en test MLlib logistic regression en andere classificatiemodellen kunnen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-282">This section contains code that shows you how tooindex categorical text data as a labeled point data type, and encode it so you can use it tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="d3e4a-283">Gelabelde point-objecten zijn RDDs die zijn geformatteerd op een manier die is vereist als de invoergegevens voor de meeste machine learning-algoritmen in MLlib.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-283">Labeled point objects are RDDs that are formatted in a way that is needed as input data by most of machine learning algorithms in MLlib.</span></span> <span data-ttu-id="d3e4a-284">Een [punt gelabeld](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is een lokale vector, dense of sparse, die is gekoppeld aan een label/antwoord.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-284">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="d3e4a-285">In deze code geeft u (afhankelijke) doelvariabele Hallo en Hallo functies toouse tootrain modellen.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-285">In this code, you specify hello target (dependent) variable and hello features toouse tootrain models.</span></span> <span data-ttu-id="d3e4a-286">Vervolgens maakt u geïndexeerde of één hot gecodeerd trainings- en testdoeleinden invoer met het label punt RDDs of gegevens frames.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-286">Then, you create indexed or one-hot encoded training and testing input labeled point RDDs or data frames.</span></span>

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


<span data-ttu-id="d3e4a-287">**Uitvoer:**</span><span class="sxs-lookup"><span data-stu-id="d3e4a-287">**Output:**</span></span>

<span data-ttu-id="d3e4a-288">Tijd toorun Hallo cel: 4 seconden.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-288">Time toorun hello cell: 4 seconds.</span></span>

### <a name="automatically-categorize-and-vectorize-features-and-targets-toouse-as-inputs-for-machine-learning-models"></a><span data-ttu-id="d3e4a-289">Automatisch categoriseren en aan functies en doelen toouse vectorize als invoer voor machine learning-modellen</span><span class="sxs-lookup"><span data-stu-id="d3e4a-289">Automatically categorize and vectorize features and targets toouse as inputs for machine learning models</span></span>
<span data-ttu-id="d3e4a-290">Spark ML toocategorize Hallo doel en functies toouse in op basis van een structuur modellering functies gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-290">Use Spark ML toocategorize hello target and features toouse in tree-based modeling functions.</span></span> <span data-ttu-id="d3e4a-291">Hallo code bestaat uit twee taken:</span><span class="sxs-lookup"><span data-stu-id="d3e4a-291">hello code completes two tasks:</span></span>

* <span data-ttu-id="d3e4a-292">Maakt een binaire doel voor classificatie door de waarde 0 of 1 tooeach gegevenspunt tussen 0 en 1 toewijzen met behulp van een drempelwaarde van 0,5.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-292">Creates a binary target for classification by assigning a value of 0 or 1 tooeach data point between 0 and 1 by using a threshold value of 0.5.</span></span>
* <span data-ttu-id="d3e4a-293">Automatisch categoriseren functies.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-293">Automatically categorizes features.</span></span> <span data-ttu-id="d3e4a-294">Als Hallo aantal afzonderlijke numerieke waarden voor de functies die kleiner is dan 32 is, wordt deze functie wordt gecategoriseerd.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-294">If hello number of distinct numerical values for any feature is less than 32, that feature is categorized.</span></span>

<span data-ttu-id="d3e4a-295">Hier volgt Hallo-code voor deze twee taken.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-295">Here's hello code for these two tasks.</span></span>

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



## <a name="binary-classification-model-predict-whether-a-tip-should-be-paid"></a><span data-ttu-id="d3e4a-296">Model van de binaire classificatie: voorspellen of een tip moet worden betaald</span><span class="sxs-lookup"><span data-stu-id="d3e4a-296">Binary classification model: Predict whether a tip should be paid</span></span>
<span data-ttu-id="d3e4a-297">In deze sectie maakt maken u drie soorten binaire classificatie modellen toopredict al dan niet een tip moet worden betaald:</span><span class="sxs-lookup"><span data-stu-id="d3e4a-297">In this section, you create three types of binary classification models toopredict whether or not a tip should be paid:</span></span>

* <span data-ttu-id="d3e4a-298">Een **logistic regressiemodel** met behulp van Hallo Spark ML `LogisticRegression()` functie</span><span class="sxs-lookup"><span data-stu-id="d3e4a-298">A **logistic regression model** by using hello Spark ML `LogisticRegression()` function</span></span>
* <span data-ttu-id="d3e4a-299">Een **classificatie van willekeurige forestmodel** met behulp van Hallo Spark ML `RandomForestClassifier()` functie</span><span class="sxs-lookup"><span data-stu-id="d3e4a-299">A **random forest classification model** by using hello Spark ML `RandomForestClassifier()` function</span></span>
* <span data-ttu-id="d3e4a-300">Een **kleurovergang prestatieverbetering classificatie boomstructuur** met behulp van Hallo MLlib `GradientBoostedTrees()` functie</span><span class="sxs-lookup"><span data-stu-id="d3e4a-300">A **gradient boosting tree classification model** by using hello MLlib `GradientBoostedTrees()` function</span></span>

### <a name="create-a-logistic-regression-model"></a><span data-ttu-id="d3e4a-301">Een logistic regressiemodel maken</span><span class="sxs-lookup"><span data-stu-id="d3e4a-301">Create a logistic regression model</span></span>
<span data-ttu-id="d3e4a-302">Maak vervolgens een logistic regressiemodel met behulp van Hallo Spark ML `LogisticRegression()` functie.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-302">Next, create a logistic regression model by using hello Spark ML `LogisticRegression()` function.</span></span> <span data-ttu-id="d3e4a-303">U maakt Hallo model bouwen code in een reeks stappen:</span><span class="sxs-lookup"><span data-stu-id="d3e4a-303">You create hello model building code in a series of steps:</span></span>

1. <span data-ttu-id="d3e4a-304">**Train Hallo model** gegevens met één parameter is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-304">**Train hello model** data with one parameter set.</span></span>
2. <span data-ttu-id="d3e4a-305">**Hallo model evalueren** op een test-gegevensset met metrische gegevens.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-305">**Evaluate hello model** on a test data set with metrics.</span></span>
3. <span data-ttu-id="d3e4a-306">**Hallo model opslaan** in Blob storage voor toekomstig gebruik.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-306">**Save hello model** in Blob storage for future consumption.</span></span>
4. <span data-ttu-id="d3e4a-307">**Hallo-score-model** tegen testgegevens.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-307">**Score hello model** against test data.</span></span>
5. <span data-ttu-id="d3e4a-308">**Hallo resultaten tekenen** met ontvanger kenmerk (ROC) curven besturingssysteem.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-308">**Plot hello results** with receiver operating characteristic (ROC) curves.</span></span>

<span data-ttu-id="d3e4a-309">Hier is Hallo-code voor deze procedures:</span><span class="sxs-lookup"><span data-stu-id="d3e4a-309">Here's hello code for these procedures:</span></span>

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

<span data-ttu-id="d3e4a-310">Laden, beoordelen en Hallo resultaten opslaan.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-310">Load, score, and save hello results.</span></span>

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


<span data-ttu-id="d3e4a-311">**Uitvoer:**</span><span class="sxs-lookup"><span data-stu-id="d3e4a-311">**Output:**</span></span>

<span data-ttu-id="d3e4a-312">ROC op testgegevens 0.9827381497557599 =</span><span class="sxs-lookup"><span data-stu-id="d3e4a-312">ROC on test data = 0.9827381497557599</span></span>

<span data-ttu-id="d3e4a-313">Python op lokale Pandas gegevens frames tooplot Hallo ROC-curve gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-313">Use Python on local Pandas data frames tooplot hello ROC curve.</span></span>

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


<span data-ttu-id="d3e4a-314">**Uitvoer:**</span><span class="sxs-lookup"><span data-stu-id="d3e4a-314">**Output:**</span></span>

![Tip of geen tip ROC-curve](./media/machine-learning-data-science-process-scala-walkthrough/plot-roc-curve-tip-or-not.png)

### <a name="create-a-random-forest-classification-model"></a><span data-ttu-id="d3e4a-316">Maken van een willekeurige indeling forestmodel</span><span class="sxs-lookup"><span data-stu-id="d3e4a-316">Create a random forest classification model</span></span>
<span data-ttu-id="d3e4a-317">Maak vervolgens een willekeurige forestmodel classificatie met behulp van Hallo Spark ML `RandomForestClassifier()` functioneren en vervolgens Hallo-model op testgegevens evalueren.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-317">Next, create a random forest classification model by using hello Spark ML `RandomForestClassifier()` function, and then evaluate hello model on test data.</span></span>

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


<span data-ttu-id="d3e4a-318">**Uitvoer:**</span><span class="sxs-lookup"><span data-stu-id="d3e4a-318">**Output:**</span></span>

<span data-ttu-id="d3e4a-319">ROC op testgegevens 0.9847103571552683 =</span><span class="sxs-lookup"><span data-stu-id="d3e4a-319">ROC on test data = 0.9847103571552683</span></span>

### <a name="create-a-gbt-classification-model"></a><span data-ttu-id="d3e4a-320">Een classificatie GBT model maken</span><span class="sxs-lookup"><span data-stu-id="d3e4a-320">Create a GBT classification model</span></span>
<span data-ttu-id="d3e4a-321">Maak vervolgens een classificatie GBT model met behulp van MLlib `GradientBoostedTrees()` functioneren en vervolgens Hallo-model op testgegevens evalueren.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-321">Next, create a GBT classification model by using MLlib's `GradientBoostedTrees()` function, and then evaluate hello model on test data.</span></span>

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


<span data-ttu-id="d3e4a-322">**Uitvoer:**</span><span class="sxs-lookup"><span data-stu-id="d3e4a-322">**Output:**</span></span>

<span data-ttu-id="d3e4a-323">Gebied onder ROC-curve: 0.9846895479241554</span><span class="sxs-lookup"><span data-stu-id="d3e4a-323">Area under ROC curve: 0.9846895479241554</span></span>

## <a name="regression-model-predict-tip-amount"></a><span data-ttu-id="d3e4a-324">Regressiemodel: tip bedrag voorspellen</span><span class="sxs-lookup"><span data-stu-id="d3e4a-324">Regression model: Predict tip amount</span></span>
<span data-ttu-id="d3e4a-325">In deze sectie maakt maken u twee soorten regressie modellen toopredict Hallo tip bedrag:</span><span class="sxs-lookup"><span data-stu-id="d3e4a-325">In this section, you create two types of regression models toopredict hello tip amount:</span></span>

* <span data-ttu-id="d3e4a-326">Een **overgegaan lineair regressiemodel** met behulp van Hallo Spark ML `LinearRegression()` functie.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-326">A **regularized linear regression model** by using hello Spark ML `LinearRegression()` function.</span></span> <span data-ttu-id="d3e4a-327">U Hallo model opslaan en Hallo-model op testgegevens evalueren.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-327">You'll save hello model and evaluate hello model on test data.</span></span>
* <span data-ttu-id="d3e4a-328">Een **structuur regressiemodel verloop versterking** met behulp van Hallo Spark ML `GBTRegressor()` functie.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-328">A **gradient-boosting tree regression model** by using hello Spark ML `GBTRegressor()` function.</span></span>

### <a name="create-a-regularized-linear-regression-model"></a><span data-ttu-id="d3e4a-329">Een overgegaan lineair regressiemodel maken</span><span class="sxs-lookup"><span data-stu-id="d3e4a-329">Create a regularized linear regression model</span></span>
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


<span data-ttu-id="d3e4a-330">**Uitvoer:**</span><span class="sxs-lookup"><span data-stu-id="d3e4a-330">**Output:**</span></span>

<span data-ttu-id="d3e4a-331">Tijd toorun Hallo cel: 13 seconden.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-331">Time toorun hello cell: 13 seconds.</span></span>

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


<span data-ttu-id="d3e4a-332">**Uitvoer:**</span><span class="sxs-lookup"><span data-stu-id="d3e4a-332">**Output:**</span></span>

<span data-ttu-id="d3e4a-333">R-sqr op testgegevens 0.5960320470835743 =</span><span class="sxs-lookup"><span data-stu-id="d3e4a-333">R-sqr on test data = 0.5960320470835743</span></span>

<span data-ttu-id="d3e4a-334">Vervolgens testresultaten query Hallo als een gegevensframe en gebruik AutoVizWidget en matplotlib toovisualize deze.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-334">Next, query hello test results as a data frame and use AutoVizWidget and matplotlib toovisualize it.</span></span>

    # RUN A SQL QUERY
    %%sql -q -o sqlResults
    select * from testResults

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, AND SO ON)
    sqlResults

<span data-ttu-id="d3e4a-335">Hallo code maakt een frame lokale gegevens van Hallo query-uitvoer en Hallo van de gegevenspunten.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-335">hello code creates a local data frame from hello query output and plots hello data.</span></span> <span data-ttu-id="d3e4a-336">Hallo `%%local` magic maakt een frame lokale gegevens `sqlResults`, die u kunt tooplot matplotlib.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-336">hello `%%local` magic creates a local data frame, `sqlResults`, which you can use tooplot with matplotlib.</span></span>

> [!NOTE]
> <span data-ttu-id="d3e4a-337">Deze Spark-magic wordt meerdere malen gebruikt in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-337">This Spark magic is used multiple times in this article.</span></span> <span data-ttu-id="d3e4a-338">Als Hallo hoeveelheid gegevens te groot is, moet u een steekproef nemen uit toocreate een gegevensframe dat in het lokale geheugen past.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-338">If hello amount of data is large, you should sample toocreate a data frame that can fit in local memory.</span></span>
> 
> 

<span data-ttu-id="d3e4a-339">Waarnemingspunten maken met behulp van Python matplotlib.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-339">Create plots by using Python matplotlib.</span></span>

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

<span data-ttu-id="d3e4a-340">**Uitvoer:**</span><span class="sxs-lookup"><span data-stu-id="d3e4a-340">**Output:**</span></span>

![Tip bedrag: werkelijk vs. voorspelde](./media/machine-learning-data-science-process-scala-walkthrough/plot-actual-vs-predicted-tip-amount.png)

### <a name="create-a-gbt-regression-model"></a><span data-ttu-id="d3e4a-342">Een regressiemodel GBT maken</span><span class="sxs-lookup"><span data-stu-id="d3e4a-342">Create a GBT regression model</span></span>
<span data-ttu-id="d3e4a-343">Een regressiemodel GBT maken met behulp van Hallo Spark ML `GBTRegressor()` functioneren en vervolgens Hallo-model op testgegevens evalueren.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-343">Create a GBT regression model by using hello Spark ML `GBTRegressor()` function, and then evaluate hello model on test data.</span></span>

<span data-ttu-id="d3e4a-344">[Structuren verloop boosted](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) ensembles van beslissingsstructuren zijn.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-344">[Gradient-boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="d3e4a-345">GBTs train besluit structuren iteratief toominimize een verlies-functie.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-345">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="d3e4a-346">U kunt GBTs gebruiken voor regressie en classificatie.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-346">You can use GBTs for regression and classification.</span></span> <span data-ttu-id="d3e4a-347">Ze categorische functies kunnen verwerken, hoeven niet functie schalen en nonlinearities en functie interacties kunnen vastleggen.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-347">They can handle categorical features, do not require feature scaling, and can capture nonlinearities and feature interactions.</span></span> <span data-ttu-id="d3e4a-348">Ook kunt u ze in een setting multiklasse classificatie.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-348">You also can use them in a multiclass-classification setting.</span></span>

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


<span data-ttu-id="d3e4a-349">**Uitvoer:**</span><span class="sxs-lookup"><span data-stu-id="d3e4a-349">**Output:**</span></span>

<span data-ttu-id="d3e4a-350">Test R-sqr is: 0.7655383534596654</span><span class="sxs-lookup"><span data-stu-id="d3e4a-350">Test R-sqr is: 0.7655383534596654</span></span>

## <a name="advanced-modeling-utilities-for-optimization"></a><span data-ttu-id="d3e4a-351">Hulpprogramma's voor geavanceerde modellering voor optimalisatie</span><span class="sxs-lookup"><span data-stu-id="d3e4a-351">Advanced modeling utilities for optimization</span></span>
<span data-ttu-id="d3e4a-352">In deze sectie gebruikt u de machine learning-hulpprogramma's die ontwikkelaars vaak voor de optimalisatie van het model gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-352">In this section, you use machine learning utilities that developers frequently use for model optimization.</span></span> <span data-ttu-id="d3e4a-353">U kunt in het bijzonder machine learning-modellen drie verschillende manieren optimaliseren met behulp van de parameter sweeping en kruisvalidatie:</span><span class="sxs-lookup"><span data-stu-id="d3e4a-353">Specifically, you can optimize machine learning models three different ways by using parameter sweeping and cross-validation:</span></span>

* <span data-ttu-id="d3e4a-354">Hallo gegevens splitsen in train en validatie sets, Hallo model optimaliseren door hyper-parameter sweeping in een trainingset en evalueren in een set validatie (lineaire regressie)</span><span class="sxs-lookup"><span data-stu-id="d3e4a-354">Split hello data into train and validation sets, optimize hello model by using hyper-parameter sweeping on a training set, and evaluate on a validation set (linear regression)</span></span>
* <span data-ttu-id="d3e4a-355">Hallo model optimaliseren door kruisvalidatie en hyper-parameter verstrekkende met behulp van Spark ML CrossValidator functie (binaire classificatie)</span><span class="sxs-lookup"><span data-stu-id="d3e4a-355">Optimize hello model by using cross-validation and hyper-parameter sweeping by using Spark ML's CrossValidator function (binary classification)</span></span>
* <span data-ttu-id="d3e4a-356">Hallo model optimaliseren door aangepaste kruisvalidatie en code van de parameter-sweeping toouse een machine learning-functie en de parameter ingesteld (lineaire regressie)</span><span class="sxs-lookup"><span data-stu-id="d3e4a-356">Optimize hello model by using custom cross-validation and parameter-sweeping code toouse any machine learning function and parameter set (linear regression)</span></span>

<span data-ttu-id="d3e4a-357">**Kruisvalidatie** is een techniek die hoe goed een op een bekende set gegevens getraind model toopredict Hallo functies van gegevenssets waarop deze is niet getraind wordt generalize evalueert.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-357">**Cross-validation** is a technique that assesses how well a model trained on a known set of data will generalize toopredict hello features of data sets on which it has not been trained.</span></span> <span data-ttu-id="d3e4a-358">Hallo is algemeen idee achter deze techniek dat een model wordt getraind van een gegevensset van bekende gegevens, en vervolgens hello nauwkeurigheid van de voorspellingen is getest op basis van een onafhankelijke set van gegevens.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-358">hello general idea behind this technique is that a model is trained on a data set of known data, and then hello accuracy of its predictions is tested against an independent data set.</span></span> <span data-ttu-id="d3e4a-359">Een veelvoorkomende implementatie is toodivide een gegevensset in *k*-vouwen en vervolgens trainen Hallo model round-robin toewijst op alle één Hallo vouwen.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-359">A common implementation is toodivide a data set into *k*-folds, and then train hello model in a round-robin fashion on all but one of hello folds.</span></span>

<span data-ttu-id="d3e4a-360">**Hyper-parameter optimalisatie** Hallo probleem van het kiezen van een set van hyper-parameters voor een leeralgoritme meestal met Hallo doel voor het optimaliseren van een meting van Hallo-algoritme op de prestaties van een onafhankelijke set van gegevens.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-360">**Hyper-parameter optimization** is hello problem of choosing a set of hyper-parameters for a learning algorithm, usually with hello goal of optimizing a measure of hello algorithm's performance on an independent data set.</span></span> <span data-ttu-id="d3e4a-361">Een hyper-parameter is een waarde die u buiten Hallo model training procedure moet opgeven.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-361">A hyper-parameter is a value that you must specify outside hello model training procedure.</span></span> <span data-ttu-id="d3e4a-362">Veronderstellingen over hyper-parameterwaarden kunnen beïnvloeden Hallo flexibiliteit en de nauwkeurigheid van het Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-362">Assumptions about hyper-parameter values can affect hello flexibility and accuracy of hello model.</span></span> <span data-ttu-id="d3e4a-363">Beslissingsstructuren hyper-parameters hebben, bijvoorbeeld zoals Hallo gewenste omvang en aantal leaves in Hallo-structuur.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-363">Decision trees have hyper-parameters, for example, such as hello desired depth and number of leaves in hello tree.</span></span> <span data-ttu-id="d3e4a-364">U moet een misclassification sancties term voor een vectormachine ondersteuning (SVM) instellen.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-364">You must set a misclassification penalty term for a support vector machine (SVM).</span></span>

<span data-ttu-id="d3e4a-365">Een algemene verbetering van de manier tooperform hyper-parameter is toouse een zoekopdracht raster, ook wel een **parameter vegen**.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-365">A common way tooperform hyper-parameter optimization is toouse a grid search, also called a **parameter sweep**.</span></span> <span data-ttu-id="d3e4a-366">In een zoekopdracht raster wordt een intensieve zoekactie uitgevoerd via Hallo waarden van een subverzameling van Hallo hyper parameter ruimte voor een leeralgoritme.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-366">In a grid search, an exhaustive search is performed through hello values of a specified subset of hello hyper-parameter space for a learning algorithm.</span></span> <span data-ttu-id="d3e4a-367">Kruisvalidatie kan voorzien van een prestaties metrische toosort Hallo optimale resultaten die wordt geproduceerd door Hallo raster zoekalgoritme.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-367">Cross-validation can supply a performance metric toosort out hello optimal results produced by hello grid search algorithm.</span></span> <span data-ttu-id="d3e4a-368">Als u kruisvalidatie hyper parameter sweeping gebruikt, kunt u problemen zoals de gegevens van een model tootraining overfitting limiet.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-368">If you use cross-validation hyper-parameter sweeping, you can help limit problems like overfitting a model tootraining data.</span></span> <span data-ttu-id="d3e4a-369">Op deze manier Hallo model behoudt Hallo capaciteit tooapply toohello algemene set gegevens vanaf welke Hallo trainingsgegevens is opgehaald.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-369">This way, hello model retains hello capacity tooapply toohello general set of data from which hello training data was extracted.</span></span>

### <a name="optimize-a-linear-regression-model-with-hyper-parameter-sweeping"></a><span data-ttu-id="d3e4a-370">Een lineair regressiemodel met hyper-parameter sweeping optimaliseren</span><span class="sxs-lookup"><span data-stu-id="d3e4a-370">Optimize a linear regression model with hyper-parameter sweeping</span></span>
<span data-ttu-id="d3e4a-371">Vervolgens gegevens splitsen in train en validatie sets, gebruik hyper-parameter van een training verstrekkende toooptimize Hallo model instelt en evalueren in een set validatie (lineaire regressie).</span><span class="sxs-lookup"><span data-stu-id="d3e4a-371">Next, split data into train and validation sets, use hyper-parameter sweeping on a training set toooptimize hello model, and evaluate on a validation set (linear regression).</span></span>

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


<span data-ttu-id="d3e4a-372">**Uitvoer:**</span><span class="sxs-lookup"><span data-stu-id="d3e4a-372">**Output:**</span></span>

<span data-ttu-id="d3e4a-373">Test R-sqr is: 0.6226484708501209</span><span class="sxs-lookup"><span data-stu-id="d3e4a-373">Test R-sqr is: 0.6226484708501209</span></span>

### <a name="optimize-hello-binary-classification-model-by-using-cross-validation-and-hyper-parameter-sweeping"></a><span data-ttu-id="d3e4a-374">Hallo binaire classificatie model optimaliseren door sweeping kruisvalidatie en hyper-parameter</span><span class="sxs-lookup"><span data-stu-id="d3e4a-374">Optimize hello binary classification model by using cross-validation and hyper-parameter sweeping</span></span>
<span data-ttu-id="d3e4a-375">Deze sectie leest u hoe toooptimize een binaire indeling met behulp van kruisvalidatie en hyper-parameter sweeping model.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-375">This section shows you how toooptimize a binary classification model by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="d3e4a-376">Dit maakt gebruik van Hallo Spark ML `CrossValidator` functie.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-376">This uses hello Spark ML `CrossValidator` function.</span></span>

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


<span data-ttu-id="d3e4a-377">**Uitvoer:**</span><span class="sxs-lookup"><span data-stu-id="d3e4a-377">**Output:**</span></span>

<span data-ttu-id="d3e4a-378">Tijd toorun Hallo cel: 33 seconden.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-378">Time toorun hello cell: 33 seconds.</span></span>

### <a name="optimize-hello-linear-regression-model-by-using-custom-cross-validation-and-parameter-sweeping-code"></a><span data-ttu-id="d3e4a-379">Hallo lineair regressiemodel met behulp van aangepaste kruisvalidatie en parameter sweeping code optimaliseren</span><span class="sxs-lookup"><span data-stu-id="d3e4a-379">Optimize hello linear regression model by using custom cross-validation and parameter-sweeping code</span></span>
<span data-ttu-id="d3e4a-380">Vervolgens Hallo model optimaliseren door aangepaste code en beste Modelparameters Hallo identificeren door middel van Hallo criterium van hoogste nauwkeurig.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-380">Next, optimize hello model by using custom code, and identify hello best model parameters by using hello criterion of highest accuracy.</span></span> <span data-ttu-id="d3e4a-381">Vervolgens maakt u het laatste model Hallo Hallo-model op testgegevens evalueren en Hallo model niet opslaan in Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-381">Then, create hello final model, evaluate hello model on test data, and save hello model in Blob storage.</span></span> <span data-ttu-id="d3e4a-382">Ten slotte Hallo model niet laden, testgegevens beoordelen en evalueren nauwkeurig.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-382">Finally, load hello model, score test data, and evaluate accuracy.</span></span>

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


<span data-ttu-id="d3e4a-383">**Uitvoer:**</span><span class="sxs-lookup"><span data-stu-id="d3e4a-383">**Output:**</span></span>

<span data-ttu-id="d3e4a-384">Tijd toorun Hallo cel: 61 seconden.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-384">Time toorun hello cell: 61 seconds.</span></span>

## <a name="consume-spark-built-machine-learning-models-automatically-with-scala"></a><span data-ttu-id="d3e4a-385">Spark is gebouwd machine learning-modellen automatisch met Scala gebruiken</span><span class="sxs-lookup"><span data-stu-id="d3e4a-385">Consume Spark-built machine learning models automatically with Scala</span></span>
<span data-ttu-id="d3e4a-386">Zie voor een overzicht van onderwerpen die helpt u bij het Hallo-taken die Hallo Gegevenswetenschap proces in Azure omvatten, [Team gegevens wetenschap proces](http://aka.ms/datascienceprocess).</span><span class="sxs-lookup"><span data-stu-id="d3e4a-386">For an overview of topics that walk you through hello tasks that comprise hello Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="d3e4a-387">[Gegevens wetenschap proces scenario's in een team](data-science-process-walkthroughs.md) beschrijft andere end-to-end-scenario's die laten zien Hallo stappen voor het Hallo-Team gegevens wetenschappelijke processen voor specifieke scenario's.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-387">[Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) describes other end-to-end walkthroughs that demonstrate hello steps in hello Team Data Science Process for specific scenarios.</span></span> <span data-ttu-id="d3e4a-388">Hallo-scenario's ook laten zien hoe toocombine cloud en on-premises hulpprogramma's en services in een werkstroom of pijplijn toocreate een intelligente toepassing.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-388">hello walkthroughs also illustrate how toocombine cloud and on-premises tools and services into a workflow or pipeline toocreate an intelligent application.</span></span>

<span data-ttu-id="d3e4a-389">[Score Spark is gebouwd machine learning-modellen](machine-learning-data-science-spark-model-consumption.md) ziet u hoe toouse Scala code tooautomatically geladen en beoordelen van nieuwe gegevens sets met machine learning-modellen in Spark is gebouwd en opgeslagen in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-389">[Score Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) shows you how toouse Scala code tooautomatically load and score new data sets with machine learning models built in Spark and saved in Azure Blob storage.</span></span> <span data-ttu-id="d3e4a-390">U kunt instructies te volgen Hallo die er en vervangt u gewoon Hallo Python-code door Scala code in dit artikel voor geautomatiseerde verbruik.</span><span class="sxs-lookup"><span data-stu-id="d3e4a-390">You can follow hello instructions provided there, and simply replace hello Python code with Scala code in this article for automated consumption.</span></span>

