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
# <a name="data-exploration-and-modeling-with-spark"></a><span data-ttu-id="90771-103">Met Spark gegevens verkennen en modelleren</span><span class="sxs-lookup"><span data-stu-id="90771-103">Data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="90771-104">In dit scenario maakt gebruik van HDInsight Spark toodo gegevensverkenning en binaire classificatie en taken van een steekproef van Hallo NYC modelleren regressie taxi reis en ritbedrag 2013 gegevensset.</span><span class="sxs-lookup"><span data-stu-id="90771-104">This walkthrough uses HDInsight Spark toodo data exploration and binary classification and regression modeling tasks on a sample of hello NYC taxi trip and fare 2013 dataset.</span></span>  <span data-ttu-id="90771-105">Dit leidt u door de stappen Hallo Hallo [gegevens wetenschap proces](http://aka.ms/datascienceprocess), end-to-end, met behulp van een HDInsight Spark-cluster gebruikt voor verwerking en Azure blobs toostore Hallo gegevens en het Hallo-modellen.</span><span class="sxs-lookup"><span data-stu-id="90771-105">It walks you through hello steps of hello [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs toostore hello data and hello models.</span></span> <span data-ttu-id="90771-106">Hallo-proces wordt verkend en gebracht van een Azure Storage-Blob gegevens visualiseren en vervolgens wordt voorbereid Hallo gegevens toobuild voorspellende modellen.</span><span class="sxs-lookup"><span data-stu-id="90771-106">hello process explores and visualizes data brought in from an Azure Storage Blob and then prepares hello data toobuild predictive models.</span></span> <span data-ttu-id="90771-107">Deze modellen zijn samenstellen met Hallo Spark MLlib toolkit toodo binaire classificatie en regressie modelleren van taken.</span><span class="sxs-lookup"><span data-stu-id="90771-107">These models are build using hello Spark MLlib toolkit toodo binary classification and regression modeling tasks.</span></span>

* <span data-ttu-id="90771-108">Hallo **binaire classificatie** taak toopredict is al dan niet een tip voor Hallo reis wordt betaald.</span><span class="sxs-lookup"><span data-stu-id="90771-108">hello **binary classification** task is toopredict whether or not a tip is paid for hello trip.</span></span> 
* <span data-ttu-id="90771-109">Hallo **regressie** taak toopredict Hallo hoeveelheid Hallo tip op basis van andere functies tip is.</span><span class="sxs-lookup"><span data-stu-id="90771-109">hello **regression** task is toopredict hello amount of hello tip based on other tip features.</span></span> 

<span data-ttu-id="90771-110">Hallo modellen we gebruiken omvatten logistic en lineaire regressie, willekeurige forests en kleurovergang gestimuleerd structuren:</span><span class="sxs-lookup"><span data-stu-id="90771-110">hello models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="90771-111">[Lineaire regressie met SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is een lineair regressiemodel die gebruikmaakt van een methode stochastische kleurovergang Daalgradiënt (SGD) en voor optimalisatie en het onderdeel schalen toopredict Hallo tip bedragen betaald.</span><span class="sxs-lookup"><span data-stu-id="90771-111">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling toopredict hello tip amounts paid.</span></span> 
* <span data-ttu-id="90771-112">[Logistic regression met LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) of regressie 'logit', is een regressiemodel dat kan worden gebruikt wanneer Hallo afhankelijke variabele categorische toodo gegevensclassificatie is.</span><span class="sxs-lookup"><span data-stu-id="90771-112">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when hello dependent variable is categorical toodo data classification.</span></span> <span data-ttu-id="90771-113">LBFGS is een quasi toegepast optimalisatie-algoritme dat benadert Hallo Broyden – Fletcher – Goldfarb – Shanno (BFGS) algoritme met een beperkte hoeveelheid computergeheugen en die wordt veel gebruikt in machine learning.</span><span class="sxs-lookup"><span data-stu-id="90771-113">LBFGS is a quasi-Newton optimization algorithm that approximates hello Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="90771-114">[Willekeurige forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) ensembles van beslissingsstructuren zijn.</span><span class="sxs-lookup"><span data-stu-id="90771-114">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="90771-115">Ze combineren veel decision trees tooreduce Hallo risico te.</span><span class="sxs-lookup"><span data-stu-id="90771-115">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="90771-116">Willekeurige forests worden gebruikt voor regressie en classificatie en categorische functies kunnen verwerken en toohello multiklassen classificatie instelling kunnen worden uitgebreid.</span><span class="sxs-lookup"><span data-stu-id="90771-116">Random forests are used for regression and classification and can handle categorical features and can be extended toohello multiclass classification setting.</span></span> <span data-ttu-id="90771-117">Ze hoeven niet functie schalen en weet kunnen toocapture niet-mogelijkheid tot en interactie van de functie.</span><span class="sxs-lookup"><span data-stu-id="90771-117">They do not require feature scaling and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="90771-118">Willekeurige forests zijn een van de meest succesvolle Hallo-machine learning-modellen voor de indeling en regressie.</span><span class="sxs-lookup"><span data-stu-id="90771-118">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="90771-119">[Verloop boosted structuren](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) ensembles van beslissingsstructuren zijn.</span><span class="sxs-lookup"><span data-stu-id="90771-119">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="90771-120">GBTs train besluit structuren iteratief toominimize een verlies-functie.</span><span class="sxs-lookup"><span data-stu-id="90771-120">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="90771-121">GBTs worden gebruikt voor regressie en classificatie en categorische functies kan verwerken, hoeven niet functie schalen en kunnen toocapture niet-mogelijkheid tot zijn en interacties functies.</span><span class="sxs-lookup"><span data-stu-id="90771-121">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="90771-122">Ze kunnen ook worden gebruikt in een setting multiklasse classificatie.</span><span class="sxs-lookup"><span data-stu-id="90771-122">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="90771-123">Hallo modellering stappen bevatten ook een code die laat zien hoe tootrain, evalueren en opslaan van elk type model.</span><span class="sxs-lookup"><span data-stu-id="90771-123">hello modeling steps also contain code showing how tootrain, evaluate, and save each type of model.</span></span> <span data-ttu-id="90771-124">Python is gebruikte toocode Hallo-oplossing en tooshow Hallo relevante waarnemingspunten.</span><span class="sxs-lookup"><span data-stu-id="90771-124">Python has been used toocode hello solution and tooshow hello relevant plots.</span></span>   

> [!NOTE]
> <span data-ttu-id="90771-125">Hoewel Hallo Spark MLlib toolkit ontworpen toowork op grote gegevenssets is, wordt hier een voorbeeld van een relatief klein (ongeveer 30 Mb met behulp van 170K rijen, ongeveer 0,1% van de oorspronkelijke NYC gegevensset Hallo) gebruikt voor het gemak.</span><span class="sxs-lookup"><span data-stu-id="90771-125">Although hello Spark MLlib toolkit is designed toowork on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of hello original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="90771-126">Hallo oefening hier opgegeven efficiënt (in ongeveer 10 minuten) op een HDInsight-cluster met 2 worker-knooppunten wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="90771-126">hello exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="90771-127">Hallo kan dezelfde code bevatten, met kleine wijzigingen worden gebruikt tooprocess grotere gegevenssets-wordt met de juiste wijzigingen voor het cachen van gegevens in het geheugen en Hallo clustergrootte wijzigen.</span><span class="sxs-lookup"><span data-stu-id="90771-127">hello same code, with minor modifications, can be used tooprocess larger data-sets, with appropriate modifications for caching data in memory and changing hello cluster size.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="90771-128">Vereisten</span><span class="sxs-lookup"><span data-stu-id="90771-128">Prerequisites</span></span>
<span data-ttu-id="90771-129">U moet een Azure-account en een 1.6 Spark (of Spark 2.0) HDInsight-cluster toocomplete in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="90771-129">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster toocomplete this walkthrough.</span></span> <span data-ttu-id="90771-130">Zie Hallo [overzicht van Gegevenswetenschap met Spark op Azure HDInsight](machine-learning-data-science-spark-overview.md) voor instructies over het toosatisfy deze vereisten.</span><span class="sxs-lookup"><span data-stu-id="90771-130">See hello [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how toosatisfy these requirements.</span></span> <span data-ttu-id="90771-131">Dit onderwerp bevat ook een beschrijving van Hallo NYC 2013 Taxi gegevens hier gebruikt en instructies over hoe tooexecute code van een Jupyter-notebook in Spark-cluster Hallo.</span><span class="sxs-lookup"><span data-stu-id="90771-131">That topic also contains a description of hello NYC 2013 Taxi data used here and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster.</span></span> 

## <a name="spark-clusters-and-notebooks"></a><span data-ttu-id="90771-132">Spark-clusters en laptops</span><span class="sxs-lookup"><span data-stu-id="90771-132">Spark clusters and notebooks</span></span>
<span data-ttu-id="90771-133">Instellingsstappen en code vindt u in dit scenario voor het gebruik van een HDInsight Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="90771-133">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="90771-134">Maar Jupyter-notebooks zijn opgegeven voor zowel HDInsight Spark 1.6 en 2.0 Spark-clusters.</span><span class="sxs-lookup"><span data-stu-id="90771-134">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="90771-135">Een beschrijving van het Hallo-notitieblokken en -koppelingen toothem vindt u in Hallo [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) voor Hallo GitHub-opslagplaats met ze.</span><span class="sxs-lookup"><span data-stu-id="90771-135">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="90771-136">Bovendien Hallo code hier en in notitieblokken Hallo gekoppeld is algemeen en moet werken op een Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="90771-136">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="90771-137">Als u geen van HDInsight Spark, Hallo clusterinstallatie gebruikmaakt en management stappen mogelijk enigszins afwijken van wat hier moet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="90771-137">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="90771-138">Voor het gemak vindt hier u koppelingen Hallo toohello Jupyter-notebooks voor Spark 1.6 (toobe worden uitgevoerd in de pySpark-kernel Hallo Hallo Jupyter-Notebook server) en Spark 2.0 (toobe in Hallo pySpark3 kernel Hallo Jupyter-Notebook server worden uitgevoerd):</span><span class="sxs-lookup"><span data-stu-id="90771-138">For convenience, here are hello links toohello Jupyter notebooks for Spark 1.6 (toobe run in hello pySpark kernel of hello Jupyter Notebook server) and  Spark 2.0 (toobe run in hello pySpark3 kernel of hello Jupyter Notebook server):</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="90771-139">Spark 1.6 laptops</span><span class="sxs-lookup"><span data-stu-id="90771-139">Spark 1.6 notebooks</span></span>

<span data-ttu-id="90771-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): bevat informatie over het tooperform gegevensverkenning, modelleren en batchscoreberekening met diverse verschillende algoritmen.</span><span class="sxs-lookup"><span data-stu-id="90771-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): Provides information on how tooperform data exploration, modeling, and scoring with several different algorithms.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="90771-141">Spark 2.0-laptops</span><span class="sxs-lookup"><span data-stu-id="90771-141">Spark 2.0 notebooks</span></span>
<span data-ttu-id="90771-142">Hallo regressie en classificatie taken die worden geïmplementeerd met een 2.0 Spark-cluster zich in afzonderlijke notebooks en Hallo classificatie notebook maakt gebruik van een andere gegevensset:</span><span class="sxs-lookup"><span data-stu-id="90771-142">hello regression and classification tasks that are implemented using a Spark 2.0 cluster are in separate notebooks and hello classification notebook uses a different data set:</span></span>

- <span data-ttu-id="90771-143">[Spark2.0-pySpark3-machine-Learning-Data-Science-Spark-Advanced-Data-Exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): dit bestand bevat informatie over hoe tooperform gegevensverkenning, modelleren en scores in Spark 2.0 opslagclusters die gebruikmaken van Hallo NYC Taxi reis en tarief gegevensset-beschreven [hier](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="90771-143">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how tooperform data exploration, modeling, and scoring in Spark 2.0 clusters using hello NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span> <span data-ttu-id="90771-144">Deze laptop is mogelijk een goed uitgangspunt voor het snel verkennen Hallo-code die we voor Spark 2.0 hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="90771-144">This notebook may be a good starting point for quickly exploring hello code we have provided for Spark 2.0.</span></span> <span data-ttu-id="90771-145">Voor een meer gedetailleerde notebook Hallo NYC Taxi gegevens analyseert, Zie de volgende notebook Hallo in deze lijst.</span><span class="sxs-lookup"><span data-stu-id="90771-145">For a more detailed notebook analyzes hello NYC Taxi data, see hello next notebook in this list.</span></span> <span data-ttu-id="90771-146">Zie na deze lijst Hallo-opmerkingen die deze laptops vergelijken.</span><span class="sxs-lookup"><span data-stu-id="90771-146">See hello notes following this list that compare these notebooks.</span></span> 
- <span data-ttu-id="90771-147">[Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): dit bestand ziet u hoe tooperform gegevens worsteling (Spark SQL en dataframe bewerkingen), exploratie, model en score berekenen met behulp van Hallo NYC Taxi reis en tarief set gegevens die worden beschreven [ Hier](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="90771-147">[Spark2.0-pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): This file shows how tooperform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using hello NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span>
- <span data-ttu-id="90771-148">[Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): dit bestand ziet u hoe tooperform gegevens worsteling (Spark SQL en dataframe bewerkingen), exploratie, model en score berekenen met behulp van bekende luchtvaartmaatschappij tijdige vertrek Hallo de gegevensset van 2011 en 2012.</span><span class="sxs-lookup"><span data-stu-id="90771-148">[Spark2.0-pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): This file shows how tooperform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using hello well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="90771-149">We Hallo luchtvaartmaatschappij gegevensset geïntegreerd met Hallo luchthaven weer gegevens (bijvoorbeeld windsnelheid, temperatuur en hoogte enz.) voorafgaande toomodeling, zodat deze weer-functies kunnen worden opgenomen in het Hallo-model.</span><span class="sxs-lookup"><span data-stu-id="90771-149">We integrated hello airline dataset with hello airport weather data (e.g. windspeed, temperature, altitude etc.) prior toomodeling, so these weather features can be included in hello model.</span></span>

<!-- -->

> [!NOTE]
> <span data-ttu-id="90771-150">Hallo luchtvaartmaatschappij dataset is toegevoegd toohello Spark 2.0 notitieblokken toobetter illustreren Hallo gebruik van de classificatie-algoritmen.</span><span class="sxs-lookup"><span data-stu-id="90771-150">hello airline dataset was added toohello Spark 2.0 notebooks toobetter illustrate hello use of classification algorithms.</span></span> <span data-ttu-id="90771-151">Zie Hallo koppelingen voor meer informatie over luchtvaartmaatschappij tijdige vertrek gegevensset en weer gegevensset te volgen:</span><span class="sxs-lookup"><span data-stu-id="90771-151">See hello following links for information about airline on-time departure dataset and weather dataset:</span></span>

>- <span data-ttu-id="90771-152">Luchtvaartmaatschappij tijdige vertrek gegevens: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span><span class="sxs-lookup"><span data-stu-id="90771-152">Airline on-time departure data: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span></span>

>- <span data-ttu-id="90771-153">Luchthaven weergegevens: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span><span class="sxs-lookup"><span data-stu-id="90771-153">Airport weather data: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span></span> 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
<span data-ttu-id="90771-154">Hallo Spark 2.0 notitieblokken op Hallo NYC taxi en luchtvaartmaatschappij vlucht vertraging-gegevenssets duurt 10 minuten of meer toorun (afhankelijk van de grootte van de Hallo van uw HDI-cluster).</span><span class="sxs-lookup"><span data-stu-id="90771-154">hello Spark 2.0 notebooks on hello NYC taxi and airline flight delay data-sets can take 10 mins or more toorun (depending on hello size of your HDI cluster).</span></span> <span data-ttu-id="90771-155">Hallo eerste laptop in Hallo boven lijst geeft veel aspecten van Hallo gegevensverkenning, visualisatie en ML-model training in een laptop die minder tijd toorun met een lagere actieve NYC gegevensset duurt, in welke Hallo taxi en tarief bestanden vooraf lid zijn: [ Spark2.0-pySpark3-machine-Learning-Data-Science-Spark-Advanced-Data-Exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) deze notebook neemt een veel kortere tijd toofinish (2-3 minuten) en kan worden een goed startpunt voor Hallo code snel verkennen we hebben opgegeven voor Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="90771-155">hello first notebook in hello above list shows many aspects of hello data exploration, visualization and ML model training in a notebook that takes less time toorun with down-sampled NYC data set, in which hello taxi and fare files have been pre-joined: [Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) This notebook takes a much shorter time toofinish (2-3 mins) and may be a good starting point for quickly exploring hello code we have provided for Spark 2.0.</span></span> 

<!-- -->

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<!-- -->

> [!NOTE]
<span data-ttu-id="90771-156">onderstaande Hallo beschrijvingen zijn verwante toousing Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="90771-156">hello descriptions below are related toousing Spark 1.6.</span></span> <span data-ttu-id="90771-157">Gebruik Hallo notitieblokken beschreven en bovenstaande voor Spark 2.0-versies.</span><span class="sxs-lookup"><span data-stu-id="90771-157">For Spark 2.0 versions, please use hello notebooks described and linked above.</span></span> 

<!-- -->

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="90771-158">Setup: opslaglocaties, bibliotheken en Hallo voorinstelling Spark-context</span><span class="sxs-lookup"><span data-stu-id="90771-158">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="90771-159">Spark is kunnen tooread en write tooAzure Storage-Blob (ook wel bekend als WASB).</span><span class="sxs-lookup"><span data-stu-id="90771-159">Spark is able tooread and write tooAzure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="90771-160">Dus een van uw bestaande gegevens opgeslagen kunnen worden verwerkt met Spark en Hallo resultaten WASB opgeslagen opnieuw in.</span><span class="sxs-lookup"><span data-stu-id="90771-160">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="90771-161">toosave modellen of bestanden in WASB moet Hallo pad toobe juist opgegeven.</span><span class="sxs-lookup"><span data-stu-id="90771-161">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="90771-162">Hallo standaard verbonden container toohello Spark-cluster kan worden verwezen met behulp van een pad die begint met: ' wasb: / / / '.</span><span class="sxs-lookup"><span data-stu-id="90771-162">hello default container attached toohello Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="90771-163">Andere locaties wordt verwezen door ' wasb: / / '.</span><span class="sxs-lookup"><span data-stu-id="90771-163">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="90771-164">Directory-paden voor opslaglocaties in WASB instellen</span><span class="sxs-lookup"><span data-stu-id="90771-164">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="90771-165">Hallo volgende codevoorbeeld wordt Hallo locatie van Hallo gegevens toobe lezen en Hallo pad voor Hallo model opslag directory toowhich Hallo model uitvoer wordt opgeslagen:</span><span class="sxs-lookup"><span data-stu-id="90771-165">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved:</span></span>

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";

    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 


### <a name="import-libraries"></a><span data-ttu-id="90771-166">Bibliotheken importeren</span><span class="sxs-lookup"><span data-stu-id="90771-166">Import libraries</span></span>
<span data-ttu-id="90771-167">Instellen is ook vereist nodig bibliotheken importeren.</span><span class="sxs-lookup"><span data-stu-id="90771-167">Set up also requires importing necessary libraries.</span></span> <span data-ttu-id="90771-168">Context voor spark instellen en importeer nodig bibliotheken Hello code te volgen:</span><span class="sxs-lookup"><span data-stu-id="90771-168">Set spark context and import necessary libraries with hello following code:</span></span>

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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="90771-169">Vooraf context voor Spark en PySpark magics</span><span class="sxs-lookup"><span data-stu-id="90771-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="90771-170">Hallo PySpark kernels die worden geleverd met Jupyter-notebooks hebben een vooraf ingestelde context.</span><span class="sxs-lookup"><span data-stu-id="90771-170">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="90771-171">Dus hoeft u niet tooset Hallo Spark of Hive-contexten expliciet voordat u begint te werken met Hallo-toepassing die u ontwikkelt.</span><span class="sxs-lookup"><span data-stu-id="90771-171">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="90771-172">Deze contexten zijn standaard voor u beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="90771-172">These contexts are available for you by default.</span></span> <span data-ttu-id="90771-173">Deze contexten zijn:</span><span class="sxs-lookup"><span data-stu-id="90771-173">These contexts are:</span></span>

* <span data-ttu-id="90771-174">SC - voor Spark</span><span class="sxs-lookup"><span data-stu-id="90771-174">sc - for Spark</span></span> 
* <span data-ttu-id="90771-175">sqlContext - voor Hive</span><span class="sxs-lookup"><span data-stu-id="90771-175">sqlContext - for Hive</span></span>

<span data-ttu-id="90771-176">Hallo PySpark-kernel biedt een aantal vooraf gedefinieerde 'magics', die zijn speciale opdrachten die u met aanroepen kunt %%.</span><span class="sxs-lookup"><span data-stu-id="90771-176">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="90771-177">Er zijn twee dergelijke opdrachten die worden gebruikt in deze codevoorbeelden.</span><span class="sxs-lookup"><span data-stu-id="90771-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="90771-178">**%% lokale** geeft aan dat Hallo-code in de volgende regels toobe lokaal wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="90771-178">**%%local** Specifies that hello code in subsequent lines is toobe executed locally.</span></span> <span data-ttu-id="90771-179">De sitecode moet geldige Python-code.</span><span class="sxs-lookup"><span data-stu-id="90771-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="90771-180">**%% sql -o <variable name>**  een Hive-query op Hallo sqlContext wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="90771-180">**%%sql -o <variable name>** Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="90771-181">Als het Hallo -o parameter is doorgegeven, Hallo resultaat van Hallo query blijft behouden in Hallo %% lokale Python context als een DataFrame Pandas.</span><span class="sxs-lookup"><span data-stu-id="90771-181">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="90771-182">Voor meer informatie over het Hallo kernels voor Jupyter-notebooks en vooraf gedefinieerde Hallo 'magics' die ze bieden, Zie [beschikbare Kernels voor Jupyter-notebooks met HDInsight Spark Linux-clusters in HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="90771-182">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="90771-183">Gegevensopname van een openbare blob</span><span class="sxs-lookup"><span data-stu-id="90771-183">Data ingestion from public blob</span></span>
<span data-ttu-id="90771-184">eerste stap van de Hallo in Hallo gegevens wetenschap proces tooingest Hallo gegevens toobe geanalyseerd van bronnen is waar is bevindt zich in uw gegevens te verkennen en modellering omgeving.</span><span class="sxs-lookup"><span data-stu-id="90771-184">hello first step in hello data science process is tooingest hello data toobe analyzed from sources where is resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="90771-185">Hallo-omgeving is Spark in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="90771-185">hello environment is Spark in this walkthrough.</span></span> <span data-ttu-id="90771-186">Deze sectie bevat Hallo code toocomplete een reeks taken:</span><span class="sxs-lookup"><span data-stu-id="90771-186">This section contains hello code toocomplete a series of tasks:</span></span>

* <span data-ttu-id="90771-187">Hallo gegevens voorbeeld toobe gemodelleerd opnemen</span><span class="sxs-lookup"><span data-stu-id="90771-187">ingest hello data sample toobe modeled</span></span>
* <span data-ttu-id="90771-188">Lees in invoergegevensset hello (opgeslagen als een bestand .tsv)</span><span class="sxs-lookup"><span data-stu-id="90771-188">read in hello input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="90771-189">indeling en schone Hallo-gegevens</span><span class="sxs-lookup"><span data-stu-id="90771-189">format and clean hello data</span></span>
* <span data-ttu-id="90771-190">maken en objecten (RDDs of gegevens frames) in het geheugen in de cache</span><span class="sxs-lookup"><span data-stu-id="90771-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="90771-191">registreren als een temp-tabel in SQL-context.</span><span class="sxs-lookup"><span data-stu-id="90771-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="90771-192">Hier volgt Hallo-code voor gegevensopname.</span><span class="sxs-lookup"><span data-stu-id="90771-192">Here is hello code for data ingestion.</span></span>

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

<span data-ttu-id="90771-193">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="90771-193">**OUTPUT:**</span></span>

<span data-ttu-id="90771-194">Tijd tooexecute boven cel: 51.72 seconden</span><span class="sxs-lookup"><span data-stu-id="90771-194">Time taken tooexecute above cell: 51.72 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="90771-195">Gegevensverkenning & visualisatie</span><span class="sxs-lookup"><span data-stu-id="90771-195">Data exploration & visualization</span></span>
<span data-ttu-id="90771-196">Zodra het Hallo-gegevens weer in Spark, is hello volgende stap in Hallo gegevens wetenschap proces toogain dieper inzicht Hallo gegevens via de exploratie en visualisatie.</span><span class="sxs-lookup"><span data-stu-id="90771-196">Once hello data has been brought into Spark, hello next step in hello data science process is toogain deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="90771-197">In deze sectie bekijken we Hallo taxi gegevens met behulp van SQL-query's en tekent Hallo target-variabelen en potentiële functies voor visuele controle.</span><span class="sxs-lookup"><span data-stu-id="90771-197">In this section, we examine hello taxi data using SQL queries and plot hello target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="90771-198">In het bijzonder uitzetten we Hallo frequentie van de passagiers tellingen in taxi reizen, Hallo frequentie van tip bedragen en hoe tips is afhankelijk van de hoeveelheid betaling en het type.</span><span class="sxs-lookup"><span data-stu-id="90771-198">Specifically, we plot hello frequency of passenger counts in taxi trips, hello frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a><span data-ttu-id="90771-199">Een histogram van passagiers aantal frequenties in voorbeeld van taxi reizen Hallo tekenen</span><span class="sxs-lookup"><span data-stu-id="90771-199">Plot a histogram of passenger count frequencies in hello sample of taxi trips</span></span>
<span data-ttu-id="90771-200">Deze code en de volgende codefragmenten SQL magische tooquery Hallo voorbeeld en lokale magische tooplot Hallo gegevens gebruiken.</span><span class="sxs-lookup"><span data-stu-id="90771-200">This code and subsequent snippets use SQL magic tooquery hello sample and local magic tooplot hello data.</span></span>

* <span data-ttu-id="90771-201">**SQL-magic (`%%sql`)** hello HDInsight PySpark-kernel ondersteunt eenvoudig inline HiveQL query's op Hallo sqlContext.</span><span class="sxs-lookup"><span data-stu-id="90771-201">**SQL magic (`%%sql`)** hello HDInsight PySpark kernel supports easy inline HiveQL queries against hello sqlContext.</span></span> <span data-ttu-id="90771-202">Hallo (-o naam_variabele) argument als een DataFrame Pandas op Hallo Jupyter server Hallo-uitvoer van de SQL-query Hallo zich blijft voordoen.</span><span class="sxs-lookup"><span data-stu-id="90771-202">hello (-o VARIABLE_NAME) argument persists hello output of hello SQL query as a Pandas DataFrame on hello Jupyter server.</span></span> <span data-ttu-id="90771-203">Dit betekent dat deze beschikbaar zijn in de lokale modus Hallo.</span><span class="sxs-lookup"><span data-stu-id="90771-203">This means it is available in hello local mode.</span></span>
* <span data-ttu-id="90771-204">Hallo  **`%%local` magic** is toorun code lokaal op Hallo Jupyter-server, waarop Hallo headnode van Hallo HDInsight-cluster wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="90771-204">hello **`%%local` magic** is used toorun code locally on hello Jupyter server, which is hello headnode of hello HDInsight cluster.</span></span> <span data-ttu-id="90771-205">Normaal gesproken gebruikt u `%%local` magische in combinatie met Hallo `%%sql` met -o parameter magic.</span><span class="sxs-lookup"><span data-stu-id="90771-205">Typically, you use `%%local` magic in conjunction with hello `%%sql` magic with -o parameter.</span></span> <span data-ttu-id="90771-206">Hallo -o parameter Hallo-uitvoer van lokaal Hallo SQL-query wilt behouden en vervolgens %% lokale magic zou de volgende set Hallo van code codefragment toorun lokaal tegen Hallo uitvoer Hallo SQL-query's die lokaal wordt bewaard</span><span class="sxs-lookup"><span data-stu-id="90771-206">hello -o parameter would persist hello output of hello SQL query locally and then %%local magic would trigger hello next set of code snippet toorun locally against hello output of hello SQL queries that is persisted locally</span></span>

<span data-ttu-id="90771-207">Hallo-uitvoer wordt automatisch weergegeven nadat u Hallo code uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="90771-207">hello output is automatically visualized after you run hello code.</span></span>

<span data-ttu-id="90771-208">Deze query haalt Hallo reizen op het aantal van de passagiers.</span><span class="sxs-lookup"><span data-stu-id="90771-208">This query retrieves hello trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # HIVEQL QUERY AGAINST hello sqlContext
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts 
    FROM taxi_train 
    WHERE passenger_count > 0 and passenger_count < 7 
    GROUP BY passenger_count 

<span data-ttu-id="90771-209">Deze code maakt een lokale gegevens tijdskader van Hallo query-uitvoer en Hallo van de gegevenspunten.</span><span class="sxs-lookup"><span data-stu-id="90771-209">This code creates a local data-frame from hello query output and plots hello data.</span></span> <span data-ttu-id="90771-210">Hallo `%%local` magic maakt een lokale gegevens-frame, `sqlResults`, die kan worden gebruikt voor het uitzetten van matplotlib.</span><span class="sxs-lookup"><span data-stu-id="90771-210">hello `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="90771-211">Deze PySpark-magic wordt meerdere malen gebruikt in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="90771-211">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="90771-212">Als Hallo hoeveelheid gegevens te groot is, moet u een steekproef nemen uit toocreate een gegevens-frame dat in het lokale geheugen past.</span><span class="sxs-lookup"><span data-stu-id="90771-212">If hello amount of data is large, you should sample toocreate a data-frame that can fit in local memory.</span></span>
> 
> 

    #CREATE LOCAL DATA-FRAME AND USE FOR MATPLOTLIB PLOTTING

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="90771-213">Hier volgt Hallo code tooplot Hallo reizen door passagiers aantallen</span><span class="sxs-lookup"><span data-stu-id="90771-213">Here is hello code tooplot hello trips by passenger counts</span></span>

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

<span data-ttu-id="90771-214">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="90771-214">**OUTPUT:**</span></span>

![De frequentie reis op het aantal passagiers](./media/machine-learning-data-science-spark-data-exploration-modeling/trip-freqency-by-passenger-count.png)

<span data-ttu-id="90771-216">U kunt kiezen uit verschillende soorten visualisaties (tabel-, cirkel, regel, gebied of balk) met behulp van Hallo **Type** menuknoppen in Hallo notebook.</span><span class="sxs-lookup"><span data-stu-id="90771-216">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using hello **Type** menu buttons in hello notebook.</span></span> <span data-ttu-id="90771-217">Hallo-balk tekent wordt hier weergegeven.</span><span class="sxs-lookup"><span data-stu-id="90771-217">hello Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="90771-218">Zet een histogram van de tip bedragen en hoe tip bedrag hangt af van de passagiers telling en het tarief bedragen.</span><span class="sxs-lookup"><span data-stu-id="90771-218">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="90771-219">Gebruik een SQL-query toosample-gegevens.</span><span class="sxs-lookup"><span data-stu-id="90771-219">Use a SQL query toosample data.</span></span>

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


<span data-ttu-id="90771-220">Deze codecel Hallo SQL-query toocreate drie waarnemingspunten Hallo gegevens gebruikt.</span><span class="sxs-lookup"><span data-stu-id="90771-220">This code cell uses hello SQL query toocreate three plots hello data.</span></span>

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


<span data-ttu-id="90771-221">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="90771-221">**OUTPUT:**</span></span> 

![Tip bedragdistributie](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-distribution.png)

![Hoeveelheid op het aantal passagiers Tip](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Tip bedrag door tarief bedrag](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="90771-225">Functie-engineering, transformatie en gegevens voorbereiding voor modellering</span><span class="sxs-lookup"><span data-stu-id="90771-225">Feature engineering, transformation and data preparation for modeling</span></span>
<span data-ttu-id="90771-226">Deze sectie wordt beschreven en vindt Hallo-code voor de procedures gebruikt tooprepare gegevens voor gebruik in ML-model.</span><span class="sxs-lookup"><span data-stu-id="90771-226">This section describes and provides hello code for procedures used tooprepare data for use in ML modeling.</span></span> <span data-ttu-id="90771-227">Er wordt weergegeven hoe toodo Hallo volgende taken:</span><span class="sxs-lookup"><span data-stu-id="90771-227">It shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="90771-228">Maakt een nieuwe functie met binning uur in verkeer tijd buckets</span><span class="sxs-lookup"><span data-stu-id="90771-228">Create a new feature by binning hours into traffic time buckets</span></span>
* <span data-ttu-id="90771-229">Index en categorische functies coderen</span><span class="sxs-lookup"><span data-stu-id="90771-229">Index and encode categorical features</span></span>
* <span data-ttu-id="90771-230">Gelabelde point-objecten voor invoer in ML functies maken</span><span class="sxs-lookup"><span data-stu-id="90771-230">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="90771-231">Onderliggende steekproeven van Hallo gegevens maken en deze te splitsen in trainings- en testdoeleinden sets</span><span class="sxs-lookup"><span data-stu-id="90771-231">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
* <span data-ttu-id="90771-232">Functie schalen</span><span class="sxs-lookup"><span data-stu-id="90771-232">Feature scaling</span></span>
* <span data-ttu-id="90771-233">Cacheobjecten in het geheugen</span><span class="sxs-lookup"><span data-stu-id="90771-233">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="90771-234">Maakt een nieuwe functie met binning uur in verkeer tijd buckets</span><span class="sxs-lookup"><span data-stu-id="90771-234">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="90771-235">Deze code laat zien hoe een nieuwe functie door uren in verkeer tijd binning toocreate tijdsintervallen en hoe toocache Hallo resulterende gegevensframe in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="90771-235">This code shows how toocreate a new feature by binning hours into traffic time buckets and then how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="90771-236">Flexibele gegevenssets gedistribueerd (RDDs) en gegevens frames herhaaldelijk gebruikt, leidt opslaan in cache tooimproved uitvoeringstijden.</span><span class="sxs-lookup"><span data-stu-id="90771-236">Where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly, caching leads tooimproved execution times.</span></span> <span data-ttu-id="90771-237">Dienovereenkomstig, we RDDs en gegevensframes cache in verschillende stadia in Hallo overzicht.</span><span class="sxs-lookup"><span data-stu-id="90771-237">Accordingly, we cache RDDs and data-frames at several stages in hello walkthrough.</span></span> 

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

<span data-ttu-id="90771-238">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="90771-238">**OUTPUT:**</span></span> 

<span data-ttu-id="90771-239">126050</span><span class="sxs-lookup"><span data-stu-id="90771-239">126050</span></span>

### <a name="index-and-encode-categorical-features-for-input-into-modeling-functions"></a><span data-ttu-id="90771-240">Index en het coderen van categorische functies voor invoer in het modelleren van functies</span><span class="sxs-lookup"><span data-stu-id="90771-240">Index and encode categorical features for input into modeling functions</span></span>
<span data-ttu-id="90771-241">Deze sectie wordt beschreven hoe tooindex of categorische functies voor invoer in Hallo modelleren functies coderen.</span><span class="sxs-lookup"><span data-stu-id="90771-241">This section shows how tooindex or encode categorical features for input into hello modeling functions.</span></span> <span data-ttu-id="90771-242">Hallo modelleren en functies van MLlib hebben functies met categorische invoergegevens toobe geïndexeerd of eerdere toouse gecodeerd voorspellen.</span><span class="sxs-lookup"><span data-stu-id="90771-242">hello modeling and predict functions of MLlib require features with categorical input data toobe indexed or encoded prior toouse.</span></span> <span data-ttu-id="90771-243">Afhankelijk van het Hallo-model of u kunt tooindex ze coderen op verschillende manieren:</span><span class="sxs-lookup"><span data-stu-id="90771-243">Depending on hello model, you need tooindex or encode them in different ways:</span></span>  

* <span data-ttu-id="90771-244">**Op basis van een structuur modellering** vereist categorieën toobe gecodeerd als numerieke waarden (bijvoorbeeld, een onderdeel met drie categorieën kan worden gecodeerd met 0, 1, 2).</span><span class="sxs-lookup"><span data-stu-id="90771-244">**Tree-based modeling** requires categories toobe encoded as numerical values (for example, a feature with three categories may be encoded with 0, 1, 2).</span></span> <span data-ttu-id="90771-245">Dit wordt geleverd door de MLlib [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) functie.</span><span class="sxs-lookup"><span data-stu-id="90771-245">This is provided by MLlib’s [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) function.</span></span> <span data-ttu-id="90771-246">Deze functie codeert een tekenreekskolom van de labels tooa kolom van het label indexen die zijn besteld op het label frequenties.</span><span class="sxs-lookup"><span data-stu-id="90771-246">This function encodes a string column of labels tooa column of label indices that are ordered by label frequencies.</span></span> <span data-ttu-id="90771-247">Hoewel geïndexeerd met numerieke waarden voor de invoer- en de verwerking van gegevens, op basis van een structuur Hallo-algoritmen opgegeven tootreat kunnen zijn op de juiste wijze als categorieën.</span><span class="sxs-lookup"><span data-stu-id="90771-247">Although indexed with numerical values for input and data handling, hello tree-based algorithms can be specified tootreat them appropriately as categories.</span></span> 
* <span data-ttu-id="90771-248">**Logistic en lineaire regressie modellen** vereisen een hot codering, where, bijvoorbeeld, een onderdeel met drie categorieën kan worden uitgebreid naar drie kolommen van de functie, waarbij elke met 0 of 1, afhankelijk van de categorie van een observatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="90771-248">**Logistic and Linear Regression models** require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="90771-249">MLlib biedt [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) werken toodo één hot codering.</span><span class="sxs-lookup"><span data-stu-id="90771-249">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function toodo one-hot encoding.</span></span> <span data-ttu-id="90771-250">Deze encoder wijst een kolom van een label indexen tooa kolom van de binaire aanvalsvectoren, met maximaal één one-waarde.</span><span class="sxs-lookup"><span data-stu-id="90771-250">This encoder maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="90771-251">Met deze codering kunt algoritmen die verwacht dat de numerieke waarden functies, zoals logistic regression toobe toegepast toocategorical functies.</span><span class="sxs-lookup"><span data-stu-id="90771-251">This encoding allows algorithms that expect numerical valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

<span data-ttu-id="90771-252">Hier volgt Hallo code tooindex en coderen categorische functies:</span><span class="sxs-lookup"><span data-stu-id="90771-252">Here is hello code tooindex and encode categorical features:</span></span>

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

<span data-ttu-id="90771-253">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="90771-253">**OUTPUT:**</span></span>

<span data-ttu-id="90771-254">Tijd tooexecute boven cel: 1.28 seconden</span><span class="sxs-lookup"><span data-stu-id="90771-254">Time taken tooexecute above cell: 1.28 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="90771-255">Gelabelde point-objecten voor invoer in ML functies maken</span><span class="sxs-lookup"><span data-stu-id="90771-255">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="90771-256">Deze sectie bevat de code die laat zien hoe tooindex categorische tekst gegevenstype als de gegevens van een gelabelde en deze te coderen zodat deze gebruikt tootrain en test MLlib logistic regression en andere classificatie-modellen worden kan.</span><span class="sxs-lookup"><span data-stu-id="90771-256">This section contains code that shows how tooindex categorical text data as a labeled point data type and encode it so that it can be used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="90771-257">Gelabelde point-objecten zijn robuuste gedistribueerd gegevenssets (RDD) geformatteerd op een manier die is vereist als de invoergegevens voor de meeste ML algoritmen in MLlib.</span><span class="sxs-lookup"><span data-stu-id="90771-257">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="90771-258">Een [punt gelabeld](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is een lokale vector, dense of sparse, die is gekoppeld aan een label/antwoord.</span><span class="sxs-lookup"><span data-stu-id="90771-258">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>  

<span data-ttu-id="90771-259">Deze sectie bevat de code die laat zien hoe tooindex categorische gegevens als een [punt gelabeld](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) gegevenstype en deze te coderen zodat deze gebruikt tootrain en test MLlib logistic regression en andere classificatie-modellen worden kan.</span><span class="sxs-lookup"><span data-stu-id="90771-259">This section contains code that shows how tooindex categorical text data as a [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) data type and encode it so that it can be used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="90771-260">Gelabelde point-objecten zijn robuuste gedistribueerd gegevenssets (RDD) die bestaan uit een label (doel/antwoord-variabele) en de functie vector.</span><span class="sxs-lookup"><span data-stu-id="90771-260">Labeled point objects are Resilient Distributed Datasets (RDD) consisting of a label (target/response variable) and feature vector.</span></span> <span data-ttu-id="90771-261">Deze indeling is nodig als invoer door veel ML algoritmen in MLlib.</span><span class="sxs-lookup"><span data-stu-id="90771-261">This format is needed as input by many ML algorithms in MLlib.</span></span>

<span data-ttu-id="90771-262">Hier volgt Hallo code tooindex en het coderen van tekstfuncties voor binaire classificatie.</span><span class="sxs-lookup"><span data-stu-id="90771-262">Here is hello code tooindex and encode text features for binary classification.</span></span>

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


<span data-ttu-id="90771-263">Hier volgt Hallo code tooencode en index categorische tekst-functies voor lineaire regressie-analyse.</span><span class="sxs-lookup"><span data-stu-id="90771-263">Here is hello code tooencode and index categorical text features for linear regression analysis.</span></span>

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


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="90771-264">Onderliggende steekproeven van Hallo gegevens maken en deze te splitsen in trainings- en testdoeleinden sets</span><span class="sxs-lookup"><span data-stu-id="90771-264">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
<span data-ttu-id="90771-265">Deze code maakt een willekeurige steekproeven van het Hallo-gegevens (25% wordt hier gebruikt).</span><span class="sxs-lookup"><span data-stu-id="90771-265">This code creates a random sampling of hello data (25% is used here).</span></span> <span data-ttu-id="90771-266">Hoewel dit niet vereist voor dit voorbeeld vanwege toohello grootte van de gegevensset hello, ziet u hoe u kunt een steekproef nemen hier zodat u weet hoe toouse voor uw eigen probleem wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="90771-266">Although it is not required for this example due toohello size of hello dataset, we demonstrate how you can sample here so you know how toouse it for your own problem when needed.</span></span> <span data-ttu-id="90771-267">Als voorbeelden groot zijn, kan dit aanzienlijke tijd tijdens de training modellen opslaan.</span><span class="sxs-lookup"><span data-stu-id="90771-267">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="90771-268">Naast splitsen we Hallo voorbeeld in trainings-onderdeel (hier 75%) en een test toouse deel (25% hier) in de classificatie en regressie modellering.</span><span class="sxs-lookup"><span data-stu-id="90771-268">Next we split hello sample into a training part (75% here) and a testing part (25% here) toouse in classification and regression modeling.</span></span>

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

<span data-ttu-id="90771-269">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="90771-269">**OUTPUT:**</span></span>

<span data-ttu-id="90771-270">Tijd tooexecute boven cel: 0,24 seconden</span><span class="sxs-lookup"><span data-stu-id="90771-270">Time taken tooexecute above cell: 0.24 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="90771-271">Functie schalen</span><span class="sxs-lookup"><span data-stu-id="90771-271">Feature scaling</span></span>
<span data-ttu-id="90771-272">Functie schaal, ook wel bekend als gegevensnormalisatie, weet u zeker dat functies met veel betaald waarden zijn niet opgegeven overmatige afwegen in objective Hallo-functie.</span><span class="sxs-lookup"><span data-stu-id="90771-272">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> <span data-ttu-id="90771-273">Hallo code voor het schalen van de functie maakt gebruik van Hallo [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale Hallo functies toounit variantie.</span><span class="sxs-lookup"><span data-stu-id="90771-273">hello code for feature scaling uses hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello features toounit variance.</span></span> <span data-ttu-id="90771-274">Het wordt geleverd door MLlib voor gebruik in lineaire regressie met stochastische kleurovergang Daalgradiënt (SGD), een populaire algoritme voor het trainen van een breed scala aan andere machine learning-modellen zoals overgegaan regressies of ondersteuning vector machines (SVM).</span><span class="sxs-lookup"><span data-stu-id="90771-274">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>

> [!NOTE]
> <span data-ttu-id="90771-275">We hebben gevonden Hallo LinearRegressionWithSGD algoritme toobe gevoelige toofeature schalen.</span><span class="sxs-lookup"><span data-stu-id="90771-275">We have found hello LinearRegressionWithSGD algorithm toobe sensitive toofeature scaling.</span></span>
> 
> 

<span data-ttu-id="90771-276">Hier volgt Hallo code tooscale variabelen voor gebruik met Hallo overgegaan lineaire SGD algoritme.</span><span class="sxs-lookup"><span data-stu-id="90771-276">Here is hello code tooscale variables for use with hello regularized linear SGD algorithm.</span></span>

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

<span data-ttu-id="90771-277">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="90771-277">**OUTPUT:**</span></span>

<span data-ttu-id="90771-278">Tijd tooexecute boven cel: 13.17 seconden</span><span class="sxs-lookup"><span data-stu-id="90771-278">Time taken tooexecute above cell: 13.17 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="90771-279">Cacheobjecten in het geheugen</span><span class="sxs-lookup"><span data-stu-id="90771-279">Cache objects in memory</span></span>
<span data-ttu-id="90771-280">Hallo-tijd die nodig is voor trainings- en testen van ML algoritmen kunnen worden verkleind door het opslaan in cache Hallo invoergegevens frame objecten die gebruikt worden voor classificatie, regressie, en functies geschaald.</span><span class="sxs-lookup"><span data-stu-id="90771-280">hello time taken for training and testing of ML algorithms can be reduced by caching hello input data frame objects used for classification, regression, and scaled features.</span></span>

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

<span data-ttu-id="90771-281">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="90771-281">**OUTPUT:**</span></span> 

<span data-ttu-id="90771-282">Tijd tooexecute boven cel: 0,15 seconden</span><span class="sxs-lookup"><span data-stu-id="90771-282">Time taken tooexecute above cell: 0.15 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="90771-283">Voorspellen of een tip wordt betaald met binaire classificatie modellen</span><span class="sxs-lookup"><span data-stu-id="90771-283">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="90771-284">Deze sectie wordt beschreven hoe gebruik drie modellen voor Hallo binaire classificatietaak van het voorspellen van al dan niet een tip voor een reis taxi wordt betaald.</span><span class="sxs-lookup"><span data-stu-id="90771-284">This section shows how use three models for hello binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="90771-285">Hallo-modellen die zijn gepresenteerd zijn:</span><span class="sxs-lookup"><span data-stu-id="90771-285">hello models presented are:</span></span>

* <span data-ttu-id="90771-286">Logistic regression overgegaan</span><span class="sxs-lookup"><span data-stu-id="90771-286">Regularized logistic regression</span></span> 
* <span data-ttu-id="90771-287">Willekeurige forestmodel</span><span class="sxs-lookup"><span data-stu-id="90771-287">Random forest model</span></span>
* <span data-ttu-id="90771-288">Kleurovergang prestatieverbetering structuren</span><span class="sxs-lookup"><span data-stu-id="90771-288">Gradient Boosting Trees</span></span>

<span data-ttu-id="90771-289">Elk model bouwen sectie code opgedeeld in stappen:</span><span class="sxs-lookup"><span data-stu-id="90771-289">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="90771-290">**Training model** gegevens met één parameterset</span><span class="sxs-lookup"><span data-stu-id="90771-290">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="90771-291">**Evaluatie model** op een test-gegevensset met metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="90771-291">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="90771-292">**Opslaan van model** in blob voor toekomstige verbruik</span><span class="sxs-lookup"><span data-stu-id="90771-292">**Saving model** in blob for future consumption</span></span>

### <a name="classification-using-logistic-regression"></a><span data-ttu-id="90771-293">Classificatie met logistic regression</span><span class="sxs-lookup"><span data-stu-id="90771-293">Classification using logistic regression</span></span>
<span data-ttu-id="90771-294">Hallo-code in deze sectie ziet u hoe tootrain, evalueren en opslaan van een regressiemodel logistic met [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) die voorspelt al dan niet een tip voor een reis in Hallo NYC taxi reis en tarief gegevensset wordt betaald.</span><span class="sxs-lookup"><span data-stu-id="90771-294">hello code in this section shows how tootrain, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

<span data-ttu-id="90771-295">**Hallo logistic regression-model met k/l en hyperparameter sweeping trainen**</span><span class="sxs-lookup"><span data-stu-id="90771-295">**Train hello logistic regression model using CV and hyperparameter sweeping**</span></span>

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


<span data-ttu-id="90771-296">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="90771-296">**OUTPUT:**</span></span> 

<span data-ttu-id="90771-297">Coëfficiënten: [0.0082065285375,-0.0223675576104,-0.0183812028036, -3.48124578069e-05,-0.00247646947233,-0.00165897881503, 0.0675394837328,-0.111823113101,-0.324609912762,-0.204549780032,-1.36499216354, 0.591088507921,-0.664263411392,-1.00439726852, 3.46567827545,-3.51025855172,-0.0471341112232,-0.043521833294, 0.000243375810385, 0.054518719222]</span><span class="sxs-lookup"><span data-stu-id="90771-297">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="90771-298">Intercept:-0.0111216486893</span><span class="sxs-lookup"><span data-stu-id="90771-298">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="90771-299">Tijd tooexecute boven cel: 14.43 seconden</span><span class="sxs-lookup"><span data-stu-id="90771-299">Time taken tooexecute above cell: 14.43 seconds</span></span>

<span data-ttu-id="90771-300">**Hallo binaire classificatie model met standaard metrische gegevens evalueren**</span><span class="sxs-lookup"><span data-stu-id="90771-300">**Evaluate hello binary classification model with standard metrics**</span></span>

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

<span data-ttu-id="90771-301">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="90771-301">**OUTPUT:**</span></span> 

<span data-ttu-id="90771-302">Gebied onder PR 0.985297691373 =</span><span class="sxs-lookup"><span data-stu-id="90771-302">Area under PR = 0.985297691373</span></span>

<span data-ttu-id="90771-303">Gebied onder ROC 0.983714670256 =</span><span class="sxs-lookup"><span data-stu-id="90771-303">Area under ROC = 0.983714670256</span></span>

<span data-ttu-id="90771-304">Samenvattende statistieken</span><span class="sxs-lookup"><span data-stu-id="90771-304">Summary Stats</span></span>

<span data-ttu-id="90771-305">Precisie 0.984304060189 =</span><span class="sxs-lookup"><span data-stu-id="90771-305">Precision = 0.984304060189</span></span>

<span data-ttu-id="90771-306">Intrekken 0.984304060189 =</span><span class="sxs-lookup"><span data-stu-id="90771-306">Recall = 0.984304060189</span></span>

<span data-ttu-id="90771-307">F1 Score 0.984304060189 =</span><span class="sxs-lookup"><span data-stu-id="90771-307">F1 Score = 0.984304060189</span></span>

<span data-ttu-id="90771-308">Tijd tooexecute boven cel: 57.61 seconden</span><span class="sxs-lookup"><span data-stu-id="90771-308">Time taken tooexecute above cell: 57.61 seconds</span></span>

<span data-ttu-id="90771-309">**Hallo ROC-curve wordt getekend.**</span><span class="sxs-lookup"><span data-stu-id="90771-309">**Plot hello ROC curve.**</span></span>

<span data-ttu-id="90771-310">Hallo *predictionAndLabelsDF* is geregistreerd als een tabel, *tmp_results*, in de vorige cel Hallo.</span><span class="sxs-lookup"><span data-stu-id="90771-310">hello *predictionAndLabelsDF* is registered as a table, *tmp_results*, in hello previous cell.</span></span> <span data-ttu-id="90771-311">*tmp_results* kunnen worden gebruikt toodo query's en resultaten in Hallo sqlResults data-frame voor het uitzetten van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="90771-311">*tmp_results* can be used toodo queries and output results into hello sqlResults data-frame for plotting.</span></span> <span data-ttu-id="90771-312">Hier volgt Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="90771-312">Here is hello code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="90771-313">Hier volgt Hallo code toomake voorspellingen en tekent Hallo ROC-curve.</span><span class="sxs-lookup"><span data-stu-id="90771-313">Here is hello code toomake predictions and plot hello ROC-curve.</span></span>

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


<span data-ttu-id="90771-314">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="90771-314">**OUTPUT:**</span></span>

![Logistic regression ROC curve.png](./media/machine-learning-data-science-spark-data-exploration-modeling/logistic-regression-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="90771-316">Classificatie van willekeurige forest</span><span class="sxs-lookup"><span data-stu-id="90771-316">Random forest classification</span></span>
<span data-ttu-id="90771-317">Hallo-code in deze sectie laat zien hoe tootrain, evalueren en opslaan van een willekeurige forestmodel die voorspelt al dan niet een tip voor een reis in Hallo NYC taxi reis en tarief gegevensset wordt betaald.</span><span class="sxs-lookup"><span data-stu-id="90771-317">hello code in this section shows how tootrain, evaluate, and save a random forest model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

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

<span data-ttu-id="90771-318">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="90771-318">**OUTPUT:**</span></span>

<span data-ttu-id="90771-319">Gebied onder ROC 0.985297691373 =</span><span class="sxs-lookup"><span data-stu-id="90771-319">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="90771-320">Tijd tooexecute boven cel: 31.09 seconden</span><span class="sxs-lookup"><span data-stu-id="90771-320">Time taken tooexecute above cell: 31.09 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="90771-321">Kleurovergang prestatieverbetering structuren classificatie</span><span class="sxs-lookup"><span data-stu-id="90771-321">Gradient boosting trees classification</span></span>
<span data-ttu-id="90771-322">Hallo-code in deze sectie laat zien hoe tootrain, evalueren en een kleurovergang prestatieverbetering structuren model die al dan niet een tip voor een reis in Hallo NYC taxi reis en tarief gegevensset wordt betaald voorspelt opslaat.</span><span class="sxs-lookup"><span data-stu-id="90771-322">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

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


<span data-ttu-id="90771-323">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="90771-323">**OUTPUT:**</span></span>

<span data-ttu-id="90771-324">Gebied onder ROC 0.985297691373 =</span><span class="sxs-lookup"><span data-stu-id="90771-324">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="90771-325">Tijd tooexecute boven cel: 19.76 seconden</span><span class="sxs-lookup"><span data-stu-id="90771-325">Time taken tooexecute above cell: 19.76 seconds</span></span>

## <a name="predict-tip-amounts-for-taxi-trips-with-regression-models"></a><span data-ttu-id="90771-326">Tip bedragen voor taxi reizen met regressie modellen voorspellen</span><span class="sxs-lookup"><span data-stu-id="90771-326">Predict tip amounts for taxi trips with regression models</span></span>
<span data-ttu-id="90771-327">Deze sectie wordt beschreven hoe gebruik drie modellen voor Hallo regressie taak van het voorspellen van Hallo Hallo tip betaald taxi reis op basis van andere functies tip hoeveelheid.</span><span class="sxs-lookup"><span data-stu-id="90771-327">This section shows how use three models for hello regression task of predicting hello amount of hello tip paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="90771-328">Hallo-modellen die zijn gepresenteerd zijn:</span><span class="sxs-lookup"><span data-stu-id="90771-328">hello models presented are:</span></span>

* <span data-ttu-id="90771-329">Lineaire regressie overgegaan</span><span class="sxs-lookup"><span data-stu-id="90771-329">Regularized linear regression</span></span>
* <span data-ttu-id="90771-330">Willekeurige forest</span><span class="sxs-lookup"><span data-stu-id="90771-330">Random forest</span></span>
* <span data-ttu-id="90771-331">Kleurovergang prestatieverbetering structuren</span><span class="sxs-lookup"><span data-stu-id="90771-331">Gradient Boosting Trees</span></span>

<span data-ttu-id="90771-332">Deze modellen zijn in Hallo inleiding beschreven.</span><span class="sxs-lookup"><span data-stu-id="90771-332">These models were described in hello introduction.</span></span> <span data-ttu-id="90771-333">Elk model bouwen sectie code opgedeeld in stappen:</span><span class="sxs-lookup"><span data-stu-id="90771-333">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="90771-334">**Training model** gegevens met één parameterset</span><span class="sxs-lookup"><span data-stu-id="90771-334">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="90771-335">**Evaluatie model** op een test-gegevensset met metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="90771-335">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="90771-336">**Opslaan van model** in blob voor toekomstige verbruik</span><span class="sxs-lookup"><span data-stu-id="90771-336">**Saving model** in blob for future consumption</span></span>

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="90771-337">Lineaire regressie met SGD</span><span class="sxs-lookup"><span data-stu-id="90771-337">Linear regression with SGD</span></span>
<span data-ttu-id="90771-338">Hallo code in deze sectie toont hoe toouse geschaald functies tootrain een lineaire regressie die stochastische kleurovergang daalgradiënt (SGD), kunnen worden gebruikt en hoe tooscore, evalueren en Hallo-model opslaan in Azure Blob Storage (WASB).</span><span class="sxs-lookup"><span data-stu-id="90771-338">hello code in this section shows how toouse scaled features tootrain a linear regression that uses stochastic gradient descent (SGD) for optimization, and how tooscore, evaluate, and save hello model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="90771-339">In onze ervaring kunnen er problemen met het Hallo-convergentie van LinearRegressionWithSGD modellen en parameters moeten toobe gewijzigd/geoptimaliseerd zorgvuldig voor het verkrijgen van een geldig model.</span><span class="sxs-lookup"><span data-stu-id="90771-339">In our experience, there can be issues with hello convergence of LinearRegressionWithSGD models, and parameters need toobe changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="90771-340">Schalen van variabelen aanzienlijk helpt bij convergentie.</span><span class="sxs-lookup"><span data-stu-id="90771-340">Scaling of variables significantly helps with convergence.</span></span> 
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

<span data-ttu-id="90771-341">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="90771-341">**OUTPUT:**</span></span>

<span data-ttu-id="90771-342">Coëfficiënten: [0.00457675809917,-0.0226314167349,-0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981,-0.000987181489428,-0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995,- 0.00990211159703,-0.00637410344522, 0.545083566179,-0.536756072402, 0.0105762393099,-0.0130117577055, 0.0129304737772,-0.00171065945959]</span><span class="sxs-lookup"><span data-stu-id="90771-342">Coefficients: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]</span></span>

<span data-ttu-id="90771-343">Intercept: 0.853872718283</span><span class="sxs-lookup"><span data-stu-id="90771-343">Intercept: 0.853872718283</span></span>

<span data-ttu-id="90771-344">RMSE 1.24190115863 =</span><span class="sxs-lookup"><span data-stu-id="90771-344">RMSE = 1.24190115863</span></span>

<span data-ttu-id="90771-345">R sqr 0.608017146081 =</span><span class="sxs-lookup"><span data-stu-id="90771-345">R-sqr = 0.608017146081</span></span>

<span data-ttu-id="90771-346">Tijd tooexecute boven cel: 58,42 seconden</span><span class="sxs-lookup"><span data-stu-id="90771-346">Time taken tooexecute above cell: 58.42 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="90771-347">Willekeurige Forest regressie</span><span class="sxs-lookup"><span data-stu-id="90771-347">Random Forest regression</span></span>
<span data-ttu-id="90771-348">Hallo-code in deze sectie laat zien hoe tootrain, evalueren en een willekeurige forest regressie die tip bedrag voor Hallo NYC taxi reis gegevens voorspelt opslaan.</span><span class="sxs-lookup"><span data-stu-id="90771-348">hello code in this section shows how tootrain, evaluate, and save a random forest regression that predicts tip amount for hello NYC taxi trip data.</span></span>

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

<span data-ttu-id="90771-349">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="90771-349">**OUTPUT:**</span></span>

<span data-ttu-id="90771-350">RMSE 0.891209218139 =</span><span class="sxs-lookup"><span data-stu-id="90771-350">RMSE = 0.891209218139</span></span>

<span data-ttu-id="90771-351">R sqr 0.759661334921 =</span><span class="sxs-lookup"><span data-stu-id="90771-351">R-sqr = 0.759661334921</span></span>

<span data-ttu-id="90771-352">Tijd tooexecute boven cel: 49.21 seconden</span><span class="sxs-lookup"><span data-stu-id="90771-352">Time taken tooexecute above cell: 49.21 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="90771-353">Kleurovergang prestatieverbetering structuren regressie</span><span class="sxs-lookup"><span data-stu-id="90771-353">Gradient boosting trees regression</span></span>
<span data-ttu-id="90771-354">Hallo-code in deze sectie laat zien hoe tootrain, evalueren en een kleurovergang prestatieverbetering structuren model die tip bedrag voor Hallo NYC taxi reis gegevens voorspelt opslaat.</span><span class="sxs-lookup"><span data-stu-id="90771-354">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts tip amount for hello NYC taxi trip data.</span></span>

<span data-ttu-id="90771-355">** Trainen en evalueren **</span><span class="sxs-lookup"><span data-stu-id="90771-355">**Train and evaluate **</span></span>

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

<span data-ttu-id="90771-356">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="90771-356">**OUTPUT:**</span></span>

<span data-ttu-id="90771-357">RMSE 0.908473148639 =</span><span class="sxs-lookup"><span data-stu-id="90771-357">RMSE = 0.908473148639</span></span>

<span data-ttu-id="90771-358">R sqr 0.753835096681 =</span><span class="sxs-lookup"><span data-stu-id="90771-358">R-sqr = 0.753835096681</span></span>

<span data-ttu-id="90771-359">Tijd tooexecute boven cel: 34.52 seconden</span><span class="sxs-lookup"><span data-stu-id="90771-359">Time taken tooexecute above cell: 34.52 seconds</span></span>

<span data-ttu-id="90771-360">**Tekenen**</span><span class="sxs-lookup"><span data-stu-id="90771-360">**Plot**</span></span>

<span data-ttu-id="90771-361">*tmp_results* is geregistreerd als een Hive-tabel in de vorige cel Hallo.</span><span class="sxs-lookup"><span data-stu-id="90771-361">*tmp_results* is registered as a Hive table in hello previous cell.</span></span> <span data-ttu-id="90771-362">Resultaten van de tabel Hallo worden uitgevoerd in Hallo *sqlResults* tijdskader voor het uitzetten van gegevens.</span><span class="sxs-lookup"><span data-stu-id="90771-362">Results from hello table are output into hello *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="90771-363">Dit is de code Hallo</span><span class="sxs-lookup"><span data-stu-id="90771-363">Here is hello code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results

<span data-ttu-id="90771-364">Hier volgt Hallo code tooplot Hallo gegevens met behulp van Hallo Jupyter-server.</span><span class="sxs-lookup"><span data-stu-id="90771-364">Here is hello code tooplot hello data using hello Jupyter server.</span></span>

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


<span data-ttu-id="90771-365">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="90771-365">**OUTPUT:**</span></span>

![Werkelijke-vs-voorspeld-tip-bedragen](./media/machine-learning-data-science-spark-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="clean-up-objects-from-memory"></a><span data-ttu-id="90771-367">Opschonen van objecten uit het geheugen</span><span class="sxs-lookup"><span data-stu-id="90771-367">Clean up objects from memory</span></span>
<span data-ttu-id="90771-368">Gebruik `unpersist()` toodelete objecten in het cachegeheugen opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="90771-368">Use `unpersist()` toodelete objects cached in memory.</span></span>

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


## <a name="record-storage-locations-of-hello-models-for-consumption-and-scoring"></a><span data-ttu-id="90771-369">Record opslaglocaties van Hallo modellen voor gebruiks- en score berekenen</span><span class="sxs-lookup"><span data-stu-id="90771-369">Record storage locations of hello models for consumption and scoring</span></span>
<span data-ttu-id="90771-370">tooconsume en score een onafhankelijke gegevensset beschreven in Hallo [Score en evalueren van Spark is gebouwd machine learning-modellen](machine-learning-data-science-spark-model-consumption.md) onderwerp, moet u toocopy en plak deze met Hallo opgeslagen modellen hier in Hallo gemaakt bestandsnamen Jupyter-notebook verbruik.</span><span class="sxs-lookup"><span data-stu-id="90771-370">tooconsume and score an independent dataset described in hello [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) topic, you need toocopy and paste these file names containing hello saved models created here into hello Consumption Jupyter notebook.</span></span> <span data-ttu-id="90771-371">Hier volgt Hallo code tooprint uit Hallo paden toomodel bestanden u er moet.</span><span class="sxs-lookup"><span data-stu-id="90771-371">Here is hello code tooprint out hello paths toomodel files you need there.</span></span>

    # MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="90771-372">**UITVOER**</span><span class="sxs-lookup"><span data-stu-id="90771-372">**OUTPUT**</span></span>

<span data-ttu-id="90771-373">logisticRegFileLoc = modelDir + 'LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568'</span><span class="sxs-lookup"><span data-stu-id="90771-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span></span>

<span data-ttu-id="90771-374">linearRegFileLoc = modelDir + 'LinearRegressionWithSGD_2016-05-0317_05_21.577773'</span><span class="sxs-lookup"><span data-stu-id="90771-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span></span>

<span data-ttu-id="90771-375">randomForestClassificationFileLoc = modelDir + 'RandomForestClassification_2016-05-0317_04_11.950206'</span><span class="sxs-lookup"><span data-stu-id="90771-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span></span>

<span data-ttu-id="90771-376">randomForestRegFileLoc = modelDir + 'RandomForestRegression_2016-05-0317_06_08.723736'</span><span class="sxs-lookup"><span data-stu-id="90771-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span></span>

<span data-ttu-id="90771-377">BoostedTreeClassificationFileLoc = modelDir + 'GradientBoostingTreeClassification_2016-05-0317_04_36.346583'</span><span class="sxs-lookup"><span data-stu-id="90771-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span></span>

<span data-ttu-id="90771-378">BoostedTreeRegressionFileLoc = modelDir + 'GradientBoostingTreeRegression_2016-05-0317_06_51.737282'</span><span class="sxs-lookup"><span data-stu-id="90771-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span></span>

## <a name="whats-next"></a><span data-ttu-id="90771-379">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="90771-379">What's next?</span></span>
<span data-ttu-id="90771-380">Nu u regressie en classificatie modellen met Hallo Spark MlLib hebt gemaakt, bent u klaar toolearn hoe tooscore en evalueren van deze modellen.</span><span class="sxs-lookup"><span data-stu-id="90771-380">Now that you have created regression and classification models with hello Spark MlLib, you are ready toolearn how tooscore and evaluate these models.</span></span> <span data-ttu-id="90771-381">Hallo geavanceerde gegevensverkenning en laptop dives diepere naar kruisvalidatie, hyper-parameter inclusief modelleren verstrekkende en model van de evaluatie.</span><span class="sxs-lookup"><span data-stu-id="90771-381">hello advanced data exploration and modeling notebook dives deeper into including cross-validation, hyper-parameter sweeping, and model evaluation.</span></span> 

<span data-ttu-id="90771-382">**Model verbruik:** toolearn hoe tooscore en evalueren Hallo classificatie en regressie modellen in dit onderwerp hebt gemaakt, Zie [Score en evalueren van Spark is gebouwd machine learning-modellen](machine-learning-data-science-spark-model-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="90771-382">**Model consumption:** toolearn how tooscore and evaluate hello classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

<span data-ttu-id="90771-383">**Kruisvalidatie en hyperparameter sweeping**: Zie [geavanceerde gegevensverkenning en modellering met Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) over de manier waarop modellen kunnen getraind met behulp van kruisvalidatie en hyper-parameter sweeping</span><span class="sxs-lookup"><span data-stu-id="90771-383">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping</span></span>

