---
title: Hallo Team gegevens wetenschappelijke processen in actie - met een Azure HDInsight Hadoop-Cluster van een gegevensset 1 TB | Microsoft Docs
description: Hallo Team gegevens wetenschappelijke processen voor een end-to-end-scenario die gebruikmaakt van een HDInsight Hadoop toobuild cluster en implementeren van een model met behulp van een grote (1 TB) openbaar gegevensset
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
ms.openlocfilehash: 59b2af02e7840cb60a4b5b2f2c8ab0611df198ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action---using-an-azure-hdinsight-hadoop-cluster-on-a-1-tb-dataset"></a><span data-ttu-id="4371c-103">Hallo Team gegevens wetenschappelijke processen in actie - met een Azure HDInsight Hadoop-Cluster van een gegevensset 1 TB</span><span class="sxs-lookup"><span data-stu-id="4371c-103">hello Team Data Science Process in action - Using an Azure HDInsight Hadoop Cluster on a 1 TB dataset</span></span>

<span data-ttu-id="4371c-104">In dit overzicht wordt gedemonstreerd met behulp van Hallo Team gegevens wetenschappelijke processen in een end-to-end-scenario met een [Azure HDInsight Hadoop-cluster](https://azure.microsoft.com/services/hdinsight/) toostore, verkennen, functie engineering en voorbeeldgegevens uit een Hallo openbaar omlaag beschikbare [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="4371c-104">In this walkthrough, we demonstrate using hello Team Data Science Process in an end-to-end scenario with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore, feature engineer, and down sample data from one of hello publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) datasets.</span></span> <span data-ttu-id="4371c-105">Azure Machine Learning toobuild een model binaire classificatie gebruiken we gegevens.</span><span class="sxs-lookup"><span data-stu-id="4371c-105">We use Azure Machine Learning toobuild a binary classification model on this data.</span></span> <span data-ttu-id="4371c-106">Ook laten we zien hoe toopublish een van deze modellen als een webservice.</span><span class="sxs-lookup"><span data-stu-id="4371c-106">We also show how toopublish one of these models as a Web service.</span></span>

<span data-ttu-id="4371c-107">Het is ook mogelijk toouse een IPython notebook tooaccomplish Hallo taken die zijn gepresenteerd in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="4371c-107">It is also possible toouse an IPython notebook tooaccomplish hello tasks presented in this walkthrough.</span></span> <span data-ttu-id="4371c-108">Gebruikers die zou zoals tootry contact met deze aanpak opnemen moet Hallo [Criteo scenario met behulp van een verbinding Hive ODBC](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="4371c-108">Users who would like tootry this approach should consult hello [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="4371c-109"><a name="dataset"></a>Beschrijving van de gegevensset Criteo</span><span class="sxs-lookup"><span data-stu-id="4371c-109"><a name="dataset"></a>Criteo Dataset Description</span></span>
<span data-ttu-id="4371c-110">Hallo Criteo gegevens is een klik voorspelling gegevensset die ongeveer 370GB gecomprimeerde gzip TSV-bestanden (~1.3TB ongecomprimeerde), die bestaat uit meer dan 4.3 miljard records.</span><span class="sxs-lookup"><span data-stu-id="4371c-110">hello Criteo data is a click prediction dataset that is approximately 370GB of gzip compressed TSV files (~1.3TB uncompressed), comprising more than 4.3 billion records.</span></span> <span data-ttu-id="4371c-111">Het is afkomstig uit 24 dagen van klik dan op gegevens die de [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span><span class="sxs-lookup"><span data-stu-id="4371c-111">It is taken from 24 days of click data made available by [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/).</span></span> <span data-ttu-id="4371c-112">Voor het gemak van gegevenswetenschappers Hallo hebben we gegevens beschikbaar toous tooexperiment met uitgepakt.</span><span class="sxs-lookup"><span data-stu-id="4371c-112">For hello convenience of data scientists, we have unzipped data available toous tooexperiment with.</span></span>

<span data-ttu-id="4371c-113">Elke record in deze gegevensset bevat 40 kolommen:</span><span class="sxs-lookup"><span data-stu-id="4371c-113">Each record in this dataset contains 40 columns:</span></span>

* <span data-ttu-id="4371c-114">de eerste kolom Hallo is een labelkolom waarin wordt aangegeven of een gebruiker klikt op een **toevoegen** (waarde 1) of niet op een (waarde 0)</span><span class="sxs-lookup"><span data-stu-id="4371c-114">hello first column is a label column that indicates whether a user clicks an **add** (value 1) or does not click one (value 0)</span></span>
* <span data-ttu-id="4371c-115">naast 13 kolommen zijn numerieke, en</span><span class="sxs-lookup"><span data-stu-id="4371c-115">next 13 columns are numeric, and</span></span>
* <span data-ttu-id="4371c-116">laatste 26 zijn categorische kolommen</span><span class="sxs-lookup"><span data-stu-id="4371c-116">last 26 are categorical columns</span></span>

<span data-ttu-id="4371c-117">Hallo-kolommen zijn geanonimiseerde en gebruiken van een reeks geïnventariseerde namen: "Col1' (voor kolom Hallo-label) te ' Col40 ' (voor Hallo laatste categorische kolom).</span><span class="sxs-lookup"><span data-stu-id="4371c-117">hello columns are anonymized and use a series of enumerated names: "Col1" (for hello label column) too'Col40" (for hello last categorical column).</span></span>            

<span data-ttu-id="4371c-118">Hier volgt een fragment van Hallo eerst 20 kolommen uit twee rapporten (rijen) van deze gegevensset:</span><span class="sxs-lookup"><span data-stu-id="4371c-118">Here is an excerpt of hello first 20 columns of two observations (rows) from this dataset:</span></span>

    Col1    Col2    Col3    Col4    Col5    Col6    Col7    Col8    Col9    Col10    Col11    Col12    Col13    Col14    Col15            Col16            Col17            Col18            Col19        Col20

    0       40      42      2       54      3       0       0       2       16      0       1       4448    4       1acfe1ee        1b2ff61f        2e8b2631        6faef306        c6fc10d3    6fcd6dcb           
    0               24              27      5               0       2       1               3       10064           9a8cb066        7a06385f        417e6103        2170fc56        acf676aa    6fcd6dcb                      

<span data-ttu-id="4371c-119">Er zijn ontbreken waarden in beide Hallo numerieke en categorische kolommen in deze dataset.</span><span class="sxs-lookup"><span data-stu-id="4371c-119">There are missing values in both hello numeric and categorical columns in this dataset.</span></span> <span data-ttu-id="4371c-120">Een eenvoudige methode voor het verwerken van de ontbrekende waarden Hallo worden beschreven.</span><span class="sxs-lookup"><span data-stu-id="4371c-120">We describe a simple method for handling hello missing values.</span></span> <span data-ttu-id="4371c-121">Aanvullende details van Hallo gegevens worden verkend wanneer we ze opslaan in de Hive-tabellen.</span><span class="sxs-lookup"><span data-stu-id="4371c-121">Additional details of hello data are explored when we store them into Hive tables.</span></span>

<span data-ttu-id="4371c-122">**Definitie:** *Clickthrough-snelheid (CTR):* dit percentage Hallo muisklikken in Hallo gegevens is.</span><span class="sxs-lookup"><span data-stu-id="4371c-122">**Definition:** *Clickthrough rate (CTR):* This is hello percentage of clicks in hello data.</span></span> <span data-ttu-id="4371c-123">In deze dataset Criteo is Hallo CTR ongeveer 3.3% of 0.033.</span><span class="sxs-lookup"><span data-stu-id="4371c-123">In this Criteo dataset, hello CTR is about 3.3% or 0.033.</span></span>

## <span data-ttu-id="4371c-124"><a name="mltasks"></a>Voorbeelden van voorspelling taken</span><span class="sxs-lookup"><span data-stu-id="4371c-124"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="4371c-125">Twee voorbeeld voorspelling problemen worden in dit scenario behandeld:</span><span class="sxs-lookup"><span data-stu-id="4371c-125">Two sample prediction problems are addressed in this walkthrough:</span></span>

1. <span data-ttu-id="4371c-126">**Binaire classificatie**: voorspelt of een gebruiker een add geklikt:</span><span class="sxs-lookup"><span data-stu-id="4371c-126">**Binary classification**: Predicts whether a user clicked an add:</span></span>
   
   * <span data-ttu-id="4371c-127">Klasse 0: Er is geen Klik</span><span class="sxs-lookup"><span data-stu-id="4371c-127">Class 0: No Click</span></span>
   * <span data-ttu-id="4371c-128">Klasse 1: klik op</span><span class="sxs-lookup"><span data-stu-id="4371c-128">Class 1: Click</span></span>
2. <span data-ttu-id="4371c-129">**Regressie**: voorspelt Hallo waarschijnlijkheid van een ad-klik van functies voor gebruikers.</span><span class="sxs-lookup"><span data-stu-id="4371c-129">**Regression**: Predicts hello probability of an ad click from user features.</span></span>

## <span data-ttu-id="4371c-130"><a name="setup"></a>Instellen van een HDInsight Hadoop-cluster voor gegevenswetenschap</span><span class="sxs-lookup"><span data-stu-id="4371c-130"><a name="setup"></a>Set Up an HDInsight Hadoop cluster for data science</span></span>
<span data-ttu-id="4371c-131">**Opmerking:** dit is doorgaans een **Admin** taak.</span><span class="sxs-lookup"><span data-stu-id="4371c-131">**Note:** This is typically an **Admin** task.</span></span>

<span data-ttu-id="4371c-132">Instellen van uw Azure-Gegevenswetenschap-omgeving voor het bouwen van predictive analytics-oplossingen met HDInsight-clusters in drie stappen:</span><span class="sxs-lookup"><span data-stu-id="4371c-132">Set up your Azure Data Science environment for building predictive analytics solutions with HDInsight clusters in three steps:</span></span>

1. <span data-ttu-id="4371c-133">[Een opslagaccount maken](../storage/common/storage-create-storage-account.md): dit opslagaccount wordt gebruikt toostore gegevens in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="4371c-133">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used toostore data in Azure Blob Storage.</span></span> <span data-ttu-id="4371c-134">Hallo-gegevens in HDInsight-clusters gebruikt, wordt hier opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4371c-134">hello data used in HDInsight clusters is stored here.</span></span>
2. <span data-ttu-id="4371c-135">[Azure HDInsight Hadoop-Clusters aanpassen voor Gegevenswetenschap](machine-learning-data-science-customize-hadoop-cluster.md): deze stap maakt u een Azure HDInsight Hadoop-cluster met 64-bits Anaconda Python 2.7 is geïnstalleerd op alle knooppunten.</span><span class="sxs-lookup"><span data-stu-id="4371c-135">[Customize Azure HDInsight Hadoop Clusters for Data Science](machine-learning-data-science-customize-hadoop-cluster.md): This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="4371c-136">Er zijn twee belangrijke stappen die u (in dit onderwerp beschreven) toocomplete bij het aanpassen van Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="4371c-136">There are two important steps (described in this topic) toocomplete when customizing hello HDInsight cluster.</span></span>
   
   * <span data-ttu-id="4371c-137">Hallo storage-account is gemaakt in stap 1 met uw HDInsight-cluster wanneer deze wordt gemaakt, moet u koppelen.</span><span class="sxs-lookup"><span data-stu-id="4371c-137">You must link hello storage account created in step 1 with your HDInsight cluster when it is created.</span></span> <span data-ttu-id="4371c-138">Dit opslagaccount wordt gebruikt voor toegang tot gegevens die kunnen worden verwerkt binnen Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="4371c-138">This storage account is used for accessing data that can be processed within hello cluster.</span></span>
   * <span data-ttu-id="4371c-139">Nadat deze is gemaakt, moet u externe toegang toohello hoofdknooppunt van Hallo cluster inschakelen.</span><span class="sxs-lookup"><span data-stu-id="4371c-139">You must enable Remote Access toohello head node of hello cluster after it is created.</span></span> <span data-ttu-id="4371c-140">Hallo RAS-referenties die u hier opgeeft (anders dan die zijn opgegeven voor de cluster Hallo bij het maken ervan) onthouden: u moet ze toocomplete Hallo volgende procedures.</span><span class="sxs-lookup"><span data-stu-id="4371c-140">Remember hello remote access credentials you specify here (different from those specified for hello cluster at its creation): you need them toocomplete hello following procedures.</span></span>
3. <span data-ttu-id="4371c-141">[Maken van een Azure ML-werkruimte](machine-learning-create-workspace.md): deze Azure Machine Learning-werkruimte wordt gebruikt voor het bouwen van machine learning-modellen na een initiële gegevensverkenning en omlaag steekproeven op Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="4371c-141">[Create an Azure ML workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used for building machine learning models after an initial data exploration and down sampling on hello HDInsight cluster.</span></span>

## <span data-ttu-id="4371c-142"><a name="getdata"></a>Ophalen van gegevens en gebruiken van een openbare bron</span><span class="sxs-lookup"><span data-stu-id="4371c-142"><a name="getdata"></a>Get and consume data from a public source</span></span>
<span data-ttu-id="4371c-143">Hallo [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) dataset kan worden geopend door te klikken op de koppeling hello, Hallo gebruiksvoorwaarden accepteren en een naam geven.</span><span class="sxs-lookup"><span data-stu-id="4371c-143">hello [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) dataset can be accessed by clicking on hello link, accepting hello terms of use, and providing a name.</span></span> <span data-ttu-id="4371c-144">Hier ziet u een momentopname van wat ziet deze als eruit:</span><span class="sxs-lookup"><span data-stu-id="4371c-144">A snapshot of what this looks like is shown here:</span></span>

![Criteo voorwaarden accepteren](./media/machine-learning-data-science-process-hive-criteo-walkthrough/hLxfI2E.png)

<span data-ttu-id="4371c-146">Klik op **doorgaan tooDownload** tooread meer over Hallo gegevensset en de beschikbaarheid.</span><span class="sxs-lookup"><span data-stu-id="4371c-146">Click **Continue tooDownload** tooread more about hello dataset and its availability.</span></span>

<span data-ttu-id="4371c-147">Hallo gegevens bevinden zich in een openbare [Azure blob-opslag](../storage/blobs/storage-dotnet-how-to-use-blobs.md) locatie: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span><span class="sxs-lookup"><span data-stu-id="4371c-147">hello data resides in a public [Azure blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) location: wasb://criteo@azuremlsampleexperiments.blob.core.windows.net/raw/.</span></span> <span data-ttu-id="4371c-148">Hallo 'wasb' verwijst tooAzure Blob Storage-locatie.</span><span class="sxs-lookup"><span data-stu-id="4371c-148">hello "wasb" refers tooAzure Blob Storage location.</span></span> 

1. <span data-ttu-id="4371c-149">Hallo-gegevens in deze openbare blob-opslag bestaat uit drie submappen van uitgepakte gegevens.</span><span class="sxs-lookup"><span data-stu-id="4371c-149">hello data in this public blob storage consists of three subfolders of unzipped data.</span></span>
   
   1. <span data-ttu-id="4371c-150">Hallo submap *Onbewerkte/telling/* bevat Hallo eerste 21 dagen aan gegevens - vanaf dag\_00 tooday\_20</span><span class="sxs-lookup"><span data-stu-id="4371c-150">hello subfolder *raw/count/* contains hello first 21 days of data - from day\_00 tooday\_20</span></span>
   2. <span data-ttu-id="4371c-151">Hallo submap *onbewerkte/train/* bestaat uit één dag van gegevens, dag\_21</span><span class="sxs-lookup"><span data-stu-id="4371c-151">hello subfolder *raw/train/* consists of a single day of data, day\_21</span></span>
   3. <span data-ttu-id="4371c-152">Hallo submap *onbewerkte en testen/* bestaat uit twee dagen aan gegevens, dag\_22 en dag\_23</span><span class="sxs-lookup"><span data-stu-id="4371c-152">hello subfolder *raw/test/* consists of two days of data, day\_22 and day\_23</span></span>
2. <span data-ttu-id="4371c-153">Voor die willen toostart met Hallo gzip onbewerkte gegevens, zijn ook beschikbaar in de hoofdmap Hallo *onbewerkte /* als day_NN.gz, waarbij NN van 00 too23 gaat.</span><span class="sxs-lookup"><span data-stu-id="4371c-153">For those who want toostart with hello raw gzip data, these are also available in hello main folder *raw/* as day_NN.gz, where NN goes from 00 too23.</span></span>

<span data-ttu-id="4371c-154">Een alternatieve methode-tooaccess verkennen en model van deze gegevens waarvoor lokale downloads verderop in dit scenario wordt uitgelegd wanneer we Hive-tabellen maakt geen nodig.</span><span class="sxs-lookup"><span data-stu-id="4371c-154">An alternative approach tooaccess, explore, and model this data that does not require any local downloads is explained later in this walkthrough when we create Hive tables.</span></span>

## <span data-ttu-id="4371c-155"><a name="login"></a>Meld u bij toohello cluster headnode</span><span class="sxs-lookup"><span data-stu-id="4371c-155"><a name="login"></a>Log in toohello cluster headnode</span></span>
<span data-ttu-id="4371c-156">toolog in toohello headnode van Hallo-cluster, gebruik Hallo [Azure-portal](https://ms.portal.azure.com) toolocate Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="4371c-156">toolog in toohello headnode of hello cluster, use hello [Azure portal](https://ms.portal.azure.com) toolocate hello cluster.</span></span> <span data-ttu-id="4371c-157">Klik op Hallo HDInsight plaats pictogram op Hallo links en dubbelklik vervolgens op Hallo-naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="4371c-157">Click hello HDInsight elephant icon on hello left and then double-click hello name of your cluster.</span></span> <span data-ttu-id="4371c-158">Navigeer toohello **configuratie** tabblad, dubbelklik op Hallo CONNECT op Hallo onder aan Hallo pagina en geef uw referenties voor externe toegang als u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="4371c-158">Navigate toohello **Configuration** tab, double-click hello CONNECT icon on hello bottom of hello page, and enter your remote access credentials when prompted.</span></span> <span data-ttu-id="4371c-159">Hiermee gaat u toohello headnode van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="4371c-159">This takes you toohello headnode of hello cluster.</span></span>

<span data-ttu-id="4371c-160">Hier volgt een typisch eerst aanmelden toohello cluster headnode ziet er als:</span><span class="sxs-lookup"><span data-stu-id="4371c-160">Here is what a typical first log in toohello cluster headnode looks like:</span></span>

![Meld u bij toocluster](./media/machine-learning-data-science-process-hive-criteo-walkthrough/Yys9Vvm.png)

<span data-ttu-id="4371c-162">Aan de linkerkant hello ziet u Hallo ' Hadoop opdrachtregel ', die onze werkpaard voor Hallo gegevensverkenning is.</span><span class="sxs-lookup"><span data-stu-id="4371c-162">On hello left, we see hello "Hadoop Command Line", which is our workhorse for hello data exploration.</span></span> <span data-ttu-id="4371c-163">Ook ziet u twee nuttig URL's - 'Hadoop Yarn Status' en 'Hadoop de naam van knooppunt'.</span><span class="sxs-lookup"><span data-stu-id="4371c-163">We also see two useful URLs - "Hadoop Yarn Status" and "Hadoop Name Node".</span></span> <span data-ttu-id="4371c-164">Hallo yarn status URL ziet u de voortgang van de taak en Hallo naam knooppunt URL geeft informatie over het Hallo-clusterconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="4371c-164">hello yarn status URL shows job progress and hello name node URL gives details on hello cluster configuration.</span></span>

<span data-ttu-id="4371c-165">Nu we worden ingesteld en klaar toobegin eerste deel van Hallo rondleiding: gegevensverkenning gebruik van Hive en voorbereiden van gegevens voor Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4371c-165">Now we are set up and ready toobegin first part of hello walkthrough: data exploration using Hive and getting data ready for Azure Machine Learning.</span></span>

## <span data-ttu-id="4371c-166"><a name="hive-db-tables"></a>Hive-database en tabellen maken</span><span class="sxs-lookup"><span data-stu-id="4371c-166"><a name="hive-db-tables"></a> Create Hive database and tables</span></span>
<span data-ttu-id="4371c-167">toocreate Hive-tabellen voor onze gegevensset Criteo open Hallo ***Hadoop-opdrachtregel*** op bureaublad van hoofdknooppunt Hallo Hallo en Voer Hallo Hive directory door te voeren opdracht Hallo</span><span class="sxs-lookup"><span data-stu-id="4371c-167">toocreate Hive tables for our Criteo dataset, open hello ***Hadoop Command Line*** on hello desktop of hello head node, and enter hello Hive directory by entering hello command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="4371c-168">Alle Hive-opdrachten uitvoeren in dit overzicht van Hallo Hive bin / directory prompt.</span><span class="sxs-lookup"><span data-stu-id="4371c-168">Run all Hive commands in this walkthrough from hello Hive bin/ directory prompt.</span></span> <span data-ttu-id="4371c-169">Dit zorgt voor problemen die pad automatisch.</span><span class="sxs-lookup"><span data-stu-id="4371c-169">This takes care of any path issues automatically.</span></span> <span data-ttu-id="4371c-170">We gebruiken Hallo termen 'Hive directory prompt', ' Hive bin / directory prompt ', en ' Hadoop opdrachtregel ' door elkaar.</span><span class="sxs-lookup"><span data-stu-id="4371c-170">We use hello terms "Hive directory prompt", "Hive bin/ directory prompt", and "Hadoop Command Line" interchangeably.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="4371c-171">tooexecute Hive-query op een altijd gebruiken Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="4371c-171">tooexecute any Hive query, one can always use hello following commands:</span></span>
> 
> 

        cd %hive_home%\bin
        hive

<span data-ttu-id="4371c-172">Na het Hallo Hive REPL wordt weergegeven met een ' hive > "aanmelden, gewoon knippen en plakken Hallo query tooexecute deze.</span><span class="sxs-lookup"><span data-stu-id="4371c-172">After hello Hive REPL appears with a "hive >"sign, simply cut and paste hello query tooexecute it.</span></span>

<span data-ttu-id="4371c-173">Hallo volgende code maakt een database 'criteo' en genereert vervolgens 4 tabellen:</span><span class="sxs-lookup"><span data-stu-id="4371c-173">hello following code creates a database "criteo" and then generates 4 tables:</span></span>

* <span data-ttu-id="4371c-174">een *tabel voor het genereren van aantallen* gebouwd op dagen dag\_00 tooday\_20,</span><span class="sxs-lookup"><span data-stu-id="4371c-174">a *table for generating counts* built on days day\_00 tooday\_20,</span></span>
* <span data-ttu-id="4371c-175">een *tabel voor gebruik als de trein gegevensset Hallo* gebouwd op dag\_21, en</span><span class="sxs-lookup"><span data-stu-id="4371c-175">a *table for use as hello train dataset* built on day\_21, and</span></span>
* <span data-ttu-id="4371c-176">twee *tabellen voor gebruik als Hallo testen gegevenssets* gebouwd op dag\_22 en dag\_23 respectievelijk.</span><span class="sxs-lookup"><span data-stu-id="4371c-176">two *tables for use as hello test datasets* built on day\_22 and day\_23 respectively.</span></span>

<span data-ttu-id="4371c-177">We onze testgegevensset opgesplitst in twee verschillende tabellen omdat een van de Hallo dagen een feestdag is, en kunt u toodetermine als Hallo model verschillen tussen een feestdag en niet met Hallo clickthrough snelheid kan detecteren.</span><span class="sxs-lookup"><span data-stu-id="4371c-177">We split our test dataset into two different tables because one of hello days is a holiday, and we want toodetermine if hello model can detect differences between a holiday and non-holiday from hello clickthrough rate.</span></span>

<span data-ttu-id="4371c-178">Hallo script [voorbeeld &#95; hive &#95; maken &#95; criteo &#95; database &#95; en &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) voor het gemak Hier wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="4371c-178">hello script [sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql) is displayed here for convenience:</span></span>

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

<span data-ttu-id="4371c-179">Er rekening mee dat alle tabellen in deze externe als we gewoon punt tooAzure Blob Storage (wasb)-locaties.</span><span class="sxs-lookup"><span data-stu-id="4371c-179">We note that all these tables are external as we simply point tooAzure Blob Storage (wasb) locations.</span></span>

<span data-ttu-id="4371c-180">**Er zijn twee manieren tooexecute ANY Hive-query die we nu vermeld.**</span><span class="sxs-lookup"><span data-stu-id="4371c-180">**There are two ways tooexecute ANY Hive query that we now mention.**</span></span>

1. <span data-ttu-id="4371c-181">**Met behulp van Hive REPL opdrachtregelprogramma Hallo**: Hallo eerst tooissue is een opdracht 'hive' en kopieer en plak een query op Hallo Hive REPL vanaf de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="4371c-181">**Using hello Hive REPL command-line**: hello first is tooissue a "hive" command and copy and paste a query at hello Hive REPL command-line.</span></span> <span data-ttu-id="4371c-182">toodo deze, komen:</span><span class="sxs-lookup"><span data-stu-id="4371c-182">toodo this, do:</span></span>
   
        cd %hive_home%\bin
        hive
   
     <span data-ttu-id="4371c-183">Nu op Hallo REPL opdrachtregelprogramma, knippen en plakken wordt deze Hallo query uitvoert.</span><span class="sxs-lookup"><span data-stu-id="4371c-183">Now at hello REPL command-line, cutting and pasting hello query executes it.</span></span>
2. <span data-ttu-id="4371c-184">**Opslaan query tooa bestands- en uitvoeren van de opdracht Hallo**: Hallo tweede is toosave Hallo query's tooa .hql-bestand ([voorbeeld &#95; hive &#95; maken &#95; criteo &#95; database &#95; en &#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) en vervolgens Hallo Geef de volgende opdracht tooexecute Hallo query:</span><span class="sxs-lookup"><span data-stu-id="4371c-184">**Saving queries tooa file and executing hello command**: hello second is toosave hello queries tooa .hql file ([sample&#95;hive&#95;create&#95;criteo&#95;database&#95;and&#95;tables.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_create_criteo_database_and_tables.hql)) and then issue hello following command tooexecute hello query:</span></span>
   
        hive -f C:\temp\sample_hive_create_criteo_database_and_tables.hql

### <a name="confirm-database-and-table-creation"></a><span data-ttu-id="4371c-185">Het maken van database en tabel bevestigen</span><span class="sxs-lookup"><span data-stu-id="4371c-185">Confirm database and table creation</span></span>
<span data-ttu-id="4371c-186">Vervolgens we Hallo database maken van Hallo bevestigen met de volgende opdracht uit Hallo Hive bin Hallo / opdrachtprompt van de map:</span><span class="sxs-lookup"><span data-stu-id="4371c-186">Next, we confirm hello creation of hello database with hello following command from hello Hive bin/ directory prompt:</span></span>

        hive -e "show databases;"

<span data-ttu-id="4371c-187">Hierdoor hebt:</span><span class="sxs-lookup"><span data-stu-id="4371c-187">This gives:</span></span>

        criteo
        default
        Time taken: 1.25 seconds, Fetched: 2 row(s)

<span data-ttu-id="4371c-188">Hiermee bevestigt u Hallo maken van een nieuwe database hello, 'criteo'.</span><span class="sxs-lookup"><span data-stu-id="4371c-188">This confirms hello creation of hello new database, "criteo".</span></span>

<span data-ttu-id="4371c-189">toosee welke tabellen wordt gemaakt, we gewoon Hallo opdracht geven hier vanuit Hallo Hive bin / opdrachtprompt van de map:</span><span class="sxs-lookup"><span data-stu-id="4371c-189">toosee what tables we created, we simply issue hello command here from hello Hive bin/ directory prompt:</span></span>

        hive -e "show tables in criteo;"

<span data-ttu-id="4371c-190">Vervolgens ziet u Hallo volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="4371c-190">We then see hello following output:</span></span>

        criteo_count
        criteo_test_day_22
        criteo_test_day_23
        criteo_train
        Time taken: 1.437 seconds, Fetched: 4 row(s)

## <span data-ttu-id="4371c-191"><a name="exploration"></a>Gegevensverkenning in component</span><span class="sxs-lookup"><span data-stu-id="4371c-191"><a name="exploration"></a> Data exploration in Hive</span></span>
<span data-ttu-id="4371c-192">We klaar toodo sommige basic gegevensverkenning in Hive.</span><span class="sxs-lookup"><span data-stu-id="4371c-192">Now we are ready toodo some basic data exploration in Hive.</span></span> <span data-ttu-id="4371c-193">We beginnen door het aantal voorbeelden in de trein Hallo Hallo te tellen en gegevenstabellen testen.</span><span class="sxs-lookup"><span data-stu-id="4371c-193">We begin by counting hello number of examples in hello train and test data tables.</span></span>

### <a name="number-of-train-examples"></a><span data-ttu-id="4371c-194">Aantal train-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="4371c-194">Number of train examples</span></span>
<span data-ttu-id="4371c-195">inhoud van Hallo [voorbeeld &#95; hive &#95; & #95 tellen; train &#95; tabel &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) worden hier weergegeven:</span><span class="sxs-lookup"><span data-stu-id="4371c-195">hello contents of [sample&#95;hive&#95;count&#95;train&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_train_table_examples.hql) are shown here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_train;

<span data-ttu-id="4371c-196">Dit levert:</span><span class="sxs-lookup"><span data-stu-id="4371c-196">This yields:</span></span>

        192215183
        Time taken: 264.154 seconds, Fetched: 1 row(s)

<span data-ttu-id="4371c-197">U kunt ook een ook afgeven Hallo volgende opdracht uit Hallo Hive bin / opdrachtprompt van de map:</span><span class="sxs-lookup"><span data-stu-id="4371c-197">Alternatively, one may also issue hello following command from hello Hive bin/ directory prompt:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_train_table_examples.hql

### <a name="number-of-test-examples-in-hello-two-test-datasets"></a><span data-ttu-id="4371c-198">Aantal voorbeelden van de test in Hallo twee test gegevenssets</span><span class="sxs-lookup"><span data-stu-id="4371c-198">Number of test examples in hello two test datasets</span></span>
<span data-ttu-id="4371c-199">We nu tellen Hallo aantal voorbeelden in Hallo twee test gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="4371c-199">We now count hello number of examples in hello two test datasets.</span></span> <span data-ttu-id="4371c-200">inhoud van Hallo [voorbeeld &#95; hive &#95; & #95 tellen; criteo &#95; test &#95; dag &#95; 22 &#95; tabel &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) hier zijn:</span><span class="sxs-lookup"><span data-stu-id="4371c-200">hello contents of [sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;22&#95;table&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_22_table_examples.hql) are here:</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_22;

<span data-ttu-id="4371c-201">Dit levert:</span><span class="sxs-lookup"><span data-stu-id="4371c-201">This yields:</span></span>

        189747893
        Time taken: 267.968 seconds, Fetched: 1 row(s)

<span data-ttu-id="4371c-202">Gebruikelijke we ook Hallo script kunnen aanroepen vanuit Hallo Hive bin / Active directory vragen door Hallo-opdracht:</span><span class="sxs-lookup"><span data-stu-id="4371c-202">As usual, we may also call hello script from hello Hive bin/ directory prompt by issuing hello command:</span></span>

        hive -f C:\temp\sample_hive_count_criteo_test_day_22_table_examples.hql

<span data-ttu-id="4371c-203">Ten slotte we naar de Hallo aantal test voorbeelden in Hallo testgegevensset op basis van dag\_23.</span><span class="sxs-lookup"><span data-stu-id="4371c-203">Finally, we examine hello number of test examples in hello test dataset based on day\_23.</span></span>

<span data-ttu-id="4371c-204">Hallo opdracht toodo dit is vergelijkbaar toohello een slechts weergegeven (Raadpleeg te[voorbeeld &#95; hive &#95; & #95 tellen; criteo &#95; test &#95; dag &#95; 23 &#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span><span class="sxs-lookup"><span data-stu-id="4371c-204">hello command toodo this is similar toohello one just shown (refer too[sample&#95;hive&#95;count&#95;criteo&#95;test&#95;day&#95;23&#95;examples.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_count_criteo_test_day_23_examples.hql)):</span></span>

        SELECT COUNT(*) FROM criteo.criteo_test_day_23;

<span data-ttu-id="4371c-205">Hierdoor hebt:</span><span class="sxs-lookup"><span data-stu-id="4371c-205">This gives:</span></span>

        178274637
        Time taken: 253.089 seconds, Fetched: 1 row(s)

### <a name="label-distribution-in-hello-train-dataset"></a><span data-ttu-id="4371c-206">Label verdeling in Hallo train gegevensset</span><span class="sxs-lookup"><span data-stu-id="4371c-206">Label distribution in hello train dataset</span></span>
<span data-ttu-id="4371c-207">Hallo label verdeling in Hallo train gegevensset is van belang.</span><span class="sxs-lookup"><span data-stu-id="4371c-207">hello label distribution in hello train dataset is of interest.</span></span> <span data-ttu-id="4371c-208">toosee, laten we zien inhoud van [voorbeeld &#95; hive &#95; criteo &#95; & #95 label; verdeling &#95; train &#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span><span class="sxs-lookup"><span data-stu-id="4371c-208">toosee this, we show contents of [sample&#95;hive&#95;criteo&#95;label&#95;distribution&#95;train&#95;table.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_label_distribution_train_table.hql):</span></span>

        SELECT Col1, COUNT(*) AS CT FROM criteo.criteo_train GROUP BY Col1;

<span data-ttu-id="4371c-209">Dit levert Hallo label distributie:</span><span class="sxs-lookup"><span data-stu-id="4371c-209">This yields hello label distribution:</span></span>

        1       6292903
        0       185922280
        Time taken: 459.435 seconds, Fetched: 2 row(s)

<span data-ttu-id="4371c-210">Houd er rekening mee dat Hallo percentage positieve labels ongeveer 3.3% (consistent met de oorspronkelijke gegevensset Hallo is).</span><span class="sxs-lookup"><span data-stu-id="4371c-210">Note that hello percentage of positive labels is about 3.3% (consistent with hello original dataset).</span></span>

### <a name="histogram-distributions-of-some-numeric-variables-in-hello-train-dataset"></a><span data-ttu-id="4371c-211">Histogram distributies van sommige numerieke variabelen in Hallo trainen gegevensset</span><span class="sxs-lookup"><span data-stu-id="4371c-211">Histogram distributions of some numeric variables in hello train dataset</span></span>
<span data-ttu-id="4371c-212">Kunnen we de Hive-systeemeigen gebruiken ' histogram\_numerieke ' toofind uit welke Hallo-distributie van de numerieke variabelen Hallo eruit werken.</span><span class="sxs-lookup"><span data-stu-id="4371c-212">We can use Hive's native "histogram\_numeric" function toofind out what hello distribution of hello numeric variables looks like.</span></span> <span data-ttu-id="4371c-213">Hier vindt u de inhoud Hallo van [voorbeeld &#95; hive &#95; criteo &#95; histogram &#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span><span class="sxs-lookup"><span data-stu-id="4371c-213">Here are hello contents of [sample&#95;hive&#95;criteo&#95;histogram&#95;numeric.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_histogram_numeric.hql):</span></span>

        SELECT CAST(hist.x as int) as bin_center, CAST(hist.y as bigint) as bin_height FROM
            (SELECT
            histogram_numeric(col2, 20) as col2_hist
            FROM
            criteo.criteo_train
            ) a
            LATERAL VIEW explode(col2_hist) exploded_table as hist;

<span data-ttu-id="4371c-214">Dit levert Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="4371c-214">This yields hello following:</span></span>

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

<span data-ttu-id="4371c-215">Hallo LATERAL BEELD - vouwen combinatie in Hive fungeert tooproduce de uitvoer van een SQL-achtige in plaats van gebruikelijke Hallo-lijst.</span><span class="sxs-lookup"><span data-stu-id="4371c-215">hello LATERAL VIEW - explode combination in Hive serves tooproduce a SQL-like output instead of hello usual list.</span></span> <span data-ttu-id="4371c-216">Opmerking dat in Hallo deze tabel, de eerste kolom Hallo komt overeen toohello bin center en Hallo tweede toohello bin frequentie.</span><span class="sxs-lookup"><span data-stu-id="4371c-216">Note that in hello this table, hello first column corresponds toohello bin center and hello second toohello bin frequency.</span></span>

### <a name="approximate-percentiles-of-some-numeric-variables-in-hello-train-dataset"></a><span data-ttu-id="4371c-217">Geschatte percentielen van sommige numerieke variabelen in Hallo trainen gegevensset</span><span class="sxs-lookup"><span data-stu-id="4371c-217">Approximate percentiles of some numeric variables in hello train dataset</span></span>
<span data-ttu-id="4371c-218">Ook is het van belang met numerieke variabelen Hallo berekening van de geschatte percentielen.</span><span class="sxs-lookup"><span data-stu-id="4371c-218">Also of interest with numeric variables is hello computation of approximate percentiles.</span></span> <span data-ttu-id="4371c-219">Hive de systeemeigen ' percentiel\_ongeveer ' Dit wordt uitgevoerd voor ons.</span><span class="sxs-lookup"><span data-stu-id="4371c-219">Hive's native "percentile\_approx" does this for us.</span></span> <span data-ttu-id="4371c-220">inhoud van Hallo [voorbeeld &#95; hive &#95; criteo &#95; geschatte &#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) zijn:</span><span class="sxs-lookup"><span data-stu-id="4371c-220">hello contents of [sample&#95;hive&#95;criteo&#95;approximate&#95;percentiles.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_approximate_percentiles.hql) are:</span></span>

        SELECT MIN(Col2) AS Col2_min, PERCENTILE_APPROX(Col2, 0.1) AS Col2_01, PERCENTILE_APPROX(Col2, 0.3) AS Col2_03, PERCENTILE_APPROX(Col2, 0.5) AS Col2_median, PERCENTILE_APPROX(Col2, 0.8) AS Col2_08, MAX(Col2) AS Col2_max FROM criteo.criteo_train;

<span data-ttu-id="4371c-221">Dit levert:</span><span class="sxs-lookup"><span data-stu-id="4371c-221">This yields:</span></span>

        1.0     2.1418600917169246      2.1418600917169246    6.21887086390288 27.53454893115633       65535.0
        Time taken: 564.953 seconds, Fetched: 1 row(s)

<span data-ttu-id="4371c-222">We dat Hallo distributie van percentielen nauw verwante toohello histogram distributie van een numerieke variabele meestal wordt te schakelen.</span><span class="sxs-lookup"><span data-stu-id="4371c-222">We remark that hello distribution of percentiles is closely related toohello histogram distribution of any numeric variable usually.</span></span>         

### <a name="find-number-of-unique-values-for-some-categorical-columns-in-hello-train-dataset"></a><span data-ttu-id="4371c-223">Aantal unieke waarden vinden voor sommige categorische kolommen in Hallo train gegevensset</span><span class="sxs-lookup"><span data-stu-id="4371c-223">Find number of unique values for some categorical columns in hello train dataset</span></span>
<span data-ttu-id="4371c-224">Nog steeds Hallo gegevensverkenning, we nu vinden voor sommige categorische kolommen, Hallo aantal unieke waarden die ze nemen.</span><span class="sxs-lookup"><span data-stu-id="4371c-224">Continuing hello data exploration, we now find, for some categorical columns, hello number of unique values they take.</span></span> <span data-ttu-id="4371c-225">toodo, laten we zien inhoud van [voorbeeld &#95; hive &#95; criteo &#95; unieke &#95; waarden &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span><span class="sxs-lookup"><span data-stu-id="4371c-225">toodo this, we show contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_categoricals.hql):</span></span>

        SELECT COUNT(DISTINCT(Col15)) AS num_uniques FROM criteo.criteo_train;

<span data-ttu-id="4371c-226">Dit levert:</span><span class="sxs-lookup"><span data-stu-id="4371c-226">This yields:</span></span>

        19011825
        Time taken: 448.116 seconds, Fetched: 1 row(s)

<span data-ttu-id="4371c-227">We Houd er rekening mee dat Col15 19M unieke waarden bevat.</span><span class="sxs-lookup"><span data-stu-id="4371c-227">We note that Col15 has 19M unique values!</span></span> <span data-ttu-id="4371c-228">Met behulp van naïve technieken zoals 'één hot codering' tooencode dergelijke hoge dimensionale categorische variabelen onbruikbare is.</span><span class="sxs-lookup"><span data-stu-id="4371c-228">Using naive techniques like "one-hot encoding" tooencode such high-dimensional categorical variables is infeasible.</span></span> <span data-ttu-id="4371c-229">In het bijzonder we uitleggen en demonstreren van een krachtige, robuuste techniek aangeroepen [Learning met telt](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) voor efficiënt aanpakken van dit probleem.</span><span class="sxs-lookup"><span data-stu-id="4371c-229">In particular, we explain and demonstrate a powerful, robust technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) for tackling this problem efficiently.</span></span>

<span data-ttu-id="4371c-230">We eindigen deze subsectie door te kijken Hallo aantal unieke waarden voor sommige andere categorische kolommen ook.</span><span class="sxs-lookup"><span data-stu-id="4371c-230">We end this sub-section by looking at hello number of unique values for some other categorical columns as well.</span></span> <span data-ttu-id="4371c-231">inhoud van Hallo [voorbeeld &#95; hive &#95; criteo &#95; unieke &#95; waarden &#95; meerdere &#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) zijn:</span><span class="sxs-lookup"><span data-stu-id="4371c-231">hello contents of [sample&#95;hive&#95;criteo&#95;unique&#95;values&#95;multiple&#95;categoricals.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_unique_values_multiple_categoricals.hql) are:</span></span>

        SELECT COUNT(DISTINCT(Col16)), COUNT(DISTINCT(Col17)),
        COUNT(DISTINCT(Col18), COUNT(DISTINCT(Col19), COUNT(DISTINCT(Col20))
        FROM criteo.criteo_train;

<span data-ttu-id="4371c-232">Dit levert:</span><span class="sxs-lookup"><span data-stu-id="4371c-232">This yields:</span></span>

        30935   15200   7349    20067   3
        Time taken: 1933.883 seconds, Fetched: 1 row(s)

<span data-ttu-id="4371c-233">Opnieuw zien we dat, met uitzondering van Col20, alle Hallo andere kolommen hebben veel unieke waarden.</span><span class="sxs-lookup"><span data-stu-id="4371c-233">Again we see that except for Col20, all hello other columns have many unique values.</span></span>

### <a name="co-occurrence-counts-of-pairs-of-categorical-variables-in-hello-train-dataset"></a><span data-ttu-id="4371c-234">Aantal paren van categorische variabelen in Hallo mede exemplaar trainen gegevensset</span><span class="sxs-lookup"><span data-stu-id="4371c-234">Co-occurrence counts of pairs of categorical variables in hello train dataset</span></span>

<span data-ttu-id="4371c-235">Hallo mede exemplaar tellingen van paren van categorische variabelen is ook van belang.</span><span class="sxs-lookup"><span data-stu-id="4371c-235">hello co-occurrence counts of pairs of categorical variables is also of interest.</span></span> <span data-ttu-id="4371c-236">Dit kan worden bepaald met behulp van Hallo-code in [voorbeeld &#95; hive &#95; criteo &#95; gekoppeld &#95; categorische &#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span><span class="sxs-lookup"><span data-stu-id="4371c-236">This can be determined using hello code in [sample&#95;hive&#95;criteo&#95;paired&#95;categorical&#95;counts.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_paired_categorical_counts.hql):</span></span>

        SELECT Col15, Col16, COUNT(*) AS paired_count FROM criteo.criteo_train GROUP BY Col15, Col16 ORDER BY paired_count DESC LIMIT 15;

<span data-ttu-id="4371c-237">We omgekeerde volgorde Hallo aantallen door hun exemplaar en bekijkt hello boven 15 in dit geval.</span><span class="sxs-lookup"><span data-stu-id="4371c-237">We reverse order hello counts by their occurrence and look at hello top 15 in this case.</span></span> <span data-ttu-id="4371c-238">Hierdoor hebt ons:</span><span class="sxs-lookup"><span data-stu-id="4371c-238">This gives us:</span></span>

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

## <span data-ttu-id="4371c-239"><a name="downsample"></a>Omlaag Hallo voorbeeldgegevenssets voor Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4371c-239"><a name="downsample"></a> Down sample hello datasets for Azure Machine Learning</span></span>
<span data-ttu-id="4371c-240">Met explored Hallo gegevenssets en gedemonstreerd hoe we dit soort exploratie geen variabelen (waaronder combinaties), wordt nu naar beneden voorbeeld Hallo gegevenssets kan zodat we modellen in Azure Machine Learning kunnen bouwen.</span><span class="sxs-lookup"><span data-stu-id="4371c-240">Having explored hello datasets and demonstrated how we may do this type of exploration for any variables (including combinations), we now down sample hello data sets so that we can build models in Azure Machine Learning.</span></span> <span data-ttu-id="4371c-241">Dat we richten op Hallo-probleem intrekken: gezien een set voorbeeld kenmerken (functie waarden van Col2 - Col40), we voorspellen als Col1 0 (geen klik) of 1 (klik is).</span><span class="sxs-lookup"><span data-stu-id="4371c-241">Recall that hello problem we focus on is: given a set of example attributes (feature values from Col2 - Col40), we predict if Col1 is a 0 (no click) or a 1 (click).</span></span>

<span data-ttu-id="4371c-242">toodown steekproef onze train en gegevenssets too1% van de oorspronkelijke grootte Hallo testen, gebruiken we de Hive-functie voor systeemeigen RAND().</span><span class="sxs-lookup"><span data-stu-id="4371c-242">toodown sample our train and test datasets too1% of hello original size, we use Hive's native RAND() function.</span></span> <span data-ttu-id="4371c-243">Hallo volgende script [voorbeeld &#95; hive &#95; criteo &#95; verkleinen &#95; train &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) doet u dit voor Hallo train gegevensset:</span><span class="sxs-lookup"><span data-stu-id="4371c-243">hello next script, [sample&#95;hive&#95;criteo&#95;downsample&#95;train&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_train_dataset.hql) does this for hello train dataset:</span></span>

        CREATE TABLE criteo.criteo_train_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        ---Now downsample and store in this table

        INSERT OVERWRITE TABLE criteo.criteo_train_downsample_1perc SELECT * FROM criteo.criteo_train WHERE RAND() <= 0.01;

<span data-ttu-id="4371c-244">Dit levert:</span><span class="sxs-lookup"><span data-stu-id="4371c-244">This yields:</span></span>

        Time taken: 12.22 seconds
        Time taken: 298.98 seconds

<span data-ttu-id="4371c-245">Hallo script [voorbeeld &#95; hive &#95; criteo &#95; verkleinen &#95; test &#95; dag &#95; 22 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) gebeurt dit voor testgegevens, dag\_22:</span><span class="sxs-lookup"><span data-stu-id="4371c-245">hello script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;22&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_22_dataset.hql) does it for test data, day\_22:</span></span>

        --- Now for test data (day_22)

        CREATE TABLE criteo.criteo_test_day_22_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_22_downsample_1perc SELECT * FROM criteo.criteo_test_day_22 WHERE RAND() <= 0.01;

<span data-ttu-id="4371c-246">Dit levert:</span><span class="sxs-lookup"><span data-stu-id="4371c-246">This yields:</span></span>

        Time taken: 1.22 seconds
        Time taken: 317.66 seconds


<span data-ttu-id="4371c-247">Ten slotte Hallo script [voorbeeld &#95; hive &#95; criteo &#95; verkleinen &#95; test &#95; dag &#95; 23 &#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) gebeurt dit voor testgegevens, dag\_23:</span><span class="sxs-lookup"><span data-stu-id="4371c-247">Finally, hello script [sample&#95;hive&#95;criteo&#95;downsample&#95;test&#95;day&#95;23&#95;dataset.hql](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/DataScienceScripts/sample_hive_criteo_downsample_test_day_23_dataset.hql) does it for test data, day\_23:</span></span>

        --- Finally test data day_23
        CREATE TABLE criteo.criteo_test_day_23_downsample_1perc (
        col1 string,col2 double,col3 double,col4 double,col5 double,col6 double,col7 double,col8 double,col9 double,col10 double,col11 double,col12 double,col13 double,col14 double,col15 string,col16 string,col17 string,col18 string,col19 string,col20 string,col21 string,col22 string,col23 string,col24 string,col25 string,col26 string,col27 string,col28 string,col29 string,col30 string,col31 string,col32 string,col33 string,col34 string,col35 string,col36 string,col37 string,col38 string,col39 string,col40 srical feature; tring)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
        LINES TERMINATED BY '\n'
        STORED AS TEXTFILE;

        INSERT OVERWRITE TABLE criteo.criteo_test_day_23_downsample_1perc SELECT * FROM criteo.criteo_test_day_23 WHERE RAND() <= 0.01;

<span data-ttu-id="4371c-248">Dit levert:</span><span class="sxs-lookup"><span data-stu-id="4371c-248">This yields:</span></span>

        Time taken: 1.86 seconds
        Time taken: 300.02 seconds

<span data-ttu-id="4371c-249">Dit zijn de gereed toouse onze omlaag door actieve trainen en te testen gegevenssets voor het bouwen van modellen in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4371c-249">With this, we are ready toouse our down sampled train and test datasets for building models in Azure Machine Learning.</span></span>

<span data-ttu-id="4371c-250">Er is een definitieve belangrijk onderdeel voordat we op tooAzure Machine Learning, namelijk problemen Hallo aantal tabel verplaatsen.</span><span class="sxs-lookup"><span data-stu-id="4371c-250">There is a final important component before we move on tooAzure Machine Learning, which is concerns hello count table.</span></span> <span data-ttu-id="4371c-251">In Hallo volgende subsectie bespreken we dit sommige beschreven.</span><span class="sxs-lookup"><span data-stu-id="4371c-251">In hello next sub-section, we discuss this in some detail.</span></span>

## <span data-ttu-id="4371c-252"><a name="count"></a>Een korte bespreking van de Hallo aantal tabel</span><span class="sxs-lookup"><span data-stu-id="4371c-252"><a name="count"></a> A brief discussion on hello count table</span></span>
<span data-ttu-id="4371c-253">Zoals u hebt gezien, hebben verschillende categorische variabelen een zeer hoge dimensionaliteit.</span><span class="sxs-lookup"><span data-stu-id="4371c-253">As we saw, several categorical variables have a very high dimensionality.</span></span> <span data-ttu-id="4371c-254">In ons scenario we een krachtige methode aangeroepen in dit [Learning met telt](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode deze variabelen in een efficiënte en krachtige manier.</span><span class="sxs-lookup"><span data-stu-id="4371c-254">In our walkthrough, we present a powerful technique called [Learning With Counts](http://blogs.technet.com/b/machinelearning/archive/2015/02/17/big-learning-made-easy-with-counts.aspx) tooencode these variables in an efficient, robust manner.</span></span> <span data-ttu-id="4371c-255">Meer informatie over deze techniek wordt Hallo koppeling.</span><span class="sxs-lookup"><span data-stu-id="4371c-255">More information on this technique is in hello link provided.</span></span>

[!NOTE]
><span data-ttu-id="4371c-256">In dit overzicht richten we op met het aantal tabellen tooproduce compact representaties van hoge-dimensionale categorische functies.</span><span class="sxs-lookup"><span data-stu-id="4371c-256">In this walkthrough, we focus on using count tables tooproduce compact representations of high-dimensional categorical features.</span></span> <span data-ttu-id="4371c-257">Dit is geen Hallo alleen manier tooencode categorische functies; voor meer informatie over andere technieken geïnteresseerd gebruikers kunnen uitchecken [one-hot-encoding](http://en.wikipedia.org/wiki/One-hot) en [hash-functie](http://en.wikipedia.org/wiki/Feature_hashing).</span><span class="sxs-lookup"><span data-stu-id="4371c-257">This is not hello only way tooencode categorical features; for more information on other techniques, interested users can check out [one-hot-encoding](http://en.wikipedia.org/wiki/One-hot) and [feature hashing](http://en.wikipedia.org/wiki/Feature_hashing).</span></span>
>

<span data-ttu-id="4371c-258">toobuild aantal tabellen op Hallo aantal gegevens, gebruiken we Hallo gegevens in Hallo map onbewerkte/aantal.</span><span class="sxs-lookup"><span data-stu-id="4371c-258">toobuild count tables on hello count data, we use hello data in hello folder raw/count.</span></span> <span data-ttu-id="4371c-259">In Hallo modelleren sectie we gebruikers zien tabellen hoe toobuild die deze tellen voor categorische functies maakt, of u kunt ook toouse een tabel vooraf samengestelde telling voor hun explorations.</span><span class="sxs-lookup"><span data-stu-id="4371c-259">In hello modeling section, we show users how toobuild these count tables for categorical features from scratch, or alternatively toouse a pre-built count table for their explorations.</span></span> <span data-ttu-id="4371c-260">In wat volgt, wanneer we verwijst te 'vooraf gemaakte aantal tabellen', bedoelen we Hallo aantal tabellen die wij verstrekken.</span><span class="sxs-lookup"><span data-stu-id="4371c-260">In what follows, when we refer too"pre-built count tables", we mean using hello count tables that we provide.</span></span> <span data-ttu-id="4371c-261">Gedetailleerde instructies over hoe tooaccess deze tabellen u in de volgende sectie Hallo vindt.</span><span class="sxs-lookup"><span data-stu-id="4371c-261">Detailed instructions on how tooaccess these tables are provided in hello next section.</span></span>

## <span data-ttu-id="4371c-262"><a name="aml"></a>Een model met Azure Machine Learning bouwen</span><span class="sxs-lookup"><span data-stu-id="4371c-262"><a name="aml"></a> Build a model with Azure Machine Learning</span></span>
<span data-ttu-id="4371c-263">Het model bouwen proces in Azure Machine Learning verloopt als volgt:</span><span class="sxs-lookup"><span data-stu-id="4371c-263">Our model building process in Azure Machine Learning follows these steps:</span></span>

1. [<span data-ttu-id="4371c-264">Hallo-gegevens ophalen uit de Hive-tabellen in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4371c-264">Get hello data from Hive tables into Azure Machine Learning</span></span>](#step1)
2. [<span data-ttu-id="4371c-265">Hallo-experiment maken: schone Hallo gegevens en featurize met aantal tabellen</span><span class="sxs-lookup"><span data-stu-id="4371c-265">Create hello experiment: clean hello data and featurize with count tables</span></span>](#step2)
3. [<span data-ttu-id="4371c-266">Build en train Hallo score-model</span><span class="sxs-lookup"><span data-stu-id="4371c-266">Build, train, and score hello model</span></span>](#step3)
4. [<span data-ttu-id="4371c-267">Hallo model evalueren</span><span class="sxs-lookup"><span data-stu-id="4371c-267">Evaluate hello model</span></span>](#step4)
5. [<span data-ttu-id="4371c-268">Hallo model publiceren als een webservice</span><span class="sxs-lookup"><span data-stu-id="4371c-268">Publish hello model as a web-service</span></span>](#step5)

<span data-ttu-id="4371c-269">We zijn nu gereed toobuild modellen in Azure Machine Learning studio.</span><span class="sxs-lookup"><span data-stu-id="4371c-269">Now we are ready toobuild models in Azure Machine Learning studio.</span></span> <span data-ttu-id="4371c-270">Onze omlaag steekproefgegevens wordt opgeslagen als Hive-tabellen in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="4371c-270">Our down sampled data is saved as Hive tables in hello cluster.</span></span> <span data-ttu-id="4371c-271">We gebruiken hello Azure Machine Learning **importgegevens** module tooread deze gegevens.</span><span class="sxs-lookup"><span data-stu-id="4371c-271">We use hello Azure Machine Learning **Import Data** module tooread this data.</span></span> <span data-ttu-id="4371c-272">Hallo referenties tooaccess Hallo storage-account van dit cluster zijn opgegeven in welke volgt.</span><span class="sxs-lookup"><span data-stu-id="4371c-272">hello credentials tooaccess hello storage account of this cluster are provided in what follows.</span></span>

### <span data-ttu-id="4371c-273"><a name="step1"></a>Stap 1: Gegevens ophalen uit de Hive-tabellen in Azure Machine Learning met Hallo gegevens importeren-module en selecteert u deze voor een machine learning-experiment</span><span class="sxs-lookup"><span data-stu-id="4371c-273"><a name="step1"></a> Step 1: Get data from Hive tables into Azure Machine Learning using hello Import Data module and select it for a machine learning experiment</span></span>
<span data-ttu-id="4371c-274">Begin met het selecteren een **+ nieuw** -> **EXPERIMENT** -> **leeg Experiment**.</span><span class="sxs-lookup"><span data-stu-id="4371c-274">Start by selecting a **+NEW** -> **EXPERIMENT** -> **Blank Experiment**.</span></span> <span data-ttu-id="4371c-275">Vervolgens Hallo **Search** vak bovenaan Hallo links, zoek naar 'Gegevens importeren'.</span><span class="sxs-lookup"><span data-stu-id="4371c-275">Then, from hello **Search** box on hello top left, search for "Import Data".</span></span> <span data-ttu-id="4371c-276">Slepen en neerzetten Hallo **importgegevens** -module op de toohello experiment canvas (Hallo middelste gedeelte welkomstscherm) toouse Hallo-module voor gegevenstoegang.</span><span class="sxs-lookup"><span data-stu-id="4371c-276">Drag and drop hello **Import Data** module on toohello experiment canvas (hello middle portion of hello screen) toouse hello module for data access.</span></span>

<span data-ttu-id="4371c-277">Dit is wat Hallo **importgegevens** lijkt tijdens het ophalen van gegevens uit Hallo Hive-tabel:</span><span class="sxs-lookup"><span data-stu-id="4371c-277">This is what hello **Import Data** looks like while getting data from hello Hive table:</span></span>

![Gegevens importeren gegevens worden opgehaald](./media/machine-learning-data-science-process-hive-criteo-walkthrough/i3zRaoj.png)

<span data-ttu-id="4371c-279">Voor Hallo **importgegevens** module Hallo waarden van Hallo-parameters die zijn opgegeven in Hallo afbeelding zijn alleen voorbeelden van Hallo sortering van waarden u moet tooprovide.</span><span class="sxs-lookup"><span data-stu-id="4371c-279">For hello **Import Data** module, hello values of hello parameters that are provided in hello graphic are just examples of hello sort of values you need tooprovide.</span></span> <span data-ttu-id="4371c-280">Hier volgt een aantal algemene richtlijnen op hoe toofill Hallo uitvoerparameter ingesteld voor Hallo **importgegevens** module.</span><span class="sxs-lookup"><span data-stu-id="4371c-280">Here is some general guidance on how toofill out hello parameter set for hello **Import Data** module.</span></span>

1. <span data-ttu-id="4371c-281">'Hive-query' kiezen voor **gegevensbron**</span><span class="sxs-lookup"><span data-stu-id="4371c-281">Choose "Hive query" for **Data Source**</span></span>
2. <span data-ttu-id="4371c-282">In Hallo **Hive databasequery** vak een eenvoudige SELECT * FROM < uw\_database\_name.your\_tabel\_name >-voldoende is.</span><span class="sxs-lookup"><span data-stu-id="4371c-282">In hello **Hive database query** box, a simple SELECT * FROM <your\_database\_name.your\_table\_name> - is enough.</span></span>
3. <span data-ttu-id="4371c-283">**Hcatalog server-URI**: als uw cluster "abc", wordt dit eenvoudig is: https://abc.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="4371c-283">**Hcatalog server URI**: If your cluster is "abc", then this is simply: https://abc.azurehdinsight.net</span></span>
4. <span data-ttu-id="4371c-284">**Hadoop-gebruikersaccountnaam**: Hallo-gebruikersnaam die is gekozen op het Hallo-tijd van het bedrijf stellen Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="4371c-284">**Hadoop user account name**: hello user name chosen at hello time of commissioning hello cluster.</span></span> <span data-ttu-id="4371c-285">(Geen Hallo RAS gebruikersnaam!)</span><span class="sxs-lookup"><span data-stu-id="4371c-285">(NOT hello Remote Access user name!)</span></span>
5. <span data-ttu-id="4371c-286">**Het wachtwoord voor gebruikersaccount Hadoop**: Hallo wachtwoord voor Hallo-gebruikersnaam die is gekozen op het Hallo-tijd van het bedrijf stellen Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="4371c-286">**Hadoop user account password**: hello password for hello user name chosen at hello time of commissioning hello cluster.</span></span> <span data-ttu-id="4371c-287">(Geen Hallo RAS wachtwoord!)</span><span class="sxs-lookup"><span data-stu-id="4371c-287">(NOT hello Remote Access password!)</span></span>
6. <span data-ttu-id="4371c-288">**Locatie van uitvoergegevens**: 'Azure' kiezen</span><span class="sxs-lookup"><span data-stu-id="4371c-288">**Location of output data**: Choose "Azure"</span></span>
7. <span data-ttu-id="4371c-289">**Naam van het Azure-opslagaccount**: opslagaccount die is gekoppeld aan cluster Hallo Hallo</span><span class="sxs-lookup"><span data-stu-id="4371c-289">**Azure storage account name**: hello storage account associated with hello cluster</span></span>
8. <span data-ttu-id="4371c-290">**Azure-toegangssleutel**: Hallo-sleutel van Hallo storage-account is gekoppeld aan het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="4371c-290">**Azure storage account key**: hello key of hello storage account associated with hello cluster.</span></span>
9. <span data-ttu-id="4371c-291">**Azure containernaam**: als de clusternaam Hallo "abc", wordt dit is meestal gewoon "abc",.</span><span class="sxs-lookup"><span data-stu-id="4371c-291">**Azure container name**: If hello cluster name is "abc", then this is simply "abc", usually.</span></span>

<span data-ttu-id="4371c-292">Eenmaal Hallo **importgegevens** ophalen van gegevens (ziet u Hallo groen maatstreepjes op Hallo Module), zijn voltooid deze gegevens opslaan als een Dataset (met een naam van uw keuze).</span><span class="sxs-lookup"><span data-stu-id="4371c-292">Once hello **Import Data** finishes getting data (you see hello green tick on hello Module), save this data as a Dataset (with a name of your choice).</span></span> <span data-ttu-id="4371c-293">Wat ziet deze eruit als:</span><span class="sxs-lookup"><span data-stu-id="4371c-293">What this looks like:</span></span>

![Gegevens importeren opslaan gegevens](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oxM73Np.png)

<span data-ttu-id="4371c-295">Klik met de rechtermuisknop Hallo uitvoerpoort Hallo **importgegevens** module.</span><span class="sxs-lookup"><span data-stu-id="4371c-295">Right-click hello output port of hello **Import Data** module.</span></span> <span data-ttu-id="4371c-296">Dit blijkt een **opslaan als gegevensset** optie en een **Visualize** optie.</span><span class="sxs-lookup"><span data-stu-id="4371c-296">This reveals a **Save as dataset** option and a **Visualize** option.</span></span> <span data-ttu-id="4371c-297">Hallo **Visualize** optie, als u klikt, wordt weergegeven, 100 rijen van Hallo-gegevens, inclusief een rechterpaneel die nuttig is voor sommige samenvattende statistieken.</span><span class="sxs-lookup"><span data-stu-id="4371c-297">hello **Visualize** option, if clicked, displays 100 rows of hello data, along with a right panel that is useful for some summary statistics.</span></span> <span data-ttu-id="4371c-298">toosave gegevens, schakelt u gewoon **opslaan als gegevensset** en volg de instructies.</span><span class="sxs-lookup"><span data-stu-id="4371c-298">toosave data, simply select **Save as dataset** and follow instructions.</span></span>

<span data-ttu-id="4371c-299">tooselect hello opgeslagen gegevensset voor gebruik in een machine learning-experiment vinden Hallo gegevenssets Hallo met **Search** vak weergegeven in de volgende afbeelding Hallo.</span><span class="sxs-lookup"><span data-stu-id="4371c-299">tooselect hello saved dataset for use in a machine learning experiment, locate hello datasets using hello **Search** box shown in hello following figure.</span></span> <span data-ttu-id="4371c-300">Klik gewoon type out Hallo-naam die u hebt opgegeven Hallo gegevensset gedeeltelijk tooaccess deze en sleep de gegevensset op Hallo Hallo hoofdpaneel.</span><span class="sxs-lookup"><span data-stu-id="4371c-300">Then simply type out hello name you gave hello dataset partially tooaccess it and drag hello dataset onto hello main panel.</span></span> <span data-ttu-id="4371c-301">Neer te zetten naar Hallo hoofdpaneel de wordt geselecteerd voor gebruik in machine learning-model.</span><span class="sxs-lookup"><span data-stu-id="4371c-301">Dropping it onto hello main panel selects it for use in machine learning modeling.</span></span>

![Drage gegevensset naar het hoofdpaneel Hallo](./media/machine-learning-data-science-process-hive-criteo-walkthrough/cl5tpGw.png)

> [!NOTE]
> <span data-ttu-id="4371c-303">Doe dit voor zowel Hallo trein en Hallo test gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="4371c-303">Do this for both hello train and hello test datasets.</span></span> <span data-ttu-id="4371c-304">Denk eraan dat toouse Hallo databasenaam en tabelnamen die u hebt opgegeven voor dit doel.</span><span class="sxs-lookup"><span data-stu-id="4371c-304">Also, remember toouse hello database name and table names that you gave for this purpose.</span></span> <span data-ttu-id="4371c-305">Hallo-waarden die worden gebruikt in de afbeelding Hallo dienen uitsluitend ter illustratie purposes.* *</span><span class="sxs-lookup"><span data-stu-id="4371c-305">hello values used in hello figure are solely for illustration purposes.**</span></span>
> 
> 

### <span data-ttu-id="4371c-306"><a name="step2"></a>Stap 2: Een eenvoudig experiment maken in Azure Machine Learning toopredict klikken / geen klikken</span><span class="sxs-lookup"><span data-stu-id="4371c-306"><a name="step2"></a> Step 2: Create a simple experiment in Azure Machine Learning toopredict clicks / no clicks</span></span>
<span data-ttu-id="4371c-307">Ons Azure ML-experiment ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="4371c-307">Our Azure ML experiment looks like this:</span></span>

![Machine Learning-experiment](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xRpVfrY.png)

<span data-ttu-id="4371c-309">We nu eens kijken hoe Hallo belangrijke onderdelen van dit experiment.</span><span class="sxs-lookup"><span data-stu-id="4371c-309">We now examine hello key components of this experiment.</span></span> <span data-ttu-id="4371c-310">Als een herinnering moeten we toodrag onze opgeslagen trainen en gegevenssets op tooour experimentcanvas eerst te testen.</span><span class="sxs-lookup"><span data-stu-id="4371c-310">As a reminder, we need toodrag our saved train and test datasets on tooour experiment canvas first.</span></span>

#### <a name="clean-missing-data"></a><span data-ttu-id="4371c-311">De ontbrekende gegevens opschonen</span><span class="sxs-lookup"><span data-stu-id="4371c-311">Clean Missing Data</span></span>
<span data-ttu-id="4371c-312">Hallo **Clean Missing Data** module biedt wat de naam al aangeeft: het ontbrekende gegevens op een manier die de gebruiker opgegeven kunnen worden schoongemaakt.</span><span class="sxs-lookup"><span data-stu-id="4371c-312">hello **Clean Missing Data** module does what its name suggests:  it cleans missing data in ways that can be user-specified.</span></span> <span data-ttu-id="4371c-313">In deze module zoekt, ziet u dit:</span><span class="sxs-lookup"><span data-stu-id="4371c-313">Looking into this module, we see this:</span></span>

![Ontbrekende gegevens opschonen](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0ycXod6.png)

<span data-ttu-id="4371c-315">We gekozen hier alle ontbrekende waarden met een 0 tooreplace.</span><span class="sxs-lookup"><span data-stu-id="4371c-315">Here, we chose tooreplace all missing values with a 0.</span></span> <span data-ttu-id="4371c-316">Er zijn andere opties, die kunnen worden gezien door te kijken Hallo opgegeven waarin dropdowns in Hallo-module.</span><span class="sxs-lookup"><span data-stu-id="4371c-316">There are other options as well, which can be seen by looking at hello dropdowns in hello module.</span></span>

#### <a name="feature-engineering-on-hello-data"></a><span data-ttu-id="4371c-317">Functie-engineering op Hallo-gegevens</span><span class="sxs-lookup"><span data-stu-id="4371c-317">Feature engineering on hello data</span></span>
<span data-ttu-id="4371c-318">Er zijn miljoenen unieke waarden voor sommige categorische functies van grote gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="4371c-318">There can be millions of unique values for some categorical features of large datasets.</span></span> <span data-ttu-id="4371c-319">Naïve-methoden zoals een hot codering voor het voorstellen van dergelijke hoge dimensionale categorische functies is volledig unfeasible.</span><span class="sxs-lookup"><span data-stu-id="4371c-319">Using naive methods such as one-hot encoding for representing such high-dimensional categorical features is entirely unfeasible.</span></span> <span data-ttu-id="4371c-320">In dit overzicht ziet u hoe toouse aantal onderdelen met de ingebouwde Azure Machine Learning-modules toogenerate weergaven van deze hoge-dimensionale categorische variabelen comprimeren.</span><span class="sxs-lookup"><span data-stu-id="4371c-320">In this walkthrough, we demonstrate how toouse count features using built-in Azure Machine Learning modules toogenerate compact representations of these high-dimensional categorical variables.</span></span> <span data-ttu-id="4371c-321">Hallo-eindresultaat is een kleinere model, sneller training en maatstaven voor prestaties die erg vergelijkbaar toousing andere technieken.</span><span class="sxs-lookup"><span data-stu-id="4371c-321">hello end-result is a smaller model size, faster training times, and performance metrics that are quite comparable toousing other techniques.</span></span>

##### <a name="building-counting-transforms"></a><span data-ttu-id="4371c-322">Gebouw transformaties tellen</span><span class="sxs-lookup"><span data-stu-id="4371c-322">Building counting transforms</span></span>
<span data-ttu-id="4371c-323">toobuild aantal functies, gebruiken we Hallo **bouwen tellen transformeren** module die beschikbaar is in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4371c-323">toobuild count features, we use hello **Build Counting Transform** module that is available in Azure Machine Learning.</span></span> <span data-ttu-id="4371c-324">Hallo module ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="4371c-324">hello module looks like this:</span></span>

<span data-ttu-id="4371c-325">![Module tellen transformeren maken](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![module bouwen tellen transformeren](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span><span class="sxs-lookup"><span data-stu-id="4371c-325">![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/e0eqKtZ.png)
![Build Counting Transform module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OdDN0vw.png)</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="4371c-326">In Hallo **tellen kolommen** vak we invoeren die we willen tooperform telt op kolommen.</span><span class="sxs-lookup"><span data-stu-id="4371c-326">In hello **Count columns** box, we enter those columns that we wish tooperform counts on.</span></span> <span data-ttu-id="4371c-327">Dit zijn meestal (zoals vermeld) hoge dimensionale categorische kolommen.</span><span class="sxs-lookup"><span data-stu-id="4371c-327">Typically, these are (as mentioned) high-dimensional categorical columns.</span></span> <span data-ttu-id="4371c-328">Aan begin hello wordt gezegd dat Hallo Criteo gegevensset heeft 26 categorische kolommen: van Col15 tooCol40.</span><span class="sxs-lookup"><span data-stu-id="4371c-328">At hello start, we mentioned that hello Criteo dataset has 26 categorical columns: from Col15 tooCol40.</span></span> <span data-ttu-id="4371c-329">Hier we tellen op alle mappen en hun indexen geven (van 15 too40 gescheiden door komma's, zoals wordt weergegeven).</span><span class="sxs-lookup"><span data-stu-id="4371c-329">Here, we count on all of them and give their indices (from 15 too40 separated by commas as shown).</span></span>
> 

<span data-ttu-id="4371c-330">toouse hello module Hallo MapReduce-modus (geschikt voor grote gegevenssets), wij toegang moet krijgen tot tooan HDInsight Hadoop-cluster (hello gebruikt voor de functie verkenning opnieuw kan worden gebruikt voor dit doel ook) en de referenties.</span><span class="sxs-lookup"><span data-stu-id="4371c-330">toouse hello module in hello MapReduce mode (appropriate for large datasets), we need access tooan HDInsight Hadoop cluster (hello one used for feature exploration can be reused for this purpose as well) and its credentials.</span></span> <span data-ttu-id="4371c-331">Hallo vorige afbeeldingen laten zien welke Hallo ingevulde waarden eruit (vervangen Hallo waarden opgegeven voor de afbeelding met die relevant zijn voor uw eigen gebruiksvoorbeeld).</span><span class="sxs-lookup"><span data-stu-id="4371c-331">hello  previous figures illustrate what hello filled-in values look like (replace hello values provided for illustration with those relevant for your own use-case).</span></span>

![Moduleparameters](./media/machine-learning-data-science-process-hive-criteo-walkthrough/05IqySf.png)

<span data-ttu-id="4371c-333">In de bovenstaande Hallo afbeelding, laten we zien hoe tooenter Hallo blob invoer locatie.</span><span class="sxs-lookup"><span data-stu-id="4371c-333">In hello figure above, we show how tooenter hello input blob location.</span></span> <span data-ttu-id="4371c-334">Deze locatie heeft gereserveerd voor het aantal tabellen maken op Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="4371c-334">This location has hello data reserved for building count tables on.</span></span>

<span data-ttu-id="4371c-335">Nadat deze module is voltooid, we kunt opslaan Hallo transformatie voor later met de rechtermuisknop op Hallo module Hallo selecteren **opslaan als transformatie** optie:</span><span class="sxs-lookup"><span data-stu-id="4371c-335">After this module finishes running, we can save hello transform for later by right-clicking hello module and selecting hello **Save as Transform** option:</span></span>

![Optie 'Opslaan als transformatie'](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IcVgvHR.png)

<span data-ttu-id="4371c-337">In onze experiment architectuur hierboven weergegeven, overeen Hallo gegevensset 'ytransform2' nauwkeurig tooa aantal transformatie opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4371c-337">In our experiment architecture shown above, hello dataset "ytransform2" corresponds precisely tooa saved count transform.</span></span> <span data-ttu-id="4371c-338">Hallo rest van dit experiment, gaan we ervan uit dat Hallo lezer gebruikt een **bouwen tellen transformeren** -module op sommige gegevens toogenerate tellingen en kan vervolgens die aantallen toogenerate aantal functies op Hallo train gebruiken en gegevenssets te testen.</span><span class="sxs-lookup"><span data-stu-id="4371c-338">For hello remainder of this experiment, we assume that hello reader used a **Build Counting Transform** module on some data toogenerate counts, and can then use those counts toogenerate count features on hello train and test datasets.</span></span>

##### <a name="choosing-what-count-features-tooinclude-as-part-of-hello-train-and-test-datasets"></a><span data-ttu-id="4371c-339">Kiezen wat functies tooinclude als onderdeel van de trein Hallo tellen en gegevenssets testen</span><span class="sxs-lookup"><span data-stu-id="4371c-339">Choosing what count features tooinclude as part of hello train and test datasets</span></span>
<span data-ttu-id="4371c-340">Zodra er een aantal transformeren gereed hebt, Hallo-gebruiker kan kiezen welke tooinclude functies in hun trein, en testen met behulp van Hallo gegevenssets **wijzigen aantal tabel Parameters** module.</span><span class="sxs-lookup"><span data-stu-id="4371c-340">Once we have a count transform ready, hello user can choose what features tooinclude in their train and test datasets using hello **Modify Count Table Parameters** module.</span></span> <span data-ttu-id="4371c-341">We deze module alleen weergeven hier voor de volledigheid, maar uit oogpunt van eenvoud daadwerkelijk gebruik deze functie niet bij ons experiment.</span><span class="sxs-lookup"><span data-stu-id="4371c-341">We just show this module here for completeness, but in interests of simplicity do not actually use it in our experiment.</span></span>

![De parameters voor aantal wijzigen](./media/machine-learning-data-science-process-hive-criteo-walkthrough/PfCHkVg.png)

<span data-ttu-id="4371c-343">In dit geval zoals u kunt zien, we hebben ervoor gekozen toouse alleen Hallo logboek-kans en tooignore Hallo kolom uitgesteld.</span><span class="sxs-lookup"><span data-stu-id="4371c-343">In this case, as can be seen, we have chosen toouse just hello log-odds and tooignore hello back off column.</span></span> <span data-ttu-id="4371c-344">We kunnen ook parameters instellen, zoals Hallo garbagecollection bin drempelwaarde, hoeveel pseudo eerdere voorbeelden tooadd voor vloeiend maken, en of toouse eventuele Laplacian ruis of niet.</span><span class="sxs-lookup"><span data-stu-id="4371c-344">We can also set parameters such as hello garbage bin threshold, how many pseudo-prior examples tooadd for smoothing, and whether toouse any Laplacian noise or not.</span></span> <span data-ttu-id="4371c-345">Al deze functies zijn geavanceerde en is toobe aangegeven dat de standaardwaarden Hallo een goed uitgangspunt voor gebruikers die nieuwe toothis-type van het genereren van de functie zijn zijn.</span><span class="sxs-lookup"><span data-stu-id="4371c-345">All these are advanced features and it is toobe noted that hello default values are a good starting point for users who are new toothis type of feature generation.</span></span>

##### <a name="data-transformation-before-generating-hello-count-features"></a><span data-ttu-id="4371c-346">Gegevenstransformatie vóór het genereren van Hallo aantal functies</span><span class="sxs-lookup"><span data-stu-id="4371c-346">Data transformation before generating hello count features</span></span>
<span data-ttu-id="4371c-347">Nu we zich richten op een belangrijk punt over onze train transformeren en testen van de gegevens van de voorafgaande tooactually genereren aantal functies.</span><span class="sxs-lookup"><span data-stu-id="4371c-347">Now we focus on an important point about transforming our train and test data prior tooactually generating count features.</span></span> <span data-ttu-id="4371c-348">Houd er rekening mee dat er twee zijn **R-Script uitvoeren** modules die worden gebruikt voordat we Hallo aantal transformatie tooour gegevens toepassen.</span><span class="sxs-lookup"><span data-stu-id="4371c-348">Note that there are two **Execute R Script** modules used before we apply hello count transform tooour data.</span></span>

![Modules R-Script uitvoeren](./media/machine-learning-data-science-process-hive-criteo-walkthrough/aF59wbc.png)

<span data-ttu-id="4371c-350">Dit is de eerste R-script Hallo:</span><span class="sxs-lookup"><span data-stu-id="4371c-350">Here is hello first R script:</span></span>

![Eerste R-script](./media/machine-learning-data-science-process-hive-criteo-walkthrough/3hkIoMx.png)

<span data-ttu-id="4371c-352">In deze R-script wijzigen we onze toonames kolommen 'Col1' te 'Col40'.</span><span class="sxs-lookup"><span data-stu-id="4371c-352">In this R script, we rename our columns toonames "Col1" too"Col40".</span></span> <span data-ttu-id="4371c-353">Dit is omdat Hallo aantal transformatie namen van deze indeling verwacht.</span><span class="sxs-lookup"><span data-stu-id="4371c-353">This is because hello count transform expects names of this format.</span></span>

<span data-ttu-id="4371c-354">In de tweede R-script hello, we Hallo-verdeling tussen klassen positieve en negatieve saldo (respectievelijk klassen 1 en 0) door downsampling Hallo negatieve klasse.</span><span class="sxs-lookup"><span data-stu-id="4371c-354">In hello second R script, we balance hello distribution between positive and negative classes (classes 1 and 0 respectively) by downsampling hello negative class.</span></span> <span data-ttu-id="4371c-355">Hallo R script hoe hier toont toodo dit:</span><span class="sxs-lookup"><span data-stu-id="4371c-355">hello R script here shows how toodo this:</span></span>

![Tweede R-script](./media/machine-learning-data-science-process-hive-criteo-walkthrough/91wvcwN.png)

<span data-ttu-id="4371c-357">In dit eenvoudige R-script gebruiken we ' pos\_neg\_verhouding ' tooset Hallo hoeveelheid balans tussen Hallo positieve en negatieve Hallo-klassen.</span><span class="sxs-lookup"><span data-stu-id="4371c-357">In this simple R script, we use "pos\_neg\_ratio" tooset hello amount of balance between hello positive and hello negative classes.</span></span> <span data-ttu-id="4371c-358">Dit is belangrijk toodo aangezien prestatievoordelen voor classificatie problemen meestal verbeteren van de klasse onbalans heeft waar Hallo klasse distributie is vervormd (intrekken dat in ons geval we 3.3% positief klasse en 96,7% negatief klasse hebben).</span><span class="sxs-lookup"><span data-stu-id="4371c-358">This is important toodo since improving class imbalance usually has performance benefits for classification problems where hello class distribution is skewed (recall that in our case, we have 3.3% positive class and 96.7% negative class).</span></span>

##### <a name="applying-hello-count-transformation-on-our-data"></a><span data-ttu-id="4371c-359">Hallo aantal transformatie toepassen op onze gegevens</span><span class="sxs-lookup"><span data-stu-id="4371c-359">Applying hello count transformation on our data</span></span>
<span data-ttu-id="4371c-360">Ten slotte gebruiken we Hallo **transformatie toepassen** module tooapply aantal transformaties op onze train Hallo en gegevenssets te testen.</span><span class="sxs-lookup"><span data-stu-id="4371c-360">Finally, we can use hello **Apply Transformation** module tooapply hello count transforms on our train and test datasets.</span></span> <span data-ttu-id="4371c-361">Deze module wordt van Hallo opgeslagen aantal transformatie als één invoer- en Hallo trainen of gegevenssets testen als andere invoer Hallo en retourneert gegevens met een aantal functies.</span><span class="sxs-lookup"><span data-stu-id="4371c-361">This module takes hello saved count transform as one input and hello train or test datasets as hello other input, and returns data with count features.</span></span> <span data-ttu-id="4371c-362">Hier wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="4371c-362">It is shown here:</span></span>

![Transformatie module toepassen](./media/machine-learning-data-science-process-hive-criteo-walkthrough/xnQvsYf.png)

##### <a name="an-excerpt-of-what-hello-count-features-look-like"></a><span data-ttu-id="4371c-364">Een fragment Hallo aantal onderdelen van het uiterlijk van</span><span class="sxs-lookup"><span data-stu-id="4371c-364">An excerpt of what hello count features look like</span></span>
<span data-ttu-id="4371c-365">Het is instructieve toosee welke functies van de count Hallo in ons geval eruit.</span><span class="sxs-lookup"><span data-stu-id="4371c-365">It is instructive toosee what hello count features look like in our case.</span></span> <span data-ttu-id="4371c-366">Hier wordt een fragment van deze weergeven:</span><span class="sxs-lookup"><span data-stu-id="4371c-366">Here we show an excerpt of this:</span></span>

![Aantal functies](./media/machine-learning-data-science-process-hive-criteo-walkthrough/FO1nNfw.png)

<span data-ttu-id="4371c-368">In dit fragment zien we dat voor kolommen die we geteld op Hallo we Hallo aantallen ophalen en meld u kans toevoeging tooany relevante backoffs.</span><span class="sxs-lookup"><span data-stu-id="4371c-368">In this excerpt, we show that for hello columns that we counted on, we get hello counts and log odds in addition tooany relevant backoffs.</span></span>

<span data-ttu-id="4371c-369">Er zijn nu gereed toobuild een Azure Machine Learning-model met behulp van deze getransformeerde gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="4371c-369">We are now ready toobuild an Azure Machine Learning model using these transformed datasets.</span></span> <span data-ttu-id="4371c-370">In de volgende sectie hello, laten we zien hoe u dit kunt doen.</span><span class="sxs-lookup"><span data-stu-id="4371c-370">In hello next section, we show how this can be done.</span></span>

### <span data-ttu-id="4371c-371"><a name="step3"></a>Stap 3: Maken, te trainen en Hallo model beoordelen</span><span class="sxs-lookup"><span data-stu-id="4371c-371"><a name="step3"></a> Step 3: Build, train, and score hello model</span></span>

#### <a name="choice-of-learner"></a><span data-ttu-id="4371c-372">Keuze van cursist</span><span class="sxs-lookup"><span data-stu-id="4371c-372">Choice of learner</span></span>
<span data-ttu-id="4371c-373">We moeten eerst een cursist toochoose.</span><span class="sxs-lookup"><span data-stu-id="4371c-373">First, we need toochoose a learner.</span></span> <span data-ttu-id="4371c-374">We zijn gaan toouse een beslissingsstructuur twee class boosted onze cursist.</span><span class="sxs-lookup"><span data-stu-id="4371c-374">We are going toouse a two class boosted decision tree as our learner.</span></span> <span data-ttu-id="4371c-375">Hier volgen de standaardopties Hallo voor deze cursist:</span><span class="sxs-lookup"><span data-stu-id="4371c-375">Here are hello default options for this learner:</span></span>

![Two-Class Boosted Decision Tree parameters](./media/machine-learning-data-science-process-hive-criteo-walkthrough/bH3ST2z.png)

<span data-ttu-id="4371c-377">Voor onze experiment zijn we continu toochoose Hallo standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="4371c-377">For our experiment, we are going toochoose hello default values.</span></span> <span data-ttu-id="4371c-378">We Houd er rekening mee dat Hallo standaardinstellingen zijn meestal zinvolle en voor een goede manier tooget snelle basislijnen op de prestaties.</span><span class="sxs-lookup"><span data-stu-id="4371c-378">We note that hello defaults are usually meaningful and a good way tooget quick baselines on performance.</span></span> <span data-ttu-id="4371c-379">U kunt op de prestaties verbeteren door verstrekkende parameters als u ervoor kiest tooonce die u hebt een basislijn.</span><span class="sxs-lookup"><span data-stu-id="4371c-379">You can improve on performance by sweeping parameters if you choose tooonce you have a baseline.</span></span>

#### <a name="train-hello-model"></a><span data-ttu-id="4371c-380">Hallo-model trainen</span><span class="sxs-lookup"><span data-stu-id="4371c-380">Train hello model</span></span>
<span data-ttu-id="4371c-381">Voor training, roepen we gewoon een **Train Model** module.</span><span class="sxs-lookup"><span data-stu-id="4371c-381">For training, we simply invoke a **Train Model** module.</span></span> <span data-ttu-id="4371c-382">Hallo twee invoer tooit zijn Hallo Two-Class Boosted Decision Tree cursist en onze train-gegevensset.</span><span class="sxs-lookup"><span data-stu-id="4371c-382">hello two inputs tooit are hello Two-Class Boosted Decision Tree learner and our train dataset.</span></span> <span data-ttu-id="4371c-383">Dit wordt hier weergegeven:</span><span class="sxs-lookup"><span data-stu-id="4371c-383">This is shown here:</span></span>

![Module Train-Model](./media/machine-learning-data-science-process-hive-criteo-walkthrough/2bZDZTy.png)

#### <a name="score-hello-model"></a><span data-ttu-id="4371c-385">Hallo-score-model</span><span class="sxs-lookup"><span data-stu-id="4371c-385">Score hello model</span></span>
<span data-ttu-id="4371c-386">Zodra er een getraind model hebt, we klaar zijn tooscore op Hallo testen gegevensset en tooevaluate de prestaties.</span><span class="sxs-lookup"><span data-stu-id="4371c-386">Once we have a trained model, we are ready tooscore on hello test dataset and tooevaluate its performance.</span></span> <span data-ttu-id="4371c-387">We doen dit met behulp van Hallo **Score Model** module weergegeven in de volgende afbeelding, samen met Hallo een **Evaluate Model** module:</span><span class="sxs-lookup"><span data-stu-id="4371c-387">We do this by using hello **Score Model** module shown in hello following figure, along with an **Evaluate Model** module:</span></span>

![De module Score Model (Scoremodel)](./media/machine-learning-data-science-process-hive-criteo-walkthrough/fydcv6u.png)

### <span data-ttu-id="4371c-389"><a name="step4"></a>Stap 4: Hallo model evalueren</span><span class="sxs-lookup"><span data-stu-id="4371c-389"><a name="step4"></a> Step 4: Evaluate hello model</span></span>
<span data-ttu-id="4371c-390">Willen we graag ten slotte tooanalyze model prestaties.</span><span class="sxs-lookup"><span data-stu-id="4371c-390">Finally, we would like tooanalyze model performance.</span></span> <span data-ttu-id="4371c-391">Meestal is een goede indicatie voor twee klasse (binair) classificatie problemen, Hallo AUC.</span><span class="sxs-lookup"><span data-stu-id="4371c-391">Usually, for two class (binary) classification problems, a good measure is hello AUC.</span></span> <span data-ttu-id="4371c-392">toovisualize, we Hallo aansluiten **Score Model** module tooan **Evaluate Model** -module voor dit.</span><span class="sxs-lookup"><span data-stu-id="4371c-392">toovisualize this, we hook up hello **Score Model** module tooan **Evaluate Model** module for this.</span></span> <span data-ttu-id="4371c-393">Te klikken op **Visualize** op Hallo **Evaluate Model** module resulteert in een afbeelding zoals Hallo volgt:</span><span class="sxs-lookup"><span data-stu-id="4371c-393">Clicking **Visualize** on hello **Evaluate Model** module yields a graphic like hello following one:</span></span>

![Module BDT model evalueren](./media/machine-learning-data-science-process-hive-criteo-walkthrough/0Tl0cdg.png)

<span data-ttu-id="4371c-395">Binair (of twee klasse) classificatie problemen met een goede indicatie van nauwkeurigheid is Hallo gebied onder Curve (AUC).</span><span class="sxs-lookup"><span data-stu-id="4371c-395">In binary (or two class) classification problems, a good measure of prediction accuracy is hello Area Under Curve (AUC).</span></span> <span data-ttu-id="4371c-396">In het volgende, laten we zien onze resultaten met dit model op onze testgegevensset.</span><span class="sxs-lookup"><span data-stu-id="4371c-396">In what follows, we show our results using this model on our test dataset.</span></span> <span data-ttu-id="4371c-397">tooget deze, klik met de rechtermuisknop Hallo uitvoerpoort Hallo **Evaluate Model** module en vervolgens **Visualize**.</span><span class="sxs-lookup"><span data-stu-id="4371c-397">tooget this, right-click hello output port of hello **Evaluate Model** module and then **Visualize**.</span></span>

![Module Evaluate Model visualiseren](./media/machine-learning-data-science-process-hive-criteo-walkthrough/IRfc7fH.png)

### <span data-ttu-id="4371c-399"><a name="step5"></a>Stap 5: Hallo model publiceren als een webservice</span><span class="sxs-lookup"><span data-stu-id="4371c-399"><a name="step5"></a> Step 5: Publish hello model as a Web service</span></span>
<span data-ttu-id="4371c-400">Hallo mogelijkheid toopublish een Azure Machine Learning-model als webservices met een minimum van fuss is een waardevolle functie algemeen beschikbaar te maken.</span><span class="sxs-lookup"><span data-stu-id="4371c-400">hello ability toopublish an Azure Machine Learning model as web services with a minimum of fuss is a valuable feature for making it widely available.</span></span> <span data-ttu-id="4371c-401">Zodra u dat hebt gedaan, kan iedereen aanroepen toohello-webservice met invoergegevens dat ze nodig hebben voorspellingen voor en Hallo-webservice Hallo model tooreturn die voorspellingen gebruikt maken.</span><span class="sxs-lookup"><span data-stu-id="4371c-401">Once that is done, anyone can make calls toohello web service with input data that they need predictions for, and hello web service uses hello model tooreturn those predictions.</span></span>

<span data-ttu-id="4371c-402">toodo, we eerst het getrainde model opslaan als een object van het getrainde Model.</span><span class="sxs-lookup"><span data-stu-id="4371c-402">toodo this, we first save our trained model as a Trained Model object.</span></span> <span data-ttu-id="4371c-403">Dit wordt gedaan met de rechtermuisknop op Hallo **Train Model** module en met behulp van Hallo **opslaan als getrainde Model** optie.</span><span class="sxs-lookup"><span data-stu-id="4371c-403">This is done by right-clicking hello **Train Model** module and using hello **Save as Trained Model** option.</span></span>

<span data-ttu-id="4371c-404">Vervolgens moet toocreate invoer en uitvoer poorten voor onze webservice:</span><span class="sxs-lookup"><span data-stu-id="4371c-404">Next, we need toocreate input and output ports for our web service:</span></span>

* <span data-ttu-id="4371c-405">een invoerpoort worden gegevens in dezelfde formulier als Hallo-gegevens die we nodig hebben voorspellingen voor Hallo</span><span class="sxs-lookup"><span data-stu-id="4371c-405">an input port takes data in hello same form as hello data that we need predictions for</span></span>
* <span data-ttu-id="4371c-406">een uitvoerpoort retourneert Hallo Scored Labels en kansen Hallo die zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="4371c-406">an output port returns hello Scored Labels and hello associated probabilities.</span></span>

#### <a name="select-a-few-rows-of-data-for-hello-input-port"></a><span data-ttu-id="4371c-407">Selecteer een paar rijen van de gegevens voor invoerpoort Hallo</span><span class="sxs-lookup"><span data-stu-id="4371c-407">Select a few rows of data for hello input port</span></span>
<span data-ttu-id="4371c-408">Het handige toouse is een **toepassen SQL transformatie** module tooselect NET 10 rijen tooserve als Hallo poort invoergegevens.</span><span class="sxs-lookup"><span data-stu-id="4371c-408">It is convenient toouse an **Apply SQL Transformation** module tooselect just 10 rows tooserve as hello input port data.</span></span> <span data-ttu-id="4371c-409">Selecteer alleen deze rijen met gegevens voor onze invoerpoort met behulp van SQL-query Hallo hier weergegeven:</span><span class="sxs-lookup"><span data-stu-id="4371c-409">Select just these rows of data for our input port using hello SQL query shown here:</span></span>

![Invoerpoort gegevens](./media/machine-learning-data-science-process-hive-criteo-walkthrough/XqVtSxu.png)

#### <a name="web-service"></a><span data-ttu-id="4371c-411">Webservice</span><span class="sxs-lookup"><span data-stu-id="4371c-411">Web service</span></span>
<span data-ttu-id="4371c-412">We klaar toorun een kleine experiment die gebruikt toopublish worden kan onze webservice.</span><span class="sxs-lookup"><span data-stu-id="4371c-412">Now we are ready toorun a small experiment that can be used toopublish our web service.</span></span>

#### <a name="generate-input-data-for-webservice"></a><span data-ttu-id="4371c-413">Genereren van de invoergegevens voor de webservice</span><span class="sxs-lookup"><span data-stu-id="4371c-413">Generate input data for webservice</span></span>
<span data-ttu-id="4371c-414">Als een stap zeroth aangezien Hallo aantal tabel groot, we nemen van een paar regels testgegevens en uitvoergegevens genereren van het aantal functies.</span><span class="sxs-lookup"><span data-stu-id="4371c-414">As a zeroth step, since hello count table is large, we take a few lines of test data and generate output data from it with count features.</span></span> <span data-ttu-id="4371c-415">Dit kan fungeren als Hallo invoergegevens indeling voor de webservice.</span><span class="sxs-lookup"><span data-stu-id="4371c-415">This can serve as hello input data format for our webservice.</span></span> <span data-ttu-id="4371c-416">Dit wordt hier weergegeven:</span><span class="sxs-lookup"><span data-stu-id="4371c-416">This is shown here:</span></span>

![De invoergegevens BDT maken](./media/machine-learning-data-science-process-hive-criteo-walkthrough/OEJMmst.png)

> [!NOTE]
> <span data-ttu-id="4371c-418">Voor de indeling van de invoergegevens hello, gebruiken we nu Hallo uitvoer Hallo **aantal Featurizer** module.</span><span class="sxs-lookup"><span data-stu-id="4371c-418">For hello input data format, we now use hello OUTPUT of hello **Count Featurizer** module.</span></span> <span data-ttu-id="4371c-419">Zodra dit is voltooid met experimenteren, Hallo uitvoer opslaan van Hallo **aantal Featurizer** module als een Dataset.</span><span class="sxs-lookup"><span data-stu-id="4371c-419">Once this experiment finishes running, save hello output from hello **Count Featurizer** module as a Dataset.</span></span> <span data-ttu-id="4371c-420">Deze gegevensset wordt gebruikt voor Hallo invoergegevens in Hallo-webservice.</span><span class="sxs-lookup"><span data-stu-id="4371c-420">This Dataset is used for hello input data in hello webservice.</span></span>
> 
> 

#### <a name="scoring-experiment-for-publishing-webservice"></a><span data-ttu-id="4371c-421">Score berekenen voor experiment voor de publicatie-webservice</span><span class="sxs-lookup"><span data-stu-id="4371c-421">Scoring experiment for publishing webservice</span></span>
<span data-ttu-id="4371c-422">Eerst laten we zien hoe dit eruitziet.</span><span class="sxs-lookup"><span data-stu-id="4371c-422">First, we show what this looks like.</span></span> <span data-ttu-id="4371c-423">Hallo essentiële structuur is een **Score Model** module die accepteert onze getrainde model-object en een paar regels met invoergegevens die wordt gegenereerd in de vorige stappen Hallo Hallo met **aantal Featurizer** module.</span><span class="sxs-lookup"><span data-stu-id="4371c-423">hello essential structure is a **Score Model** module that accepts our trained model object and a few lines of input data that we generated in hello previous steps using hello **Count Featurizer** module.</span></span> <span data-ttu-id="4371c-424">We gebruiken de tooproject 'Kolommen in gegevensset selecteren' hello Scored labels en Hallo Score kansen.</span><span class="sxs-lookup"><span data-stu-id="4371c-424">We use "Select Columns in Dataset" tooproject out hello Scored labels and hello Score probabilities.</span></span>

![Kolommen in gegevensset selecteren](./media/machine-learning-data-science-process-hive-criteo-walkthrough/kRHrIbe.png)

<span data-ttu-id="4371c-426">U ziet hoe Hallo **Select Columns in Dataset** module kan worden gebruikt voor 'uitgefilterd' gegevens uit een gegevensset.</span><span class="sxs-lookup"><span data-stu-id="4371c-426">Notice how hello **Select Columns in Dataset** module can be used for 'filtering' data out from a dataset.</span></span> <span data-ttu-id="4371c-427">We weergeven hier Hallo-inhoud:</span><span class="sxs-lookup"><span data-stu-id="4371c-427">We show hello contents here:</span></span>

![Filteren met hello Select Columns in Dataset-module](./media/machine-learning-data-science-process-hive-criteo-walkthrough/oVUJC9K.png)

<span data-ttu-id="4371c-429">tooget hello blauw invoer en uitvoer poorten, klikt u op **voorbereiden webservice** op Hallo rechtsonder.</span><span class="sxs-lookup"><span data-stu-id="4371c-429">tooget hello blue input and output ports, you simply click **prepare webservice** at hello bottom right.</span></span> <span data-ttu-id="4371c-430">Dit experiment uitgevoerd kunt ook ons toopublish Hallo-webservice: klikt u op Hallo **WEBSERVICE PUBLICEERT** pictogram Hallo onderkant rechts, weergegeven hier:</span><span class="sxs-lookup"><span data-stu-id="4371c-430">Running this experiment also allows us toopublish hello web service: click hello **PUBLISH WEB SERVICE** icon at hello bottom right, shown here:</span></span>

![Webservice publiceren](./media/machine-learning-data-science-process-hive-criteo-walkthrough/WO0nens.png)

<span data-ttu-id="4371c-432">Zodra het Hallo-webservice wordt gepubliceerd, krijgen we omgeleide tooa pagina die er zo uitziet:</span><span class="sxs-lookup"><span data-stu-id="4371c-432">Once hello webservice is published, we get redirected tooa page that looks thus:</span></span>

![Web service-dashboard](./media/machine-learning-data-science-process-hive-criteo-walkthrough/YKzxAA5.png)

<span data-ttu-id="4371c-434">Twee koppelingen voor webservices zien we aan de linkerkant Hallo:</span><span class="sxs-lookup"><span data-stu-id="4371c-434">We see two links for webservices on hello left side:</span></span>

* <span data-ttu-id="4371c-435">Hallo **aanvragen/reacties** Service (of RR's) zijn alleen bedoeld voor één voorspellingen en is er met deze workshop gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4371c-435">hello **REQUEST/RESPONSE** Service (or RRS) is meant for single predictions and is what we utilize in this workshop.</span></span>
* <span data-ttu-id="4371c-436">Hallo **BATCHUITVOERING** Service (BES) wordt gebruikt voor voorspellingen batch en vereist dat Hallo invoergegevens gebruikt toomake voorspellingen zich in Azure Blob Storage bevinden.</span><span class="sxs-lookup"><span data-stu-id="4371c-436">hello **BATCH EXECUTION** Service (BES) is used for batch predictions and requires that hello input data used toomake predictions reside in Azure Blob Storage.</span></span>

<span data-ttu-id="4371c-437">Te klikken op de koppeling Hallo **aanvragen/reacties** duurt tooa pagina waarmee ons blik vooraf code in C#, python en R. Deze code kan gemakkelijk worden gebruikt voor het maken van aanroepen toohello webservice.</span><span class="sxs-lookup"><span data-stu-id="4371c-437">Clicking on hello link **REQUEST/RESPONSE** takes us tooa page that gives us pre-canned code in C#, python, and R. This code can be conveniently used for making calls toohello webservice.</span></span> <span data-ttu-id="4371c-438">Houd er rekening mee dat Hallo API-sleutel op deze pagina moet toobe gebruikt voor verificatie.</span><span class="sxs-lookup"><span data-stu-id="4371c-438">Note that hello API key on this page needs toobe used for authentication.</span></span>

<span data-ttu-id="4371c-439">Het is handige toocopy deze python via tooa nieuwe cel in Hallo IPython notebook code.</span><span class="sxs-lookup"><span data-stu-id="4371c-439">It is convenient toocopy this python code over tooa new cell in hello IPython notebook.</span></span>

<span data-ttu-id="4371c-440">We weergeven hier een segment van python-code met de juiste API-sleutel Hallo.</span><span class="sxs-lookup"><span data-stu-id="4371c-440">Here we show a segment of python code with hello correct API key.</span></span>

![Python-code](./media/machine-learning-data-science-process-hive-criteo-walkthrough/f8N4L4g.png)

<span data-ttu-id="4371c-442">Houd er rekening mee dat we Hallo standaard API-sleutel hebt vervangen door onze webservices-API-sleutel.</span><span class="sxs-lookup"><span data-stu-id="4371c-442">Note that we replaced hello default API key with our webservices's API key.</span></span> <span data-ttu-id="4371c-443">Te klikken op **uitvoeren** op deze cel in een IPython levert notebook Hallo antwoord te volgen:</span><span class="sxs-lookup"><span data-stu-id="4371c-443">Clicking **Run** on this cell in an IPython notebook yields hello following response:</span></span>

![IPython antwoord](./media/machine-learning-data-science-process-hive-criteo-walkthrough/KSxmia2.png)

<span data-ttu-id="4371c-445">We zien dat voor Hallo twee voorbeelden die we gevraagd over (in JSON-framework Hallo van Hallo pythonscript) testen, we antwoorden terug in de vorm Hallo 'Scored Labels, Scored kansen'.</span><span class="sxs-lookup"><span data-stu-id="4371c-445">We see that for hello two test examples we asked about (in hello JSON framework of hello python script), we get back answers in hello form "Scored Labels, Scored Probabilities".</span></span> <span data-ttu-id="4371c-446">Opmerking die in dit geval we hebt gekozen Hallo standaardwaarden die vooraf voorgedefinieerde Hallo-code bevat (0 voor alle numerieke kolommen en Hallo tekenreeks '' waarde '' voor alle categorische kolommen).</span><span class="sxs-lookup"><span data-stu-id="4371c-446">Note that in this case, we chose hello default values that hello pre-canned code provides (0's for all numeric columns and hello string "value" for all categorical columns).</span></span>

<span data-ttu-id="4371c-447">Hiermee is onze end-to-end-overzicht die laat zien hoe toohandle grootschalige gegevensset met Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4371c-447">This concludes our end-to-end walkthrough showing how toohandle large-scale dataset using Azure Machine Learning.</span></span> <span data-ttu-id="4371c-448">We gestart met een terabyte van gegevens, een Voorspellend model samengesteld en wordt geïmplementeerd als een webservice in de cloud Hallo.</span><span class="sxs-lookup"><span data-stu-id="4371c-448">We started with a terabyte of data, constructed a prediction model and deployed it as a web service in hello cloud.</span></span>

