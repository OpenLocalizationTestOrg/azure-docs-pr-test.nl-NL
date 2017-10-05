---
title: Het Team gegevens wetenschap proces in actie - met een Azure HDInsight Hadoop-Cluster van een gegevensset 1 TB | Microsoft Docs
description: Met behulp van het Team gegevens wetenschap proces voor een end-to-end-scenario die gebruikmaakt van een HDInsight Hadoop-cluster te bouwen en implementeren van een model met behulp van een grote (1 TB) openbaar gegevensset
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 72d958c4-3205-49b9-ad82-47998d400d2b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 8e6143bca819c9a0484221f8b4feb319aaaa73f5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="the-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a><span data-ttu-id="71afe-103">Het Team gegevens wetenschap proces in actie - met een Azure HDInsight Hadoop-Cluster van een gegevensset 1 TB</span><span class="sxs-lookup"><span data-stu-id="71afe-103">The Team Data Science Process in action - Using an Azure HDInsight Hadoop Cluster on a 1 TB dataset</span></span>

<span data-ttu-id="71afe-104">In dit overzicht wordt gedemonstreerd met behulp van het Team gegevens wetenschap proces in een end-to-end-scenario met een [Azure HDInsight Hadoop-cluster](https://azure.microsoft.com/services/hdinsight/) om op te slaan, verkennen, functie engineer van en naar beneden voorbeeldgegevens uit een van algemeen beschikbaar [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="71afe-104">In this walkthrough, we demonstrate using the Team Data Science Process in an end-to-end scenario with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore, feature engineer, and down sample data from one of the publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) datasets.</span></span> <span data-ttu-id="71afe-105">We Azure Machine Learning gebruiken voor het bouwen van een binaire classificatie-model in deze gegevens.</span><span class="sxs-lookup"><span data-stu-id="71afe-105">We use Azure Machine Learning to build a binary classification model on this data.</span></span> <span data-ttu-id="71afe-106">Ook laten we zien hoe u een van deze modellen als een webservice publiceert.</span><span class="sxs-lookup"><span data-stu-id="71afe-106">We also show how to publish one of these models as a Web service.</span></span>

<span data-ttu-id="71afe-107">Het is ook mogelijk om te gebruiken een laptop IPython taken die zijn gepresenteerd in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="71afe-107">It is also possible to use an IPython notebook to accomplish the tasks presented in this walkthrough.</span></span> <span data-ttu-id="71afe-108">Gebruikers die u wilt proberen deze benadering moeten contact opnemen met de [Criteo scenario met behulp van een verbinding Hive ODBC](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="71afe-108">Users who would like to try this approach should consult the [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="71afe-109"><a name="dataset"></a>Beschrijving van de gegevensset Criteo</span><span class="sxs-lookup"><span data-stu-id="71afe-109"><a name="dataset"></a>Criteo Dataset Description</span></span>
<span data-ttu-id="71afe-110">De Criteo gegevens is een klik voorspelling gegevensset die ongeveer 370GB gecomprimeerde gzip TSV-bestanden (~1.3TB ongecomprimeerde), die bestaat uit meer dan 4.3 miljard records.</span><span class="sxs-lookup"><span data-stu-id="71afe-110">The Criteo data is a click prediction dataset that is approximately 370GB of gzip compressed TSV files (~1.3TB uncompressed), comprising more than 4.3 billion records.</span></span> <span data-ttu-id="71afe-111">Het is afkomstig uit 24 dagen van klik dan op gegevens die de [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span><span class="sxs-lookup"><span data-stu-id="71afe-111">It is taken from 24 days of click data made available by [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span></span> <span data-ttu-id="71afe-112">Voor het gemak van gegevenswetenschappers, hebben we gegevens beschikbaar voor ons om te experimenteren met uitgepakt.</span><span class="sxs-lookup"><span data-stu-id="71afe-112">For the convenience of data scientists, we have unzipped data available to us to experiment with.</span></span>

<span data-ttu-id="71afe-113">Elke record in deze gegevensset bevat 40 kolommen:</span><span class="sxs-lookup"><span data-stu-id="71afe-113">Each record in this dataset contains 40 columns:</span></span>

* <span data-ttu-id="71afe-114">de eerste kolom is een labelkolom waarin wordt aangegeven of een gebruiker klikt op een **toevoegen** (waarde 1) of niet op een (waarde 0)</span><span class="sxs-lookup"><span data-stu-id="71afe-114">the first column is a label column that indicates whether a user clicks an **add** (value 1) or does not click one (value 0)</span></span>
* <span data-ttu-id="71afe-115">naast 13 kolommen zijn numerieke, en</span><span class="sxs-lookup"><span data-stu-id="71afe-115">next 13 columns are numeric, and</span></span>
* <span data-ttu-id="71afe-116">laatste 26 zijn categorische kolommen</span><span class="sxs-lookup"><span data-stu-id="71afe-116">last 26 are categorical columns</span></span>

<span data-ttu-id="71afe-117">De kolommen zijn geanonimiseerde en gebruiken van een reeks geïnventariseerde namen: "Col1' (voor de labelkolom) naar ' Col40 ' (voor de laatste categorische kolom).</span><span class="sxs-lookup"><span data-stu-id="71afe-117">The columns are anonymized and use a series of enumerated names: "Col1" (for the label column) to 'Col40" (for the last categorical column).</span></span>            

<span data-ttu-id="71afe-118">Hier volgt een fragment van de eerste 20 kolommen uit twee rapporten (rijen) van deze gegevensset:</span><span class="sxs-lookup"><span data-stu-id="71afe-118">Here is an excerpt of the first 20 columns of two observations (rows) from this dataset:</span></span>

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

<span data-ttu-id="71afe-119">Er zijn ontbreken waarden in de numerieke en categorische kolommen in deze dataset.</span><span class="sxs-lookup"><span data-stu-id="71afe-119">There are missing values in both the numeric and categorical columns in this dataset.</span></span> <span data-ttu-id="71afe-120">Een eenvoudige methode voor het verwerken van de ontbrekende waarden worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="71afe-120">We describe a simple method for handling the missing values.</span></span> <span data-ttu-id="71afe-121">Aanvullende details van de gegevens worden verkend wanneer we ze opslaan in de Hive-tabellen.</span><span class="sxs-lookup"><span data-stu-id="71afe-121">Additional details of the data are explored when we store them into Hive tables.</span></span>

<span data-ttu-id="71afe-122">**Definitie:** *Clickthrough-snelheid (CTR):* dit is het percentage muisklikken in de gegevens.</span><span class="sxs-lookup"><span data-stu-id="71afe-122">**Definition:** *Clickthrough rate (CTR):* This is the percentage of clicks in the data.</span></span> <span data-ttu-id="71afe-123">In deze dataset Criteo is de CTR ongeveer 3.3% of 0.033.</span><span class="sxs-lookup"><span data-stu-id="71afe-123">In this Criteo dataset, the CTR is about 3.3% or 0.033.</span></span>

## <span data-ttu-id="71afe-124"><a name="mltasks"></a>Voorbeelden van voorspelling taken</span><span class="sxs-lookup"><span data-stu-id="71afe-124"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="71afe-125">Twee voorbeeld voorspelling problemen worden in dit scenario behandeld:</span><span class="sxs-lookup"><span data-stu-id="71afe-125">Two sample prediction problems are addressed in this walkthrough:</span></span>

1. <span data-ttu-id="71afe-126">**Binaire classificatie**: voorspelt of een gebruiker een add geklikt:</span><span class="sxs-lookup"><span data-stu-id="71afe-126">**Binary classification**: Predicts whether a user clicked an add:</span></span>
   
   * <span data-ttu-id="71afe-127">Klasse 0: Er is geen Klik</span><span class="sxs-lookup"><span data-stu-id="71afe-127">Class 0: No Click</span></span>
   * <span data-ttu-id="71afe-128">Klasse 1: klik op</span><span class="sxs-lookup"><span data-stu-id="71afe-128">Class 1: Click</span></span>
2. <span data-ttu-id="71afe-129">**Regressie**: de waarschijnlijkheid van een ad-klik van functies voor gebruikers worden voorspeld.</span><span class="sxs-lookup"><span data-stu-id="71afe-129">**Regression**: Predicts the probability of an ad click from user features.</span></span>

## <span data-ttu-id="71afe-130"><a name="setup"></a>Instellen van een HDInsight Hadoop-cluster voor gegevenswetenschap</span><span class="sxs-lookup"><span data-stu-id="71afe-130"><a name="setup"></a>Set Up an HDInsight Hadoop cluster for data science</span></span>
<span data-ttu-id="71afe-131">**Opmerking:** dit is doorgaans een **Admin** taak.</span><span class="sxs-lookup"><span data-stu-id="71afe-131">**Note:** This is typically an **Admin** task.</span></span>

<span data-ttu-id="71afe-132">Instellen van uw Azure-Gegevenswetenschap-omgeving voor het bouwen van predictive analytics-oplossingen met HDInsight-clusters in drie stappen:</span><span class="sxs-lookup"><span data-stu-id="71afe-132">Set up your Azure Data Science environment for building predictive analytics solutions with HDInsight clusters in three steps:</span></span>

1. <span data-ttu-id="71afe-133">[Een opslagaccount maken](../storage/common/storage-create-storage-account.md): dit opslagaccount wordt gebruikt voor het opslaan van gegevens in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="71afe-133">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used to store data in Azure Blob Storage.</span></span> <span data-ttu-id="71afe-134">De gegevens in HDInsight-clusters gebruikt, wordt hier opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="71afe-134">The data used in HDInsight clusters is stored here.</span></span>
2. <span data-ttu-id="71afe-135">[Azure HDInsight Hadoop-Clusters aanpassen voor Gegevenswetenschap](machine-learning-data-science-customize-hadoop-cluster.md): deze stap maakt u een Azure HDInsight Hadoop-cluster met 64-bits Anaconda Python 2.7 is geïnstalleerd op alle knooppunten.</span><span class="sxs-lookup"><span data-stu-id="71afe-135">[Customize Azure HDInsight Hadoop Clusters for Data Science](machine-learning-data-science-customize-hadoop-cluster.md): This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="71afe-136">Er zijn twee belangrijke stappen die u (in dit onderwerp beschreven) moeten worden uitgevoerd bij het aanpassen van het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="71afe-136">There are two important steps (described in this topic) to complete when customizing the HDInsight cluster.</span></span>
   
   * <span data-ttu-id="71afe-137">Het opslagaccount dat is gemaakt in stap 1 met uw HDInsight-cluster wanneer deze wordt gemaakt, moet u koppelen.</span><span class="sxs-lookup"><span data-stu-id="71afe-137">You must link the storage account created in step 1 with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="71afe-138">Dit opslagaccount wordt gebruikt voor toegang tot gegevens die kunnen worden verwerkt binnen het cluster.</span><span class="sxs-lookup"><span data-stu-id="71afe-138">This storage account is used for accessing data that can be processed within the cluster.</span></span>
   * <span data-ttu-id="71afe-139">Nadat deze is gemaakt, moet u externe toegang inschakelen met het hoofdknooppunt van het cluster.</span><span class="sxs-lookup"><span data-stu-id="71afe-139">You must enable Remote Access to the head node of the cluster after it is created.</span></span> <span data-ttu-id="71afe-140">Vergeet niet de RAS-referenties die u hier opgeeft (anders dan die zijn opgegeven voor het cluster bij het maken ervan): u moet de volgende procedures uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="71afe-140">Remember the remote access credentials you specify here (different from those specified for the cluster at its creation): you need them to complete the following procedures.</span></span>
3. <span data-ttu-id="71afe-141">[Maken van een Azure ML-werkruimte](machine-learning-create-workspace.md): deze Azure Machine Learning-werkruimte wordt gebruikt voor het bouwen van machine learning-modellen na een initiële gegevensverkenning en omlaag steekproeven op het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="71afe-141">[Create an Azure ML workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used for building machine learning models after an initial data exploration and down sampling on the HDInsight cluster.</span></span>

## <span data-ttu-id="71afe-142"><a name="getdata"></a>Ophalen van gegevens en gebruiken van een openbare bron</span><span class="sxs-lookup"><span data-stu-id="71afe-142"><a name="getdata"></a>Get and consume data from a public source</span></span>
<span data-ttu-id="71afe-143">De [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) dataset kan worden geopend door op de koppeling te klikken, de gebruiksvoorwaarden accepteren en een naam geven.</span><span class="sxs-lookup"><span data-stu-id="71afe-143">The [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) dataset can be accessed by clicking on the link, accepting the terms of use, and providing a name.</span></span> <span data-ttu-id="71afe-144">Hier ziet u een momentopname van wat ziet deze als eruit:</span><span class="sxs-lookup"><span data-stu-id="71afe-144">A snapshot of what this looks like is shown here:</span></span>

![Criteo voorwaarden accepteren](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

<span data-ttu-id="71afe-146">Klik op **doorgaan naar downloaden** voor meer informatie over de gegevensset en de beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="71afe-146">Click **Continue to Download** to read more about the dataset and its availability.</span></span>

<span data-ttu-id="71afe-147">De gegevens zich in een openbare [Azure blob-opslag](../storage/blobs/storage-dotnet-how-to-use-blobs.md) locatie: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span><span class="sxs-lookup"><span data-stu-id="71afe-147">The data resides in a public [Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) location: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span></span> <span data-ttu-id="71afe-148">De 'wasb"verwijst naar Azure Blob Storage-locatie.</span><span class="sxs-lookup"><span data-stu-id="71afe-148">The "wasb" refers to Azure Blob Storage location.</span></span> 

1. <span data-ttu-id="71afe-149">De gegevens in deze openbare blob-opslag bestaat uit drie submappen van uitgepakte gegevens.</span><span class="sxs-lookup"><span data-stu-id="71afe-149">The data in this public blob storage consists of three subfolders of unzipped data.</span></span>
   
   1. <span data-ttu-id="71afe-150">De submap *Onbewerkte/telling/* bevat de eerste 21 dagen aan gegevens - vanaf dag\_00 op dag\_20</span><span class="sxs-lookup"><span data-stu-id="71afe-150">The subfolder *raw/count/* contains the first 21 days of data - from day\_00 to day\_20</span></span>
   2. <span data-ttu-id="71afe-151">De submap *onbewerkte/train/* bestaat uit één dag van gegevens, dag\_21</span><span class="sxs-lookup"><span data-stu-id="71afe-151">The subfolder *raw/train/* consists of a single day of data, day\_21</span></span>
   3. <span data-ttu-id="71afe-152">De submap *onbewerkte en testen/* bestaat uit twee dagen aan gegevens, dag\_22 en dag\_23</span><span class="sxs-lookup"><span data-stu-id="71afe-152">The subfolder *raw/test/* consists of two days of data, day\_22 and day\_23</span></span>
2. <span data-ttu-id="71afe-153">Voor degenen die moet worden gestart met de onbewerkte gzip-gegevens, zijn ook beschikbaar in de hoofdmap *onbewerkte /* als day_NN.gz, waarbij NN tussen 00 en 23 gaat.</span><span class="sxs-lookup"><span data-stu-id="71afe-153">For those who want to start with the raw gzip data, these are also available in the main folder *raw/* as day_NN.gz, where NN goes from 00 to 23.</span></span>

<span data-ttu-id="71afe-154">Een alternatieve methode om toegang tot, onderzoek en het model dat deze gegevens waarvoor lokale downloads niet verderop in dit scenario wordt uitgelegd wanneer we Hive-tabellen maken.</span><span class="sxs-lookup"><span data-stu-id="71afe-154">An alternative approach to access, explore, and model this data that does not require any local downloads is explained later in this walkthrough when we create Hive tables.</span></span>

## <span data-ttu-id="71afe-155"><a name="login"></a>Meld u aan het cluster headnode bij</span><span class="sxs-lookup"><span data-stu-id="71afe-155"><a name="login"></a>Log in to the cluster headnode</span></span>
<span data-ttu-id="71afe-156">Voor het aanmelden bij de headnode van het cluster, gebruikt u de [Azure-portal](https://ms.portal.azure.com) vinden van het cluster.</span><span class="sxs-lookup"><span data-stu-id="71afe-156">To log in to the headnode of the cluster, use the [Azure portal](https://ms.portal.azure.com) to locate the cluster.</span></span> <span data-ttu-id="71afe-157">Klik op het pictogram HDInsight plaats aan de linkerkant en dubbelklik vervolgens op de naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="71afe-157">Click the HDInsight elephant icon on the left and then double-click the name of your cluster.</span></span> <span data-ttu-id="71afe-158">Navigeer naar de **configuratie** tabblad, dubbelklik op het pictogram CONNECT aan de onderkant van de pagina en geef uw referenties voor externe toegang als u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="71afe-158">Navigate to the **Configuration** tab, double-click the CONNECT icon on the bottom of the page, and enter your remote access credentials when prompted.</span></span> <span data-ttu-id="71afe-159">Hiermee gaat u naar de headnode van het cluster.</span><span class="sxs-lookup"><span data-stu-id="71afe-159">This takes you to the headnode of the cluster.</span></span>

<span data-ttu-id="71afe-160">Hier volgt een typisch eerst aanmelden op het cluster headnode ziet er als:</span><span class="sxs-lookup"><span data-stu-id="71afe-160">Here is what a typical first log in to the cluster headnode looks like:</span></span>

![Meld u aan het cluster](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

<span data-ttu-id="71afe-162">Aan de linkerkant ziet u de ' Hadoop opdrachtregel ', die onze werkpaard voor de gegevensverkenning is.</span><span class="sxs-lookup"><span data-stu-id="71afe-162">On the left, we see the "Hadoop Command Line", which is our workhorse for the data exploration.</span></span> <span data-ttu-id="71afe-163">Ook ziet u twee nuttig URL's - 'Hadoop Yarn Status' en 'Hadoop de naam van knooppunt'.</span><span class="sxs-lookup"><span data-stu-id="71afe-163">We also see two useful URLs - "Hadoop Yarn Status" and "Hadoop Name Node".</span></span> <span data-ttu-id="71afe-164">De URL van de status yarn geeft de voortgang van de taak en de URL van de naam van knooppunt geeft informatie over de configuratie van het cluster.</span><span class="sxs-lookup"><span data-stu-id="71afe-164">The yarn status URL shows job progress and the name node URL gives details on the cluster configuration.</span></span>

<span data-ttu-id="71afe-165">Nu we worden ingesteld en klaar om te beginnen met de eerste deel van deze stapsgewijze Kennismaking: gegevensverkenning gebruik van Hive en voorbereiden van gegevens voor Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="71afe-165">Now we are set up and ready to begin first part of the walkthrough: data exploration using Hive and getting data ready for Azure Machine Learning.</span></span>

## <span data-ttu-id="71afe-166"><a name="hive-db-tables"></a>Hive-database en tabellen maken</span><span class="sxs-lookup"><span data-stu-id="71afe-166"><a name="hive-db-tables"></a> Create Hive database and tables</span></span>
<span data-ttu-id="71afe-167">Voor het maken van Hive-tabellen voor onze gegevensset Criteo, opent u de ***Hadoop-opdrachtregel*** op het bureaublad van het hoofdknooppunt en voer de Hive-map met de opdracht</span><span class="sxs-lookup"><span data-stu-id="71afe-167">To create Hive tables for our Criteo dataset, open the ***Hadoop Command Line*** on the desktop of the head node, and enter the Hive directory by entering the command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="71afe-168">Alle Hive-opdrachten uitvoeren in dit overzicht van de opslaglocatie Hive / directory prompt.</span><span class="sxs-lookup"><span data-stu-id="71afe-168">Run all Hive commands in this walkthrough from the Hive bin/ directory prompt.</span></span> <span data-ttu-id="71afe-169">Dit zorgt voor problemen die pad automatisch.</span><span class="sxs-lookup"><span data-stu-id="71afe-169">This takes care of any path issues automatically.</span></span> <span data-ttu-id="71afe-170">We gebruiken de termen 'Hive directory prompt', ' Hive bin / directory prompt ', en ' Hadoop opdrachtregel ' door elkaar.</span><span class="sxs-lookup"><span data-stu-id="71afe-170">We use the terms "Hive directory prompt", "Hive bin/ directory prompt", and "Hadoop Command Line" interchangeably.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="71afe-171">Voor het uitvoeren van een Hive-query, kan een altijd gebruik van de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="71afe-171">To execute any Hive query, one can always use the following commands:</span></span>
> 
> 

        cd %hive_home%\bin
        hive

<span data-ttu-id="71afe-172">Nadat de Hive-REPL wordt weergegeven met een ' hive > "aanmelden, gewoon knippen en plakken de query voor het uitvoeren van deze.</span><span class="sxs-lookup"><span data-stu-id="71afe-172">After the Hive REPL appears with a "hive >"sign, simply cut and paste the query to execute it.</span></span>

<span data-ttu-id="71afe-173">De volgende code maakt een database 'criteo' en genereert vervolgens 4 tabellen:</span><span class="sxs-lookup"><span data-stu-id="71afe-173">The following code creates a database "criteo" and then generates 4 tables:</span></span>

* <span data-ttu-id="71afe-174">een *tabel voor het genereren van aantallen* gebouwd op dagen dag\_00 op dag\_20,</span><span class="sxs-lookup"><span data-stu-id="71afe-174">a *table for generating counts* built on days day\_00 to day\_20,</span></span>
* <span data-ttu-id="71afe-175">een *tabel voor gebruik als de trein gegevensset* gebouwd op dag\_21, en</span><span class="sxs-lookup"><span data-stu-id="71afe-175">a *table for use as the train dataset* built on day\_21, and</span></span>
* <span data-ttu-id="71afe-176">twee *tabellen voor gebruik als de test-gegevenssets* gebouwd op dag\_22 en dag\_23 respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="71afe-176">two *tables for use as the test datasets* built on day\_22 and day\_23 respectively.</span></span>

<span data-ttu-id="71afe-177">We onze testgegevensset opgesplitst in twee verschillende tabellen omdat een van de dagen een vakantie is en we bepalen willen als het model verschillen tussen een feestdag en niet van de snelheid clickthrough kunt detecteren.</span><span class="sxs-lookup"><span data-stu-id="71afe-177">We split our test dataset into two different tables because one of the days is a holiday, and we want to determine if the model can detect differences between a holiday and non-holiday from the clickthrough rate.</span></span>

<span data-ttu-id="71afe-178">Het script [voorbeeld &#95; hive &#95; maken &#95; criteo &#95; database &#95; en &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) voor het gemak Hier wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="71afe-178">The script [sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) is displayed here for convenience:</span></span>

    CREATE DATABASE IF NOT EXISTS criteo;
    DROP TABLE IF EXISTS criteo.criteo_count;
    CREATE TABLE criteo.criteo_count (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/count';

    DROP TABLE IF EXISTS criteo.criteo_train;
    CREATE TABLE criteo.criteo_train (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/train';

    DROP TABLE IF EXISTS criteo.criteo_test_day_22;
    CREATE TABLE criteo.criteo_test_day_22 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_22';

    DROP TABLE IF EXISTS criteo.criteo_test_day_23;
    CREATE TABLE criteo.criteo_test_day_23 (
    col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE LOCATION 'wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/test/day_23';

<span data-ttu-id="71afe-179">We Houd er rekening mee dat alle tabellen in deze externe zijn als we simpelweg naar Azure Blob Storage (wasb)-locaties wijst.</span><span class="sxs-lookup"><span data-stu-id="71afe-179">We note that all these tables are external as we simply point to Azure Blob Storage (wasb) locations.</span></span>

<span data-ttu-id="71afe-180">**Er zijn twee manieren een Hive-query die we nu vermeld uit te voeren.**</span><span class="sxs-lookup"><span data-stu-id="71afe-180">**There are two ways to execute ANY Hive query that we now mention.**</span></span>

1. <span data-ttu-id="71afe-181">**Met behulp van de opdrachtregel Hive-REPL**: de eerste is voor het verlenen van een opdracht 'hive' en kopieer en plak een query op de opdrachtregel Hive-REPL.</span><span class="sxs-lookup"><span data-stu-id="71afe-181">**Using the Hive REPL command-line**: The first is to issue a "hive" command and copy and paste a query at the Hive REPL command-line.</span></span> <span data-ttu-id="71afe-182">U doet dit door het volgende te doen:</span><span class="sxs-lookup"><span data-stu-id="71afe-182">To do this, do:</span></span>
   
        cd %hive_home%\bin
        hive
   
     <span data-ttu-id="71afe-183">Nu op de opdrachtregel REPL knippen en plakken van de query wordt uitgevoerd het.</span><span class="sxs-lookup"><span data-stu-id="71afe-183">Now at the REPL command-line, cutting and pasting the query executes it.</span></span>
2. <span data-ttu-id="71afe-184">**Een query's opslaan en uitvoeren van de opdracht**: de tweede is het opslaan van de query's in een bestand .hql ([voorbeeld &#95; hive &#95; maken &#95; criteo &#95; database &#95; en &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) en vervolgens voert u de volgende opdracht de query uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="71afe-184">**Saving queries to a file and executing the command**: The second is to save the queries to a .hql file ([sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) and then issue the following command to execute the query:</span></span>
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a><span data-ttu-id="71afe-185">Het maken van database en tabel bevestigen</span><span class="sxs-lookup"><span data-stu-id="71afe-185">Confirm database and table creation</span></span>
<span data-ttu-id="71afe-186">Vervolgens wordt het maken van de database met de volgende opdracht uit de Hive-opslaglocatie bevestigen / opdrachtprompt van de map:</span><span class="sxs-lookup"><span data-stu-id="71afe-186">Next, we confirm the creation of the database with the following command from the Hive bin/ directory prompt:</span></span>

        hive -e "show databases;"

<span data-ttu-id="71afe-187">Hierdoor hebt:</span><span class="sxs-lookup"><span data-stu-id="71afe-187">This gives:</span></span>

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

<span data-ttu-id="71afe-188">Hiermee bevestigt u het maken van de nieuwe database 'criteo'.</span><span class="sxs-lookup"><span data-stu-id="71afe-188">This confirms the creation of the new database, "criteo".</span></span>

<span data-ttu-id="71afe-189">Om te zien welke tabellen die zijn gemaakt, geven we gewoon de opdracht uit de Hive-opslaglocatie / opdrachtprompt van de map:</span><span class="sxs-lookup"><span data-stu-id="71afe-189">To see what tables we created, we simply issue the command here from the Hive bin/ directory prompt:</span></span>

        hive -e "show tables in criteo;"

<span data-ttu-id="71afe-190">Vervolgens ziet u de volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="71afe-190">We then see the following output:</span></span>

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <span data-ttu-id="71afe-191"><a name="exploration"></a>Gegevensverkenning in component</span><span class="sxs-lookup"><span data-stu-id="71afe-191"><a name="exploration"></a> Data exploration in Hive</span></span>
<span data-ttu-id="71afe-192">We kunnen nu klaar voor sommige basic gegevensverkenning in Hive.</span><span class="sxs-lookup"><span data-stu-id="71afe-192">Now we are ready to do some basic data exploration in Hive.</span></span> <span data-ttu-id="71afe-193">We beginnen met het aantal voorbeelden in de trein tellen en gegevenstabellen testen.</span><span class="sxs-lookup"><span data-stu-id="71afe-193">We begin by counting the number of examples in the train and test data tables.</span></span>

### <a name="number-of-train-examples"></a><span data-ttu-id="71afe-194">Aantal train-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="71afe-194">Number of train examples</span></span>
<span data-ttu-id="71afe-195">De inhoud van [voorbeeld &#95; hive &#95; & #95 tellen; train &#95; tabel &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) worden hier weergegeven:</span><span class="sxs-lookup"><span data-stu-id="71afe-195">The contents of [sample&#95;hive&#95;count&#95;train&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) are shown here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_train;

<span data-ttu-id="71afe-196">Dit levert:</span><span class="sxs-lookup"><span data-stu-id="71afe-196">This yields:</span></span>

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

<span data-ttu-id="71afe-197">U kunt ook een mag de volgende opdracht uit de Hive-opslaglocatie eveneens verlenen / opdrachtprompt van de map:</span><span class="sxs-lookup"><span data-stu-id="71afe-197">Alternatively, one may also issue the following command from the Hive bin/ directory prompt:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-the-two-test-datasets"></a><span data-ttu-id="71afe-198">Aantal voorbeelden van de test in de twee gegevenssets van de test</span><span class="sxs-lookup"><span data-stu-id="71afe-198">Number of test examples in the two test datasets</span></span>
<span data-ttu-id="71afe-199">We tellen het aantal voorbeelden in de twee gegevenssets van de test nu.</span><span class="sxs-lookup"><span data-stu-id="71afe-199">We now count the number of examples in the two test datasets.</span></span> <span data-ttu-id="71afe-200">De inhoud van [voorbeeld &#95; hive &#95; & #95 tellen; criteo &#95; test &#95; dag &#95; 22 &#95; tabel &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) hier zijn:</span><span class="sxs-lookup"><span data-stu-id="71afe-200">The contents of [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;22&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) are here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

<span data-ttu-id="71afe-201">Dit levert:</span><span class="sxs-lookup"><span data-stu-id="71afe-201">This yields:</span></span>

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

<span data-ttu-id="71afe-202">Gebruikelijke we ook het script kan aanroepen vanuit de Hive-opslaglocatie / Active directory vragen door de opdracht:</span><span class="sxs-lookup"><span data-stu-id="71afe-202">As usual, we may also call the script from the Hive bin/ directory prompt by issuing the command:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

<span data-ttu-id="71afe-203">Ten slotte wordt het aantal voorbeelden van de test in de testgegevensset op basis van dag onderzoeken\_23.</span><span class="sxs-lookup"><span data-stu-id="71afe-203">Finally, we examine the number of test examples in the test dataset based on day\_23.</span></span>

<span data-ttu-id="71afe-204">De opdracht om dit te doen is vergelijkbaar met alleen wordt weergegeven (Raadpleeg [voorbeeld &#95; hive &#95; & #95 tellen; criteo &#95; test &#95; dag &#95; 23 &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span><span class="sxs-lookup"><span data-stu-id="71afe-204">The command to do this is similar to the one just shown (refer to [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;23&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

<span data-ttu-id="71afe-205">Hierdoor hebt:</span><span class="sxs-lookup"><span data-stu-id="71afe-205">This gives:</span></span>

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-the-train-dataset"></a><span data-ttu-id="71afe-206">Distributiepunten in de gegevensset train label</span><span class="sxs-lookup"><span data-stu-id="71afe-206">Label distribution in the train dataset</span></span>
<span data-ttu-id="71afe-207">De distributie van het label in de gegevensset train is van belang.</span><span class="sxs-lookup"><span data-stu-id="71afe-207">The label distribution in the train dataset is of interest.</span></span> <span data-ttu-id="71afe-208">Als u wilt dit ziet, laten we zien inhoud van [voorbeeld &#95; hive &#95; criteo &#95; & #95 label; verdeling &#95; train &#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span><span class="sxs-lookup"><span data-stu-id="71afe-208">To see this, we show contents of [sample&#95;hive&#95;criteo&#95;label&#95;distribution&#95;train&#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span></span>

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

<span data-ttu-id="71afe-209">Dit geeft de label-distributie:</span><span class="sxs-lookup"><span data-stu-id="71afe-209">This yields the label distribution:</span></span>

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

<span data-ttu-id="71afe-210">Houd er rekening mee dat het percentage positieve labels ongeveer 3.3% (consistent met de oorspronkelijke gegevensset is).</span><span class="sxs-lookup"><span data-stu-id="71afe-210">Note that the percentage of positive labels is about 3.3% (consistent with the original dataset).</span></span>

### <a name="histogram-distributions-of-some-numeric-variables-in-the-train-dataset"></a><span data-ttu-id="71afe-211">Histogram distributies van bepaalde numerieke variabelen in de gegevensset train</span><span class="sxs-lookup"><span data-stu-id="71afe-211">Histogram distributions of some numeric variables in the train dataset</span></span>
<span data-ttu-id="71afe-212">We kunnen gebruiken van Hive systeemeigen ' histogram\_numerieke ' functie om erachter te komen hoe de distributie van de numerieke variabelen eruit ziet.</span><span class="sxs-lookup"><span data-stu-id="71afe-212">We can use Hive's native "histogram\_numeric" function to find out what the distribution of the numeric variables looks like.</span></span> <span data-ttu-id="71afe-213">Hier vindt u de inhoud van [voorbeeld &#95; hive &#95; criteo &#95; histogram &#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span><span class="sxs-lookup"><span data-stu-id="71afe-213">Here are the contents of [sample&#95;hive&#95;criteo&#95;histogram&#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span></span>

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

<span data-ttu-id="71afe-214">Dit resulteert in het volgende:</span><span class="sxs-lookup"><span data-stu-id="71afe-214">This yields the following:</span></span>

        26      155878415
        2606    92753
        6755    22086
        11202   6922
        14432   4163
        17815   2488
        21072   1901
        24113   1283
        27429   1225
        30818   906
        34512   723
        38026   387
        41007   290
        43417   312
        45797   571
        49819   428
        53505   328
        56853   527
        61004   160
        65510   3446
        Time taken: 317.851 seconds, Fetched: 20 row(s)

<span data-ttu-id="71afe-215">De LATERAL BEELD - vouwen combinatie in Hive fungeert voor het produceren van een SQL-achtige uitvoer in plaats van de gebruikelijke lijst.</span><span class="sxs-lookup"><span data-stu-id="71afe-215">The LATERAL VIEW - explode combination in Hive serves to produce a SQL-like output instead of the usual list.</span></span> <span data-ttu-id="71afe-216">Houd er rekening mee dat in deze tabel de eerste kolom komt overeen met de opslaglocatie center en de tweede de frequentie van de opslaglocatie.</span><span class="sxs-lookup"><span data-stu-id="71afe-216">Note that in the this table, the first column corresponds to the bin center and the second to the bin frequency.</span></span>

### <a name="approximate-percentiles-of-some-numeric-variables-in-the-train-dataset"></a><span data-ttu-id="71afe-217">Geschatte percentielen van bepaalde numerieke variabelen in de gegevensset train</span><span class="sxs-lookup"><span data-stu-id="71afe-217">Approximate percentiles of some numeric variables in the train dataset</span></span>
<span data-ttu-id="71afe-218">Is ook de berekening van de geschatte percentielen van belang met numerieke variabelen.</span><span class="sxs-lookup"><span data-stu-id="71afe-218">Also of interest with numeric variables is the computation of approximate percentiles.</span></span> <span data-ttu-id="71afe-219">Hive de systeemeigen ' percentiel\_ongeveer ' Dit wordt uitgevoerd voor ons.</span><span class="sxs-lookup"><span data-stu-id="71afe-219">Hive's native "percentile\_approx" does this for us.</span></span> <span data-ttu-id="71afe-220">De inhoud van [voorbeeld &#95; hive &#95; criteo &#95; geschatte &#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) zijn:</span><span class="sxs-lookup"><span data-stu-id="71afe-220">The contents of [sample&#95;hive&#95;criteo&#95;approximate&#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) are:</span></span>

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

<span data-ttu-id="71afe-221">Dit levert:</span><span class="sxs-lookup"><span data-stu-id="71afe-221">This yields:</span></span>

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

<span data-ttu-id="71afe-222">We dat de distributie van percentielen is verwant aan de distributie van het histogram van een numerieke variabele meestal te schakelen.</span><span class="sxs-lookup"><span data-stu-id="71afe-222">We remark that the distribution of percentiles is closely related to the histogram distribution of any numeric variable usually.</span></span>         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-the-train-dataset"></a><span data-ttu-id="71afe-223">Aantal unieke waarden vinden voor sommige categorische kolommen in de gegevensset train</span><span class="sxs-lookup"><span data-stu-id="71afe-223">Find number of unique values for some categorical columns in the train dataset</span></span>
<span data-ttu-id="71afe-224">U doorgaat met de gegevensverkenning, vinden we nu, voor sommige categorische kolommen, het aantal unieke waarden die ze nemen.</span><span class="sxs-lookup"><span data-stu-id="71afe-224">Continuing the data exploration, we now find, for some categorical columns, the number of unique values they take.</span></span> <span data-ttu-id="71afe-225">U doet dit door laten we zien inhoud van [voorbeeld &#95; hive &#95; criteo &#95; unieke &#95; waarden &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span><span class="sxs-lookup"><span data-stu-id="71afe-225">To do this, we show contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span></span>

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

<span data-ttu-id="71afe-226">Dit levert:</span><span class="sxs-lookup"><span data-stu-id="71afe-226">This yields:</span></span>

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

<span data-ttu-id="71afe-227">We Houd er rekening mee dat Col15 19M unieke waarden bevat.</span><span class="sxs-lookup"><span data-stu-id="71afe-227">We note that Col15 has 19M unique values!</span></span> <span data-ttu-id="71afe-228">Met behulp van naïve technieken zoals 'één hot codering' is voor het coderen van dergelijke hoge dimensionale categorische variabelen onbruikbare.</span><span class="sxs-lookup"><span data-stu-id="71afe-228">Using naive techniques like "one-hot encoding" to encode such high-dimensional categorical variables is infeasible.</span></span> <span data-ttu-id="71afe-229">In het bijzonder we uitleggen en demonstreren van een krachtige, robuuste techniek aangeroepen [Learning met telt](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) voor efficiënt aanpakken van dit probleem.</span><span class="sxs-lookup"><span data-stu-id="71afe-229">In particular, we explain and demonstrate a powerful, robust technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) for tackling this problem efficiently.</span></span>

<span data-ttu-id="71afe-230">We beëindigen deze subsectie door te kijken naar het aantal unieke waarden voor sommige andere categorische kolommen ook.</span><span class="sxs-lookup"><span data-stu-id="71afe-230">We end this sub-section by looking at the number of unique values for some other categorical columns as well.</span></span> <span data-ttu-id="71afe-231">De inhoud van [voorbeeld &#95; hive &#95; criteo &#95; unieke &#95; waarden &#95; meerdere &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) zijn:</span><span class="sxs-lookup"><span data-stu-id="71afe-231">The contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;multiple&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) are:</span></span>

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

<span data-ttu-id="71afe-232">Dit levert:</span><span class="sxs-lookup"><span data-stu-id="71afe-232">This yields:</span></span>

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

<span data-ttu-id="71afe-233">Opnieuw zien we dat Col20, met uitzondering van de kolommen veel unieke waarden.</span><span class="sxs-lookup"><span data-stu-id="71afe-233">Again we see that except for Col20, all the other columns have many unique values.</span></span>

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-the-train-dataset"></a><span data-ttu-id="71afe-234">Mede exemplaar telt paren van categorische variabelen in de gegevensset train</span><span class="sxs-lookup"><span data-stu-id="71afe-234">Co-occurrence counts of pairs of categorical variables in the train dataset</span></span>

<span data-ttu-id="71afe-235">Het aantal mede exemplaar uit paren van categorische variabelen is ook van belang.</span><span class="sxs-lookup"><span data-stu-id="71afe-235">The co-occurrence counts of pairs of categorical variables is also of interest.</span></span> <span data-ttu-id="71afe-236">Dit kan worden bepaald met de code in [voorbeeld &#95; hive &#95; criteo &#95; gekoppeld &#95; categorische &#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span><span class="sxs-lookup"><span data-stu-id="71afe-236">This can be determined using the code in [sample&#95;hive&#95;criteo&#95;paired&#95;categorical&#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span></span>

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

<span data-ttu-id="71afe-237">We omgekeerde hun exemplaar van het aantal sorteren en zoek boven 15 in dit geval.</span><span class="sxs-lookup"><span data-stu-id="71afe-237">We reverse order the counts by their occurrence and look at the top 15 in this case.</span></span> <span data-ttu-id="71afe-238">Hierdoor hebt ons:</span><span class="sxs-lookup"><span data-stu-id="71afe-238">This gives us:</span></span>

        ad98e872        cea68cd3        8964458
        ad98e872        3dbb483e        8444762
        ad98e872        43ced263        3082503
        ad98e872        420acc05        2694489
        ad98e872        ac4c5591        2559535
        ad98e872        fb1e95da        2227216
        ad98e872        8af1edc8        1794955
        ad98e872        e56937ee        1643550
        ad98e872        d1fade1c        1348719
        ad98e872        977b4431        1115528
        e5f3fd8d        a15d1051        959252
        ad98e872        dd86c04a        872975
        349b3fec        a52ef97d        821062
        e5f3fd8d        a0aaffa6        792250
        265366bf        6f5c7c41        782142
        Time taken: 560.22 seconds, Fetched: 15 row(s)

## <span data-ttu-id="71afe-239"><a name="downsample"></a>Omlaag voorbeeld gegevenssets voor Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="71afe-239"><a name="downsample"></a> Down sample the datasets for Azure Machine Learning</span></span>
<span data-ttu-id="71afe-240">Met de gegevenssets verkend en gedemonstreerd hoe we kan doen dit soort exploratie geen variabelen (waaronder combinaties), wordt nu naar beneden voorbeeld de gegevenssets zodat we modellen in Azure Machine Learning kunnen bouwen.</span><span class="sxs-lookup"><span data-stu-id="71afe-240">Having explored the datasets and demonstrated how we may do this type of exploration for any variables (including combinations), we now down sample the data sets so that we can build models in Azure Machine Learning.</span></span> <span data-ttu-id="71afe-241">Let erop dat het probleem dat we richten op: een set voorbeeld kenmerken (functie waarden van Col2 - Col40) opgegeven, we voorspellen als Col1 0 (geen klik) of 1 (klik is).</span><span class="sxs-lookup"><span data-stu-id="71afe-241">Recall that the problem we focus on is: given a set of example attributes (feature values from Col2 - Col40), we predict if Col1 is a 0 (no click) or a 1 (click).</span></span>

<span data-ttu-id="71afe-242">Omlaag steekproef onze train en gegevenssets niet 1% van de oorspronkelijke grootte testen, gebruiken we Hive van systeemeigen ASELECT() functie.</span><span class="sxs-lookup"><span data-stu-id="71afe-242">To down sample our train and test datasets to 1% of the original size, we use Hive's native RAND() function.</span></span> <span data-ttu-id="71afe-243">Het volgende script [voorbeeld &#95; hive &#95; criteo &#95; verkleinen &#95; train &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) doet u dit voor de gegevensset train:</span><span class="sxs-lookup"><span data-stu-id="71afe-243">The next script, [sample&#95;hive&#95;criteo&#95;downsample&#95;train&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) does this for the train dataset:</span></span>

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

<span data-ttu-id="71afe-244">Dit levert:</span><span class="sxs-lookup"><span data-stu-id="71afe-244">This yields:</span></span>

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

<span data-ttu-id="71afe-245">Het script [voorbeeld &#95; hive &#95; criteo &#95; verkleinen &#95; test &#95; dag &#95; 22 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) gebeurt dit voor testgegevens, dag\_22:</span><span class="sxs-lookup"><span data-stu-id="71afe-245">The script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;22&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) does it for test data, day\_22:</span></span>

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

<span data-ttu-id="71afe-246">Dit levert:</span><span class="sxs-lookup"><span data-stu-id="71afe-246">This yields:</span></span>

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


<span data-ttu-id="71afe-247">Ten slotte wordt het script [voorbeeld &#95; hive &#95; criteo &#95; verkleinen &#95; test &#95; dag &#95; 23 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) gebeurt dit voor testgegevens, dag\_23:</span><span class="sxs-lookup"><span data-stu-id="71afe-247">Finally, the script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;23&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) does it for test data, day\_23:</span></span>

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

<span data-ttu-id="71afe-248">Dit levert:</span><span class="sxs-lookup"><span data-stu-id="71afe-248">This yields:</span></span>

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

<span data-ttu-id="71afe-249">Dit zijn gereed voor gebruik van onze omlaag opgevangen train en test gegevenssets voor het bouwen van modellen in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="71afe-249">With this, we are ready to use our down sampled train and test datasets for building models in Azure Machine Learning.</span></span>

<span data-ttu-id="71afe-250">Er is een definitieve belangrijk onderdeel voordat we verder gaan met Azure Machine Learning, wat betreft de count-tabel.</span><span class="sxs-lookup"><span data-stu-id="71afe-250">There is a final important component before we move on to Azure Machine Learning, which is concerns the count table.</span></span> <span data-ttu-id="71afe-251">In de volgende subsectie bespreken we dit sommige beschreven.</span><span class="sxs-lookup"><span data-stu-id="71afe-251">In the next sub-section, we discuss this in some detail.</span></span>

## <span data-ttu-id="71afe-252"><a name="count"></a>Een korte bespreking van de count-tabel</span><span class="sxs-lookup"><span data-stu-id="71afe-252"><a name="count"></a> A brief discussion on the count table</span></span>
<span data-ttu-id="71afe-253">Zoals u hebt gezien, hebben verschillende categorische variabelen een zeer hoge dimensionaliteit.</span><span class="sxs-lookup"><span data-stu-id="71afe-253">As we saw, several categorical variables have a very high dimensionality.</span></span> <span data-ttu-id="71afe-254">In ons scenario we een krachtige methode aangeroepen in dit [Learning met telt](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) voor het coderen van deze variabelen in een efficiënte en krachtige manier.</span><span class="sxs-lookup"><span data-stu-id="71afe-254">In our walkthrough, we present a powerful technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) to encode these variables in an efficient, robust manner.</span></span> <span data-ttu-id="71afe-255">Meer informatie over deze techniek is in de koppeling.</span><span class="sxs-lookup"><span data-stu-id="71afe-255">More information on this technique is in the link provided.</span></span>

[!NOTE]
><span data-ttu-id="71afe-256">We richten op het aantal tabellen gebruiken voor het produceren van compact representaties van hoge-dimensionale categorische functies in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="71afe-256">In this walkthrough, we focus on using count tables to produce compact representations of high-dimensional categorical features.</span></span> <span data-ttu-id="71afe-257">Dit is niet de enige manier voor het coderen van functies categorische; voor meer informatie over andere technieken geïnteresseerd gebruikers kunnen uitchecken [one-hot-encoding](http://en.wikipedia.org/wiki/One-hot) en [hash-functie](http://en.wikipedia.org/wiki/Feature_hashing).</span><span class="sxs-lookup"><span data-stu-id="71afe-257">This is not the only way to encode categorical features; for more information on other techniques, interested users can check out [one-hot-encoding](http://en.wikipedia.org/wiki/One-hot) and [feature hashing](http://en.wikipedia.org/wiki/Feature_hashing).</span></span>
>

<span data-ttu-id="71afe-258">Aantal tabellen op de gegevens van het aantal bouwen, gebruiken we de gegevens in de map onbewerkte/aantal.</span><span class="sxs-lookup"><span data-stu-id="71afe-258">To build count tables on the count data, we use the data in the folder raw/count.</span></span> <span data-ttu-id="71afe-259">In de sectie modellering laten we zien gebruikers deze aantal tabellen voor categorische functies helemaal, maken of u kunt ook een aantal vooraf gemaakte tabel gebruiken voor hun explorations.</span><span class="sxs-lookup"><span data-stu-id="71afe-259">In the modeling section, we show users how to build these count tables for categorical features from scratch, or alternatively to use a pre-built count table for their explorations.</span></span> <span data-ttu-id="71afe-260">In welke volgt wanneer we verwijzen naar 'vooraf samengestelde aantal tabellen', bedoelen we met behulp van het aantal tabellen die wij verstrekken.</span><span class="sxs-lookup"><span data-stu-id="71afe-260">In what follows, when we refer to "pre-built count tables", we mean using the count tables that we provide.</span></span> <span data-ttu-id="71afe-261">Gedetailleerde instructies over toegang krijgen tot deze tabellen zijn beschikbaar in de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="71afe-261">Detailed instructions on how to access these tables are provided in the next section.</span></span>

## <span data-ttu-id="71afe-262"><a name="aml"></a>Een model met Azure Machine Learning bouwen</span><span class="sxs-lookup"><span data-stu-id="71afe-262"><a name="aml"></a> Build a model with Azure Machine Learning</span></span>
<span data-ttu-id="71afe-263">Het model bouwen proces in Azure Machine Learning verloopt als volgt:</span><span class="sxs-lookup"><span data-stu-id="71afe-263">Our model building process in Azure Machine Learning follows these steps:</span></span>

1. [<span data-ttu-id="71afe-264">De gegevens ophalen uit de Hive-tabellen in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="71afe-264">Get the data from Hive tables into Azure Machine Learning</span></span>](#step1)
2. [<span data-ttu-id="71afe-265">Het experiment maken: de gegevens en featurize met aantal tabellen opschonen</span><span class="sxs-lookup"><span data-stu-id="71afe-265">Create the experiment: clean the data and featurize with count tables</span></span>](#step2)
3. [<span data-ttu-id="71afe-266">Bouwen, te trainen en het model beoordelen</span><span class="sxs-lookup"><span data-stu-id="71afe-266">Build, train, and score the model</span></span>](#step3)
4. [<span data-ttu-id="71afe-267">Het model evalueren</span><span class="sxs-lookup"><span data-stu-id="71afe-267">Evaluate the model</span></span>](#step4)
5. [<span data-ttu-id="71afe-268">Het model publiceren als een webservice</span><span class="sxs-lookup"><span data-stu-id="71afe-268">Publish the model as a web-service</span></span>](#step5)

<span data-ttu-id="71afe-269">We zijn nu gereed voor het bouwen van modellen in Azure Machine Learning studio.</span><span class="sxs-lookup"><span data-stu-id="71afe-269">Now we are ready to build models in Azure Machine Learning studio.</span></span> <span data-ttu-id="71afe-270">Onze omlaag steekproefgegevens wordt opgeslagen als Hive-tabellen in het cluster.</span><span class="sxs-lookup"><span data-stu-id="71afe-270">Our down sampled data is saved as Hive tables in the cluster.</span></span> <span data-ttu-id="71afe-271">We gebruiken de Azure Machine Learning **importgegevens** module om deze gegevens te lezen.</span><span class="sxs-lookup"><span data-stu-id="71afe-271">We use the Azure Machine Learning **Import Data** module to read this data.</span></span> <span data-ttu-id="71afe-272">De referenties voor toegang tot het opslagaccount van dit cluster zijn opgegeven in het volgende.</span><span class="sxs-lookup"><span data-stu-id="71afe-272">The credentials to access the storage account of this cluster are provided in what follows.</span></span>

### <span data-ttu-id="71afe-273"><a name="step1"></a>Stap 1: Gegevens ophalen uit de Hive-tabellen in Azure Machine Learning met de module gegevens importeren en selecteren om een machine learning-experiment</span><span class="sxs-lookup"><span data-stu-id="71afe-273"><a name="step1"></a> Step 1: Get data from Hive tables into Azure Machine Learning using the Import Data module and select it for a machine learning experiment</span></span>
<span data-ttu-id="71afe-274">Begin met het selecteren een **+ nieuw** -> **EXPERIMENT** -> **leeg Experiment**.</span><span class="sxs-lookup"><span data-stu-id="71afe-274">Start by selecting a **+NEW** -> **EXPERIMENT** -> **Blank Experiment**.</span></span> <span data-ttu-id="71afe-275">Klik vanuit de **Search** vak op de bovenste links, zoek naar 'Gegevens importeren'.</span><span class="sxs-lookup"><span data-stu-id="71afe-275">Then, from the **Search** box on the top left, search for "Import Data".</span></span> <span data-ttu-id="71afe-276">Slepen en neerzetten de **importgegevens** module doorsturen naar het experiment (middelste gedeelte van het scherm) met de module voor gegevenstoegang canvas.</span><span class="sxs-lookup"><span data-stu-id="71afe-276">Drag and drop the **Import Data** module on to the experiment canvas (the middle portion of the screen) to use the module for data access.</span></span>

<span data-ttu-id="71afe-277">Dit is wat de **importgegevens** lijkt tijdens het ophalen van gegevens uit de Hive-tabel:</span><span class="sxs-lookup"><span data-stu-id="71afe-277">This is what the **Import Data** looks like while getting data from the Hive table:</span></span>

![Gegevens importeren gegevens worden opgehaald](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

<span data-ttu-id="71afe-279">Voor de **importgegevens** module, de waarden van de parameters die beschikbaar zijn in de afbeelding zijn alleen voorbeelden van de sortering van waarden die u moet opgeven.</span><span class="sxs-lookup"><span data-stu-id="71afe-279">For the **Import Data** module, the values of the parameters that are provided in the graphic are just examples of the sort of values you need to provide.</span></span> <span data-ttu-id="71afe-280">Hier volgt een aantal algemene richtlijnen voor het invullen van de parameter is ingesteld voor de **importgegevens** module.</span><span class="sxs-lookup"><span data-stu-id="71afe-280">Here is some general guidance on how to fill out the parameter set for the **Import Data** module.</span></span>

1. <span data-ttu-id="71afe-281">'Hive-query' kiezen voor **gegevensbron**</span><span class="sxs-lookup"><span data-stu-id="71afe-281">Choose "Hive query" for **Data Source**</span></span>
2. <span data-ttu-id="71afe-282">In de **Hive databasequery** vak een eenvoudige SELECT * FROM < uw\_database\_name.your\_tabel\_name >-voldoende is.</span><span class="sxs-lookup"><span data-stu-id="71afe-282">In the **Hive database query** box, a simple SELECT * FROM <your\_database\_name.your\_table\_name> - is enough.</span></span>
3. <span data-ttu-id="71afe-283">**Hcatalog server-URI**: als uw cluster "abc", wordt dit eenvoudig is: https://abc.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="71afe-283">**Hcatalog server URI**: If your cluster is "abc", then this is simply: https://abc.azurehdinsight.net</span></span>
4. <span data-ttu-id="71afe-284">**Hadoop-gebruikersaccountnaam**: de naam van de gebruiker gekozen op het moment van het bedrijf stellen van het cluster.</span><span class="sxs-lookup"><span data-stu-id="71afe-284">**Hadoop user account name**: The user name chosen at the time of commissioning the cluster.</span></span> <span data-ttu-id="71afe-285">(Niet de RAS-gebruikersnaam!)</span><span class="sxs-lookup"><span data-stu-id="71afe-285">(NOT the Remote Access user name!)</span></span>
5. <span data-ttu-id="71afe-286">**Het wachtwoord voor gebruikersaccount Hadoop**: het wachtwoord voor de naam van de gebruiker gekozen op het moment van het bedrijf stellen van het cluster.</span><span class="sxs-lookup"><span data-stu-id="71afe-286">**Hadoop user account password**: The password for the user name chosen at the time of commissioning the cluster.</span></span> <span data-ttu-id="71afe-287">(Niet de RAS-wachtwoord!)</span><span class="sxs-lookup"><span data-stu-id="71afe-287">(NOT the Remote Access password!)</span></span>
6. <span data-ttu-id="71afe-288">**Locatie van uitvoergegevens**: 'Azure' kiezen</span><span class="sxs-lookup"><span data-stu-id="71afe-288">**Location of output data**: Choose "Azure"</span></span>
7. <span data-ttu-id="71afe-289">**Naam van het Azure-opslagaccount**: het storage-account die is gekoppeld aan het cluster</span><span class="sxs-lookup"><span data-stu-id="71afe-289">**Azure storage account name**: The storage account associated with the cluster</span></span>
8. <span data-ttu-id="71afe-290">**Azure-toegangssleutel**: de sleutel van het opslagaccount die is gekoppeld aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="71afe-290">**Azure storage account key**: The key of the storage account associated with the cluster.</span></span>
9. <span data-ttu-id="71afe-291">**Azure containernaam**: als de clusternaam is "abc", wordt dit gewoon "abc", meestal is.</span><span class="sxs-lookup"><span data-stu-id="71afe-291">**Azure container name**: If the cluster name is "abc", then this is simply "abc", usually.</span></span>

<span data-ttu-id="71afe-292">Eenmaal de **importgegevens** ophalen van gegevens (ziet u de groene maatstreepjes op de Module), zijn voltooid deze gegevens opslaan als een Dataset (met een naam van uw keuze).</span><span class="sxs-lookup"><span data-stu-id="71afe-292">Once the **Import Data** finishes getting data (you see the green tick on the Module), save this data as a Dataset (with a name of your choice).</span></span> <span data-ttu-id="71afe-293">Wat ziet deze eruit als:</span><span class="sxs-lookup"><span data-stu-id="71afe-293">What this looks like:</span></span>

![Gegevens importeren opslaan gegevens](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

<span data-ttu-id="71afe-295">Met de rechtermuisknop op de uitvoerpoort van de **importgegevens** module.</span><span class="sxs-lookup"><span data-stu-id="71afe-295">Right-click the output port of the **Import Data** module.</span></span> <span data-ttu-id="71afe-296">Dit blijkt een **opslaan als gegevensset** optie en een **Visualize** optie.</span><span class="sxs-lookup"><span data-stu-id="71afe-296">This reveals a **Save as dataset** option and a **Visualize** option.</span></span> <span data-ttu-id="71afe-297">De **Visualize** optie, als u klikt, wordt weergegeven, 100 rijen van de gegevens, inclusief een rechterpaneel die nuttig is voor sommige samenvattende statistieken.</span><span class="sxs-lookup"><span data-stu-id="71afe-297">The **Visualize** option, if clicked, displays 100 rows of the data, along with a right panel that is useful for some summary statistics.</span></span> <span data-ttu-id="71afe-298">Gegevens moeten worden opgeslagen, selecteert u de **opslaan als gegevensset** en volg de instructies.</span><span class="sxs-lookup"><span data-stu-id="71afe-298">To save data, simply select **Save as dataset** and follow instructions.</span></span>

<span data-ttu-id="71afe-299">Schakel de opgeslagen gegevensset voor gebruik in een machine learning-experiment, zoek de gegevenssets met behulp van de **Search** vak weergegeven in de volgende afbeelding.</span><span class="sxs-lookup"><span data-stu-id="71afe-299">To select the saved dataset for use in a machine learning experiment, locate the datasets using the **Search** box shown in the following figure.</span></span> <span data-ttu-id="71afe-300">Typ vervolgens gewoon de naam hebt u de gegevensset gedeeltelijk toegang hebben en sleep de gegevensset naar het hoofdpaneel gegeven.</span><span class="sxs-lookup"><span data-stu-id="71afe-300">Then simply type out the name you gave the dataset partially to access it and drag the dataset onto the main panel.</span></span> <span data-ttu-id="71afe-301">Neer te zetten naar het hoofdpaneel de wordt geselecteerd voor gebruik in machine learning-model.</span><span class="sxs-lookup"><span data-stu-id="71afe-301">Dropping it onto the main panel selects it for use in machine learning modeling.</span></span>

![Drage gegevensset naar het hoofdpaneel](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> <span data-ttu-id="71afe-303">Doe dit voor zowel de trein en de test-gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="71afe-303">Do this for both the train and the test datasets.</span></span> <span data-ttu-id="71afe-304">Bovendien moet de databasenaam en tabelnamen die u hebt opgegeven voor dit doel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="71afe-304">Also, remember to use the database name and table names that you gave for this purpose.</span></span> <span data-ttu-id="71afe-305">De waarden die worden gebruikt in de afbeelding dienen uitsluitend ter illustratie purposes.* *</span><span class="sxs-lookup"><span data-stu-id="71afe-305">The values used in the figure are solely for illustration purposes.**</span></span>
> 
> 

### <span data-ttu-id="71afe-306"><a name="step2"></a>Stap 2: Een eenvoudig experiment maken in Azure Machine Learning om te voorspellen klikken / geen klikken</span><span class="sxs-lookup"><span data-stu-id="71afe-306"><a name="step2"></a> Step 2: Create a simple experiment in Azure Machine Learning to predict clicks / no clicks</span></span>
<span data-ttu-id="71afe-307">Ons Azure ML-experiment ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="71afe-307">Our Azure ML experiment looks like this:</span></span>

![Machine Learning-experiment](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

<span data-ttu-id="71afe-309">We nu eens kijken hoe de belangrijkste onderdelen van dit experiment.</span><span class="sxs-lookup"><span data-stu-id="71afe-309">We now examine the key components of this experiment.</span></span> <span data-ttu-id="71afe-310">Als een herinnering moeten we onze opgeslagen train slepen en gegevenssets die u aan bij onze experimentcanvas eerst te testen.</span><span class="sxs-lookup"><span data-stu-id="71afe-310">As a reminder, we need to drag our saved train and test datasets on to our experiment canvas first.</span></span>

#### <a name="clean-missing-data"></a><span data-ttu-id="71afe-311">De ontbrekende gegevens opschonen</span><span class="sxs-lookup"><span data-stu-id="71afe-311">Clean Missing Data</span></span>
<span data-ttu-id="71afe-312">De **Clean Missing Data** module biedt wat de naam al aangeeft: het ontbrekende gegevens op een manier die de gebruiker opgegeven kunnen worden schoongemaakt.</span><span class="sxs-lookup"><span data-stu-id="71afe-312">The **Clean Missing Data** module does what its name suggests:  it cleans missing data in ways that can be user-specified.</span></span> <span data-ttu-id="71afe-313">In deze module zoekt, ziet u dit:</span><span class="sxs-lookup"><span data-stu-id="71afe-313">Looking into this module, we see this:</span></span>

![Ontbrekende gegevens opschonen](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

<span data-ttu-id="71afe-315">Hier hebt alle ontbrekende waarden vervangt door een 0.</span><span class="sxs-lookup"><span data-stu-id="71afe-315">Here, we chose to replace all missing values with a 0.</span></span> <span data-ttu-id="71afe-316">Er zijn ook andere opties wilt invoeren die kunnen worden gezien door te kijken in de vervolgkeuzelijsten in de module.</span><span class="sxs-lookup"><span data-stu-id="71afe-316">There are other options as well, which can be seen by looking at the dropdowns in the module.</span></span>

#### <a name="feature-engineering-on-the-data"></a><span data-ttu-id="71afe-317">Functie-engineering op de gegevens</span><span class="sxs-lookup"><span data-stu-id="71afe-317">Feature engineering on the data</span></span>
<span data-ttu-id="71afe-318">Er zijn miljoenen unieke waarden voor sommige categorische functies van grote gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="71afe-318">There can be millions of unique values for some categorical features of large datasets.</span></span> <span data-ttu-id="71afe-319">Naïve-methoden zoals een hot codering voor het voorstellen van dergelijke hoge dimensionale categorische functies is volledig unfeasible.</span><span class="sxs-lookup"><span data-stu-id="71afe-319">Using naive methods such as one-hot encoding for representing such high-dimensional categorical features is entirely unfeasible.</span></span> <span data-ttu-id="71afe-320">In dit overzicht ziet u hoe u een aantal functies met ingebouwde Azure Machine Learning-modules voor het genereren van compact representaties van deze hoge-dimensionale categorische variabelen gebruiken.</span><span class="sxs-lookup"><span data-stu-id="71afe-320">In this walkthrough, we demonstrate how to use count features using built-in Azure Machine Learning modules to generate compact representations of these high-dimensional categorical variables.</span></span> <span data-ttu-id="71afe-321">Het eindresultaat is een kleinere model, sneller training en maatstaven voor prestaties die erg vergelijkbaar zijn met andere technieken.</span><span class="sxs-lookup"><span data-stu-id="71afe-321">The end-result is a smaller model size, faster training times, and performance metrics that are quite comparable to using other techniques.</span></span>

##### <a name="building-counting-transforms"></a><span data-ttu-id="71afe-322">Gebouw transformaties tellen</span><span class="sxs-lookup"><span data-stu-id="71afe-322">Building counting transforms</span></span>
<span data-ttu-id="71afe-323">Aantal functies bouwen, gebruiken we de **bouwen tellen transformeren** module die beschikbaar is in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="71afe-323">To build count features, we use the **Build Counting Transform** module that is available in Azure Machine Learning.</span></span> <span data-ttu-id="71afe-324">De module ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="71afe-324">The module looks like this:</span></span>

<span data-ttu-id="71afe-325">![Module tellen transformeren maken](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![module bouwen tellen transformeren](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span><span class="sxs-lookup"><span data-stu-id="71afe-325">![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="71afe-326">In de **tellen kolommen** vak vullen we de kolommen die we uitvoeren telt willen op.</span><span class="sxs-lookup"><span data-stu-id="71afe-326">In the **Count columns** box, we enter those columns that we wish to perform counts on.</span></span> <span data-ttu-id="71afe-327">Dit zijn meestal (zoals vermeld) hoge dimensionale categorische kolommen.</span><span class="sxs-lookup"><span data-stu-id="71afe-327">Typically, these are (as mentioned) high-dimensional categorical columns.</span></span> <span data-ttu-id="71afe-328">Aan het begin wordt vermeld dat de dataset Criteo 26 categorische kolommen bevat: van Col15 naar Col40.</span><span class="sxs-lookup"><span data-stu-id="71afe-328">At the start, we mentioned that the Criteo dataset has 26 categorical columns: from Col15 to Col40.</span></span> <span data-ttu-id="71afe-329">Hier we tellen op alle mappen en hun indexen geven (van 15 tot 40 gescheiden door komma's, zoals wordt weergegeven).</span><span class="sxs-lookup"><span data-stu-id="71afe-329">Here, we count on all of them and give their indices (from 15 to 40 separated by commas as shown).</span></span>
> 

<span data-ttu-id="71afe-330">De module gebruiken in de modus MapReduce (geschikt voor grote gegevenssets), moeten we toegang tot een HDInsight Hadoop-cluster (gebruikt voor de functie verkenning opnieuw kan worden gebruikt voor dit doel ook) en de referenties.</span><span class="sxs-lookup"><span data-stu-id="71afe-330">To use the module in the MapReduce mode (appropriate for large datasets), we need access to an HDInsight Hadoop cluster (the one used for feature exploration can be reused for this purpose as well) and its credentials.</span></span> <span data-ttu-id="71afe-331">In de vorige afbeeldingen laten zien wat de ingevulde waarden eruit (Vervang de waarden voor de afbeelding met die relevant zijn voor uw eigen gebruiksvoorbeeld).</span><span class="sxs-lookup"><span data-stu-id="71afe-331">The  previous figures illustrate what the filled-in values look like (replace the values provided for illustration with those relevant for your own use-case).</span></span>

![Moduleparameters](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

<span data-ttu-id="71afe-333">In de bovenstaande afbeelding laten we zien hoe de locatie van de blob-invoerbron invoeren.</span><span class="sxs-lookup"><span data-stu-id="71afe-333">In the figure above, we show how to enter the input blob location.</span></span> <span data-ttu-id="71afe-334">Deze locatie heeft de gegevens die zijn gereserveerd voor het aantal tabellen maken op.</span><span class="sxs-lookup"><span data-stu-id="71afe-334">This location has the data reserved for building count tables on.</span></span>

<span data-ttu-id="71afe-335">Nadat deze module is voltooid, we kunnen de transformatie voor later opslaan met de rechtermuisknop op de module en selecteert u de **opslaan als transformatie** optie:</span><span class="sxs-lookup"><span data-stu-id="71afe-335">After this module finishes running, we can save the transform for later by right-clicking the module and selecting the **Save as Transform** option:</span></span>

![Optie 'Opslaan als transformatie'](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

<span data-ttu-id="71afe-337">In onze experiment architectuur hierboven weergegeven, correspondeert de gegevensset 'ytransform2' nauwkeurig opgeslagen aantal transformatie.</span><span class="sxs-lookup"><span data-stu-id="71afe-337">In our experiment architecture shown above, the dataset "ytransform2" corresponds precisely to a saved count transform.</span></span> <span data-ttu-id="71afe-338">Voor de rest van dit experiment, gaan we ervan uit dat de lezer gebruikt een **bouwen tellen transformeren** -module op bepaalde gegevens aantallen genereert, en gebruik vervolgens de aantallen voor het genereren van aantal kunt functies op de trein en test gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="71afe-338">For the remainder of this experiment, we assume that the reader used a **Build Counting Transform** module on some data to generate counts, and can then use those counts to generate count features on the train and test datasets.</span></span>

##### <a name="choosing-what-count-features-to-include-as-part-of-the-train-and-test-datasets"></a><span data-ttu-id="71afe-339">Kiezen welke aantal functies voor het opnemen als onderdeel van de trein en test gegevenssets</span><span class="sxs-lookup"><span data-stu-id="71afe-339">Choosing what count features to include as part of the train and test datasets</span></span>
<span data-ttu-id="71afe-340">Zodra er een aantal transformeren gereed hebt, de gebruiker kan kiezen welke functies wilt opnemen in hun train en testen met behulp van gegevenssets de **wijzigen aantal tabel Parameters** module.</span><span class="sxs-lookup"><span data-stu-id="71afe-340">Once we have a count transform ready, the user can choose what features to include in their train and test datasets using the **Modify Count Table Parameters** module.</span></span> <span data-ttu-id="71afe-341">We deze module alleen weergeven hier voor de volledigheid, maar uit oogpunt van eenvoud daadwerkelijk gebruik deze functie niet bij ons experiment.</span><span class="sxs-lookup"><span data-stu-id="71afe-341">We just show this module here for completeness, but in interests of simplicity do not actually use it in our experiment.</span></span>

![De parameters voor aantal wijzigen](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

<span data-ttu-id="71afe-343">In dit geval zoals u kunt zien, we hebben ervoor gekozen alleen de logboek-kans gebruiken en de achtergrond uit kolom negeren.</span><span class="sxs-lookup"><span data-stu-id="71afe-343">In this case, as can be seen, we have chosen to use just the log-odds and to ignore the back off column.</span></span> <span data-ttu-id="71afe-344">We kunnen ook parameters instellen, zoals de drempelwaarde van de opslaglocatie garbagecollection hoeveel pseudo eerdere voorbeelden voor het vloeiend maken en of u alle ruis Laplacian of niet toe te voegen.</span><span class="sxs-lookup"><span data-stu-id="71afe-344">We can also set parameters such as the garbage bin threshold, how many pseudo-prior examples to add for smoothing, and whether to use any Laplacian noise or not.</span></span> <span data-ttu-id="71afe-345">Al deze functies zijn geavanceerde en het is om te worden opgemerkt dat de standaardwaarden zijn een goed uitgangspunt voor gebruikers die niet bekend met dit type functie generatie bent.</span><span class="sxs-lookup"><span data-stu-id="71afe-345">All these are advanced features and it is to be noted that the default values are a good starting point for users who are new to this type of feature generation.</span></span>

##### <a name="data-transformation-before-generating-the-count-features"></a><span data-ttu-id="71afe-346">Gegevenstransformatie vóór het genereren van de count-functies</span><span class="sxs-lookup"><span data-stu-id="71afe-346">Data transformation before generating the count features</span></span>
<span data-ttu-id="71afe-347">Nu we gericht op een belangrijk punt over onze train transformeren en testgegevens vóór het genereren van daadwerkelijk aantal functies.</span><span class="sxs-lookup"><span data-stu-id="71afe-347">Now we focus on an important point about transforming our train and test data prior to actually generating count features.</span></span> <span data-ttu-id="71afe-348">Houd er rekening mee dat er twee zijn **R-Script uitvoeren** modules die worden gebruikt voordat we de count-transformatie op onze gegevens toepast.</span><span class="sxs-lookup"><span data-stu-id="71afe-348">Note that there are two **Execute R Script** modules used before we apply the count transform to our data.</span></span>

![Modules R-Script uitvoeren](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

<span data-ttu-id="71afe-350">Dit is het eerste R-script:</span><span class="sxs-lookup"><span data-stu-id="71afe-350">Here is the first R script:</span></span>

![Eerste R-script](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

<span data-ttu-id="71afe-352">In deze R-script wijzigen we onze kolommen aan namen 'Col1' naar 'Col40'.</span><span class="sxs-lookup"><span data-stu-id="71afe-352">In this R script, we rename our columns to names "Col1" to "Col40".</span></span> <span data-ttu-id="71afe-353">Dit komt doordat de count-transformatie namen van deze indeling verwacht.</span><span class="sxs-lookup"><span data-stu-id="71afe-353">This is because the count transform expects names of this format.</span></span>

<span data-ttu-id="71afe-354">In het tweede R-script we een balans vinden tussen de verdeling tussen klassen positieve en negatieve (respectievelijk klassen 1 en 0) door de negatieve klasse downsampling.</span><span class="sxs-lookup"><span data-stu-id="71afe-354">In the second R script, we balance the distribution between positive and negative classes (classes 1 and 0 respectively) by downsampling the negative class.</span></span> <span data-ttu-id="71afe-355">Het R-script laat zien hoe u dit doet:</span><span class="sxs-lookup"><span data-stu-id="71afe-355">The R script here shows how to do this:</span></span>

![Tweede R-script](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

<span data-ttu-id="71afe-357">In dit eenvoudige R-script gebruiken we ' pos\_neg\_verhouding ' het bedrag van balans tussen de positieve en negatieve klassen instellen.</span><span class="sxs-lookup"><span data-stu-id="71afe-357">In this simple R script, we use "pos\_neg\_ratio" to set the amount of balance between the positive and the negative classes.</span></span> <span data-ttu-id="71afe-358">Dit is belangrijk te doen omdat meestal verbeteren van de klasse onbalans prestatievoordelen voor classificatie problemen waar de klasse-distributie is vervormd (intrekken dat in ons geval we 3.3% positief klasse en 96,7% negatief klasse hebben).</span><span class="sxs-lookup"><span data-stu-id="71afe-358">This is important to do since improving class imbalance usually has performance benefits for classification problems where the class distribution is skewed (recall that in our case, we have 3.3% positive class and 96.7% negative class).</span></span>

##### <a name="applying-the-count-transformation-on-our-data"></a><span data-ttu-id="71afe-359">De transformatie aantal toepassen op onze gegevens</span><span class="sxs-lookup"><span data-stu-id="71afe-359">Applying the count transformation on our data</span></span>
<span data-ttu-id="71afe-360">Ten slotte kunnen we gebruiken de **transformatie toepassen** module voor het toepassen van de count-transformaties op onze train en gegevenssets te testen.</span><span class="sxs-lookup"><span data-stu-id="71afe-360">Finally, we can use the **Apply Transformation** module to apply the count transforms on our train and test datasets.</span></span> <span data-ttu-id="71afe-361">Deze module wordt de transformatie opgeslagen aantal als één invoer- en de trein of test gegevenssets als andere invoer en retourneert gegevens met een aantal functies.</span><span class="sxs-lookup"><span data-stu-id="71afe-361">This module takes the saved count transform as one input and the train or test datasets as the other input, and returns data with count features.</span></span> <span data-ttu-id="71afe-362">Hier wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="71afe-362">It is shown here:</span></span>

![Transformatie module toepassen](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-the-count-features-look-like"></a><span data-ttu-id="71afe-364">Een fragment van welke het aantal functies eruit</span><span class="sxs-lookup"><span data-stu-id="71afe-364">An excerpt of what the count features look like</span></span>
<span data-ttu-id="71afe-365">Het is om te zien hoe de functies count eruit in ons geval instructieve.</span><span class="sxs-lookup"><span data-stu-id="71afe-365">It is instructive to see what the count features look like in our case.</span></span> <span data-ttu-id="71afe-366">Hier wordt een fragment van deze weergeven:</span><span class="sxs-lookup"><span data-stu-id="71afe-366">Here we show an excerpt of this:</span></span>

![Aantal functies](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

<span data-ttu-id="71afe-368">In dit fragment zien we dat voor de kolommen die we op geteld, we het aantal ophalen en kans naast eventuele relevante backoffs logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="71afe-368">In this excerpt, we show that for the columns that we counted on, we get the counts and log odds in addition to any relevant backoffs.</span></span>

<span data-ttu-id="71afe-369">Er zijn nu gereed voor het bouwen van een Azure Machine Learning-model met behulp van deze getransformeerde gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="71afe-369">We are now ready to build an Azure Machine Learning model using these transformed datasets.</span></span> <span data-ttu-id="71afe-370">We zien hoe u kunt dit doen in de volgende sectie.</span><span class="sxs-lookup"><span data-stu-id="71afe-370">In the next section, we show how this can be done.</span></span>

### <span data-ttu-id="71afe-371"><a name="step3"></a>Stap 3: Bouwen, te trainen en het model beoordelen</span><span class="sxs-lookup"><span data-stu-id="71afe-371"><a name="step3"></a> Step 3: Build, train, and score the model</span></span>

#### <a name="choice-of-learner"></a><span data-ttu-id="71afe-372">Keuze van cursist</span><span class="sxs-lookup"><span data-stu-id="71afe-372">Choice of learner</span></span>
<span data-ttu-id="71afe-373">Eerst moet ervoor kiezen een cursist.</span><span class="sxs-lookup"><span data-stu-id="71afe-373">First, we need to choose a learner.</span></span> <span data-ttu-id="71afe-374">We gaan een beslissingsstructuur twee class boosted als onze cursist gebruiken.</span><span class="sxs-lookup"><span data-stu-id="71afe-374">We are going to use a two class boosted decision tree as our learner.</span></span> <span data-ttu-id="71afe-375">Hier volgen de standaardopties voor deze cursist:</span><span class="sxs-lookup"><span data-stu-id="71afe-375">Here are the default options for this learner:</span></span>

![Two-Class Boosted Decision Tree parameters](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

<span data-ttu-id="71afe-377">We gaan Kies de standaardwaarden voor onze experiment.</span><span class="sxs-lookup"><span data-stu-id="71afe-377">For our experiment, we are going to choose the default values.</span></span> <span data-ttu-id="71afe-378">We Houd er rekening mee dat de standaardwaarden meestal zinvolle zijn en een goede manier om snel basislijnen op de prestaties.</span><span class="sxs-lookup"><span data-stu-id="71afe-378">We note that the defaults are usually meaningful and a good way to get quick baselines on performance.</span></span> <span data-ttu-id="71afe-379">U kunt op de prestaties verbeteren door verstrekkende parameters als u zodra er een basislijn.</span><span class="sxs-lookup"><span data-stu-id="71afe-379">You can improve on performance by sweeping parameters if you choose to once you have a baseline.</span></span>

#### <a name="train-the-model"></a><span data-ttu-id="71afe-380">Het model trainen</span><span class="sxs-lookup"><span data-stu-id="71afe-380">Train the model</span></span>
<span data-ttu-id="71afe-381">Voor training, roepen we gewoon een **Train Model** module.</span><span class="sxs-lookup"><span data-stu-id="71afe-381">For training, we simply invoke a **Train Model** module.</span></span> <span data-ttu-id="71afe-382">De twee invoeren aan zijn de cursist Two-Class Boosted Decision Tree en onze train-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="71afe-382">The two inputs to it are the Two-Class Boosted Decision Tree learner and our train dataset.</span></span> <span data-ttu-id="71afe-383">Dit wordt hier weergegeven:</span><span class="sxs-lookup"><span data-stu-id="71afe-383">This is shown here:</span></span>

![Module Train-Model](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-the-model"></a><span data-ttu-id="71afe-385">Het model scoren</span><span class="sxs-lookup"><span data-stu-id="71afe-385">Score the model</span></span>
<span data-ttu-id="71afe-386">Zodra er een getraind model hebt, zijn wij gereed om te beoordelen op de testgegevensset en evalueren van de prestaties.</span><span class="sxs-lookup"><span data-stu-id="71afe-386">Once we have a trained model, we are ready to score on the test dataset and to evaluate its performance.</span></span> <span data-ttu-id="71afe-387">We dit doen via de **Score Model** module weergegeven in de volgende afbeelding, samen met een **Evaluate Model** module:</span><span class="sxs-lookup"><span data-stu-id="71afe-387">We do this by using the **Score Model** module shown in the following figure, along with an **Evaluate Model** module:</span></span>

![De module Score Model (Scoremodel)](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <span data-ttu-id="71afe-389"><a name="step4"></a>Stap 4: Het model beoordelen</span><span class="sxs-lookup"><span data-stu-id="71afe-389"><a name="step4"></a> Step 4: Evaluate the model</span></span>
<span data-ttu-id="71afe-390">Tot slot willen we model prestaties analyseren.</span><span class="sxs-lookup"><span data-stu-id="71afe-390">Finally, we would like to analyze model performance.</span></span> <span data-ttu-id="71afe-391">Meestal is een goede indicatie voor twee klasse (binair) classificatie problemen, de AUC.</span><span class="sxs-lookup"><span data-stu-id="71afe-391">Usually, for two class (binary) classification problems, a good measure is the AUC.</span></span> <span data-ttu-id="71afe-392">Als u wilt dit visualiseren, we aansluiten de **Score Model** module die u wilt een **Evaluate Model** -module voor dit.</span><span class="sxs-lookup"><span data-stu-id="71afe-392">To visualize this, we hook up the **Score Model** module to an **Evaluate Model** module for this.</span></span> <span data-ttu-id="71afe-393">Te klikken op **Visualize** op de **Evaluate Model** module resulteert in een afbeelding zoals de volgende:</span><span class="sxs-lookup"><span data-stu-id="71afe-393">Clicking **Visualize** on the **Evaluate Model** module yields a graphic like the following one:</span></span>

![Module BDT model evalueren](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

<span data-ttu-id="71afe-395">Binair (of twee klasse) classificatie problemen met een goede indicatie van nauwkeurigheid is het gebied onder Curve (AUC).</span><span class="sxs-lookup"><span data-stu-id="71afe-395">In binary (or two class) classification problems, a good measure of prediction accuracy is the Area Under Curve (AUC).</span></span> <span data-ttu-id="71afe-396">In het volgende, laten we zien onze resultaten met dit model op onze testgegevensset.</span><span class="sxs-lookup"><span data-stu-id="71afe-396">In what follows, we show our results using this model on our test dataset.</span></span> <span data-ttu-id="71afe-397">Als u dit, met de rechtermuisknop op de uitvoerpoort van de **Evaluate Model** module en vervolgens **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="71afe-397">To get this, right-click the output port of the **Evaluate Model** module and then **Visualize**.</span></span>

![Module Evaluate Model visualiseren](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <span data-ttu-id="71afe-399"><a name="step5"></a>Stap 5: Het model publiceren als een webservice</span><span class="sxs-lookup"><span data-stu-id="71afe-399"><a name="step5"></a> Step 5: Publish the model as a Web service</span></span>
<span data-ttu-id="71afe-400">De mogelijkheid voor het publiceren van een Azure Machine Learning-model als webservices met een minimum van fuss is een zeer nuttige functie voor het maken van het algemeen beschikbaar.</span><span class="sxs-lookup"><span data-stu-id="71afe-400">The ability to publish an Azure Machine Learning model as web services with a minimum of fuss is a valuable feature for making it widely available.</span></span> <span data-ttu-id="71afe-401">Zodra u dat hebt gedaan, kan iedereen bellen naar de webservice met invoer gegevens die ze voorspellingen voor nodig hebt, en het model om te retourneren die voorspellingen maakt gebruik van de webservice.</span><span class="sxs-lookup"><span data-stu-id="71afe-401">Once that is done, anyone can make calls to the web service with input data that they need predictions for, and the web service uses the model to return those predictions.</span></span>

<span data-ttu-id="71afe-402">U doet dit door opslaan we eerst het getrainde model als een object van het getrainde Model.</span><span class="sxs-lookup"><span data-stu-id="71afe-402">To do this, we first save our trained model as a Trained Model object.</span></span> <span data-ttu-id="71afe-403">Dit wordt gedaan met de rechtermuisknop op de **Train Model** module en met behulp van de **opslaan als getrainde Model** optie.</span><span class="sxs-lookup"><span data-stu-id="71afe-403">This is done by right-clicking the **Train Model** module and using the **Save as Trained Model** option.</span></span>

<span data-ttu-id="71afe-404">Vervolgens moet voor het maken van de invoer en uitvoer van poorten voor onze webservice:</span><span class="sxs-lookup"><span data-stu-id="71afe-404">Next, we need to create input and output ports for our web service:</span></span>

* <span data-ttu-id="71afe-405">een invoerpoort worden gegevens in het formulier van de gegevens die we nodig hebben voorspellingen voor</span><span class="sxs-lookup"><span data-stu-id="71afe-405">an input port takes data in the same form as the data that we need predictions for</span></span>
* <span data-ttu-id="71afe-406">een uitvoerpoort de Scored Labels en de bijbehorende waarschijnlijkheid geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="71afe-406">an output port returns the Scored Labels and the associated probabilities.</span></span>

#### <a name="select-a-few-rows-of-data-for-the-input-port"></a><span data-ttu-id="71afe-407">Selecteer een paar rijen van de gegevens voor de invoer-poort</span><span class="sxs-lookup"><span data-stu-id="71afe-407">Select a few rows of data for the input port</span></span>
<span data-ttu-id="71afe-408">Het is gemakkelijk te gebruiken een **toepassen SQL transformatie** module om net 10 rijen als de invoerpoort gegevens te selecteren.</span><span class="sxs-lookup"><span data-stu-id="71afe-408">It is convenient to use an **Apply SQL Transformation** module to select just 10 rows to serve as the input port data.</span></span> <span data-ttu-id="71afe-409">Selecteer alleen deze rijen met gegevens voor onze invoerpoort met behulp van de SQL-query die hier worden weergegeven:</span><span class="sxs-lookup"><span data-stu-id="71afe-409">Select just these rows of data for our input port using the SQL query shown here:</span></span>

![Invoerpoort gegevens](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a><span data-ttu-id="71afe-411">Webservice</span><span class="sxs-lookup"><span data-stu-id="71afe-411">Web service</span></span>
<span data-ttu-id="71afe-412">We zijn nu gereed voor gebruik van een kleine experiment die kan worden gebruikt voor het publiceren van de webservice.</span><span class="sxs-lookup"><span data-stu-id="71afe-412">Now we are ready to run a small experiment that can be used to publish our web service.</span></span>

#### <a name="generate-input-data-for-webservice"></a><span data-ttu-id="71afe-413">Genereren van de invoergegevens voor de webservice</span><span class="sxs-lookup"><span data-stu-id="71afe-413">Generate input data for webservice</span></span>
<span data-ttu-id="71afe-414">Als een stap zeroth aangezien de tabel aantal groot, we nemen van een paar regels testgegevens en uitvoergegevens genereren van het aantal functies.</span><span class="sxs-lookup"><span data-stu-id="71afe-414">As a zeroth step, since the count table is large, we take a few lines of test data and generate output data from it with count features.</span></span> <span data-ttu-id="71afe-415">Dit kan fungeren als de invoergegevens notatie voor de webservice.</span><span class="sxs-lookup"><span data-stu-id="71afe-415">This can serve as the input data format for our webservice.</span></span> <span data-ttu-id="71afe-416">Dit wordt hier weergegeven:</span><span class="sxs-lookup"><span data-stu-id="71afe-416">This is shown here:</span></span>

![De invoergegevens BDT maken](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> <span data-ttu-id="71afe-418">Voor de indeling invoergegevens gebruiken we nu de uitvoer van de **aantal Featurizer** module.</span><span class="sxs-lookup"><span data-stu-id="71afe-418">For the input data format, we now use the OUTPUT of the **Count Featurizer** module.</span></span> <span data-ttu-id="71afe-419">Zodra dit is voltooid met experimenteren, sla de uitvoer van de **aantal Featurizer** module als een Dataset.</span><span class="sxs-lookup"><span data-stu-id="71afe-419">Once this experiment finishes running, save the output from the **Count Featurizer** module as a Dataset.</span></span> <span data-ttu-id="71afe-420">Deze gegevensset wordt gebruikt voor de invoergegevens in de webservice.</span><span class="sxs-lookup"><span data-stu-id="71afe-420">This Dataset is used for the input data in the webservice.</span></span>
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a><span data-ttu-id="71afe-421">Score berekenen voor experiment voor de publicatie-webservice</span><span class="sxs-lookup"><span data-stu-id="71afe-421">Scoring experiment for publishing webservice</span></span>
<span data-ttu-id="71afe-422">Eerst laten we zien hoe dit eruitziet.</span><span class="sxs-lookup"><span data-stu-id="71afe-422">First, we show what this looks like.</span></span> <span data-ttu-id="71afe-423">De structuur van essentieel belang is een **Score Model** module die accepteert onze getrainde model-object en een paar regels met invoergegevens die wordt gegenereerd in de vorige stappen met behulp van de **aantal Featurizer** module.</span><span class="sxs-lookup"><span data-stu-id="71afe-423">The essential structure is a **Score Model** module that accepts our trained model object and a few lines of input data that we generated in the previous steps using the **Count Featurizer** module.</span></span> <span data-ttu-id="71afe-424">We gebruiken 'Kolommen in gegevensset selecteren' aan de Scored labels en de waarschijnlijkheid Score-project.</span><span class="sxs-lookup"><span data-stu-id="71afe-424">We use "Select Columns in Dataset" to project out the Scored labels and the Score probabilities.</span></span>

![Kolommen in gegevensset selecteren](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

<span data-ttu-id="71afe-426">U ziet hoe de **Select Columns in Dataset** module kan worden gebruikt voor 'uitgefilterd' gegevens uit een gegevensset.</span><span class="sxs-lookup"><span data-stu-id="71afe-426">Notice how the **Select Columns in Dataset** module can be used for 'filtering' data out from a dataset.</span></span> <span data-ttu-id="71afe-427">We weergeven de inhoud hier:</span><span class="sxs-lookup"><span data-stu-id="71afe-427">We show the contents here:</span></span>

![Filteren met de Select Columns in Dataset-module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

<span data-ttu-id="71afe-429">Als u de blauwe invoer en uitvoerpoorten, klikt u op **voorbereiden webservice** aan de onderkant rechts.</span><span class="sxs-lookup"><span data-stu-id="71afe-429">To get the blue input and output ports, you simply click **prepare webservice** at the bottom right.</span></span> <span data-ttu-id="71afe-430">Dit experiment uitgevoerd ook kan worden uitgevoerd op de webservice publiceren: klik op de **WEBSERVICE PUBLICEERT** pictogram aan de onderkant rechts, weergegeven hier:</span><span class="sxs-lookup"><span data-stu-id="71afe-430">Running this experiment also allows us to publish the web service: click the **PUBLISH WEB SERVICE** icon at the bottom right, shown here:</span></span>

![Webservice publiceren](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

<span data-ttu-id="71afe-432">Als de webservice is gepubliceerd, krijgen we omgeleid naar een pagina die er zo uitziet:</span><span class="sxs-lookup"><span data-stu-id="71afe-432">Once the webservice is published, we get redirected to a page that looks thus:</span></span>

![Web service-dashboard](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

<span data-ttu-id="71afe-434">Twee koppelingen voor webservices zien we aan de linkerkant:</span><span class="sxs-lookup"><span data-stu-id="71afe-434">We see two links for webservices on the left side:</span></span>

* <span data-ttu-id="71afe-435">De **aanvragen/reacties** Service (of RR's) zijn alleen bedoeld voor één voorspellingen en is er met deze workshop gebruiken.</span><span class="sxs-lookup"><span data-stu-id="71afe-435">The **REQUEST/RESPONSE** Service (or RRS) is meant for single predictions and is what we utilize in this workshop.</span></span>
* <span data-ttu-id="71afe-436">De **BATCHUITVOERING** Service (BES) wordt gebruikt voor voorspellingen batch en vereist dat de invoergegevens gebruikt voor het maken van voorspellingen zich bevinden in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="71afe-436">The **BATCH EXECUTION** Service (BES) is used for batch predictions and requires that the input data used to make predictions reside in Azure Blob Storage.</span></span>

<span data-ttu-id="71afe-437">Op de koppeling te klikken **aanvragen/reacties** vergt ons naar een pagina die we de code in C#, python en R. vooraf blik Deze code kan gemakkelijk worden gebruikt voor het aanroepen van de webservice.</span><span class="sxs-lookup"><span data-stu-id="71afe-437">Clicking on the link **REQUEST/RESPONSE** takes us to a page that gives us pre-canned code in C#, python, and R. This code can be conveniently used for making calls to the webservice.</span></span> <span data-ttu-id="71afe-438">Houd er rekening mee dat de API-sleutel op deze pagina moet worden gebruikt voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="71afe-438">Note that the API key on this page needs to be used for authentication.</span></span>

<span data-ttu-id="71afe-439">Is het handig deze python-code naar een nieuwe cel in de notebook IPython overschreven.</span><span class="sxs-lookup"><span data-stu-id="71afe-439">It is convenient to copy this python code over to a new cell in the IPython notebook.</span></span>

<span data-ttu-id="71afe-440">We weergeven hier een segment van python-code met de juiste API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="71afe-440">Here we show a segment of python code with the correct API key.</span></span>

![Python-code](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

<span data-ttu-id="71afe-442">Houd er rekening mee dat we de standaard-API-sleutel hebt vervangen door onze webservices-API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="71afe-442">Note that we replaced the default API key with our webservices's API key.</span></span> <span data-ttu-id="71afe-443">Te klikken op **uitvoeren** op deze cel in een IPython notebook resulteert in het volgende antwoord:</span><span class="sxs-lookup"><span data-stu-id="71afe-443">Clicking **Run** on this cell in an IPython notebook yields the following response:</span></span>

![IPython antwoord](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

<span data-ttu-id="71afe-445">We zien dat voor de twee test voorbeelden die we gevraagd over (in het kader van de JSON van het pythonscript), we weer antwoorden in de vorm krijgen 'Scored Labels, Scored kansen'.</span><span class="sxs-lookup"><span data-stu-id="71afe-445">We see that for the two test examples we asked about (in the JSON framework of the python script), we get back answers in the form "Scored Labels, Scored Probabilities".</span></span> <span data-ttu-id="71afe-446">Houd er rekening mee dat in dit geval we hebt gekozen de standaardwaarden vooraf voorgedefinieerde biedt (0 voor alle numerieke kolommen en de tekenreeks '' waarde '' voor alle categorische kolommen).</span><span class="sxs-lookup"><span data-stu-id="71afe-446">Note that in this case, we chose the default values that the pre-canned code provides (0's for all numeric columns and the string "value" for all categorical columns).</span></span>

<span data-ttu-id="71afe-447">Hiermee is onze end-to-end procedure voor het afhandelen van grootschalige gegevensset met Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="71afe-447">This concludes our end-to-end walkthrough showing how to handle large-scale dataset using Azure Machine Learning.</span></span> <span data-ttu-id="71afe-448">We de slag met een terabyte van gegevens, een Voorspellend model samengesteld en wordt geïmplementeerd als een webservice in de cloud.</span><span class="sxs-lookup"><span data-stu-id="71afe-448">We started with a terabyte of data, constructed a prediction model and deployed it as a web service in the cloud.</span></span>

