---
title: aaaBuild en implementeren van een machine learning-model met SQL Server op een virtuele machine in Azure | Microsoft-Docs
description: Geavanceerde analyses proces en de technologie in actie
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6066b083-262c-4453-a712-a5c05acc3df8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: fashah;bradsev
ms.openlocfilehash: 30ba9a9e3cf65f75015e13f9c7876dcbccc5bc47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-server"></a><span data-ttu-id="bf1ff-103">Hallo Team gegevens wetenschappelijke processen in actie: met behulp van SQL Server</span><span class="sxs-lookup"><span data-stu-id="bf1ff-103">hello Team Data Science Process in action: using SQL Server</span></span>
<span data-ttu-id="bf1ff-104">In deze zelfstudie helpt u bij het Hallo-proces voor het maken en implementeren van een machine learning-model met behulp van SQL Server en een openbare gegevensset--hello [NYC Taxi reizen](http://www.andresmh.com/nyctaxitrips/) gegevensset.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-104">In this tutorial, you walk through hello process of building and deploying a machine learning model using SQL Server and a publicly available dataset -- hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="bf1ff-105">Hallo procedure volgt een standaard wetenschappelijke werkstroom: opnemen en Hallo gegevens verkennen, functies toofacilitate learning, engineering en vervolgens bouwen en implementeren van een model.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-105">hello procedure follows a standard data science workflow: ingest and explore hello data, engineer features toofacilitate learning, then build and deploy a model.</span></span>

## <span data-ttu-id="bf1ff-106"><a name="dataset"></a>NYC Taxi reizen gegevensset beschrijving</span><span class="sxs-lookup"><span data-stu-id="bf1ff-106"><a name="dataset"></a>NYC Taxi Trips Dataset Description</span></span>
<span data-ttu-id="bf1ff-107">Hallo NYC Taxi reis gegevens is ongeveer 20GB gecomprimeerde CSV-bestanden (~ 48GB ongecomprimeerde), die bestaat uit meer dan 173 miljoen afzonderlijke reizen en Hallo ervoor staat voor elke reis betaald.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-107">hello NYC Taxi Trip data is about 20GB of compressed CSV files (~48GB uncompressed), comprising more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="bf1ff-108">Elke record reis omvat Hallo ophalen en inleverbibliotheek locatie en tijd, geanonimiseerde hack (van stuurprogramma) licentienummer en nummer straten (taxi van unieke id).</span><span class="sxs-lookup"><span data-stu-id="bf1ff-108">Each trip record includes hello pickup and drop-off location and time, anonymized hack (driver's) license number and medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="bf1ff-109">Hallo-gegevens bevat informatie over alle reizen Hallo jaar 2013 en is beschikbaar in twee gegevenssets voor elke maand na Hallo:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-109">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="bf1ff-110">Hallo 'trip_data' CSV bevat reis details, zoals het aantal passagiers, ophalen en dropoff punten reis duur en duur van reis.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-110">hello 'trip_data' CSV contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="bf1ff-111">Hier volgen enkele voorbeeldrecords:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-111">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="bf1ff-112">Hello trip_fare CSV details van Hallo tarief betaald voor elke reis, zoals betalingstype tarief bedrag, extra kosten en belastingen, tips en tolgelden en Hallo totaalbedrag betaald bevat.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-112">hello 'trip_fare' CSV contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="bf1ff-113">Hier volgen enkele voorbeeldrecords:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-113">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="bf1ff-114">Hallo unieke sleutel toojoin reis\_gegevens en reis\_tarief dat bestaat uit Hallo velden: straten, hack\_en ophalen van certificaat\_datetime.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-114">hello unique key toojoin trip\_data and trip\_fare is composed of hello fields: medallion, hack\_licence and pickup\_datetime.</span></span>

## <span data-ttu-id="bf1ff-115"><a name="mltasks"></a>Voorbeelden van voorspelling taken</span><span class="sxs-lookup"><span data-stu-id="bf1ff-115"><a name="mltasks"></a>Examples of Prediction Tasks</span></span>
<span data-ttu-id="bf1ff-116">We drie voorspelling problemen op basis van Hallo wordt formuleren *tip\_bedrag*, namelijk:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-116">We will formulate three prediction problems based on hello *tip\_amount*, namely:</span></span>

1. <span data-ttu-id="bf1ff-117">Binaire classificatie: voorspellen of een tip betaald is voor een reis, dat wil zeggen een *tip\_bedrag* die groter is dan $0 een voorbeeld van een positieve is, terwijl een *tip\_bedrag* van $0 is een voorbeeld van een negatief.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-117">Binary classification: Predict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="bf1ff-118">Multiklassen classificatie: toopredict Hallo bereik van een tip voor Hallo reis betaald.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-118">Multiclass classification: toopredict hello range of tip paid for hello trip.</span></span> <span data-ttu-id="bf1ff-119">We delen Hallo *tip\_bedrag* in vijf opslaglocaties of klassen:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-119">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="bf1ff-120">Taak regressie: toopredict Hallo hoeveelheid tip voor een reis betaald.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-120">Regression task: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="bf1ff-121"><a name="setup"></a>Instellen hello Azure gegevens wetenschappelijke omgeving voor geavanceerde analyses</span><span class="sxs-lookup"><span data-stu-id="bf1ff-121"><a name="setup"></a>Setting Up hello Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="bf1ff-122">Zoals u van Hallo zien kunt [uw omgeving plannen](machine-learning-data-science-plan-your-environment.md) handleiding, er zijn verschillende opties toowork met Hallo NYC Taxi reizen gegevensset in Azure:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-122">As you can see from hello [Plan Your Environment](machine-learning-data-science-plan-your-environment.md) guide, there are several options toowork with hello NYC Taxi Trips dataset in Azure:</span></span>

* <span data-ttu-id="bf1ff-123">Werken met gegevens in Azure blobs Hallo vervolgens Azure Machine Learning-model</span><span class="sxs-lookup"><span data-stu-id="bf1ff-123">Work with hello data in Azure blobs then model in Azure Machine Learning</span></span>
* <span data-ttu-id="bf1ff-124">Hallo gegevens laden in een SQL Server-database en de Azure Machine Learning-model</span><span class="sxs-lookup"><span data-stu-id="bf1ff-124">Load hello data into a SQL Server database then model in Azure Machine Learning</span></span>

<span data-ttu-id="bf1ff-125">In deze zelfstudie wordt gedemonstreerd parallelle bulkimport van Hallo gegevens tooa SQL Server, gegevensverkenning, functie engineering en omlaag sampling met behulp van SQL Server Management Studio, alsmede IPython laptop gebruiken.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-125">In this tutorial we will demonstrate parallel bulk import of hello data tooa SQL Server, data exploration, feature engineering and down sampling using SQL Server Management Studio as well as using IPython Notebook.</span></span> <span data-ttu-id="bf1ff-126">[Voorbeeld van scripts](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) en [IPython notitieblokken](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) in GitHub worden gedeeld.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-126">[Sample scripts](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/DataScienceScripts) and [IPython notebooks](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks) are shared in GitHub.</span></span> <span data-ttu-id="bf1ff-127">Een voorbeeld IPython notebook toowork met Hallo-gegevens in Azure BLOB's is ook beschikbaar in Hallo dezelfde locatie.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-127">A sample IPython notebook toowork with hello data in Azure blobs is also available in hello same location.</span></span>

<span data-ttu-id="bf1ff-128">tooset van uw omgeving voor Gegevenswetenschap Azure:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-128">tooset up your Azure Data Science environment:</span></span>

1. [<span data-ttu-id="bf1ff-129">Een opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="bf1ff-129">Create a storage account</span></span>](../storage/common/storage-create-storage-account.md)
2. [<span data-ttu-id="bf1ff-130">Een Azure Machine Learning-werkruimte maken</span><span class="sxs-lookup"><span data-stu-id="bf1ff-130">Create an Azure Machine Learning workspace</span></span>](machine-learning-create-workspace.md)
3. <span data-ttu-id="bf1ff-131">[Inrichten van een virtuele Machine van de gegevens wetenschappelijke](machine-learning-data-science-setup-sql-server-virtual-machine.md), waarmee u een SQL-Server en een IPython laptop-server.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-131">[Provision a Data Science Virtual Machine](machine-learning-data-science-setup-sql-server-virtual-machine.md), which provides a SQL Server and an IPython Notebook server.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bf1ff-132">Hallo-voorbeeldscripts en IPython notitieblokken gedownloade tooyour Gegevenswetenschap virtuele machine worden tijdens het installatieproces Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-132">hello sample scripts and IPython notebooks will be downloaded tooyour Data Science virtual machine during hello setup process.</span></span> <span data-ttu-id="bf1ff-133">Wanneer Hallo VM-script voor na de installatie is voltooid, zijn Hallo voorbeelden in de bibliotheek documenten van de VM:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-133">When hello VM post-installation script completes, hello samples will be in your VM's Documents library:</span></span>  
   > 
   > * <span data-ttu-id="bf1ff-134">Voorbeeld Scripts:`C:\Users\<user_name>\Documents\Data Science Scripts`</span><span class="sxs-lookup"><span data-stu-id="bf1ff-134">Sample Scripts: `C:\Users\<user_name>\Documents\Data Science Scripts`</span></span>  
   > * <span data-ttu-id="bf1ff-135">Voorbeeld IPython notitieblokken:`C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span><span class="sxs-lookup"><span data-stu-id="bf1ff-135">Sample IPython Notebooks: `C:\Users\<user_name>\Documents\IPython Notebooks\DataScienceSamples`</span></span>  
   >   <span data-ttu-id="bf1ff-136">waar `<user_name>` is Windows-aanmeldingsnaam van de VM.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-136">where `<user_name>` is your VM's Windows login name.</span></span> <span data-ttu-id="bf1ff-137">Toohello voorbeeld mappen als wordt verwezen **voorbeeldscripts** en **voorbeeld IPython notitieblokken**.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-137">We will refer toohello sample folders as **Sample Scripts** and **Sample IPython Notebooks**.</span></span>
   > 
   > 

<span data-ttu-id="bf1ff-138">Op basis van Hallo gegevensset grootte, de locatie van de gegevensbron en Hallo geselecteerde Azure doelomgeving, dit scenario is vergelijkbaar te[Scenario \#5: grote gegevensset in een lokale bestanden doel-SQL-Server in Azure VM](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span><span class="sxs-lookup"><span data-stu-id="bf1ff-138">Based on hello dataset size, data source location, and hello selected Azure target environment, this scenario is similar too[Scenario \#5: Large dataset in a local files, target SQL Server in Azure VM](machine-learning-data-science-plan-sample-scenarios.md#largelocaltodb).</span></span>

## <span data-ttu-id="bf1ff-139"><a name="getdata"></a>Hallo gegevens ophalen uit de openbare bron</span><span class="sxs-lookup"><span data-stu-id="bf1ff-139"><a name="getdata"></a>Get hello Data from Public Source</span></span>
<span data-ttu-id="bf1ff-140">Hallo tooget [NYC Taxi reizen](http://www.andresmh.com/nyctaxitrips/) gegevensset van de openbare locatie, mag u Hallo-methoden die zijn beschreven in [gegevens verplaatsen tooand uit Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) toocopy Hallo gegevens tooyour nieuwe virtuele machine.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-140">tooget hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset from its public location, you may use any of hello methods described in [Move Data tooand from Azure Blob Storage](machine-learning-data-science-move-azure-blob.md) toocopy hello data tooyour new virtual machine.</span></span>

<span data-ttu-id="bf1ff-141">toocopy hello gegevens met behulp van AzCopy:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-141">toocopy hello data using AzCopy:</span></span>

1. <span data-ttu-id="bf1ff-142">Meld u bij tooyour virtuele machine (VM)</span><span class="sxs-lookup"><span data-stu-id="bf1ff-142">Log in tooyour virtual machine (VM)</span></span>
2. <span data-ttu-id="bf1ff-143">Een nieuwe map maken in de gegevensschijf Hallo van de virtuele machine (Opmerking: gebruik geen tijdelijke schijf die wordt geleverd bij de virtuele machine als een gegevensschijf Hallo Hallo).</span><span class="sxs-lookup"><span data-stu-id="bf1ff-143">Create a new directory in hello VM's data disk (Note: Do not use hello Temporary Disk which comes with hello VM as a Data Disk).</span></span>
3. <span data-ttu-id="bf1ff-144">Voer Hallo Azcopy-opdrachtregel de volgende, waarbij < path_to_data_folder > vervangt door de gegevensmap van uw in (2) gemaakt in een opdrachtpromptvenster:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-144">In a Command Prompt window, run hello following Azcopy command line, replacing <path_to_data_folder> with your data folder created in (2):</span></span>
   
        "C:\Program Files (x86)\Microsoft SDKs\Azure\AzCopy\azcopy" /Source:https://nyctaxitrips.blob.core.windows.net/data /Dest:<path_to_data_folder> /S
   
    <span data-ttu-id="bf1ff-145">Wanneer Hallo AzCopy is voltooid, in totaal 24 ingepakte CSV-bestanden (12 voor reis\_gegevens en 12 voor reis\_tarief) moet in de map data Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-145">When hello AzCopy completes, a total of 24 zipped CSV files (12 for trip\_data and 12 for trip\_fare) should be in hello data folder.</span></span>
4. <span data-ttu-id="bf1ff-146">Pak de bestanden gedownload Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-146">Unzip hello downloaded files.</span></span> <span data-ttu-id="bf1ff-147">Houd er rekening mee Hallo map waar Hallo ongecomprimeerde bestanden zich bevinden.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-147">Note hello folder where hello uncompressed files reside.</span></span> <span data-ttu-id="bf1ff-148">Deze map worden waarnaar wordt verwezen tooas Hallo < pad\_naar\_gegevens\_bestanden\>.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-148">This folder will be referred tooas hello <path\_to\_data\_files\>.</span></span>

## <span data-ttu-id="bf1ff-149"><a name="dbload"></a>Gegevens voor bulksgewijs importeren in SQL Server-Database</span><span class="sxs-lookup"><span data-stu-id="bf1ff-149"><a name="dbload"></a>Bulk Import Data into SQL Server Database</span></span>
<span data-ttu-id="bf1ff-150">Hallo prestaties laden/overdracht van grote hoeveelheden gegevens tooan SQL-database en de volgende query's kunnen worden verbeterd via *gepartitioneerde tabellen en weergaven*.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-150">hello performance of loading/transferring large amounts of data tooan SQL database and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> <span data-ttu-id="bf1ff-151">In deze sectie zult we Hallo-instructies die worden beschreven [parallelle bulksgewijs gegevens importeren met behulp van SQL partitietabellen](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate een nieuwe database en Hallo gegevens laden in gepartitioneerde tabellen parallel.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-151">In this section, we will follow hello instructions described in [Parallel Bulk Data Import Using SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md) toocreate a new database and load hello data into partitioned tables in parallel.</span></span>

1. <span data-ttu-id="bf1ff-152">Terwijl u bent aangemeld tooyour VM, start **SQL Server Management Studio**.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-152">While logged in tooyour VM, start **SQL Server Management Studio**.</span></span>
2. <span data-ttu-id="bf1ff-153">Verbinding maken met Windows-verificatie.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-153">Connect using Windows Authentication.</span></span>
   
    ![SSMS verbinden][12]
3. <span data-ttu-id="bf1ff-155">Als u hebt nog niet gewijzigd Hallo SQL Server-verificatiemodus en een nieuwe SQL-aanmeldingsgebruiker gemaakt, opent u Hallo scriptbestand met de naam **wijzigen\_auth.sql** in Hallo **voorbeeldscripts** map.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-155">If you have not yet changed hello SQL Server authentication mode and created a new SQL login user, open hello script file named **change\_auth.sql** in hello **Sample Scripts** folder.</span></span> <span data-ttu-id="bf1ff-156">Hallo standaard-gebruikersnaam en wachtwoord wijzigen.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-156">Change hello  default user name and password.</span></span> <span data-ttu-id="bf1ff-157">Klik op **! Uitvoeren van** in Hallo werkbalk toorun Hallo script.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-157">Click **!Execute** in hello toolbar toorun hello script.</span></span>
   
    ![Script uitvoeren][13]
4. <span data-ttu-id="bf1ff-159">Controleren en/of SQL Server standaard database en logboekbestanden mappen tooensure die zojuist databases gemaakt worden opgeslagen in een gegevensschijf Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-159">Verify and/or change hello SQL Server default database and log folders tooensure that newly created databases will be stored in a Data Disk.</span></span> <span data-ttu-id="bf1ff-160">Hallo SQL Server VM-installatiekopie die is geoptimaliseerd voor datawarehousing belastingen is vooraf geconfigureerd met gegevens en logboekbestanden schijven.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-160">hello SQL Server VM image that is optimized for datawarehousing loads is pre-configured with data and log disks.</span></span> <span data-ttu-id="bf1ff-161">Als u nieuwe virtuele harde schijven toegevoegd tijdens het Hallo VM-installatieproces uw virtuele machine bevat geen een gegevensschijf Hallo standaardmappen als volgt te wijzigen:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-161">If your VM did not include a Data Disk and you added new virtual hard disks during hello VM setup process, change hello default folders as follows:</span></span>
   
   * <span data-ttu-id="bf1ff-162">Klik met de rechtermuisknop Hallo SQL-servernaam in Hallo links deelvenster en klik op **eigenschappen**.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-162">Right-click hello SQL Server name in hello left panel and click **Properties**.</span></span>
     
       ![Eigenschappen van SQL Server][14]
   * <span data-ttu-id="bf1ff-164">Selecteer **Database-instellingen** van Hallo **een pagina selecteren** toohello links lijst.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-164">Select **Database Settings** from hello **Select a page** list toohello left.</span></span>
   * <span data-ttu-id="bf1ff-165">Controleren en/of Hallo wijzigen **Database standaardlocaties** toohello **gegevensschijf** locaties van uw keuze.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-165">Verify and/or change hello **Database default locations** toohello **Data Disk** locations of your choice.</span></span> <span data-ttu-id="bf1ff-166">Dit is waar nieuwe databases zich bevinden als gemaakt met de standaardinstellingen locatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-166">This is where new databases reside if created with hello default location settings.</span></span>
     
       ![Standaardinstellingen van de SQL-Database][15]  
5. <span data-ttu-id="bf1ff-168">toocreate een nieuwe database en een set bestandsgroepen toohold Hallo gepartitioneerde tabellen, opent u het voorbeeldscript Hallo **maken\_db\_default.sql**.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-168">toocreate a new database and a set of filegroups toohold hello partitioned tables, open hello sample script **create\_db\_default.sql**.</span></span> <span data-ttu-id="bf1ff-169">Hallo script maakt een nieuwe database met de naam **TaxiNYC** en 12 bestandsgroepen op Hallo gegevens standaardlocatie.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-169">hello script will create a new database named **TaxiNYC** and 12 filegroups in hello default data location.</span></span> <span data-ttu-id="bf1ff-170">Elke bestandsgroep bevatten één maand in reis\_gegevens en reis\_ritbedrag gegevens.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-170">Each filegroup will hold one month of trip\_data and trip\_fare data.</span></span> <span data-ttu-id="bf1ff-171">Wijzig de databasenaam hello, desgewenst.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-171">Modify hello database name, if desired.</span></span> <span data-ttu-id="bf1ff-172">Klik op **! Uitvoeren van** toorun Hallo script.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-172">Click **!Execute** toorun hello script.</span></span>
6. <span data-ttu-id="bf1ff-173">Maak vervolgens twee partitietabellen, één voor Hallo reis\_gegevens en een andere voor Hallo reis\_tarief.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-173">Next, create two partition tables, one for hello trip\_data and another for hello trip\_fare.</span></span> <span data-ttu-id="bf1ff-174">Hallo-voorbeeldscript Open **maken\_gepartitioneerde\_table.sql**, die wordt:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-174">Open hello sample script **create\_partitioned\_table.sql**, which will:</span></span>
   
   * <span data-ttu-id="bf1ff-175">Maak een partitie functie toosplit Hallo gegevens per maand.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-175">Create a partition function toosplit hello data by month.</span></span>
   * <span data-ttu-id="bf1ff-176">Maak een partitie schema toomap elke maand gegevens tooa andere bestandsgroep.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-176">Create a partition scheme toomap each month's data tooa different filegroup.</span></span>
   * <span data-ttu-id="bf1ff-177">Maken van twee partitieschema van gepartitioneerde tabellen toegewezen toohello: **nyctaxi\_reis** bevatten Hallo reis\_gegevens en **nyctaxi\_tarief** Hallo reis bevatten \_ritbedrag gegevens.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-177">Create two partitioned tables mapped toohello partition scheme: **nyctaxi\_trip** will hold hello trip\_data and **nyctaxi\_fare** will hold hello trip\_fare data.</span></span>
     
     <span data-ttu-id="bf1ff-178">Klik op **! Uitvoeren van** toorun Hallo script en Hallo gepartitioneerde tabellen maken.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-178">Click **!Execute** toorun hello script and create hello partitioned tables.</span></span>
7. <span data-ttu-id="bf1ff-179">In Hallo **voorbeeldscripts** map, er zijn twee PowerShell-voorbeeldscripts opgegeven toodemonstrate parallelle bulkimport gegevenstabellen tooSQL-Server.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-179">In hello **Sample Scripts** folder, there are two sample PowerShell scripts provided toodemonstrate parallel bulk imports of data tooSQL Server tables.</span></span>
   
   * <span data-ttu-id="bf1ff-180">**BCP\_parallelle\_generic.ps1** is een algemeen script tooparallel bulksgewijs Importeer gegevens in een tabel.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-180">**bcp\_parallel\_generic.ps1** is a generic script tooparallel bulk import data into a table.</span></span> <span data-ttu-id="bf1ff-181">Wijzig dit script tooset Hallo invoer- en variabelen zoals aangegeven in de regels met opmerkingen in script Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-181">Modify this script tooset hello input and target variables as indicated in hello comment lines in hello script.</span></span>
   * <span data-ttu-id="bf1ff-182">**BCP\_parallelle\_nyctaxi.ps1** is een vooraf geconfigureerde versie van de algemene script Hallo en gebruikte tootooload beide tabellen voor Hallo NYC Taxi reizen gegevens kan worden.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-182">**bcp\_parallel\_nyctaxi.ps1** is a pre-configured version of hello generic script and can be used tootooload both tables for hello NYC Taxi Trips data.</span></span>  
8. <span data-ttu-id="bf1ff-183">Klik met de rechtermuisknop Hallo **bcp\_parallelle\_nyctaxi.ps1** scriptnaam en klikt u op **bewerken** tooopen in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-183">Right-click hello **bcp\_parallel\_nyctaxi.ps1** script name and click **Edit** tooopen it in PowerShell.</span></span> <span data-ttu-id="bf1ff-184">Revisie Hallo vooraf ingestelde variabelen en wijzigen van de naam van de geselecteerde database volgens tooyour, invoergegevens map doelmap logboek en paden toohello voorbeeldbestanden indeling **nyctaxi_trip.xml** en **nyctaxi\_ fare.XML** (opgegeven in Hallo **voorbeeldscripts** map).</span><span class="sxs-lookup"><span data-stu-id="bf1ff-184">Review hello preset variables and modify according tooyour selected database name, input data folder, target log folder, and paths toohello  sample format files **nyctaxi_trip.xml** and **nyctaxi\_fare.xml** (provided in hello **Sample Scripts** folder).</span></span>
   
    ![Gegevens voor bulksgewijs importeren][16]
   
    <span data-ttu-id="bf1ff-186">U kunt ook Hallo verificatiemodus selecteren, standaard Windows-verificatie.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-186">You may also select hello authentication mode, default is Windows Authentication.</span></span> <span data-ttu-id="bf1ff-187">Klik op Hallo groene pijl in Hallo werkbalk toorun.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-187">Click hello green arrow in hello toolbar toorun.</span></span> <span data-ttu-id="bf1ff-188">Hallo-script wordt gestart, 24 importeren bulkbewerkingen in parallelle 12 voor elke gepartitioneerde tabel.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-188">hello script will launch 24 bulk import operations in parallel, 12 for each partitioned table.</span></span> <span data-ttu-id="bf1ff-189">U kunt voortgang Hallo gegevens importeren door het Hallo-standaardgegevensmap voor SQL Server te openen als hierboven.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-189">You may monitor hello data import progress by opening hello SQL Server default data folder as set above.</span></span>
9. <span data-ttu-id="bf1ff-190">Hallo PowerShell script rapporten Hallo begin- en eindtijd.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-190">hello PowerShell script reports hello starting and ending times.</span></span> <span data-ttu-id="bf1ff-191">Wanneer alle bulksgewijs invoer is voltooid, wordt de Hallo eindtijd gerapporteerd.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-191">When all bulk imports complete, hello ending time is reported.</span></span> <span data-ttu-id="bf1ff-192">Controleer Hallo doel logboek map tooverify die Hallo bulkimport is gelukt, dat wil zeggen, er geen fouten in de doelmap logboek Hallo gemeld.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-192">Check hello target log folder tooverify that hello bulk imports were successful, i.e., no errors reported in hello target log folder.</span></span>
10. <span data-ttu-id="bf1ff-193">Uw database is nu gereed voor exploratie, functie-engineering en andere bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-193">Your database is now ready for exploration, feature engineering, and other operations as desired.</span></span> <span data-ttu-id="bf1ff-194">Aangezien Hallo tabellen worden gepartitioneerd volgens toohello **ophalen\_datetime** veld, query's, waaronder **ophalen\_datetime** voorwaarden in Hallo  **WAAR** component profiteert van Hallo partitieschema.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-194">Since hello tables are partitioned according toohello **pickup\_datetime** field, queries which include **pickup\_datetime** conditions in hello **WHERE** clause will benefit from hello partition scheme.</span></span>
11. <span data-ttu-id="bf1ff-195">In **SQL Server Management Studio**, verkennen Hallo opgegeven voorbeeldscript **voorbeeld\_queries.sql**.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-195">In **SQL Server Management Studio**, explore hello provided sample script **sample\_queries.sql**.</span></span> <span data-ttu-id="bf1ff-196">toorun van Hallo voorbeeldquery's markeren Hallo regels query en klik vervolgens op **! Uitvoeren van** op Hallo-werkbalk.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-196">toorun any of hello sample queries, highlight hello query lines then click **!Execute** in hello toolbar.</span></span>
12. <span data-ttu-id="bf1ff-197">Hallo NYC Taxi reizen gegevens is geladen in twee afzonderlijke tabellen.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-197">hello NYC Taxi Trips data is loaded in two separate tables.</span></span> <span data-ttu-id="bf1ff-198">tooimprove join-bewerkingen, het is raadzaam tooindex Hallo tabellen.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-198">tooimprove join operations, it is highly recommended tooindex hello tables.</span></span> <span data-ttu-id="bf1ff-199">Hallo voorbeeldscript **maken\_gepartitioneerde\_index.sql** maakt gepartitioneerde indexen op Hallo samengestelde join-sleutel **straten, hack\_licentie en ophalen\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-199">hello sample script **create\_partitioned\_index.sql** creates partitioned indexes on hello composite join key **medallion, hack\_license, and pickup\_datetime**.</span></span>

## <span data-ttu-id="bf1ff-200"><a name="dbexplore"></a>Gegevensverkenning en functie-Engineering in SQL Server</span><span class="sxs-lookup"><span data-stu-id="bf1ff-200"><a name="dbexplore"></a>Data Exploration and Feature Engineering in SQL Server</span></span>
<span data-ttu-id="bf1ff-201">In deze sectie voert we gegevens te verkennen en functie genereren met behulp van SQL-query's rechtstreeks in Hallo **SQL Server Management Studio** met behulp van SQL Server-database Hallo eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-201">In this section, we will perform data exploration and feature generation by running SQL queries directly in hello **SQL Server Management Studio** using hello SQL Server database created earlier.</span></span> <span data-ttu-id="bf1ff-202">Een voorbeeld van een script met de naam **voorbeeld\_queries.sql** vindt u in Hallo **voorbeeldscripts** map.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-202">A sample script named **sample\_queries.sql** is provided in hello **Sample Scripts** folder.</span></span> <span data-ttu-id="bf1ff-203">Hallo script toochange Hallo-databasenaam wijzigen als deze van de standaard Hallo verschilt: **TaxiNYC**.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-203">Modify hello script toochange hello database name, if it is different from hello default: **TaxiNYC**.</span></span>

<span data-ttu-id="bf1ff-204">In deze oefening wordt:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-204">In this exercise, we will:</span></span>

* <span data-ttu-id="bf1ff-205">Verbinding te maken met**SQL Server Management Studio** met behulp van op Windows-verificatie of via SQL-verificatie en Hallo SQL-aanmeldingsnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-205">Connect too**SQL Server Management Studio** using either Windows Authentication or using SQL Authentication and hello SQL login name and password.</span></span>
* <span data-ttu-id="bf1ff-206">Verken de gegevens distributies van enkele velden in verschillende tijdvensters.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="bf1ff-207">Onderzoek de kwaliteit van de gegevens van Hallo breedtegraad velden.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-207">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="bf1ff-208">Genereren van binaire en multiklassen classificatielabels op basis van Hallo **tip\_bedrag**.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-208">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="bf1ff-209">Genereren van functies en reis afstanden compute/vergelijken.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="bf1ff-210">Hallo twee tabellen samenvoegen en uitpakken van een steekproef die gebruikt toobuild modellen worden.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-210">Join hello two tables and extract a random sample that will be used toobuild models.</span></span>

<span data-ttu-id="bf1ff-211">Wanneer u klaar tooproceed tooAzure Machine Learning bent, mag u ofwel:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-211">When you are ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="bf1ff-212">Sla Hallo uiteindelijke SQL query tooextract en voorbeeld Hallo gegevens en kopiëren en plakken Hallo query rechtstreeks in een [importgegevens] [ import-data] -module in Azure Machine Learning, of</span><span class="sxs-lookup"><span data-stu-id="bf1ff-212">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="bf1ff-213">Hallo door actieve behouden en engineering gegevens die u van plan bent toouse voor model bouwen in een nieuwe database tabel en nieuwe tabel Hallo gebruiken in Hallo [importgegevens] [ import-data] -module in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-213">Persist hello sampled and engineered data you plan toouse for model building in a new database table and use hello new table in hello [Import Data][import-data] module in Azure Machine Learning.</span></span>

<span data-ttu-id="bf1ff-214">In deze sectie wordt we Hallo laatste querybewerking tooextract en voorbeeld Hallo gegevens opslaan.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-214">In this section we will save hello final query tooextract and sample hello data.</span></span> <span data-ttu-id="bf1ff-215">de tweede methode Hello wordt geïllustreerd in Hallo [Gegevensverkenning en functie-Engineering in IPython Notebook](#ipnb) sectie.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-215">hello second method is demonstrated in hello [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span>

<span data-ttu-id="bf1ff-216">Voor een snelle verificatie van Hallo aantal rijen en kolommen in hello in tabellen ingevuld eerder met parallelle bulkimport,</span><span class="sxs-lookup"><span data-stu-id="bf1ff-216">For a quick verification of hello number of rows and columns in hello tables populated earlier using parallel bulk import,</span></span>

    -- Report number of rows in table nyctaxi_trip without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('nyctaxi_trip')

    -- Report number of columns in table nyctaxi_trip
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = 'nyctaxi_trip'

#### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="bf1ff-217">Exploratie: Reis distributie door straten</span><span class="sxs-lookup"><span data-stu-id="bf1ff-217">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="bf1ff-218">In dit voorbeeld identificeert Hallo straten (taxi getallen) met meer dan 100 reizen binnen een bepaalde periode.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-218">This example identifies hello medallion (taxi numbers) with more than 100 trips within a given time period.</span></span> <span data-ttu-id="bf1ff-219">Hallo query wilt profiteren van Hallo gepartitioneerde tabeltoegang omdat deze wordt waarbij door Hallo partitieschema van **ophalen\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-219">hello query would benefit from hello partitioned table access since it is conditioned by hello partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="bf1ff-220">Opvragen van de volledige gegevensset Hallo maakt ook gebruik van de gepartitioneerde tabel Hallo en/of index van de scan.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-220">Querying hello full dataset will also make use of hello partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

#### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="bf1ff-221">Exploratie: Reis distributie door straten en hack_license</span><span class="sxs-lookup"><span data-stu-id="bf1ff-221">Exploration: Trip distribution by medallion and hack_license</span></span>
    SELECT medallion, hack_license, COUNT(*)
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

#### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="bf1ff-222">Gegevens beoordeling: Controleer of records met onjuiste lengtegraad en/of breedtegraad</span><span class="sxs-lookup"><span data-stu-id="bf1ff-222">Data Quality Assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="bf1ff-223">In dit voorbeeld onderzoekt als Hallo lengtegraad en/of breedtegraad velden een ongeldige waarde bevatten (radiaal graden moet tussen-90 en 90), of (0, 0) coördinaten.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-223">This example investigates if any of hello longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM nyctaxi_trip
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

#### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="bf1ff-224">Exploratie: Gekantelde vs. Niet reizen punt distributie</span><span class="sxs-lookup"><span data-stu-id="bf1ff-224">Exploration: Tipped vs. Not Tipped Trips distribution</span></span>
<span data-ttu-id="bf1ff-225">Dit voorbeeld wordt gezocht naar Hallo aantal reizen die zijn punt versus geen punt in een bepaald moment periode (of in de volledige gegevensset Hallo als die betrekking hebben op Hallo volledige jaar).</span><span class="sxs-lookup"><span data-stu-id="bf1ff-225">This example finds hello number of trips that were tipped vs. not tipped in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="bf1ff-226">Deze verdeling weerspiegelt Hallo binaire label distributie toobe later gebruikt voor het modelleren van de binaire indeling.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-226">This distribution reflects hello binary label distribution toobe later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM nyctaxi_fare
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

#### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="bf1ff-227">Exploratie: Tip distributie van de klasse-bereik</span><span class="sxs-lookup"><span data-stu-id="bf1ff-227">Exploration: Tip Class/Range Distribution</span></span>
<span data-ttu-id="bf1ff-228">In dit voorbeeld berekent Hallo distributie van tip bereiken in een bepaald moment periode (of in de volledige gegevensset Hallo als die betrekking hebben op Hallo volledige jaar).</span><span class="sxs-lookup"><span data-stu-id="bf1ff-228">This example computes hello distribution of tip ranges in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="bf1ff-229">Dit is distributiepunt Hallo Hallo label klassen die later wordt gebruikt voor multiklassen classificatie modellering.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-229">This is hello distribution of hello label classes that will be used later for multiclass classification modeling.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_fare
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

#### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="bf1ff-230">Exploratie: Berekenen en reis afstand vergelijken</span><span class="sxs-lookup"><span data-stu-id="bf1ff-230">Exploration: Compute and Compare Trip Distance</span></span>
<span data-ttu-id="bf1ff-231">In dit voorbeeld Hallo ophalen en inleverbibliotheek lengtegraad converteert en breedtegraad tooSQL Geografie verwijst, Hallo reis afstand met behulp van SQL Geografie punten verschil wordt berekend en retourneert een willekeurig aantal Hallo resultaten voor vergelijking.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-231">This example converts hello pickup and drop-off longitude and latitude tooSQL geography points, computes hello trip distance using SQL geography points difference, and returns a random sample of hello results for comparison.</span></span> <span data-ttu-id="bf1ff-232">Hallo voorbeeld beperkt Hallo resultaten toovalid coördineert alleen met behulp van Hallo kwaliteit assessment gegevensquery eerder besproken.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-232">hello example limits hello results toovalid coordinates only using hello data quality assessment query covered earlier.</span></span>

    SELECT
    pickup_location=geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326)
    ,dropoff_location=geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326)
    ,trip_distance
    ,computedist=round(geography::STPointFromText('POINT(' + pickup_longitude + ' ' + pickup_latitude + ')', 4326).STDistance(geography::STPointFromText('POINT(' + dropoff_longitude + ' ' + dropoff_latitude + ')', 4326))/1000, 2)
    FROM nyctaxi_trip
    tablesample(0.01 percent)
    WHERE CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND   CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

#### <a name="feature-engineering-in-sql-queries"></a><span data-ttu-id="bf1ff-233">Functie-Engineering in SQL-query 's</span><span class="sxs-lookup"><span data-stu-id="bf1ff-233">Feature Engineering in SQL Queries</span></span>
<span data-ttu-id="bf1ff-234">Hallo label genereren en Geografie conversie exploratie query's kunnen ook gebruikte toogenerate labels en-functies worden door het verwijderen van onderdeel tellen Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-234">hello label generation and geography conversion exploration queries can also be used toogenerate labels/features by removing hello counting part.</span></span> <span data-ttu-id="bf1ff-235">Voorbeelden van technische SQL aanvullende functies zijn beschikbaar in Hallo [Gegevensverkenning en functie-Engineering in IPython Notebook](#ipnb) sectie.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-235">Additional feature engineering SQL examples are provided in hello [Data Exploration and Feature Engineering in IPython Notebook](#ipnb) section.</span></span> <span data-ttu-id="bf1ff-236">Het is efficiënter toorun Hallo functie generatie query's in de volledige gegevensset hello of een grote subset van met behulp van SQL-query's die rechtstreeks op Hallo SQL Server database-exemplaar worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-236">It is more efficient toorun hello feature generation queries on hello full dataset or a large subset of it using SQL queries which run directly on hello SQL Server database instance.</span></span> <span data-ttu-id="bf1ff-237">Hallo-query's kunnen worden uitgevoerd in **SQL Server Management Studio**, IPython laptop of elk hulpprogramma/ontwikkelomgeving die toegang heeft tot database Hallo lokaal of extern.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-237">hello queries may be executed in **SQL Server Management Studio**, IPython Notebook or any development tool/environment which can access hello database locally or remotely.</span></span>

#### <a name="preparing-data-for-model-building"></a><span data-ttu-id="bf1ff-238">Voorbereiden van gegevens voor het Model bouwen</span><span class="sxs-lookup"><span data-stu-id="bf1ff-238">Preparing Data for Model Building</span></span>
<span data-ttu-id="bf1ff-239">Hallo volgende joins Hallo query **nyctaxi\_reis** en **nyctaxi\_tarief** tabellen, genereert een label binaire classificatie **punt**, een meerdere klasse classificatie label **tip\_klasse**, en extraheert met een willekeurige steekproef 1% uit Hallo volledige gekoppelde gegevensset.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-239">hello following query joins hello **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a 1% random sample from hello full joined dataset.</span></span> <span data-ttu-id="bf1ff-240">Deze query kan worden gekopieerd en geplakt rechtstreeks in Hallo [Azure Machine Learning Studio](https://studio.azureml.net) [importgegevens] [ import-data] -module voor directe gegevensopname van Hallo SQL Server-database exemplaar in Azure.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-240">This query can be copied then pasted directly in hello [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from hello SQL Server database instance in Azure.</span></span> <span data-ttu-id="bf1ff-241">Hallo query worden records met onjuiste uitgesloten (0, 0) coördinaten.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-241">hello query excludes records with incorrect (0, 0) coordinates.</span></span>

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM nyctaxi_trip t, nyctaxi_fare f
    TABLESAMPLE (1 percent)
    WHERE t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'


## <span data-ttu-id="bf1ff-242"><a name="ipnb"></a>Gegevensverkenning en functie-Engineering in IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="bf1ff-242"><a name="ipnb"></a>Data Exploration and Feature Engineering in IPython Notebook</span></span>
<span data-ttu-id="bf1ff-243">In deze sectie wordt uitgevoerd, er gegevensverkenning en functie genereren met behulp van Python- en SQL-query's op Hallo SQL Server-database eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-243">In this section, we will perform data exploration and feature generation using both Python and SQL queries against hello SQL Server database created earlier.</span></span> <span data-ttu-id="bf1ff-244">Een voorbeeld IPython notebook met de naam **machine-Learning-data-science-process-sql-story.ipynb** vindt u in Hallo **voorbeeld IPython notitieblokken** map.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-244">A sample IPython notebook named **machine-Learning-data-science-process-sql-story.ipynb** is provided in hello **Sample IPython Notebooks** folder.</span></span> <span data-ttu-id="bf1ff-245">Deze laptop is ook beschikbaar op [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span><span class="sxs-lookup"><span data-stu-id="bf1ff-245">This notebook is also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/DataScienceProcess/iPythonNotebooks).</span></span>

<span data-ttu-id="bf1ff-246">Hallo aanbevolen volgorde bij het werken met big data is Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-246">hello recommended sequence when working with big data is hello following:</span></span>

* <span data-ttu-id="bf1ff-247">Gelezen in een klein aantal Hallo gegevens in een kader gegevens in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-247">Read in a small sample of hello data into an in-memory data frame.</span></span>
* <span data-ttu-id="bf1ff-248">Uitvoeren van sommige visualisaties en explorations met Hallo steekproefgegevens.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-248">Perform some visualizations and explorations using hello sampled data.</span></span>
* <span data-ttu-id="bf1ff-249">Experiment met functie-engineering Hallo met voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-249">Experiment with feature engineering using hello sampled data.</span></span>
* <span data-ttu-id="bf1ff-250">Voor grotere gegevensverkenning gebruiken voor gegevensmanipulatie en functie-engineering, Python tooissue SQL-query's rechtstreeks op Hallo SQL Server-database in hello Azure VM.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-250">For larger data exploration, data manipulation and feature engineering, use Python tooissue SQL Queries directly against hello SQL Server database in hello Azure VM.</span></span>
* <span data-ttu-id="bf1ff-251">Bepaal Hallo voorbeeld grootte toouse voor het bouwen van Azure Machine Learning-model.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-251">Decide hello sample size toouse for Azure Machine Learning model building.</span></span>

<span data-ttu-id="bf1ff-252">Als u klaar bent tooproceed tooAzure Machine Learning, mag u ofwel:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-252">When ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="bf1ff-253">Sla Hallo uiteindelijke SQL query tooextract en voorbeeld Hallo gegevens en kopiëren en plakken Hallo query rechtstreeks in een [importgegevens] [ import-data] -module in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-253">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="bf1ff-254">Deze methode wordt geïllustreerd in Hallo [gebouw modellen in Azure Machine Learning](#mlmodel) sectie.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-254">This method is demonstrated in hello [Building Models in Azure Machine Learning](#mlmodel) section.</span></span>    
2. <span data-ttu-id="bf1ff-255">Hallo door actieve en engineering gegevens die u van plan bent toouse voor model bouwen in een nieuwe database behouden en gebruik deze nieuwe tabel Hallo in Hallo [importgegevens] [ import-data] module.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-255">Persist hello sampled and engineered data you plan toouse for model building in a new database table, then use hello new table in hello [Import Data][import-data] module.</span></span>

<span data-ttu-id="bf1ff-256">Hallo volgen een paar gegevensverkenning: gegevensvisualisatie en voorbeelden engineering-functie.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-256">hello following are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="bf1ff-257">Zie voor meer voorbeelden Hallo voorbeeld SQL IPython laptop in Hallo **voorbeeld IPython notitieblokken** map.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-257">For more examples, see hello sample SQL IPython notebook in hello **Sample IPython Notebooks** folder.</span></span>

#### <a name="initialize-database-credentials"></a><span data-ttu-id="bf1ff-258">Databasereferenties initialiseren</span><span class="sxs-lookup"><span data-stu-id="bf1ff-258">Initialize Database Credentials</span></span>
<span data-ttu-id="bf1ff-259">De verbindingsinstellingen voor database in de volgende variabelen Hallo initialiseren:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-259">Initialize your database connection settings in hello following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database server>

#### <a name="create-database-connection"></a><span data-ttu-id="bf1ff-260">Databaseverbinding maken</span><span class="sxs-lookup"><span data-stu-id="bf1ff-260">Create Database Connection</span></span>
    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

#### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="bf1ff-261">Rapport aantal rijen en kolommen in tabel nyctaxi_trip</span><span class="sxs-lookup"><span data-stu-id="bf1ff-261">Report number of rows and columns in table nyctaxi_trip</span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('nyctaxi_trip')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('nyctaxi_trip')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="bf1ff-262">Totale aantal rijen 173179759 =</span><span class="sxs-lookup"><span data-stu-id="bf1ff-262">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="bf1ff-263">Totale aantal kolommen = 14</span><span class="sxs-lookup"><span data-stu-id="bf1ff-263">Total number of columns = 14</span></span>

#### <a name="read-in-a-small-data-sample-from-hello-sql-server-database"></a><span data-ttu-id="bf1ff-264">Lees in een kleine hoeveelheden gegevens voorbeeld Hallo SQL Server-Database</span><span class="sxs-lookup"><span data-stu-id="bf1ff-264">Read-in a small data sample from hello SQL Server Database</span></span>
    t0 = time.time()

    query = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (0.05 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="bf1ff-265">Tijd tooread Hallo-voorbeeldtabel is 6.492000 seconden</span><span class="sxs-lookup"><span data-stu-id="bf1ff-265">Time tooread hello sample table is 6.492000 seconds</span></span>  
<span data-ttu-id="bf1ff-266">Aantal rijen en kolommen opgehaald = (84952, 21)</span><span class="sxs-lookup"><span data-stu-id="bf1ff-266">Number of rows and columns retrieved = (84952, 21)</span></span>

#### <a name="descriptive-statistics"></a><span data-ttu-id="bf1ff-267">Beschrijvende statistiek</span><span class="sxs-lookup"><span data-stu-id="bf1ff-267">Descriptive Statistics</span></span>
<span data-ttu-id="bf1ff-268">U bent nu klaar tooexplore Hallo door actieve gegevens.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-268">Now are ready tooexplore hello sampled data.</span></span> <span data-ttu-id="bf1ff-269">We beginnen met de beschrijvende statistieken voor Hallo kijken **reis\_afstand** (of andere) sleutelvelden:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-269">We start with looking at descriptive statistics for hello **trip\_distance** (or any other) field(s):</span></span>

    df1['trip_distance'].describe()

#### <a name="visualization-box-plot-example"></a><span data-ttu-id="bf1ff-270">Visualisatie: Voorbeeld van grafiek</span><span class="sxs-lookup"><span data-stu-id="bf1ff-270">Visualization: Box Plot Example</span></span>
<span data-ttu-id="bf1ff-271">Vervolgens kijken we Hallo BoxPlot voor Hallo reis afstand toovisualize hello quantiles</span><span class="sxs-lookup"><span data-stu-id="bf1ff-271">Next we look at hello box plot for hello trip distance toovisualize hello quantiles</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![Tekenen van #1][1]

#### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="bf1ff-273">Visualisatie: Distributie tekent voorbeeld</span><span class="sxs-lookup"><span data-stu-id="bf1ff-273">Visualization: Distribution Plot Example</span></span>
    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Tekenen van #2][2]

#### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="bf1ff-275">Visualisatie: De balk en de regel waarnemingspunten</span><span class="sxs-lookup"><span data-stu-id="bf1ff-275">Visualization: Bar and Line Plots</span></span>
<span data-ttu-id="bf1ff-276">In dit voorbeeld we Hallo reis afstand in vijf opslaglocaties bin en visualiseren Hallo binning resultaten.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-276">In this example, we bin hello trip distance into five bins and visualize hello binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="bf1ff-277">We kunnen tekenen Hallo hierboven bin distributie in een balk of regel tekent zoals hieronder</span><span class="sxs-lookup"><span data-stu-id="bf1ff-277">We can plot hello above bin distribution in a bar or line plot as below</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Tekenen van #3][3]

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Tekenen van #4][4]

#### <a name="visualization-scatterplot-example"></a><span data-ttu-id="bf1ff-280">Visualisatie: Scatterplot voorbeeld</span><span class="sxs-lookup"><span data-stu-id="bf1ff-280">Visualization: Scatterplot Example</span></span>
<span data-ttu-id="bf1ff-281">Laten we zien spreidingsgrafiek tekent tussen **reis\_tijd\_in\_sec** en **reis\_afstand** toosee als er correlatie</span><span class="sxs-lookup"><span data-stu-id="bf1ff-281">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** toosee if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![#6 tekenen][6]

<span data-ttu-id="bf1ff-283">We kunnen op dezelfde manier controleren of Hallo relatie tussen **snelheid\_code** en **reis\_afstand**.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-283">Similarly we can check hello relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![#8 tekenen][8]

### <a name="sub-sampling-hello-data-in-sql"></a><span data-ttu-id="bf1ff-285">Onderliggende steekproeven Hallo gegevens in SQL</span><span class="sxs-lookup"><span data-stu-id="bf1ff-285">Sub-Sampling hello Data in SQL</span></span>
<span data-ttu-id="bf1ff-286">Bij het voorbereiden van gegevens voor model bouwen in [Azure Machine Learning Studio](https://studio.azureml.net), desgewenst kunt u ofwel op Hallo **toouse voor SQL-query rechtstreeks in Hallo importgegevens module** of Hallo is ontworpen en actieve behouden gegevens in een nieuwe tabel, kunt u in Hallo [importgegevens] [ import-data] module met een eenvoudige **Selecteer * FROM < uw\_nieuwe\_tabel\_name >**.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-286">When preparing data for model building in [Azure Machine Learning Studio](https://studio.azureml.net), you may either decide on hello **SQL query toouse directly in hello Import Data module** or persist hello engineered and sampled data in a new table, which you could use in hello [Import Data][import-data] module with a simple **SELECT * FROM <your\_new\_table\_name>**.</span></span>

<span data-ttu-id="bf1ff-287">In deze sectie we maken een nieuwe tabel toohold Hallo door actieve en engineering gegevens.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-287">In this section we will create a new table toohold hello sampled and engineered data.</span></span> <span data-ttu-id="bf1ff-288">Een voorbeeld van een directe SQL-query voor het model bouwen wordt verstrekt in Hallo [Gegevensverkenning en functie-Engineering in SQL Server](#dbexplore) sectie.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-288">An example of a direct SQL query for model building is provided in hello [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="create-a-sample-table-and-populate-with-1-of-hello-joined-tables-drop-table-first-if-it-exists"></a><span data-ttu-id="bf1ff-289">Maak een voorbeeldtabel en Populate met % 1 van Hallo die lid zijn van tabellen.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-289">Create a Sample Table and Populate with 1% of hello Joined Tables.</span></span> <span data-ttu-id="bf1ff-290">Verwijderen in de eerste tabel als deze bestaat.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-290">Drop Table First if it Exists.</span></span>
<span data-ttu-id="bf1ff-291">In deze sectie we Hallo-tabellen samenvoegen **nyctaxi\_reis** en **nyctaxi\_tarief**, ophalen van een steekproef van 1% en Hallo door actieve gegevens in de naam van een nieuwe tabel behouden  **nyctaxi\_één\_procent**:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-291">In this section, we join hello tables **nyctaxi\_trip** and **nyctaxi\_fare**, extract a 1% random sample, and persist hello sampled data in a new table name **nyctaxi\_one\_percent**:</span></span>

    cursor = conn.cursor()

    drop_table_if_exists = '''
        IF OBJECT_ID('nyctaxi_one_percent', 'U') IS NOT NULL DROP TABLE nyctaxi_one_percent
    '''

    nyctaxi_one_percent_insert = '''
        SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount
        INTO nyctaxi_one_percent
        FROM nyctaxi_trip t, nyctaxi_fare f
        TABLESAMPLE (1 PERCENT)
        WHERE t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
        AND   pickup_longitude <> '0' AND dropoff_longitude <> '0'
    '''

    cursor.execute(drop_table_if_exists)
    cursor.execute(nyctaxi_one_percent_insert)
    cursor.commit()

### <a name="data-exploration-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="bf1ff-292">Gegevensverkenning met SQL-query's in IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="bf1ff-292">Data Exploration using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="bf1ff-293">In deze sectie besproken voor gegevens distributies met Hallo 1-% actieve gegevens op die wordt bewaard in de nieuwe tabel Hallo die we eerder hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-293">In this section, we explore data distributions using hello 1% sampled data which is persisted in hello new table we created above.</span></span> <span data-ttu-id="bf1ff-294">Houd er rekening mee dat vergelijkbare explorations kunnen worden uitgevoerd met behulp van de oorspronkelijke tabellen hello, waarbij optioneel **TABLESAMPLE** toolimit Hallo exploratie voorbeeld of door het beperken van Hallo resulteert tooa opgegeven tijdsperiode Hallo **ophalen \_datetime** partities, zoals geïllustreerd in Hallo [Gegevensverkenning en functie-Engineering in SQL Server](#dbexplore) sectie.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-294">Note that similar explorations can be performed using hello original tables, optionally using **TABLESAMPLE** toolimit hello exploration sample or by limiting hello results tooa given time period using hello **pickup\_datetime** partitions, as illustrated in hello [Data Exploration and Feature Engineering in SQL Server](#dbexplore) section.</span></span>

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="bf1ff-295">Exploratie: Dagelijkse distributie van reizen</span><span class="sxs-lookup"><span data-stu-id="bf1ff-295">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="bf1ff-296">Exploratie: Reis distributie per straten</span><span class="sxs-lookup"><span data-stu-id="bf1ff-296">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM nyctaxi_one_percent
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

### <a name="feature-generation-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="bf1ff-297">Functie genereren met behulp van SQL-query's in IPython Notebook</span><span class="sxs-lookup"><span data-stu-id="bf1ff-297">Feature Generation Using SQL Queries in IPython Notebook</span></span>
<span data-ttu-id="bf1ff-298">In deze sectie er nieuwe labels worden gegenereerd en functies direct met SQL-query's, op Hallo 1% voorbeeldtabel we gemaakt in de vorige sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-298">In this section we will generate new labels and features directly using SQL queries, operating on hello 1% sample table we created in hello previous section.</span></span>

#### <a name="label-generation-generate-class-labels"></a><span data-ttu-id="bf1ff-299">Label generatie: Labels van de klasse te genereren</span><span class="sxs-lookup"><span data-stu-id="bf1ff-299">Label Generation: Generate Class Labels</span></span>
<span data-ttu-id="bf1ff-300">In Hallo voorbeeld te volgen, er twee sets met labels toouse voor modellering gegenereerd:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-300">In hello following example, we generate two sets of labels toouse for modeling:</span></span>

1. <span data-ttu-id="bf1ff-301">Binaire klasse Labels **punt** (als een tip krijgt voorspellen)</span><span class="sxs-lookup"><span data-stu-id="bf1ff-301">Binary Class Labels **tipped** (predicting if a tip will be given)</span></span>
2. <span data-ttu-id="bf1ff-302">Multiklassen Labels **tip\_klasse** (voorspellen Hallo tip bin of bereik)</span><span class="sxs-lookup"><span data-stu-id="bf1ff-302">Multiclass Labels **tip\_class** (predicting hello tip bin or range)</span></span>
   
        nyctaxi_one_percent_add_col = '''
            ALTER TABLE nyctaxi_one_percent ADD tipped bit, tip_class int
        '''
   
        cursor.execute(nyctaxi_one_percent_add_col)
        cursor.commit()
   
        nyctaxi_one_percent_update_col = '''
            UPDATE nyctaxi_one_percent
            SET
               tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
               tip_class = CASE WHEN (tip_amount = 0) THEN 0
                                WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                                WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                                WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                                ELSE 4
                            END
        '''
   
        cursor.execute(nyctaxi_one_percent_update_col)
        cursor.commit()

#### <a name="feature-engineering-count-features-for-categorical-columns"></a><span data-ttu-id="bf1ff-303">Functie-Engineering: Aantal functies voor Categorische kolommen</span><span class="sxs-lookup"><span data-stu-id="bf1ff-303">Feature Engineering: Count Features for Categorical Columns</span></span>
<span data-ttu-id="bf1ff-304">In dit voorbeeld transformeert een categorische veld in een numeriek veld door te vervangen elke categorie met Hallo telling van de instanties in Hallo-gegevens.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-304">This example transforms a categorical field into a numeric field by replacing each category with hello count of its occurrences in hello data.</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD cmt_count int, vts_count int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B AS
        (
            SELECT medallion, hack_license,
                SUM(CASE WHEN vendor_id = 'cmt' THEN 1 ELSE 0 END) AS cmt_count,
                SUM(CASE WHEN vendor_id = 'vts' THEN 1 ELSE 0 END) AS vts_count
            FROM nyctaxi_one_percent
            GROUP BY medallion, hack_license
        )

        UPDATE nyctaxi_one_percent
        SET nyctaxi_one_percent.cmt_count = B.cmt_count,
            nyctaxi_one_percent.vts_count = B.vts_count
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion AND A.hack_license = B.hack_license
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-bin-features-for-numerical-columns"></a><span data-ttu-id="bf1ff-305">Functie-Engineering: Bin functies voor numerieke kolommen</span><span class="sxs-lookup"><span data-stu-id="bf1ff-305">Feature Engineering: Bin features for Numerical Columns</span></span>
<span data-ttu-id="bf1ff-306">In dit voorbeeld transformeert een continue numeriek veld in de vooraf ingestelde categorie bereiken, numeriek veld dat wil zeggen, transformatie in een categorische veld.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-306">This example transforms a continuous numeric field into preset category ranges, i.e., transform numeric field into a categorical field.</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent ADD trip_time_bin int
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        WITH B(medallion,hack_license,pickup_datetime,trip_time_in_secs, BinNumber ) AS
        (
            SELECT medallion,hack_license,pickup_datetime,trip_time_in_secs,
            NTILE(5) OVER (ORDER BY trip_time_in_secs) AS BinNumber from nyctaxi_one_percent
        )

        UPDATE nyctaxi_one_percent
        SET trip_time_bin = B.BinNumber
        FROM nyctaxi_one_percent A INNER JOIN B
        ON A.medallion = B.medallion
        AND A.hack_license = B.hack_license
        AND A.pickup_datetime = B.pickup_datetime
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="feature-engineering-extract-location-features-from-decimal-latitudelongitude"></a><span data-ttu-id="bf1ff-307">Functie-Engineering: Functies van de locatie van decimale breedtegraad/lengtegraad uitpakken</span><span class="sxs-lookup"><span data-stu-id="bf1ff-307">Feature Engineering: Extract Location Features from Decimal Latitude/Longitude</span></span>
<span data-ttu-id="bf1ff-308">In dit voorbeeld uitvalt Hallo decimale weergave van een veld breedtegraad en/of lengtegraad in meerdere regio velden van verschillende mate van granulatie, zoals land, stad, stad, blok, enzovoort. Hallo nieuwe geo-velden zijn niet toegewezen tooactual locaties.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-308">This example breaks down hello decimal representation of a latitude and/or longitude field into multiple region fields of different granularity, such as, country, city, town, block, etc. Note that hello new geo-fields are not mapped tooactual locations.</span></span> <span data-ttu-id="bf1ff-309">Zie voor informatie over toewijzing geocode locaties, [Bing Maps REST Services](https://msdn.microsoft.com/library/ff701710.aspx).</span><span class="sxs-lookup"><span data-stu-id="bf1ff-309">For information on mapping geocode locations, see [Bing Maps REST Services](https://msdn.microsoft.com/library/ff701710.aspx).</span></span>

    nyctaxi_one_percent_insert_col = '''
        ALTER TABLE nyctaxi_one_percent
        ADD l1 varchar(6), l2 varchar(3), l3 varchar(3), l4 varchar(3),
            l5 varchar(3), l6 varchar(3), l7 varchar(3)
    '''

    cursor.execute(nyctaxi_one_percent_insert_col)
    cursor.commit()

    nyctaxi_one_percent_update_col = '''
        UPDATE nyctaxi_one_percent
        SET l1=round(pickup_longitude,0)
            , l2 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 1 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),1,1) ELSE '0' END     
            , l3 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 2 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),2,1) ELSE '0' END     
            , l4 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 3 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),3,1) ELSE '0' END     
            , l5 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 4 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),4,1) ELSE '0' END     
            , l6 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 5 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),5,1) ELSE '0' END     
            , l7 = CASE WHEN LEN (PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1)) >= 6 THEN SUBSTRING(PARSENAME(ROUND(ABS(pickup_longitude) - FLOOR(ABS(pickup_longitude)),6),1),6,1) ELSE '0' END
    '''

    cursor.execute(nyctaxi_one_percent_update_col)
    cursor.commit()

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a><span data-ttu-id="bf1ff-310">Controleer of de uiteindelijke vorm Hallo van Hallo featurized tabel</span><span class="sxs-lookup"><span data-stu-id="bf1ff-310">Verify hello final form of hello featurized table</span></span>
    query = '''SELECT TOP 100 * FROM nyctaxi_one_percent'''
    pd.read_sql(query,conn)

<span data-ttu-id="bf1ff-311">Er zijn nu gereed tooproceed toomodel bouwen en implementeren van modellen in [Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="bf1ff-311">We are now ready tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="bf1ff-312">Hallo-gegevens is gereed voor Hallo voorspelling problemen geïdentificeerd eerder, namelijk:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-312">hello data is ready for any of hello prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="bf1ff-313">Binaire classificatie: toopredict al dan niet een tip voor een zakenreis is betaald.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-313">Binary classification: toopredict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="bf1ff-314">Multiklassen classificatie: toopredict Hallo bereik van een tip betaald, toohello op basis van vooraf gedefinieerde klassen.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-314">Multiclass classification: toopredict hello range of tip paid, according toohello previously defined classes.</span></span>
3. <span data-ttu-id="bf1ff-315">Taak regressie: toopredict Hallo hoeveelheid tip voor een reis betaald.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-315">Regression task: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="bf1ff-316"><a name="mlmodel"></a>Gebouw modellen in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="bf1ff-316"><a name="mlmodel"></a>Building Models in Azure Machine Learning</span></span>
<span data-ttu-id="bf1ff-317">toobegin Hallo oefening modelleren, meld u bij tooyour Azure Machine Learning-werkruimte.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-317">toobegin hello modeling exercise, log in tooyour Azure Machine Learning workspace.</span></span> <span data-ttu-id="bf1ff-318">Als u nog geen een machine learning-werkruimte hebt gemaakt, raadpleegt u [maken van een Azure Machine Learning-werkruimte](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="bf1ff-318">If you have not yet created a machine learning workspace, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="bf1ff-319">de slag met Azure Machine Learning tooget Zie [wat is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="bf1ff-319">tooget started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="bf1ff-320">Meld u bij te[Azure Machine Learning Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="bf1ff-320">Log in too[Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="bf1ff-321">Hallo-startpagina Studio biedt een schat aan informatie, video's, zelfstudies, koppelingen toohello Modules verwijzing en andere bronnen.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-321">hello Studio Home page provides a wealth of information, videos, tutorials, links toohello Modules Reference, and other resources.</span></span> <span data-ttu-id="bf1ff-322">Raadpleeg voor meer informatie over Azure Machine Learning Hallo [Azure Machine Learning-documentatiecentrum](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="bf1ff-322">Fore more information about Azure Machine Learning, consult hello [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="bf1ff-323">Een typische trainingsexperiment bestaat uit Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-323">A typical training experiment consists of hello following:</span></span>

1. <span data-ttu-id="bf1ff-324">Maak een **+ nieuw** experimenteren.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-324">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="bf1ff-325">Hallo gegevens tooAzure Machine Learning ophalen.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-325">Get hello data tooAzure Machine Learning.</span></span>
3. <span data-ttu-id="bf1ff-326">Vooraf verwerken, transformeren en manipuleren van Hallo gegevens zo nodig.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-326">Pre-process, transform and manipulate hello data as needed.</span></span>
4. <span data-ttu-id="bf1ff-327">Genereren onderdelen naar behoefte.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-327">Generate features as needed.</span></span>
5. <span data-ttu-id="bf1ff-328">Hallo gegevens splitsen in training/testen/validatie gegevenssets (of afzonderlijke gegevenssets hebben voor elk).</span><span class="sxs-lookup"><span data-stu-id="bf1ff-328">Split hello data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="bf1ff-329">Selecteer een of meer machine learning-algoritmen, afhankelijk van Hallo probleem toosolve leren.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-329">Select one or more machine learning algorithms depending on hello learning problem toosolve.</span></span> <span data-ttu-id="bf1ff-330">Bijvoorbeeld binaire classificatie, multiklassen classificatie, regressie.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-330">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="bf1ff-331">Een of meer modellen Hallo training gegevensset met trainen.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-331">Train one or more models using hello training dataset.</span></span>
8. <span data-ttu-id="bf1ff-332">Hallo validatie gegevensset met Hallo getraind modellen beoordelen.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-332">Score hello validation dataset using hello trained model(s).</span></span>
9. <span data-ttu-id="bf1ff-333">Hallo modellen toocompute Hallo relevante meetgegevens voor Hallo learning probleem evalueren.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-333">Evaluate hello model(s) toocompute hello relevant metrics for hello learning problem.</span></span>
10. <span data-ttu-id="bf1ff-334">Afstellen Hallo modellen en selecteer Hallo best model toodeploy.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-334">Fine tune hello model(s) and select hello best model toodeploy.</span></span>

<span data-ttu-id="bf1ff-335">In deze oefening hebben we al verkend en engineering Hallo-gegevens in SQL Server en besloten op Hallo voorbeeld grootte tooingest in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-335">In this exercise, we have already explored and engineered hello data in SQL Server, and decided on hello sample size tooingest in Azure Machine Learning.</span></span> <span data-ttu-id="bf1ff-336">toobuild een of meer van de Hallo voorspellende modellen die we besloten:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-336">toobuild one or more of hello prediction models we decided:</span></span>

1. <span data-ttu-id="bf1ff-337">Hallo gegevens tooAzure Machine Learning ophalen met behulp van Hallo [gegevens importeren] [ import-data] module beschikbaar in Hallo **gegevensinvoer en uitvoer** sectie.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-337">Get hello data tooAzure Machine Learning using hello [Import Data][import-data] module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="bf1ff-338">Zie voor meer informatie, Hallo [importgegevens] [ import-data] verwijzingspagina module.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-338">For more information, see hello [Import Data][import-data] module reference page.</span></span>
   
    ![Gegevens van Azure Machine Learning importeren][17]
2. <span data-ttu-id="bf1ff-340">Selecteer **Azure SQL Database** als Hallo **gegevensbron** in Hallo **eigenschappen** Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-340">Select **Azure SQL Database** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="bf1ff-341">Voer Hallo database DNS-naam in Hallo **databaseservernaam** veld.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-341">Enter hello database DNS name in hello **Database server name** field.</span></span> <span data-ttu-id="bf1ff-342">Indeling:`tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="bf1ff-342">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="bf1ff-343">Voer Hallo **databasenaam** in het bijbehorende veld Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-343">Enter hello **Database name** in hello corresponding field.</span></span>
5. <span data-ttu-id="bf1ff-344">Voer Hallo **SQL-gebruikersnaam** in Hallo ** Server aqccount gebruikersnaam en wachtwoord in Hallo Hallo **Server het wachtwoord voor gebruikersaccount**.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-344">Enter hello **SQL user name** in hello **Server user aqccount name, and hello password in hello **Server user account password**.</span></span>
6. <span data-ttu-id="bf1ff-345">Controleer **accepteren servercertificaat** optie.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-345">Check **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="bf1ff-346">In Hallo **databasequery** bewerken van tekst, Hallo query welke uitgepakt Hallo nodig databasevelden (inclusief eventuele berekende velden zoals Hallo labels) en pijl-omlaag voorbeelden Hallo gegevens toohello gewenst samplegrootte plakken.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-346">In hello **Database query** edit text area, paste hello query which extracts hello necessary database fields (including any computed fields such as hello labels) and down samples hello data toohello desired sample size.</span></span>

<span data-ttu-id="bf1ff-347">Een voorbeeld van een binaire indeling experiment lezen van gegevens rechtstreeks van Hallo SQL Server-database is in Hallo afbeelding hieronder.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-347">An example of a binary classification experiment reading data directly from hello SQL Server database is in hello figure below.</span></span> <span data-ttu-id="bf1ff-348">Vergelijkbare experimenten kunnen worden samengesteld voor multiklassen classificatie en regressie problemen.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-348">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Azure Machine Learning Train][10]

> [!IMPORTANT]
> <span data-ttu-id="bf1ff-350">In Hallo modelleren ophalen van gegevens en wordt de query-voorbeelden die zijn opgegeven in de vorige secties **alle labels voor Hallo drie modellering oefeningen zijn opgenomen in de query Hallo**.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-350">In hello modeling data extraction and sampling query examples provided in previous sections, **all labels for hello three modeling exercises are included in hello query**.</span></span> <span data-ttu-id="bf1ff-351">Een belangrijke (vereist) stap in elk Hallo modelleren oefeningen is te**uitsluiten** onnodige labels voor Hallo Hallo andere twee problemen en andere **doel lekken**.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-351">An important (required) step in each of hello modeling exercises is too**exclude** hello unnecessary labels for hello other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="bf1ff-352">Voor bijvoorbeeld bij gebruik van binaire classificatie gebruiken Hallo label **punt** en Hallo velden uitsluiten **tip\_klasse**, **tip\_bedrag**, en **totale\_bedrag**.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-352">For e.g., when using binary classification, use hello label **tipped** and exclude hello fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="bf1ff-353">Hallo laatste doel lekken omdat ze Hallo tip impliceren worden betaald.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-353">hello latter are target leaks since they imply hello tip paid.</span></span>
> 
> <span data-ttu-id="bf1ff-354">overbodige kolommen tooexclude en/of doel lekken, mag u Hallo [Select Columns in Dataset] [ select-columns] module of Hallo [metagegevens bewerken] [ edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="bf1ff-354">tooexclude unnecessary columns and/or target leaks, you may use hello [Select Columns in Dataset][select-columns] module or hello [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="bf1ff-355">Zie voor meer informatie [Select Columns in Dataset] [ select-columns] en [metagegevens bewerken] [ edit-metadata] verwijzen naar pagina's.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-355">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="bf1ff-356"><a name="mldeploy"></a>Implementeren van modellen in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="bf1ff-356"><a name="mldeploy"></a>Deploying Models in Azure Machine Learning</span></span>
<span data-ttu-id="bf1ff-357">Wanneer uw model klaar is, kunt u het eenvoudig implementeren als een webservice rechtstreeks vanuit het Hallo-experiment.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-357">When your model is ready, you can easily deploy it as a web service directly from hello experiment.</span></span> <span data-ttu-id="bf1ff-358">Zie voor meer informatie over het implementeren van Azure Machine Learning-webservices [Azure Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="bf1ff-358">For more information about deploying Azure Machine Learning web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="bf1ff-359">een nieuwe webservice toodeploy, moet u:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-359">toodeploy a new web service, you need to:</span></span>

1. <span data-ttu-id="bf1ff-360">Een score experiment maken.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-360">Create a scoring experiment.</span></span>
2. <span data-ttu-id="bf1ff-361">Hallo-webservice implementeren.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-361">Deploy hello web service.</span></span>

<span data-ttu-id="bf1ff-362">toocreate een score berekenen experimenteren van een **voltooid** training experiment, klikt u op **maken score berekenen EXPERIMENTEREN** in lagere actiebalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-362">toocreate a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in hello lower action bar.</span></span>

![Score berekenen voor Azure][18]

<span data-ttu-id="bf1ff-364">Azure Machine Learning probeert een score experiment op basis van onderdelen van Hallo trainingsexperiment Hallo toocreate.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-364">Azure Machine Learning will attempt toocreate a scoring experiment based on hello components of hello training experiment.</span></span> <span data-ttu-id="bf1ff-365">In het bijzonder wordt:</span><span class="sxs-lookup"><span data-stu-id="bf1ff-365">In particular, it will:</span></span>

1. <span data-ttu-id="bf1ff-366">Hallo getraind model opslaan en Hallo model trainingsmodules verwijderen.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-366">Save hello trained model and remove hello model training modules.</span></span>
2. <span data-ttu-id="bf1ff-367">Een logische identificeren **poort invoer** toorepresent Hallo invoergegevens schema verwacht.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-367">Identify a logical **input port** toorepresent hello expected input data schema.</span></span>
3. <span data-ttu-id="bf1ff-368">Een logische identificeren **uitvoerpoort** toorepresent Hallo verwachte web service-uitvoerschema.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-368">Identify a logical **output port** toorepresent hello expected web service output schema.</span></span>

<span data-ttu-id="bf1ff-369">Wanneer Hallo experiment score berekenen is gemaakt, bekijken en indien nodig aanpassen.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-369">When hello scoring experiment is created, review it and adjust as needed.</span></span> <span data-ttu-id="bf1ff-370">Een typische aanpassing is tooreplace hello invoergegevensset en/of de query met een exclusief label velden, zoals deze is alleen beschikbaar wanneer het Hallo-service wordt genoemd.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-370">A typical adjustment is tooreplace hello input dataset and/or query with one which excludes label fields, as these will not be available when hello service is called.</span></span> <span data-ttu-id="bf1ff-371">Het is ook dat een goede gewoonte tooreduce Hallo grootte van Hallo invoer gegevensset en/of queryparameters tooa enkele records, net voldoende tooindicate Hallo invoer schema.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-371">It is also a good practice tooreduce hello size of hello input dataset and/or query tooa few records, just enough tooindicate hello input schema.</span></span> <span data-ttu-id="bf1ff-372">Voor de uitvoerpoort hello, het algemene tooexclude alle invoervelden en bevat alleen Hallo **Scored Labels** en **berekend kansen** in uitvoer met behulp van Hallo Hallo [kolommen in gegevensset selecteren ] [ select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-372">For hello output port, it is common tooexclude all input fields and only include hello **Scored Labels** and **Scored Probabilities** in hello output using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="bf1ff-373">Een voorbeeld van een experiment score berekenen is in Hallo afbeelding hieronder.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-373">A sample scoring experiment is in hello figure below.</span></span> <span data-ttu-id="bf1ff-374">Als u klaar bent toodeploy, klikt u op Hallo **WEBSERVICE PUBLICEERT** knop in lagere actiebalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-374">When ready toodeploy, click hello **PUBLISH WEB SERVICE** button in hello lower action bar.</span></span>

![Azure Machine Learning publiceren][11]

<span data-ttu-id="bf1ff-376">toorecap, in deze zelfstudie scenario hebt u een Azure data wetenschap-omgeving hebt gewerkt met een grote openbare gegevensset alle Hallo manier van gegevens overname toomodel trainings- en implementeren van een Azure Machine Learning-webservice gemaakt.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-376">toorecap, in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset all hello way from data acquisition toomodel training and deploying of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="bf1ff-377">Licentie-informatie</span><span class="sxs-lookup"><span data-stu-id="bf1ff-377">License Information</span></span>
<span data-ttu-id="bf1ff-378">In dit voorbeeld scenario en de bijbehorende scripts en IPython notebook(s) worden gedeeld door Microsoft onder Hallo MIT-licentie.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-378">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="bf1ff-379">Controleer de Hallo LICENSE.txt bestand in de directory Hallo van Hallo voorbeeldcode op GitHub voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="bf1ff-379">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

### <a name="references"></a><span data-ttu-id="bf1ff-380">Verwijzingen</span><span class="sxs-lookup"><span data-stu-id="bf1ff-380">References</span></span>
<span data-ttu-id="bf1ff-381">• [Andrés Monroy NYC Taxi reizen downloadpagina](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="bf1ff-381">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="bf1ff-382">• [FOILing NYC Taxi reis gegevens door Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="bf1ff-382">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="bf1ff-383">• [NYC Taxi en Limousine Commissie onderzoek en statistieken](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="bf1ff-383">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[1]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sql-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sql-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sql-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sql-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sql-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sql-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sql-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sql-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sql-walkthrough/amlscoring.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
