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
# <a name="analyze-flight-delay-data-by-using-hive-on-linux-based-hdinsight"></a>Vertraging vluchtgegevens analyseren met behulp van Hive in HDInsight op basis van Linux

Meer informatie over hoe tooanalyze vertraging vluchtgegevens met Hive in HDInsight op basis van Linux vervolgens exporteren Hallo gegevens tooAzure SQL-Database met behulp van Sqoop.

> [!IMPORTANT]
> Hallo stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

### <a name="prerequisites"></a>Vereisten

* **Een HDInsight-cluster**. Zie [aan de slag met Hadoop met Hive in HDInsight op Linux](hdinsight-hadoop-linux-tutorial-get-started.md) voor stapsgewijze instructies voor het maken van een nieuwe Linux gebaseerde HDInsight-cluster.

* **Azure SQL-database**. U kunt een Azure SQL database gebruiken als een doelgegevensopslagplaats. Als u een SQL-Database niet al hebt, raadpleegt u [SQL Database tutorial: Maak een SQL-database in minuten](../sql-database/sql-database-get-started.md).

* **Azure CLI**. Als u niet hello Azure CLI hebt geïnstalleerd, raadpleegt u [installeren en configureren van Azure CLI Hallo](../cli-install-nodejs.md) voor meer stappen.

## <a name="download-hello-flight-data"></a>Hallo vluchtgegevens downloaden

1. Te bladeren[onderzoek en beheer-innovatieve technologie, Bureau vervoer statistieken][rita-website].

2. Selecteer op Hallo pagina Hallo volgende waarden:

   | Naam | Waarde |
   | --- | --- |
   | Filteren van jaar |2013 |
   | Periode filteren |Januari |
   | Velden |Jaar FlightDate, UniqueCarrier, Carrier, FlightNum, OriginAirportID, oorsprong, OriginCityName, OriginState, DestAirportID, Dest, DestCityName, DestState, DepDelayMinutes, ArrDelay, ArrDelayMinutes, CarrierDelay, WeatherDelay, NASDelay, SecurityDelay, LateAircraftDelay. Alle andere velden wissen |

3. Klik op **Downloaden**.

## <a name="upload-hello-data"></a>Hallo gegevens uploaden

1. Hallo opdracht tooupload Hallo zip-bestand toohello HDInsight-cluster hoofdknooppunt volgende gebruiken:

    ```
    scp FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:
    ```

    Vervang **FILENAME** met de naam van zip-bestand Hallo Hallo. Vervang **gebruikersnaam** met Hallo SSH-aanmelding voor Hallo HDInsight-cluster. CLUSTERNAAM met de naam van de HDInsight-cluster Hallo Hallo vervangen.

   > [!NOTE]
   > Als u een wachtwoord tooauthenticate uw SSH-aanmelding gebruikt, wordt u gevraagd Hallo wachtwoord op te geven. Als u een openbare sleutel gebruikt, moet u mogelijk toouse hello `-i` parameter en Hallo pad toohello die overeenkomt met de persoonlijke sleutel opgeven. Bijvoorbeeld `scp -i ~/.ssh/id_rsa FILENAME.zip USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:`.

2. Zodra Hallo uploaden is voltooid, sluit u toohello-cluster via SSH:

    ```ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net```

    Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

3. Eenmaal zijn verbonden, gebruikt u Hallo toounzip Hallo ZIP-bestand te volgen:

    ```
    unzip FILENAME.zip
    ```

    Met deze opdracht wordt een CSV-bestand dat is ongeveer 60 MB.

4. Hallo Volg hiervoor opdracht toocreate een map op het HDInsight-opslag gebruiken en kopieer Hallo toohello map:

    ```
    hdfs dfs -mkdir -p /tutorials/flightdelays/data
    hdfs dfs -put FILENAME.csv /tutorials/flightdelays/data/
    ```

## <a name="create-and-run-hello-hiveql"></a>Maken en Hallo HiveQL uitvoeren

Gebruik Hallo volgende stappen tooimport gegevens uit Hallo CSV-bestand naar een Hive-tabel met de naam **vertragingen**.

1. Gebruik Hallo volgende opdracht toocreate en bewerken van een nieuw bestand met de naam **flightdelays.hql**:

    ```
    nano flightdelays.hql
    ```

    Gebruik Hallo tekst als Hallo inhoud van dit bestand te volgen:

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

2. Gebruik-bestand Hallo toosave **Ctrl + X**, klikt u vervolgens **Y** .

3. toostart Hive en Voer Hallo **flightdelays.hql** bestand, Hallo volgende opdracht gebruiken:

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -f flightdelays.hql
    ```

   > [!NOTE]
   > In dit voorbeeld `localhost` wordt gebruikt, aangezien u verbonden toohello hoofdknooppunt van de HDInsight-cluster hello, namelijk waarop HiveServer2 wordt uitgevoerd.

4. Eenmaal Hallo __flightdelays.hql__ script is voltooid met, gebruik Hallo volgende opdracht tooopen een interactieve Beeline sessie:

    ```
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http'
    ```

5. Wanneer u Hallo ontvangt `jdbc:hive2://localhost:10001/>` gevraagd, gebruikt u Hallo volgende query tooretrieve gegevens uit de vertraging vluchtgegevens Hallo geïmporteerd.

    ```hiveql
    INSERT OVERWRITE DIRECTORY '/tutorials/flightdelays/output'
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    SELECT regexp_replace(origin_city_name, '''', ''),
        avg(weather_delay)
    FROM delays
    WHERE weather_delay IS NOT NULL
    GROUP BY origin_city_name;
    ```

    Deze query haalt u een lijst met plaatsen ervaren weer vertragingen, samen met de Hallo gemiddelde tijd uit te stellen en te op te slaan`/tutorials/flightdelays/output`. Later, Sqoop Hallo gegevens leest vanaf deze locatie en exporteren tooAzure SQL-Database.

6. Voer tooexit Beeline, `!quit` Hallo een opdrachtprompt.

## <a name="create-a-sql-database"></a>Een SQL-database maken

Als u al een SQL-Database, moet u de naam van de server Hallo ophalen. U vindt Hallo-servernaam in Hallo [Azure-portal](https://portal.azure.com) door te selecteren **SQL-Databases**, en u vervolgens filteren op naam Hallo Hallo database toouse wenst. Hallo-servernaam wordt vermeld in Hallo **SERVER** kolom.

Als u nog geen een SQL-Database, gebruikt de informatie Hallo in [SQL Database tutorial: Maak een SQL-database in minuten](../sql-database/sql-database-get-started.md) toocreate een. De naam van Hallo is gebruikt voor het Hallo-database opgeslagen.

## <a name="create-a-sql-database-table"></a>Een SQL-databasetabel maken

> [!NOTE]
> Er zijn veel manieren tooconnect tooSQL Database en een tabel te maken. Hallo na gebruik van de stappen [FreeTDS](http://www.freetds.org/) van Hallo HDInsight-cluster.


1. SSH tooconnect toohello Linux gebaseerde HDInsight-cluster en Voer Hallo stappen uit te voeren van Hallo SSH-sessie gebruiken.

2. Hallo opdracht tooinstall FreeTDS volgende gebruiken:

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

3. Zodra Hallo-installatie is voltooid, gebruikt u Hallo opdracht tooconnect toohello SQL Database-server te volgen. Vervang **serverName** met Hallo SQL Database-servernaam. Vervang **adminLogin** en **adminPassword** met Hallo-aanmelding voor SQL-Database. Vervang **databaseName** met Hallo databasenaam.

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    U ontvangt uitvoer vergelijkbare toohello volgende tekst:

    ```
    locale is "en_US.UTF-8"
    locale charset is "UTF-8"
    using default charset "UTF-8"
    Default database being set toosqooptest
    1>
    ```

4. Op Hallo `1>` gevraagd, voert u Hallo volgende regels:

    ```
    CREATE TABLE [dbo].[delays](
    [origin_city_name] [nvarchar](50) NOT NULL,
    [weather_delay] float,
    CONSTRAINT [PK_delays] PRIMARY KEY CLUSTERED   
    ([origin_city_name] ASC))
    GO
    ```

    Wanneer Hallo `GO` instructie wordt ingevoerd, Hallo vorige instructies worden geëvalueerd. Deze query maakt een tabel met de naam **vertragingen**, met een geclusterde index.

    Gebruik Hallo na tooverify query die tabel Hallo is gemaakt:

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    Hallo uitvoer is vergelijkbaar toohello de volgende tekst:

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    databaseName       dbo     delays      BASE TABLE
    ```

5. Voer `exit` op Hallo `1>` vragen tooexit Hallo tsql-hulpprogramma.

## <a name="export-data-with-sqoop"></a>Gegevens exporteren met Sqoop

1. Gebruik Hallo opdracht tooverify Sqoop ziet uw SQL-Database te volgen:

    ```
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> --password <adminPassword>
    ```

    Deze opdracht retourneert een lijst met databases, met inbegrip van Hallo-database die u Hallo vertragingen tabel in eerder hebt gemaakt.

2. Gebruik Hallo volgende opdracht tooexport gegevens uit hivesampletable toohello mobiledata tabel:

    ```
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=<databaseName>' --username <adminLogin> --password <adminPassword> --table 'delays' --export-dir '/tutorials/flightdelays/output' --fields-terminated-by '\t' -m 1
    ```

    Sqoop toohello-database met Hallo vertragingen tabel verbindt en exporteert u gegevens van Hallo `/tutorials/flightdelays/output` mappentabel toohello vertragingen.

3. Nadat het Hallo-opdracht is voltooid, gebruikt u Hallo tooconnect toohello database met TSQL te volgen:

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D <databaseName>
    ```

    Eenmaal zijn verbonden, is gebruik Hallo na instructies tooverify die gegevens Hallo geëxporteerde toohello mobiledata tabel:

    ```
    SELECT * FROM delays
    GO
    ```

    U ziet een lijst met gegevens in de tabel Hallo. Type `exit` tooexit Hallo tsql-hulpprogramma.

## <a id="nextsteps"></a> Volgende stappen

toolearn meer manieren toowork met gegevens in HDInsight, Zie Hallo volgende documenten:

* [Hive gebruiken met HDInsight][hdinsight-use-hive]
* [Oozie gebruiken met HDInsight][hdinsight-use-oozie]
* [Sqoop gebruiken met HDInsight][hdinsight-use-sqoop]
* [Pig gebruiken met HDInsight][hdinsight-use-pig]
* [Het ontwikkelen van Java-MapReduce-programma's voor HDInsight][hdinsight-develop-mapreduce]
* [Python Hadoop-streaming van programma's voor HDInsight ontwikkelen][hdinsight-develop-streaming]

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
