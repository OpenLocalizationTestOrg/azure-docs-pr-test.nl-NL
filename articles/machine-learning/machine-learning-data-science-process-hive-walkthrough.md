---
title: aaaExplore gegevens in een Hadoop-cluster en modellen maken in Azure Machine Learning | Microsoft Docs
description: Hallo Team gegevens wetenschappelijke processen voor een end-to-end-scenario die gebruikmaakt van een HDInsight Hadoop toobuild cluster en implementeren van een model met behulp van een openbaar gegevensset.
services: machine-learning,hdinsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: e9e76c91-d0f6-483d-bae7-2d3157b86aa0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: hangzh;bradsev
ms.openlocfilehash: a371032e356ffc366af0d6fbe364af281b6efd19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-use-azure-hdinsight-hadoop-clusters"></a><span data-ttu-id="e4395-103">Hallo Team gegevens wetenschappelijke processen in actie: gebruik Azure HDInsight Hadoop-clusters</span><span class="sxs-lookup"><span data-stu-id="e4395-103">hello Team Data Science Process in action: Use Azure HDInsight Hadoop clusters</span></span>
<span data-ttu-id="e4395-104">In dit scenario, gebruiken we Hallo [Team gegevens wetenschap proces (TDSP)](data-science-process-overview.md) aan een end-to-end-scenario met een [Azure HDInsight Hadoop-cluster](https://azure.microsoft.com/services/hdinsight/) toostore, verkennen en gegevens van de engineer van Hallo openbaar functies beschikbare [NYC Taxi reizen](http://www.andresmh.com/nyctaxitrips/) gegevensset en toodown voorbeeldgegevens Hallo.</span><span class="sxs-lookup"><span data-stu-id="e4395-104">In this walkthrough, we use hello [Team Data Science Process (TDSP)](data-science-process-overview.md) in an end-to-end scenario using an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore and feature engineer data from hello publicly available [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset, and toodown sample hello data.</span></span> <span data-ttu-id="e4395-105">Modellen van het Hallo-gegevens zijn gebouwd met Azure Machine Learning toohandle binaire en multiklassen classificatie en regressie voorspellende taken.</span><span class="sxs-lookup"><span data-stu-id="e4395-105">Models of hello data are built with Azure Machine Learning toohandle binary and multiclass classification and regression predictive tasks.</span></span>

<span data-ttu-id="e4395-106">Zie voor een overzicht dat toont hoe toohandle een grotere gegevensset (1 terabyte) voor een vergelijkbaar scenario met behulp van HDInsight Hadoop-clusters voor gegevensverwerking, [Team gegevens wetenschap proces - met behulp van Azure HDInsight Hadoop-Clusters op een gegevensset 1 TB](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="e4395-106">For a walkthrough that shows how toohandle a larger (1 terabyte) dataset for a similar scenario using HDInsight Hadoop clusters for data processing, see [Team Data Science Process - Using Azure HDInsight Hadoop Clusters on a 1 TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md).</span></span>

<span data-ttu-id="e4395-107">Het is ook mogelijk toouse een IPython notebook tooaccomplish Hallo aangeboden Hallo scenario Hallo 1 TB gegevensset met taken.</span><span class="sxs-lookup"><span data-stu-id="e4395-107">It is also possible toouse an IPython notebook tooaccomplish hello tasks presented hello walkthrough using hello 1 TB dataset.</span></span> <span data-ttu-id="e4395-108">Gebruikers die zou zoals tootry contact met deze aanpak opnemen moet Hallo [Criteo scenario met behulp van een verbinding Hive ODBC](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) onderwerp.</span><span class="sxs-lookup"><span data-stu-id="e4395-108">Users who would like tootry this approach should consult hello [Criteo walkthrough using a Hive ODBC connection](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/DataScienceProcess/iPythonNotebooks/machine-Learning-data-science-process-hive-walkthrough-criteo.ipynb) topic.</span></span>

## <span data-ttu-id="e4395-109"><a name="dataset"></a>Beschrijving van de NYC Taxi reizen gegevensset</span><span class="sxs-lookup"><span data-stu-id="e4395-109"><a name="dataset"></a>NYC Taxi Trips Dataset description</span></span>
<span data-ttu-id="e4395-110">Hallo NYC Taxi reis gegevens is ongeveer 20GB gecomprimeerde door komma's gescheiden waarden (CSV)-bestanden (~ 48GB ongecomprimeerde), die bestaat uit meer dan 173 miljoen afzonderlijke reizen en Hallo ervoor staat voor elke reis betaald.</span><span class="sxs-lookup"><span data-stu-id="e4395-110">hello NYC Taxi Trip data is about 20GB of compressed comma-separated values (CSV) files (~48GB uncompressed), comprising more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="e4395-111">Elke record reis omvat Hallo ophalen en inleverbibliotheek locatie en tijd, geanonimiseerde hack (van stuurprogramma) licentienummer en nummer straten (taxi van unieke id).</span><span class="sxs-lookup"><span data-stu-id="e4395-111">Each trip record includes hello pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="e4395-112">Hallo-gegevens bevat informatie over alle reizen Hallo jaar 2013 en is beschikbaar in twee gegevenssets voor elke maand na Hallo:</span><span class="sxs-lookup"><span data-stu-id="e4395-112">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="e4395-113">Hallo 'trip_data' CSV-bestanden bevatten reis details, zoals het aantal passagiers, ophalen en dropoff punten reis duur en duur van reis.</span><span class="sxs-lookup"><span data-stu-id="e4395-113">hello 'trip_data' CSV files contain trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="e4395-114">Hier volgen enkele voorbeeldrecords:</span><span class="sxs-lookup"><span data-stu-id="e4395-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="e4395-115">Hallo 'trip_fare' CSV-bestanden bevatten details van Hallo tarief betaald voor elke reis, zoals betalingstype tarief bedrag, extra kosten en belastingen, tips en tolgelden en Hallo totaalbedrag betaald.</span><span class="sxs-lookup"><span data-stu-id="e4395-115">hello 'trip_fare' CSV files contain details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="e4395-116">Hier volgen enkele voorbeeldrecords:</span><span class="sxs-lookup"><span data-stu-id="e4395-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="e4395-117">Hallo unieke sleutel toojoin reis\_gegevens en reis\_tarief dat bestaat uit Hallo velden: straten, hack\_en ophalen van certificaat\_datetime.</span><span class="sxs-lookup"><span data-stu-id="e4395-117">hello unique key toojoin trip\_data and trip\_fare is composed of hello fields: medallion, hack\_licence and pickup\_datetime.</span></span>

<span data-ttu-id="e4395-118">alle tooget Hallo details relevante tooa bepaalde reis is voldoende toojoin met drie sleutels: 'straten' Hallo ' inbreken\_licentie ' en ' ophalen\_datetime '.</span><span class="sxs-lookup"><span data-stu-id="e4395-118">tooget all of hello details relevant tooa particular trip, it is sufficient toojoin with three keys: hello "medallion", "hack\_license" and "pickup\_datetime".</span></span>

<span data-ttu-id="e4395-119">Wanneer we deze opslaan in de Hive-tabellen kort beschreven sommige meer details van Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="e4395-119">We describe some more details of hello data when we store them into Hive tables shortly.</span></span>

## <span data-ttu-id="e4395-120"><a name="mltasks"></a>Voorbeelden van voorspelling taken</span><span class="sxs-lookup"><span data-stu-id="e4395-120"><a name="mltasks"></a>Examples of prediction tasks</span></span>
<span data-ttu-id="e4395-121">Wanneer gegevens nadert, helpt Hallo soort voorspellingen dat u toomake op basis van de analyse wilt bepalen verduidelijken Hallo taken dat u tooinclude van het proces moet.</span><span class="sxs-lookup"><span data-stu-id="e4395-121">When approaching data, determining hello kind of predictions you want toomake based on its analysis helps clarify hello tasks that you will need tooinclude in your process.</span></span>
<span data-ttu-id="e4395-122">Hier volgen drie voorbeelden van voorspelling problemen die we in dit overzicht waarvan formulering is gebaseerd op Hallo oplossen *tip\_bedrag*:</span><span class="sxs-lookup"><span data-stu-id="e4395-122">Here are three examples of prediction problems that we address in this walkthrough whose formulation is based on hello *tip\_amount*:</span></span>

1. <span data-ttu-id="e4395-123">**Binaire classificatie**: voorspellen of een tip betaald is voor een reis, dat wil zeggen een *tip\_bedrag* die groter is dan $0 een voorbeeld van een positieve is, terwijl een *tip\_bedrag* van $0 is een voorbeeld van een negatief.</span><span class="sxs-lookup"><span data-stu-id="e4395-123">**Binary classification**: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0
2. <span data-ttu-id="e4395-124">**Multiklassen classificatie**: toopredict Hallo bereik van tip bedragen Hallo reis betaald.</span><span class="sxs-lookup"><span data-stu-id="e4395-124">**Multiclass classification**: toopredict hello range of tip amounts paid for hello trip.</span></span> <span data-ttu-id="e4395-125">We delen Hallo *tip\_bedrag* in vijf opslaglocaties of klassen:</span><span class="sxs-lookup"><span data-stu-id="e4395-125">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="e4395-126">**Regressie taak**: toopredict Hallo hoeveelheid Hallo tip voor een reis betaald.</span><span class="sxs-lookup"><span data-stu-id="e4395-126">**Regression task**: toopredict hello amount of hello tip paid for a trip.</span></span>  

## <span data-ttu-id="e4395-127"><a name="setup"></a>Instellen van een HDInsight Hadoop-cluster voor geavanceerde analyses</span><span class="sxs-lookup"><span data-stu-id="e4395-127"><a name="setup"></a>Set up an HDInsight Hadoop cluster for advanced analytics</span></span>
> [!NOTE]
> <span data-ttu-id="e4395-128">Dit is doorgaans een **Admin** taak.</span><span class="sxs-lookup"><span data-stu-id="e4395-128">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="e4395-129">U kunt instellen wanneer er een Azure-omgeving voor geavanceerde analyses die gebruikmaakt van een HDInsight-cluster in drie stappen:</span><span class="sxs-lookup"><span data-stu-id="e4395-129">You can set up an Azure environment for advanced analytics that employs an HDInsight cluster in three steps:</span></span>

1. <span data-ttu-id="e4395-130">[Een opslagaccount maken](../storage/common/storage-create-storage-account.md): dit opslagaccount wordt gebruikt voor het opslaan van gegevens in Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="e4395-130">[Create a storage account](../storage/common/storage-create-storage-account.md): This storage account is used for storing data in Azure Blob Storage.</span></span> <span data-ttu-id="e4395-131">Hallo-gegevens in HDInsight-clusters gebruikt ook bevinden zich hier.</span><span class="sxs-lookup"><span data-stu-id="e4395-131">hello data used in HDInsight clusters also resides here.</span></span>
2. <span data-ttu-id="e4395-132">[Aanpassen van Azure HDInsight Hadoop-clusters voor Hallo Advanced Analytics-proces en de technologie](machine-learning-data-science-customize-hadoop-cluster.md).</span><span class="sxs-lookup"><span data-stu-id="e4395-132">[Customize Azure HDInsight Hadoop clusters for hello Advanced Analytics Process and Technology](machine-learning-data-science-customize-hadoop-cluster.md).</span></span> <span data-ttu-id="e4395-133">Deze stap maakt een Azure HDInsight Hadoop-cluster met 64-bits Anaconda Python 2.7 geïnstalleerd op alle knooppunten.</span><span class="sxs-lookup"><span data-stu-id="e4395-133">This step creates an Azure HDInsight Hadoop cluster with 64-bit Anaconda Python 2.7 installed on all nodes.</span></span> <span data-ttu-id="e4395-134">Er zijn twee belangrijke stappen tooremember tijdens het aanpassen van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="e4395-134">There are two important steps tooremember while customizing your HDInsight cluster.</span></span>
   
   * <span data-ttu-id="e4395-135">Houd er rekening mee toolink Hallo storage-account gemaakt in stap 1 met uw HDInsight-cluster bij het maken van deze.</span><span class="sxs-lookup"><span data-stu-id="e4395-135">Remember toolink hello storage account created in step 1 with your HDInsight cluster when creating it.</span></span> <span data-ttu-id="e4395-136">Dit opslagaccount wordt gebruikt tooaccess gegevens dat wordt verwerkt binnen Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="e4395-136">This storage account is used tooaccess data that is processed within hello cluster.</span></span>
   * <span data-ttu-id="e4395-137">Nadat het Hallo-cluster is gemaakt, schakelt u RAS toohello hoofdknooppunt van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="e4395-137">After hello cluster is created, enable Remote Access toohello head node of hello cluster.</span></span> <span data-ttu-id="e4395-138">Navigeer toohello **configuratie** tabblad en klik op **externe inschakelen**.</span><span class="sxs-lookup"><span data-stu-id="e4395-138">Navigate toohello **Configuration** tab and click **Enable Remote**.</span></span> <span data-ttu-id="e4395-139">Deze stap bevat Hallo gebruikersreferenties gebruikt voor externe aanmelding.</span><span class="sxs-lookup"><span data-stu-id="e4395-139">This step specifies hello user credentials used for remote login.</span></span>
3. <span data-ttu-id="e4395-140">[Maken van een Azure Machine Learning-werkruimte](machine-learning-create-workspace.md): deze Azure Machine Learning-werkruimte is gebruikte toobuild machine learning-modellen.</span><span class="sxs-lookup"><span data-stu-id="e4395-140">[Create an Azure Machine Learning workspace](machine-learning-create-workspace.md): This Azure Machine Learning workspace is used toobuild machine learning models.</span></span> <span data-ttu-id="e4395-141">Deze taak is gericht, na het voltooien van een initiële gegevensverkenning en omlaag steekproeven van Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="e4395-141">This task is addressed after completing an initial data exploration and down sampling using hello HDInsight cluster.</span></span>

## <span data-ttu-id="e4395-142"><a name="getdata"></a>Hallo-gegevens ophalen uit een openbare bron</span><span class="sxs-lookup"><span data-stu-id="e4395-142"><a name="getdata"></a>Get hello data from a public source</span></span>
> [!NOTE]
> <span data-ttu-id="e4395-143">Dit is doorgaans een **Admin** taak.</span><span class="sxs-lookup"><span data-stu-id="e4395-143">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="e4395-144">Hallo tooget [NYC Taxi reizen](http://www.andresmh.com/nyctaxitrips/) gegevensset van de openbare locatie, mag u Hallo-methoden die zijn beschreven in [gegevens verplaatsen tooand uit Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) toocopy Hallo gegevens tooyour machine.</span><span class="sxs-lookup"><span data-stu-id="e4395-144">tooget hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of hello methods described in [Move Data tooand from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) toocopy hello data tooyour machine.</span></span>

<span data-ttu-id="e4395-145">Hier worden beschreven hoe gebruik AzCopy tootransfer Hallo bestanden met gegevens.</span><span class="sxs-lookup"><span data-stu-id="e4395-145">Here we describe how use AzCopy tootransfer hello files containing data.</span></span> <span data-ttu-id="e4395-146">toodownload en installeer AzCopy instructies Hallo op [aan de slag met het AzCopy-opdrachtregelprogramma Hallo](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="e4395-146">toodownload and install AzCopy follow hello instructions at [Getting Started with hello AzCopy Command-Line Utility](../storage/common/storage-use-azcopy.md).</span></span>

1. <span data-ttu-id="e4395-147">Vanuit een opdrachtpromptvenster uitgeven Hallo AzCopy opdrachten te volgen en vervangt *< path_to_data_folder >* met de gewenste bestemming Hallo:</span><span class="sxs-lookup"><span data-stu-id="e4395-147">From a Command Prompt window, issue hello following AzCopy commands, replacing *<path_to_data_folder>* with hello desired destination:</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S

1. <span data-ttu-id="e4395-148">Wanneer Hallo kopie is voltooid, zijn in totaal 24 ZIP-bestanden in de map data Hallo gekozen.</span><span class="sxs-lookup"><span data-stu-id="e4395-148">When hello copy completes, a total of 24 zipped files are in hello data folder chosen.</span></span> <span data-ttu-id="e4395-149">Pak Hallo gedownloade bestanden toohello dezelfde map op uw lokale machine.</span><span class="sxs-lookup"><span data-stu-id="e4395-149">Unzip hello downloaded files toohello same directory on your local machine.</span></span> <span data-ttu-id="e4395-150">Noteer Hallo map waar Hallo ongecomprimeerde bestanden zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="e4395-150">Make a note of hello folder where hello uncompressed files reside.</span></span> <span data-ttu-id="e4395-151">Deze map worden waarnaar wordt verwezen tooas hello *< pad\_naar\_unzipped_data\_bestanden\>*  is het volgende.</span><span class="sxs-lookup"><span data-stu-id="e4395-151">This folder will be referred tooas hello *<path\_to\_unzipped_data\_files\>* is what follows.</span></span>

## <span data-ttu-id="e4395-152"><a name="upload"></a>Hallo gegevens toohello standaardcontainer van Azure HDInsight Hadoop-cluster uploaden</span><span class="sxs-lookup"><span data-stu-id="e4395-152"><a name="upload"></a>Upload hello data toohello default container of Azure HDInsight Hadoop cluster</span></span>
> [!NOTE]
> <span data-ttu-id="e4395-153">Dit is doorgaans een **Admin** taak.</span><span class="sxs-lookup"><span data-stu-id="e4395-153">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="e4395-154">Volgende AzCopy opdrachten Vervang in Hallo Hallo parameters met Hallo werkelijke waarden die u hebt opgegeven bij het maken van Hallo Hadoop-cluster te volgen en ritsen Hallo gegevensbestanden worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="e4395-154">In hello following AzCopy commands, replace hello following parameters with hello actual values that you specified when creating hello Hadoop cluster and unzipping hello data files.</span></span>

* <span data-ttu-id="e4395-155">***&#60; path_to_data_folder >*** Hallo-directory (samen met het pad) op uw computer met bestanden die zijn uitgepakt Hallo gegevens</span><span class="sxs-lookup"><span data-stu-id="e4395-155">***&#60;path_to_data_folder>*** hello directory (along with path) on your machine that contain hello unzipped data files</span></span>  
* <span data-ttu-id="e4395-156">***&#60; opslagaccountnaam van Hadoop-cluster >*** Hallo storage-account die is gekoppeld aan uw HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="e4395-156">***&#60;storage account name of Hadoop cluster>*** hello storage account associated with your HDInsight cluster</span></span>
* <span data-ttu-id="e4395-157">***&#60; standaardcontainer van Hadoop-cluster >*** Hallo standaardcontainer gebruikt door het cluster.</span><span class="sxs-lookup"><span data-stu-id="e4395-157">***&#60;default container of Hadoop cluster>*** hello default container used by your cluster.</span></span> <span data-ttu-id="e4395-158">Houd er rekening mee dat Hallo-naam van de standaard Hallo container is meestal Hallo dezelfde naam als Hallo cluster zelf.</span><span class="sxs-lookup"><span data-stu-id="e4395-158">Note that hello name of hello default container is usually hello same name as hello cluster itself.</span></span> <span data-ttu-id="e4395-159">Als het Hallo-cluster wordt 'abc123.azurehdinsight.net' genoemd, is de standaardcontainer Hallo abc123.</span><span class="sxs-lookup"><span data-stu-id="e4395-159">For example, if hello cluster is called "abc123.azurehdinsight.net", hello default container is abc123.</span></span>
* <span data-ttu-id="e4395-160">***&#60; opslagaccountsleutel >*** Hallo-sleutel voor Hallo storage-account die wordt gebruikt door het cluster</span><span class="sxs-lookup"><span data-stu-id="e4395-160">***&#60;storage account key>*** hello key for hello storage account used by your cluster</span></span>

<span data-ttu-id="e4395-161">Hallo na twee AzCopy opdrachten vanaf een opdrachtprompt of een Windows PowerShell-venster op de computer worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e4395-161">From a Command Prompt or a Windows PowerShell window in your machine, run hello following two AzCopy commands.</span></span>

<span data-ttu-id="e4395-162">Met deze opdracht Hallo reis gegevens te uploaden***nyctaxitripraw*** map in de standaardcontainer Hallo van Hallo Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="e4395-162">This command uploads hello trip data too***nyctaxitripraw*** directory in hello default container of hello Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxitripraw /DestKey:<storage account key> /S /Pattern:trip_data_*.csv

<span data-ttu-id="e4395-163">Met deze opdracht Hallo tarief gegevens te uploaden***nyctaxifareraw*** map in de standaardcontainer Hallo van Hallo Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="e4395-163">This command uploads hello fare data too***nyctaxifareraw*** directory in hello default container of hello Hadoop cluster.</span></span>

        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:<path_to_unzipped_data_files> /Dest:https://<storage account name of Hadoop cluster>.blob.core.windows.net/<default container of Hadoop cluster>/nyctaxifareraw /DestKey:<storage account key> /S /Pattern:trip_fare_*.csv

<span data-ttu-id="e4395-164">Hallo gegevens moet nu in Azure Blob Storage en gereed toobe verbruikt binnen Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="e4395-164">hello data should now in Azure Blob Storage and ready toobe consumed within hello HDInsight cluster.</span></span>

## <span data-ttu-id="e4395-165"><a name="#download-hql-files"></a>Meld u aan bij de hoofdknooppunt Hallo van Hadoop-cluster en en voorbereiden voor experimentele data-analyse</span><span class="sxs-lookup"><span data-stu-id="e4395-165"><a name="#download-hql-files"></a>Log into hello head node of Hadoop cluster and and prepare for exploratory data analysis</span></span>
> [!NOTE]
> <span data-ttu-id="e4395-166">Dit is doorgaans een **Admin** taak.</span><span class="sxs-lookup"><span data-stu-id="e4395-166">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="e4395-167">tooaccess hello hoofdknooppunt van Hallo cluster voor experimentele data-analyse en omlaag steekproeven van het Hallo-gegevens, volgt u Hallo procedure beschreven in [toegang Hallo Head knooppunt van Hadoop-Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span><span class="sxs-lookup"><span data-stu-id="e4395-167">tooaccess hello head node of hello cluster for exploratory data analysis and down sampling of hello data, follow hello procedure outlined in [Access hello Head Node of Hadoop Cluster](machine-learning-data-science-customize-hadoop-cluster.md#headnode).</span></span>

<span data-ttu-id="e4395-168">In dit scenario, gebruiken we voornamelijk query's die zijn geschreven [Hive](https://hive.apache.org/), een querytaal SQL-achtige, tooperform voorlopige gegevens explorations.</span><span class="sxs-lookup"><span data-stu-id="e4395-168">In this walkthrough, we primarily use queries written in [Hive](https://hive.apache.org/), a SQL-like query language, tooperform preliminary data explorations.</span></span> <span data-ttu-id="e4395-169">Hallo Hive-query's worden opgeslagen in .hql bestanden.</span><span class="sxs-lookup"><span data-stu-id="e4395-169">hello Hive queries are stored in .hql files.</span></span> <span data-ttu-id="e4395-170">We vervolgens steekproef deze gegevens toobe in Azure Machine Learning gebruikt voor het bouwen van modellen omlaag.</span><span class="sxs-lookup"><span data-stu-id="e4395-170">We then down sample this data toobe used within Azure Machine Learning for building models.</span></span>

<span data-ttu-id="e4395-171">tooprepare hello cluster voor experimentele data-analyse, we downloaden Hallo .hql bestanden met relevante Hive-scripts Hallo van [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) tooa lokale map (C:\temp) op Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="e4395-171">tooprepare hello cluster for exploratory data analysis, we download hello .hql files containing hello relevant Hive scripts from [github](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) tooa local directory (C:\temp) on hello head node.</span></span> <span data-ttu-id="e4395-172">toodo deze, open Hallo **opdrachtprompt** vanuit Hallo hoofdknooppunt Hallo-cluster en probleem Hallo volgende twee opdrachten:</span><span class="sxs-lookup"><span data-stu-id="e4395-172">toodo this, open hello **Command Prompt** from within hello head node of hello cluster and issue hello following two commands:</span></span>

    set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/DataScienceProcess/DataScienceScripts/Download_DataScience_Scripts.ps1'

    @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"

<span data-ttu-id="e4395-173">Deze twee opdrachten zal alle .hql bestanden downloaden die nodig zijn in dit scenario toohello lokale directory ***C:\temp &#92;*** in Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="e4395-173">These two commands will download all .hql files needed in this walkthrough toohello local directory ***C:\temp&#92;*** in hello head node.</span></span>

## <span data-ttu-id="e4395-174"><a name="#hive-db-tables"></a>Hive-database en per maand gepartitioneerde tabellen maken</span><span class="sxs-lookup"><span data-stu-id="e4395-174"><a name="#hive-db-tables"></a>Create Hive database and tables partitioned by month</span></span>
> [!NOTE]
> <span data-ttu-id="e4395-175">Dit is doorgaans een **Admin** taak.</span><span class="sxs-lookup"><span data-stu-id="e4395-175">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="e4395-176">Er zijn nu gereed toocreate Hive-tabellen voor onze NYC taxi dataset.</span><span class="sxs-lookup"><span data-stu-id="e4395-176">We are now ready toocreate Hive tables for our NYC taxi dataset.</span></span>
<span data-ttu-id="e4395-177">Open in hoofdknooppunt Hallo van Hadoop-cluster Hallo Hallo ***Hadoop-opdrachtregel*** op bureaublad van hoofdknooppunt Hallo Hallo en Voer Hallo Hive directory door te voeren opdracht Hallo</span><span class="sxs-lookup"><span data-stu-id="e4395-177">In hello head node of hello Hadoop cluster, open hello ***Hadoop Command Line*** on hello desktop of hello head node, and enter hello Hive directory by entering hello command</span></span>

    cd %hive_home%\bin

> [!NOTE]
> <span data-ttu-id="e4395-178">**Alle Hive-opdrachten uitvoeren in dit overzicht van Hallo hierboven Hive bin / directory prompt. Dit zorgt voor problemen die pad automatisch. We gebruiken Hallo termen 'Hive directory prompt', ' Hive bin / directory prompt ', en "Hadoop-opdrachtregel ' door elkaar in dit scenario.**</span><span class="sxs-lookup"><span data-stu-id="e4395-178">**Run all Hive commands in this walkthrough from hello above Hive bin/ directory prompt. This will take care of any path issues automatically. We use hello terms "Hive directory prompt", "Hive bin/ directory prompt",  and "Hadoop Command Line" interchangeably in this walkthrough.**</span></span>
> 
> 

<span data-ttu-id="e4395-179">Voer vanaf Hallo Hive directory prompt Hallo opdracht in Hadoop opdrachtregel van Hallo hoofdknooppunt toosubmit Hallo Hive query toocreate Hive-database en tabellen te volgen:</span><span class="sxs-lookup"><span data-stu-id="e4395-179">From hello Hive directory prompt, enter hello following command in Hadoop Command Line of hello head node toosubmit hello Hive query toocreate Hive database and tables:</span></span>

    hive -f "C:\temp\sample_hive_create_db_and_tables.hql"

<span data-ttu-id="e4395-180">Hier volgt Hallo inhoud Hallo ***C:\temp\sample\_hive\_maken\_db\_en\_tables.hql*** -bestand dat wordt gemaakt van Hive database ***nyctaxidb *** en tabellen ***reis*** en ***tarief***.</span><span class="sxs-lookup"><span data-stu-id="e4395-180">Here is hello content of hello ***C:\temp\sample\_hive\_create\_db\_and\_tables.hql*** file which creates Hive database ***nyctaxidb*** and tables ***trip*** and ***fare***.</span></span>

    create database if not exists nyctaxidb;

    create external table if not exists nyctaxidb.trip
    (
        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double)  
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/trip' TBLPROPERTIES('skip.header.line.count'='1');

    create external table if not exists nyctaxidb.fare
    (
        medallion string,
        hack_license string,
        vendor_id string,
        pickup_datetime string,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double)
    PARTITIONED BY (month int)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' lines terminated by '\n'
    STORED AS TEXTFILE LOCATION 'wasb:///nyctaxidbdata/fare' TBLPROPERTIES('skip.header.line.count'='1');

<span data-ttu-id="e4395-181">Deze Hive-script maakt twee tabellen:</span><span class="sxs-lookup"><span data-stu-id="e4395-181">This Hive script creates two tables:</span></span>

* <span data-ttu-id="e4395-182">Hallo 'trip' tabel bevat reis details van elke rijpositie (stuurprogrammagegevens, ophalen tijd, reis afstand en tijden)</span><span class="sxs-lookup"><span data-stu-id="e4395-182">hello "trip" table contains trip details of each ride (driver details, pickup time, trip distance and times)</span></span>
* <span data-ttu-id="e4395-183">Hallo 'tarief' tabel bevat tarief details (tarief, tip bedrag, tolgelden en toeslagen).</span><span class="sxs-lookup"><span data-stu-id="e4395-183">hello "fare" table contains fare details (fare amount, tip amount, tolls and surcharges).</span></span>

<span data-ttu-id="e4395-184">Als u extra hulp nodig hebt met deze procedures of tooinvestigate alternatieve waarden wilt, raadpleegt u Hallo sectie [indienen Hive-query's rechtstreeks vanuit Hallo Hadoop-opdrachtregel ](machine-learning-data-science-move-hive-tables.md#submit).</span><span class="sxs-lookup"><span data-stu-id="e4395-184">If you need any additional assistance with these procedures or want tooinvestigate alternative ones, see hello section [Submit Hive queries directly from hello Hadoop Command Line ](machine-learning-data-science-move-hive-tables.md#submit).</span></span>

## <span data-ttu-id="e4395-185"><a name="#load-data"></a>Laad tooHive gegevenstabellen door partities</span><span class="sxs-lookup"><span data-stu-id="e4395-185"><a name="#load-data"></a>Load Data tooHive tables by partitions</span></span>
> [!NOTE]
> <span data-ttu-id="e4395-186">Dit is doorgaans een **Admin** taak.</span><span class="sxs-lookup"><span data-stu-id="e4395-186">This is typically an **Admin** task.</span></span>
> 
> 

<span data-ttu-id="e4395-187">Hallo NYC taxi gegevensset heeft een natuurlijke partitioneren per maand, die we tooenable verwerking en queryprestaties sneller worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e4395-187">hello NYC taxi dataset has a natural partitioning by month, which we use tooenable faster processing and query times.</span></span> <span data-ttu-id="e4395-188">Hallo onderstaande PowerShell-opdrachten (uitgegeven door Hallo Hive directory via Hallo **Hadoop-opdrachtregel**) laden van gegevens toohello 'trip' en 'tarief' Hive-tabellen gepartitioneerd per maand.</span><span class="sxs-lookup"><span data-stu-id="e4395-188">hello PowerShell commands below (issued from hello Hive directory using hello **Hadoop Command Line**) load data toohello "trip" and "fare" Hive tables partitioned by month.</span></span>

    for /L %i IN (1,1,12) DO (hive -hiveconf MONTH=%i -f "C:\temp\sample_hive_load_data_by_partitions.hql")

<span data-ttu-id="e4395-189">Hallo *voorbeeld\_hive\_laden\_gegevens\_door\_partitions.hql* bestand bevat de volgende Hallo **laden** opdrachten.</span><span class="sxs-lookup"><span data-stu-id="e4395-189">hello *sample\_hive\_load\_data\_by\_partitions.hql* file contains hello following **LOAD** commands.</span></span>

    LOAD DATA INPATH 'wasb:///nyctaxitripraw/trip_data_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.trip PARTITION (month=${hiveconf:MONTH});
    LOAD DATA INPATH 'wasb:///nyctaxifareraw/trip_fare_${hiveconf:MONTH}.csv' INTO TABLE nyctaxidb.fare PARTITION (month=${hiveconf:MONTH});

<span data-ttu-id="e4395-190">Opmerking een aantal Hive-query's die we hier in Hallo exploratie proces gebruiken betrekking hebben op slechts één partitie of op een aantal partities opzoeken.</span><span class="sxs-lookup"><span data-stu-id="e4395-190">Note that a number of Hive queries we use here in hello exploration process involve looking at just a single partition or at only a couple of partitions.</span></span> <span data-ttu-id="e4395-191">Maar deze query's over Hallo volledige gegevens kunnen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e4395-191">But these queries could be run across hello entire data.</span></span>

### <span data-ttu-id="e4395-192"><a name="#show-db"></a>Databases weergeven in Hallo HDInsight Hadoop-cluster</span><span class="sxs-lookup"><span data-stu-id="e4395-192"><a name="#show-db"></a>Show databases in hello HDInsight Hadoop cluster</span></span>
<span data-ttu-id="e4395-193">tooshow hello databases die zijn gemaakt in HDInsight Hadoop-cluster in Hallo Hadoop opdrachtregelvenster, Hallo volgende opdracht in de Hadoop-opdrachtregel uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e4395-193">tooshow hello databases created in HDInsight Hadoop cluster inside hello Hadoop Command Line window, run hello following command in Hadoop Command Line:</span></span>

    hive -e "show databases;"

### <span data-ttu-id="e4395-194"><a name="#show-tables"></a>Hallo Hive-tabellen in Hallo nyctaxidb database weergeven</span><span class="sxs-lookup"><span data-stu-id="e4395-194"><a name="#show-tables"></a>Show hello Hive tables in hello nyctaxidb database</span></span>
<span data-ttu-id="e4395-195">tooshow hello tabellen in Hallo nyctaxidb database Hallo volgende opdracht in de Hadoop-opdrachtregel uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e4395-195">tooshow hello tables in hello nyctaxidb database, run hello following command in Hadoop Command Line:</span></span>

    hive -e "show tables in nyctaxidb;"

<span data-ttu-id="e4395-196">We kunt bevestigen dat Hallo tabellen worden gepartitioneerd door onderstaande Hallo-opdracht:</span><span class="sxs-lookup"><span data-stu-id="e4395-196">We can confirm that hello tables are partitioned by issuing hello command below:</span></span>

    hive -e "show partitions nyctaxidb.trip;"

<span data-ttu-id="e4395-197">Hallo verwachte uitvoer wordt hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="e4395-197">hello expected output is shown below:</span></span>

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 2.075 seconds, Fetched: 12 row(s)

<span data-ttu-id="e4395-198">Op deze manier kunnen we dat die Hallo tarief tabel is gepartitioneerd door onderstaande Hallo-opdracht:</span><span class="sxs-lookup"><span data-stu-id="e4395-198">Similarly, we can ensure that hello fare table is partitioned by issuing hello command below:</span></span>

    hive -e "show partitions nyctaxidb.fare;"

<span data-ttu-id="e4395-199">Hallo verwachte uitvoer wordt hieronder weergegeven:</span><span class="sxs-lookup"><span data-stu-id="e4395-199">hello expected output is shown below:</span></span>

    month=1
    month=10
    month=11
    month=12
    month=2
    month=3
    month=4
    month=5
    month=6
    month=7
    month=8
    month=9
    Time taken: 1.887 seconds, Fetched: 12 row(s)

## <span data-ttu-id="e4395-200"><a name="#explore-hive"></a>Gegevensverkenning en functie-engineering in component</span><span class="sxs-lookup"><span data-stu-id="e4395-200"><a name="#explore-hive"></a>Data exploration and feature engineering in Hive</span></span>
> [!NOTE]
> <span data-ttu-id="e4395-201">Dit is doorgaans een **gegevens wetenschappelijk** taak.</span><span class="sxs-lookup"><span data-stu-id="e4395-201">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="e4395-202">Hallo gegevensverkenning en functies van technische taken voor Hallo gegevens geladen in de Hive-tabellen Hallo kan worden gerealiseerd met Hive-query's.</span><span class="sxs-lookup"><span data-stu-id="e4395-202">hello data exploration and feature engineering tasks for hello data loaded into hello Hive tables can be accomplished using Hive queries.</span></span> <span data-ttu-id="e4395-203">Hier volgen enkele voorbeelden van dergelijke taken dat we in deze sectie doorlopen:</span><span class="sxs-lookup"><span data-stu-id="e4395-203">Here are examples of such tasks that we walk you through in this section:</span></span>

* <span data-ttu-id="e4395-204">Hallo bovenste 10 records weergeven in beide tabellen.</span><span class="sxs-lookup"><span data-stu-id="e4395-204">View hello top 10 records in both tables.</span></span>
* <span data-ttu-id="e4395-205">Verken de gegevens distributies van enkele velden in verschillende tijdvensters.</span><span class="sxs-lookup"><span data-stu-id="e4395-205">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="e4395-206">Onderzoek de kwaliteit van de gegevens van Hallo breedtegraad velden.</span><span class="sxs-lookup"><span data-stu-id="e4395-206">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="e4395-207">Genereren van binaire en multiklassen classificatielabels op basis van Hallo **tip\_bedrag**.</span><span class="sxs-lookup"><span data-stu-id="e4395-207">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="e4395-208">Functies door Hallo directe trip afstanden computing genereren.</span><span class="sxs-lookup"><span data-stu-id="e4395-208">Generate features by computing hello direct trip distances.</span></span>

### <a name="exploration-view-hello-top-10-records-in-table-trip"></a><span data-ttu-id="e4395-209">Exploratie: Hallo bovenste 10 records in de tabel reis weergeven</span><span class="sxs-lookup"><span data-stu-id="e4395-209">Exploration: View hello top 10 records in table trip</span></span>
> [!NOTE]
> <span data-ttu-id="e4395-210">Dit is doorgaans een **gegevens wetenschappelijk** taak.</span><span class="sxs-lookup"><span data-stu-id="e4395-210">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="e4395-211">toosee hoe gegevens Hallo zien eruit, we naar de 10 records uit elke tabel.</span><span class="sxs-lookup"><span data-stu-id="e4395-211">toosee what hello data looks like, we examine 10 records from each table.</span></span> <span data-ttu-id="e4395-212">Hallo twee query's afzonderlijk volgende uit Hallo Hive directory prompt in Hallo Hadoop-opdrachtregel console tooinspect Hallo records worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e4395-212">Run hello following two queries separately from hello Hive directory prompt in hello Hadoop Command Line console tooinspect hello records.</span></span>

<span data-ttu-id="e4395-213">tooget hello bovenste 10 records in de tabel Hallo 'trip' van de eerste maand Hallo:</span><span class="sxs-lookup"><span data-stu-id="e4395-213">tooget hello top 10 records in hello table "trip" from hello first month:</span></span>

    hive -e "select * from nyctaxidb.trip where month=1 limit 10;"

<span data-ttu-id="e4395-214">tooget hello bovenste 10 records in de tabel Hallo 'tarief' van de eerste maand Hallo:</span><span class="sxs-lookup"><span data-stu-id="e4395-214">tooget hello top 10 records in hello table "fare" from hello first month:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;"

<span data-ttu-id="e4395-215">Het is vaak nuttig toosave Hallo records tooa bestand om handige weer te geven.</span><span class="sxs-lookup"><span data-stu-id="e4395-215">It is often useful toosave hello records tooa file for convenient viewing.</span></span> <span data-ttu-id="e4395-216">Een kleine wijziging toohello hierboven query bewerkstelligt dit:</span><span class="sxs-lookup"><span data-stu-id="e4395-216">A small change toohello above query accomplishes this:</span></span>

    hive -e "select * from nyctaxidb.fare where month=1 limit 10;" > C:\temp\testoutput

### <a name="exploration-view-hello-number-of-records-in-each-of-hello-12-partitions"></a><span data-ttu-id="e4395-217">Exploratie: Hallo aantal records dat in alle Hallo 12 partities weergeven</span><span class="sxs-lookup"><span data-stu-id="e4395-217">Exploration: View hello number of records in each of hello 12 partitions</span></span>
> [!NOTE]
> <span data-ttu-id="e4395-218">Dit is doorgaans een **gegevens wetenschappelijk** taak.</span><span class="sxs-lookup"><span data-stu-id="e4395-218">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="e4395-219">Is van belang hoe Hallo aantal reizen tijdens kalenderjaar Hallo varieert Hallo.</span><span class="sxs-lookup"><span data-stu-id="e4395-219">Of interest is hello how hello number of trips varies during hello calendar year.</span></span> <span data-ttu-id="e4395-220">Groeperen per maand, kunnen wij toosee hoe deze verdeling van reizen eruit ziet.</span><span class="sxs-lookup"><span data-stu-id="e4395-220">Grouping by month allows us toosee what this distribution of trips looks like.</span></span>

    hive -e "select month, count(*) from nyctaxidb.trip group by month;"

<span data-ttu-id="e4395-221">Hierdoor hebt ons Hallo uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e4395-221">This gives us hello output :</span></span>

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 283.406 seconds, Fetched: 12 row(s)

<span data-ttu-id="e4395-222">Hier de eerste kolom Hallo Hallo maand en Hallo tweede Hallo aantal reizen voor die maand.</span><span class="sxs-lookup"><span data-stu-id="e4395-222">Here, hello first column is hello month and hello second is hello number of trips for that month.</span></span>

<span data-ttu-id="e4395-223">We kunnen ook Hallo kunt u het totale aantal records in onze gegevensset reis tellen door uitgifte van de volgende opdracht bij de opdrachtprompt van de map Hallo Hive Hallo.</span><span class="sxs-lookup"><span data-stu-id="e4395-223">We can also count hello total number of records in our trip data set by issuing hello following command at hello Hive directory prompt.</span></span>

    hive -e "select count(*) from nyctaxidb.trip;"

<span data-ttu-id="e4395-224">Dit levert:</span><span class="sxs-lookup"><span data-stu-id="e4395-224">This yields:</span></span>

    173179759
    Time taken: 284.017 seconds, Fetched: 1 row(s)

<span data-ttu-id="e4395-225">Opdrachten vergelijkbare toothose weergegeven voor Hallo reis gegevensset kunnen we Hive-query's uit Hallo Hive directory prompt voor Hallo tarief gegevensset toovalidate Hallo aantal records uitgeven.</span><span class="sxs-lookup"><span data-stu-id="e4395-225">Using commands similar toothose shown for hello trip data set, we can issue Hive queries from hello Hive directory prompt for hello fare data set toovalidate hello number of records.</span></span>

    hive -e "select month, count(*) from nyctaxidb.fare group by month;"

<span data-ttu-id="e4395-226">Hierdoor hebt ons Hallo uitvoer:</span><span class="sxs-lookup"><span data-stu-id="e4395-226">This gives us hello output:</span></span>

    1       14776615
    2       13990176
    3       15749228
    4       15100468
    5       15285049
    6       14385456
    7       13823840
    8       12597109
    9       14107693
    10      15004556
    11      14388451
    12      13971118
    Time taken: 253.955 seconds, Fetched: 12 row(s)

<span data-ttu-id="e4395-227">Houd er rekening mee dat Hallo exact hetzelfde aantal bezoeken per maand wordt geretourneerd voor beide gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="e4395-227">Note that hello exact same number of trips per month is returned for both data sets.</span></span> <span data-ttu-id="e4395-228">Dit biedt Hallo eerste validatie die Hallo gegevens correct zijn geladen.</span><span class="sxs-lookup"><span data-stu-id="e4395-228">This provides hello first validation that hello data has been loaded correctly.</span></span>

<span data-ttu-id="e4395-229">Hallo kunt u het totale aantal records in de gegevensset voor Hallo tarief tellen kan worden gedaan met de opdracht Hallo hieronder uit Hallo Hive directory opdrachtprompt:</span><span class="sxs-lookup"><span data-stu-id="e4395-229">Counting hello total number of records in hello fare data set can be done using hello command below from hello Hive directory prompt:</span></span>

    hive -e "select count(*) from nyctaxidb.fare;"

<span data-ttu-id="e4395-230">Dit levert:</span><span class="sxs-lookup"><span data-stu-id="e4395-230">This yields :</span></span>

    173179759
    Time taken: 186.683 seconds, Fetched: 1 row(s)

<span data-ttu-id="e4395-231">Totaal aantal records in beide tabellen Hallo is ook Hallo dezelfde.</span><span class="sxs-lookup"><span data-stu-id="e4395-231">hello total number of records in both tables is also hello same.</span></span> <span data-ttu-id="e4395-232">Dit biedt een tweede validatie die Hallo gegevens correct zijn geladen.</span><span class="sxs-lookup"><span data-stu-id="e4395-232">This provides a second validation that hello data has been loaded correctly.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="e4395-233">Exploratie: Reis distributie door straten</span><span class="sxs-lookup"><span data-stu-id="e4395-233">Exploration: Trip distribution by medallion</span></span>
> [!NOTE]
> <span data-ttu-id="e4395-234">Dit is doorgaans een **gegevens wetenschappelijk** taak.</span><span class="sxs-lookup"><span data-stu-id="e4395-234">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="e4395-235">In dit voorbeeld identificeert Hallo straten (taxi getallen) met meer dan 100 reizen binnen een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="e4395-235">This example identifies hello medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="e4395-236">Hallo query voordelen van Hallo gepartitioneerd tabeltoegang omdat deze wordt waarbij door Hallo partitie variabele **maand**.</span><span class="sxs-lookup"><span data-stu-id="e4395-236">hello query benefits from hello partitioned table access since it is conditioned by hello partition variable **month**.</span></span> <span data-ttu-id="e4395-237">Hallo-queryresultaten tooa lokaal bestand queryoutput.tsv zijn geschreven in `C:\temp` op Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="e4395-237">hello query results are written tooa local file queryoutput.tsv in `C:\temp` on hello head node.</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="e4395-238">Hier is Hallo inhoud van *voorbeeld\_hive\_reis\_aantal\_door\_medallion.hql* -bestand voor inspectie.</span><span class="sxs-lookup"><span data-stu-id="e4395-238">Here is hello content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="e4395-239">Hallo straten in Hallo NYC taxi gegevensset identificeert een unieke CAB-bestand.</span><span class="sxs-lookup"><span data-stu-id="e4395-239">hello medallion in hello NYC taxi data set identifies a unique cab.</span></span> <span data-ttu-id="e4395-240">We kunnen identificeren welke cab-bestanden zijn 'bezet' door vragen aan welke u meer dan een bepaald aantal reizen aangebracht in een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="e4395-240">We can identify which cabs are "busy" by asking which ones made more than a certain number of trips in a particular time period.</span></span> <span data-ttu-id="e4395-241">Hallo volgende voorbeeld identificeert cabinetbestanden die uit meer dan honderd reizen Hallo eerste drie maanden, en slaat Hallo query resultaten tooa lokaal bestand C:\temp\queryoutput.tsv.</span><span class="sxs-lookup"><span data-stu-id="e4395-241">hello following example identifies cabs that made more than a hundred trips in hello first three months, and saves hello query results tooa local file, C:\temp\queryoutput.tsv.</span></span>

<span data-ttu-id="e4395-242">Hier is Hallo inhoud van *voorbeeld\_hive\_reis\_aantal\_door\_medallion.hql* -bestand voor inspectie.</span><span class="sxs-lookup"><span data-stu-id="e4395-242">Here is hello content of *sample\_hive\_trip\_count\_by\_medallion.hql* file for inspection.</span></span>

    SELECT medallion, COUNT(*) as med_count
    FROM nyctaxidb.fare
    WHERE month<=3
    GROUP BY medallion
    HAVING med_count > 100
    ORDER BY med_count desc;

<span data-ttu-id="e4395-243">Component van Hallo directory prompt onderstaande probleem Hallo-opdracht:</span><span class="sxs-lookup"><span data-stu-id="e4395-243">From hello Hive directory prompt, issue hello command below :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion.hql" > C:\temp\queryoutput.tsv

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="e4395-244">Exploratie: Reis distributie door straten en hack_license</span><span class="sxs-lookup"><span data-stu-id="e4395-244">Exploration: Trip distribution by medallion and hack_license</span></span>
> [!NOTE]
> <span data-ttu-id="e4395-245">Dit is doorgaans een **gegevens wetenschappelijk** taak.</span><span class="sxs-lookup"><span data-stu-id="e4395-245">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="e4395-246">Wanneer een dataset verkennen, willen we vaak tooexamine Hallo aantal co-exemplaren van groepen van waarden.</span><span class="sxs-lookup"><span data-stu-id="e4395-246">When exploring a dataset, we frequently want tooexamine hello number of co-occurences of groups of values.</span></span> <span data-ttu-id="e4395-247">Deze sectie vindt u een voorbeeld van hoe toodo dit voor CAB-bestanden en stuurprogramma's.</span><span class="sxs-lookup"><span data-stu-id="e4395-247">This section provide an example of how toodo this for cabs and drivers.</span></span>

<span data-ttu-id="e4395-248">Hallo *voorbeeld\_hive\_reis\_aantal\_door\_straten\_license.hql* bestandsgroepen Hallo tarief gegevens is ingesteld op 'straten' en 'hack_license' en retourneert de aantallen voor elke combinatie.</span><span class="sxs-lookup"><span data-stu-id="e4395-248">hello *sample\_hive\_trip\_count\_by\_medallion\_license.hql* file groups hello fare data set on "medallion" and "hack_license" and returns counts of each combination.</span></span> <span data-ttu-id="e4395-249">Hieronder vindt u de inhoud ervan.</span><span class="sxs-lookup"><span data-stu-id="e4395-249">Below are its contents.</span></span>

    SELECT medallion, hack_license, COUNT(*) as trip_count
    FROM nyctaxidb.fare
    WHERE month=1
    GROUP BY medallion, hack_license
    HAVING trip_count > 100
    ORDER BY trip_count desc;

<span data-ttu-id="e4395-250">Deze query retourneert CAB-bestand en een bepaald stuurprogramma combinaties gesorteerd op aflopende aantal heen.</span><span class="sxs-lookup"><span data-stu-id="e4395-250">This query returns cab and particular driver combinations ordered by descending number of trips.</span></span>

<span data-ttu-id="e4395-251">Component van Hallo directory prompt, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e4395-251">From hello Hive directory prompt, run :</span></span>

    hive -f "C:\temp\sample_hive_trip_count_by_medallion_license.hql" > C:\temp\queryoutput.tsv

<span data-ttu-id="e4395-252">Hallo-queryresultaten worden tooa lokaal bestand C:\temp\queryoutput.tsv geschreven.</span><span class="sxs-lookup"><span data-stu-id="e4395-252">hello query results are written tooa local file C:\temp\queryoutput.tsv.</span></span>

### <a name="exploration-assessing-data-quality-by-checking-for-invalid-longitudelatitude-records"></a><span data-ttu-id="e4395-253">Exploratie: Beoordeling van de kwaliteit van de gegevens door te controleren op Ongeldige lengtegraad/breedtegraad records</span><span class="sxs-lookup"><span data-stu-id="e4395-253">Exploration: Assessing data quality by checking for invalid longitude/latitude records</span></span>
> [!NOTE]
> <span data-ttu-id="e4395-254">Dit is doorgaans een **gegevens wetenschappelijk** taak.</span><span class="sxs-lookup"><span data-stu-id="e4395-254">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="e4395-255">Een algemene doelstelling van experimentele gegevensanalyse is tooweed ongeldige of onjuiste records.</span><span class="sxs-lookup"><span data-stu-id="e4395-255">A common objective of exploratory data analysis is tooweed out invalid or bad records.</span></span> <span data-ttu-id="e4395-256">Hallo bepaalt voorbeeld in deze sectie of ofwel hello lengte of breedte velden een waarde ver buiten Hallo NYC gebied bevatten.</span><span class="sxs-lookup"><span data-stu-id="e4395-256">hello example in this section determines whether either hello longitude or latitude fields contain a value far outside hello NYC area.</span></span> <span data-ttu-id="e4395-257">Aangezien het waarschijnlijk dat dergelijke records een onjuiste lengtegraad-breedtegraadwaarden hebben, willen we tooeliminate van alle gegevens die toobe is gebruikt voor het model.</span><span class="sxs-lookup"><span data-stu-id="e4395-257">Since it is likely that such records have an erroneous longitude-latitude values, we want tooeliminate them from any data that is toobe used for modeling.</span></span>

<span data-ttu-id="e4395-258">Hier is Hallo inhoud van *voorbeeld\_hive\_kwaliteit\_assessment.hql* -bestand voor inspectie.</span><span class="sxs-lookup"><span data-stu-id="e4395-258">Here is hello content of *sample\_hive\_quality\_assessment.hql* file for inspection.</span></span>

        SELECT COUNT(*) FROM nyctaxidb.trip
        WHERE month=1
        AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(pickup_latitude AS float) NOT BETWEEN 30 AND 90
        OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND -30
        OR    CAST(dropoff_latitude AS float) NOT BETWEEN 30 AND 90);


<span data-ttu-id="e4395-259">Component van Hallo directory prompt, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e4395-259">From hello Hive directory prompt, run :</span></span>

    hive -S -f "C:\temp\sample_hive_quality_assessment.hql"

<span data-ttu-id="e4395-260">Hallo *-S* argument dat is opgenomen in deze opdracht wordt onderdrukt Hallo status scherm afdruk van Hallo kaart/verminderen Hive-taken.</span><span class="sxs-lookup"><span data-stu-id="e4395-260">hello *-S* argument included in this command suppresses hello status screen printout of hello Hive Map/Reduce jobs.</span></span> <span data-ttu-id="e4395-261">Dit is nuttig omdat op deze manier Hallo scherm afdrukken Hallo voor Hive-query-uitvoer beter leesbaar.</span><span class="sxs-lookup"><span data-stu-id="e4395-261">This is useful because it makes hello screen print of hello Hive query output more readable.</span></span>

### <a name="exploration-binary-class-distributions-of-trip-tips"></a><span data-ttu-id="e4395-262">Exploratie: Binaire klasse distributies reis tips</span><span class="sxs-lookup"><span data-stu-id="e4395-262">Exploration: Binary class distributions of trip tips</span></span>
> [!NOTE]
> <span data-ttu-id="e4395-263">Dit is doorgaans een **gegevens wetenschappelijk** taak.</span><span class="sxs-lookup"><span data-stu-id="e4395-263">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="e4395-264">Voor binair klassificatieprobleem Hallo die worden beschreven in Hallo [voorbeelden van voorspelling taken](machine-learning-data-science-process-hive-walkthrough.md#mltasks) sectie is nuttig tooknow of een tip of niet is opgegeven.</span><span class="sxs-lookup"><span data-stu-id="e4395-264">For hello binary classification problem outlined in hello [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section, it is useful tooknow whether a tip was given or not.</span></span> <span data-ttu-id="e4395-265">Deze verdeling van tips is binaire:</span><span class="sxs-lookup"><span data-stu-id="e4395-265">This distribution of tips is binary:</span></span>

* <span data-ttu-id="e4395-266">Tip gegeven (klasse 1, tip\_bedrag > $0)</span><span class="sxs-lookup"><span data-stu-id="e4395-266">tip given(Class 1, tip\_amount > $0)</span></span>  
* <span data-ttu-id="e4395-267">Er is geen tip (klasse 0, tip\_bedrag = $0).</span><span class="sxs-lookup"><span data-stu-id="e4395-267">no tip (Class 0, tip\_amount = $0).</span></span>

<span data-ttu-id="e4395-268">Hallo *voorbeeld\_hive\_punt\_frequencies.hql* bestand hieronder wordt weergegeven, wordt dit.</span><span class="sxs-lookup"><span data-stu-id="e4395-268">hello *sample\_hive\_tipped\_frequencies.hql* file shown below does this.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount > 0, 1, 0) as tipped, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tipped;

<span data-ttu-id="e4395-269">Component van Hallo directory prompt, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e4395-269">From hello Hive directory prompt, run:</span></span>

    hive -f "C:\temp\sample_hive_tipped_frequencies.hql"


### <a name="exploration-class-distributions-in-hello-multiclass-setting"></a><span data-ttu-id="e4395-270">Exploratie: Klasse distributies in multiklassen Hallo-instelling</span><span class="sxs-lookup"><span data-stu-id="e4395-270">Exploration: Class distributions in hello multiclass setting</span></span>
> [!NOTE]
> <span data-ttu-id="e4395-271">Dit is doorgaans een **gegevens wetenschappelijk** taak.</span><span class="sxs-lookup"><span data-stu-id="e4395-271">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="e4395-272">Voor multiklassen klassificatieprobleem Hallo die worden beschreven in Hallo [voorbeelden van voorspelling taken](machine-learning-data-science-process-hive-walkthrough.md#mltasks) sectie deze gegevensset ook gepaard tooa natuurlijke classificatie waar willen we graag toopredict Hallo hoeveelheid Hallo tips gegeven.</span><span class="sxs-lookup"><span data-stu-id="e4395-272">For hello multiclass classification problem outlined in hello [Examples of prediction tasks](machine-learning-data-science-process-hive-walkthrough.md#mltasks) section this data set also lends itself tooa natural classification where we would like toopredict hello amount of hello tips given.</span></span> <span data-ttu-id="e4395-273">We kunnen opslaglocaties toodefine tip bereiken in Hallo query gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e4395-273">We can use bins toodefine tip ranges in hello query.</span></span> <span data-ttu-id="e4395-274">tooget Hallo klasse Distributies voor Hallo verschillende tip bereiken, gebruiken we Hallo *voorbeeld\_hive\_tip\_bereik\_frequencies.hql* bestand.</span><span class="sxs-lookup"><span data-stu-id="e4395-274">tooget hello class distributions for hello various tip ranges, we use hello *sample\_hive\_tip\_range\_frequencies.hql* file.</span></span> <span data-ttu-id="e4395-275">Hieronder vindt u de inhoud ervan.</span><span class="sxs-lookup"><span data-stu-id="e4395-275">Below are its contents.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq
    FROM
    (
        SELECT if(tip_amount=0, 0,
            if(tip_amount>0 and tip_amount<=5, 1,
            if(tip_amount>5 and tip_amount<=10, 2,
            if(tip_amount>10 and tip_amount<=20, 3, 4)))) as tip_class, tip_amount
        FROM nyctaxidb.fare
    )tc
    GROUP BY tip_class;

<span data-ttu-id="e4395-276">Voert de volgende opdracht uit vanaf de opdrachtregel Hadoop console Hallo:</span><span class="sxs-lookup"><span data-stu-id="e4395-276">Run hello following command from Hadoop Command Line console:</span></span>

    hive -f "C:\temp\sample_hive_tip_range_frequencies.hql"

### <a name="exploration-compute-direct-distance-between-two-longitude-latitude-locations"></a><span data-ttu-id="e4395-277">Exploratie: Compute Direct afstand tussen twee lengtegraad breedtegraad-locaties</span><span class="sxs-lookup"><span data-stu-id="e4395-277">Exploration: Compute Direct Distance Between Two Longitude-Latitude Locations</span></span>
> [!NOTE]
> <span data-ttu-id="e4395-278">Dit is doorgaans een **gegevens wetenschappelijk** taak.</span><span class="sxs-lookup"><span data-stu-id="e4395-278">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="e4395-279">Met een meting van Hallo direct afstand kunt ons toofind uit Hallo discrepantie is tussen deze en Hallo werkelijke krachtvoertuigen afstand.</span><span class="sxs-lookup"><span data-stu-id="e4395-279">Having a measure of hello direct distance allows us toofind out hello discrepancy between it and hello actual trip distance.</span></span> <span data-ttu-id="e4395-280">We deze functie stimuleren door wijzen dat een passagiers kleiner kan zijn waarschijnlijk tootip als ze dat stuurprogramma Hallo achterhalen ze opzettelijk heeft genomen door een veel langer route.</span><span class="sxs-lookup"><span data-stu-id="e4395-280">We motivate this feature by pointing out that a passenger might be less likely tootip if they figure out that hello driver has intentionally taken them by a much longer route.</span></span>

<span data-ttu-id="e4395-281">toosee hello vergelijking tussen de werkelijke reis afstand en Hallo [Haversine afstand](http://en.wikipedia.org/wiki/Haversine_formula) tussen twee lengtegraad breedtegraad punten (afstand Hallo 'groot cirkel'), gebruiken we Hallo trigonometrische functies beschikbaar binnen Hive, dus:</span><span class="sxs-lookup"><span data-stu-id="e4395-281">toosee hello comparison between actual trip distance and hello [Haversine distance](http://en.wikipedia.org/wiki/Haversine_formula) between two longitude-latitude points (hello "great circle" distance), we use hello trigonometric functions available within Hive, thus :</span></span>

    set R=3959;
    set pi=radians(180);

    insert overwrite directory 'wasb:///queryoutputdir'

    select pickup_longitude, pickup_latitude, dropoff_longitude, dropoff_latitude, trip_distance, trip_time_in_secs,
    ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
     *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
     *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
     /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
     +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*
     pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance
    from nyctaxidb.trip
    where month=1
    and pickup_longitude between -90 and -30
    and pickup_latitude between 30 and 90
    and dropoff_longitude between -90 and -30
    and dropoff_latitude between 30 and 90;

<span data-ttu-id="e4395-282">In bovenstaande Hallo query, R is Hallo radius Hallo Earth in mijl en pi geconverteerde tooradians is.</span><span class="sxs-lookup"><span data-stu-id="e4395-282">In hello query above, R is hello radius of hello Earth in miles, and pi is converted tooradians.</span></span> <span data-ttu-id="e4395-283">Houd er rekening mee dat Hallo lengtegraad breedtegraad punten zijn 'gefilterde' tooremove-waarden die verre Hallo NYC gebied zijn.</span><span class="sxs-lookup"><span data-stu-id="e4395-283">Note that hello longitude-latitude points are "filtered" tooremove values that are far from hello NYC area.</span></span>

<span data-ttu-id="e4395-284">In dit geval schrijven we onze resultaten tooa map met de naam 'queryoutputdir'.</span><span class="sxs-lookup"><span data-stu-id="e4395-284">In this case, we write our results tooa directory called "queryoutputdir".</span></span> <span data-ttu-id="e4395-285">Hallo reeks opdrachten die hieronder wordt weergegeven maakt eerst deze uitvoermap en Hallo Hive-opdracht wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e4395-285">hello sequence of commands shown below first creates this output directory, and then runs hello Hive command.</span></span>

<span data-ttu-id="e4395-286">Component van Hallo directory prompt, uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e4395-286">From hello Hive directory prompt, run:</span></span>

    hdfs dfs -mkdir wasb:///queryoutputdir

    hive -f "C:\temp\sample_hive_trip_direct_distance.hql"


<span data-ttu-id="e4395-287">Hallo queryresultaten worden geschreven too9 Azure blobs ***queryoutputdir/000000\_0*** te ***queryoutputdir/000008\_0*** onder de standaardcontainer Hallo van Hallo Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="e4395-287">hello query results are written too9 Azure blobs ***queryoutputdir/000000\_0*** too ***queryoutputdir/000008\_0*** under hello default container of hello Hadoop cluster.</span></span>

<span data-ttu-id="e4395-288">toosee hello grootte van afzonderlijke blobs hello, we Hallo volgende opdracht uit Hallo Hive directory prompt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="e4395-288">toosee hello size of hello individual blobs, we run hello following command from hello Hive directory prompt :</span></span>

    hdfs dfs -ls wasb:///queryoutputdir

<span data-ttu-id="e4395-289">toosee hello inhoud van een bepaald bestand spreken 000000\_0, gebruiken we de Hadoop `copyToLocal` opdracht dus.</span><span class="sxs-lookup"><span data-stu-id="e4395-289">toosee hello contents of a given file, say 000000\_0, we use Hadoop's `copyToLocal` command, thus.</span></span>

    hdfs dfs -copyToLocal wasb:///queryoutputdir/000000_0 C:\temp\tempfile

> [!WARNING]
> <span data-ttu-id="e4395-290">`copyToLocal`erg langzaam voor grote bestanden en wordt niet aanbevolen voor gebruik met deze.</span><span class="sxs-lookup"><span data-stu-id="e4395-290">`copyToLocal` can be very slow for large files, and is not recommended for use with them.</span></span>  
> 
> 

<span data-ttu-id="e4395-291">Een groot voordeel van deze gegevens zich bevinden in een Azure-blob is dat mogelijk besproken voor het Hallo-gegevens in Azure Machine Learning met Hallo [importgegevens] [ import-data] module.</span><span class="sxs-lookup"><span data-stu-id="e4395-291">A key advantage of having this data reside in an Azure blob is that we may explore hello data within Azure Machine Learning using hello [Import Data][import-data] module.</span></span>

## <span data-ttu-id="e4395-292"><a name="#downsample"></a>Omlaag gegevens en build samplemodellen in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e4395-292"><a name="#downsample"></a>Down sample data and build models in Azure Machine Learning</span></span>
> [!NOTE]
> <span data-ttu-id="e4395-293">Dit is doorgaans een **gegevens wetenschappelijk** taak.</span><span class="sxs-lookup"><span data-stu-id="e4395-293">This is typically a **Data Scientist** task.</span></span>
> 
> 

<span data-ttu-id="e4395-294">Na analysefase Hallo experimentele gegevens zijn er nu klaar toodown voorbeeldgegevens Hallo voor het bouwen van modellen in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e4395-294">After hello exploratory data analysis phase, we are now ready toodown sample hello data for building models in Azure Machine Learning.</span></span> <span data-ttu-id="e4395-295">In deze sectie laten we zien hoe toouse een Hive query toodown Hallo voorbeeldgegevens, die vervolgens toegankelijk is vanuit Hallo [importgegevens] [ import-data] -module in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e4395-295">In this section, we show how toouse a Hive query toodown sample hello data, which is then accessed from hello [Import Data][import-data] module in Azure Machine Learning.</span></span>

### <a name="down-sampling-hello-data"></a><span data-ttu-id="e4395-296">Omlaag steekproef nemen van Hallo-gegevens</span><span class="sxs-lookup"><span data-stu-id="e4395-296">Down sampling hello data</span></span>
<span data-ttu-id="e4395-297">Er zijn twee stappen in deze procedure.</span><span class="sxs-lookup"><span data-stu-id="e4395-297">There are two steps in this procedure.</span></span> <span data-ttu-id="e4395-298">Eerst we Hallo toevoegen **nyctaxidb.trip** en **nyctaxidb.fare** tabellen op de drie sleutels die aanwezig in alle records zijn: 'straten', ' inbreken\_licentie ', en "ophalen\_datetime-waarde '.</span><span class="sxs-lookup"><span data-stu-id="e4395-298">First we join hello **nyctaxidb.trip** and **nyctaxidb.fare** tables on three keys that are present in all records : "medallion", "hack\_license", and "pickup\_datetime".</span></span> <span data-ttu-id="e4395-299">Er vervolgens een label binaire classificatie gegenereerd **punt** en een label met meerdere klasse classificatie **tip\_klasse**.</span><span class="sxs-lookup"><span data-stu-id="e4395-299">We then generate a binary classification label **tipped** and a multi-class classification label **tip\_class**.</span></span>

<span data-ttu-id="e4395-300">toobe kunnen toouse Hallo omlaag steekproefgegevens rechtstreeks vanuit Hallo [importgegevens] [ import-data] module in Azure Machine Learning, is het nodig toostore Hallo resultaten van Hallo hierboven query tooan interne Hive-tabel.</span><span class="sxs-lookup"><span data-stu-id="e4395-300">toobe able toouse hello down sampled data directly from hello [Import Data][import-data] module in Azure Machine Learning, it is necessary toostore hello results of hello above query tooan internal Hive table.</span></span> <span data-ttu-id="e4395-301">In het volgende, we een interne Hive-tabel maken en de inhoud ervan te vullen met Hallo die lid zijn van en naar beneden steekproefgegevens.</span><span class="sxs-lookup"><span data-stu-id="e4395-301">In what follows, we create an internal Hive table and populate its contents with hello joined and down sampled data.</span></span>

<span data-ttu-id="e4395-302">Hallo query geldt Hive standaardfuncties rechtstreeks toogenerate Hallo uur van de dag, week van jaar werkdag (1 staat voor maandag en 7 staat voor zondag) van Hallo ' ophalen\_datetime ' veld en Hallo direct afstand tussen Hallo ophalen en dropoff locaties.</span><span class="sxs-lookup"><span data-stu-id="e4395-302">hello query applies standard Hive functions directly toogenerate hello hour of day, week of year, weekday (1 stands for Monday, and 7 stands for Sunday) from hello "pickup\_datetime" field,  and hello direct distance between hello pickup and dropoff locations.</span></span> <span data-ttu-id="e4395-303">Gebruikers kunnen verwijzen, te[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) voor een volledige lijst van deze functies.</span><span class="sxs-lookup"><span data-stu-id="e4395-303">Users can refer too[LanguageManual UDF](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+UDF) for a complete list of such functions.</span></span>

<span data-ttu-id="e4395-304">Hallo query daarna naar beneden voorbeelden Hallo gegevens zodat Hallo queryresultaten in hello Azure Machine Learning Studio inpassen kunnen.</span><span class="sxs-lookup"><span data-stu-id="e4395-304">hello query then down samples hello data so that hello query results can fit into hello Azure Machine Learning Studio.</span></span> <span data-ttu-id="e4395-305">Alleen ongeveer 1% van de oorspronkelijke gegevensset hello wordt geïmporteerd in Hallo Studio.</span><span class="sxs-lookup"><span data-stu-id="e4395-305">Only about 1% of hello original dataset is imported into hello Studio.</span></span>

<span data-ttu-id="e4395-306">Hieronder vindt u de inhoud Hallo van *voorbeeld\_hive\_voorbereiden\_voor\_aml\_full.hql* worden gegevens voorbereid voor model bouwen in Azure Machine Learning-bestand.</span><span class="sxs-lookup"><span data-stu-id="e4395-306">Below are hello contents of *sample\_hive\_prepare\_for\_aml\_full.hql* file that prepares data for model building in Azure Machine Learning.</span></span>

        set R = 3959;
        set pi=radians(180);

        create table if not exists nyctaxidb.nyctaxi_downsampled_dataset (

        medallion string,
        hack_license string,
        vendor_id string,
        rate_code string,
        store_and_fwd_flag string,
        pickup_datetime string,
        dropoff_datetime string,
        pickup_hour string,
        pickup_week string,
        weekday string,
        passenger_count int,
        trip_time_in_secs double,
        trip_distance double,
        pickup_longitude double,
        pickup_latitude double,
        dropoff_longitude double,
        dropoff_latitude double,
        direct_distance double,
        payment_type string,
        fare_amount double,
        surcharge double,
        mta_tax double,
        tip_amount double,
        tolls_amount double,
        total_amount double,
        tipped string,
        tip_class string
        )
        row format delimited fields terminated by ','
        lines terminated by '\n'
        stored as textfile;

        --- now insert contents of hello join into hello above internal table

        insert overwrite table nyctaxidb.nyctaxi_downsampled_dataset
        select
        t.medallion,
        t.hack_license,
        t.vendor_id,
        t.rate_code,
        t.store_and_fwd_flag,
        t.pickup_datetime,
        t.dropoff_datetime,
        hour(t.pickup_datetime) as pickup_hour,
        weekofyear(t.pickup_datetime) as pickup_week,
        from_unixtime(unix_timestamp(t.pickup_datetime, 'yyyy-MM-dd HH:mm:ss'),'u') as weekday,
        t.passenger_count,
        t.trip_time_in_secs,
        t.trip_distance,
        t.pickup_longitude,
        t.pickup_latitude,
        t.dropoff_longitude,
        t.dropoff_latitude,
        t.direct_distance,
        f.payment_type,
        f.fare_amount,
        f.surcharge,
        f.mta_tax,
        f.tip_amount,
        f.tolls_amount,
        f.total_amount,
        if(tip_amount>0,1,0) as tipped,
        if(tip_amount=0,0,
        if(tip_amount>0 and tip_amount<=5,1,
        if(tip_amount>5 and tip_amount<=10,2,
        if(tip_amount>10 and tip_amount<=20,3,4)))) as tip_class

        from
        (
        select
        medallion,
        hack_license,
        vendor_id,
        rate_code,
        store_and_fwd_flag,
        pickup_datetime,
        dropoff_datetime,
        passenger_count,
        trip_time_in_secs,
        trip_distance,
        pickup_longitude,
        pickup_latitude,
        dropoff_longitude,
        dropoff_latitude,
        ${hiveconf:R}*2*2*atan((1-sqrt(1-pow(sin((dropoff_latitude-pickup_latitude)
        *${hiveconf:pi}/180/2),2)-cos(pickup_latitude*${hiveconf:pi}/180)
        *cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2)))
        /sqrt(pow(sin((dropoff_latitude-pickup_latitude)*${hiveconf:pi}/180/2),2)
        +cos(pickup_latitude*${hiveconf:pi}/180)*cos(dropoff_latitude*${hiveconf:pi}/180)*pow(sin((dropoff_longitude-pickup_longitude)*${hiveconf:pi}/180/2),2))) as direct_distance,
        rand() as sample_key

        from nyctaxidb.trip
        where pickup_latitude between 30 and 90
            and pickup_longitude between -90 and -30
            and dropoff_latitude between 30 and 90
            and dropoff_longitude between -90 and -30
        )t
        join
        (
        select
        medallion,
        hack_license,
        vendor_id,
        pickup_datetime,
        payment_type,
        fare_amount,
        surcharge,
        mta_tax,
        tip_amount,
        tolls_amount,
        total_amount
        from nyctaxidb.fare
        )f
        on t.medallion=f.medallion and t.hack_license=f.hack_license and t.pickup_datetime=f.pickup_datetime
        where t.sample_key<=0.01

<span data-ttu-id="e4395-307">toorun deze query uit Hallo Hive directory vragen:</span><span class="sxs-lookup"><span data-stu-id="e4395-307">toorun this query, from hello Hive directory prompt :</span></span>

    hive -f "C:\temp\sample_hive_prepare_for_aml_full.hql"

<span data-ttu-id="e4395-308">Nu er een interne tabel 'nyctaxidb.nyctaxi_downsampled_dataset', wat kan worden geopend met behulp van Hallo [importgegevens] [ import-data] module op basis van Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e4395-308">We now have an internal table "nyctaxidb.nyctaxi_downsampled_dataset" which can be accessed using hello [Import Data][import-data] module from Azure Machine Learning.</span></span> <span data-ttu-id="e4395-309">We kunnen deze gegevensset bovendien gebruiken voor het bouwen van Machine Learning-modellen.</span><span class="sxs-lookup"><span data-stu-id="e4395-309">Furthermore, we may use this dataset for building Machine Learning models.</span></span>  

### <a name="use-hello-import-data-module-in-azure-machine-learning-tooaccess-hello-down-sampled-data"></a><span data-ttu-id="e4395-310">Hallo gegevens importeren-module gebruiken in Azure Machine Learning tooaccess Hallo omlaag steekproefgegevens</span><span class="sxs-lookup"><span data-stu-id="e4395-310">Use hello Import Data module in Azure Machine Learning tooaccess hello down sampled data</span></span>
<span data-ttu-id="e4395-311">Vereisten voor het uitgeven van Hive-query's in Hallo [importgegevens] [ import-data] -module van Azure Machine Learning, moeten we tooan Azure Machine Learning-werkruimte te openen en toegang tot de referenties toohello Hallo cluster en de bijbehorende opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="e4395-311">As prerequisites for issuing Hive queries in hello [Import Data][import-data] module of Azure Machine Learning, we need access tooan Azure Machine Learning workspace and access toohello credentials of hello cluster and its associated storage account.</span></span>

<span data-ttu-id="e4395-312">Sommige gegevens op Hallo [importgegevens] [ import-data] module en Hallo parameters tooinput:</span><span class="sxs-lookup"><span data-stu-id="e4395-312">Some details on hello [Import Data][import-data] module and hello parameters tooinput :</span></span>

<span data-ttu-id="e4395-313">**HCatalog server-URI**: als Hallo clusternaam abc123, wordt dit eenvoudig is: https://abc123.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="e4395-313">**HCatalog server URI**: If hello cluster name is abc123, then this is simply : https://abc123.azurehdinsight.net</span></span>

<span data-ttu-id="e4395-314">**Hadoop-gebruikersaccountnaam** : gebruikersnaam Hallo gekozen voor Hallo-cluster (**niet** Hallo RAS-gebruikersnaam)</span><span class="sxs-lookup"><span data-stu-id="e4395-314">**Hadoop user account name** : hello user name chosen for hello cluster (**not** hello remote access user name)</span></span>

<span data-ttu-id="e4395-315">**Hadoop ser accountwachtwoord** : Hallo wachtwoord gekozen voor Hallo-cluster (**niet** Hallo-wachtwoord voor externe toegang)</span><span class="sxs-lookup"><span data-stu-id="e4395-315">**Hadoop ser account password** : hello password chosen for hello cluster (**not** hello remote access password)</span></span>

<span data-ttu-id="e4395-316">**Locatie van uitvoergegevens** : dit toobe Azure is gekozen.</span><span class="sxs-lookup"><span data-stu-id="e4395-316">**Location of output data** : This is chosen toobe Azure.</span></span>

<span data-ttu-id="e4395-317">**Naam van het Azure-opslagaccount** : naam van Hallo standaardopslagaccount die zijn gekoppeld aan het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="e4395-317">**Azure storage account name** : Name of hello default storage account associated with hello cluster.</span></span>

<span data-ttu-id="e4395-318">**Azure containernaam** : dit Hallo standaard containernaam voor Hallo-cluster is en wordt dezelfde doorgaans als clusternaam Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="e4395-318">**Azure container name** : This is hello default container name for hello cluster, and is typically hello same as hello cluster name.</span></span> <span data-ttu-id="e4395-319">Voor een cluster 'abc123' genoemd, is dit alleen abc123.</span><span class="sxs-lookup"><span data-stu-id="e4395-319">For a cluster called "abc123", this is just abc123.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4395-320">**Een tabel die we willen tooquery Hallo met [importgegevens] [ import-data] module in Azure Machine Learning een interne tabel moet zijn.**</span><span class="sxs-lookup"><span data-stu-id="e4395-320">**Any table we wish tooquery using hello [Import Data][import-data] module in Azure Machine Learning must be an internal table.**</span></span> <span data-ttu-id="e4395-321">Een tip om te bepalen of een tabel T in een database D.db een interne tabel is is als volgt.</span><span class="sxs-lookup"><span data-stu-id="e4395-321">A tip for determining if a table T in a database D.db is an internal table is as follows.</span></span>
> 
> 

<span data-ttu-id="e4395-322">Component van Hallo directory prompt probleem Hallo-opdracht:</span><span class="sxs-lookup"><span data-stu-id="e4395-322">From hello Hive directory prompt, issue hello command :</span></span>

    hdfs dfs -ls wasb:///D.db/T

<span data-ttu-id="e4395-323">Als Hallo-tabel een interne tabel is en dit ingevuld, wordt de inhoud moeten hier weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e4395-323">If hello table is an internal table and it is populated, its contents must show here.</span></span> <span data-ttu-id="e4395-324">Een andere manier toodetermine toouse hello Azure Storage Explorer of een tabel een interne tabel is is.</span><span class="sxs-lookup"><span data-stu-id="e4395-324">Another way toodetermine whether a table is an internal table is toouse hello Azure Storage Explorer.</span></span> <span data-ttu-id="e4395-325">Gebruik deze toonavigate toohello standaard containernaam van Hallo cluster en vervolgens filteren op Hallo tabelnaam.</span><span class="sxs-lookup"><span data-stu-id="e4395-325">Use it toonavigate toohello default container name of hello cluster, and then filter by hello table name.</span></span> <span data-ttu-id="e4395-326">Als Hallo tabel en de inhoud ervan wordt getoond, bevestigt dit dat het is een interne tabel.</span><span class="sxs-lookup"><span data-stu-id="e4395-326">If hello table and its contents show up, this confirms that it is an internal table.</span></span>

<span data-ttu-id="e4395-327">Hier volgt een momentopname van Hallo Hive-query en Hallo [importgegevens] [ import-data] module:</span><span class="sxs-lookup"><span data-stu-id="e4395-327">Here is a snapshot of hello Hive query and hello [Import Data][import-data] module:</span></span>

![Hive-query voor gegevens importeren-module](./media/machine-learning-data-science-process-hive-walkthrough/1eTYf52.png)

<span data-ttu-id="e4395-329">Sinds onze omlaag steekproefgegevens bevindt zich in de standaardcontainer hello, Hallo resulterende Hive-query uit Azure Machine Learning is zeer eenvoudig en is alleen een "Selecteer * uit nyctaxidb.nyctaxi\_verkleind\_gegevens '.</span><span class="sxs-lookup"><span data-stu-id="e4395-329">Note that since our down sampled data resides in hello default container, hello resulting Hive query from Azure Machine Learning is very simple and is just a "SELECT * FROM nyctaxidb.nyctaxi\_downsampled\_data".</span></span>

<span data-ttu-id="e4395-330">Hallo dataset kan nu worden gebruikt als startpunt voor het bouwen van Machine Learning-modellen Hallo.</span><span class="sxs-lookup"><span data-stu-id="e4395-330">hello dataset may now be used as hello starting point for building Machine Learning models.</span></span>

### <span data-ttu-id="e4395-331"><a name="mlmodel"></a>Bouwen van modellen in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="e4395-331"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="e4395-332">Er wordt nu kunnen tooproceed toomodel gebouw en implementatie van het model in [Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="e4395-332">We are now able tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="e4395-333">Hallo-gegevens is gereed voor ons toouse in Hallo voorspelling problemen hierboven adressering:</span><span class="sxs-lookup"><span data-stu-id="e4395-333">hello data is ready for us toouse in addressing hello prediction problems identified above:</span></span>

<span data-ttu-id="e4395-334">**1. Binaire classificatie**: toopredict al dan niet een tip voor een zakenreis is betaald.</span><span class="sxs-lookup"><span data-stu-id="e4395-334">**1. Binary classification**: toopredict whether or not a tip was paid for a trip.</span></span>

<span data-ttu-id="e4395-335">**Cursist gebruikt:** Two-class logistic regression</span><span class="sxs-lookup"><span data-stu-id="e4395-335">**Learner used:** Two-class logistic regression</span></span>

<span data-ttu-id="e4395-336">a.</span><span class="sxs-lookup"><span data-stu-id="e4395-336">a.</span></span> <span data-ttu-id="e4395-337">Voor dit probleem op door is onze label doel (of een klasse) "punt".</span><span class="sxs-lookup"><span data-stu-id="e4395-337">For this problem, our target (or class) label is "tipped".</span></span> <span data-ttu-id="e4395-338">Onze oorspronkelijke omlaag actieve gegevensset heeft een aantal kolommen die doel lekken voor dit experiment classificatie.</span><span class="sxs-lookup"><span data-stu-id="e4395-338">Our original down-sampled dataset has a few columns that are target leaks for this classification experiment.</span></span> <span data-ttu-id="e4395-339">Met name: tip\_klasse, tip\_bedrag en totaal\_bedrag onthullen informatie over Hallo doellabel dat is niet beschikbaar voor het testen van tijd.</span><span class="sxs-lookup"><span data-stu-id="e4395-339">In particular : tip\_class, tip\_amount, and total\_amount reveal information about hello target label that is not available at testing time.</span></span> <span data-ttu-id="e4395-340">We deze kolommen verwijderen uit met behulp van Hallo overweging [Select Columns in Dataset] [ select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="e4395-340">We remove these columns from consideration using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="e4395-341">Hallo momentopname hieronder ziet u onze toopredict experiment al dan niet een tip voor een bepaalde reis is betaald.</span><span class="sxs-lookup"><span data-stu-id="e4395-341">hello snapshot below shows our experiment toopredict whether or not a tip was paid for a given trip.</span></span>

![Experiment momentopname](./media/machine-learning-data-science-process-hive-walkthrough/QGxRz5A.png)

<span data-ttu-id="e4395-343">b.</span><span class="sxs-lookup"><span data-stu-id="e4395-343">b.</span></span> <span data-ttu-id="e4395-344">Ons doel label distributies zijn voor dit experiment ongeveer 1:1.</span><span class="sxs-lookup"><span data-stu-id="e4395-344">For this experiment, our target label distributions were roughly 1:1.</span></span>

<span data-ttu-id="e4395-345">Hallo momentopname hieronder toont de distributie Hallo van tip klasse labels voor Hallo binair klassificatieprobleem.</span><span class="sxs-lookup"><span data-stu-id="e4395-345">hello snapshot below shows hello distribution of tip class labels for hello binary classification problem.</span></span>

![Distributie van tip klasse labels](./media/machine-learning-data-science-process-hive-walkthrough/9mM4jlD.png)

<span data-ttu-id="e4395-347">Als gevolg hiervan krijgen we een AUC van 0.987 zoals weergegeven in onderstaande afbeelding ziet Hallo.</span><span class="sxs-lookup"><span data-stu-id="e4395-347">As a result, we obtain an AUC of 0.987 as shown in hello figure below.</span></span>

![AUC waarde](./media/machine-learning-data-science-process-hive-walkthrough/8JDT0F8.png)

<span data-ttu-id="e4395-349">**2. Multiklassen classificatie**: toopredict Hallo bereik van tip bedragen betaald Hallo reis Hallo eerder gebruikte klassen gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="e4395-349">**2. Multiclass classification**: toopredict hello range of tip amounts paid for hello trip, using hello previously defined classes.</span></span>

<span data-ttu-id="e4395-350">**Cursist gebruikt:** Multiklassen logistic regression</span><span class="sxs-lookup"><span data-stu-id="e4395-350">**Learner used:** Multiclass logistic regression</span></span>

<span data-ttu-id="e4395-351">a.</span><span class="sxs-lookup"><span data-stu-id="e4395-351">a.</span></span> <span data-ttu-id="e4395-352">Voor dit probleem op door het label voor onze doel (of een klasse) is ' tip\_klasse ' die kan duren voordat een van vijf waarden (0,1,2,3,4).</span><span class="sxs-lookup"><span data-stu-id="e4395-352">For this problem, our target (or class) label is "tip\_class" which can take one of five values (0,1,2,3,4).</span></span> <span data-ttu-id="e4395-353">Net als bij Hallo binaire classificatie hebben we enkele kolommen die doel lekken voor dit experiment.</span><span class="sxs-lookup"><span data-stu-id="e4395-353">As in hello binary classification case, we have a few columns that are target leaks for this experiment.</span></span> <span data-ttu-id="e4395-354">Met name: punt, tip\_bedrag totale\_bedrag onthullen informatie over Hallo doellabel dat is niet beschikbaar voor het testen van tijd.</span><span class="sxs-lookup"><span data-stu-id="e4395-354">In particular : tipped, tip\_amount, total\_amount reveal information about hello target label that is not available at testing time.</span></span> <span data-ttu-id="e4395-355">Verwijderen we deze kolommen met Hallo [Select Columns in Dataset] [ select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="e4395-355">We remove these columns using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="e4395-356">Hallo momentopname hieronder bevat onze experiment toopredict in welke opslaglocatie een tip waarschijnlijk toofall is (klasse 0: tip = $0, 1 klasse: tip > $0 en tip < = $5, klasse 2: tip > $5 en tip < = $10, klasse 3: tip > $10 en tip < = $20 Klasse 4: tip > $20)</span><span class="sxs-lookup"><span data-stu-id="e4395-356">hello snapshot below shows our experiment toopredict in which bin a tip is likely toofall ( Class 0: tip = $0, class 1 : tip > $0 and tip <= $5, Class 2 : tip > $5 and tip <= $10, Class 3 : tip > $10 and tip <= $20, Class 4 : tip > $20)</span></span>

![Experiment momentopname](./media/machine-learning-data-science-process-hive-walkthrough/5ztv0n0.png)

<span data-ttu-id="e4395-358">Nu zien hoe de distributie van onze werkelijke test klasse eruit ziet.</span><span class="sxs-lookup"><span data-stu-id="e4395-358">We now show what our actual test class distribution looks like.</span></span> <span data-ttu-id="e4395-359">Zien we dat klasse 0 en 1 van de klasse gangbare zijn, hello andere klassen zijn zeldzame.</span><span class="sxs-lookup"><span data-stu-id="e4395-359">We see that while Class 0 and Class 1 are prevalent, hello other classes are rare.</span></span>

![Klasse distributie testen](./media/machine-learning-data-science-process-hive-walkthrough/Vy1FUKa.png)

<span data-ttu-id="e4395-361">b.</span><span class="sxs-lookup"><span data-stu-id="e4395-361">b.</span></span> <span data-ttu-id="e4395-362">We gebruiken een matrix verwarring toolook op onze accuratesse voorspelling voor dit experiment.</span><span class="sxs-lookup"><span data-stu-id="e4395-362">For this experiment, we use a confusion matrix toolook at our prediction accuracies.</span></span> <span data-ttu-id="e4395-363">Dit wordt hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="e4395-363">This is shown below.</span></span>

![Verwarring matrix](./media/machine-learning-data-science-process-hive-walkthrough/cxFmErM.png)

<span data-ttu-id="e4395-365">Houd er rekening mee dat hoewel onze accuratesse klasse op Hallo gangbare klassen behoorlijk geschikt, Hallo model wordt niet goed werk 'learning' op Hallo zeldzame klassen.</span><span class="sxs-lookup"><span data-stu-id="e4395-365">Note that while our class accuracies on hello prevalent classes is quite good, hello model does not do a good job of "learning" on hello rarer classes.</span></span>

<span data-ttu-id="e4395-366">**3. Regressie taak**: toopredict Hallo hoeveelheid tip voor een reis betaald.</span><span class="sxs-lookup"><span data-stu-id="e4395-366">**3. Regression task**: toopredict hello amount of tip paid for a trip.</span></span>

<span data-ttu-id="e4395-367">**Cursist gebruikt:** Boosted decision tree</span><span class="sxs-lookup"><span data-stu-id="e4395-367">**Learner used:** Boosted decision tree</span></span>

<span data-ttu-id="e4395-368">a.</span><span class="sxs-lookup"><span data-stu-id="e4395-368">a.</span></span> <span data-ttu-id="e4395-369">Voor dit probleem op door het label voor onze doel (of een klasse) is ' tip\_bedrag '.</span><span class="sxs-lookup"><span data-stu-id="e4395-369">For this problem, our target (or class) label is "tip\_amount".</span></span> <span data-ttu-id="e4395-370">Ons doel lekken in dit geval zijn: punt, tip\_klasse, totale\_bedrag; deze variabelen die zijn op basis van informatie over Hallo tip hoeveelheid die doorgaans niet beschikbaar voor het testen van tijd duidelijk.</span><span class="sxs-lookup"><span data-stu-id="e4395-370">Our target leaks in this case are : tipped, tip\_class, total\_amount ; all these variables reveal information about hello tip amount that is typically unavailable at testing time.</span></span> <span data-ttu-id="e4395-371">Verwijderen we deze kolommen met Hallo [Select Columns in Dataset] [ select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="e4395-371">We remove these columns using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="e4395-372">Hallo momentopname belows bevat onze experiment toopredict Hallo hoeveelheid Hallo tip gegeven.</span><span class="sxs-lookup"><span data-stu-id="e4395-372">hello snapshot belows shows our experiment toopredict hello amount of hello given tip.</span></span>

![Experiment momentopname](./media/machine-learning-data-science-process-hive-walkthrough/11TZWgV.png)

<span data-ttu-id="e4395-374">b.</span><span class="sxs-lookup"><span data-stu-id="e4395-374">b.</span></span> <span data-ttu-id="e4395-375">Regressie problemen, we Hallo accuratesse van onze voorspelling meten door te kijken Hallo kwadraat fout in Hallo voorspellingen Hallo determinatiecoëfficiënt en Hallo zoals.</span><span class="sxs-lookup"><span data-stu-id="e4395-375">For regression problems, we measure hello accuracies of our prediction by looking at hello squared error in hello predictions, hello coefficient of determination, and hello like.</span></span> <span data-ttu-id="e4395-376">We weergegeven deze hieronder.</span><span class="sxs-lookup"><span data-stu-id="e4395-376">We show these below.</span></span>

![Voorspelling statistieken](./media/machine-learning-data-science-process-hive-walkthrough/Jat9mrz.png)

<span data-ttu-id="e4395-378">Zien we dat de determinatiecoëfficiënt over Hallo 0.709, is door onze coëfficiënten model: de overdracht van ongeveer 71% van de variantie hello wordt uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="e4395-378">We see that about hello coefficient of determination is 0.709, implying about 71% of hello variance is explained by our model coefficients.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e4395-379">meer informatie over Azure Machine Learning toolearn en hoe tooaccess en deze gebruiken, raadpleegt u te[wat is Machine Learning?](machine-learning-what-is-machine-learning.md).</span><span class="sxs-lookup"><span data-stu-id="e4395-379">toolearn more about Azure Machine Learning and how tooaccess and use it, please refer too[What's Machine Learning?](machine-learning-what-is-machine-learning.md).</span></span> <span data-ttu-id="e4395-380">Een zeer nuttig resource voor het afspelen van met een aantal Machine Learning-experimenten in Azure Machine Learning is Hallo [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/).</span><span class="sxs-lookup"><span data-stu-id="e4395-380">A very useful resource for playing with a bunch of Machine Learning experiments on Azure Machine Learning is hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/).</span></span> <span data-ttu-id="e4395-381">Hallo-galerie bevat informatie over een kleurenbereik van experimenten en biedt een uitgebreide inleiding in Hallo scala aan mogelijkheden van Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="e4395-381">hello Gallery covers a gamut of experiments and provides a thorough introduction into hello range of capabilities of Azure Machine Learning.</span></span>
> 
> 

## <a name="license-information"></a><span data-ttu-id="e4395-382">Licentie-informatie</span><span class="sxs-lookup"><span data-stu-id="e4395-382">License Information</span></span>
<span data-ttu-id="e4395-383">In dit voorbeeld scenario en de bijbehorende scripts worden gedeeld door Microsoft onder Hallo MIT-licentie.</span><span class="sxs-lookup"><span data-stu-id="e4395-383">This sample walkthrough and its accompanying scripts are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="e4395-384">Controleer de Hallo LICENSE.txt bestand in de directory Hallo van Hallo voorbeeldcode op GitHub voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e4395-384">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="e4395-385">Verwijzingen</span><span class="sxs-lookup"><span data-stu-id="e4395-385">References</span></span>
<span data-ttu-id="e4395-386">• [Andrés Monroy NYC Taxi reizen downloadpagina](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="e4395-386">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="e4395-387">• [FOILing NYC Taxi reis gegevens door Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="e4395-387">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="e4395-388">• [NYC Taxi en Limousine Commissie onderzoek en statistieken](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="e4395-388">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[2]: ./media/machine-learning-data-science-process-hive-walkthrough/output-hive-results-3.png
[11]: ./media/machine-learning-data-science-process-hive-walkthrough/hive-reader-properties.png
[12]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-training.png
[13]: ./media/machine-learning-data-science-process-hive-walkthrough/create-scoring-experiment.png
[14]: ./media/machine-learning-data-science-process-hive-walkthrough/binary-classification-scoring.png
[15]: ./media/machine-learning-data-science-process-hive-walkthrough/amlreader.png

<!-- Module References -->
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
