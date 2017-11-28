---
title: Gegevensverkenning en modellering met Spark | Microsoft Docs
description: De gegevens te verkennen en modellering mogelijkheden van de toolkit MLlib Spark op Azure gepresenteerd.
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
ms.openlocfilehash: 711407f7dd9e6d442e3f04a23962487f4808e8e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="data-exploration-and-modeling-with-spark"></a><span data-ttu-id="5e34e-103">Met Spark gegevens verkennen en modelleren</span><span class="sxs-lookup"><span data-stu-id="5e34e-103">Data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="5e34e-104">In dit scenario worden gebruikt voor gegevensverkenning HDInsight Spark en binaire classificatie en taken van een steekproef van de NYC modelleren regressie taxi reis en ritbedrag 2013 gegevensset.</span><span class="sxs-lookup"><span data-stu-id="5e34e-104">This walkthrough uses HDInsight Spark to do data exploration and binary classification and regression modeling tasks on a sample of the NYC taxi trip and fare 2013 dataset.</span></span>  <span data-ttu-id="5e34e-105">Dit leidt u door de stappen van de [gegevens wetenschap proces](http://aka.ms/datascienceprocess)end-to- end, met behulp van een HDInsight Spark-cluster voor verwerking en Azure blobs voor het opslaan van de gegevens en de modellen.</span><span class="sxs-lookup"><span data-stu-id="5e34e-105">It walks you through the steps of the [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs to store the data and the models.</span></span> <span data-ttu-id="5e34e-106">Het proces wordt verkend en gebracht van een Azure Storage-Blob gegevens visualiseren en vervolgens worden de gegevens voor het bouwen van voorspellende modellen voorbereid.</span><span class="sxs-lookup"><span data-stu-id="5e34e-106">The process explores and visualizes data brought in from an Azure Storage Blob and then prepares the data to build predictive models.</span></span> <span data-ttu-id="5e34e-107">Deze modellen zijn build binaire classificatie en regressie modellering taken uitvoeren met de toolkit Spark MLlib.</span><span class="sxs-lookup"><span data-stu-id="5e34e-107">These models are build using the Spark MLlib toolkit to do binary classification and regression modeling tasks.</span></span>

* <span data-ttu-id="5e34e-108">De **binaire classificatie** taak is om te voorspellen of een tip voor de reis wordt betaald.</span><span class="sxs-lookup"><span data-stu-id="5e34e-108">The **binary classification** task is to predict whether or not a tip is paid for the trip.</span></span> 
* <span data-ttu-id="5e34e-109">De **regressie** taak is het voorspellen van de hoeveelheid de tip op basis van andere tip-functies.</span><span class="sxs-lookup"><span data-stu-id="5e34e-109">The **regression** task is to predict the amount of the tip based on other tip features.</span></span> 

<span data-ttu-id="5e34e-110">De modellen we gebruiken omvatten logistic en lineaire regressie, willekeurige forests en kleurovergang gestimuleerd structuren:</span><span class="sxs-lookup"><span data-stu-id="5e34e-110">The models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="5e34e-111">[Lineaire regressie met SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is een lineair regressiemodel die gebruikmaakt van een methode stochastische kleurovergang Daalgradiënt (SGD) en voor optimalisatie en het onderdeel schalen om te voorspellen van de bedragen tip betaald.</span><span class="sxs-lookup"><span data-stu-id="5e34e-111">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling to predict the tip amounts paid.</span></span> 
* <span data-ttu-id="5e34e-112">[Logistic regression met LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) of regressie 'logit', is een regressiemodel dat kan worden gebruikt wanneer de afhankelijke variabele categorische doen gegevensclassificatie is.</span><span class="sxs-lookup"><span data-stu-id="5e34e-112">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when the dependent variable is categorical to do data classification.</span></span> <span data-ttu-id="5e34e-113">LBFGS is een quasi toegepast optimalisatie-algoritme dat benadert de Broyden – Fletcher – Goldfarb – Shanno (BFGS)-algoritme met een beperkte hoeveelheid computergeheugen en die wordt veel gebruikt in machine learning.</span><span class="sxs-lookup"><span data-stu-id="5e34e-113">LBFGS is a quasi-Newton optimization algorithm that approximates the Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="5e34e-114">[Willekeurige forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) ensembles van beslissingsstructuren zijn.</span><span class="sxs-lookup"><span data-stu-id="5e34e-114">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="5e34e-115">Ze combineren veel beslissingsstructuren om het risico te beperken.</span><span class="sxs-lookup"><span data-stu-id="5e34e-115">They combine many decision trees to reduce the risk of overfitting.</span></span> <span data-ttu-id="5e34e-116">Willekeurige forests worden gebruikt voor regressie en classificatie en categorische functies kunnen verwerken en kunnen worden uitgebreid naar de instelling multiklassen classificatie.</span><span class="sxs-lookup"><span data-stu-id="5e34e-116">Random forests are used for regression and classification and can handle categorical features and can be extended to the multiclass classification setting.</span></span> <span data-ttu-id="5e34e-117">Ze hoeven niet functie schalen en kunnen niet met mogelijkheid tot vastleggen en interacties functie zijn.</span><span class="sxs-lookup"><span data-stu-id="5e34e-117">They do not require feature scaling and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="5e34e-118">Willekeurige forests zijn een van de meest succesvolle machine learning-modellen voor de indeling en regressie.</span><span class="sxs-lookup"><span data-stu-id="5e34e-118">Random forests are one of the most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="5e34e-119">[Verloop boosted structuren](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) ensembles van beslissingsstructuren zijn.</span><span class="sxs-lookup"><span data-stu-id="5e34e-119">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="5e34e-120">GBTs training beslissingsstructuren iteratief aan een functie gegevensverlies te minimaliseren.</span><span class="sxs-lookup"><span data-stu-id="5e34e-120">GBTs train decision trees iteratively to minimize a loss function.</span></span> <span data-ttu-id="5e34e-121">GBTs worden gebruikt voor regressie en classificatie en categorische functies kan verwerken, hoeven niet functie schalen en kunnen niet met mogelijkheid tot vastleggen en interacties functie.</span><span class="sxs-lookup"><span data-stu-id="5e34e-121">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="5e34e-122">Ze kunnen ook worden gebruikt in een setting multiklasse classificatie.</span><span class="sxs-lookup"><span data-stu-id="5e34e-122">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="5e34e-123">De stappen modellering ook bevatten code waarin wordt getoond hoe te trainen, evalueren en opslaan van elk type model.</span><span class="sxs-lookup"><span data-stu-id="5e34e-123">The modeling steps also contain code showing how to train, evaluate, and save each type of model.</span></span> <span data-ttu-id="5e34e-124">Code van de oplossing en weergeven van de relevante waarnemingspunten is Python gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5e34e-124">Python has been used to code the solution and to show the relevant plots.</span></span>   

> [!NOTE]
> <span data-ttu-id="5e34e-125">Hoewel de toolkit Spark MLlib is ontworpen om te werken op grote gegevenssets, wordt hier een voorbeeld van een relatief klein (ongeveer 30 Mb met behulp van 170K rijen, ongeveer 0,1% van de oorspronkelijke gegevensset van de NYC) gebruikt voor het gemak.</span><span class="sxs-lookup"><span data-stu-id="5e34e-125">Although the Spark MLlib toolkit is designed to work on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of the original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="5e34e-126">De hier opgegeven oefening efficiënt (in ongeveer 10 minuten) op een HDInsight-cluster met 2 worker-knooppunten wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5e34e-126">The exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="5e34e-127">De dezelfde code, met kleine wijzigingen kan worden gebruikt voor het verwerken van grotere gegevenssets-wordt met de juiste wijzigingen voor het cachen van gegevens in het geheugen en het wijzigen van de clustergrootte.</span><span class="sxs-lookup"><span data-stu-id="5e34e-127">The same code, with minor modifications, can be used to process larger data-sets, with appropriate modifications for caching data in memory and changing the cluster size.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="5e34e-128">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5e34e-128">Prerequisites</span></span>
<span data-ttu-id="5e34e-129">U moet een Azure-account en een 1.6 Spark (of Spark 2.0) HDInsight-cluster voor dit scenario.</span><span class="sxs-lookup"><span data-stu-id="5e34e-129">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster to complete this walkthrough.</span></span> <span data-ttu-id="5e34e-130">Zie de [overzicht van Gegevenswetenschap met Spark op Azure HDInsight](machine-learning-data-science-spark-overview.md) voor instructies voor het voldoen aan deze eisen.</span><span class="sxs-lookup"><span data-stu-id="5e34e-130">See the [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how to satisfy these requirements.</span></span> <span data-ttu-id="5e34e-131">Dit onderwerp bevat ook een beschrijving van de NYC 2013 Taxi gegevens hier gebruikt en instructies over het uitvoeren van code van een Jupyter-notebook in Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="5e34e-131">That topic also contains a description of the NYC 2013 Taxi data used here and instructions on how to execute code from a Jupyter notebook on the Spark cluster.</span></span> 

## <a name="spark-clusters-and-notebooks"></a><span data-ttu-id="5e34e-132">Spark-clusters en laptops</span><span class="sxs-lookup"><span data-stu-id="5e34e-132">Spark clusters and notebooks</span></span>
<span data-ttu-id="5e34e-133">Instellingsstappen en code vindt u in dit scenario voor het gebruik van een HDInsight Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="5e34e-133">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="5e34e-134">Maar Jupyter-notebooks zijn opgegeven voor zowel HDInsight Spark 1.6 en 2.0 Spark-clusters.</span><span class="sxs-lookup"><span data-stu-id="5e34e-134">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="5e34e-135">Een beschrijving van de laptops en koppelingen naar deze vindt u in de [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) voor de GitHub-opslagplaats met deze.</span><span class="sxs-lookup"><span data-stu-id="5e34e-135">A description of the notebooks and links to them are provided in the [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for the GitHub repository containing them.</span></span> <span data-ttu-id="5e34e-136">Bovendien moet de code hier en in de gekoppelde laptops is algemeen en moet werken op een Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="5e34e-136">Moreover, the code here and in the linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="5e34e-137">Als u HDInsight Spark niet gebruikt, is het mogelijk dat de cluster-installatie en beheer stappen enigszins afwijken van wat hier moet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5e34e-137">If you are not using HDInsight Spark, the cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="5e34e-138">Voor het gemak zijn hier de koppelingen naar de Jupyter-notebooks voor Spark 1.6 (om te worden uitgevoerd in de pySpark-kernel van de server Jupyter-Notebook) en Spark 2.0 (om te worden uitgevoerd in de kernel pySpark3 van de server Jupyter-Notebook):</span><span class="sxs-lookup"><span data-stu-id="5e34e-138">For convenience, here are the links to the Jupyter notebooks for Spark 1.6 (to be run in the pySpark kernel of the Jupyter Notebook server) and  Spark 2.0 (to be run in the pySpark3 kernel of the Jupyter Notebook server):</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="5e34e-139">Spark 1.6 laptops</span><span class="sxs-lookup"><span data-stu-id="5e34e-139">Spark 1.6 notebooks</span></span>

<span data-ttu-id="5e34e-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): bevat informatie over het uitvoeren van gegevensverkenning modelleren en batchscoreberekening met diverse verschillende algoritmen.</span><span class="sxs-lookup"><span data-stu-id="5e34e-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): Provides information on how to perform data exploration, modeling, and scoring with several different algorithms.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="5e34e-141">Spark 2.0-laptops</span><span class="sxs-lookup"><span data-stu-id="5e34e-141">Spark 2.0 notebooks</span></span>
<span data-ttu-id="5e34e-142">De regressie en classificatie taken die zijn geïmplementeerd met een 2.0 Spark-cluster in afzonderlijke notitieblokken zijn en de classificatie-notebook gebruikt een andere gegevensset:</span><span class="sxs-lookup"><span data-stu-id="5e34e-142">The regression and classification tasks that are implemented using a Spark 2.0 cluster are in separate notebooks and the classification notebook uses a different data set:</span></span>

- <span data-ttu-id="5e34e-143">[Spark2.0-pySpark3-machine-Learning-Data-Science-Spark-Advanced-Data-Exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): dit bestand bevat informatie over het uitvoeren van gegevensverkenning, modelleren, en met behulp van de NYC Taxi reis scores in Spark 2.0-clusters en tarief gegevensset-beschreven [hier](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="5e34e-143">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how to perform data exploration, modeling, and scoring in Spark 2.0 clusters using the NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span> <span data-ttu-id="5e34e-144">Deze laptop is mogelijk een goed uitgangspunt voor het snel verkennen van de code die we voor Spark 2.0 hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="5e34e-144">This notebook may be a good starting point for quickly exploring the code we have provided for Spark 2.0.</span></span> <span data-ttu-id="5e34e-145">Voor een meer gedetailleerde notebook de gegevens van de NYC Taxi analyseert, Zie de volgende notebook in deze lijst.</span><span class="sxs-lookup"><span data-stu-id="5e34e-145">For a more detailed notebook analyzes the NYC Taxi data, see the next notebook in this list.</span></span> <span data-ttu-id="5e34e-146">Zie de opmerkingen na deze lijst die deze laptops vergelijken.</span><span class="sxs-lookup"><span data-stu-id="5e34e-146">See the notes following this list that compare these notebooks.</span></span> 
- <span data-ttu-id="5e34e-147">[Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): dit bestand ziet u hoe u gegevens worsteling (Spark SQL en dataframe bewerkingen), exploratie, model en score berekenen met behulp van de NYC Taxi reis en tarief set gegevens die worden beschreven [hier ](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span><span class="sxs-lookup"><span data-stu-id="5e34e-147">[Spark2.0-pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): This file shows how to perform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using the NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span>
- <span data-ttu-id="5e34e-148">[Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): dit bestand wordt beschreven hoe gegevens worsteling (Spark SQL en dataframe bewerkingen), exploratie, model en score berekenen met behulp van de bekende luchtvaartmaatschappij tijdige afwijking uitvoeren de gegevensset van 2011 en 2012.</span><span class="sxs-lookup"><span data-stu-id="5e34e-148">[Spark2.0-pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): This file shows how to perform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using the well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="5e34e-149">Wij de luchtvaartmaatschappij gegevensset met de luchthaven weergegevens (bijvoorbeeld windsnelheid, temperatuur, hoogte enz.) geïntegreerd vóór modelleren, zodat deze weer-functies kunnen worden opgenomen in het model.</span><span class="sxs-lookup"><span data-stu-id="5e34e-149">We integrated the airline dataset with the airport weather data (e.g. windspeed, temperature, altitude etc.) prior to modeling, so these weather features can be included in the model.</span></span>

<!-- -->

> [!NOTE]
> <span data-ttu-id="5e34e-150">De gegevensset luchtvaartmaatschappij is toegevoegd aan de laptops Spark 2.0 ter illustratie van het gebruik van bestandsclassificatie-algoritmen beter.</span><span class="sxs-lookup"><span data-stu-id="5e34e-150">The airline dataset was added to the Spark 2.0 notebooks to better illustrate the use of classification algorithms.</span></span> <span data-ttu-id="5e34e-151">Zie de volgende koppelingen voor meer informatie over luchtvaartmaatschappij tijdige vertrek gegevensset en gegevensset weer:</span><span class="sxs-lookup"><span data-stu-id="5e34e-151">See the following links for information about airline on-time departure dataset and weather dataset:</span></span>

>- <span data-ttu-id="5e34e-152">Luchtvaartmaatschappij tijdige vertrek gegevens: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span><span class="sxs-lookup"><span data-stu-id="5e34e-152">Airline on-time departure data: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span></span>

>- <span data-ttu-id="5e34e-153">Luchthaven weergegevens: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span><span class="sxs-lookup"><span data-stu-id="5e34e-153">Airport weather data: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span></span> 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
<span data-ttu-id="5e34e-154">De notitieblokken Spark 2.0 op de NYC taxi en luchtvaartmaatschappij vlucht vertraging-gegevenssets duurt 10 minuten of langer om uit te voeren (afhankelijk van de grootte van uw HDI-cluster).</span><span class="sxs-lookup"><span data-stu-id="5e34e-154">The Spark 2.0 notebooks on the NYC taxi and airline flight delay data-sets can take 10 mins or more to run (depending on the size of your HDI cluster).</span></span> <span data-ttu-id="5e34e-155">De eerste laptop in de bovenstaande lijst geeft veel aspecten van de gegevensverkenning, visualisatie en ML-model opleiding in een laptop die het kost minder tijd om uit te voeren met een lagere actieve NYC gegevensset, waarin de bestanden taxi en tarief vooraf lid zijn: [ Spark2.0-pySpark3-machine-Learning-Data-Science-Spark-Advanced-Data-Exploration-Modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) deze notebook neemt een veel kortere tijd om te voltooien (2-3 minuten) en kan worden een goed startpunt voor de code die we hebben opgegeven snel verkennen voor Spark 2.0.</span><span class="sxs-lookup"><span data-stu-id="5e34e-155">The first notebook in the above list shows many aspects of the data exploration, visualization and ML model training in a notebook that takes less time to run with down-sampled NYC data set, in which the taxi and fare files have been pre-joined: [Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) This notebook takes a much shorter time to finish (2-3 mins) and may be a good starting point for quickly exploring the code we have provided for Spark 2.0.</span></span> 

<!-- -->

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<!-- -->

> [!NOTE]
<span data-ttu-id="5e34e-156">De onderstaande beschrijvingen zijn gerelateerd aan met behulp van Spark 1.6.</span><span class="sxs-lookup"><span data-stu-id="5e34e-156">The descriptions below are related to using Spark 1.6.</span></span> <span data-ttu-id="5e34e-157">Gebruik de laptops beschreven en bovenstaande voor Spark 2.0-versies.</span><span class="sxs-lookup"><span data-stu-id="5e34e-157">For Spark 2.0 versions, please use the notebooks described and linked above.</span></span> 

<!-- -->

## <a name="setup-storage-locations-libraries-and-the-preset-spark-context"></a><span data-ttu-id="5e34e-158">Setup: opslaglocaties, bibliotheken en de vooraf ingestelde Spark-context</span><span class="sxs-lookup"><span data-stu-id="5e34e-158">Setup: storage locations, libraries, and the preset Spark context</span></span>
<span data-ttu-id="5e34e-159">Spark kan lezen en schrijven naar Azure Storage-Blob (ook wel bekend als WASB).</span><span class="sxs-lookup"><span data-stu-id="5e34e-159">Spark is able to read and write to Azure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="5e34e-160">Zodat uw bestaande gegevens opgeslagen kunnen er worden verwerkt met behulp van Spark en de resultaten opgeslagen opnieuw in WASB.</span><span class="sxs-lookup"><span data-stu-id="5e34e-160">So any of your existing data stored there can be processed using Spark and the results stored again in WASB.</span></span>

<span data-ttu-id="5e34e-161">Voor het opslaan van modellen of bestanden in WASB, moet het pad correct worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="5e34e-161">To save models or files in WASB, the path needs to be specified properly.</span></span> <span data-ttu-id="5e34e-162">De standaard-container die is gekoppeld aan het Spark-cluster kan worden verwezen met behulp van een pad die begint met: ' wasb: / / / '.</span><span class="sxs-lookup"><span data-stu-id="5e34e-162">The default container attached to the Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="5e34e-163">Andere locaties wordt verwezen door ' wasb: / / '.</span><span class="sxs-lookup"><span data-stu-id="5e34e-163">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="5e34e-164">Directory-paden voor opslaglocaties in WASB instellen</span><span class="sxs-lookup"><span data-stu-id="5e34e-164">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="5e34e-165">Het volgende codevoorbeeld geeft de locatie van de gegevens moeten worden gelezen en het pad voor het model opslagmap waarin de uitvoer van het model is opgeslagen:</span><span class="sxs-lookup"><span data-stu-id="5e34e-165">The following code sample specifies the location of the data to be read and the path for the model storage directory to which the model output is saved:</span></span>

    # SET PATHS TO FILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";

    # SET THE MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT THE FINAL BACKSLASH IN THE PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 


### <a name="import-libraries"></a><span data-ttu-id="5e34e-166">Bibliotheken importeren</span><span class="sxs-lookup"><span data-stu-id="5e34e-166">Import libraries</span></span>
<span data-ttu-id="5e34e-167">Instellen is ook vereist nodig bibliotheken importeren.</span><span class="sxs-lookup"><span data-stu-id="5e34e-167">Set up also requires importing necessary libraries.</span></span> <span data-ttu-id="5e34e-168">Context voor spark instellen en importeer nodig bibliotheken met de volgende code:</span><span class="sxs-lookup"><span data-stu-id="5e34e-168">Set spark context and import necessary libraries with the following code:</span></span>

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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="5e34e-169">Vooraf context voor Spark en PySpark magics</span><span class="sxs-lookup"><span data-stu-id="5e34e-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="5e34e-170">De PySpark-kernels die worden geleverd met Jupyter-notebooks hebben een vooraf ingestelde context.</span><span class="sxs-lookup"><span data-stu-id="5e34e-170">The PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="5e34e-171">Dus u hoeft niet in te stellen de Spark of Hive-contexten expliciet voordat u begint met het werken met de toepassing die u ontwikkelt.</span><span class="sxs-lookup"><span data-stu-id="5e34e-171">So you do not need to set the Spark or Hive contexts explicitly before you start working with the application you are developing.</span></span> <span data-ttu-id="5e34e-172">Deze contexten zijn standaard voor u beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="5e34e-172">These contexts are available for you by default.</span></span> <span data-ttu-id="5e34e-173">Deze contexten zijn:</span><span class="sxs-lookup"><span data-stu-id="5e34e-173">These contexts are:</span></span>

* <span data-ttu-id="5e34e-174">SC - voor Spark</span><span class="sxs-lookup"><span data-stu-id="5e34e-174">sc - for Spark</span></span> 
* <span data-ttu-id="5e34e-175">sqlContext - voor Hive</span><span class="sxs-lookup"><span data-stu-id="5e34e-175">sqlContext - for Hive</span></span>

<span data-ttu-id="5e34e-176">De PySpark-kernel biedt een aantal vooraf gedefinieerde 'magics', die zijn speciale opdrachten die u met aanroepen kunt %%.</span><span class="sxs-lookup"><span data-stu-id="5e34e-176">The PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="5e34e-177">Er zijn twee dergelijke opdrachten die worden gebruikt in deze codevoorbeelden.</span><span class="sxs-lookup"><span data-stu-id="5e34e-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="5e34e-178">**%% lokale** geeft aan dat de code in de volgende regels wordt lokaal uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5e34e-178">**%%local** Specifies that the code in subsequent lines is to be executed locally.</span></span> <span data-ttu-id="5e34e-179">De sitecode moet geldige Python-code.</span><span class="sxs-lookup"><span data-stu-id="5e34e-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="5e34e-180">**%% sql -o <variable name>**  een Hive-query op de sqlContext wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5e34e-180">**%%sql -o <variable name>** Executes a Hive query against the sqlContext.</span></span> <span data-ttu-id="5e34e-181">Als de parameter -o is doorgegeven, het resultaat van de query wordt bewaard de %% lokale Python context als een DataFrame Pandas.</span><span class="sxs-lookup"><span data-stu-id="5e34e-181">If the -o parameter is passed, the result of the query is persisted in the %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="5e34e-182">Voor meer informatie over de kernels voor Jupyter-notebooks en de vooraf gedefinieerde 'magics' die ze bieden, Zie [beschikbare Kernels voor Jupyter-notebooks met HDInsight Spark Linux-clusters in HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span><span class="sxs-lookup"><span data-stu-id="5e34e-182">For more information on the kernels for Jupyter notebooks and the predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="5e34e-183">Gegevensopname van een openbare blob</span><span class="sxs-lookup"><span data-stu-id="5e34e-183">Data ingestion from public blob</span></span>
<span data-ttu-id="5e34e-184">De eerste stap in het proces van de wetenschappelijke gegevens is om op te nemen van de gegevens te analyseren van bronnen waar is bevindt zich in uw gegevens te verkennen en modellering omgeving.</span><span class="sxs-lookup"><span data-stu-id="5e34e-184">The first step in the data science process is to ingest the data to be analyzed from sources where is resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="5e34e-185">De omgeving is Spark in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="5e34e-185">The environment is Spark in this walkthrough.</span></span> <span data-ttu-id="5e34e-186">Deze sectie bevat de code voor het voltooien van een reeks taken:</span><span class="sxs-lookup"><span data-stu-id="5e34e-186">This section contains the code to complete a series of tasks:</span></span>

* <span data-ttu-id="5e34e-187">de steekproef gemodelleerd opnemen</span><span class="sxs-lookup"><span data-stu-id="5e34e-187">ingest the data sample to be modeled</span></span>
* <span data-ttu-id="5e34e-188">Lees in de invoergegevensset (opgeslagen als een bestand .tsv)</span><span class="sxs-lookup"><span data-stu-id="5e34e-188">read in the input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="5e34e-189">indeling en de gegevens opgeschoond</span><span class="sxs-lookup"><span data-stu-id="5e34e-189">format and clean the data</span></span>
* <span data-ttu-id="5e34e-190">maken en objecten (RDDs of gegevens frames) in het geheugen in de cache</span><span class="sxs-lookup"><span data-stu-id="5e34e-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="5e34e-191">registreren als een temp-tabel in SQL-context.</span><span class="sxs-lookup"><span data-stu-id="5e34e-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="5e34e-192">Hier volgt de code voor gegevensopname.</span><span class="sxs-lookup"><span data-stu-id="5e34e-192">Here is the code for data ingestion.</span></span>

    # INGEST DATA

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_train_file = sc.textFile(taxi_train_file_loc)

    # GET SCHEMA OF THE FILE FROM HEADER
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

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="5e34e-193">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="5e34e-193">**OUTPUT:**</span></span>

<span data-ttu-id="5e34e-194">Tijd uitvoering boven cel: 51.72 seconden</span><span class="sxs-lookup"><span data-stu-id="5e34e-194">Time taken to execute above cell: 51.72 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="5e34e-195">Gegevensverkenning & visualisatie</span><span class="sxs-lookup"><span data-stu-id="5e34e-195">Data exploration & visualization</span></span>
<span data-ttu-id="5e34e-196">Nadat de gegevens in Spark is ingesteld, is de volgende stap in het proces van de wetenschappelijke gegevens dieper inzicht van de gegevens via de exploratie en visualisatie te krijgen.</span><span class="sxs-lookup"><span data-stu-id="5e34e-196">Once the data has been brought into Spark, the next step in the data science process is to gain deeper understanding of the data through exploration and visualization.</span></span> <span data-ttu-id="5e34e-197">In deze sectie we de taxi gegevens met behulp van SQL-query's controleren en de doelvariabelen en potentiële functies voor visuele inspectie tekenen.</span><span class="sxs-lookup"><span data-stu-id="5e34e-197">In this section, we examine the taxi data using SQL queries and plot the target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="5e34e-198">In het bijzonder voert u de frequentie van de passagiers aantallen in taxi reizen, de frequentie van tip bedragen en hoe tips is afhankelijk van de hoeveelheid betaling en het type.</span><span class="sxs-lookup"><span data-stu-id="5e34e-198">Specifically, we plot the frequency of passenger counts in taxi trips, the frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-the-sample-of-taxi-trips"></a><span data-ttu-id="5e34e-199">Een histogram van passagiers aantal frequenties in de steekproef van taxi heen wordt getekend</span><span class="sxs-lookup"><span data-stu-id="5e34e-199">Plot a histogram of passenger count frequencies in the sample of taxi trips</span></span>
<span data-ttu-id="5e34e-200">Deze code en de volgende codefragmenten gebruik van SQL-magic query uitvoeren op de lokale magic de gegevens worden uitgezet en voorbeelden.</span><span class="sxs-lookup"><span data-stu-id="5e34e-200">This code and subsequent snippets use SQL magic to query the sample and local magic to plot the data.</span></span>

* <span data-ttu-id="5e34e-201">**SQL-magic (`%%sql`)** eenvoudig inline HiveQL query's op de sqlContext biedt ondersteuning voor het HDInsight-PySpark-kernel.</span><span class="sxs-lookup"><span data-stu-id="5e34e-201">**SQL magic (`%%sql`)** The HDInsight PySpark kernel supports easy inline HiveQL queries against the sqlContext.</span></span> <span data-ttu-id="5e34e-202">De (-o naam_variabele) argument als een DataFrame Pandas op de Jupyter-server de uitvoer van de SQL-query zich blijft voordoen.</span><span class="sxs-lookup"><span data-stu-id="5e34e-202">The (-o VARIABLE_NAME) argument persists the output of the SQL query as a Pandas DataFrame on the Jupyter server.</span></span> <span data-ttu-id="5e34e-203">Dit betekent dat deze beschikbaar zijn in de lokale modus.</span><span class="sxs-lookup"><span data-stu-id="5e34e-203">This means it is available in the local mode.</span></span>
* <span data-ttu-id="5e34e-204">De  **`%%local` magic** code lokaal uitvoeren op de Jupyter-server, waarop de headnode van het HDInsight-cluster wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="5e34e-204">The **`%%local` magic** is used to run code locally on the Jupyter server, which is the headnode of the HDInsight cluster.</span></span> <span data-ttu-id="5e34e-205">Normaal gesproken gebruikt u `%%local` magische in combinatie met de `%%sql` met -o parameter magic.</span><span class="sxs-lookup"><span data-stu-id="5e34e-205">Typically, you use `%%local` magic in conjunction with the `%%sql` magic with -o parameter.</span></span> <span data-ttu-id="5e34e-206">De uitvoer van de SQL-query lokaal wilt behouden door de parameter -o en vervolgens %% lokale magic zou de volgende reeks codefragment lokaal uitvoeren op basis van de uitvoer van de SQL-query's die lokaal wordt bewaard</span><span class="sxs-lookup"><span data-stu-id="5e34e-206">The -o parameter would persist the output of the SQL query locally and then %%local magic would trigger the next set of code snippet to run locally against the output of the SQL queries that is persisted locally</span></span>

<span data-ttu-id="5e34e-207">De uitvoer wordt automatisch weergegeven nadat u de code hebt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5e34e-207">The output is automatically visualized after you run the code.</span></span>

<span data-ttu-id="5e34e-208">Deze query haalt de reizen op het aantal van de passagiers.</span><span class="sxs-lookup"><span data-stu-id="5e34e-208">This query retrieves the trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # HIVEQL QUERY AGAINST THE sqlContext
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts 
    FROM taxi_train 
    WHERE passenger_count > 0 and passenger_count < 7 
    GROUP BY passenger_count 

<span data-ttu-id="5e34e-209">Deze code maakt een lokale gegevens tijdskader van de query-uitvoer en de gegevens zijn getekend.</span><span class="sxs-lookup"><span data-stu-id="5e34e-209">This code creates a local data-frame from the query output and plots the data.</span></span> <span data-ttu-id="5e34e-210">De `%%local` magic maakt een lokale gegevens-frame, `sqlResults`, die kan worden gebruikt voor het uitzetten van matplotlib.</span><span class="sxs-lookup"><span data-stu-id="5e34e-210">The `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="5e34e-211">Deze PySpark-magic wordt meerdere malen gebruikt in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="5e34e-211">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="5e34e-212">Als de hoeveelheid gegevens te groot is, moet u een steekproef nemen voor het maken van een gegevens-frame dat past in het lokale geheugen.</span><span class="sxs-lookup"><span data-stu-id="5e34e-212">If the amount of data is large, you should sample to create a data-frame that can fit in local memory.</span></span>
> 
> 

    #CREATE LOCAL DATA-FRAME AND USE FOR MATPLOTLIB PLOTTING

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # USE THE JUPYTER AUTO-PLOTTING FEATURE TO CREATE INTERACTIVE FIGURES. 
    # CLICK ON THE TYPE OF PLOT TO BE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="5e34e-213">Hier volgt de code voor het uitzetten van de reizen door passagiers aantallen</span><span class="sxs-lookup"><span data-stu-id="5e34e-213">Here is the code to plot the trips by passenger counts</span></span>

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

<span data-ttu-id="5e34e-214">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="5e34e-214">**OUTPUT:**</span></span>

![De frequentie reis op het aantal passagiers](./media/machine-learning-data-science-spark-data-exploration-modeling/trip-freqency-by-passenger-count.png)

<span data-ttu-id="5e34e-216">U kunt kiezen uit verschillende soorten visualisaties (tabel-, cirkel, regel, gebied of balk) met behulp van de **Type** menuknoppen in de notebook.</span><span class="sxs-lookup"><span data-stu-id="5e34e-216">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using the **Type** menu buttons in the notebook.</span></span> <span data-ttu-id="5e34e-217">De grafiek balk wordt hier weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5e34e-217">The Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="5e34e-218">Zet een histogram van de tip bedragen en hoe tip bedrag hangt af van de passagiers telling en het tarief bedragen.</span><span class="sxs-lookup"><span data-stu-id="5e34e-218">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="5e34e-219">Gebruik een SQL-query om de voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="5e34e-219">Use a SQL query to sample data.</span></span>

    #PLOT HISTOGRAM OF TIP AMOUNTS AND VARIATION BY PASSENGER COUNT AND PAYMENT TYPE

    # HIVEQL QUERY AGAINST THE sqlContext
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


<span data-ttu-id="5e34e-220">Deze codecel gebruikt de SQL-query om de gegevens van drie waarnemingspunten maken.</span><span class="sxs-lookup"><span data-stu-id="5e34e-220">This code cell uses the SQL query to create three plots the data.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
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


<span data-ttu-id="5e34e-221">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="5e34e-221">**OUTPUT:**</span></span> 

![Tip bedragdistributie](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-distribution.png)

![Hoeveelheid op het aantal passagiers Tip](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-passenger-count.png)

![Tip bedrag door tarief bedrag](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="5e34e-225">Functie-engineering, transformatie en gegevens voorbereiding voor modellering</span><span class="sxs-lookup"><span data-stu-id="5e34e-225">Feature engineering, transformation and data preparation for modeling</span></span>
<span data-ttu-id="5e34e-226">Deze sectie wordt beschreven en vindt u de code voor procedures voor het voorbereiden van gegevens voor gebruik in ML-model.</span><span class="sxs-lookup"><span data-stu-id="5e34e-226">This section describes and provides the code for procedures used to prepare data for use in ML modeling.</span></span> <span data-ttu-id="5e34e-227">Er wordt weergegeven hoe de volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5e34e-227">It shows how to do the following tasks:</span></span>

* <span data-ttu-id="5e34e-228">Maakt een nieuwe functie met binning uur in verkeer tijd buckets</span><span class="sxs-lookup"><span data-stu-id="5e34e-228">Create a new feature by binning hours into traffic time buckets</span></span>
* <span data-ttu-id="5e34e-229">Index en categorische functies coderen</span><span class="sxs-lookup"><span data-stu-id="5e34e-229">Index and encode categorical features</span></span>
* <span data-ttu-id="5e34e-230">Gelabelde point-objecten voor invoer in ML functies maken</span><span class="sxs-lookup"><span data-stu-id="5e34e-230">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="5e34e-231">Een onderliggende steekproeven van de gegevens maken en deze te splitsen in trainings- en testdoeleinden sets</span><span class="sxs-lookup"><span data-stu-id="5e34e-231">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
* <span data-ttu-id="5e34e-232">Functie schalen</span><span class="sxs-lookup"><span data-stu-id="5e34e-232">Feature scaling</span></span>
* <span data-ttu-id="5e34e-233">Cacheobjecten in het geheugen</span><span class="sxs-lookup"><span data-stu-id="5e34e-233">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="5e34e-234">Maakt een nieuwe functie met binning uur in verkeer tijd buckets</span><span class="sxs-lookup"><span data-stu-id="5e34e-234">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="5e34e-235">Deze code laat zien hoe u een nieuwe functie maakt met binning uren in verkeer tijd buckets en hoe u in de cache van het resulterende gegevensframe in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="5e34e-235">This code shows how to create a new feature by binning hours into traffic time buckets and then how to cache the resulting data frame in memory.</span></span> <span data-ttu-id="5e34e-236">Flexibele gegevenssets gedistribueerd (RDDs) en gegevens frames herhaaldelijk gebruikt, leidt opslaan in cache tot verbeterde uitvoeringstijden.</span><span class="sxs-lookup"><span data-stu-id="5e34e-236">Where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly, caching leads to improved execution times.</span></span> <span data-ttu-id="5e34e-237">Dienovereenkomstig, we RDDs en gegevensframes cache in verschillende fasen in het overzicht.</span><span class="sxs-lookup"><span data-stu-id="5e34e-237">Accordingly, we cache RDDs and data-frames at several stages in the walkthrough.</span></span> 

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
    # THE .COUNT() GOES THROUGH THE ENTIRE DATA-FRAME,
    # MATERIALIZES IT IN MEMORY, AND GIVES THE COUNT OF ROWS.
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()

<span data-ttu-id="5e34e-238">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="5e34e-238">**OUTPUT:**</span></span> 

<span data-ttu-id="5e34e-239">126050</span><span class="sxs-lookup"><span data-stu-id="5e34e-239">126050</span></span>

### <a name="index-and-encode-categorical-features-for-input-into-modeling-functions"></a><span data-ttu-id="5e34e-240">Index en het coderen van categorische functies voor invoer in het modelleren van functies</span><span class="sxs-lookup"><span data-stu-id="5e34e-240">Index and encode categorical features for input into modeling functions</span></span>
<span data-ttu-id="5e34e-241">Deze sectie wordt beschreven hoe index of categorische functies voor invoer in de functies modellering coderen.</span><span class="sxs-lookup"><span data-stu-id="5e34e-241">This section shows how to index or encode categorical features for input into the modeling functions.</span></span> <span data-ttu-id="5e34e-242">Het model en het voorspellen van de functies van MLlib functies met categorische invoergegevens worden geïndexeerd of gecodeerd vóór gebruik vereist.</span><span class="sxs-lookup"><span data-stu-id="5e34e-242">The modeling and predict functions of MLlib require features with categorical input data to be indexed or encoded prior to use.</span></span> <span data-ttu-id="5e34e-243">Afhankelijk van het model moet u de index of ze coderen op verschillende manieren:</span><span class="sxs-lookup"><span data-stu-id="5e34e-243">Depending on the model, you need to index or encode them in different ways:</span></span>  

* <span data-ttu-id="5e34e-244">**Op basis van een structuur modellering** vereist categorieën moeten worden gecodeerd als numerieke waarden (bijvoorbeeld, een onderdeel met drie categorieën kan worden gecodeerd met 0, 1, 2).</span><span class="sxs-lookup"><span data-stu-id="5e34e-244">**Tree-based modeling** requires categories to be encoded as numerical values (for example, a feature with three categories may be encoded with 0, 1, 2).</span></span> <span data-ttu-id="5e34e-245">Dit wordt geleverd door de MLlib [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) functie.</span><span class="sxs-lookup"><span data-stu-id="5e34e-245">This is provided by MLlib’s [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) function.</span></span> <span data-ttu-id="5e34e-246">Deze functie codeert een tekenreekskolom van de labels aan een kolom van een label-indexen die zijn besteld op het label frequenties.</span><span class="sxs-lookup"><span data-stu-id="5e34e-246">This function encodes a string column of labels to a column of label indices that are ordered by label frequencies.</span></span> <span data-ttu-id="5e34e-247">Hoewel geïndexeerd met numerieke waarden voor de invoer- en de verwerking van gegevens, kunnen de structuur gebaseerde algoritmen worden opgegeven op de juiste manier behandelen als categorieën.</span><span class="sxs-lookup"><span data-stu-id="5e34e-247">Although indexed with numerical values for input and data handling, the tree-based algorithms can be specified to treat them appropriately as categories.</span></span> 
* <span data-ttu-id="5e34e-248">**Logistic en lineaire regressie modellen** vereisen een hot codering, where, bijvoorbeeld, een onderdeel met drie categorieën kan worden uitgebreid naar drie kolommen van de functie, waarbij elke met 0 of 1, afhankelijk van de categorie van een observatie.</span><span class="sxs-lookup"><span data-stu-id="5e34e-248">**Logistic and Linear Regression models** require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on the category of an observation.</span></span> <span data-ttu-id="5e34e-249">MLlib biedt [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) doen van één hot codering.</span><span class="sxs-lookup"><span data-stu-id="5e34e-249">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function to do one-hot encoding.</span></span> <span data-ttu-id="5e34e-250">Een kolom van een label indexen deze encoder toegewezen aan een kolom van de binaire aanvalsvectoren, met maximaal één one-waarde.</span><span class="sxs-lookup"><span data-stu-id="5e34e-250">This encoder maps a column of label indices to a column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="5e34e-251">Met deze codering kunt algoritmen die numerieke waarden functies, zoals logistic regression, moet worden toegepast op categorische functies verwacht.</span><span class="sxs-lookup"><span data-stu-id="5e34e-251">This encoding allows algorithms that expect numerical valued features, such as logistic regression, to be applied to categorical features.</span></span>

<span data-ttu-id="5e34e-252">Dit is de code om te indexeren en coderen categorische functies:</span><span class="sxs-lookup"><span data-stu-id="5e34e-252">Here is the code to index and encode categorical features:</span></span>

    # INDEX AND ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES    
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

    # INDEX AND ENCODE VENDOR_ID
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_train_with_newFeatures) # Input data-frame is the cleaned one from above
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="5e34e-253">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="5e34e-253">**OUTPUT:**</span></span>

<span data-ttu-id="5e34e-254">Tijd uitvoering boven cel: 1.28 seconden</span><span class="sxs-lookup"><span data-stu-id="5e34e-254">Time taken to execute above cell: 1.28 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="5e34e-255">Gelabelde point-objecten voor invoer in ML functies maken</span><span class="sxs-lookup"><span data-stu-id="5e34e-255">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="5e34e-256">In deze sectie bevat de code die wordt beschreven hoe categorische gegevens als een gegevenstype gelabelde punt index en deze coderen zodat deze kan worden gebruikt voor het trainen en te testen MLlib logistic regression en andere classificatie-modellen.</span><span class="sxs-lookup"><span data-stu-id="5e34e-256">This section contains code that shows how to index categorical text data as a labeled point data type and encode it so that it can be used to train and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="5e34e-257">Gelabelde point-objecten zijn robuuste gedistribueerd gegevenssets (RDD) geformatteerd op een manier die is vereist als de invoergegevens voor de meeste ML algoritmen in MLlib.</span><span class="sxs-lookup"><span data-stu-id="5e34e-257">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="5e34e-258">Een [punt gelabeld](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is een lokale vector, dense of sparse, die is gekoppeld aan een label/antwoord.</span><span class="sxs-lookup"><span data-stu-id="5e34e-258">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>  

<span data-ttu-id="5e34e-259">Deze sectie bevat de code die laat zien hoe index categorische gegevens als een [punt gelabeld](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) gegevenstype en deze te coderen zodat deze kan worden gebruikt voor het trainen en te testen MLlib logistic regression en andere classificatie-modellen.</span><span class="sxs-lookup"><span data-stu-id="5e34e-259">This section contains code that shows how to index categorical text data as a [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) data type and encode it so that it can be used to train and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="5e34e-260">Gelabelde point-objecten zijn robuuste gedistribueerd gegevenssets (RDD) die bestaan uit een label (doel/antwoord-variabele) en de functie vector.</span><span class="sxs-lookup"><span data-stu-id="5e34e-260">Labeled point objects are Resilient Distributed Datasets (RDD) consisting of a label (target/response variable) and feature vector.</span></span> <span data-ttu-id="5e34e-261">Deze indeling is nodig als invoer door veel ML algoritmen in MLlib.</span><span class="sxs-lookup"><span data-stu-id="5e34e-261">This format is needed as input by many ML algorithms in MLlib.</span></span>

<span data-ttu-id="5e34e-262">Dit is de code om te indexeren en het coderen van tekstfuncties voor binaire classificatie.</span><span class="sxs-lookup"><span data-stu-id="5e34e-262">Here is the code to index and encode text features for binary classification.</span></span>

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


<span data-ttu-id="5e34e-263">Dit is de code voor het coderen en indexeren categorische tekstfuncties voor lineaire regressie-analyse.</span><span class="sxs-lookup"><span data-stu-id="5e34e-263">Here is the code to encode and index categorical text features for linear regression analysis.</span></span>

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


### <a name="create-a-random-sub-sampling-of-the-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="5e34e-264">Een onderliggende steekproeven van de gegevens maken en deze te splitsen in trainings- en testdoeleinden sets</span><span class="sxs-lookup"><span data-stu-id="5e34e-264">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
<span data-ttu-id="5e34e-265">Deze code maakt een willekeurige steekproef van de gegevens (25% wordt hier gebruikt).</span><span class="sxs-lookup"><span data-stu-id="5e34e-265">This code creates a random sampling of the data (25% is used here).</span></span> <span data-ttu-id="5e34e-266">Hoewel dit niet vereist voor dit voorbeeld vanwege de grootte van de gegevensset, ziet u hoe u kunt een steekproef nemen hier dus u kunt gebruiken voor uw eigen probleem wanneer deze nodig is.</span><span class="sxs-lookup"><span data-stu-id="5e34e-266">Although it is not required for this example due to the size of the dataset, we demonstrate how you can sample here so you know how to use it for your own problem when needed.</span></span> <span data-ttu-id="5e34e-267">Als voorbeelden groot zijn, kan dit aanzienlijke tijd tijdens de training modellen opslaan.</span><span class="sxs-lookup"><span data-stu-id="5e34e-267">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="5e34e-268">Naast we het voorbeeld in een training gedeelte (hier 75%) en een test deel (25% hier) moet worden gebruikt in de classificatie en regressie modellering opgesplitst.</span><span class="sxs-lookup"><span data-stu-id="5e34e-268">Next we split the sample into a training part (75% here) and a testing part (25% here) to use in classification and regression modeling.</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="5e34e-269">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="5e34e-269">**OUTPUT:**</span></span>

<span data-ttu-id="5e34e-270">Tijd uitvoering boven cel: 0,24 seconden</span><span class="sxs-lookup"><span data-stu-id="5e34e-270">Time taken to execute above cell: 0.24 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="5e34e-271">Functie schalen</span><span class="sxs-lookup"><span data-stu-id="5e34e-271">Feature scaling</span></span>
<span data-ttu-id="5e34e-272">Functie schaal, ook wel bekend als gegevensnormalisatie, weet u zeker dat functies met veel betaald waarden zijn niet opgegeven overmatige afwegen in de beoogde functie.</span><span class="sxs-lookup"><span data-stu-id="5e34e-272">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in the objective function.</span></span> <span data-ttu-id="5e34e-273">De code voor de functie schalen maakt gebruik van de [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) schalen van de functies verschillen eenheid.</span><span class="sxs-lookup"><span data-stu-id="5e34e-273">The code for feature scaling uses the [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) to scale the features to unit variance.</span></span> <span data-ttu-id="5e34e-274">Het wordt geleverd door MLlib voor gebruik in lineaire regressie met stochastische kleurovergang Daalgradiënt (SGD), een populaire algoritme voor het trainen van een breed scala aan andere machine learning-modellen zoals overgegaan regressies of ondersteuning vector machines (SVM).</span><span class="sxs-lookup"><span data-stu-id="5e34e-274">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>

> [!NOTE]
> <span data-ttu-id="5e34e-275">Er is vastgesteld dat het algoritme LinearRegressionWithSGD gevoelig functie schalen.</span><span class="sxs-lookup"><span data-stu-id="5e34e-275">We have found the LinearRegressionWithSGD algorithm to be sensitive to feature scaling.</span></span>
> 
> 

<span data-ttu-id="5e34e-276">Dit is de code op schaal variabelen voor gebruik met de regularized lineaire SGD-algoritme.</span><span class="sxs-lookup"><span data-stu-id="5e34e-276">Here is the code to scale variables for use with the regularized linear SGD algorithm.</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="5e34e-277">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="5e34e-277">**OUTPUT:**</span></span>

<span data-ttu-id="5e34e-278">Tijd uitvoering boven cel: 13.17 seconden</span><span class="sxs-lookup"><span data-stu-id="5e34e-278">Time taken to execute above cell: 13.17 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="5e34e-279">Cacheobjecten in het geheugen</span><span class="sxs-lookup"><span data-stu-id="5e34e-279">Cache objects in memory</span></span>
<span data-ttu-id="5e34e-280">De benodigde tijd voor trainings- en testdoeleinden ML algoritmen kan worden verkleind door het frame invoergegevens objecten voor classificatie, regressie, gebruikt en de uitgebreide functies opslaan in cache.</span><span class="sxs-lookup"><span data-stu-id="5e34e-280">The time taken for training and testing of ML algorithms can be reduced by caching the input data frame objects used for classification, regression, and scaled features.</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="5e34e-281">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="5e34e-281">**OUTPUT:**</span></span> 

<span data-ttu-id="5e34e-282">Tijd uitvoering boven cel: 0,15 seconden</span><span class="sxs-lookup"><span data-stu-id="5e34e-282">Time taken to execute above cell: 0.15 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="5e34e-283">Voorspellen of een tip wordt betaald met binaire classificatie modellen</span><span class="sxs-lookup"><span data-stu-id="5e34e-283">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="5e34e-284">Deze sectie wordt beschreven hoe gebruik drie modellen voor de classificatietaak binaire van het voorspellen van al dan niet een tip voor een reis taxi wordt betaald.</span><span class="sxs-lookup"><span data-stu-id="5e34e-284">This section shows how use three models for the binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="5e34e-285">De modellen die zijn gepresenteerd zijn:</span><span class="sxs-lookup"><span data-stu-id="5e34e-285">The models presented are:</span></span>

* <span data-ttu-id="5e34e-286">Logistic regression overgegaan</span><span class="sxs-lookup"><span data-stu-id="5e34e-286">Regularized logistic regression</span></span> 
* <span data-ttu-id="5e34e-287">Willekeurige forestmodel</span><span class="sxs-lookup"><span data-stu-id="5e34e-287">Random forest model</span></span>
* <span data-ttu-id="5e34e-288">Kleurovergang prestatieverbetering structuren</span><span class="sxs-lookup"><span data-stu-id="5e34e-288">Gradient Boosting Trees</span></span>

<span data-ttu-id="5e34e-289">Elk model bouwen sectie code opgedeeld in stappen:</span><span class="sxs-lookup"><span data-stu-id="5e34e-289">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="5e34e-290">**Training model** gegevens met één parameterset</span><span class="sxs-lookup"><span data-stu-id="5e34e-290">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="5e34e-291">**Evaluatie model** op een test-gegevensset met metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="5e34e-291">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="5e34e-292">**Opslaan van model** in blob voor toekomstige verbruik</span><span class="sxs-lookup"><span data-stu-id="5e34e-292">**Saving model** in blob for future consumption</span></span>

### <a name="classification-using-logistic-regression"></a><span data-ttu-id="5e34e-293">Classificatie met logistic regression</span><span class="sxs-lookup"><span data-stu-id="5e34e-293">Classification using logistic regression</span></span>
<span data-ttu-id="5e34e-294">De code in deze sectie ziet u hoe te trainen, evalueren en opslaan van een regressiemodel logistic met [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) die voorspelt al dan niet een tip voor een reis in de gegevensset NYC taxi reis en tarief wordt betaald.</span><span class="sxs-lookup"><span data-stu-id="5e34e-294">The code in this section shows how to train, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

<span data-ttu-id="5e34e-295">**Het gebruik van k/l en hyperparameter sweeping logistic regressiemodel trainen**</span><span class="sxs-lookup"><span data-stu-id="5e34e-295">**Train the logistic regression model using CV and hyperparameter sweeping**</span></span>

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

    # PRINT COEFFICIENTS AND INTERCEPT OF THE MODEL
    # NOTE: There are 20 coefficient terms for the 10 features, 
    #       and the different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitModel.weights))
    print("Intercept: " + str(logitModel.intercept))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="5e34e-296">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="5e34e-296">**OUTPUT:**</span></span> 

<span data-ttu-id="5e34e-297">Coëfficiënten: [0.0082065285375,-0.0223675576104,-0.0183812028036, -3.48124578069e-05,-0.00247646947233,-0.00165897881503, 0.0675394837328,-0.111823113101,-0.324609912762,-0.204549780032,-1.36499216354, 0.591088507921,-0.664263411392,-1.00439726852, 3.46567827545,-3.51025855172,-0.0471341112232,-0.043521833294, 0.000243375810385, 0.054518719222]</span><span class="sxs-lookup"><span data-stu-id="5e34e-297">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="5e34e-298">Intercept:-0.0111216486893</span><span class="sxs-lookup"><span data-stu-id="5e34e-298">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="5e34e-299">Tijd uitvoering boven cel: 14.43 seconden</span><span class="sxs-lookup"><span data-stu-id="5e34e-299">Time taken to execute above cell: 14.43 seconds</span></span>

<span data-ttu-id="5e34e-300">**Evalueren van het model binaire classificatie met standaard metrische gegevens**</span><span class="sxs-lookup"><span data-stu-id="5e34e-300">**Evaluate the binary classification model with standard metrics**</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="5e34e-301">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="5e34e-301">**OUTPUT:**</span></span> 

<span data-ttu-id="5e34e-302">Gebied onder PR 0.985297691373 =</span><span class="sxs-lookup"><span data-stu-id="5e34e-302">Area under PR = 0.985297691373</span></span>

<span data-ttu-id="5e34e-303">Gebied onder ROC 0.983714670256 =</span><span class="sxs-lookup"><span data-stu-id="5e34e-303">Area under ROC = 0.983714670256</span></span>

<span data-ttu-id="5e34e-304">Samenvattende statistieken</span><span class="sxs-lookup"><span data-stu-id="5e34e-304">Summary Stats</span></span>

<span data-ttu-id="5e34e-305">Precisie 0.984304060189 =</span><span class="sxs-lookup"><span data-stu-id="5e34e-305">Precision = 0.984304060189</span></span>

<span data-ttu-id="5e34e-306">Intrekken 0.984304060189 =</span><span class="sxs-lookup"><span data-stu-id="5e34e-306">Recall = 0.984304060189</span></span>

<span data-ttu-id="5e34e-307">F1 Score 0.984304060189 =</span><span class="sxs-lookup"><span data-stu-id="5e34e-307">F1 Score = 0.984304060189</span></span>

<span data-ttu-id="5e34e-308">Tijd uitvoering boven cel: 57.61 seconden</span><span class="sxs-lookup"><span data-stu-id="5e34e-308">Time taken to execute above cell: 57.61 seconds</span></span>

<span data-ttu-id="5e34e-309">**De ROC-curve wordt getekend.**</span><span class="sxs-lookup"><span data-stu-id="5e34e-309">**Plot the ROC curve.**</span></span>

<span data-ttu-id="5e34e-310">De *predictionAndLabelsDF* is geregistreerd als een tabel, *tmp_results*, in de vorige cel.</span><span class="sxs-lookup"><span data-stu-id="5e34e-310">The *predictionAndLabelsDF* is registered as a table, *tmp_results*, in the previous cell.</span></span> <span data-ttu-id="5e34e-311">*tmp_results* kan worden gebruikt voor query's wilt en uitvoer resultaten in het sqlResults data-frame voor het uitzetten van.</span><span class="sxs-lookup"><span data-stu-id="5e34e-311">*tmp_results* can be used to do queries and output results into the sqlResults data-frame for plotting.</span></span> <span data-ttu-id="5e34e-312">Dit is de code.</span><span class="sxs-lookup"><span data-stu-id="5e34e-312">Here is the code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="5e34e-313">Hier volgt de code voor het maken van voorspellingen en de ROC-curve tekenen.</span><span class="sxs-lookup"><span data-stu-id="5e34e-313">Here is the code to make predictions and plot the ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
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


<span data-ttu-id="5e34e-314">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="5e34e-314">**OUTPUT:**</span></span>

![Logistic regression ROC curve.png](./media/machine-learning-data-science-spark-data-exploration-modeling/logistic-regression-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="5e34e-316">Classificatie van willekeurige forest</span><span class="sxs-lookup"><span data-stu-id="5e34e-316">Random forest classification</span></span>
<span data-ttu-id="5e34e-317">De code in deze sectie wordt beschreven hoe trainen, evalueren en opslaan van een willekeurige forestmodel die voorspelt al dan niet een tip voor een reis in de gegevensset NYC taxi reis en tarief wordt betaald.</span><span class="sxs-lookup"><span data-stu-id="5e34e-317">The code in this section shows how to train, evaluate, and save a random forest model that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

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
    ## UN-COMMENT IF YOU WANT TO PRINT TREES
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="5e34e-318">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="5e34e-318">**OUTPUT:**</span></span>

<span data-ttu-id="5e34e-319">Gebied onder ROC 0.985297691373 =</span><span class="sxs-lookup"><span data-stu-id="5e34e-319">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="5e34e-320">Tijd uitvoering boven cel: 31.09 seconden</span><span class="sxs-lookup"><span data-stu-id="5e34e-320">Time taken to execute above cell: 31.09 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="5e34e-321">Kleurovergang prestatieverbetering structuren classificatie</span><span class="sxs-lookup"><span data-stu-id="5e34e-321">Gradient boosting trees classification</span></span>
<span data-ttu-id="5e34e-322">De code in deze sectie wordt beschreven hoe trainen, evalueren, en een kleurovergang prestatieverbetering structuren model die al dan niet een tip wordt betaald voor een reis in de NYC taxi reis voorspelt opslaat en ritbedrag gegevensset.</span><span class="sxs-lookup"><span data-stu-id="5e34e-322">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

    #PREDICT WHETHER A TIP IS PAID OR NOT USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo, numIterations=5)
    ## UNCOMMENT IF YOU WANT TO PRINT TREE DETAILS
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="5e34e-323">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="5e34e-323">**OUTPUT:**</span></span>

<span data-ttu-id="5e34e-324">Gebied onder ROC 0.985297691373 =</span><span class="sxs-lookup"><span data-stu-id="5e34e-324">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="5e34e-325">Tijd uitvoering boven cel: 19.76 seconden</span><span class="sxs-lookup"><span data-stu-id="5e34e-325">Time taken to execute above cell: 19.76 seconds</span></span>

## <a name="predict-tip-amounts-for-taxi-trips-with-regression-models"></a><span data-ttu-id="5e34e-326">Tip bedragen voor taxi reizen met regressie modellen voorspellen</span><span class="sxs-lookup"><span data-stu-id="5e34e-326">Predict tip amounts for taxi trips with regression models</span></span>
<span data-ttu-id="5e34e-327">Deze sectie wordt beschreven hoe drie modellen gebruiken voor de taak regressie van het voorspellen van de hoeveelheid de tip voor een taxi reis op basis van andere functies tip betaald.</span><span class="sxs-lookup"><span data-stu-id="5e34e-327">This section shows how use three models for the regression task of predicting the amount of the tip paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="5e34e-328">De modellen die zijn gepresenteerd zijn:</span><span class="sxs-lookup"><span data-stu-id="5e34e-328">The models presented are:</span></span>

* <span data-ttu-id="5e34e-329">Lineaire regressie overgegaan</span><span class="sxs-lookup"><span data-stu-id="5e34e-329">Regularized linear regression</span></span>
* <span data-ttu-id="5e34e-330">Willekeurige forest</span><span class="sxs-lookup"><span data-stu-id="5e34e-330">Random forest</span></span>
* <span data-ttu-id="5e34e-331">Kleurovergang prestatieverbetering structuren</span><span class="sxs-lookup"><span data-stu-id="5e34e-331">Gradient Boosting Trees</span></span>

<span data-ttu-id="5e34e-332">Deze modellen zijn beschreven in de introductie.</span><span class="sxs-lookup"><span data-stu-id="5e34e-332">These models were described in the introduction.</span></span> <span data-ttu-id="5e34e-333">Elk model bouwen sectie code opgedeeld in stappen:</span><span class="sxs-lookup"><span data-stu-id="5e34e-333">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="5e34e-334">**Training model** gegevens met één parameterset</span><span class="sxs-lookup"><span data-stu-id="5e34e-334">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="5e34e-335">**Evaluatie model** op een test-gegevensset met metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="5e34e-335">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="5e34e-336">**Opslaan van model** in blob voor toekomstige verbruik</span><span class="sxs-lookup"><span data-stu-id="5e34e-336">**Saving model** in blob for future consumption</span></span>

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="5e34e-337">Lineaire regressie met SGD</span><span class="sxs-lookup"><span data-stu-id="5e34e-337">Linear regression with SGD</span></span>
<span data-ttu-id="5e34e-338">De code in deze sectie leest hoe u geschaalde functies voor het trainen van een lineaire regressie die gebruikmaakt van stochastische kleurovergang daalgradiënt (SGD) voor optimalisatie en te beoordelen, evalueren en sla het model in Azure Blob Storage (WASB).</span><span class="sxs-lookup"><span data-stu-id="5e34e-338">The code in this section shows how to use scaled features to train a linear regression that uses stochastic gradient descent (SGD) for optimization, and how to score, evaluate, and save the model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="5e34e-339">In onze ervaring kunnen er problemen met de convergentie van LinearRegressionWithSGD modellen en parameters moeten worden gewijzigd/geoptimaliseerd zorgvuldig voor het verkrijgen van een geldig model.</span><span class="sxs-lookup"><span data-stu-id="5e34e-339">In our experience, there can be issues with the convergence of LinearRegressionWithSGD models, and parameters need to be changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="5e34e-340">Schalen van variabelen aanzienlijk helpt bij convergentie.</span><span class="sxs-lookup"><span data-stu-id="5e34e-340">Scaling of variables significantly helps with convergence.</span></span> 
> 
> 

    #PREDICT TIP AMOUNTS USING LINEAR REGRESSION WITH SGD

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel
    from pyspark.mllib.evaluation import RegressionMetrics
    from scipy import stats

    # USE SCALED FEATURES TO TRAIN MODEL
    linearModel = LinearRegressionWithSGD.train(oneHotTRAINregScaled, iterations=100, step = 0.1, regType='l2', regParam=0.1, intercept = True)

    # PRINT COEFFICIENTS AND INTERCEPT OF THE MODEL
    # NOTE: There are 20 coefficient terms for the 10 features, 
    #       and the different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(linearModel.weights))
    print("Intercept: " + str(linearModel.intercept))

    # SCORE ON SCALED TEST DATA-SET & EVALUATE
    predictionAndLabels = oneHotTESTregScaled.map(lambda lp: (float(linearModel.predict(lp.features)), lp.label))
    testMetrics = RegressionMetrics(predictionAndLabels)

    # PRINT TEST METRICS
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL WITH DATE-STAMP IN THE DEFAULT BLOB FOR THE CLUSTER
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="5e34e-341">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="5e34e-341">**OUTPUT:**</span></span>

<span data-ttu-id="5e34e-342">Coëfficiënten: [0.00457675809917,-0.0226314167349,-0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981,-0.000987181489428,-0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995,- 0.00990211159703,-0.00637410344522, 0.545083566179,-0.536756072402, 0.0105762393099,-0.0130117577055, 0.0129304737772,-0.00171065945959]</span><span class="sxs-lookup"><span data-stu-id="5e34e-342">Coefficients: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]</span></span>

<span data-ttu-id="5e34e-343">Intercept: 0.853872718283</span><span class="sxs-lookup"><span data-stu-id="5e34e-343">Intercept: 0.853872718283</span></span>

<span data-ttu-id="5e34e-344">RMSE 1.24190115863 =</span><span class="sxs-lookup"><span data-stu-id="5e34e-344">RMSE = 1.24190115863</span></span>

<span data-ttu-id="5e34e-345">R sqr 0.608017146081 =</span><span class="sxs-lookup"><span data-stu-id="5e34e-345">R-sqr = 0.608017146081</span></span>

<span data-ttu-id="5e34e-346">Tijd uitvoering boven cel: 58,42 seconden</span><span class="sxs-lookup"><span data-stu-id="5e34e-346">Time taken to execute above cell: 58.42 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="5e34e-347">Willekeurige Forest regressie</span><span class="sxs-lookup"><span data-stu-id="5e34e-347">Random Forest regression</span></span>
<span data-ttu-id="5e34e-348">De code in deze sectie wordt beschreven hoe trainen, evalueren en een willekeurige forest regressie die tip bedrag van de NYC taxi reis gegevens voorspelt opslaan.</span><span class="sxs-lookup"><span data-stu-id="5e34e-348">The code in this section shows how to train, evaluate, and save a random forest regression that predicts tip amount for the NYC taxi trip data.</span></span>

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
    ## UN-COMMENT IF YOU WANT TO PRING TREES
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="5e34e-349">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="5e34e-349">**OUTPUT:**</span></span>

<span data-ttu-id="5e34e-350">RMSE 0.891209218139 =</span><span class="sxs-lookup"><span data-stu-id="5e34e-350">RMSE = 0.891209218139</span></span>

<span data-ttu-id="5e34e-351">R sqr 0.759661334921 =</span><span class="sxs-lookup"><span data-stu-id="5e34e-351">R-sqr = 0.759661334921</span></span>

<span data-ttu-id="5e34e-352">Tijd uitvoering boven cel: 49.21 seconden</span><span class="sxs-lookup"><span data-stu-id="5e34e-352">Time taken to execute above cell: 49.21 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="5e34e-353">Kleurovergang prestatieverbetering structuren regressie</span><span class="sxs-lookup"><span data-stu-id="5e34e-353">Gradient boosting trees regression</span></span>
<span data-ttu-id="5e34e-354">De code in deze sectie wordt beschreven hoe trainen, evalueren en een kleurovergang prestatieverbetering structuren model die tip bedrag van de NYC taxi reis gegevens voorspelt opslaat.</span><span class="sxs-lookup"><span data-stu-id="5e34e-354">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts tip amount for the NYC taxi trip data.</span></span>

<span data-ttu-id="5e34e-355">** Trainen en evalueren **</span><span class="sxs-lookup"><span data-stu-id="5e34e-355">**Train and evaluate **</span></span>

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

    # CONVER RESULTS TO DF AND REGISER TEMP TABLE
    test_predictions = sqlContext.createDataFrame(predictionAndLabels)
    test_predictions.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="5e34e-356">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="5e34e-356">**OUTPUT:**</span></span>

<span data-ttu-id="5e34e-357">RMSE 0.908473148639 =</span><span class="sxs-lookup"><span data-stu-id="5e34e-357">RMSE = 0.908473148639</span></span>

<span data-ttu-id="5e34e-358">R sqr 0.753835096681 =</span><span class="sxs-lookup"><span data-stu-id="5e34e-358">R-sqr = 0.753835096681</span></span>

<span data-ttu-id="5e34e-359">Tijd uitvoering boven cel: 34.52 seconden</span><span class="sxs-lookup"><span data-stu-id="5e34e-359">Time taken to execute above cell: 34.52 seconds</span></span>

<span data-ttu-id="5e34e-360">**Tekenen**</span><span class="sxs-lookup"><span data-stu-id="5e34e-360">**Plot**</span></span>

<span data-ttu-id="5e34e-361">*tmp_results* is geregistreerd als een Hive-tabel in de vorige cel.</span><span class="sxs-lookup"><span data-stu-id="5e34e-361">*tmp_results* is registered as a Hive table in the previous cell.</span></span> <span data-ttu-id="5e34e-362">Resultaten van de tabel worden uitgevoerd in de *sqlResults* tijdskader voor het uitzetten van gegevens.</span><span class="sxs-lookup"><span data-stu-id="5e34e-362">Results from the table are output into the *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="5e34e-363">Dit is de code</span><span class="sxs-lookup"><span data-stu-id="5e34e-363">Here is the code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results

<span data-ttu-id="5e34e-364">Hier volgt de code voor het uitzetten van de gegevens met behulp van de Jupyter-server.</span><span class="sxs-lookup"><span data-stu-id="5e34e-364">Here is the code to plot the data using the Jupyter server.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
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


<span data-ttu-id="5e34e-365">**UITVOER:**</span><span class="sxs-lookup"><span data-stu-id="5e34e-365">**OUTPUT:**</span></span>

![Werkelijke-vs-voorspeld-tip-bedragen](./media/machine-learning-data-science-spark-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="clean-up-objects-from-memory"></a><span data-ttu-id="5e34e-367">Opschonen van objecten uit het geheugen</span><span class="sxs-lookup"><span data-stu-id="5e34e-367">Clean up objects from memory</span></span>
<span data-ttu-id="5e34e-368">Gebruik `unpersist()` verwijderen van objecten in het cachegeheugen opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="5e34e-368">Use `unpersist()` to delete objects cached in memory.</span></span>

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


## <a name="record-storage-locations-of-the-models-for-consumption-and-scoring"></a><span data-ttu-id="5e34e-369">De opslaglocaties record van de modellen voor gebruiks- en score berekenen</span><span class="sxs-lookup"><span data-stu-id="5e34e-369">Record storage locations of the models for consumption and scoring</span></span>
<span data-ttu-id="5e34e-370">Om te gebruiken en beoordelen van een onafhankelijke gegevensset wordt beschreven in de [Score en evalueren van Spark is gebouwd machine learning-modellen](machine-learning-data-science-spark-model-consumption.md) onderwerp, moet u kopieert en plakt u deze met de opgeslagen modellen die hier worden gemaakt in het verbruik bestandsnamen Jupyter-notebook.</span><span class="sxs-lookup"><span data-stu-id="5e34e-370">To consume and score an independent dataset described in the [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) topic, you need to copy and paste these file names containing the saved models created here into the Consumption Jupyter notebook.</span></span> <span data-ttu-id="5e34e-371">Dit is de code de paden naar modelbestanden u er moet afdrukken.</span><span class="sxs-lookup"><span data-stu-id="5e34e-371">Here is the code to print out the paths to model files you need there.</span></span>

    # MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="5e34e-372">**UITVOER**</span><span class="sxs-lookup"><span data-stu-id="5e34e-372">**OUTPUT**</span></span>

<span data-ttu-id="5e34e-373">logisticRegFileLoc = modelDir + 'LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568'</span><span class="sxs-lookup"><span data-stu-id="5e34e-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span></span>

<span data-ttu-id="5e34e-374">linearRegFileLoc = modelDir + 'LinearRegressionWithSGD_2016-05-0317_05_21.577773'</span><span class="sxs-lookup"><span data-stu-id="5e34e-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span></span>

<span data-ttu-id="5e34e-375">randomForestClassificationFileLoc = modelDir + 'RandomForestClassification_2016-05-0317_04_11.950206'</span><span class="sxs-lookup"><span data-stu-id="5e34e-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span></span>

<span data-ttu-id="5e34e-376">randomForestRegFileLoc = modelDir + 'RandomForestRegression_2016-05-0317_06_08.723736'</span><span class="sxs-lookup"><span data-stu-id="5e34e-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span></span>

<span data-ttu-id="5e34e-377">BoostedTreeClassificationFileLoc = modelDir + 'GradientBoostingTreeClassification_2016-05-0317_04_36.346583'</span><span class="sxs-lookup"><span data-stu-id="5e34e-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span></span>

<span data-ttu-id="5e34e-378">BoostedTreeRegressionFileLoc = modelDir + 'GradientBoostingTreeRegression_2016-05-0317_06_51.737282'</span><span class="sxs-lookup"><span data-stu-id="5e34e-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span></span>

## <a name="whats-next"></a><span data-ttu-id="5e34e-379">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5e34e-379">What's next?</span></span>
<span data-ttu-id="5e34e-380">Nu u regressie en classificatie modellen met de MlLib Spark hebt gemaakt, bent u klaar om te leren hoe u kunt beoordelen en evalueren van deze modellen.</span><span class="sxs-lookup"><span data-stu-id="5e34e-380">Now that you have created regression and classification models with the Spark MlLib, you are ready to learn how to score and evaluate these models.</span></span> <span data-ttu-id="5e34e-381">De geavanceerde gegevensverkenning en laptop modelleren diepere dives naar kruisvalidatie, hyper-parameter verstrekkende, inclusief en model van evaluatie.</span><span class="sxs-lookup"><span data-stu-id="5e34e-381">The advanced data exploration and modeling notebook dives deeper into including cross-validation, hyper-parameter sweeping, and model evaluation.</span></span> 

<span data-ttu-id="5e34e-382">**Model verbruik:** voor informatie over het beoordelen en evalueren van de classificatie en regressie modellen in dit onderwerp hebt gemaakt, Zie [Score en evalueren van Spark is gebouwd machine learning-modellen](machine-learning-data-science-spark-model-consumption.md).</span><span class="sxs-lookup"><span data-stu-id="5e34e-382">**Model consumption:** To learn how to score and evaluate the classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

<span data-ttu-id="5e34e-383">**Kruisvalidatie en hyperparameter sweeping**: Zie [geavanceerde gegevensverkenning en modellering met Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) over de manier waarop modellen kunnen getraind met behulp van kruisvalidatie en hyper-parameter sweeping</span><span class="sxs-lookup"><span data-stu-id="5e34e-383">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping</span></span>

