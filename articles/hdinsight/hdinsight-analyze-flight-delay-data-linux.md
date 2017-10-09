---
title: aaaAnalyze vlucht vertraging gegevens met Hive in HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe toouse tooanalyze vluchtgegevens op Linux gebaseerde HDInsight Hive en exporteer Hallo gegevens tooSQL Sqoop-Database.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 0c23a079-981a-4079-b3f7-ad147b4609e5
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 7830457a7100880dff1c647dde1b4d203bfea3c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a><span data-ttu-id="4046a-103">Vertraging vluchtgegevens analyseren met behulp van Hive in HDInsight op basis van Linux</span><span class="sxs-lookup"><span data-stu-id="4046a-103">Analyze flight delay data by using Hive on Linux-based HDInsight</span></span>

<span data-ttu-id="4046a-104">Meer informatie over hoe tooanalyze vertraging vluchtgegevens met Hive in HDInsight op basis van Linux vervolgens exporteren Hallo gegevens tooAzure SQL-Database met behulp van Sqoop.</span><span class="sxs-lookup"><span data-stu-id="4046a-104">Learn how tooanalyze flight delay data using Hive on Linux-based HDInsight then export hello data tooAzure SQL Database using Sqoop.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4046a-105">Hallo stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux.</span><span class="sxs-lookup"><span data-stu-id="4046a-105">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="4046a-106">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="4046a-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4046a-107">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4046a-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

### <a name="prerequisites"></a><span data-ttu-id="4046a-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4046a-108">Prerequisites</span></span>

* <span data-ttu-id="4046a-109">**Een HDInsight-cluster**.</span><span class="sxs-lookup"><span data-stu-id="4046a-109">**An HDInsight cluster**.</span></span> <span data-ttu-id="4046a-110">Zie [aan de slag met Hadoop met Hive in HDInsight op Linux](hdinsight-hadoop-linux-tutorial-get-started.md) voor stapsgewijze instructies voor het maken van een nieuwe Linux gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="4046a-110">See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md) for steps on creating a new Linux-based HDInsight cluster.</span></span>

* <span data-ttu-id="4046a-111">**Azure SQL-database**.</span><span class="sxs-lookup"><span data-stu-id="4046a-111">**Azure SQL Database**.</span></span> <span data-ttu-id="4046a-112">U kunt een Azure SQL database gebruiken als een doelgegevensopslagplaats.</span><span class="sxs-lookup"><span data-stu-id="4046a-112">You use an Azure SQL database as a destination data store.</span></span> <span data-ttu-id="4046a-113">Als u een SQL-Database niet al hebt, raadpleegt u [SQL Database tutorial: Maak een SQL-database in minuten](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4046a-113">If you do not have a SQL Database already, see [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span>

* <span data-ttu-id="4046a-114">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="4046a-114">**Azure CLI**.</span></span> <span data-ttu-id="4046a-115">Als u niet hello Azure CLI hebt geïnstalleerd, raadpleegt u [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) voor meer stappen.</span><span class="sxs-lookup"><span data-stu-id="4046a-115">If you have not installed hello Azure CLI, see [Install and Configure hello Azure CLI](../cli-install-nodejs.md) for more steps.</span></span>

## <a name="download-hello-flight-data"></a><span data-ttu-id="4046a-116">Hallo vluchtgegevens downloaden</span><span class="sxs-lookup"><span data-stu-id="4046a-116">Download hello flight data</span></span>

1. <span data-ttu-id="4046a-117">Te bladeren[onderzoek en beheer-innovatieve technologie, Bureau vervoer statistieken][rita-website].</span><span class="sxs-lookup"><span data-stu-id="4046a-117">Browse too[Research and Innovative Technology Administration, Bureau of Transportation Statistics][rita-website].</span></span>

2. <span data-ttu-id="4046a-118">Selecteer op Hallo pagina Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="4046a-118">On hello page, select hello following values:</span></span>

   | <span data-ttu-id="4046a-119">Naam</span><span class="sxs-lookup"><span data-stu-id="4046a-119">Name</span></span> | <span data-ttu-id="4046a-120">Waarde</span><span class="sxs-lookup"><span data-stu-id="4046a-120">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="4046a-121">Filteren van jaar</span><span class="sxs-lookup"><span data-stu-id="4046a-121">Filter Year</span></span> |<span data-ttu-id="4046a-122">2013</span><span class="sxs-lookup"><span data-stu-id="4046a-122">2013</span></span> |
   | <span data-ttu-id="4046a-123">Periode filteren</span><span class="sxs-lookup"><span data-stu-id="4046a-123">Filter Period</span></span> |<span data-ttu-id="4046a-124">Januari</span><span class="sxs-lookup"><span data-stu-id="4046a-124">January</span></span> |
   | <span data-ttu-id="4046a-125">Velden</span><span class="sxs-lookup"><span data-stu-id="4046a-125">Fields</span></span> |<span data-ttu-id="4046a-126">Jaar FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, oorsprong, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span><span class="sxs-lookup"><span data-stu-id="4046a-126">Year, FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, Origin, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay.</span></span> <span data-ttu-id="4046a-127">Alle andere velden wissen</span><span class="sxs-lookup"><span data-stu-id="4046a-127">Clear all other fields</span></span> |

3. <span data-ttu-id="4046a-128">Klik op **Downloaden**.</span><span class="sxs-lookup"><span data-stu-id="4046a-128">Click **Download**.</span></span>

## <a name="upload-hello-data"></a><span data-ttu-id="4046a-129">Hallo gegevens uploaden</span><span class="sxs-lookup"><span data-stu-id="4046a-129">Upload hello data</span></span>

1. <span data-ttu-id="4046a-130">Hallo opdracht tooupload Hallo zip-bestand toohello HDInsight-cluster hoofdknooppunt volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="4046a-130">Use hello following command tooupload hello zip file toohello HDInsight cluster head node:</span></span>

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="4046a-131">Vervang **FILENAME** met de naam van zip-bestand Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="4046a-131">Replace **FILENAME** with hello name of hello zip file.</span></span> <span data-ttu-id="4046a-132">Vervang **gebruikersnaam** met Hallo SSH-aanmelding voor Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="4046a-132">Replace **USERNAME** with hello SSH login for hello HDInsight cluster.</span></span> <span data-ttu-id="4046a-133">CLUSTERNAAM met de naam van de HDInsight-cluster Hallo Hallo vervangen.</span><span class="sxs-lookup"><span data-stu-id="4046a-133">Replace CLUSTERNAME with hello name of hello HDInsight cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4046a-134">Als u een wachtwoord tooauthenticate uw SSH-aanmelding gebruikt, wordt u gevraagd Hallo wachtwoord op te geven.</span><span class="sxs-lookup"><span data-stu-id="4046a-134">If you use a password tooauthenticate your SSH login, you are prompted for hello password.</span></span> <span data-ttu-id="4046a-135">Als u een openbare sleutel gebruikt, moet u mogelijk toouse hello `-i` parameter en Hallo pad toohello die overeenkomt met de persoonlijke sleutel opgeven.</span><span class="sxs-lookup"><span data-stu-id="4046a-135">If you used a public key, you may need toouse hello `-i` parameter and specify hello path toohello matching private key.</span></span> <span data-ttu-id="4046a-136">Bijvoorbeeld `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="4046a-136">For example, `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="4046a-137">Zodra Hallo uploaden is voltooid, sluit u toohello-cluster via SSH:</span><span class="sxs-lookup"><span data-stu-id="4046a-137">Once hello upload has completed, connect toohello cluster using SSH:</span></span>

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    <span data-ttu-id="4046a-138">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4046a-138">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="4046a-139">Eenmaal zijn verbonden, gebruikt u Hallo toounzip Hallo ZIP-bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="4046a-139">Once connected, use hello following toounzip hello .zip file:</span></span>

    ```
    unzip FILENAME.zip
    ```

    <span data-ttu-id="4046a-140">Met deze opdracht wordt een CSV-bestand dat is ongeveer 60 MB.</span><span class="sxs-lookup"><span data-stu-id="4046a-140">This command extracts a .csv file that is roughly 60 MB.</span></span>

4. <span data-ttu-id="4046a-141">Hallo Volg hiervoor opdracht toocreate een map op het HDInsight-opslag gebruiken en kopieer Hallo toohello map:</span><span class="sxs-lookup"><span data-stu-id="4046a-141">Use hello following command toocreate a directory on HDInsight storage, and then copy hello file toohello directory:</span></span>

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-hello-hiveql"></a><span data-ttu-id="4046a-142">Maken en Hallo HiveQL uitvoeren</span><span class="sxs-lookup"><span data-stu-id="4046a-142">Create and run hello HiveQL</span></span>

<span data-ttu-id="4046a-143">Gebruik Hallo volgende stappen tooimport gegevens uit Hallo CSV-bestand naar een Hive-tabel met de naam **vertragingen**.</span><span class="sxs-lookup"><span data-stu-id="4046a-143">Use hello following steps tooimport data from hello CSV file into a Hive table named **Delays**.</span></span>

1. <span data-ttu-id="4046a-144">Gebruik Hallo volgende opdracht toocreate en bewerken van een nieuw bestand met de naam **flightdelays.hql**:</span><span class="sxs-lookup"><span data-stu-id="4046a-144">Use hello following command toocreate and edit a new file named **flightdelays.hql**:</span></span>

    ```
    nano flightdelays.hql
    ```

    <span data-ttu-id="4046a-145">Gebruik Hallo tekst als Hallo inhoud van dit bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="4046a-145">Use hello following text as hello contents of this file:</span></span>

    ```hiveql
    DROP TABLE delays_raw;
    -- Creates an external table over hello csv file
    CREATE EXTERNAL TABLE delays_raw (
        YEAR string,
        FL_DATE string,
        UNIQUE_CARRIER string,
        CARRIER string,
        FL_NUM string,
        ORIGIN_AIRPORT_ID string,
        ORIGIN string,
        ORIGIN_CITY_NAME string,
        ORIGIN_CITY_NAME_TEMP string,
        ORIGIN_STATE_ABR string,
        DEST_AIRPORT_ID string,
        DEST string,
        DEST_CITY_NAME string,
        DEST_CITY_NAME_TEMP string,
        DEST_STATE_ABR string,
        DEP_DELAY_NEW float,
        ARR_DELAY_NEW float,
        CARRIER_DELAY float,
        WEATHER_DELAY float,
        NAS_DELAY float,
        SECURITY_DELAY float,
        LATE_AIRCRAFT_DELAY float)
    -- hello following lines describe hello format and location of hello file
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ','
    LINES TERMINATED BY '\n'
    STORED AS TEXTFILE
    LOCATION '/tutorials/flightdelays/data';

    -- Drop hello delays table if it exists
    DROP TABLE delays;
    -- Create hello delays table and populate it with data
    -- pulled in from hello CSV file (via hello external table defined previously)
    CREATE TABLE delays AS
    SELECT YEAR AS year,
        FL_DATE AS flight_date,
        substring(UNIQUE_CARRIER, 2, length(UNIQUE_CARRIER) -1) AS unique_carrier,
        substring(CARRIER, 2, length(CARRIER) -1) AS carrier,
        substring(FL_NUM, 2, length(FL_NUM) -1) AS flight_num,
        ORIGIN_AIRPORT_ID AS origin_airport_id,
        substring(ORIGIN, 2, length(ORIGIN) -1) AS origin_airport_code,
        substring(ORIGIN_CITY_NAME, 2) AS origin_city_name,
        substring(ORIGIN_STATE_ABR, 2, length(ORIGIN_STATE_ABR) -1)  AS origin_state_abr,
        DEST_AIRPORT_ID AS dest_airport_id,
        substring(DEST, 2, length(DEST) -1) AS dest_airport_code,
        substring(DEST_CITY_NAME,2) AS dest_city_name,
        substring(DEST_STATE_ABR, 2, length(DEST_STATE_ABR) -1) AS dest_state_abr,
        DEP_DELAY_NEW AS dep_delay_new,
        ARR_DELAY_NEW AS arr_delay_new,
        CARRIER_DELAY AS carrier_delay,
        WEATHER_DELAY AS weather_delay,
        NAS_DELAY AS nas_delay,
        SECURITY_DELAY AS security_delay,
        LATE_AIRCRAFT_DELAY AS late_aircraft_delay
    FROM delays_raw;
    ```

2. <span data-ttu-id="4046a-146">Gebruik-bestand Hallo toosave **Ctrl + X**, klikt u vervolgens **Y** .</span><span class="sxs-lookup"><span data-stu-id="4046a-146">toosave hello file, use **Ctrl + X**, then **Y** .</span></span>

3. <span data-ttu-id="4046a-147">toostart Hive en Voer Hallo **flightdelays.hql** bestand, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="4046a-147">toostart Hive and run hello **flightdelays.hql** file, use hello following command:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > <span data-ttu-id="4046a-148">In dit voorbeeld `localhost` wordt gebruikt, aangezien u verbonden toohello hoofdknooppunt van de HDInsight-cluster hello, namelijk waarop HiveServer2 wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4046a-148">In this example, `localhost` is used since you are connected toohello head node of hello HDInsight cluster, which is where HiveServer2 is running.</span></span>

4. <span data-ttu-id="4046a-149">Eenmaal Hallo __flightdelays.hql__ script is voltooid met, gebruik Hallo volgende opdracht tooopen een interactieve Beeline sessie:</span><span class="sxs-lookup"><span data-stu-id="4046a-149">Once hello __flightdelays.hql__ script finishes running, use hello following command tooopen an interactive Beeline session:</span></span>

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. <span data-ttu-id="4046a-150">Wanneer u Hallo ontvangt `jdbc:hive2://localhost:10001/>` gevraagd, gebruikt u Hallo volgende query tooretrieve gegevens uit de vertraging vluchtgegevens Hallo geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="4046a-150">When you receive hello `jdbc:hive2://localhost:10001/>` prompt, use hello following query tooretrieve data from hello imported flight delay data.</span></span>

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    <span data-ttu-id="4046a-151">Deze query haalt u een lijst met plaatsen ervaren weer vertragingen, samen met de Hallo gemiddelde tijd uit te stellen en te op te slaan`/tutorials/flightdelays/output`.</span><span class="sxs-lookup"><span data-stu-id="4046a-151">This query retrieves a list of cities that experienced weather delays, along with hello average delay time, and save it too`/tutorials/flightdelays/output`.</span></span> <span data-ttu-id="4046a-152">Later, Sqoop Hallo gegevens leest vanaf deze locatie en exporteren tooAzure SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="4046a-152">Later, Sqoop reads hello data from this location and export it tooAzure SQL Database.</span></span>

6. <span data-ttu-id="4046a-153">Voer tooexit Beeline, `!quit` Hallo een opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="4046a-153">tooexit Beeline, enter `!quit` at hello prompt.</span></span>

## <a name="create-a-sql-database"></a><span data-ttu-id="4046a-154">Een SQL-database maken</span><span class="sxs-lookup"><span data-stu-id="4046a-154">Create a SQL Database</span></span>

<span data-ttu-id="4046a-155">Als u al een SQL-Database, moet u de naam van de server Hallo ophalen.</span><span class="sxs-lookup"><span data-stu-id="4046a-155">If you already have a SQL Database, you must get hello server name.</span></span> <span data-ttu-id="4046a-156">U vindt Hallo-servernaam in Hallo [Azure-portal](https://portal.azure.com) door te selecteren **SQL-Databases**, en u vervolgens filteren op naam Hallo Hallo database toouse wenst.</span><span class="sxs-lookup"><span data-stu-id="4046a-156">You can find hello server name in hello [Azure portal](https://portal.azure.com) by selecting **SQL Databases**, and then filtering on hello name of hello database you wish toouse.</span></span> <span data-ttu-id="4046a-157">Hallo-servernaam wordt vermeld in Hallo **SERVER** kolom.</span><span class="sxs-lookup"><span data-stu-id="4046a-157">hello server name is listed in hello **SERVER** column.</span></span>

<span data-ttu-id="4046a-158">Als u nog geen een SQL-Database, gebruikt de informatie Hallo in [SQL Database tutorial: Maak een SQL-database in minuten](../sql-database/sql-database-get-started.md) toocreate een.</span><span class="sxs-lookup"><span data-stu-id="4046a-158">If you do not already have a SQL Database, use hello information in [SQL Database tutorial: Create a SQL database in minutes](../sql-database/sql-database-get-started.md) toocreate one.</span></span> <span data-ttu-id="4046a-159">De naam van Hallo is gebruikt voor het Hallo-database opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="4046a-159">Save hello server name used for hello database.</span></span>

## <a name="create-a-sql-database-table"></a><span data-ttu-id="4046a-160">Een SQL-databasetabel maken</span><span class="sxs-lookup"><span data-stu-id="4046a-160">Create a SQL Database table</span></span>

> [!NOTE]
> <span data-ttu-id="4046a-161">Er zijn veel manieren tooconnect tooSQL Database en een tabel te maken.</span><span class="sxs-lookup"><span data-stu-id="4046a-161">There are many ways tooconnect tooSQL Database and create a table.</span></span> <span data-ttu-id="4046a-162">Hallo na gebruik van de stappen [FreeTDS](http://www.freetds.org/) van Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="4046a-162">hello following steps use [FreeTDS](http://www.freetds.org/) from hello HDInsight cluster.</span></span>


1. <span data-ttu-id="4046a-163">SSH tooconnect toohello Linux gebaseerde HDInsight-cluster en Voer Hallo stappen uit te voeren van Hallo SSH-sessie gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4046a-163">Use SSH tooconnect toohello Linux-based HDInsight cluster, and run hello following steps from hello SSH session.</span></span>

2. <span data-ttu-id="4046a-164">Hallo opdracht tooinstall FreeTDS volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="4046a-164">Use hello following command tooinstall FreeTDS:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. <span data-ttu-id="4046a-165">Zodra Hallo-installatie is voltooid, gebruikt u Hallo opdracht tooconnect toohello SQL Database-server te volgen.</span><span class="sxs-lookup"><span data-stu-id="4046a-165">Once hello install completes, use hello following command tooconnect toohello SQL Database server.</span></span> <span data-ttu-id="4046a-166">Vervang **serverName** met Hallo SQL Database-servernaam.</span><span class="sxs-lookup"><span data-stu-id="4046a-166">Replace **serverName** with hello SQL Database server name.</span></span> <span data-ttu-id="4046a-167">Vervang **adminLogin** en **adminPassword** met Hallo-aanmelding voor SQL-Database.</span><span class="sxs-lookup"><span data-stu-id="4046a-167">Replace **adminLogin** and **adminPassword** with hello login for SQL Database.</span></span> <span data-ttu-id="4046a-168">Vervang **databaseName** met Hallo databasenaam.</span><span class="sxs-lookup"><span data-stu-id="4046a-168">Replace **databaseName** with hello database name.</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="4046a-169">U ontvangt uitvoer vergelijkbare toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="4046a-169">You receive output similar toohello following text:</span></span>

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set toosqooptest
    1>
    ```

4. <span data-ttu-id="4046a-170">Op Hallo `1>` gevraagd, voert u Hallo volgende regels:</span><span class="sxs-lookup"><span data-stu-id="4046a-170">At hello `1>` prompt, enter hello following lines:</span></span>

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    <span data-ttu-id="4046a-171">Wanneer Hallo `GO` instructie wordt ingevoerd, Hallo vorige instructies worden geëvalueerd.</span><span class="sxs-lookup"><span data-stu-id="4046a-171">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="4046a-172">Deze query maakt een tabel met de naam **vertragingen**, met een geclusterde index.</span><span class="sxs-lookup"><span data-stu-id="4046a-172">This query creates a table named **delays**, with a clustered index.</span></span>

    <span data-ttu-id="4046a-173">Gebruik Hallo na tooverify query die tabel Hallo is gemaakt:</span><span class="sxs-lookup"><span data-stu-id="4046a-173">Use hello following query tooverify that hello table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="4046a-174">Hallo uitvoer is vergelijkbaar toohello de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="4046a-174">hello output is similar toohello following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. <span data-ttu-id="4046a-175">Voer `exit` op Hallo `1>` vragen tooexit Hallo tsql-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="4046a-175">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="export-data-with-sqoop"></a><span data-ttu-id="4046a-176">Gegevens exporteren met Sqoop</span><span class="sxs-lookup"><span data-stu-id="4046a-176">Export data with Sqoop</span></span>

1. <span data-ttu-id="4046a-177">Gebruik Hallo opdracht tooverify Sqoop ziet uw SQL-Database te volgen:</span><span class="sxs-lookup"><span data-stu-id="4046a-177">Use hello following command tooverify that Sqoop can see your SQL Database:</span></span>

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    <span data-ttu-id="4046a-178">Deze opdracht retourneert een lijst met databases, met inbegrip van Hallo-database die u Hallo vertragingen tabel in eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4046a-178">This command returns a list of databases, including hello database that you created hello delays table in earlier.</span></span>

2. <span data-ttu-id="4046a-179">Gebruik Hallo volgende opdracht tooexport gegevens uit hivesampletable toohello mobiledata tabel:</span><span class="sxs-lookup"><span data-stu-id="4046a-179">Use hello following command tooexport data from hivesampletable toohello mobiledata table:</span></span>

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="4046a-180">Sqoop toohello-database met Hallo vertragingen tabel verbindt en exporteert u gegevens van Hallo `/tutorials/flightdelays/output` mappentabel toohello vertragingen.</span><span class="sxs-lookup"><span data-stu-id="4046a-180">Sqoop connects toohello database containing hello delays table, and exports data from hello `/tutorials/flightdelays/output` directory toohello delays table.</span></span>

3. <span data-ttu-id="4046a-181">Nadat het Hallo-opdracht is voltooid, gebruikt u Hallo tooconnect toohello database met TSQL te volgen:</span><span class="sxs-lookup"><span data-stu-id="4046a-181">After hello command completes, use hello following tooconnect toohello database using TSQL:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    <span data-ttu-id="4046a-182">Eenmaal zijn verbonden, is gebruik Hallo na instructies tooverify die gegevens Hallo geëxporteerde toohello mobiledata tabel:</span><span class="sxs-lookup"><span data-stu-id="4046a-182">Once connected, use hello following statements tooverify that hello data was exported toohello mobiledata table:</span></span>

    ```
    SELECT * FROM delays
    GO
    ```

    <span data-ttu-id="4046a-183">U ziet een lijst met gegevens in de tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="4046a-183">You should see a listing of data in hello table.</span></span> <span data-ttu-id="4046a-184">Type `exit` tooexit Hallo tsql-hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="4046a-184">Type `exit` tooexit hello tsql utility.</span></span>

## <span data-ttu-id="4046a-185"><a id="nextsteps"></a> Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4046a-185"><a id="nextsteps"></a> Next steps</span></span>

<span data-ttu-id="4046a-186">toolearn meer manieren toowork met gegevens in HDInsight, Zie Hallo volgende documenten:</span><span class="sxs-lookup"><span data-stu-id="4046a-186">toolearn more ways toowork with data in HDInsight, see hello following documents:</span></span>

* <span data-ttu-id="4046a-187">[Hive gebruiken met HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="4046a-187">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="4046a-188">[Oozie gebruiken met HDInsight][hdinsight-use-oozie]</span><span class="sxs-lookup"><span data-stu-id="4046a-188">[Use Oozie with HDInsight][hdinsight-use-oozie]</span></span>
* <span data-ttu-id="4046a-189">[Sqoop gebruiken met HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="4046a-189">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="4046a-190">[Pig gebruiken met HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="4046a-190">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="4046a-191">[Het ontwikkelen van Java-MapReduce-programma's voor HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="4046a-191">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>
* <span data-ttu-id="4046a-192">[Python Hadoop-streaming van programma's voor HDInsight ontwikkelen][hdinsight-develop-streaming]</span><span class="sxs-lookup"><span data-stu-id="4046a-192">[Develop Python Hadoop streaming programs for HDInsight][hdinsight-develop-streaming]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/


[rita-website]: http://www.transtats.bts.gov/DL_SelectFields.asp?Table_ID=236&DB_Short_Name=On-Time
[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[hdinsight-use-oozie]: hdinsight-use-oozie-linux-mac.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-develop-streaming]: hdinsight-hadoop-streaming-python.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[hadoop-hiveql]: https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
