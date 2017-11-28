---
title: 'Hallo Team gegevens wetenschappelijke processen in actie: met behulp van SQL Data Warehouse | Microsoft Docs'
description: Geavanceerde analyses proces en de technologie in actie
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 88ba8e28-0bd7-49fe-8320-5dfa83b65724
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;hangzh;weig
ms.openlocfilehash: b1b6371583a023d32e33db59464cafd8c3b767d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="hello-team-data-science-process-in-action-using-sql-data-warehouse"></a><span data-ttu-id="8f744-103">Hallo Team gegevens wetenschappelijke processen in actie: met behulp van SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="8f744-103">hello Team Data Science Process in action: using SQL Data Warehouse</span></span>
<span data-ttu-id="8f744-104">In deze zelfstudie wordt beschreven hoe u maken en implementeren van een machine learning-model met behulp van SQL Data Warehouse (SQL DW) voor een openbaar dataset--hello [NYC Taxi reizen](http://www.andresmh.com/nyctaxitrips/) gegevensset.</span><span class="sxs-lookup"><span data-stu-id="8f744-104">In this tutorial, we walk you through building and deploying a machine learning model using SQL Data Warehouse (SQL DW) for a publicly available dataset -- hello [NYC Taxi Trips](http://www.andresmh.com/nyctaxitrips/) dataset.</span></span> <span data-ttu-id="8f744-105">Hallo binaire classificatie model samengesteld voorspelt al dan niet een tip voor een reis is betaald, en modellen voor multiklassen classificatie en regressie worden ook besproken die Hallo distributie voor betaalde Hallo tip bedragen voorspellen.</span><span class="sxs-lookup"><span data-stu-id="8f744-105">hello binary classification model constructed predicts whether or not a tip is paid for a trip, and models for multiclass classification and regression are also discussed that predict hello distribution for hello tip amounts paid.</span></span>

<span data-ttu-id="8f744-106">Hallo procedure volgt Hallo [Team gegevens wetenschap proces (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) werkstroom.</span><span class="sxs-lookup"><span data-stu-id="8f744-106">hello procedure follows hello [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) workflow.</span></span> <span data-ttu-id="8f744-107">Laten we zien hoe een wetenschappelijke gegevensomgeving toosetup hoe tooload gegevens in SQL DW Hallo en hoe SQL DW of Hallo een tooexplore IPython Notebook gegevens en engineer u het toomodel functies gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8f744-107">We show how toosetup a data science environment, how tooload hello data into SQL DW, and how use either SQL DW or an IPython Notebook tooexplore hello data and engineer features toomodel.</span></span> <span data-ttu-id="8f744-108">Vervolgens wordt gedemonstreerd hoe toobuild en implementeren van een model met Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="8f744-108">We then show how toobuild and deploy a model with Azure Machine Learning.</span></span>

## <span data-ttu-id="8f744-109"><a name="dataset"></a>Hallo NYC Taxi reizen gegevensset</span><span class="sxs-lookup"><span data-stu-id="8f744-109"><a name="dataset"></a>hello NYC Taxi Trips dataset</span></span>
<span data-ttu-id="8f744-110">Hallo NYC Taxi reis gegevens bestaat uit ongeveer 20GB gecomprimeerde CSV-bestanden (~ 48GB ongecomprimeerde), opnemen van meer dan 173 miljoen afzonderlijke reizen en Hallo ervoor staat voor elke reis betaald.</span><span class="sxs-lookup"><span data-stu-id="8f744-110">hello NYC Taxi Trip data consists of about 20GB of compressed CSV files (~48GB uncompressed), recording more than 173 million individual trips and hello fares paid for each trip.</span></span> <span data-ttu-id="8f744-111">Elke record reis omvat Hallo ophalen en inleverbibliotheek locaties en tijden, geanonimiseerde inbreken licentienummer (stuurprogramma van) en Hallo nummer straten (taxi van unieke id).</span><span class="sxs-lookup"><span data-stu-id="8f744-111">Each trip record includes hello pickup and drop-off locations and times, anonymized hack (driver's) license number, and hello medallion (taxi’s unique id) number.</span></span> <span data-ttu-id="8f744-112">Hallo-gegevens bevat informatie over alle reizen Hallo jaar 2013 en is beschikbaar in twee gegevenssets voor elke maand na Hallo:</span><span class="sxs-lookup"><span data-stu-id="8f744-112">hello data covers all trips in hello year 2013 and is provided in hello following two datasets for each month:</span></span>

1. <span data-ttu-id="8f744-113">Hallo **trip_data.csv** bestand reis details, zoals het aantal passagiers, ophalen en dropoff punten reis duur en duur van reis bevat.</span><span class="sxs-lookup"><span data-stu-id="8f744-113">hello **trip_data.csv** file contains trip details, such as number of passengers, pickup and dropoff points, trip duration, and trip length.</span></span> <span data-ttu-id="8f744-114">Hier volgen enkele voorbeeldrecords:</span><span class="sxs-lookup"><span data-stu-id="8f744-114">Here are a few sample records:</span></span>
   
        medallion,hack_license,vendor_id,rate_code,store_and_fwd_flag,pickup_datetime,dropoff_datetime,passenger_count,trip_time_in_secs,trip_distance,pickup_longitude,pickup_latitude,dropoff_longitude,dropoff_latitude
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,1,N,2013-01-01 15:11:48,2013-01-01 15:18:10,4,382,1.00,-73.978165,40.757977,-73.989838,40.751171
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-06 00:18:35,2013-01-06 00:22:54,1,259,1.50,-74.006683,40.731781,-73.994499,40.75066
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,1,N,2013-01-05 18:49:41,2013-01-05 18:54:23,1,282,1.10,-74.004707,40.73777,-74.009834,40.726002
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:54:15,2013-01-07 23:58:20,2,244,.70,-73.974602,40.759945,-73.984734,40.759388
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,1,N,2013-01-07 23:25:03,2013-01-07 23:34:24,1,560,2.10,-73.97625,40.748528,-74.002586,40.747868
2. <span data-ttu-id="8f744-115">Hallo **trip_fare.csv** bestand bevat de details van Hallo tarief betaald voor elke reis, zoals betalingstype tarief bedrag, extra kosten en belastingen, tips en tolgelden en Hallo totaalbedrag betaald.</span><span class="sxs-lookup"><span data-stu-id="8f744-115">hello **trip_fare.csv** file contains details of hello fare paid for each trip, such as payment type, fare amount, surcharge and taxes, tips and tolls, and hello total amount paid.</span></span> <span data-ttu-id="8f744-116">Hier volgen enkele voorbeeldrecords:</span><span class="sxs-lookup"><span data-stu-id="8f744-116">Here are a few sample records:</span></span>
   
        medallion, hack_license, vendor_id, pickup_datetime, payment_type, fare_amount, surcharge, mta_tax, tip_amount, tolls_amount, total_amount
        89D227B655E5C82AECF13C3F540D4CF4,BA96DE419E711691B9445D6A6307C170,CMT,2013-01-01 15:11:48,CSH,6.5,0,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-06 00:18:35,CSH,6,0.5,0.5,0,0,7
        0BD7C8F5BA12B88E0B67BED28BEA73D8,9FD8F69F0804BDB5549F40E9DA1BE472,CMT,2013-01-05 18:49:41,CSH,5.5,1,0.5,0,0,7
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:54:15,CSH,5,0.5,0.5,0,0,6
        DFD2202EE08F7A8DC9A57B02ACB81FE2,51EE87E3205C985EF8431D850C786310,CMT,2013-01-07 23:25:03,CSH,9.5,0.5,0.5,0,0,10.5

<span data-ttu-id="8f744-117">Hallo **unieke sleutel** toojoin reis gebruikt\_gegevens en reis\_tarief bestaat uit de volgende drie velden Hallo:</span><span class="sxs-lookup"><span data-stu-id="8f744-117">hello **unique key** used toojoin trip\_data and trip\_fare is composed of hello following three fields:</span></span>

* <span data-ttu-id="8f744-118">straten,</span><span class="sxs-lookup"><span data-stu-id="8f744-118">medallion,</span></span>
* <span data-ttu-id="8f744-119">inbreken\_licentie en</span><span class="sxs-lookup"><span data-stu-id="8f744-119">hack\_license and</span></span>
* <span data-ttu-id="8f744-120">ophalen\_datetime.</span><span class="sxs-lookup"><span data-stu-id="8f744-120">pickup\_datetime.</span></span>

## <span data-ttu-id="8f744-121"><a name="mltasks"></a>Adres van de drie typen taken voorspelling</span><span class="sxs-lookup"><span data-stu-id="8f744-121"><a name="mltasks"></a>Address three types of prediction tasks</span></span>
<span data-ttu-id="8f744-122">We drie voorspelling problemen op basis van Hallo formuleren *tip\_bedrag* tooillustrate drie soorten taken modelleren:</span><span class="sxs-lookup"><span data-stu-id="8f744-122">We formulate three prediction problems based on hello *tip\_amount* tooillustrate three kinds of modeling tasks:</span></span>

1. <span data-ttu-id="8f744-123">**Binaire classificatie**: toopredict al dan niet een tip betaald is voor een reis, dat wil zeggen een *tip\_bedrag* die groter is dan $0 een voorbeeld van een positieve is, terwijl een *tip\_bedrag* van $0 is een voorbeeld van een negatief.</span><span class="sxs-lookup"><span data-stu-id="8f744-123">**Binary classification**: toopredict whether or not a tip was paid for a trip, i.e. a *tip\_amount* that is greater than $0 is a positive example, while a *tip\_amount* of $0 is a negative example.</span></span>
2. <span data-ttu-id="8f744-124">**Multiklassen classificatie**: toopredict Hallo bereik van een tip voor Hallo reis betaald.</span><span class="sxs-lookup"><span data-stu-id="8f744-124">**Multiclass classification**: toopredict hello range of tip paid for hello trip.</span></span> <span data-ttu-id="8f744-125">We delen Hallo *tip\_bedrag* in vijf opslaglocaties of klassen:</span><span class="sxs-lookup"><span data-stu-id="8f744-125">We divide hello *tip\_amount* into five bins or classes:</span></span>
   
        Class 0 : tip_amount = $0
        Class 1 : tip_amount > $0 and tip_amount <= $5
        Class 2 : tip_amount > $5 and tip_amount <= $10
        Class 3 : tip_amount > $10 and tip_amount <= $20
        Class 4 : tip_amount > $20
3. <span data-ttu-id="8f744-126">**Regressie taak**: toopredict Hallo hoeveelheid tip voor een reis betaald.</span><span class="sxs-lookup"><span data-stu-id="8f744-126">**Regression task**: toopredict hello amount of tip paid for a trip.</span></span>  

## <span data-ttu-id="8f744-127"><a name="setup"></a>Hello Azure gegevens wetenschappelijke omgeving voor geavanceerde analyses instellen</span><span class="sxs-lookup"><span data-stu-id="8f744-127"><a name="setup"></a>Set up hello Azure data science environment for advanced analytics</span></span>
<span data-ttu-id="8f744-128">tooset van uw omgeving Gegevenswetenschap Azure als volgt te werk.</span><span class="sxs-lookup"><span data-stu-id="8f744-128">tooset up your Azure Data Science environment, follow these steps.</span></span>

<span data-ttu-id="8f744-129">**Uw eigen Azure blob storage-account maken**</span><span class="sxs-lookup"><span data-stu-id="8f744-129">**Create your own Azure blob storage account**</span></span>

* <span data-ttu-id="8f744-130">Wanneer u uw eigen Azure-blobopslag inricht, kiest u een geografische locatie voor uw Azure blob storage in of zo dicht mogelijk te**Zuid-centraal VS**, dit is waar Hallo NYC Taxi gegevens wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="8f744-130">When you provision your own Azure blob storage, choose a geo-location for your Azure blob storage in or as close as possible too**South Central US**, which is where hello NYC Taxi data is stored.</span></span> <span data-ttu-id="8f744-131">Hallo-gegevens worden gekopieerd met behulp van AzCopy van Hallo openbare blob storage-container tooa container in uw eigen opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="8f744-131">hello data will be copied using AzCopy from hello public blob storage container tooa container in your own storage account.</span></span> <span data-ttu-id="8f744-132">Hallo dichter bij de Azure blob-opslag is tooSouth VS-midden, hello sneller (stap 4) van deze taak wordt voltooid.</span><span class="sxs-lookup"><span data-stu-id="8f744-132">hello closer your Azure blob storage is tooSouth Central US, hello faster this task (Step 4) will be completed.</span></span>
* <span data-ttu-id="8f744-133">toocreate account van uw eigen Azure-opslag, volg Hallo stappen die worden beschreven op [over Azure storage-accounts](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="8f744-133">toocreate your own Azure storage account, follow hello steps outlined at [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="8f744-134">Niet zeker toomake opmerkingen over Hallo waarden voor de volgende opslagaccountreferenties als ze later in dit scenario worden vereist.</span><span class="sxs-lookup"><span data-stu-id="8f744-134">Be sure toomake notes on hello values for following storage account credentials as they will be needed later in this walkthrough.</span></span>
  
  * <span data-ttu-id="8f744-135">**Naam van het opslagaccount**</span><span class="sxs-lookup"><span data-stu-id="8f744-135">**Storage Account Name**</span></span>
  * <span data-ttu-id="8f744-136">**De sleutel van opslagaccount**</span><span class="sxs-lookup"><span data-stu-id="8f744-136">**Storage Account Key**</span></span>
  * <span data-ttu-id="8f744-137">**Containernaam** (die u wilt dat Hallo gegevens toobe opgeslagen in hello Azure blob-opslag)</span><span class="sxs-lookup"><span data-stu-id="8f744-137">**Container Name** (which you want hello data toobe stored in hello Azure blob storage)</span></span>

<span data-ttu-id="8f744-138">**Inrichten van uw Azure SQL DW-exemplaar.**</span><span class="sxs-lookup"><span data-stu-id="8f744-138">**Provision your Azure SQL DW instance.**</span></span>
<span data-ttu-id="8f744-139">Ga als volgt Hallo-documentatie op [maken van een SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision een exemplaar van SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8f744-139">Follow hello documentation at [Create a SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-get-started-provision.md) tooprovision a SQL Data Warehouse instance.</span></span> <span data-ttu-id="8f744-140">Zorg ervoor dat u notaties op Hallo SQL Data Warehouse-referenties die worden gebruikt in latere stappen te volgen.</span><span class="sxs-lookup"><span data-stu-id="8f744-140">Make sure that you make notations on hello following SQL Data Warehouse credentials which will be used in later steps.</span></span>

* <span data-ttu-id="8f744-141">**Servernaam**: <server Name>. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="8f744-141">**Server Name**: <server Name>.database.windows.net</span></span>
* <span data-ttu-id="8f744-142">**De naam van de SQLDW (Database)**</span><span class="sxs-lookup"><span data-stu-id="8f744-142">**SQLDW (Database) Name**</span></span>
* <span data-ttu-id="8f744-143">**Gebruikersnaam**</span><span class="sxs-lookup"><span data-stu-id="8f744-143">**Username**</span></span>
* <span data-ttu-id="8f744-144">**Wachtwoord**</span><span class="sxs-lookup"><span data-stu-id="8f744-144">**Password**</span></span>

<span data-ttu-id="8f744-145">**Installeer Visual Studio en SQL Server Data Tools.**</span><span class="sxs-lookup"><span data-stu-id="8f744-145">**Install Visual Studio and SQL Server Data Tools.**</span></span> <span data-ttu-id="8f744-146">Zie voor instructies [Visual Studio 2015 installeren en/of SSDT (SQL Server Data Tools) voor SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="8f744-146">For instructions, see [Install Visual Studio 2015 and/or SSDT (SQL Server Data Tools) for SQL Data Warehouse](../sql-data-warehouse/sql-data-warehouse-install-visual-studio.md).</span></span>

<span data-ttu-id="8f744-147">**Verbinding maken met Azure SQL DW tooyour met Visual Studio.**</span><span class="sxs-lookup"><span data-stu-id="8f744-147">**Connect tooyour Azure SQL DW with Visual Studio.**</span></span> <span data-ttu-id="8f744-148">Voor instructies raadpleegt u de stappen 1 en 2 in [tooAzure SQL Data Warehouse met Visual Studio verbinding](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span><span class="sxs-lookup"><span data-stu-id="8f744-148">For instructions, see steps 1 & 2 in [Connect tooAzure SQL Data Warehouse with Visual Studio](../sql-data-warehouse/sql-data-warehouse-connect-overview.md).</span></span>

> [!NOTE]
> <span data-ttu-id="8f744-149">Voer hello volgende SQL-query op database Hallo u hebt gemaakt in uw SQL Data Warehouse (verbinding maken onderwerp, in plaats van Hallo query is opgegeven in stap 3 van Hallo) te**een hoofdsleutel**.</span><span class="sxs-lookup"><span data-stu-id="8f744-149">Run hello following SQL query on hello database you created in your SQL Data Warehouse (instead of hello query provided in step 3 of hello connect topic,) too**create a master key**.</span></span>
> 
> 

    BEGIN TRY
           --Try toocreate hello master key
        CREATE MASTER KEY
    END TRY
    BEGIN CATCH
           --If hello master key exists, do nothing
    END CATCH;

<span data-ttu-id="8f744-150">**Een Azure Machine Learning-werkruimte onder uw Azure-abonnement maken.**</span><span class="sxs-lookup"><span data-stu-id="8f744-150">**Create an Azure Machine Learning workspace under your Azure subscription.**</span></span> <span data-ttu-id="8f744-151">Zie voor instructies [maken van een Azure Machine Learning-werkruimte](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="8f744-151">For instructions, see [Create an Azure Machine Learning workspace](machine-learning-create-workspace.md).</span></span>

## <span data-ttu-id="8f744-152"><a name="getdata"></a>Hallo gegevens laden in SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="8f744-152"><a name="getdata"></a>Load hello data into SQL Data Warehouse</span></span>
<span data-ttu-id="8f744-153">Open een Windows PowerShell-opdracht-console.</span><span class="sxs-lookup"><span data-stu-id="8f744-153">Open a Windows PowerShell command console.</span></span> <span data-ttu-id="8f744-154">Voer de volgende Hallo PowerShell-opdrachten toodownload Hallo voorbeeld SQL scriptbestanden die we delen met u op GitHub tooa lokale map die u met de parameter Hallo opgeeft *- DestDir*.</span><span class="sxs-lookup"><span data-stu-id="8f744-154">Run hello following PowerShell commands toodownload hello example SQL script files that we share with you on GitHub tooa local directory that you specify with hello parameter *-DestDir*.</span></span> <span data-ttu-id="8f744-155">U kunt wijzigen Hallo-waarde van parameter *- DestDir* tooany lokale map.</span><span class="sxs-lookup"><span data-stu-id="8f744-155">You can change hello value of parameter *-DestDir* tooany local directory.</span></span> <span data-ttu-id="8f744-156">Als *- DestDir* niet bestaat, wordt deze gemaakt door Hallo PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="8f744-156">If *-DestDir* does not exist, it will be created by hello PowerShell script.</span></span>

> [!NOTE]
> <span data-ttu-id="8f744-157">U moet mogelijk te**als Administrator uitvoeren** bij het uitvoeren van de volgende PowerShell-script op als Hallo uw *DestDir* directory moet Administrator-bevoegdheden toocreate of toowrite-tooit.</span><span class="sxs-lookup"><span data-stu-id="8f744-157">You might need too**Run as Administrator** when executing hello following PowerShell script if your *DestDir* directory needs Administrator privilege toocreate or toowrite tooit.</span></span>
> 
> 

    $source = "https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/Download_Scripts_SQLDW_Walkthrough.ps1"
    $ps1_dest = "$pwd\Download_Scripts_SQLDW_Walkthrough.ps1"
    $wc = New-Object System.Net.WebClient
    $wc.DownloadFile($source, $ps1_dest)
    .\Download_Scripts_SQLDW_Walkthrough.ps1 –DestDir 'C:\tempSQLDW'

<span data-ttu-id="8f744-158">Na voltooiing van uitvoering, verandert de huidige werkmap te*- DestDir*.</span><span class="sxs-lookup"><span data-stu-id="8f744-158">After successful execution, your current working directory changes too*-DestDir*.</span></span> <span data-ttu-id="8f744-159">U moet kunnen toosee scherm zoals hieronder:</span><span class="sxs-lookup"><span data-stu-id="8f744-159">You should be able toosee screen like below:</span></span>

![][19]

<span data-ttu-id="8f744-160">In uw *- DestDir*, Hallo volgen in de beheerdersmodus een PowerShell-script uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="8f744-160">In your *-DestDir*, execute hello following PowerShell script in administrator mode:</span></span>

    ./SQLDW_Data_Import.ps1

<span data-ttu-id="8f744-161">Wanneer Hallo PowerShell-script wordt uitgevoerd voor Hallo eerst, u gevraagd tooinput Hallo informatie van uw Azure SQL DW en uw Azure blob storage-account.</span><span class="sxs-lookup"><span data-stu-id="8f744-161">When hello PowerShell script runs for hello first time, you will be asked tooinput hello information from your Azure SQL DW and your Azure blob storage account.</span></span> <span data-ttu-id="8f744-162">Wanneer dit PowerShell-script is voltooid wordt met voor Hallo eerst Hallo referenties u invoer zijn geschreven configuratiebestand tooa SQLDW.conf in de huidige werkmap Hallo.</span><span class="sxs-lookup"><span data-stu-id="8f744-162">When this PowerShell script completes running for hello first time, hello credentials you input will have been written tooa configuration file SQLDW.conf in hello present working directory.</span></span> <span data-ttu-id="8f744-163">Hallo heeft toekomstige uitvoering van dit bestand PowerShell-script Hallo optie tooread alle benodigde parameters van dit configuratiebestand.</span><span class="sxs-lookup"><span data-stu-id="8f744-163">hello future run of this PowerShell script file has hello option tooread all needed parameters from this configuration file.</span></span> <span data-ttu-id="8f744-164">Als u nodig hebt toochange sommige parameters, kunt u kiezen tooinput Hallo parameters op het welkomstscherm bij de prompt door dit configuratiebestand verwijderen en het invoeren van parameterwaarden Hallo wanneer daarom wordt gevraagd of toochange Hallo parameterwaarden door Hallo SQLDW.conf bestand te bewerken in uw *- DestDir* directory.</span><span class="sxs-lookup"><span data-stu-id="8f744-164">If you need toochange some parameters, you can choose tooinput hello parameters on hello screen upon prompt by deleting this configuration file and inputting hello parameters values as prompted or toochange hello parameter values by editing hello SQLDW.conf file in your *-DestDir* directory.</span></span>

> [!NOTE]
> <span data-ttu-id="8f744-165">In de volgorde tooavoid schema naam een conflict veroorzaakt met degenen die al aanwezig zijn in uw Azure SQL DW bij het lezen van parameters rechtstreeks van Hallo SQLDW.conf bestand, wordt een willekeurig getal 3-cijferige uit Hallo SQLDW.conf bestand toohello schemanaam toegevoegd als Hallo standaardnaam schema voor elke uitvoering.</span><span class="sxs-lookup"><span data-stu-id="8f744-165">In order tooavoid schema name conflicts with those that already exist in your Azure SQL DW, when reading parameters directly from hello SQLDW.conf file, a 3-digit random number is added toohello schema name from hello SQLDW.conf file as hello default schema name for each run.</span></span> <span data-ttu-id="8f744-166">Hallo PowerShell-script wordt u mogelijk gevraagd voor de naam van een schema: gebruiker goeddunken Hallo naam worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="8f744-166">hello PowerShell script may prompt you for a schema name: hello name may be specified at user discretion.</span></span>
> 
> 

<span data-ttu-id="8f744-167">Dit **PowerShell-script** bestand is voltooid Hallo taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="8f744-167">This **PowerShell script** file completes hello following tasks:</span></span>

* <span data-ttu-id="8f744-168">**Downloadt en installeert AzCopy**als AzCopy nog niet is geïnstalleerd</span><span class="sxs-lookup"><span data-stu-id="8f744-168">**Downloads and installs AzCopy**, if AzCopy is not already installed</span></span>
  
        $AzCopy_path = SearchAzCopy
        if ($AzCopy_path -eq $null){
               Write-Host "AzCopy.exe is not found in C:\Program Files*. Now, start installing AzCopy..." -ForegroundColor "Yellow"
            InstallAzCopy
            $AzCopy_path = SearchAzCopy
        }
            $env_path = $env:Path
            for ($i=0; $i -lt $AzCopy_path.count; $i++){
                if ($AzCopy_path.count -eq 1){
                    $AzCopy_path_i = $AzCopy_path
                } else {
                    $AzCopy_path_i = $AzCopy_path[$i]
                }
                if ($env_path -notlike '*' +$AzCopy_path_i+'*'){
                    Write-Host $AzCopy_path_i 'not in system path, add it...'
                    [Environment]::SetEnvironmentVariable("Path", "$AzCopy_path_i;$env_path", "Machine")
                    $env:Path = [System.Environment]::GetEnvironmentVariable("Path","Machine")
                    $env_path = $env:Path
                }
* <span data-ttu-id="8f744-169">**Kopieert de gegevens tooyour persoonlijke blob storage-account** van een openbare blob met AzCopy Hallo</span><span class="sxs-lookup"><span data-stu-id="8f744-169">**Copies data tooyour private blob storage account** from hello public blob with AzCopy</span></span>
  
        Write-Host "AzCopy is copying data from public blob tooyo storage account. It may take a while..." -ForegroundColor "Yellow"
        $start_time = Get-Date
        AzCopy.exe /Source:$Source /Dest:$DestURL /DestKey:$StorageAccountKey /S
        $end_time = Get-Date
        $time_span = $end_time - $start_time
        $total_seconds = [math]::Round($time_span.TotalSeconds,2)
        Write-Host "AzCopy finished copying data. Please check your storage account tooverify." -ForegroundColor "Yellow"
        Write-Host "This step (copying data from public blob tooyour storage account) takes $total_seconds seconds." -ForegroundColor "Green"
* <span data-ttu-id="8f744-170">**Laden van gegevens met Polybase (door het uitvoeren van LoadDataToSQLDW.sql) tooyour Azure SQL DW** van uw persoonlijke blob storage-account met de volgende opdrachten Hallo.</span><span class="sxs-lookup"><span data-stu-id="8f744-170">**Loads data using Polybase (by executing LoadDataToSQLDW.sql) tooyour Azure SQL DW** from your private blob storage account with hello following commands.</span></span>
  
  * <span data-ttu-id="8f744-171">Een schema maken</span><span class="sxs-lookup"><span data-stu-id="8f744-171">Create a schema</span></span>
    
          EXEC (''CREATE SCHEMA {schemaname};'');
  * <span data-ttu-id="8f744-172">Een-scoped databasereferentie maken</span><span class="sxs-lookup"><span data-stu-id="8f744-172">Create a database scoped credential</span></span>
    
          CREATE DATABASE SCOPED CREDENTIAL {KeyAlias}
          WITH IDENTITY = ''asbkey'' ,
          Secret = ''{StorageAccountKey}''
  * <span data-ttu-id="8f744-173">Maken van een externe gegevensbron voor een Azure storage-blob</span><span class="sxs-lookup"><span data-stu-id="8f744-173">Create an external data source for an Azure storage blob</span></span>
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_trip_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
    
          CREATE EXTERNAL DATA SOURCE {nyctaxi_fare_storage}
          WITH
          (
              TYPE = HADOOP,
              LOCATION =''wasbs://{ContainerName}@{StorageAccountName}.blob.core.windows.net'',
              CREDENTIAL = {KeyAlias}
          )
          ;
  * <span data-ttu-id="8f744-174">Maak een externe bestandsindeling voor een csv-bestand.</span><span class="sxs-lookup"><span data-stu-id="8f744-174">Create an external file format for a csv file.</span></span> <span data-ttu-id="8f744-175">Gegevens zijn niet-gecomprimeerde en velden worden gescheiden met het sluisteken Hallo.</span><span class="sxs-lookup"><span data-stu-id="8f744-175">Data is uncompressed and fields are separated with hello pipe character.</span></span>
    
          CREATE EXTERNAL FILE FORMAT {csv_file_format}
          WITH
          (   
              FORMAT_TYPE = DELIMITEDTEXT,
              FORMAT_OPTIONS  
              (
                  FIELD_TERMINATOR ='','',
                  USE_TYPE_DEFAULT = TRUE
              )
          )
          ;
  * <span data-ttu-id="8f744-176">Externe tarief en tabellen voor NYC taxi gegevensset reis maken in Azure blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="8f744-176">Create external fare and trip tables for NYC taxi dataset in Azure blob storage.</span></span>
    
          CREATE EXTERNAL TABLE {external_nyctaxi_fare}
          (
              medallion varchar(50) not null,
              hack_license varchar(50) not null,
              vendor_id char(3),
              pickup_datetime datetime not null,
              payment_type char(3),
              fare_amount float,
              surcharge float,
              mta_tax float,
              tip_amount float,
              tolls_amount float,
              total_amount float
          )
          with (
              LOCATION    = ''/nyctaxifare/'',
              DATA_SOURCE = {nyctaxi_fare_storage},
              FILE_FORMAT = {csv_file_format},
              REJECT_TYPE = VALUE,
              REJECT_VALUE = 12     
          )  

            CREATE EXTERNAL TABLE {external_nyctaxi_trip}
            (
                   medallion varchar(50) not null,
                   hack_license varchar(50)  not null,
                   vendor_id char(3),
                   rate_code char(3),
                   store_and_fwd_flag char(3),
                   pickup_datetime datetime  not null,
                   dropoff_datetime datetime,
                   passenger_count int,
                   trip_time_in_secs bigint,
                   trip_distance float,
                   pickup_longitude varchar(30),
                   pickup_latitude varchar(30),
                   dropoff_longitude varchar(30),
                   dropoff_latitude varchar(30)
            )
            with (
                LOCATION    = ''/nyctaxitrip/'',
                DATA_SOURCE = {nyctaxi_trip_storage},
                FILE_FORMAT = {csv_file_format},
                REJECT_TYPE = VALUE,
                REJECT_VALUE = 12         
            )

    - <span data-ttu-id="8f744-177">Gegevens uit externe tabellen in Azure blob storage tooSQL Data Warehouse laden</span><span class="sxs-lookup"><span data-stu-id="8f744-177">Load data from external tables in Azure blob storage tooSQL Data Warehouse</span></span>

            CREATE TABLE {schemaname}.{nyctaxi_fare}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_fare}
            ;

            CREATE TABLE {schemaname}.{nyctaxi_trip}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            SELECT *
            FROM   {external_nyctaxi_trip}
            ;

    - <span data-ttu-id="8f744-178">Maken van een gegevenstabel voorbeeld (NYCTaxi_Sample) en gegevens tooit invoegen van het SQL-query's op Hallo reis en tarief tabellen selecteren.</span><span class="sxs-lookup"><span data-stu-id="8f744-178">Create a sample data table (NYCTaxi_Sample) and insert data tooit from selecting SQL queries on hello trip and fare tables.</span></span> <span data-ttu-id="8f744-179">(Een aantal stappen van dit scenario moet toouse deze voorbeeldtabel.)</span><span class="sxs-lookup"><span data-stu-id="8f744-179">(Some steps of this walkthrough needs toouse this sample table.)</span></span>

            CREATE TABLE {schemaname}.{nyctaxi_sample}
            WITH
            (   
                CLUSTERED COLUMNSTORE INDEX,
                DISTRIBUTION = HASH(medallion)
            )
            AS
            (
                SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount, f.total_amount, f.tip_amount,
                tipped = CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END,
                tip_class = CASE
                        WHEN (tip_amount = 0) THEN 0
                        WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
                        WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
                        WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
                        ELSE 4
                    END
                FROM {schemaname}.{nyctaxi_trip} t, {schemaname}.{nyctaxi_fare} f
                WHERE datepart("mi",t.pickup_datetime) = 1
                AND t.medallion = f.medallion
                AND   t.hack_license = f.hack_license
                AND   t.pickup_datetime = f.pickup_datetime
                AND   pickup_longitude <> ''0''
                AND   dropoff_longitude <> ''0''
            )
            ;

<span data-ttu-id="8f744-180">laadtijden van invloed op Hallo geografische locatie van uw storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="8f744-180">hello geographic location of your storage accounts affects load times.</span></span>

> [!NOTE]
> <span data-ttu-id="8f744-181">Afhankelijk van Hallo geografische locatie van uw persoonlijke blob storage-account, Hallo-proces voor het kopiëren van gegevens uit een openbare blob tooyour persoonlijke storage-account kan ongeveer 15 minuten duren, of zelfs meer en hello verwerken van het laden van gegevens uit uw storage-account Azure SQL DW tooyour kan duurt ongeveer 20 minuten of langer.</span><span class="sxs-lookup"><span data-stu-id="8f744-181">Depending on hello geographical location of your private blob storage account, hello process of copying data from a public blob tooyour private storage account can take about 15 minutes, or even longer,and hello process of loading data from your storage account tooyour Azure SQL DW could take 20 minutes or longer.</span></span>  
> 
> 

<span data-ttu-id="8f744-182">Hebt u toodecide wat doen als er dubbele bron en doel-bestanden.</span><span class="sxs-lookup"><span data-stu-id="8f744-182">You will have toodecide what do if you have duplicate source and destination files.</span></span>

> [!NOTE]
> <span data-ttu-id="8f744-183">Als Hallo .csv-bestanden toobe gekopieerd van Hallo openbare blob-opslag tooyour persoonlijke blob storage-account al in uw persoonlijke blob storage-account bestaat, AzCopy u wordt gevraagd of u wilt dat toooverwrite ze.</span><span class="sxs-lookup"><span data-stu-id="8f744-183">If hello .csv files toobe copied from hello public blob storage tooyour private blob storage account already exist in your private blob storage account, AzCopy will ask you whether you want toooverwrite them.</span></span> <span data-ttu-id="8f744-184">Als u niet dat toooverwrite ze, invoer wilt  **n**  wanneer u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="8f744-184">If you do not want toooverwrite them, input **n** when prompted.</span></span> <span data-ttu-id="8f744-185">Als u wilt dat toooverwrite **alle** , invoer **een** wanneer u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="8f744-185">If you want toooverwrite **all** of them, input **a** when prompted.</span></span> <span data-ttu-id="8f744-186">U kunt ook invoer **y** afzonderlijk toooverwrite .csv-bestanden.</span><span class="sxs-lookup"><span data-stu-id="8f744-186">You can also input **y** toooverwrite .csv files individually.</span></span>
> 
> 

![#21 tekenen][21]

<span data-ttu-id="8f744-188">U kunt uw eigen gegevens.</span><span class="sxs-lookup"><span data-stu-id="8f744-188">You can use your own data.</span></span> <span data-ttu-id="8f744-189">Als uw gegevens in uw on-premises machine in uw toepassing praktijk is, kunt u nog steeds AzCopy tooupload lokale gegevens tooyour persoonlijke Azure-blobopslag.</span><span class="sxs-lookup"><span data-stu-id="8f744-189">If your data is in your on-premises machine in your real life application, you can still use AzCopy tooupload on-premises data tooyour private Azure blob storage.</span></span> <span data-ttu-id="8f744-190">U hoeft alleen toochange hello **bron** locatie, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, in Hallo AzCopy-opdracht van Hallo PowerShell script bestand toohello lokale map met uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="8f744-190">You only need toochange hello **Source** location, `$Source = "http://getgoing.blob.core.windows.net/public/nyctaxidataset"`, in hello AzCopy command of hello PowerShell script file toohello local directory that contains your data.</span></span>

> [!TIP]
> <span data-ttu-id="8f744-191">Als uw gegevens zich al in uw persoonlijke Azure blob-opslag in uw toepassing praktijk, kunt u Hallo AzCopy stap in Hallo PowerShell-script en Hallo gegevens tooAzure SQL DW rechtstreeks te uploaden overslaan.</span><span class="sxs-lookup"><span data-stu-id="8f744-191">If your data is already in your private Azure blob storage in your real life application, you can skip hello AzCopy step in hello PowerShell script and directly upload hello data tooAzure SQL DW.</span></span> <span data-ttu-id="8f744-192">Hiervoor moet extra bewerkt van Hallo script tootailor toohello indeling van uw gegevens.</span><span class="sxs-lookup"><span data-stu-id="8f744-192">This will require additional edits of hello script tootailor it toohello format of your data.</span></span>
> 
> 

<span data-ttu-id="8f744-193">Deze Powershell-script ook aangesloten in hello Azure SQL DW-informatie naar Hallo exploratie voorbeeld gegevensbestanden SQLDW_Explorations.sql, SQLDW_Explorations.ipynb en SQLDW_Explorations_Scripts.py zodat deze drie bestanden gereed toobe geprobeerd onmiddellijk uit Nadat de Hallo PowerShell-script is voltooid.</span><span class="sxs-lookup"><span data-stu-id="8f744-193">This Powershell script also plugs in hello Azure SQL DW information into hello data exploration example files SQLDW_Explorations.sql, SQLDW_Explorations.ipynb, and SQLDW_Explorations_Scripts.py so that these three files are ready toobe tried out instantly after hello PowerShell script completes.</span></span>

<span data-ttu-id="8f744-194">Na een geslaagde uitvoering, ziet u scherm, zoals hieronder:</span><span class="sxs-lookup"><span data-stu-id="8f744-194">After a successful execution, you will see screen like below:</span></span>

![][20]

## <span data-ttu-id="8f744-195"><a name="dbexplore"></a>Gegevensverkenning en functie-engineering in Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="8f744-195"><a name="dbexplore"></a>Data exploration and feature engineering in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="8f744-196">In deze sectie we gegevens te verkennen en functie generatie uitvoeren door met het SQL-query's uitvoeren in Azure SQL DW direct met **Visual Studio Data Tools**.</span><span class="sxs-lookup"><span data-stu-id="8f744-196">In this section, we perform data exploration and feature generation by running SQL queries against Azure SQL DW directly using **Visual Studio Data Tools**.</span></span> <span data-ttu-id="8f744-197">Alle SQL-query's gebruikt in deze sectie vindt u in Hallo voorbeeld van een script met de naam *SQLDW_Explorations.sql*.</span><span class="sxs-lookup"><span data-stu-id="8f744-197">All SQL queries used in this section can be found in hello sample script named *SQLDW_Explorations.sql*.</span></span> <span data-ttu-id="8f744-198">Dit bestand is al gedownload tooyour lokale directory door Hallo PowerShell-script.</span><span class="sxs-lookup"><span data-stu-id="8f744-198">This file has already been downloaded tooyour local directory by hello PowerShell script.</span></span> <span data-ttu-id="8f744-199">U kunt ook ophalen via [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span><span class="sxs-lookup"><span data-stu-id="8f744-199">You can also retrieve it from [GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/SQLDW/SQLDW_Explorations.sql).</span></span> <span data-ttu-id="8f744-200">Maar Hallo-bestand in GitHub heeft geen hello Azure SQL DW-informatie is aangesloten.</span><span class="sxs-lookup"><span data-stu-id="8f744-200">But hello file in GitHub does not have hello Azure SQL DW information plugged in.</span></span>

<span data-ttu-id="8f744-201">Verbinding maken met Visual Studio Hallo SQL DW-aanmeldingsnaam en wachtwoord van Azure SQL DW tooyour en geopend Hallo **SQL Object Explorer** tooconfirm Hallo database en tabellen zijn geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="8f744-201">Connect tooyour Azure SQL DW using Visual Studio with hello SQL DW login name and password and open up hello **SQL Object Explorer** tooconfirm hello database and tables have been imported.</span></span> <span data-ttu-id="8f744-202">Hallo ophalen *SQLDW_Explorations.sql* bestand.</span><span class="sxs-lookup"><span data-stu-id="8f744-202">Retrieve hello *SQLDW_Explorations.sql* file.</span></span>

> [!NOTE]
> <span data-ttu-id="8f744-203">tooopen een Parallel Data Warehouse (PDW) query-editor gebruiken Hallo **nieuwe Query** opdracht terwijl uw PDW is geselecteerd in Hallo **SQL Object Explorer**.</span><span class="sxs-lookup"><span data-stu-id="8f744-203">tooopen a Parallel Data Warehouse (PDW) query editor, use hello **New Query** command while your PDW is selected in hello **SQL Object Explorer**.</span></span> <span data-ttu-id="8f744-204">Hallo standaard de SQL-query-editor wordt niet ondersteund door PDW.</span><span class="sxs-lookup"><span data-stu-id="8f744-204">hello standard SQL query editor is not supported by PDW.</span></span>
> 
> 

<span data-ttu-id="8f744-205">Hier volgen Hallo type gegevens te verkennen en functie generatie uitgevoerd in deze sectie:</span><span class="sxs-lookup"><span data-stu-id="8f744-205">Here are hello type of data exploration and feature generation tasks performed in this section:</span></span>

* <span data-ttu-id="8f744-206">Verken de gegevens distributies van enkele velden in verschillende tijdvensters.</span><span class="sxs-lookup"><span data-stu-id="8f744-206">Explore data distributions of a few fields in varying time windows.</span></span>
* <span data-ttu-id="8f744-207">Onderzoek de kwaliteit van de gegevens van Hallo breedtegraad velden.</span><span class="sxs-lookup"><span data-stu-id="8f744-207">Investigate data quality of hello longitude and latitude fields.</span></span>
* <span data-ttu-id="8f744-208">Genereren van binaire en multiklassen classificatielabels op basis van Hallo **tip\_bedrag**.</span><span class="sxs-lookup"><span data-stu-id="8f744-208">Generate binary and multiclass classification labels based on hello **tip\_amount**.</span></span>
* <span data-ttu-id="8f744-209">Genereren van functies en reis afstanden compute/vergelijken.</span><span class="sxs-lookup"><span data-stu-id="8f744-209">Generate features and compute/compare trip distances.</span></span>
* <span data-ttu-id="8f744-210">Hallo twee tabellen samenvoegen en uitpakken van een steekproef die gebruikt toobuild modellen worden.</span><span class="sxs-lookup"><span data-stu-id="8f744-210">Join hello two tables and extract a random sample that will be used toobuild models.</span></span>

### <a name="data-import-verification"></a><span data-ttu-id="8f744-211">Gegevens importeren verificatie</span><span class="sxs-lookup"><span data-stu-id="8f744-211">Data import verification</span></span>
<span data-ttu-id="8f744-212">Deze query's bieden een snelle Hallo aantal rijen en kolommen in tabellen ingevuld met oudere versies van Polybase parallelle bulksgewijs importeert, Hallo-verificatie</span><span class="sxs-lookup"><span data-stu-id="8f744-212">These queries provide a quick verification of hello number of rows and columns in hello tables populated earlier using Polybase's parallel bulk import,</span></span>

    -- Report number of rows in table <nyctaxi_trip> without table scan
    SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')

    -- Report number of columns in table <nyctaxi_trip>
    SELECT COUNT(*) FROM information_schema.columns WHERE table_name = '<nyctaxi_trip>' AND table_schema = '<schemaname>'

<span data-ttu-id="8f744-213">**Uitvoer:** krijgt u 173,179,759 rijen en 14 kolommen.</span><span class="sxs-lookup"><span data-stu-id="8f744-213">**Output:** You should get 173,179,759 rows and 14 columns.</span></span>

### <a name="exploration-trip-distribution-by-medallion"></a><span data-ttu-id="8f744-214">Exploratie: Reis distributie door straten</span><span class="sxs-lookup"><span data-stu-id="8f744-214">Exploration: Trip distribution by medallion</span></span>
<span data-ttu-id="8f744-215">Deze voorbeeldquery identificeert Hallo medallions (taxi getallen) die meer dan 100 reizen voltooid binnen een opgegeven periode.</span><span class="sxs-lookup"><span data-stu-id="8f744-215">This example query identifies hello medallions (taxi numbers) that completed more than 100 trips within a specified time period.</span></span> <span data-ttu-id="8f744-216">Hallo query wilt profiteren van Hallo gepartitioneerde tabeltoegang omdat deze wordt waarbij door Hallo partitieschema van **ophalen\_datetime**.</span><span class="sxs-lookup"><span data-stu-id="8f744-216">hello query would benefit from hello partitioned table access since it is conditioned by hello partition scheme of **pickup\_datetime**.</span></span> <span data-ttu-id="8f744-217">Opvragen van de volledige gegevensset Hallo maakt ook gebruik van de gepartitioneerde tabel Hallo en/of index van de scan.</span><span class="sxs-lookup"><span data-stu-id="8f744-217">Querying hello full dataset will also make use of hello partitioned table and/or index scan.</span></span>

    SELECT medallion, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    GROUP BY medallion
    HAVING COUNT(*) > 100

<span data-ttu-id="8f744-218">**Uitvoer:** Hallo query moet een tabel met rijen geven Hallo 13,369 medallions (taxi's) worden geretourneerd en Hallo aantal reis voltooid door ze in 2013.</span><span class="sxs-lookup"><span data-stu-id="8f744-218">**Output:** hello query should return a table with rows specifying hello 13,369 medallions (taxis) and hello number of trip completed by them in 2013.</span></span> <span data-ttu-id="8f744-219">de laatste kolom Hallo bevat Hallo aantal Hallo reizen voltooid.</span><span class="sxs-lookup"><span data-stu-id="8f744-219">hello last column contains hello count of hello number of trips completed.</span></span>

### <a name="exploration-trip-distribution-by-medallion-and-hacklicense"></a><span data-ttu-id="8f744-220">Exploratie: Reis distributie door straten en hack_license</span><span class="sxs-lookup"><span data-stu-id="8f744-220">Exploration: Trip distribution by medallion and hack_license</span></span>
<span data-ttu-id="8f744-221">In dit voorbeeld identificeert Hallo medallions (taxi getallen) en hack_license getallen (stuurprogramma's) die voltooid zijn meer dan 100 reizen binnen een opgegeven periode.</span><span class="sxs-lookup"><span data-stu-id="8f744-221">This example identifies hello medallions (taxi numbers) and hack_license numbers (drivers) that completed more than 100 trips within a specified time period.</span></span>

    SELECT medallion, hack_license, COUNT(*)
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130131'
    GROUP BY medallion, hack_license
    HAVING COUNT(*) > 100

<span data-ttu-id="8f744-222">**Uitvoer:** Hallo query als resultaat moet een tabel met 13,369 rijen Hallo 13,369 auto stuurprogramma-id's die u meer die 100 reizen in 2013 hebt opgeven.</span><span class="sxs-lookup"><span data-stu-id="8f744-222">**Output:** hello query should return a table with 13,369 rows specifying hello 13,369 car/driver IDs that have completed more that 100 trips in 2013.</span></span> <span data-ttu-id="8f744-223">de laatste kolom Hallo bevat Hallo aantal Hallo reizen voltooid.</span><span class="sxs-lookup"><span data-stu-id="8f744-223">hello last column contains hello count of hello number of trips completed.</span></span>

### <a name="data-quality-assessment-verify-records-with-incorrect-longitude-andor-latitude"></a><span data-ttu-id="8f744-224">Gegevens beoordeling: Controleer of records met onjuiste lengtegraad en/of breedtegraad</span><span class="sxs-lookup"><span data-stu-id="8f744-224">Data quality assessment: Verify records with incorrect longitude and/or latitude</span></span>
<span data-ttu-id="8f744-225">In dit voorbeeld onderzoekt als Hallo lengtegraad en/of breedtegraad velden een ongeldige waarde bevatten (radiaal graden moet tussen-90 en 90), of (0, 0) coördinaten.</span><span class="sxs-lookup"><span data-stu-id="8f744-225">This example investigates if any of hello longitude and/or latitude fields either contain an invalid value (radian degrees should be between -90 and 90), or have (0, 0) coordinates.</span></span>

    SELECT COUNT(*) FROM <schemaname>.<nyctaxi_trip>
    WHERE pickup_datetime BETWEEN '20130101' AND '20130331'
    AND  (CAST(pickup_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(pickup_latitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_longitude AS float) NOT BETWEEN -90 AND 90
    OR    CAST(dropoff_latitude AS float) NOT BETWEEN -90 AND 90
    OR    (pickup_longitude = '0' AND pickup_latitude = '0')
    OR    (dropoff_longitude = '0' AND dropoff_latitude = '0'))

<span data-ttu-id="8f744-226">**Uitvoer:** Hallo query retourneert 837,467 reizen die ongeldige lengtegraad en/of breedtegraad velden hebben.</span><span class="sxs-lookup"><span data-stu-id="8f744-226">**Output:** hello query returns 837,467 trips that have invalid longitude and/or latitude fields.</span></span>

### <a name="exploration-tipped-vs-not-tipped-trips-distribution"></a><span data-ttu-id="8f744-227">Exploratie: Punt versus niet Gekantelde reizen distributie</span><span class="sxs-lookup"><span data-stu-id="8f744-227">Exploration: Tipped vs. not tipped trips distribution</span></span>
<span data-ttu-id="8f744-228">Dit voorbeeld wordt gezocht naar Hallo aantal reizen versus Hallo nummer zijn punt wanneer geen punt zijn in een opgegeven periode (of in de volledige gegevensset Hallo als die betrekking hebben op Hallo volledige jaar als u deze hier is ingesteld).</span><span class="sxs-lookup"><span data-stu-id="8f744-228">This example finds hello number of trips that were tipped vs. hello number that were not tipped in a specified time period (or in hello full dataset if covering hello full year as it is set up here).</span></span> <span data-ttu-id="8f744-229">Deze verdeling weerspiegelt Hallo binaire label distributie toobe later gebruikt voor het modelleren van de binaire indeling.</span><span class="sxs-lookup"><span data-stu-id="8f744-229">This distribution reflects hello binary label distribution toobe later used for binary classification modeling.</span></span>

    SELECT tipped, COUNT(*) AS tip_freq FROM (
      SELECT CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped, tip_amount
      FROM <schemaname>.<nyctaxi_fare>
      WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tipped

<span data-ttu-id="8f744-230">**Uitvoer:** Hallo query moet return Hallo volgende frequenties tip voor Hallo jaar 2013: 90,447,622 punt en 82,264,709 niet punt.</span><span class="sxs-lookup"><span data-stu-id="8f744-230">**Output:** hello query should return hello following tip frequencies for hello year 2013: 90,447,622 tipped and 82,264,709 not-tipped.</span></span>

### <a name="exploration-tip-classrange-distribution"></a><span data-ttu-id="8f744-231">Exploratie: Verdeling Tip klasse/bereik</span><span class="sxs-lookup"><span data-stu-id="8f744-231">Exploration: Tip class/range distribution</span></span>
<span data-ttu-id="8f744-232">In dit voorbeeld berekent Hallo distributie van tip bereiken in een bepaald moment periode (of in de volledige gegevensset Hallo als die betrekking hebben op Hallo volledige jaar).</span><span class="sxs-lookup"><span data-stu-id="8f744-232">This example computes hello distribution of tip ranges in a given time period (or in hello full dataset if covering hello full year).</span></span> <span data-ttu-id="8f744-233">Dit is distributiepunt Hallo Hallo label klassen die later wordt gebruikt voor multiklassen classificatie modellering.</span><span class="sxs-lookup"><span data-stu-id="8f744-233">This is hello distribution of hello label classes that will be used later for multiclass classification modeling.</span></span>

    SELECT tip_class, COUNT(*) AS tip_freq FROM (
        SELECT CASE
            WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_fare>
    WHERE pickup_datetime BETWEEN '20130101' AND '20131231') tc
    GROUP BY tip_class

<span data-ttu-id="8f744-234">**Uitvoer:**</span><span class="sxs-lookup"><span data-stu-id="8f744-234">**Output:**</span></span>

| <span data-ttu-id="8f744-235">tip_class</span><span class="sxs-lookup"><span data-stu-id="8f744-235">tip_class</span></span> | <span data-ttu-id="8f744-236">tip_freq</span><span class="sxs-lookup"><span data-stu-id="8f744-236">tip_freq</span></span> |
| --- | --- |
| <span data-ttu-id="8f744-237">1</span><span class="sxs-lookup"><span data-stu-id="8f744-237">1</span></span> |<span data-ttu-id="8f744-238">82230915</span><span class="sxs-lookup"><span data-stu-id="8f744-238">82230915</span></span> |
| <span data-ttu-id="8f744-239">2</span><span class="sxs-lookup"><span data-stu-id="8f744-239">2</span></span> |<span data-ttu-id="8f744-240">6198803</span><span class="sxs-lookup"><span data-stu-id="8f744-240">6198803</span></span> |
| <span data-ttu-id="8f744-241">3</span><span class="sxs-lookup"><span data-stu-id="8f744-241">3</span></span> |<span data-ttu-id="8f744-242">1932223</span><span class="sxs-lookup"><span data-stu-id="8f744-242">1932223</span></span> |
| <span data-ttu-id="8f744-243">0</span><span class="sxs-lookup"><span data-stu-id="8f744-243">0</span></span> |<span data-ttu-id="8f744-244">82264625</span><span class="sxs-lookup"><span data-stu-id="8f744-244">82264625</span></span> |
| <span data-ttu-id="8f744-245">4</span><span class="sxs-lookup"><span data-stu-id="8f744-245">4</span></span> |<span data-ttu-id="8f744-246">85765</span><span class="sxs-lookup"><span data-stu-id="8f744-246">85765</span></span> |

### <a name="exploration-compute-and-compare-trip-distance"></a><span data-ttu-id="8f744-247">Exploratie: Berekenen en reis afstand vergelijken</span><span class="sxs-lookup"><span data-stu-id="8f744-247">Exploration: Compute and compare trip distance</span></span>
<span data-ttu-id="8f744-248">In dit voorbeeld Hallo ophalen en inleverbibliotheek lengtegraad converteert en breedtegraad tooSQL Geografie verwijst, Hallo reis afstand met behulp van SQL Geografie punten verschil wordt berekend en retourneert een willekeurig aantal Hallo resultaten voor vergelijking.</span><span class="sxs-lookup"><span data-stu-id="8f744-248">This example converts hello pickup and drop-off longitude and latitude tooSQL geography points, computes hello trip distance using SQL geography points difference, and returns a random sample of hello results for comparison.</span></span> <span data-ttu-id="8f744-249">Hallo voorbeeld beperkt Hallo resultaten toovalid coördineert alleen met behulp van Hallo kwaliteit assessment gegevensquery eerder besproken.</span><span class="sxs-lookup"><span data-stu-id="8f744-249">hello example limits hello results toovalid coordinates only using hello data quality assessment query covered earlier.</span></span>

    /****** Object:  UserDefinedFunction [dbo].[fnCalculateDistance] ******/
    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function toocalculate hello direct distance  in mile between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

### <a name="feature-engineering-using-sql-functions"></a><span data-ttu-id="8f744-250">Functie-engineering met behulp van SQL-functies</span><span class="sxs-lookup"><span data-stu-id="8f744-250">Feature engineering using SQL functions</span></span>
<span data-ttu-id="8f744-251">SQL-functies kunnen soms een efficiënte optie voor functie-engineering zijn.</span><span class="sxs-lookup"><span data-stu-id="8f744-251">Sometimes SQL functions can be an efficient option for feature engineering.</span></span> <span data-ttu-id="8f744-252">In dit overzicht hebben we een SQL functie toocalculate Hallo direct afstand tussen Hallo ophalen en dropoff locaties gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="8f744-252">In this walkthrough, we defined a SQL function toocalculate hello direct distance between hello pickup and dropoff locations.</span></span> <span data-ttu-id="8f744-253">U kunt uitvoeren Hallo volgende SQL-scripts in **Visual Studio Data Tools**.</span><span class="sxs-lookup"><span data-stu-id="8f744-253">You can run hello following SQL scripts in **Visual Studio Data Tools**.</span></span>

<span data-ttu-id="8f744-254">Hier volgt Hallo SQL-script waarmee wordt gedefinieerd Hallo afstand-functie.</span><span class="sxs-lookup"><span data-stu-id="8f744-254">Here is hello SQL script that defines hello distance function.</span></span>

    SET ANSI_NULLS ON
    GO

    SET QUOTED_IDENTIFIER ON
    GO

    IF EXISTS (SELECT * FROM sys.objects WHERE type IN ('FN', 'IF') AND name = 'fnCalculateDistance')
      DROP FUNCTION fnCalculateDistance
    GO

    -- User-defined function calculate hello direct distance between two geographical coordinates.
    CREATE FUNCTION [dbo].[fnCalculateDistance] (@Lat1 float, @Long1 float, @Lat2 float, @Long2 float)

    RETURNS float
    AS
    BEGIN
          DECLARE @distance decimal(28, 10)
          -- Convert tooradians
          SET @Lat1 = @Lat1 / 57.2958
          SET @Long1 = @Long1 / 57.2958
          SET @Lat2 = @Lat2 / 57.2958
          SET @Long2 = @Long2 / 57.2958
          -- Calculate distance
          SET @distance = (SIN(@Lat1) * SIN(@Lat2)) + (COS(@Lat1) * COS(@Lat2) * COS(@Long2 - @Long1))
          --Convert toomiles
          IF @distance <> 0
          BEGIN
            SET @distance = 3958.75 * ATAN(SQRT(1 - POWER(@distance, 2)) / @distance);
          END
          RETURN @distance
    END
    GO

<span data-ttu-id="8f744-255">Hier volgt een voorbeeld toocall deze functie toogenerate functies in uw SQL-query:</span><span class="sxs-lookup"><span data-stu-id="8f744-255">Here is an example toocall this function toogenerate features in your SQL query:</span></span>

    -- Sample query toocall hello function toocreate features
    SELECT pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude,
    dbo.fnCalculateDistance(pickup_latitude, pickup_longitude, dropoff_latitude, dropoff_longitude) AS DirectDistance
    FROM <schemaname>.<nyctaxi_trip>
    WHERE datepart("mi",pickup_datetime)=1
    AND CAST(pickup_latitude AS float) BETWEEN -90 AND 90
    AND CAST(dropoff_latitude AS float) BETWEEN -90 AND 90
    AND pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="8f744-256">**Uitvoer:** deze query wordt een tabel (met 2,803,538 rijen) gegenereerd met ophalen en dropoff Latitude en lengten en de bijbehorende van Hallo directe afstanden in mijl.</span><span class="sxs-lookup"><span data-stu-id="8f744-256">**Output:** This query generates a table (with 2,803,538 rows) with pickup and dropoff latitudes and longitudes and hello corresponding direct distances in miles.</span></span> <span data-ttu-id="8f744-257">Hier volgen Hallo resultaten voor de eerste 3 rijen:</span><span class="sxs-lookup"><span data-stu-id="8f744-257">Here are hello results for first 3 rows:</span></span>

|  | <span data-ttu-id="8f744-258">pickup_latitude</span><span class="sxs-lookup"><span data-stu-id="8f744-258">pickup_latitude</span></span> | <span data-ttu-id="8f744-259">pickup_longitude</span><span class="sxs-lookup"><span data-stu-id="8f744-259">pickup_longitude</span></span> | <span data-ttu-id="8f744-260">dropoff_latitude</span><span class="sxs-lookup"><span data-stu-id="8f744-260">dropoff_latitude</span></span> | <span data-ttu-id="8f744-261">dropoff_longitude</span><span class="sxs-lookup"><span data-stu-id="8f744-261">dropoff_longitude</span></span> | <span data-ttu-id="8f744-262">DirectDistance</span><span class="sxs-lookup"><span data-stu-id="8f744-262">DirectDistance</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="8f744-263">1</span><span class="sxs-lookup"><span data-stu-id="8f744-263">1</span></span> |<span data-ttu-id="8f744-264">40.731804</span><span class="sxs-lookup"><span data-stu-id="8f744-264">40.731804</span></span> |<span data-ttu-id="8f744-265">-74.001083</span><span class="sxs-lookup"><span data-stu-id="8f744-265">-74.001083</span></span> |<span data-ttu-id="8f744-266">40.736622</span><span class="sxs-lookup"><span data-stu-id="8f744-266">40.736622</span></span> |<span data-ttu-id="8f744-267">-73.988953</span><span class="sxs-lookup"><span data-stu-id="8f744-267">-73.988953</span></span> |<span data-ttu-id="8f744-268">.7169601222</span><span class="sxs-lookup"><span data-stu-id="8f744-268">.7169601222</span></span> |
| <span data-ttu-id="8f744-269">2</span><span class="sxs-lookup"><span data-stu-id="8f744-269">2</span></span> |<span data-ttu-id="8f744-270">40.715794</span><span class="sxs-lookup"><span data-stu-id="8f744-270">40.715794</span></span> |<span data-ttu-id="8f744-271">-74,010635</span><span class="sxs-lookup"><span data-stu-id="8f744-271">-74,010635</span></span> |<span data-ttu-id="8f744-272">40.725338</span><span class="sxs-lookup"><span data-stu-id="8f744-272">40.725338</span></span> |<span data-ttu-id="8f744-273">-74.00399</span><span class="sxs-lookup"><span data-stu-id="8f744-273">-74.00399</span></span> |<span data-ttu-id="8f744-274">.7448343721</span><span class="sxs-lookup"><span data-stu-id="8f744-274">.7448343721</span></span> |
| <span data-ttu-id="8f744-275">3</span><span class="sxs-lookup"><span data-stu-id="8f744-275">3</span></span> |<span data-ttu-id="8f744-276">40.761456</span><span class="sxs-lookup"><span data-stu-id="8f744-276">40.761456</span></span> |<span data-ttu-id="8f744-277">-73.999886</span><span class="sxs-lookup"><span data-stu-id="8f744-277">-73.999886</span></span> |<span data-ttu-id="8f744-278">40.766544</span><span class="sxs-lookup"><span data-stu-id="8f744-278">40.766544</span></span> |<span data-ttu-id="8f744-279">-73.988228</span><span class="sxs-lookup"><span data-stu-id="8f744-279">-73.988228</span></span> |<span data-ttu-id="8f744-280">0.7037227967</span><span class="sxs-lookup"><span data-stu-id="8f744-280">0.7037227967</span></span> |

### <a name="prepare-data-for-model-building"></a><span data-ttu-id="8f744-281">Gegevens voorbereiden voor het model bouwen</span><span class="sxs-lookup"><span data-stu-id="8f744-281">Prepare data for model building</span></span>
<span data-ttu-id="8f744-282">Hallo volgende joins Hallo query **nyctaxi\_reis** en **nyctaxi\_tarief** tabellen, genereert een label binaire classificatie **punt**, een meerdere klasse classificatie label **tip\_klasse**, en een voorbeeld van een haalt uit Hallo volledige gekoppelde gegevensset.</span><span class="sxs-lookup"><span data-stu-id="8f744-282">hello following query joins hello **nyctaxi\_trip** and **nyctaxi\_fare** tables, generates a binary classification label **tipped**, a multi-class classification label **tip\_class**, and extracts a sample from hello full joined dataset.</span></span> <span data-ttu-id="8f744-283">Hallo steekproeven wordt uitgevoerd door bij het ophalen van een subset van Hallo reizen op basis van tijd ophalen.</span><span class="sxs-lookup"><span data-stu-id="8f744-283">hello sampling is done by retrieving a subset of hello trips based on pickup time.</span></span>  <span data-ttu-id="8f744-284">Deze query kan worden gekopieerd en geplakt rechtstreeks in Hallo [Azure Machine Learning Studio](https://studio.azureml.net) [importgegevens] [ import-data] -module voor directe gegevensopname vanaf Hallo SQL database-exemplaar in Azure.</span><span class="sxs-lookup"><span data-stu-id="8f744-284">This query can be copied then pasted directly in hello [Azure Machine Learning Studio](https://studio.azureml.net) [Import Data][import-data] module for direct data ingestion from hello SQL database instance in Azure.</span></span> <span data-ttu-id="8f744-285">Hallo query worden records met onjuiste uitgesloten (0, 0) coördinaten.</span><span class="sxs-lookup"><span data-stu-id="8f744-285">hello query excludes records with incorrect (0, 0) coordinates.</span></span>

    SELECT t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax, f.tolls_amount,     f.total_amount, f.tip_amount,
        CASE WHEN (tip_amount > 0) THEN 1 ELSE 0 END AS tipped,
        CASE WHEN (tip_amount = 0) THEN 0
            WHEN (tip_amount > 0 AND tip_amount <= 5) THEN 1
            WHEN (tip_amount > 5 AND tip_amount <= 10) THEN 2
            WHEN (tip_amount > 10 AND tip_amount <= 20) THEN 3
            ELSE 4
        END AS tip_class
    FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
    WHERE datepart("mi",t.pickup_datetime) = 1
    AND   t.medallion = f.medallion
    AND   t.hack_license = f.hack_license
    AND   t.pickup_datetime = f.pickup_datetime
    AND   pickup_longitude != '0' AND dropoff_longitude != '0'

<span data-ttu-id="8f744-286">Wanneer u klaar tooproceed tooAzure Machine Learning bent, mag u ofwel:</span><span class="sxs-lookup"><span data-stu-id="8f744-286">When you are ready tooproceed tooAzure Machine Learning, you may either:</span></span>  

1. <span data-ttu-id="8f744-287">Sla Hallo uiteindelijke SQL query tooextract en voorbeeld Hallo gegevens en kopiëren en plakken Hallo query rechtstreeks in een [importgegevens] [ import-data] -module in Azure Machine Learning, of</span><span class="sxs-lookup"><span data-stu-id="8f744-287">Save hello final SQL query tooextract and sample hello data and copy-paste hello query directly into a [Import Data][import-data] module in Azure Machine Learning, or</span></span>
2. <span data-ttu-id="8f744-288">Hallo door actieve en permanent engineering gegevens die u van plan bent toouse voor model bouwen in een nieuwe SQL DW tabel en de nieuwe tabel hello gebruiken in Hallo [importgegevens] [ import-data] -module in Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="8f744-288">Persist hello sampled and engineered data you plan toouse for model building in a new SQL DW table and use hello new table in hello [Import Data][import-data] module in Azure Machine Learning.</span></span> <span data-ttu-id="8f744-289">Hallo PowerShell-script in een eerdere stap heeft dit voor u gedaan.</span><span class="sxs-lookup"><span data-stu-id="8f744-289">hello PowerShell script in earlier step has done this for you.</span></span> <span data-ttu-id="8f744-290">U kunt rechtstreeks uit deze tabel in Hallo gegevens importeren-module lezen.</span><span class="sxs-lookup"><span data-stu-id="8f744-290">You can read directly from this table in hello Import Data module.</span></span>

## <span data-ttu-id="8f744-291"><a name="ipnb"></a>Gegevensverkenning en functie-engineering in IPython notebook</span><span class="sxs-lookup"><span data-stu-id="8f744-291"><a name="ipnb"></a>Data exploration and feature engineering in IPython notebook</span></span>
<span data-ttu-id="8f744-292">In deze sectie wordt uitgevoerd, er gegevensverkenning en functie genereren met behulp van beide Python en SQL-query's op Hallo SQL DW eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8f744-292">In this section, we will perform data exploration and feature generation using both Python and SQL queries against hello SQL DW created earlier.</span></span> <span data-ttu-id="8f744-293">Een voorbeeld IPython notebook met de naam **SQLDW_Explorations.ipynb** en een scriptbestand Python **SQLDW_Explorations_Scripts.py** lokale map voor gedownloade tooyour zijn.</span><span class="sxs-lookup"><span data-stu-id="8f744-293">A sample IPython notebook named **SQLDW_Explorations.ipynb** and a Python script file **SQLDW_Explorations_Scripts.py** have been downloaded tooyour local directory.</span></span> <span data-ttu-id="8f744-294">Ze zijn ook beschikbaar is op [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span><span class="sxs-lookup"><span data-stu-id="8f744-294">They are also available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/SQLDW).</span></span> <span data-ttu-id="8f744-295">Deze twee bestanden zijn identiek in Python-scripts.</span><span class="sxs-lookup"><span data-stu-id="8f744-295">These two files are identical in Python scripts.</span></span> <span data-ttu-id="8f744-296">Hallo Python scriptbestand beschikbaar tooyou als er geen een IPython laptop-server.</span><span class="sxs-lookup"><span data-stu-id="8f744-296">hello Python script file is provided tooyou in case you do not have an IPython Notebook server.</span></span> <span data-ttu-id="8f744-297">Deze twee bestanden zijn ontworpen onder Python steekproef **Python 2.7**.</span><span class="sxs-lookup"><span data-stu-id="8f744-297">These two sample Python files are designed under **Python 2.7**.</span></span>

<span data-ttu-id="8f744-298">Hallo nodig Azure SQL DW-informatie in Hallo steekproef IPython Notebook en Hallo Python script bestand gedownloade tooyour lokale computer is aangesloten door Hallo PowerShell-script eerder.</span><span class="sxs-lookup"><span data-stu-id="8f744-298">hello needed Azure SQL DW information in hello sample IPython Notebook and hello Python script file downloaded tooyour local machine has been plugged in by hello PowerShell script previously.</span></span> <span data-ttu-id="8f744-299">Ze zijn uitvoerbare zonder dat aanpassingen.</span><span class="sxs-lookup"><span data-stu-id="8f744-299">They are executable without any modification.</span></span>

<span data-ttu-id="8f744-300">Als u al een AzureML-werkruimte hebt ingesteld, kunt u rechtstreeks uploaden Hallo voorbeeld IPython Notebook toohello AzureML IPython Notebook service en start het uitvoert.</span><span class="sxs-lookup"><span data-stu-id="8f744-300">If you have already set up an AzureML workspace, you can directly upload hello sample IPython Notebook toohello AzureML IPython Notebook service and start running it.</span></span> <span data-ttu-id="8f744-301">Hier volgen Hallo stappen tooupload tooAzureML IPython Notebook service:</span><span class="sxs-lookup"><span data-stu-id="8f744-301">Here are hello steps tooupload tooAzureML IPython Notebook service:</span></span>

1. <span data-ttu-id="8f744-302">Aanmelden tooyour AzureML werkruimte 'Studio' hello boven, en op 'NOTITIEBLOKKEN' aan de linkerkant Hallo van Hallo-webpagina.</span><span class="sxs-lookup"><span data-stu-id="8f744-302">Log in tooyour AzureML workspace, click "Studio" at hello top, and click "NOTEBOOKS" on hello left side of hello web page.</span></span>
   
    ![#22 tekenen][22]
2. <span data-ttu-id="8f744-304">Klik op 'Nieuw' op Hallo links benedenhoek van Hallo webpagina en selecteer ' Python 2".</span><span class="sxs-lookup"><span data-stu-id="8f744-304">Click "NEW" on hello left bottom corner of hello web page, and select "Python 2".</span></span> <span data-ttu-id="8f744-305">Vervolgens een toohello naam laptop en klik op Hallo vinkje toocreate Hallo nieuw leeg IPython Notebook.</span><span class="sxs-lookup"><span data-stu-id="8f744-305">Then, provide a name toohello notebook and click hello check mark toocreate hello new blank IPython Notebook.</span></span>
   
    ![#23 tekenen][23]
3. <span data-ttu-id="8f744-307">Klik op Hallo 'Jupyter' symbool op Hallo links bovenhoek van Hallo nieuwe IPython laptop.</span><span class="sxs-lookup"><span data-stu-id="8f744-307">Click hello "Jupyter" symbol on hello left top corner of hello new IPython Notebook.</span></span>
   
    ![#24 tekenen][24]
4. <span data-ttu-id="8f744-309">Slepen en neerzetten Hallo voorbeeld IPython Notebook toohello **structuur** pagina van uw service van AzureML IPython Notebook en klik op **uploaden**.</span><span class="sxs-lookup"><span data-stu-id="8f744-309">Drag and drop hello sample IPython Notebook toohello **tree** page of your AzureML IPython Notebook service, and click **Upload**.</span></span> <span data-ttu-id="8f744-310">Vervolgens worden Hallo voorbeeld IPython Notebook geüploade toohello AzureML IPython Notebook service.</span><span class="sxs-lookup"><span data-stu-id="8f744-310">Then, hello sample IPython Notebook will be uploaded toohello AzureML IPython Notebook service.</span></span>
   
    ![#25 tekenen][25]

<span data-ttu-id="8f744-312">In de volgorde toorun Hallo steekproef IPython Notebook of Python-scriptbestand Hallo, hello volgende Python pakketten zijn vereist.</span><span class="sxs-lookup"><span data-stu-id="8f744-312">In order toorun hello sample IPython Notebook or hello Python script file, hello following Python packages are needed.</span></span> <span data-ttu-id="8f744-313">Als u Hallo AzureML IPython Notebook service gebruikt, zijn deze pakketten vooraf geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="8f744-313">If you are using hello AzureML IPython Notebook service, these packages have been pre-installed.</span></span>

    - <span data-ttu-id="8f744-314">pandas</span><span class="sxs-lookup"><span data-stu-id="8f744-314">pandas</span></span>
    - <span data-ttu-id="8f744-315">numpy</span><span class="sxs-lookup"><span data-stu-id="8f744-315">numpy</span></span>
    - <span data-ttu-id="8f744-316">matplotlib</span><span class="sxs-lookup"><span data-stu-id="8f744-316">matplotlib</span></span>
    - <span data-ttu-id="8f744-317">pyodbc</span><span class="sxs-lookup"><span data-stu-id="8f744-317">pyodbc</span></span>
    - <span data-ttu-id="8f744-318">PyTables</span><span class="sxs-lookup"><span data-stu-id="8f744-318">PyTables</span></span>

<span data-ttu-id="8f744-319">Hallo aanbevolen volgorde wanneer geavanceerde analytische oplossingen bouwen op AzureML met grote hoeveelheden gegevens is Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="8f744-319">hello recommended sequence when building advanced analytical solutions on AzureML with large data is hello following:</span></span>

* <span data-ttu-id="8f744-320">Gelezen in een klein aantal Hallo gegevens in een kader gegevens in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="8f744-320">Read in a small sample of hello data into an in-memory data frame.</span></span>
* <span data-ttu-id="8f744-321">Uitvoeren van sommige visualisaties en explorations met Hallo steekproefgegevens.</span><span class="sxs-lookup"><span data-stu-id="8f744-321">Perform some visualizations and explorations using hello sampled data.</span></span>
* <span data-ttu-id="8f744-322">Experiment met functie-engineering Hallo met voorbeeldgegevens.</span><span class="sxs-lookup"><span data-stu-id="8f744-322">Experiment with feature engineering using hello sampled data.</span></span>
* <span data-ttu-id="8f744-323">Voor grotere gegevensverkenning gebruiken voor gegevensmanipulatie en functie-engineering, Python tooissue SQL-query's rechtstreeks met de Hallo SQL DW.</span><span class="sxs-lookup"><span data-stu-id="8f744-323">For larger data exploration, data manipulation and feature engineering, use Python tooissue SQL Queries directly against hello SQL DW.</span></span>
* <span data-ttu-id="8f744-324">Bepaal Hallo voorbeeld grootte toobe geschikt is voor het bouwen van Azure Machine Learning-model.</span><span class="sxs-lookup"><span data-stu-id="8f744-324">Decide hello sample size toobe suitable for Azure Machine Learning model building.</span></span>

<span data-ttu-id="8f744-325">de volgende Hallo zijn enkele gegevensverkenning, gegevensvisualisatie en engineering voorbeelden van functies.</span><span class="sxs-lookup"><span data-stu-id="8f744-325">hello followings are a few data exploration, data visualization, and feature engineering examples.</span></span> <span data-ttu-id="8f744-326">Meer gegevens explorations vindt u in het voorbeeld Hallo IPython Notebook en Python Hallo-script voorbeeldbestand.</span><span class="sxs-lookup"><span data-stu-id="8f744-326">More data explorations can be found in hello sample IPython Notebook and hello sample Python script file.</span></span>

### <a name="initialize-database-credentials"></a><span data-ttu-id="8f744-327">Databasereferenties initialiseren</span><span class="sxs-lookup"><span data-stu-id="8f744-327">Initialize database credentials</span></span>
<span data-ttu-id="8f744-328">De verbindingsinstellingen voor database in de volgende variabelen Hallo initialiseren:</span><span class="sxs-lookup"><span data-stu-id="8f744-328">Initialize your database connection settings in hello following variables:</span></span>

    SERVER_NAME=<server name>
    DATABASE_NAME=<database name>
    USERID=<user name>
    PASSWORD=<password>
    DB_DRIVER = <database driver>

### <a name="create-database-connection"></a><span data-ttu-id="8f744-329">Databaseverbinding maken</span><span class="sxs-lookup"><span data-stu-id="8f744-329">Create database connection</span></span>
<span data-ttu-id="8f744-330">Hier volgt Hallo verbindingsreeks die Hallo verbinding toohello database wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8f744-330">Here is hello connection string that creates hello connection toohello database.</span></span>

    CONNECTION_STRING = 'DRIVER={'+DRIVER+'};SERVER='+SERVER_NAME+';DATABASE='+DATABASE_NAME+';UID='+USERID+';PWD='+PASSWORD
    conn = pyodbc.connect(CONNECTION_STRING)

### <a name="report-number-of-rows-and-columns-in-table-nyctaxitrip"></a><span data-ttu-id="8f744-331">Rapport aantal rijen en kolommen in de tabel < nyctaxi_trip ></span><span class="sxs-lookup"><span data-stu-id="8f744-331">Report number of rows and columns in table <nyctaxi_trip></span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_trip>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_trip>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="8f744-332">Totale aantal rijen 173179759 =</span><span class="sxs-lookup"><span data-stu-id="8f744-332">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="8f744-333">Totale aantal kolommen = 14</span><span class="sxs-lookup"><span data-stu-id="8f744-333">Total number of columns = 14</span></span>

### <a name="report-number-of-rows-and-columns-in-table-nyctaxifare"></a><span data-ttu-id="8f744-334">Rapport aantal rijen en kolommen in de tabel < nyctaxi_fare ></span><span class="sxs-lookup"><span data-stu-id="8f744-334">Report number of rows and columns in table <nyctaxi_fare></span></span>
    nrows = pd.read_sql('''
        SELECT SUM(rows) FROM sys.partitions
        WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_fare>')
    ''', conn)

    print 'Total number of rows = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''
        SELECT COUNT(*) FROM information_schema.columns
        WHERE table_name = ('<nyctaxi_fare>') AND table_schema = ('<schemaname>')
    ''', conn)

    print 'Total number of columns = %d' % ncols.iloc[0,0]

* <span data-ttu-id="8f744-335">Totale aantal rijen 173179759 =</span><span class="sxs-lookup"><span data-stu-id="8f744-335">Total number of rows = 173179759</span></span>  
* <span data-ttu-id="8f744-336">Totale aantal kolommen = 11</span><span class="sxs-lookup"><span data-stu-id="8f744-336">Total number of columns = 11</span></span>

### <a name="read-in-a-small-data-sample-from-hello-sql-data-warehouse-database"></a><span data-ttu-id="8f744-337">Lees in een kleine hoeveelheden gegevens voorbeeld Hallo SQL Data Warehouse-Database</span><span class="sxs-lookup"><span data-stu-id="8f744-337">Read-in a small data sample from hello SQL Data Warehouse Database</span></span>
    t0 = time.time()

    query = '''
        SELECT TOP 10000 t.*, f.payment_type, f.fare_amount, f.surcharge, f.mta_tax,
            f.tolls_amount, f.total_amount, f.tip_amount
        FROM <schemaname>.<nyctaxi_trip> t, <schemaname>.<nyctaxi_fare> f
        WHERE datepart("mi",t.pickup_datetime) = 1
        AND   t.medallion = f.medallion
        AND   t.hack_license = f.hack_license
        AND   t.pickup_datetime = f.pickup_datetime
    '''

    df1 = pd.read_sql(query, conn)

    t1 = time.time()
    print 'Time tooread hello sample table is %f seconds' % (t1-t0)

    print 'Number of rows and columns retrieved = (%d, %d)' % (df1.shape[0], df1.shape[1])

<span data-ttu-id="8f744-338">Tijd tooread Hallo-voorbeeldtabel is 14.096495 seconden.</span><span class="sxs-lookup"><span data-stu-id="8f744-338">Time tooread hello sample table is 14.096495 seconds.</span></span>  
<span data-ttu-id="8f744-339">Aantal rijen en kolommen opgehaald = (1000, 21).</span><span class="sxs-lookup"><span data-stu-id="8f744-339">Number of rows and columns retrieved = (1000, 21).</span></span>

### <a name="descriptive-statistics"></a><span data-ttu-id="8f744-340">Beschrijvende statistiek</span><span class="sxs-lookup"><span data-stu-id="8f744-340">Descriptive statistics</span></span>
<span data-ttu-id="8f744-341">U bent nu klaar tooexplore Hallo door actieve gegevens.</span><span class="sxs-lookup"><span data-stu-id="8f744-341">Now you are ready tooexplore hello sampled data.</span></span> <span data-ttu-id="8f744-342">We beginnen met sommige beschrijvende statistieken voor Hallo kijken **reis\_afstand** (of andere velden die u kiest toospecify).</span><span class="sxs-lookup"><span data-stu-id="8f744-342">We start with looking at some descriptive statistics for hello **trip\_distance** (or any other fields you choose toospecify).</span></span>

    df1['trip_distance'].describe()

### <a name="visualization-box-plot-example"></a><span data-ttu-id="8f744-343">Visualisatie: Voorbeeld van grafiek</span><span class="sxs-lookup"><span data-stu-id="8f744-343">Visualization: Box plot example</span></span>
<span data-ttu-id="8f744-344">Vervolgens kijken we Hallo BoxPlot voor Hallo reis afstand toovisualize hello quantiles.</span><span class="sxs-lookup"><span data-stu-id="8f744-344">Next we look at hello box plot for hello trip distance toovisualize hello quantiles.</span></span>

    df1.boxplot(column='trip_distance',return_type='dict')

![Tekenen van #1][1]

### <a name="visualization-distribution-plot-example"></a><span data-ttu-id="8f744-346">Visualisatie: Distributie tekent voorbeeld</span><span class="sxs-lookup"><span data-stu-id="8f744-346">Visualization: Distribution plot example</span></span>
<span data-ttu-id="8f744-347">Waarnemingspunten die Hallo distributie en een histogram Hallo visualiseren actieve reis afstanden.</span><span class="sxs-lookup"><span data-stu-id="8f744-347">Plots that visualize hello distribution and a histogram for hello sampled trip distances.</span></span>

    fig = plt.figure()
    ax1 = fig.add_subplot(1,2,1)
    ax2 = fig.add_subplot(1,2,2)
    df1['trip_distance'].plot(ax=ax1,kind='kde', style='b-')
    df1['trip_distance'].hist(ax=ax2, bins=100, color='k')

![Tekenen van #2][2]

### <a name="visualization-bar-and-line-plots"></a><span data-ttu-id="8f744-349">Visualisatie: Staaf- en tekent de regel</span><span class="sxs-lookup"><span data-stu-id="8f744-349">Visualization: Bar and line plots</span></span>
<span data-ttu-id="8f744-350">In dit voorbeeld we Hallo reis afstand in vijf opslaglocaties bin en visualiseren Hallo binning resultaten.</span><span class="sxs-lookup"><span data-stu-id="8f744-350">In this example, we bin hello trip distance into five bins and visualize hello binning results.</span></span>

    trip_dist_bins = [0, 1, 2, 4, 10, 1000]
    df1['trip_distance']
    trip_dist_bin_id = pd.cut(df1['trip_distance'], trip_dist_bins)
    trip_dist_bin_id

<span data-ttu-id="8f744-351">We kunnen Hallo hierboven bin distributie in een balk wordt getekend of tekent met regel:</span><span class="sxs-lookup"><span data-stu-id="8f744-351">We can plot hello above bin distribution in a bar or line plot with:</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='bar')

![Tekenen van #3][3]

<span data-ttu-id="8f744-353">en</span><span class="sxs-lookup"><span data-stu-id="8f744-353">and</span></span>

    pd.Series(trip_dist_bin_id).value_counts().plot(kind='line')

![Tekenen van #4][4]

### <a name="visualization-scatterplot-examples"></a><span data-ttu-id="8f744-355">Visualisatie: Scatterplot voorbeelden</span><span class="sxs-lookup"><span data-stu-id="8f744-355">Visualization: Scatterplot examples</span></span>
<span data-ttu-id="8f744-356">Laten we zien spreidingsgrafiek tekent tussen **reis\_tijd\_in\_sec** en **reis\_afstand** toosee als er correlatie</span><span class="sxs-lookup"><span data-stu-id="8f744-356">We show scatter plot between **trip\_time\_in\_secs** and **trip\_distance** toosee if there is any correlation</span></span>

    plt.scatter(df1['trip_time_in_secs'], df1['trip_distance'])

![#6 tekenen][6]

<span data-ttu-id="8f744-358">We kunnen op dezelfde manier controleren of Hallo relatie tussen **snelheid\_code** en **reis\_afstand**.</span><span class="sxs-lookup"><span data-stu-id="8f744-358">Similarly we can check hello relationship between **rate\_code** and **trip\_distance**.</span></span>

    plt.scatter(df1['passenger_count'], df1['trip_distance'])

![#8 tekenen][8]

### <a name="data-exploration-on-sampled-data-using-sql-queries-in-ipython-notebook"></a><span data-ttu-id="8f744-360">Gegevensverkenning op steekproefgegevens met SQL-query's in IPython notebook</span><span class="sxs-lookup"><span data-stu-id="8f744-360">Data exploration on sampled data using SQL queries in IPython notebook</span></span>
<span data-ttu-id="8f744-361">In deze sectie besproken voor gegevens distributies met Hallo door actieve gegevens op die wordt bewaard in de nieuwe tabel Hallo die we eerder hebben gemaakt.</span><span class="sxs-lookup"><span data-stu-id="8f744-361">In this section, we explore data distributions using hello sampled data which is persisted in hello new table we created above.</span></span> <span data-ttu-id="8f744-362">Houd er rekening mee dat vergelijkbare explorations kunnen worden uitgevoerd met behulp van de oorspronkelijke tabellen Hallo.</span><span class="sxs-lookup"><span data-stu-id="8f744-362">Note that similar explorations can be performed using hello original tables.</span></span>

#### <a name="exploration-report-number-of-rows-and-columns-in-hello-sampled-table"></a><span data-ttu-id="8f744-363">Exploratie: Rapport aantal rijen en kolommen in Hallo actieve tabel</span><span class="sxs-lookup"><span data-stu-id="8f744-363">Exploration: Report number of rows and columns in hello sampled table</span></span>
    nrows = pd.read_sql('''SELECT SUM(rows) FROM sys.partitions WHERE object_id = OBJECT_ID('<schemaname>.<nyctaxi_sample>')''', conn)
    print 'Number of rows in sample = %d' % nrows.iloc[0,0]

    ncols = pd.read_sql('''SELECT count(*) FROM information_schema.columns WHERE table_name = ('<nyctaxi_sample>') AND table_schema = '<schemaname>'''', conn)
    print 'Number of columns in sample = %d' % ncols.iloc[0,0]

#### <a name="exploration-tippednot-tripped-distribution"></a><span data-ttu-id="8f744-364">Exploratie: Punt/niet omzeild distributie</span><span class="sxs-lookup"><span data-stu-id="8f744-364">Exploration: Tipped/not tripped Distribution</span></span>
    query = '''
        SELECT tipped, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tipped
        '''

    pd.read_sql(query, conn)

#### <a name="exploration-tip-class-distribution"></a><span data-ttu-id="8f744-365">Exploratie: Tip klasse distributie</span><span class="sxs-lookup"><span data-stu-id="8f744-365">Exploration: Tip class distribution</span></span>
    query = '''
        SELECT tip_class, count(*) AS tip_freq
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY tip_class
    '''

    tip_class_dist = pd.read_sql(query, conn)

#### <a name="exploration-plot-hello-tip-distribution-by-class"></a><span data-ttu-id="8f744-366">Exploratie: Hallo tip distributie door klasse tekenen</span><span class="sxs-lookup"><span data-stu-id="8f744-366">Exploration: Plot hello tip distribution by class</span></span>
    tip_class_dist['tip_freq'].plot(kind='bar')

![#26 tekenen][26]

#### <a name="exploration-daily-distribution-of-trips"></a><span data-ttu-id="8f744-368">Exploratie: Dagelijkse distributie van reizen</span><span class="sxs-lookup"><span data-stu-id="8f744-368">Exploration: Daily distribution of trips</span></span>
    query = '''
        SELECT CONVERT(date, dropoff_datetime) AS date, COUNT(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY CONVERT(date, dropoff_datetime)
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-per-medallion"></a><span data-ttu-id="8f744-369">Exploratie: Reis distributie per straten</span><span class="sxs-lookup"><span data-stu-id="8f744-369">Exploration: Trip distribution per medallion</span></span>
    query = '''
        SELECT medallion,count(*) AS c
        FROM <schemaname>.<nyctaxi_sample>
        GROUP BY medallion
    '''

    pd.read_sql(query,conn)

#### <a name="exploration-trip-distribution-by-medallion-and-hack-license"></a><span data-ttu-id="8f744-370">Exploratie: Reis distributie door straten en hack licentie</span><span class="sxs-lookup"><span data-stu-id="8f744-370">Exploration: Trip distribution by medallion and hack license</span></span>
    query = '''select medallion, hack_license,count(*) from <schemaname>.<nyctaxi_sample> group by medallion, hack_license'''
    pd.read_sql(query,conn)


#### <a name="exploration-trip-time-distribution"></a><span data-ttu-id="8f744-371">Exploratie: Verdeling reis</span><span class="sxs-lookup"><span data-stu-id="8f744-371">Exploration: Trip time distribution</span></span>
    query = '''select trip_time_in_secs, count(*) from <schemaname>.<nyctaxi_sample> group by trip_time_in_secs order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-trip-distance-distribution"></a><span data-ttu-id="8f744-372">Exploratie: Reis afstand distributie</span><span class="sxs-lookup"><span data-stu-id="8f744-372">Exploration: Trip distance distribution</span></span>
    query = '''select floor(trip_distance/5)*5 as tripbin, count(*) from <schemaname>.<nyctaxi_sample> group by floor(trip_distance/5)*5 order by count(*) desc'''
    pd.read_sql(query,conn)

#### <a name="exploration-payment-type-distribution"></a><span data-ttu-id="8f744-373">Exploratie: Betaling type distributiepunt</span><span class="sxs-lookup"><span data-stu-id="8f744-373">Exploration: Payment type distribution</span></span>
    query = '''select payment_type,count(*) from <schemaname>.<nyctaxi_sample> group by payment_type'''
    pd.read_sql(query,conn)

#### <a name="verify-hello-final-form-of-hello-featurized-table"></a><span data-ttu-id="8f744-374">Controleer of de uiteindelijke vorm Hallo van Hallo featurized tabel</span><span class="sxs-lookup"><span data-stu-id="8f744-374">Verify hello final form of hello featurized table</span></span>
    query = '''SELECT TOP 100 * FROM <schemaname>.<nyctaxi_sample>'''
    pd.read_sql(query,conn)

## <span data-ttu-id="8f744-375"><a name="mlmodel"></a>Bouwen van modellen in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="8f744-375"><a name="mlmodel"></a>Build models in Azure Machine Learning</span></span>
<span data-ttu-id="8f744-376">Er zijn nu gereed tooproceed toomodel bouwen en implementeren van modellen in [Azure Machine Learning](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="8f744-376">We are now ready tooproceed toomodel building and model deployment in [Azure Machine Learning](https://studio.azureml.net).</span></span> <span data-ttu-id="8f744-377">Hallo-gegevens is gereed toobe in Hallo voorspelling problemen geïdentificeerd eerder, namelijk gebruikt:</span><span class="sxs-lookup"><span data-stu-id="8f744-377">hello data is ready toobe used in any of hello prediction problems identified earlier, namely:</span></span>

1. <span data-ttu-id="8f744-378">**Binaire classificatie**: toopredict al dan niet een tip voor een zakenreis is betaald.</span><span class="sxs-lookup"><span data-stu-id="8f744-378">**Binary classification**: toopredict whether or not a tip was paid for a trip.</span></span>
2. <span data-ttu-id="8f744-379">**Multiklassen classificatie**: toopredict Hallo bereik van een tip betaald, toohello op basis van vooraf gedefinieerde klassen.</span><span class="sxs-lookup"><span data-stu-id="8f744-379">**Multiclass classification**: toopredict hello range of tip paid, according toohello previously defined classes.</span></span>
3. <span data-ttu-id="8f744-380">**Regressie taak**: toopredict Hallo hoeveelheid tip voor een reis betaald.</span><span class="sxs-lookup"><span data-stu-id="8f744-380">**Regression task**: toopredict hello amount of tip paid for a trip.</span></span>  

<span data-ttu-id="8f744-381">toobegin Hallo oefening modelleren, meld u bij tooyour **Azure Machine Learning** werkruimte.</span><span class="sxs-lookup"><span data-stu-id="8f744-381">toobegin hello modeling exercise, log in tooyour **Azure Machine Learning** workspace.</span></span> <span data-ttu-id="8f744-382">Als u nog geen een machine learning-werkruimte hebt gemaakt, raadpleegt u [maken van een Azure ML-werkruimte](machine-learning-create-workspace.md).</span><span class="sxs-lookup"><span data-stu-id="8f744-382">If you have not yet created a machine learning workspace, see [Create an Azure ML workspace](machine-learning-create-workspace.md).</span></span>

1. <span data-ttu-id="8f744-383">de slag met Azure Machine Learning tooget Zie [wat is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span><span class="sxs-lookup"><span data-stu-id="8f744-383">tooget started with Azure Machine Learning, see [What is Azure Machine Learning Studio?](machine-learning-what-is-ml-studio.md)</span></span>
2. <span data-ttu-id="8f744-384">Meld u bij te[Azure Machine Learning Studio](https://studio.azureml.net).</span><span class="sxs-lookup"><span data-stu-id="8f744-384">Log in too[Azure Machine Learning Studio](https://studio.azureml.net).</span></span>
3. <span data-ttu-id="8f744-385">Hallo-startpagina Studio biedt een schat aan informatie, video's, zelfstudies, koppelingen toohello Modules verwijzing en andere bronnen.</span><span class="sxs-lookup"><span data-stu-id="8f744-385">hello Studio Home page provides a wealth of information, videos, tutorials, links toohello Modules Reference, and other resources.</span></span> <span data-ttu-id="8f744-386">Raadpleeg voor meer informatie over Azure Machine Learning Hallo [Azure Machine Learning-documentatiecentrum](https://azure.microsoft.com/documentation/services/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="8f744-386">For more information about Azure Machine Learning, consult hello [Azure Machine Learning Documentation Center](https://azure.microsoft.com/documentation/services/machine-learning/).</span></span>

<span data-ttu-id="8f744-387">Een typische trainingsexperiment bestaat uit Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="8f744-387">A typical training experiment consists of hello following steps:</span></span>

1. <span data-ttu-id="8f744-388">Maak een **+ nieuw** experimenteren.</span><span class="sxs-lookup"><span data-stu-id="8f744-388">Create a **+NEW** experiment.</span></span>
2. <span data-ttu-id="8f744-389">Hallo-gegevens ophalen voor Azure ML.</span><span class="sxs-lookup"><span data-stu-id="8f744-389">Get hello data into Azure ML.</span></span>
3. <span data-ttu-id="8f744-390">Vooraf verwerken, transformeren en manipuleren van Hallo gegevens zo nodig.</span><span class="sxs-lookup"><span data-stu-id="8f744-390">Pre-process, transform and manipulate hello data as needed.</span></span>
4. <span data-ttu-id="8f744-391">Genereren onderdelen naar behoefte.</span><span class="sxs-lookup"><span data-stu-id="8f744-391">Generate features as needed.</span></span>
5. <span data-ttu-id="8f744-392">Hallo gegevens splitsen in training/testen/validatie gegevenssets (of afzonderlijke gegevenssets hebben voor elk).</span><span class="sxs-lookup"><span data-stu-id="8f744-392">Split hello data into training/validation/testing datasets(or have separate datasets for each).</span></span>
6. <span data-ttu-id="8f744-393">Selecteer een of meer machine learning-algoritmen, afhankelijk van Hallo probleem toosolve leren.</span><span class="sxs-lookup"><span data-stu-id="8f744-393">Select one or more machine learning algorithms depending on hello learning problem toosolve.</span></span> <span data-ttu-id="8f744-394">Bijvoorbeeld binaire classificatie, multiklassen classificatie, regressie.</span><span class="sxs-lookup"><span data-stu-id="8f744-394">E.g., binary classification, multiclass classification, regression.</span></span>
7. <span data-ttu-id="8f744-395">Een of meer modellen Hallo training gegevensset met trainen.</span><span class="sxs-lookup"><span data-stu-id="8f744-395">Train one or more models using hello training dataset.</span></span>
8. <span data-ttu-id="8f744-396">Hallo validatie gegevensset met Hallo getraind modellen beoordelen.</span><span class="sxs-lookup"><span data-stu-id="8f744-396">Score hello validation dataset using hello trained model(s).</span></span>
9. <span data-ttu-id="8f744-397">Hallo modellen toocompute Hallo relevante meetgegevens voor Hallo learning probleem evalueren.</span><span class="sxs-lookup"><span data-stu-id="8f744-397">Evaluate hello model(s) toocompute hello relevant metrics for hello learning problem.</span></span>
10. <span data-ttu-id="8f744-398">Afstellen Hallo modellen en selecteer Hallo best model toodeploy.</span><span class="sxs-lookup"><span data-stu-id="8f744-398">Fine tune hello model(s) and select hello best model toodeploy.</span></span>

<span data-ttu-id="8f744-399">In deze oefening hebben we al verkend en engineering Hallo-gegevens in SQL Data Warehouse en besloten op Hallo voorbeeld grootte tooingest in Azure ML.</span><span class="sxs-lookup"><span data-stu-id="8f744-399">In this exercise, we have already explored and engineered hello data in SQL Data Warehouse, and decided on hello sample size tooingest in Azure ML.</span></span> <span data-ttu-id="8f744-400">Ga als volgt Hallo procedure toobuild een of meer van de Hallo voorspellende modellen:</span><span class="sxs-lookup"><span data-stu-id="8f744-400">Here is hello procedure toobuild one or more of hello prediction models:</span></span>

1. <span data-ttu-id="8f744-401">Hallo-gegevens ophalen voor Azure ML Hallo met [importgegevens] [ import-data] module beschikbaar in Hallo **gegevensinvoer en uitvoer** sectie.</span><span class="sxs-lookup"><span data-stu-id="8f744-401">Get hello data into Azure ML using hello [Import Data][import-data] module, available in hello **Data Input and Output** section.</span></span> <span data-ttu-id="8f744-402">Zie voor meer informatie, Hallo [importgegevens] [ import-data] verwijzingspagina module.</span><span class="sxs-lookup"><span data-stu-id="8f744-402">For more information, see hello [Import Data][import-data] module reference page.</span></span>
   
    ![Gegevens importeren voor Azure ML][17]
2. <span data-ttu-id="8f744-404">Selecteer **Azure SQL Database** als Hallo **gegevensbron** in Hallo **eigenschappen** Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="8f744-404">Select **Azure SQL Database** as hello **Data source** in hello **Properties** panel.</span></span>
3. <span data-ttu-id="8f744-405">Voer Hallo database DNS-naam in Hallo **databaseservernaam** veld.</span><span class="sxs-lookup"><span data-stu-id="8f744-405">Enter hello database DNS name in hello **Database server name** field.</span></span> <span data-ttu-id="8f744-406">Indeling:`tcp:<your_virtual_machine_DNS_name>,1433`</span><span class="sxs-lookup"><span data-stu-id="8f744-406">Format: `tcp:<your_virtual_machine_DNS_name>,1433`</span></span>
4. <span data-ttu-id="8f744-407">Voer Hallo **databasenaam** in het bijbehorende veld Hallo.</span><span class="sxs-lookup"><span data-stu-id="8f744-407">Enter hello **Database name** in hello corresponding field.</span></span>
5. <span data-ttu-id="8f744-408">Voer Hallo *SQL-gebruikersnaam* in Hallo **Server gebruikersaccountnaam**, en Hallo *wachtwoord* in Hallo **Server het wachtwoord voor gebruikersaccount**.</span><span class="sxs-lookup"><span data-stu-id="8f744-408">Enter hello *SQL user name* in hello **Server user account name**, and hello *password* in hello **Server user account password**.</span></span>
6. <span data-ttu-id="8f744-409">Controleer de Hallo **accepteren servercertificaat** optie.</span><span class="sxs-lookup"><span data-stu-id="8f744-409">Check hello **Accept any server certificate** option.</span></span>
7. <span data-ttu-id="8f744-410">In Hallo **databasequery** bewerken van tekst, Hallo query welke uitgepakt Hallo nodig databasevelden (inclusief eventuele berekende velden zoals Hallo labels) en pijl-omlaag voorbeelden Hallo gegevens toohello gewenst samplegrootte plakken.</span><span class="sxs-lookup"><span data-stu-id="8f744-410">In hello **Database query** edit text area, paste hello query which extracts hello necessary database fields (including any computed fields such as hello labels) and down samples hello data toohello desired sample size.</span></span>

<span data-ttu-id="8f744-411">Een voorbeeld van een binaire indeling experiment lezen van gegevens rechtstreeks van Hallo SQL Data Warehouse-database is in onderstaande afbeelding ziet hello (onthouden tooreplace Hallo tabelnamen nyctaxi_trip en nyctaxi_fare door Hallo schema naam en het Hallo tabelnamen die u gebruikt in uw overzicht).</span><span class="sxs-lookup"><span data-stu-id="8f744-411">An example of a binary classification experiment reading data directly from hello SQL Data Warehouse database is in hello figure below (remember tooreplace hello table names nyctaxi_trip and nyctaxi_fare by hello schema name and hello table names you used in your walkthrough).</span></span> <span data-ttu-id="8f744-412">Vergelijkbare experimenten kunnen worden samengesteld voor multiklassen classificatie en regressie problemen.</span><span class="sxs-lookup"><span data-stu-id="8f744-412">Similar experiments can be constructed for multiclass classification and regression problems.</span></span>

![Azure ML Train][10]

> [!IMPORTANT]
> <span data-ttu-id="8f744-414">In Hallo modelleren ophalen van gegevens en wordt de query-voorbeelden die zijn opgegeven in de vorige secties **alle labels voor Hallo drie modellering oefeningen zijn opgenomen in de query Hallo**.</span><span class="sxs-lookup"><span data-stu-id="8f744-414">In hello modeling data extraction and sampling query examples provided in previous sections, **all labels for hello three modeling exercises are included in hello query**.</span></span> <span data-ttu-id="8f744-415">Een belangrijke (vereist) stap in elk Hallo modelleren oefeningen is te**uitsluiten** onnodige labels voor Hallo Hallo andere twee problemen en andere **doel lekken**.</span><span class="sxs-lookup"><span data-stu-id="8f744-415">An important (required) step in each of hello modeling exercises is too**exclude** hello unnecessary labels for hello other two problems, and any other **target leaks**.</span></span> <span data-ttu-id="8f744-416">Bijvoorbeeld: bij gebruik van binaire classificatie gebruiken Hallo label **punt** en Hallo velden uitsluiten **tip\_klasse**, **tip\_bedrag**, en **totale\_bedrag**.</span><span class="sxs-lookup"><span data-stu-id="8f744-416">For example, when using binary classification, use hello label **tipped** and exclude hello fields **tip\_class**, **tip\_amount**, and **total\_amount**.</span></span> <span data-ttu-id="8f744-417">Hallo laatste doel lekken omdat ze Hallo tip impliceren worden betaald.</span><span class="sxs-lookup"><span data-stu-id="8f744-417">hello latter are target leaks since they imply hello tip paid.</span></span>
> 
> <span data-ttu-id="8f744-418">tooexclude alle overbodige kolommen of doel lekken, mag u Hallo [Select Columns in Dataset] [ select-columns] module of Hallo [metagegevens bewerken] [ edit-metadata].</span><span class="sxs-lookup"><span data-stu-id="8f744-418">tooexclude any unnecessary columns or target leaks, you may use hello [Select Columns in Dataset][select-columns] module or hello [Edit Metadata][edit-metadata].</span></span> <span data-ttu-id="8f744-419">Zie voor meer informatie [Select Columns in Dataset] [ select-columns] en [metagegevens bewerken] [ edit-metadata] verwijzen naar pagina's.</span><span class="sxs-lookup"><span data-stu-id="8f744-419">For more information, see [Select Columns in Dataset][select-columns] and [Edit Metadata][edit-metadata] reference pages.</span></span>
> 
> 

## <span data-ttu-id="8f744-420"><a name="mldeploy"></a>Modellen in Azure Machine Learning implementeren</span><span class="sxs-lookup"><span data-stu-id="8f744-420"><a name="mldeploy"></a>Deploy models in Azure Machine Learning</span></span>
<span data-ttu-id="8f744-421">Wanneer uw model klaar is, kunt u het eenvoudig implementeren als een webservice rechtstreeks vanuit het Hallo-experiment.</span><span class="sxs-lookup"><span data-stu-id="8f744-421">When your model is ready, you can easily deploy it as a web service directly from hello experiment.</span></span> <span data-ttu-id="8f744-422">Zie voor meer informatie over het implementeren van Azure ML webservices [Azure Machine Learning-webservice implementeren](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="8f744-422">For more information about deploying Azure ML web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="8f744-423">een nieuwe webservice toodeploy, moet u:</span><span class="sxs-lookup"><span data-stu-id="8f744-423">toodeploy a new web service, you need to:</span></span>

1. <span data-ttu-id="8f744-424">Een score experiment maken.</span><span class="sxs-lookup"><span data-stu-id="8f744-424">Create a scoring experiment.</span></span>
2. <span data-ttu-id="8f744-425">Hallo-webservice implementeren.</span><span class="sxs-lookup"><span data-stu-id="8f744-425">Deploy hello web service.</span></span>

<span data-ttu-id="8f744-426">toocreate een score berekenen experimenteren van een **voltooid** training experiment, klikt u op **maken score berekenen EXPERIMENTEREN** in lagere actiebalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="8f744-426">toocreate a scoring experiment from a **Finished** training experiment, click **CREATE SCORING EXPERIMENT** in hello lower action bar.</span></span>

![Score berekenen voor Azure][18]

<span data-ttu-id="8f744-428">Azure Machine Learning probeert een score experiment op basis van onderdelen van Hallo trainingsexperiment Hallo toocreate.</span><span class="sxs-lookup"><span data-stu-id="8f744-428">Azure Machine Learning will attempt toocreate a scoring experiment based on hello components of hello training experiment.</span></span> <span data-ttu-id="8f744-429">In het bijzonder wordt:</span><span class="sxs-lookup"><span data-stu-id="8f744-429">In particular, it will:</span></span>

1. <span data-ttu-id="8f744-430">Hallo getraind model opslaan en Hallo model trainingsmodules verwijderen.</span><span class="sxs-lookup"><span data-stu-id="8f744-430">Save hello trained model and remove hello model training modules.</span></span>
2. <span data-ttu-id="8f744-431">Een logische identificeren **poort invoer** toorepresent Hallo invoergegevens schema verwacht.</span><span class="sxs-lookup"><span data-stu-id="8f744-431">Identify a logical **input port** toorepresent hello expected input data schema.</span></span>
3. <span data-ttu-id="8f744-432">Een logische identificeren **uitvoerpoort** toorepresent Hallo verwachte web service-uitvoerschema.</span><span class="sxs-lookup"><span data-stu-id="8f744-432">Identify a logical **output port** toorepresent hello expected web service output schema.</span></span>

<span data-ttu-id="8f744-433">Wanneer Hallo experiment score berekenen is gemaakt, controleren en maken indien nodig aanpassen.</span><span class="sxs-lookup"><span data-stu-id="8f744-433">When hello scoring experiment is created, review it and make adjust as needed.</span></span> <span data-ttu-id="8f744-434">Een typische aanpassing is tooreplace hello invoergegevensset en/of de query met een exclusief label velden, zoals deze is alleen beschikbaar wanneer het Hallo-service wordt genoemd.</span><span class="sxs-lookup"><span data-stu-id="8f744-434">A typical adjustment is tooreplace hello input dataset and/or query with one which excludes label fields, as these will not be available when hello service is called.</span></span> <span data-ttu-id="8f744-435">Het is ook dat een goede gewoonte tooreduce Hallo grootte van Hallo invoer gegevensset en/of queryparameters tooa enkele records, net voldoende tooindicate Hallo invoer schema.</span><span class="sxs-lookup"><span data-stu-id="8f744-435">It is also a good practice tooreduce hello size of hello input dataset and/or query tooa few records, just enough tooindicate hello input schema.</span></span> <span data-ttu-id="8f744-436">Voor de uitvoerpoort hello, het algemene tooexclude alle invoervelden en bevat alleen Hallo **Scored Labels** en **berekend kansen** in uitvoer met behulp van Hallo Hallo [kolommen in gegevensset selecteren ] [ select-columns] module.</span><span class="sxs-lookup"><span data-stu-id="8f744-436">For hello output port, it is common tooexclude all input fields and only include hello **Scored Labels** and **Scored Probabilities** in hello output using hello [Select Columns in Dataset][select-columns] module.</span></span>

<span data-ttu-id="8f744-437">Een voorbeeld van een experiment score berekenen is opgegeven in Hallo afbeelding hieronder.</span><span class="sxs-lookup"><span data-stu-id="8f744-437">A sample scoring experiment is provided in hello figure below.</span></span> <span data-ttu-id="8f744-438">Als u klaar bent toodeploy, klikt u op Hallo **WEBSERVICE PUBLICEERT** knop in lagere actiebalk Hallo.</span><span class="sxs-lookup"><span data-stu-id="8f744-438">When ready toodeploy, click hello **PUBLISH WEB SERVICE** button in hello lower action bar.</span></span>

![Azure ML publiceren][11]

## <a name="summary"></a><span data-ttu-id="8f744-440">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="8f744-440">Summary</span></span>
<span data-ttu-id="8f744-441">toorecap wat we in deze zelfstudie scenario hebben gedaan, hebt u een Azure data wetenschap-omgeving hebt gewerkt met een grote openbare gegevensset hebt gemaakt die deze begeleidt Hallo Team gegevens wetenschappelijke processen, alle Hallo manier van gegevens overname toomodel training en vervolgens toohello implementatie van een Azure Machine Learning-webservice.</span><span class="sxs-lookup"><span data-stu-id="8f744-441">toorecap what we have done in this walkthrough tutorial, you have created an Azure data science environment, worked with a large public dataset, taking it through hello Team Data Science Process, all hello way from data acquisition toomodel training, and then toohello deployment of an Azure Machine Learning web service.</span></span>

### <a name="license-information"></a><span data-ttu-id="8f744-442">Licentie-informatie</span><span class="sxs-lookup"><span data-stu-id="8f744-442">License information</span></span>
<span data-ttu-id="8f744-443">In dit voorbeeld scenario en de bijbehorende scripts en IPython notebook(s) worden gedeeld door Microsoft onder Hallo MIT-licentie.</span><span class="sxs-lookup"><span data-stu-id="8f744-443">This sample walkthrough and its accompanying scripts and IPython notebook(s) are shared by Microsoft under hello MIT license.</span></span> <span data-ttu-id="8f744-444">Controleer de Hallo LICENSE.txt bestand in de directory Hallo van Hallo voorbeeldcode op GitHub voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8f744-444">Please check hello LICENSE.txt file in in hello directory of hello sample code on GitHub for more details.</span></span>

## <a name="references"></a><span data-ttu-id="8f744-445">Verwijzingen</span><span class="sxs-lookup"><span data-stu-id="8f744-445">References</span></span>
<span data-ttu-id="8f744-446">• [Andrés Monroy NYC Taxi reizen downloadpagina](http://www.andresmh.com/nyctaxitrips/)</span><span class="sxs-lookup"><span data-stu-id="8f744-446">•    [Andrés Monroy NYC Taxi Trips Download Page](http://www.andresmh.com/nyctaxitrips/)</span></span>  
<span data-ttu-id="8f744-447">• [FOILing NYC Taxi reis gegevens door Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span><span class="sxs-lookup"><span data-stu-id="8f744-447">•    [FOILing NYC’s Taxi Trip Data by Chris Whong](http://chriswhong.com/open-data/foil_nyc_taxi/) </span></span>  
<span data-ttu-id="8f744-448">• [NYC Taxi en Limousine Commissie onderzoek en statistieken](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span><span class="sxs-lookup"><span data-stu-id="8f744-448">•    [NYC Taxi and Limousine Commission Research and Statistics](https://www1.nyc.gov/html/tlc/html/about/statistics.shtml)</span></span>

[1]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_26_1.png
[2]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_28_1.png
[3]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_35_1.png
[4]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_36_1.png
[5]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_39_1.png
[6]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_42_1.png
[7]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_44_1.png
[8]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_46_1.png
[9]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sql-walkthrough_71_1.png
[10]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremltrain.png
[11]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azuremlpublish.png
[12]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ssmsconnect.png
[13]: ./media/machine-learning-data-science-process-sqldw-walkthrough/executescript.png
[14]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqlserverproperties.png
[15]: ./media/machine-learning-data-science-process-sqldw-walkthrough/sqldefaultdirs.png
[16]: ./media/machine-learning-data-science-process-sqldw-walkthrough/bulkimport.png
[17]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlreader.png
[18]: ./media/machine-learning-data-science-process-sqldw-walkthrough/amlscoring.png
[19]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_download_scripts.png
[20]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ps_load_data.png
[21]: ./media/machine-learning-data-science-process-sqldw-walkthrough/azcopy-overwrite.png
[22]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-1.png
[23]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-2.png
[24]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-3.png
[25]: ./media/machine-learning-data-science-process-sqldw-walkthrough/ipnb-service-aml-4.png
[26]: ./media/machine-learning-data-science-process-sqldw-walkthrough/tip_class_hist_1.png


<!-- Module References -->
[edit-metadata]: https://msdn.microsoft.com/library/azure/370b6676-c11c-486f-bf73-35349f842a66/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[import-data]: https://msdn.microsoft.com/library/azure/4e1b0fe6-aded-4b3f-a36f-39b8862b9004/
