---
title: 'Schaalbare Gegevenswetenschap met Azure Data Lake: een end-to-end-overzicht | Microsoft Docs'
description: Hoe taken toouse Azure Data Lake toodo gegevens te verkennen en binaire classificatie op een dataset.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 91a8207f-1e57-4570-b7fc-7c5fa858ffeb
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: bradsev;weig
ms.openlocfilehash: 8b05457ae7045a7aaed350a7502469f2247161e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="scalable-data-science-with-azure-data-lake-an-end-to-end-walkthrough"></a><span data-ttu-id="087de-103">Schaalbare Gegevenswetenschap met Azure Data Lake: een end-to-end-overzicht</span><span class="sxs-lookup"><span data-stu-id="087de-103">Scalable Data Science with Azure Data Lake: An end-to-end Walkthrough</span></span>
<span data-ttu-id="087de-104">Dit overzicht toont hoe toouse Azure Data Lake toodo gegevensverkenning en binaire classificatie taken van een steekproef van de NYC Hallo taxi reis en tarief gegevensset toopredict al dan niet een tip worden betaald door een tarief.</span><span class="sxs-lookup"><span data-stu-id="087de-104">This walkthrough shows how toouse Azure Data Lake toodo data exploration and binary classification tasks on a sample of hello NYC taxi trip and fare dataset toopredict whether or not a tip will be paid by a fare.</span></span> <span data-ttu-id="087de-105">Dit leidt u door de stappen Hallo Hallo [Team gegevens wetenschap proces](http://aka.ms/datascienceprocess)end-to- end, van gegevens overname toomodel training en toohello implementatie van een webservice die Hallo model publiceert.</span><span class="sxs-lookup"><span data-stu-id="087de-105">It walks you through hello steps of hello [Team Data Science Process](http://aka.ms/datascienceprocess), end-to-end, from data acquisition toomodel training, and then toohello deployment of a web service that publishes hello model.</span></span>

### <a name="azure-data-lake-analytics"></a><span data-ttu-id="087de-106">Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="087de-106">Azure Data Lake Analytics</span></span>
<span data-ttu-id="087de-107">Hallo [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) heeft alle Hallo mogelijkheden vereist toomake gemakkelijk voor gegevens verzameld toostore gegevens van elke grootte, vorm en de snelheid en tooconduct gegevensverwerking advanced analytics en machine learning-model met hoge schaalbaarheid in een rendabele manier.</span><span class="sxs-lookup"><span data-stu-id="087de-107">hello [Microsoft Azure Data Lake](https://azure.microsoft.com/solutions/data-lake/) has all hello capabilities required toomake it easy for data scientists toostore data of any size, shape and speed, and tooconduct data processing, advanced analytics, and machine learning modeling with high scalability in a cost-effective way.</span></span>   <span data-ttu-id="087de-108">U betaalt op basis van per taak alleen wanneer de gegevens daadwerkelijk wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="087de-108">You pay on a per-job basis, only when data is actually being processed.</span></span> <span data-ttu-id="087de-109">Azure Data Lake Analytics bevat U-SQL, een taal of overvloeiingen Hallo declaratieve aard van SQL met Hallo expressieve voordelen van C# tooprovide schaalbare gedistribueerde query-mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="087de-109">Azure Data Lake Analytics includes U-SQL, a language that blends hello declarative nature of SQL with hello expressive power of C# tooprovide scalable distributed query capability.</span></span> <span data-ttu-id="087de-110">Hiermee kunt u tooprocess ongestructureerde gegevens door het schema toepassen op lezen, plaatst u aangepaste regels en door de gebruiker gedefinieerde functies (UDF's) en omvat uitbreidbaarheid tooenable fijn gedetailleerde controle over hoe tooexecute op grote schaal.</span><span class="sxs-lookup"><span data-stu-id="087de-110">It enables you tooprocess unstructured data by applying schema on read, insert custom logic and user defined functions (UDFs), and includes extensibility tooenable fine grained control over how tooexecute at scale.</span></span> <span data-ttu-id="087de-111">toolearn meer informatie over het Hallo-ontwerpplan achter de U-SQL, Zie [Visual Studio-blogbericht](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span><span class="sxs-lookup"><span data-stu-id="087de-111">toolearn more about hello design philosophy behind U-SQL, see [Visual Studio blog post](https://blogs.msdn.microsoft.com/visualstudio/2015/09/28/introducing-u-sql-a-language-that-makes-big-data-processing-easy/).</span></span>

<span data-ttu-id="087de-112">Data Lake Analytics is ook een belangrijk onderdeel van Cortana Analytics Suite en werkt met Azure SQL Data Warehouse, Power BI en Data Factory.</span><span class="sxs-lookup"><span data-stu-id="087de-112">Data Lake Analytics is also a key part of Cortana Analytics Suite and works with Azure SQL Data Warehouse, Power BI, and Data Factory.</span></span> <span data-ttu-id="087de-113">Hierdoor krijgt u een volledig cloud big data en geavanceerde analyses platform.</span><span class="sxs-lookup"><span data-stu-id="087de-113">This gives you a complete cloud big data and advanced analytics platform.</span></span>

<span data-ttu-id="087de-114">In dit scenario begint met het Hallo-vereisten en bronnen die nodig toocomplete Hallo taken met Data Lake Analytics die Hallo gegevens wetenschappelijke processen vormen en hoe beschrijven tooinstall ze.</span><span class="sxs-lookup"><span data-stu-id="087de-114">This walkthrough begins by describing hello prerequisites and resources that are needed toocomplete hello tasks with Data Lake Analytics that form hello data science process and how tooinstall them.</span></span> <span data-ttu-id="087de-115">Het bevat een overzicht van Hallo gegevensverwerking stappen met U-SQL en tot slot wordt weergegeven hoe toouse Python en Hive met Azure Machine Learning Studio toobuild en Hallo voorspellende modellen implementeren.</span><span class="sxs-lookup"><span data-stu-id="087de-115">Then it outlines hello data processing steps using U-SQL and concludes by showing how toouse Python and Hive with Azure Machine Learning Studio toobuild and deploy hello predictive models.</span></span> 

### <a name="u-sql-and-visual-studio"></a><span data-ttu-id="087de-116">U-SQL en Visual Studio</span><span class="sxs-lookup"><span data-stu-id="087de-116">U-SQL and Visual Studio</span></span>
<span data-ttu-id="087de-117">In dit scenario raadt het gebruik van Visual Studio tooedit U-SQL-scripts tooprocess Hallo gegevensset.</span><span class="sxs-lookup"><span data-stu-id="087de-117">This walkthrough recommends using Visual Studio tooedit U-SQL scripts tooprocess hello dataset.</span></span> <span data-ttu-id="087de-118">Hallo U-SQL-scripts zijn hier beschreven en vindt u in een afzonderlijk bestand.</span><span class="sxs-lookup"><span data-stu-id="087de-118">hello U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="087de-119">Hallo-proces omvat opnemen en steekproef nemen van Hallo gegevens verkennen.</span><span class="sxs-lookup"><span data-stu-id="087de-119">hello process includes ingesting, exploring, and sampling hello data.</span></span> <span data-ttu-id="087de-120">U ziet ook hoe toorun een U-SQL script taak in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="087de-120">It also shows how toorun a U-SQL scripted job from hello Azure portal.</span></span> <span data-ttu-id="087de-121">Hive-tabellen worden gemaakt voor het Hallo-gegevens in een gekoppelde HDInsight-cluster toofacilitate Hallo bouwen en de implementatie van een model binaire classificatie in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="087de-121">Hive tables are created for hello data in an associated HDInsight cluster toofacilitate hello building and deployment of a binary classification model in Azure Machine Learning Studio.</span></span>  

### <a name="python"></a><span data-ttu-id="087de-122">Python</span><span class="sxs-lookup"><span data-stu-id="087de-122">Python</span></span>
<span data-ttu-id="087de-123">In dit scenario bevat ook een sectie die laat zien hoe toobuild en implementeren van een Voorspellend model met behulp van Python met Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="087de-123">This walkthrough also contains a section that shows how toobuild and deploy a predictive model using Python with Azure Machine Learning Studio.</span></span>  <span data-ttu-id="087de-124">We voorzien van een Jupyter-notebook Hallo Python-scripts voor de stappen in dit proces.</span><span class="sxs-lookup"><span data-stu-id="087de-124">We provide a Jupyter notebook with hello Python scripts for these steps in this process.</span></span> <span data-ttu-id="087de-125">Hallo-notebook bevat een code voor een aantal extra functie engineering stappen en de modellen constructie zoals multiklassen classificatie en regressie modelleren bovendien toohello binaire classificatie model die hier wordt beschreven.</span><span class="sxs-lookup"><span data-stu-id="087de-125">hello notebook includes code for some additional feature engineering steps and models construction such as multiclass classification and regression modeling in addition toohello binary classification model outlined here.</span></span> <span data-ttu-id="087de-126">Hallo regressie taak is toopredict Hallo hoeveelheid Hallo tip op basis van andere functies tip.</span><span class="sxs-lookup"><span data-stu-id="087de-126">hello regression task is toopredict hello amount of hello tip based on other tip features.</span></span> 

### <a name="azure-machine-learning"></a><span data-ttu-id="087de-127">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="087de-127">Azure Machine Learning</span></span>
<span data-ttu-id="087de-128">Azure Machine Learning Studio is gebruikte toobuild en Hallo voorspellende modellen implementeren.</span><span class="sxs-lookup"><span data-stu-id="087de-128">Azure Machine Learning Studio is used toobuild and deploy hello predictive models.</span></span> <span data-ttu-id="087de-129">Dit wordt gedaan met behulp van twee methoden: eerst met Python-scripts en klik vervolgens met de Hive-tabellen in een HDInsight (Hadoop)-cluster.</span><span class="sxs-lookup"><span data-stu-id="087de-129">This is done using two approaches: first with Python scripts and then with Hive tables on an HDInsight (Hadoop) cluster.</span></span>

### <a name="scripts"></a><span data-ttu-id="087de-130">Scripts</span><span class="sxs-lookup"><span data-stu-id="087de-130">Scripts</span></span>
<span data-ttu-id="087de-131">Alleen Hallo principal stappen worden beschreven in dit scenario.</span><span class="sxs-lookup"><span data-stu-id="087de-131">Only hello principal steps are outlined in this walkthrough.</span></span> <span data-ttu-id="087de-132">U kunt downloaden Hallo volledige **U-SQL-script** en **Jupyter-Notebook** van [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span><span class="sxs-lookup"><span data-stu-id="087de-132">You can download hello full **U-SQL script** and **Jupyter Notebook** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="087de-133">Vereisten</span><span class="sxs-lookup"><span data-stu-id="087de-133">Prerequisites</span></span>
<span data-ttu-id="087de-134">Voordat u deze onderwerpen, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="087de-134">Before you begin these topics, you must have hello following:</span></span>

* <span data-ttu-id="087de-135">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="087de-135">An Azure subscription.</span></span> <span data-ttu-id="087de-136">Als u nog geen een, Zie [gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="087de-136">If you do not already have one, see [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="087de-137">(Aanbevolen) Visual Studio 2013 of later.</span><span class="sxs-lookup"><span data-stu-id="087de-137">[Recommended] Visual Studio 2013 or later.</span></span> <span data-ttu-id="087de-138">Als u nog geen een van deze versies zijn geïnstalleerd, kunt u downloaden met een gratis versie van de Community van [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span><span class="sxs-lookup"><span data-stu-id="087de-138">If you do not already have one of these versions installed, you can download a free Community version from [Visual Studio Community](https://www.visualstudio.com/vs/community/).</span></span>

> [!NOTE]
> <span data-ttu-id="087de-139">U kunt hello Azure Portal toosubmit Azure Data Lake-query's ook gebruiken in plaats van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="087de-139">Instead of Visual Studio, you can also use hello Azure Portal toosubmit Azure Data Lake queries.</span></span> <span data-ttu-id="087de-140">We geven instructies over hoe toodo dus met Visual Studio, en ook op de portal in de sectie Hallo Hallo met de titel **verwerken van gegevens met U-SQL**.</span><span class="sxs-lookup"><span data-stu-id="087de-140">We will provide instructions on how toodo so both with Visual Studio and on hello portal in hello section titled **Process data with U-SQL**.</span></span> 
> 
> 


## <a name="prepare-data-science-environment-for-azure-data-lake"></a><span data-ttu-id="087de-141">Gegevens wetenschappelijke omgeving voor Azure Data Lake voorbereiden</span><span class="sxs-lookup"><span data-stu-id="087de-141">Prepare data science environment for Azure Data Lake</span></span>
<span data-ttu-id="087de-142">tooprepare Hallo gegevens wetenschappelijke omgeving voor dit scenario maakt Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="087de-142">tooprepare hello data science environment for this walkthrough, create hello following resources:</span></span>

* <span data-ttu-id="087de-143">Azure Data Lake Store (ADLS)</span><span class="sxs-lookup"><span data-stu-id="087de-143">Azure Data Lake Store (ADLS)</span></span> 
* <span data-ttu-id="087de-144">Azure Data Lake Analytics (ADLA)</span><span class="sxs-lookup"><span data-stu-id="087de-144">Azure Data Lake Analytics (ADLA)</span></span>
* <span data-ttu-id="087de-145">Azure Blob storage-account</span><span class="sxs-lookup"><span data-stu-id="087de-145">Azure Blob storage account</span></span>
* <span data-ttu-id="087de-146">Azure Machine Learning Studio-account</span><span class="sxs-lookup"><span data-stu-id="087de-146">Azure Machine Learning Studio account</span></span>
* <span data-ttu-id="087de-147">Azure Data Lake Tools voor Visual Studio (aanbevolen)</span><span class="sxs-lookup"><span data-stu-id="087de-147">Azure Data Lake Tools for Visual Studio (Recommended)</span></span>

<span data-ttu-id="087de-148">Deze sectie biedt instructies voor het toocreate van deze bronnen.</span><span class="sxs-lookup"><span data-stu-id="087de-148">This section provides instructions on how toocreate each of these resources.</span></span> <span data-ttu-id="087de-149">Als u toouse Hive-tabellen met Azure Machine Learning, in plaats van Python, toobuild een model kiest, moet u ook tooprovision een HDInsight (Hadoop)-cluster.</span><span class="sxs-lookup"><span data-stu-id="087de-149">If you choose toouse Hive tables with Azure Machine Learning, instead of Python, toobuild a model,you will also need tooprovision an HDInsight (Hadoop) cluster.</span></span> <span data-ttu-id="087de-150">Deze alternatieve procedure in in de juiste sectie Hallo hieronder beschreven.</span><span class="sxs-lookup"><span data-stu-id="087de-150">This alternative procedure in described in hello appropriate section below.</span></span>


> [!NOTE]
> <span data-ttu-id="087de-151">Hallo **Azure Data Lake Store** kunnen worden gemaakt van afzonderlijk of bij het maken van Hallo **Azure Data Lake Analytics** als Hallo standaard opslag.</span><span class="sxs-lookup"><span data-stu-id="087de-151">hello **Azure Data Lake Store** can be created either separately or when you create hello **Azure Data Lake Analytics** as hello default storage.</span></span> <span data-ttu-id="087de-152">Instructies voor het maken van elk van deze resources afzonderlijk hieronder wordt verwezen, maar moet Hallo Data Lake storage-account niet afzonderlijk worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="087de-152">Instructions are referenced for creating each of these resources separately below, but hello Data Lake storage account need not be created separately.</span></span>
>
> 

### <a name="create-an-azure-data-lake-store"></a><span data-ttu-id="087de-153">Maken van een Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="087de-153">Create an Azure Data Lake Store</span></span>


<span data-ttu-id="087de-154">Maken van een ADLS van Hallo [Azure Portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="087de-154">Create an ADLS from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="087de-155">Zie voor meer informatie [een HDInsight-cluster maken met Data Lake Store met Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="087de-155">For details, see [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="087de-156">Ervoor tooset up Hallo Cluster AAD-identiteit in Hallo worden **DataSource** blade Hallo **optionele configuratie** blade er beschreven.</span><span class="sxs-lookup"><span data-stu-id="087de-156">Be sure tooset up hello Cluster AAD Identity in hello **DataSource** blade of hello **Optional Configuration** blade described there.</span></span> 

 ![3](./media/machine-learning-data-science-process-data-lake-walkthrough/3-create-ADLS.PNG)

### <a name="create-an-azure-data-lake-analytics-account"></a><span data-ttu-id="087de-158">Een Azure Data Lake Analytics-account maken</span><span class="sxs-lookup"><span data-stu-id="087de-158">Create an Azure Data Lake Analytics account</span></span>
<span data-ttu-id="087de-159">Maken van een account ADLA van Hallo [Azure Portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="087de-159">Create an ADLA account from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="087de-160">Zie voor meer informatie [zelfstudie: aan de slag met Azure Data Lake Analytics met Azure Portal](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="087de-160">For details, see [Tutorial: get started with Azure Data Lake Analytics using Azure Portal](../data-lake-analytics/data-lake-analytics-get-started-portal.md).</span></span> 

 ![4](./media/machine-learning-data-science-process-data-lake-walkthrough/4-create-ADLA-new.PNG)

### <a name="create-an-azure-blob-storage-account"></a><span data-ttu-id="087de-162">Een Azure Blob storage-account maken</span><span class="sxs-lookup"><span data-stu-id="087de-162">Create an Azure Blob storage account</span></span>
<span data-ttu-id="087de-163">Een Azure Blob storage-account maken vanuit Hallo [Azure Portal](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="087de-163">Create an Azure Blob storage account from hello [Azure Portal](http://portal.azure.com).</span></span> <span data-ttu-id="087de-164">Zie voor meer informatie, Hallo maken een opslagaccount in sectie [over Azure storage-accounts](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="087de-164">For details, see hello Create a storage account section in [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span>

 ![5](./media/machine-learning-data-science-process-data-lake-walkthrough/5-Create-Azure-Blob.PNG)

### <a name="set-up-an-azure-machine-learning-studio-account"></a><span data-ttu-id="087de-166">Een Azure Machine Learning Studio-account instellen</span><span class="sxs-lookup"><span data-stu-id="087de-166">Set up an Azure Machine Learning Studio account</span></span>
<span data-ttu-id="087de-167">Aanmelden van/naar Azure Machine Learning Studio vanuit Hallo [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) pagina.</span><span class="sxs-lookup"><span data-stu-id="087de-167">Sign up/into Azure Machine Learning Studio from hello [Azure Machine Learning](https://azure.microsoft.com/services/machine-learning/) page.</span></span> <span data-ttu-id="087de-168">Klik op Hallo **nu aan de slag** knop en kies vervolgens een 'Gratis werkruimte' of 'Standaard werkruimte'.</span><span class="sxs-lookup"><span data-stu-id="087de-168">Click on hello **Get started now** button and then choose a "Free Workspace" or "Standard Workspace".</span></span> <span data-ttu-id="087de-169">Hierna kunt u zich kunt toocreate experimenten in Azure ML Studio.</span><span class="sxs-lookup"><span data-stu-id="087de-169">After this you will be able toocreate experiments in Azure ML Studio.</span></span>  

### <a name="install-azure-data-lake-tools-recommended"></a><span data-ttu-id="087de-170">Installeren van Azure Data Lake Tools (aanbevolen)</span><span class="sxs-lookup"><span data-stu-id="087de-170">Install Azure Data Lake Tools [Recommended]</span></span>
<span data-ttu-id="087de-171">Azure Data Lake Tools installeren voor uw versie van Visual Studio van [Azure Data Lake Tools voor Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="087de-171">Install Azure Data Lake Tools for your version of Visual Studio from [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

 ![6](./media/machine-learning-data-science-process-data-lake-walkthrough/6-install-ADL-tools-VS.PNG)

<span data-ttu-id="087de-173">Nadat het Hallo-installatie wordt voltooid, opent u van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="087de-173">After hello installation finishes successfully, open up Visual Studio.</span></span> <span data-ttu-id="087de-174">U ziet Hallo Data Lake tabblad Hallo menu Hallo bovenaan.</span><span class="sxs-lookup"><span data-stu-id="087de-174">You should see hello Data Lake tab hello menu at hello top.</span></span> <span data-ttu-id="087de-175">Uw Azure-resources moeten worden weergegeven in het linkerpaneel Hallo wanneer je je bij uw Azure-account aanmelden.</span><span class="sxs-lookup"><span data-stu-id="087de-175">Your Azure resources should appear in hello left panel when you sign into your Azure account.</span></span>

 ![7](./media/machine-learning-data-science-process-data-lake-walkthrough/7-install-ADL-tools-VS-done.PNG)

## <a name="hello-nyc-taxi-trips-dataset"></a><span data-ttu-id="087de-177">Hallo NYC Taxi reizen gegevensset</span><span class="sxs-lookup"><span data-stu-id="087de-177">hello NYC Taxi Trips dataset</span></span>
<span data-ttu-id="087de-178">Hallo gegevensset wordt hier gebruikt, is een openbaar gegevensset--hello [NYC Taxi reizen gegevensset](http://www.andresmh.com/nyctaxitrips/).</span><span class="sxs-lookup"><span data-stu-id="087de-178">hello data set we used here is a publicly available dataset -- hello [NYC Taxi Trips dataset](http://www.andresmh.com/nyctaxitrips/).</span></span> <span data-ttu-id="087de-179">Hallo NYC Taxi reis gegevens bestaat uit ongeveer 20GB gecomprimeerde CSV-bestanden (~ 48GB ongecomprimeerde), opnemen van meer dan 173 miljoen afzonderlijke reizen en Hallo ervoor staat voor elke reis betaald.</span><span class="sxs-lookup"><span data-stu-id="087de-179">hello NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="087de-180">Elke record reis omvat Hallo ophalen en inleverbibliotheek locaties en tijden, geanonimiseerde inbreken licentienummer (stuurprogramma van) en Hallo nummer straten (taxi van unieke id).</span><span class="sxs-lookup"><span data-stu-id="087de-180">Each trip record includes hello pickup and drop-off locations and times, anonymized hack (driver's) license number, and hello medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="087de-181">Hallo-gegevens bevat informatie over alle reizen Hallo jaar 2013 en is beschikbaar in twee gegevenssets voor elke maand na Hallo:</span><span class="sxs-lookup"><span data-stu-id="087de-181">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

* <span data-ttu-id="087de-182">Hallo 'trip_data' CSV bevat reis details, zoals het aantal passagiers, ophalen en dropoff punten reis duur en duur van reis.</span><span class="sxs-lookup"><span data-stu-id="087de-182">hello 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="087de-183">Hier volgen enkele voorbeeldrecords:</span><span class="sxs-lookup"><span data-stu-id="087de-183">Here are a few sample records:</span></span>
  
       medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count, trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
* <span data-ttu-id="087de-184">Hello trip_fare CSV details van Hallo tarief betaald voor elke reis, zoals betalingstype tarief bedrag, extra kosten en belastingen, tips en tolgelden en Hallo totaalbedrag betaald bevat.</span><span class="sxs-lookup"><span data-stu-id="087de-184">hello 'trip_fare' CSV contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="087de-185">Hier volgen enkele voorbeeldrecords:</span><span class="sxs-lookup"><span data-stu-id="087de-185">Here are a few sample records:</span></span>
  
       medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
       89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
       0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
       DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="087de-186">Hallo unieke sleutel toojoin reis\_gegevens en reis\_tarief bestaat uit de volgende drie velden Hallo: straten, hack\_licentie en ophalen van\_datetime.</span><span class="sxs-lookup"><span data-stu-id="087de-186">hello unique key toojoin trip\_data and trip\_fare is composed of hello following three fields: medallion, hack\_license and pickup\_datetime.</span></span> <span data-ttu-id="087de-187">Hallo onbewerkte CSV-bestanden kunnen worden geopend vanuit een openbare Azure-opslag-blob.</span><span class="sxs-lookup"><span data-stu-id="087de-187">hello raw CSV files can be accessed from a public Azure storage blob.</span></span> <span data-ttu-id="087de-188">Hallo U-SQL-script voor deze koppeling in Hallo is [tabellen reis en tarief samenvoegen](#join) sectie.</span><span class="sxs-lookup"><span data-stu-id="087de-188">hello U-SQL script for this join is in hello [Join trip and fare tables](#join) section.</span></span>

## <a name="process-data-with-u-sql"></a><span data-ttu-id="087de-189">Verwerken van gegevens met U-SQL</span><span class="sxs-lookup"><span data-stu-id="087de-189">Process data with U-SQL</span></span>
<span data-ttu-id="087de-190">Hallo gegevensverwerkingstaken geïllustreerd in deze sectie bevatten opnemen, controleren van de kwaliteit, verkennen en steekproef nemen van Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="087de-190">hello data processing tasks illustrated in this section include ingesting, checking quality, exploring, and sampling hello data.</span></span> <span data-ttu-id="087de-191">Ook wordt gedemonstreerd hoe toojoin reis en tarief tabellen.</span><span class="sxs-lookup"><span data-stu-id="087de-191">We also show how toojoin trip and fare tables.</span></span> <span data-ttu-id="087de-192">het laatste gedeelte Hallo toont uitvoeren een U-SQL-script taak van hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="087de-192">hello final section shows run a U-SQL scripted job from hello Azure portal.</span></span> <span data-ttu-id="087de-193">Hier vindt u koppelingen tooeach subsectie:</span><span class="sxs-lookup"><span data-stu-id="087de-193">Here are links tooeach subsection:</span></span>

* [<span data-ttu-id="087de-194">Gegevensopname: in van een openbare blob-gegevens lezen</span><span class="sxs-lookup"><span data-stu-id="087de-194">Data ingestion: read in data from public blob</span></span>](#ingest)
* [<span data-ttu-id="087de-195">Data quality controles</span><span class="sxs-lookup"><span data-stu-id="087de-195">Data quality checks</span></span>](#quality)
* [<span data-ttu-id="087de-196">Gegevensverkenning</span><span class="sxs-lookup"><span data-stu-id="087de-196">Data exploration</span></span>](#explore)
* [<span data-ttu-id="087de-197">Tabellen reis en tarief samenvoegen</span><span class="sxs-lookup"><span data-stu-id="087de-197">Join trip and fare tables</span></span>](#join)
* [<span data-ttu-id="087de-198">Gegevens steekproeven</span><span class="sxs-lookup"><span data-stu-id="087de-198">Data sampling</span></span>](#sample)
* [<span data-ttu-id="087de-199">U-SQL-taken uitvoeren</span><span class="sxs-lookup"><span data-stu-id="087de-199">Run U-SQL jobs</span></span>](#run)

<span data-ttu-id="087de-200">Hallo U-SQL-scripts zijn hier beschreven en vindt u in een afzonderlijk bestand.</span><span class="sxs-lookup"><span data-stu-id="087de-200">hello U-SQL scripts are described here and provided in a separate file.</span></span> <span data-ttu-id="087de-201">U kunt downloaden Hallo volledige **U-SQL-scripts** van [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span><span class="sxs-lookup"><span data-stu-id="087de-201">You can download hello full **U-SQL scripts** from [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough).</span></span>

<span data-ttu-id="087de-202">tooexecute U-SQL Visual Studio openen, klikt u op **File--> Nieuw Project-->**, kies **U-SQL Project**, een naam en sla het tooa map.</span><span class="sxs-lookup"><span data-stu-id="087de-202">tooexecute U-SQL, Open Visual Studio, click **File --> New --> Project**, choose **U-SQL Project**, name and save it tooa folder.</span></span>

![8](./media/machine-learning-data-science-process-data-lake-walkthrough/8-create-USQL-project.PNG)

> [!NOTE]
> <span data-ttu-id="087de-204">Het is mogelijk toouse hello Azure Portal tooexecute U-SQL in plaats van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="087de-204">It is possible toouse hello Azure Portal tooexecute U-SQL instead of Visual Studio.</span></span> <span data-ttu-id="087de-205">U kunt toohello Azure Data Lake Analytics-resource op Hallo portal navigeert en het verzenden van query's rechtstreeks als geïllustreerd in de volgende afbeelding Hallo.</span><span class="sxs-lookup"><span data-stu-id="087de-205">You can navigate toohello Azure Data Lake Analytics resource on hello portal and submit queries directly as illustrated in hello following figure.</span></span>
> 
> 

![9](./media/machine-learning-data-science-process-data-lake-walkthrough/9-portal-submit-job.PNG)

### <span data-ttu-id="087de-207"><a name="ingest"></a>Gegevensopname: In van een openbare blob-gegevens lezen</span><span class="sxs-lookup"><span data-stu-id="087de-207"><a name="ingest"></a>Data Ingestion: Read in data from public blob</span></span>
<span data-ttu-id="087de-208">Hallo-locatie van Hallo gegevens in Azure blob Hallo waarnaar wordt verwezen als  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**  en kunnen worden geëxtraheerd met behulp van **Extractors.Csv()**.</span><span class="sxs-lookup"><span data-stu-id="087de-208">hello location of hello data in hello Azure blob is referenced as **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** and can be extracted using **Extractors.Csv()**.</span></span> <span data-ttu-id="087de-209">Vervangen door uw eigen containernaam en opslagaccountnaam in de volgende scripts voor container_name@blob_storage_account_name hello wasb adres.</span><span class="sxs-lookup"><span data-stu-id="087de-209">Substitute your own container name and storage account name in following scripts for container_name@blob_storage_account_name in hello wasb address.</span></span> <span data-ttu-id="087de-210">Aangezien Hallo bestandsnamen in dezelfde indeling zijn, kunnen we gebruiken **reis\_data_ {\*\}CSV** tooread in alle 12 reis-bestanden.</span><span class="sxs-lookup"><span data-stu-id="087de-210">Since hello file names are in same format, we can use **trip\_data_{\*\}.csv** tooread in all 12 trip files.</span></span> 

    ///Read in Trip data
    @trip0 =
        EXTRACT 
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string
    // This is reading 12 trip data from blob
    FROM "wasb://container_name@blob_storage_account_name.blob.core.windows.net/nyctaxitrip/trip_data_{*}.csv"
    USING Extractors.Csv();

<span data-ttu-id="087de-211">Omdat er in de eerste rij Hallo headers, we moet tooremove Hallo headers en kolomtypen wijzigen in de juiste waarden.</span><span class="sxs-lookup"><span data-stu-id="087de-211">Since there are headers in hello first row, we need tooremove hello headers and change column types into appropriate ones.</span></span> <span data-ttu-id="087de-212">We kunnen opslaan Hallo verwerkt gegevens tooAzure Data Lake Storage met **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ of tooAzure Blob storage-account met  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name** .</span><span class="sxs-lookup"><span data-stu-id="087de-212">We can either save hello processed data tooAzure Data Lake Storage using **swebhdfs://data_lake_storage_name.azuredatalakestorage.net/folder_name/file_name**_ or tooAzure Blob storage account using  **wasb://container_name@blob_storage_account_name.blob.core.windows.net/blob_name**.</span></span> 

    // change data types
    @trip =
        SELECT 
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        DateTime.Parse(pickup_datetime) AS pickup_datetime,
        DateTime.Parse(dropoff_datetime) AS dropoff_datetime,
        Int32.Parse(passenger_count) AS passenger_count,
        Double.Parse(trip_time_in_secs) AS trip_time_in_secs,
        Double.Parse(trip_distance) AS trip_distance,
        (pickup_longitude==string.Empty ? 0: float.Parse(pickup_longitude)) AS pickup_longitude,
        (pickup_latitude==string.Empty ? 0: float.Parse(pickup_latitude)) AS pickup_latitude,
        (dropoff_longitude==string.Empty ? 0: float.Parse(dropoff_longitude)) AS dropoff_longitude,
        (dropoff_latitude==string.Empty ? 0: float.Parse(dropoff_latitude)) AS dropoff_latitude
    FROM @trip0
    WHERE medallion != "medallion";

    ////output data tooADL
    OUTPUT @trip   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_trip.csv"
    USING Outputters.Csv(); 

    ////Output data tooblob
    OUTPUT @trip   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_trip.csv"
    USING Outputters.Csv();  

<span data-ttu-id="087de-213">We kunnen op dezelfde manier lezen in Hallo tarief gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="087de-213">Similarly we can read in hello fare data sets.</span></span> <span data-ttu-id="087de-214">Klik met de rechtermuisknop op Azure Data Lake Store, kunt u toolook uw gegevens op **Azure Portal--> Data Explorer** of **Verkenner** vanuit Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="087de-214">Right click Azure Data Lake Store, you can choose toolook at your data in **Azure Portal --> Data Explorer** or **File Explorer** within Visual Studio.</span></span> 

 ![10](./media/machine-learning-data-science-process-data-lake-walkthrough/10-data-in-ADL-VS.PNG)

 ![11](./media/machine-learning-data-science-process-data-lake-walkthrough/11-data-in-ADL.PNG)

### <span data-ttu-id="087de-217"><a name="quality"></a>Data quality controles</span><span class="sxs-lookup"><span data-stu-id="087de-217"><a name="quality"></a>Data quality checks</span></span>
<span data-ttu-id="087de-218">Nadat reis en tarief tabellen zijn gelezen, kunnen data quality controles worden uitgevoerd in de volgende manieren Hallo.</span><span class="sxs-lookup"><span data-stu-id="087de-218">After trip and fare tables have been read in, data quality checks can be done in hello following way.</span></span> <span data-ttu-id="087de-219">Hallo resulterende CSV-bestanden zijn uitvoer tooAzure Blob storage of Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="087de-219">hello resulting CSV files can be output tooAzure Blob storage or Azure Data Lake Store.</span></span> 

<span data-ttu-id="087de-220">Hallo aantal medallions en uniek aantal medallions vinden:</span><span class="sxs-lookup"><span data-stu-id="087de-220">Find hello number of medallions and unique number of medallions:</span></span>

    ///check hello number of medallions and unique number of medallions
    @trip2 =
        SELECT
        medallion,
        vendor_id,
        pickup_datetime.Month AS pickup_month
        FROM @trip;

    @ex_1 =
        SELECT
        pickup_month, 
        COUNT(medallion) AS cnt_medallion,
        COUNT(DISTINCT(medallion)) AS unique_medallion
        FROM @trip2
        GROUP BY pickup_month;
        OUTPUT @ex_1   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_1.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="087de-221">Deze medallions waarop meer dan 100 reizen vinden:</span><span class="sxs-lookup"><span data-stu-id="087de-221">Find those medallions that had more than 100 trips:</span></span>

    ///find those medallions that had more than 100 trips
    @ex_2 =
        SELECT medallion,
               COUNT(medallion) AS cnt_medallion
        FROM @trip2
        //where pickup_datetime >= "2013-01-01t00:00:00.0000000" and pickup_datetime <= "2013-04-01t00:00:00.0000000"
        GROUP BY medallion
        HAVING COUNT(medallion) > 100;
        OUTPUT @ex_2   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_2.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="087de-222">Ongeldige records in termen van pickup_longitude vinden:</span><span class="sxs-lookup"><span data-stu-id="087de-222">Find those invalid records in terms of pickup_longitude:</span></span>

    ///find those invalid records in terms of pickup_longitude
    @ex_3 =
        SELECT COUNT(medallion) AS cnt_invalid_pickup_longitude
        FROM @trip
        WHERE
        pickup_longitude <- 90 OR pickup_longitude > 90;
        OUTPUT @ex_3   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_3.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="087de-223">Ontbrekende waarden vinden voor sommige variabelen:</span><span class="sxs-lookup"><span data-stu-id="087de-223">Find missing values for some variables:</span></span>

    //check missing values
    @res =
        SELECT *,
               (medallion == null? 1 : 0) AS missing_medallion
        FROM @trip;

    @trip_summary6 =
        SELECT 
            vendor_id,
        SUM(missing_medallion) AS medallion_empty, 
        COUNT(medallion) AS medallion_total,
        COUNT(DISTINCT(medallion)) AS medallion_total_unique  
        FROM @res
        GROUP BY vendor_id;
    OUTPUT @trip_summary6
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_16.csv"
    USING Outputters.Csv();



### <span data-ttu-id="087de-224"><a name="explore"></a>Gegevensverkenning</span><span class="sxs-lookup"><span data-stu-id="087de-224"><a name="explore"></a>Data exploration</span></span>
<span data-ttu-id="087de-225">Kan doen we enkele gegevens verkenning tooget beter inzicht te krijgen van Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="087de-225">We can do some data exploration tooget a better understanding of hello data.</span></span>

<span data-ttu-id="087de-226">Hallo-distributie van reizen Gekantelde en punt niet vinden:</span><span class="sxs-lookup"><span data-stu-id="087de-226">Find hello distribution of tipped and non-tipped trips:</span></span>

    ///tipped vs. not tipped distribution
    @tip_or_not =
        SELECT *,
               (tip_amount > 0 ? 1: 0) AS tipped
        FROM @fare;

    @ex_4 =
        SELECT tipped,
               COUNT(*) AS tip_freq
        FROM @tip_or_not
        GROUP BY tipped;
        OUTPUT @ex_4   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_4.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="087de-227">Hallo-distributie van tip bedrag met afgekapte waarden vinden: 0,5,10 en 20 bedragen.</span><span class="sxs-lookup"><span data-stu-id="087de-227">Find hello distribution of tip amount with cut-off values: 0,5,10,and 20 dollars.</span></span>

    //tip class/range distribution
    @tip_class =
        SELECT *,
               (tip_amount >20? 4: (tip_amount >10? 3:(tip_amount >5 ? 2:(tip_amount > 0 ? 1: 0)))) AS tip_class
        FROM @fare;
    @ex_5 =
        SELECT tip_class,
               COUNT(*) AS tip_freq
        FROM @tip_class
        GROUP BY tip_class;
        OUTPUT @ex_5   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_5.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="087de-228">Elementaire statistische gegevens van reis afstand vinden:</span><span class="sxs-lookup"><span data-stu-id="087de-228">Find basic statistics of trip distance:</span></span>

    // find basic statistics for trip_distance
    @trip_summary4 =
        SELECT 
            vendor_id,
            COUNT(*) AS cnt_row,
            MIN(trip_distance) AS min_trip_distance,
            MAX(trip_distance) AS max_trip_distance,
            AVG(trip_distance) AS avg_trip_distance 
        FROM @trip
        GROUP BY vendor_id;
    OUTPUT @trip_summary4
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_14.csv"
    USING Outputters.Csv();

<span data-ttu-id="087de-229">Hallo percentielen van reis afstand vinden:</span><span class="sxs-lookup"><span data-stu-id="087de-229">Find hello percentiles of trip distance:</span></span>

    // find percentiles of trip_distance
    @trip_summary3 =
        SELECT DISTINCT vendor_id AS vendor,
                        PERCENTILE_DISC(0.25) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.5) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc,
                        PERCENTILE_DISC(0.75) WITHIN GROUP(ORDER BY trip_distance) OVER(PARTITION BY vendor_id) AS median_trip_distance_disc
        FROM @trip;
       // group by vendor_id;
    OUTPUT @trip_summary3
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_13.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="087de-230"><a name="join"></a>Tabellen reis en tarief samenvoegen</span><span class="sxs-lookup"><span data-stu-id="087de-230"><a name="join"></a>Join trip and fare tables</span></span>
<span data-ttu-id="087de-231">Reis en tarief tabellen kunnen worden gekoppeld door straten, hack_license en pickup_time.</span><span class="sxs-lookup"><span data-stu-id="087de-231">Trip and fare tables can be joined by medallion, hack_license, and pickup_time.</span></span>

    //join trip and fare table

    @model_data_full =
    SELECT t.*, 
    f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,  f.total_amount, f.tip_amount,
    (f.tip_amount > 0 ? 1: 0) AS tipped,
    (f.tip_amount >20? 4: (f.tip_amount >10? 3:(f.tip_amount >5 ? 2:(f.tip_amount > 0 ? 1: 0)))) AS tip_class
    FROM @trip AS t JOIN  @fare AS f
    ON   (t.medallion == f.medallion AND t.hack_license == f.hack_license AND t.pickup_datetime == f.pickup_datetime)
    WHERE   (pickup_longitude != 0 AND dropoff_longitude != 0 );

    //// output tooblob
    OUTPUT @model_data_full   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 

    ////output data tooADL
    OUTPUT @model_data_full   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_7_full_data.csv"
    USING Outputters.Csv(); 


<span data-ttu-id="087de-232">Voor elk niveau van het aantal passagiers Hallo aantal records, gemiddelde tip bedrag, afwijking van tip bedrag, percentage Gekantelde heen te berekenen.</span><span class="sxs-lookup"><span data-stu-id="087de-232">For each level of passenger count, calculate hello number of records, average tip amount, variance of tip amount, percentage of tipped trips.</span></span>

    // contigency table
    @trip_summary8 =
        SELECT passenger_count,
               COUNT(*) AS cnt,
               AVG(tip_amount) AS avg_tip_amount,
               VAR(tip_amount) AS var_tip_amount,
               SUM(tipped) AS cnt_tipped,
               (float)SUM(tipped)/COUNT(*) AS pct_tipped
        FROM @model_data_full
        GROUP BY passenger_count;
        OUTPUT @trip_summary8
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_17.csv"
    USING Outputters.Csv();


### <span data-ttu-id="087de-233"><a name="sample"></a>Gegevens steekproeven</span><span class="sxs-lookup"><span data-stu-id="087de-233"><a name="sample"></a>Data sampling</span></span>
<span data-ttu-id="087de-234">Eerst wordt willekeurig selecteren 0,1% Hallo gegevens uit de gekoppelde tabel Hallo:</span><span class="sxs-lookup"><span data-stu-id="087de-234">First we randomly select 0.1% of hello data from hello joined table:</span></span>

    //random select 1/1000 data for modeling purpose
    @addrownumberres_randomsample =
    SELECT *,
            ROW_NUMBER() OVER() AS rownum
    FROM @model_data_full;

    @model_data_random_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_randomsample
    WHERE rownum % 1000 == 0;

    OUTPUT @model_data_random_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_7_random_1_1000.csv"
    USING Outputters.Csv(); 

<span data-ttu-id="087de-235">We doen vervolgens steekproeven toepassing stratificatie door binaire variabele tip_class:</span><span class="sxs-lookup"><span data-stu-id="087de-235">Then we do stratified sampling by binary variable tip_class:</span></span>

    //stratified random select 1/1000 data for modeling purpose
    @addrownumberres_stratifiedsample =
    SELECT *,
            ROW_NUMBER() OVER(PARTITION BY tip_class) AS rownum
    FROM @model_data_full;

    @model_data_stratified_sample_1_1000 =
    SELECT *
    FROM @addrownumberres_stratifiedsample
    WHERE rownum % 1000 == 0;
    //// output tooblob
    OUTPUT @model_data_stratified_sample_1_1000   
    too"wasb://container_name@blob_storage_account_name.blob.core.windows.net/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 
    ////output data tooADL
    OUTPUT @model_data_stratified_sample_1_1000   
    too"swebhdfs://data_lake_storage_name.azuredatalakestore.net/nyctaxi_folder/demo_ex_9_stratified_1_1000.csv"
    USING Outputters.Csv(); 


### <span data-ttu-id="087de-236"><a name="run"></a>U-SQL-taken uitvoeren</span><span class="sxs-lookup"><span data-stu-id="087de-236"><a name="run"></a>Run U-SQL jobs</span></span>
<span data-ttu-id="087de-237">Wanneer u klaar bent U-SQL-scripts, kunt u deze met uw Azure Data Lake Analytics-account toohello-server verzenden.</span><span class="sxs-lookup"><span data-stu-id="087de-237">When you finish editing U-SQL scripts, you can submit them toohello server using your Azure Data Lake Analytics account.</span></span> <span data-ttu-id="087de-238">Klik op **Data Lake**, **Submit Job**, selecteer uw **Analytics-Account**, kies **parallelle uitvoering**, en klik op **verzenden**  knop.</span><span class="sxs-lookup"><span data-stu-id="087de-238">Click **Data Lake**, **Submit Job**, select your **Analytics Account**, choose **Parallelism**, and click **Submit** button.</span></span>  

 ![12](./media/machine-learning-data-science-process-data-lake-walkthrough/12-submit-USQL.PNG)

<span data-ttu-id="087de-240">Wanneer het Hallo-taak met succes is voldaan, wordt Hallo status van de taak weergegeven in Visual Studio voor bewaking.</span><span class="sxs-lookup"><span data-stu-id="087de-240">When hello job is complied successfully, hello status of your job will be displayed in Visual Studio for monitoring.</span></span> <span data-ttu-id="087de-241">Nadat het Hallo-taak is voltooid, kunt u zelfs replay Hallo taak uitvoeringsproces en uitzoeken Hallo bottleneck stappen tooimprove de efficiëntie van uw taak.</span><span class="sxs-lookup"><span data-stu-id="087de-241">After hello job finishes running, you can even replay hello job execution process and find out hello bottleneck steps tooimprove your job efficiency.</span></span> <span data-ttu-id="087de-242">U kunt ook gaan tooAzure Portal toocheck Hallo status van uw U-SQL-taken.</span><span class="sxs-lookup"><span data-stu-id="087de-242">You can also go tooAzure Portal toocheck hello status of your U-SQL jobs.</span></span>

 ![13](./media/machine-learning-data-science-process-data-lake-walkthrough/13-USQL-running-v2.PNG)

 ![14](./media/machine-learning-data-science-process-data-lake-walkthrough/14-USQL-jobs-portal.PNG)

<span data-ttu-id="087de-245">U kunt nu de uitvoerbestanden Hallo in Azure Blob storage of Azure Portal controleren.</span><span class="sxs-lookup"><span data-stu-id="087de-245">Now you can check hello output files in either Azure Blob storage or Azure Portal.</span></span> <span data-ttu-id="087de-246">We gebruiken de voorbeeldgegevens Hallo toepassing stratificatie voor onze modelleren in de volgende stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="087de-246">We will use hello stratified sample data for our modeling in hello next step.</span></span>

 ![15](./media/machine-learning-data-science-process-data-lake-walkthrough/15-U-SQL-output-csv.PNG)

 ![16](./media/machine-learning-data-science-process-data-lake-walkthrough/16-U-SQL-output-csv-portal.PNG)

## <a name="build-and-deploy-models-in-azure-machine-learning"></a><span data-ttu-id="087de-249">Bouwen en implementeren van modellen in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="087de-249">Build and deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="087de-250">Ziet u twee opties die beschikbaar zijn voor uw toopull gegevens in Azure Machine Learning toobuild en</span><span class="sxs-lookup"><span data-stu-id="087de-250">We demonstrate two options available for you toopull data into Azure Machine Learning toobuild and</span></span> 

* <span data-ttu-id="087de-251">In de eerste optie Hallo, gebruikt u Hallo door actieve gegevens die is geschreven tooan Azure-Blob (in Hallo **gegevens steekproeven** bovenstaande stap) en gebruik van Python toobuild en modellen van Azure Machine Learning implementeren.</span><span class="sxs-lookup"><span data-stu-id="087de-251">In hello first option, you use hello sampled data that has been written tooan Azure Blob (in hello **Data sampling** step above) and use Python toobuild and deploy models from Azure Machine Learning.</span></span> 
* <span data-ttu-id="087de-252">In de tweede optie Hallo kunt u een query Hallo-gegevens in Azure Data Lake rechtstreeks met behulp van een Hive-query.</span><span class="sxs-lookup"><span data-stu-id="087de-252">In hello second option, you query hello data in Azure Data Lake directly using a Hive query.</span></span> <span data-ttu-id="087de-253">Deze optie vereist dat u een nieuwe HDInsight-cluster maken, of gebruik een bestaand HDInsight-cluster waar Hallo Hive punt toohello NY Taxi gegevens in Azure Data Lake Storage-tabellen.</span><span class="sxs-lookup"><span data-stu-id="087de-253">This option requires that you create a new HDInsight cluster or use an existing HDInsight cluster where hello Hive tables point toohello NY Taxi data in Azure Data Lake Storage.</span></span>  <span data-ttu-id="087de-254">Beide deze opties hieronder besproken.</span><span class="sxs-lookup"><span data-stu-id="087de-254">We discuss both these options below.</span></span> 

## <a name="option-1-use-python-toobuild-and-deploy-machine-learning-models"></a><span data-ttu-id="087de-255">Optie 1: Gebruik Python toobuild en machine learning-modellen implementeren</span><span class="sxs-lookup"><span data-stu-id="087de-255">Option 1: Use Python toobuild and deploy machine learning models</span></span>
<span data-ttu-id="087de-256">toobuild en implementeren van machine learning-modellen met behulp van Python, een Jupyter-Notebook maken op uw lokale computer of in Azure Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="087de-256">toobuild and deploy machine learning models using Python, create a Jupyter Notebook on your local machine or in Azure Machine Learning Studio.</span></span> <span data-ttu-id="087de-257">Hallo Jupyter-Notebook opgegeven op [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) bevat volledige code tooexplore Hallo, visualiseren van gegevens, functie-engineering, modellering en implementatie.</span><span class="sxs-lookup"><span data-stu-id="087de-257">hello Jupyter Notebook  provided on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/AzureDataLakeWalkthrough) contains hello full code tooexplore, visualize data, feature engineering, modeling and deployment.</span></span> <span data-ttu-id="087de-258">In dit artikel, laten we zien alleen Hallo modelleren en implementatie.</span><span class="sxs-lookup"><span data-stu-id="087de-258">In this article, we show just hello modeling and deployment.</span></span> 

### <a name="import-python-libraries"></a><span data-ttu-id="087de-259">Python-bibliotheken importeren</span><span class="sxs-lookup"><span data-stu-id="087de-259">Import Python libraries</span></span>
<span data-ttu-id="087de-260">In de volgorde toorun Hallo steekproef Jupyter-Notebook of Python-scriptbestand Hallo, hello volgende Python pakketten zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="087de-260">In order toorun hello sample Jupyter Notebook or hello Python script file, hello following Python packages are needed.</span></span> <span data-ttu-id="087de-261">Als u Hallo service van AzureML-Notebook gebruikt, zijn deze pakketten vooraf worden geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="087de-261">If you are using hello AzureML Notebook service, these packages have been pre-installed.</span></span>

    import pandas as pd
    from pandas import Series, DataFrame
    import numpy as np
    import matplotlib.pyplot as plt
    from time import time
    import pyodbc
    import os
    from azure.storage.blob import BlobService
    import tables
    import time
    import zipfile
    import random
    import sklearn
    from sklearn.linear_model import LogisticRegression
    from sklearn.cross_validation import train_test_split
    from sklearn import metrics
    from __future__ import division
    from sklearn import linear_model
    from azureml import services


### <a name="read-in-hello-data-from-blob"></a><span data-ttu-id="087de-262">Lees in Hallo gegevens uit blob</span><span class="sxs-lookup"><span data-stu-id="087de-262">Read in hello data from blob</span></span>
* <span data-ttu-id="087de-263">Verbindingsreeks</span><span class="sxs-lookup"><span data-stu-id="087de-263">Connection String</span></span>   
  
        CONTAINERNAME = 'test1'
        STORAGEACCOUNTNAME = 'XXXXXXXXX'
        STORAGEACCOUNTKEY = 'YYYYYYYYYYYYYYYYYYYYYYYYYYYY'
        BLOBNAME = 'demo_ex_9_stratified_1_1000_copy.csv'
        blob_service = BlobService(account_name=STORAGEACCOUNTNAME,account_key=STORAGEACCOUNTKEY)
* <span data-ttu-id="087de-264">Lees in als tekst</span><span class="sxs-lookup"><span data-stu-id="087de-264">Read in as text</span></span>
  
        t1 = time.time()
        data = blob_service.get_blob_to_text(CONTAINERNAME,BLOBNAME).split("\n")
        t2 = time.time()
        print(("It takes %s seconds tooread in "+BLOBNAME) % (t2 - t1))
  
  ![17](./media/machine-learning-data-science-process-data-lake-walkthrough/17-python_readin_csv.PNG)    
* <span data-ttu-id="087de-266">Toevoegen van kolomnamen en afzonderlijke kolommen</span><span class="sxs-lookup"><span data-stu-id="087de-266">Add column names and separate columns</span></span>
  
        colnames = ['medallion','hack_license','vendor_id','rate_code','store_and_fwd_flag','pickup_datetime','dropoff_datetime',
        'passenger_count','trip_time_in_secs','trip_distance','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'payment_type', 'fare_amount', 'surcharge', 'mta_tax', 'tolls_amount',  'total_amount', 'tip_amount', 'tipped', 'tip_class', 'rownum']
        df1 = pd.DataFrame([sub.split(",") for sub in data], columns = colnames)
* <span data-ttu-id="087de-267">Sommige kolommen toonumeric wijzigen</span><span class="sxs-lookup"><span data-stu-id="087de-267">Change some columns toonumeric</span></span>
  
        cols_2_float = ['trip_time_in_secs','pickup_longitude','pickup_latitude','dropoff_longitude','dropoff_latitude',
        'fare_amount', 'surcharge','mta_tax','tolls_amount','total_amount','tip_amount', 'passenger_count','trip_distance'
        ,'tipped','tip_class','rownum']
        for col in cols_2_float:
            df1[col] = df1[col].astype(float)

### <a name="build-machine-learning-models"></a><span data-ttu-id="087de-268">Machine learning-modellen maken</span><span class="sxs-lookup"><span data-stu-id="087de-268">Build machine learning models</span></span>
<span data-ttu-id="087de-269">Hier maken we een model binaire classificatie toopredict of een zakenreis is punt of niet.</span><span class="sxs-lookup"><span data-stu-id="087de-269">Here we build a binary classification model toopredict whether a trip is tipped or not.</span></span> <span data-ttu-id="087de-270">Hallo Jupyter-Notebook kunt u andere twee modellen: multiklassen classificatie en regressie-modellen.</span><span class="sxs-lookup"><span data-stu-id="087de-270">In hello Jupyter Notebook you can find other two models: multiclass classification, and regression models.</span></span>

* <span data-ttu-id="087de-271">Eerst moet u toocreate dummy-variabelen die kunnen worden gebruikt in scikit-modellen meer</span><span class="sxs-lookup"><span data-stu-id="087de-271">First we need toocreate dummy variables that can be used in scikit-learn models</span></span>
  
        df1_payment_type_dummy = pd.get_dummies(df1['payment_type'], prefix='payment_type_dummy')
        df1_vendor_id_dummy = pd.get_dummies(df1['vendor_id'], prefix='vendor_id_dummy')
* <span data-ttu-id="087de-272">Gegevens kader voor Hallo model maken</span><span class="sxs-lookup"><span data-stu-id="087de-272">Create data frame for hello modeling</span></span>
  
        cols_to_keep = ['tipped', 'trip_distance', 'passenger_count']
        data = df1[cols_to_keep].join([df1_payment_type_dummy,df1_vendor_id_dummy])
  
        X = data.iloc[:,1:]
        Y = data.tipped
* <span data-ttu-id="087de-273">Trainings- en testdoeleinden 60 40 splitsen</span><span class="sxs-lookup"><span data-stu-id="087de-273">Training and testing 60-40 split</span></span>
  
        X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.4, random_state=0)
* <span data-ttu-id="087de-274">Logistic Regression in trainingset</span><span class="sxs-lookup"><span data-stu-id="087de-274">Logistic Regression in training set</span></span>
  
        model = LogisticRegression()
        logit_fit = model.fit(X_train, Y_train)
        print ('Coefficients: \n', logit_fit.coef_)
        Y_train_pred = logit_fit.predict(X_train)
  
       ![c1](./media/machine-learning-data-science-process-data-lake-walkthrough/c1-py-logit-coefficient.PNG)
* <span data-ttu-id="087de-275">Score testen gegevensset</span><span class="sxs-lookup"><span data-stu-id="087de-275">Score testing data set</span></span>
  
        Y_test_pred = logit_fit.predict(X_test)
* <span data-ttu-id="087de-276">Evaluatie van metrische gegevens berekenen</span><span class="sxs-lookup"><span data-stu-id="087de-276">Calculate Evaluation metrics</span></span>
  
        fpr_train, tpr_train, thresholds_train = metrics.roc_curve(Y_train, Y_train_pred)
        print fpr_train, tpr_train, thresholds_train
  
        fpr_test, tpr_test, thresholds_test = metrics.roc_curve(Y_test, Y_test_pred) 
        print fpr_test, tpr_test, thresholds_test
  
        #AUC
        print metrics.auc(fpr_train,tpr_train)
        print metrics.auc(fpr_test,tpr_test)
  
        #Confusion Matrix
        print metrics.confusion_matrix(Y_train,Y_train_pred)
        print metrics.confusion_matrix(Y_test,Y_test_pred)
  
       ![c2](./media/machine-learning-data-science-process-data-lake-walkthrough/c2-py-logit-evaluation.PNG)

### <a name="build-web-service-api-and-consume-it-in-python"></a><span data-ttu-id="087de-277">API-webservice bouwen en deze wordt gebruikt in Python</span><span class="sxs-lookup"><span data-stu-id="087de-277">Build Web Service API and consume it in Python</span></span>
<span data-ttu-id="087de-278">We willen toooperationalize Hallo machine learning-model nadat deze is opgebouwd.</span><span class="sxs-lookup"><span data-stu-id="087de-278">We want toooperationalize hello machine learning model after it has been built.</span></span> <span data-ttu-id="087de-279">We gebruiken hier Hallo binaire logistic model als voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="087de-279">Here we use hello binary logistic model as an example.</span></span> <span data-ttu-id="087de-280">Zorg ervoor dat Hallo scikit-versie in uw lokale machine is 0.15.1 meer.</span><span class="sxs-lookup"><span data-stu-id="087de-280">Make sure hello scikit-learn version in your local machine is 0.15.1.</span></span> <span data-ttu-id="087de-281">U hebt geen tooworry over deze als u Azure ML studio service gebruiken.</span><span class="sxs-lookup"><span data-stu-id="087de-281">You don't have tooworry about this if you use Azure ML studio service.</span></span>

* <span data-ttu-id="087de-282">Uw werkruimte-referenties uit de instellingen voor Azure ML studio vinden.</span><span class="sxs-lookup"><span data-stu-id="087de-282">Find your workspace credentials from Azure ML studio settings.</span></span> <span data-ttu-id="087de-283">Klik op in Azure Machine Learning Studio **instellingen** --> **naam** --> **autorisatie Tokens**.</span><span class="sxs-lookup"><span data-stu-id="087de-283">In Azure Machine Learning Studio, click **Settings** --> **Name** --> **Authorization Tokens**.</span></span> 
  
    ![C3](./media/machine-learning-data-science-process-data-lake-walkthrough/c3-workspace-id.PNG)

        workspaceid = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'
        auth_token = 'xxxxxxxxxxxxxxxxxxxxxxxxxxx'

* <span data-ttu-id="087de-285">Web-Service maken</span><span class="sxs-lookup"><span data-stu-id="087de-285">Create Web Service</span></span>
  
        @services.publish(workspaceid, auth_token) 
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float, payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(int) #0, or 1
        def predictNYCTAXI(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            inputArray = [trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH, payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS]
            return logit_fit.predict(inputArray)
* <span data-ttu-id="087de-286">Web Servicereferenties ophalen</span><span class="sxs-lookup"><span data-stu-id="087de-286">Get web service credentials</span></span>
  
        url = predictNYCTAXI.service.url
        api_key =  predictNYCTAXI.service.api_key
  
        print url
        print api_key
  
        @services.service(url, api_key)
        @services.types(trip_distance = float, passenger_count = float, payment_type_dummy_CRD = float, payment_type_dummy_CSH=float,payment_type_dummy_DIS = float, payment_type_dummy_NOC = float, payment_type_dummy_UNK = float, vendor_id_dummy_CMT = float, vendor_id_dummy_VTS = float)
        @services.returns(float)
        def NYCTAXIPredictor(trip_distance, passenger_count, payment_type_dummy_CRD, payment_type_dummy_CSH,payment_type_dummy_DIS, payment_type_dummy_NOC, payment_type_dummy_UNK, vendor_id_dummy_CMT, vendor_id_dummy_VTS ):
            pass
* <span data-ttu-id="087de-287">Web service API-aanroep.</span><span class="sxs-lookup"><span data-stu-id="087de-287">Call Web service API.</span></span> <span data-ttu-id="087de-288">U hebt toowait 5 tot 10 seconden na de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="087de-288">You have toowait 5-10 seconds after hello previous step.</span></span>
  
        NYCTAXIPredictor(1,2,1,0,0,0,0,0,1)
  
       ![c4](./media/machine-learning-data-science-process-data-lake-walkthrough/c4-call-API.PNG)

## <a name="option-2-create-and-deploy-models-directly-in-azure-machine-learning"></a><span data-ttu-id="087de-289">Optie 2: Maken en implementeren van modellen rechtstreeks in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="087de-289">Option 2: Create and deploy models directly in Azure Machine Learning</span></span>
<span data-ttu-id="087de-290">Azure Machine Learning Studio kunt lezen van gegevens rechtstreeks vanuit de Azure Data Lake Store en vervolgens worden gebruikte toocreate en implementeren van modellen.</span><span class="sxs-lookup"><span data-stu-id="087de-290">Azure Machine Learning Studio can read data directly from Azure Data Lake Store and then be used toocreate and deploy models.</span></span> <span data-ttu-id="087de-291">Deze methode maakt gebruik van een Hive-tabel verwijst op Hallo Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="087de-291">This approach uses a Hive table that points at hello Azure Data Lake Store.</span></span> <span data-ttu-id="087de-292">Dit vereist dat een aparte Azure HDInsight-cluster worden ingericht, op welke Hallo Hive tabel is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="087de-292">This requires that a separate Azure HDInsight cluster be provisioned, on which hello Hive table is created.</span></span> <span data-ttu-id="087de-293">Hallo van de volgende secties tonen hoe toodo dit.</span><span class="sxs-lookup"><span data-stu-id="087de-293">hello following sections show how toodo this.</span></span> 

### <a name="create-an-hdinsight-linux-cluster"></a><span data-ttu-id="087de-294">Een HDInsight Linux-Cluster maken</span><span class="sxs-lookup"><span data-stu-id="087de-294">Create an HDInsight Linux Cluster</span></span>
<span data-ttu-id="087de-295">Maken van een HDInsight-Cluster (Linux) van Hallo [Azure Portal](http://portal.azure.com). Zie voor meer informatie, Hallo **maken van een HDInsight-cluster met toegang tooAzure Data Lake Store** in sectie [een HDInsight-cluster maken met Data Lake Store met Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="087de-295">Create an HDInsight Cluster (Linux) from hello [Azure Portal](http://portal.azure.com).For details, see hello **Create an HDInsight cluster with access tooAzure Data Lake Store** section in [Create an HDInsight cluster with Data Lake Store using Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

 ![18](./media/machine-learning-data-science-process-data-lake-walkthrough/18-create_HDI_cluster.PNG)

### <a name="create-hive-table-in-hdinsight"></a><span data-ttu-id="087de-297">Hive-tabel maken in HDInsight</span><span class="sxs-lookup"><span data-stu-id="087de-297">Create Hive table in HDInsight</span></span>
<span data-ttu-id="087de-298">We maken nu Hive-tabellen toobe gebruikt in Azure Machine Learning Studio in Hallo HDInsight-cluster met behulp van Hallo-gegevens in de vorige stap Hallo opgeslagen in Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="087de-298">Now we create Hive tables toobe used in Azure Machine Learning Studio in hello HDInsight cluster using hello data stored in Azure Data Lake Store in hello previous step.</span></span> <span data-ttu-id="087de-299">Ga toohello HDInsight-cluster zojuist hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="087de-299">Go toohello HDInsight cluster just created.</span></span> <span data-ttu-id="087de-300">Klik op **instellingen** --> **eigenschappen** --> **Cluster AAD-identiteit** --> **ADLS-toegang**, Zorg dat uw Azure Data Lake Store-account is toegevoegd in de lijst Hallo met lezen, schrijven en uitvoeren van rechten.</span><span class="sxs-lookup"><span data-stu-id="087de-300">Click **Settings** --> **Properties** --> **Cluster AAD Identity** --> **ADLS Access**, make sure your Azure Data Lake Store account is added in hello list with read, write and execute rights.</span></span> 

 ![19](./media/machine-learning-data-science-process-data-lake-walkthrough/19-HDI-cluster-add-ADLS.PNG)

<span data-ttu-id="087de-302">Klik vervolgens op **Dashboard** volgende toohello **instellingen** knop en een venster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="087de-302">Then click **Dashboard** next toohello **Settings** button and a window will pop up.</span></span> <span data-ttu-id="087de-303">Klik op **Hive-weergave** rechtsboven Hallo pagina en u ziet in Hallo Hallo **Query-Editor**.</span><span class="sxs-lookup"><span data-stu-id="087de-303">Click **Hive View** in hello upper right corner of hello page and you will see hello **Query Editor**.</span></span>

 ![20](./media/machine-learning-data-science-process-data-lake-walkthrough/20-HDI-dashboard.PNG)

 ![21](./media/machine-learning-data-science-process-data-lake-walkthrough/21-Hive-Query-Editor-v2.PNG)

<span data-ttu-id="087de-306">Een tabel in de volgende Hive scripts toocreate Hallo plakken.</span><span class="sxs-lookup"><span data-stu-id="087de-306">Paste in hello following Hive scripts toocreate a table.</span></span> <span data-ttu-id="087de-307">Hallo-locatie van de gegevensbron is in Azure Data Lake Store-documentatie op deze manier: **adl://data_lake_store_name.azuredatalakestore.net:443/mapnaam/bestandsnaam**.</span><span class="sxs-lookup"><span data-stu-id="087de-307">hello location of data source is in Azure Data Lake Store reference in this way: **adl://data_lake_store_name.azuredatalakestore.net:443/folder_name/file_name**.</span></span>

    CREATE EXTERNAL TABLE nyc_stratified_sample
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count string,
        trip_time_in_secs string,
        trip_distance string,
        pickup_longitude string,
        pickup_latitude string,
        dropoff_longitude string,
        dropoff_latitude string,
      payment_type string,
      fare_amount string,
      surcharge string,
      mta_tax string,
      tolls_amount string,
      total_amount string,
      tip_amount string,
      tipped string,
      tip_class string,
      rownum string
      )
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    LOCATION 'adl://data_lake_storage_name.azuredatalakestore.net:443/nyctaxi_folder/demo_ex_9_stratified_1_1000_copy.csv';


<span data-ttu-id="087de-308">Wanneer het Hallo-query is voltooid, ziet u Hallo resultaten als volgt:</span><span class="sxs-lookup"><span data-stu-id="087de-308">When hello query finishes running, you will see hello results like this:</span></span>

 ![22](./media/machine-learning-data-science-process-data-lake-walkthrough/22-Hive-Query-results.PNG)

### <a name="build-and-deploy-models-in-azure-machine-learning-studio"></a><span data-ttu-id="087de-310">Bouwen en implementeren van modellen in Azure Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="087de-310">Build and deploy models in Azure Machine Learning Studio</span></span>
<span data-ttu-id="087de-311">We zijn nu gereed toobuild en implementeren van een model dat voorspelt al dan niet een tip met Azure Machine Learning wordt betaald.</span><span class="sxs-lookup"><span data-stu-id="087de-311">We are now ready toobuild and deploy a model that predicts whether or not a tip is paid with Azure Machine Learning.</span></span> <span data-ttu-id="087de-312">Hallo toepassing stratificatie voorbeeldgegevens is gereed toobe gebruikt in deze binaire classificatie (tip of niet) probleem.</span><span class="sxs-lookup"><span data-stu-id="087de-312">hello stratified sample data is ready toobe used in this binary classification (tip or not) problem.</span></span> <span data-ttu-id="087de-313">Hallo voorspellende modellen met multiklassen classificatie (tip_class) en regressie (tip_amount) kan ook worden gemaakt en geïmplementeerd met Azure Machine Learning Studio maar hier alleen wordt gedemonstreerd hoe toohandle Hallo case met behulp van Hallo binaire classificatie model.</span><span class="sxs-lookup"><span data-stu-id="087de-313">hello predictive models using multiclass classification (tip_class) and regression (tip_amount) can also be built and deployed with Azure Machine Learning Studio, but here we only show how toohandle hello case using hello binary classification model.</span></span>

1. <span data-ttu-id="087de-314">Hallo-gegevens ophalen voor Azure ML Hallo met **importgegevens** module beschikbaar in Hallo **gegevensinvoer en uitvoer** sectie.</span><span class="sxs-lookup"><span data-stu-id="087de-314">Get hello data into Azure ML using hello **Import Data** module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="087de-315">Zie voor meer informatie, Hallo [gegevens importeren-module](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) -verwijzingspagina.</span><span class="sxs-lookup"><span data-stu-id="087de-315">For more information, see hello [Import Data module](https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/) reference page.</span></span>
2. <span data-ttu-id="087de-316">Selecteer **Hive-Query** als Hallo **gegevensbron** in Hallo **eigenschappen** Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="087de-316">Select **Hive Query** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="087de-317">Plakken Hallo volgende Hive-script in Hallo **Hive databasequery** editor</span><span class="sxs-lookup"><span data-stu-id="087de-317">Paste hello following Hive script in hello **Hive database query** editor</span></span>
   
        select * from nyc_stratified_sample;
4. <span data-ttu-id="087de-318">Voer Hallo URI van HDInsight-cluster (dit vindt u in Azure Portal), Hadoop-referenties, de locatie van uitvoergegevens en Azure storage-accountnaam naam/sleutelcontainer.</span><span class="sxs-lookup"><span data-stu-id="087de-318">Enter hello URI of HDInsight cluster (this can be found in Azure Portal), Hadoop credentials, location of output data, and Azure storage account name/key/container name.</span></span>
   
   ![23](./media/machine-learning-data-science-process-data-lake-walkthrough/23-reader-module-v3.PNG)  

<span data-ttu-id="087de-320">Een voorbeeld van een binaire indeling experiment lezen van gegevens van Hive-tabel wordt weergegeven in onderstaande afbeelding ziet Hallo.</span><span class="sxs-lookup"><span data-stu-id="087de-320">An example of a binary classification experiment reading data from Hive table is shown in hello figure below.</span></span>

 ![24](./media/machine-learning-data-science-process-data-lake-walkthrough/24-AML-exp.PNG)

<span data-ttu-id="087de-322">Nadat het Hallo-experiment is gemaakt, klikt u op **webservice ingesteld** --> **Predictive-webservice**</span><span class="sxs-lookup"><span data-stu-id="087de-322">After hello experiment is created, click  **Set Up Web Service** --> **Predictive Web Service**</span></span>

 ![25](./media/machine-learning-data-science-process-data-lake-walkthrough/25-AML-exp-deploy.PNG)

<span data-ttu-id="087de-324">Voer Hallo automatisch gemaakt score berekenen experiment, wanneer deze is voltooid, klikt u op **Web Service implementeren**</span><span class="sxs-lookup"><span data-stu-id="087de-324">Run hello automatically created scoring experiment, when it finishes, click **Deploy Web Service**</span></span>

 ![26](./media/machine-learning-data-science-process-data-lake-walkthrough/26-AML-exp-deploy-web.PNG)

<span data-ttu-id="087de-326">Hallo web servicedashboard wordt kort weergegeven:</span><span class="sxs-lookup"><span data-stu-id="087de-326">hello web service dashboard will be displayed shortly:</span></span>

 ![27](./media/machine-learning-data-science-process-data-lake-walkthrough/27-AML-web-api.PNG)

## <a name="summary"></a><span data-ttu-id="087de-328">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="087de-328">Summary</span></span>
<span data-ttu-id="087de-329">U kunt een omgeving met wetenschappelijke gegevens voor het bouwen van schaalbare end-to-end-oplossingen in Azure Data Lake hebt gemaakt door de procedure is voltooid.</span><span class="sxs-lookup"><span data-stu-id="087de-329">By completing this walkthrough you have created a data science environment for building scalable end-to-end solutions in Azure Data Lake.</span></span> <span data-ttu-id="087de-330">Deze omgeving is gebruikte tooanalyze een grote openbare gegevensset, duurt deze stappen Hallo canonieke Hallo gegevens wetenschappelijke processen van aanschaf van gegevens via een model training, en vervolgens toohello implementatie van Hallo model als een webservice.</span><span class="sxs-lookup"><span data-stu-id="087de-330">This environment was used tooanalyze a large public dataset, taking it through hello canonical steps of hello Data Science Process, from data acquisition through model training, and then toohello deployment of hello model as a web service.</span></span> <span data-ttu-id="087de-331">U-SQL is gebruikte tooprocess, verkennen en Hallo voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="087de-331">U-SQL was used tooprocess, explore and sample hello data.</span></span> <span data-ttu-id="087de-332">Python en Hive zijn gebruikt met Azure Machine Learning Studio toobuild en implementeren van voorspellende modellen.</span><span class="sxs-lookup"><span data-stu-id="087de-332">Python and Hive were used with Azure Machine Learning Studio toobuild and deploy predictive models.</span></span>

## <a name="whats-next"></a><span data-ttu-id="087de-333">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="087de-333">What's next?</span></span>
<span data-ttu-id="087de-334">Hallo leertraject voor de [Team gegevens wetenschap proces (TDSP)](http://aka.ms/datascienceprocess) biedt koppelingen tootopics met een beschrijving van elke stap in Hallo advanced analytics-proces.</span><span class="sxs-lookup"><span data-stu-id="087de-334">hello learning path for the [Team Data Science Process (TDSP)](http://aka.ms/datascienceprocess) provides links tootopics describing each step in hello advanced analytics process.</span></span> <span data-ttu-id="087de-335">Er zijn een aantal scenario's die worden gespecificeerd op Hallo [Team gegevens wetenschap proces scenario's](data-science-process-walkthroughs.md) die toepassingen hoe pagina toouse resources en services in verschillende predictive analytics-scenario's:</span><span class="sxs-lookup"><span data-stu-id="087de-335">There are a series of walkthroughs itemized on hello [Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) page that showcase how toouse resources and services in various predictive analytics scenarios:</span></span>

* [<span data-ttu-id="087de-336">Hallo Team gegevens wetenschappelijke processen in actie: met behulp van SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="087de-336">hello Team Data Science Process in action: using SQL Data Warehouse</span></span>](machine-learning-data-science-process-sqldw-walkthrough.md)
* [<span data-ttu-id="087de-337">Hallo Team gegevens wetenschappelijke processen in actie: met behulp van HDInsight Hadoop-clusters</span><span class="sxs-lookup"><span data-stu-id="087de-337">hello Team Data Science Process in action: using HDInsight Hadoop clusters</span></span>](machine-learning-data-science-process-hive-walkthrough.md)
* [<span data-ttu-id="087de-338">Hallo Team gegevens wetenschappelijke processen: met behulp van SQL Server</span><span class="sxs-lookup"><span data-stu-id="087de-338">hello Team Data Science Process: using SQL Server</span></span>](machine-learning-data-science-process-sql-walkthrough.md)
* [<span data-ttu-id="087de-339">Overzicht van het gebruik van Hallo gegevens wetenschap proces Spark op Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="087de-339">Overview of hello Data Science Process using Spark on Azure HDInsight</span></span>](machine-learning-data-science-spark-overview.md)

