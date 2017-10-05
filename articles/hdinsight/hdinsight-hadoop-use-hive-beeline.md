---
title: Gebruik Beeline met Apache Hive - Azure HDInsight | Microsoft Docs
description: Informatie over het gebruik van de client Beeline Hive-query's uitvoeren met Hadoop op HDInsight. Beeline is een hulpprogramma voor het werken met HiveServer2 via JDBC vast.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: beeline hive, hive beeline
ms.assetid: 3adfb1ba-8924-4a13-98db-10a67ab24fca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 153044aafa3a67ee85bb1997beb821777c938563
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-beeline-client-with-apache-hive"></a><span data-ttu-id="9f5d2-105">De client Beeline gebruiken met Apache Hive</span><span class="sxs-lookup"><span data-stu-id="9f5d2-105">Use the Beeline client with Apache Hive</span></span>

<span data-ttu-id="9f5d2-106">Informatie over het gebruik [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) Hive-query's uitvoeren op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-106">Learn how to use [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) to run Hive queries on HDInsight.</span></span>

<span data-ttu-id="9f5d2-107">Beeline is een Hive-client die is opgenomen op de hoofdknooppunten van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-107">Beeline is a Hive client that is included on the head nodes of your HDInsight cluster.</span></span> <span data-ttu-id="9f5d2-108">Beeline maakt JDBC verbinding met HiveServer2, een service die wordt gehost op uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-108">Beeline uses JDBC to connect to HiveServer2, a service hosted on your HDInsight cluster.</span></span> <span data-ttu-id="9f5d2-109">U kunt ook Beeline gebruiken voor toegang tot de Hive in HDInsight op afstand via internet.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-109">You can also use Beeline to access Hive on HDInsight remotely over the internet.</span></span> <span data-ttu-id="9f5d2-110">De volgende tabel bevat de verbindingsreeksen voor gebruik met Beeline:</span><span class="sxs-lookup"><span data-stu-id="9f5d2-110">The following table provides connection strings for use with Beeline:</span></span>

| <span data-ttu-id="9f5d2-111">Waar u Beeline van uitvoert</span><span class="sxs-lookup"><span data-stu-id="9f5d2-111">Where you run Beeline from</span></span> | <span data-ttu-id="9f5d2-112">Parameters</span><span class="sxs-lookup"><span data-stu-id="9f5d2-112">Parameters</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9f5d2-113">Een SSH-verbinding naar een headnode of edge-knooppunt</span><span class="sxs-lookup"><span data-stu-id="9f5d2-113">An SSH connection to a headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| <span data-ttu-id="9f5d2-114">Buiten het cluster</span><span class="sxs-lookup"><span data-stu-id="9f5d2-114">Outside the cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> <span data-ttu-id="9f5d2-115">Vervang `admin` met de cluster-aanmeldingsaccount voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-115">Replace `admin` with the cluster login account for your cluster.</span></span>
>
> <span data-ttu-id="9f5d2-116">Vervang `password` met het wachtwoord voor de aanmeldingsaccount van het cluster.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-116">Replace `password` with the password for the cluster login account.</span></span>
>
> <span data-ttu-id="9f5d2-117">Vervang `clustername` door de naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-117">Replace `clustername` with the name of your HDInsight cluster.</span></span>

## <span data-ttu-id="9f5d2-118"><a id="prereq"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="9f5d2-118"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="9f5d2-119">Een op Linux gebaseerde Hadoop op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-119">A Linux-based Hadoop on HDInsight cluster.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="9f5d2-120">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-120">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9f5d2-121">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="9f5d2-122">Een SSH-client of een lokale Beeline-client.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-122">An SSH client or a local Beeline client.</span></span> <span data-ttu-id="9f5d2-123">De meeste van de stappen in dit document wordt ervan uitgegaan dat u van Beeline van een SSH-sessie met het cluster gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-123">Most of the steps in this document assume that you are using Beeline from an SSH session to the cluster.</span></span> <span data-ttu-id="9f5d2-124">Zie voor meer informatie over het uitvoeren van Beeline van buiten het cluster de [Beeline op afstand gebruiken](#remote) sectie.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-124">For information on running Beeline from outside the cluster, see the [use Beeline remotely](#remote) section.</span></span>

    <span data-ttu-id="9f5d2-125">Zie voor meer informatie over het gebruik van SSH [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9f5d2-125">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="9f5d2-126"><a id="beeline"></a>Gebruik Beeline</span><span class="sxs-lookup"><span data-stu-id="9f5d2-126"><a id="beeline"></a>Use Beeline</span></span>

1. <span data-ttu-id="9f5d2-127">Bij het starten van Beeline, moet u een verbindingsreeks opgeven voor HiveServer2 op uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-127">When starting Beeline, you must provide a connection string for HiveServer2 on your HDInsight cluster.</span></span> <span data-ttu-id="9f5d2-128">Voor het uitvoeren van de opdracht van buiten het cluster, moet u ook de naam van het cluster aanmelding account opgeven (standaard `admin`) en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-128">To run the command from outside the cluster, you must also provide the cluster login account name (default `admin`) and password.</span></span> <span data-ttu-id="9f5d2-129">Gebruik de volgende tabel om te zoeken de indeling voor een verbindingsreeks en parameters moet worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="9f5d2-129">Use the following table to find the connection string format and parameters to use:</span></span>

    | <span data-ttu-id="9f5d2-130">Waar u Beeline van uitvoert</span><span class="sxs-lookup"><span data-stu-id="9f5d2-130">Where you run Beeline from</span></span> | <span data-ttu-id="9f5d2-131">Parameters</span><span class="sxs-lookup"><span data-stu-id="9f5d2-131">Parameters</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="9f5d2-132">Een SSH-verbinding naar een headnode of edge-knooppunt</span><span class="sxs-lookup"><span data-stu-id="9f5d2-132">An SSH connection to a headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | <span data-ttu-id="9f5d2-133">Buiten het cluster</span><span class="sxs-lookup"><span data-stu-id="9f5d2-133">Outside the cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    <span data-ttu-id="9f5d2-134">De volgende opdracht kan bijvoorbeeld worden gebruikt voor Beeline van een SSH-sessie starten met het cluster:</span><span class="sxs-lookup"><span data-stu-id="9f5d2-134">For example, the following command can be used to start Beeline from an SSH session to the cluster:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    <span data-ttu-id="9f5d2-135">Deze opdracht wordt de client Beeline gestart en verbinding maakt met HiveServer2 op het hoofdknooppunt van het cluster.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-135">This command starts the Beeline client, and connects to HiveServer2 on the cluster head node.</span></span> <span data-ttu-id="9f5d2-136">Zodra de opdracht is voltooid, wordt u aankomt bij een `jdbc:hive2://headnodehost:10001/>` prompt.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-136">Once the command completes, you arrive at a `jdbc:hive2://headnodehost:10001/>` prompt.</span></span>

2. <span data-ttu-id="9f5d2-137">Beeline opdrachten beginnen met een `!` teken, bijvoorbeeld `!help` geeft help weer.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-137">Beeline commands begin with a `!` character, for example `!help` displays help.</span></span> <span data-ttu-id="9f5d2-138">Maar het `!` voor bepaalde opdrachten kunnen worden weggelaten.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-138">However the `!` can be omitted for some commands.</span></span> <span data-ttu-id="9f5d2-139">Bijvoorbeeld: `help` werkt ook.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-139">For example, `help` also works.</span></span>

    <span data-ttu-id="9f5d2-140">Er is een `!sql`, dat wordt gebruikt voor het uitvoeren van HiveQL-instructies.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-140">There is a `!sql`, which is used to execute HiveQL statements.</span></span> <span data-ttu-id="9f5d2-141">HiveQL wordt echter zo vaak gebruikt dat kunt u de voorgaande weglaten `!sql`.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-141">However, HiveQL is so commonly used that you can omit the preceding `!sql`.</span></span> <span data-ttu-id="9f5d2-142">De volgende twee instructies zijn gelijkwaardig:</span><span class="sxs-lookup"><span data-stu-id="9f5d2-142">The following two statements are equivalent:</span></span>

    ```hiveql
    !sql show tables;
    show tables;
    ```

    <span data-ttu-id="9f5d2-143">Op een nieuw cluster slechts één tabel wordt vermeld: **hivesampletable**.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-143">On a new cluster, only one table is listed: **hivesampletable**.</span></span>

3. <span data-ttu-id="9f5d2-144">Gebruik de volgende opdracht om het schema voor de hivesampletable weer te geven:</span><span class="sxs-lookup"><span data-stu-id="9f5d2-144">Use the following command to display the schema for the hivesampletable:</span></span>

    ```hiveql
    describe hivesampletable;
    ```

    <span data-ttu-id="9f5d2-145">Deze opdracht retourneert de volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="9f5d2-145">This command returns the following information:</span></span>

        +-----------------------+------------+----------+--+
        |       col_name        | data_type  | comment  |
        +-----------------------+------------+----------+--+
        | clientid              | string     |          |
        | querytime             | string     |          |
        | market                | string     |          |
        | deviceplatform        | string     |          |
        | devicemake            | string     |          |
        | devicemodel           | string     |          |
        | state                 | string     |          |
        | country               | string     |          |
        | querydwelltime        | double     |          |
        | sessionid             | bigint     |          |
        | sessionpagevieworder  | bigint     |          |
        +-----------------------+------------+----------+--+

    <span data-ttu-id="9f5d2-146">Deze informatie beschrijft de kolommen in de tabel.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-146">This information describes the columns in the table.</span></span> <span data-ttu-id="9f5d2-147">Terwijl sommige query's op deze gegevens kan worden uitgevoerd, gaan we in plaats daarvan een nieuwe tabel maken om te laten zien hoe u gegevens laadt in Hive en een schema hebt toegepast.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-147">While we could perform some queries against this data, let's instead create a brand new table to demonstrate how to load data into Hive and apply a schema.</span></span>

4. <span data-ttu-id="9f5d2-148">Voer de volgende instructies voor het maken van een tabel met de naam **log4jLogs** met behulp van voorbeeldgegevens voorzien van het HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="9f5d2-148">Enter the following statements to create a table named **log4jLogs** by using sample data provided with the HDInsight cluster:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    <span data-ttu-id="9f5d2-149">Deze instructies uitvoeren de volgende acties:</span><span class="sxs-lookup"><span data-stu-id="9f5d2-149">These statements perform the following actions:</span></span>

    * <span data-ttu-id="9f5d2-150">`DROP TABLE`-Als de tabel bestaat, wordt deze verwijderd.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-150">`DROP TABLE` - If the table exists, it is deleted.</span></span>

    * <span data-ttu-id="9f5d2-151">`CREATE EXTERNAL TABLE`-Maakt een **externe** tabel in Hive.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-151">`CREATE EXTERNAL TABLE` - Creates an **external** table in Hive.</span></span> <span data-ttu-id="9f5d2-152">De tabeldefinitie opslaan externe tabellen alleen in Hive.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-152">External tables only store the table definition in Hive.</span></span> <span data-ttu-id="9f5d2-153">De gegevens blijft op de oorspronkelijke locatie.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-153">The data is left in the original location.</span></span>

    * <span data-ttu-id="9f5d2-154">`ROW FORMAT`-Hoe de gegevens zijn ingedeeld.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-154">`ROW FORMAT` - How the data is formatted.</span></span> <span data-ttu-id="9f5d2-155">In dit geval worden de velden in elk logboek gescheiden door een spatie.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-155">In this case, the fields in each log are separated by a space.</span></span>

    * <span data-ttu-id="9f5d2-156">`STORED AS TEXTFILE LOCATION`-Waarin de gegevens worden opgeslagen en in welke bestandsindeling.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-156">`STORED AS TEXTFILE LOCATION` - Where the data is stored and in what file format.</span></span>

    * <span data-ttu-id="9f5d2-157">`SELECT`: Hiermee kunt u een telling van alle rijen waarin kolom **t4** bevat de waarde **[fout]**.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-157">`SELECT` - Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="9f5d2-158">Deze query retourneert een waarde van **3** omdat er zijn drie rijen met deze waarde.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-158">This query returns a value of **3** as there are three rows that contain this value.</span></span>

    * <span data-ttu-id="9f5d2-159">`INPUT__FILE__NAME LIKE '%.log'`-Hive probeert het schema toepassen op alle bestanden in de map.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-159">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts to apply the schema to all files in the directory.</span></span> <span data-ttu-id="9f5d2-160">In dit geval wordt bevat de map bestanden die niet overeenkomen met het schema.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-160">In this case, the directory contains files that do not match the schema.</span></span> <span data-ttu-id="9f5d2-161">Om te voorkomen dat een garbagecollection-gegevens in de resultaten, deze instructie vertelt Hive dat we alleen gegevens uit bestanden eindigt op moet retourneren. log.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-161">To prevent garbage data in the results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

  > [!NOTE]
  > <span data-ttu-id="9f5d2-162">Externe tabellen moeten worden gebruikt wanneer u de onderliggende gegevens wordt bijgewerkt door een externe bron verwacht.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-162">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="9f5d2-163">Bijvoorbeeld, een uploadproces geautomatiseerde gegevens of een MapReduce-bewerking.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-163">For example, an automated data upload process or a MapReduce operation.</span></span>
  >
  > <span data-ttu-id="9f5d2-164">Verwijderen van een externe tabel komt **niet** de gegevens, de definitie van de tabel verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-164">Dropping an external table does **not** delete the data, only the table definition.</span></span>

    <span data-ttu-id="9f5d2-165">De uitvoer van deze opdracht is vergelijkbaar met de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="9f5d2-165">The output of this command is similar to the following text:</span></span>

        INFO  : Tez session hasn't been created yet. Opening session
        INFO  :

        INFO  : Status: Running (Executing on YARN cluster with App id application_1443698635933_0001)

        INFO  : Map 1: -/-      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0(+1)/1
        INFO  : Map 1: 1/1      Reducer 2: 1/1
        +----------+--------+--+
        |   sev    | count  |
        +----------+--------+--+
        | [ERROR]  | 3      |
        +----------+--------+--+
        1 row selected (47.351 seconds)

5. <span data-ttu-id="9f5d2-166">Gebruiken om af te sluiten Beeline `!exit`.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-166">To exit Beeline, use `!exit`.</span></span>

## <span data-ttu-id="9f5d2-167"><a id="file"></a>Gebruik Beeline een HiveQL-bestand uit te voeren</span><span class="sxs-lookup"><span data-stu-id="9f5d2-167"><a id="file"></a>Use Beeline to run a HiveQL file</span></span>

<span data-ttu-id="9f5d2-168">Gebruik de volgende stappen uit om te maken van een bestand en voer vervolgens met behulp van Beeline.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-168">Use the following steps to create a file, then run it using Beeline.</span></span>

1. <span data-ttu-id="9f5d2-169">Gebruik de volgende opdracht voor het maken van een bestand met de naam **query.hql**:</span><span class="sxs-lookup"><span data-stu-id="9f5d2-169">Use the following command to create a file named **query.hql**:</span></span>

    ```bash
    nano query.hql
    ```

2. <span data-ttu-id="9f5d2-170">Gebruik de volgende tekst als de inhoud van het bestand.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-170">Use the following text as the contents of the file.</span></span> <span data-ttu-id="9f5d2-171">Deze query maakt een nieuwe 'interne' tabel met de naam **foutenlogboeken**:</span><span class="sxs-lookup"><span data-stu-id="9f5d2-171">This query creates a new 'internal' table named **errorLogs**:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    <span data-ttu-id="9f5d2-172">Deze instructies uitvoeren de volgende acties:</span><span class="sxs-lookup"><span data-stu-id="9f5d2-172">These statements perform the following actions:</span></span>

    * <span data-ttu-id="9f5d2-173">**MAKEN van tabel als niet bestaat** -als de tabel niet al bestaat, wordt deze gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-173">**CREATE TABLE IF NOT EXISTS** - If the table does not already exist, it is created.</span></span> <span data-ttu-id="9f5d2-174">Aangezien de **externe** trefwoord wordt niet gebruikt, wordt deze instructie maakt u een interne tabel.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-174">Since the **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="9f5d2-175">Interne tabellen worden opgeslagen in het datawarehouse Hive en volledig worden beheerd door Hive.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-175">Internal tables are stored in the Hive data warehouse and are managed completely by Hive.</span></span>
    * <span data-ttu-id="9f5d2-176">**OPGESLAGEN AS ORC** -slaat de gegevens geoptimaliseerd rij kolommen (ORC)-indeling.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-176">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="9f5d2-177">ORC is een maximaal geoptimaliseerd en efficiënte indeling voor het opslaan van gegevens met Hive.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-177">ORC format is a highly optimized and efficient format for storing Hive data.</span></span>
    * <span data-ttu-id="9f5d2-178">**INSERT OVERSCHRIJVEN... Selecteer** -selecteert rijen uit de **log4jLogs** tabel met **[fout]**, voegt u vervolgens de gegevens in de **foutenlogboeken** tabel.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-178">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9f5d2-179">In tegenstelling tot externe tabellen voor het verwijderen van een interne tabel worden verwijderd en de onderliggende gegevens.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-179">Unlike external tables, dropping an internal table deletes the underlying data as well.</span></span>

3. <span data-ttu-id="9f5d2-180">Gebruiken om het bestand opslaat, **Ctrl**+**_X**, voer dan **Y**, en tot slot **Enter**.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-180">To save the file, use **Ctrl**+**_X**, then enter **Y**, and finally **Enter**.</span></span>

4. <span data-ttu-id="9f5d2-181">Gebruik de volgende in het bestand met Beeline uit te voeren:</span><span class="sxs-lookup"><span data-stu-id="9f5d2-181">Use the following to run the file using Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > <span data-ttu-id="9f5d2-182">De `-i` parameter Beeline begint, voert u de instructies in het bestand query.hql.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-182">The `-i` parameter starts Beeline, runs the statements in the query.hql file.</span></span> <span data-ttu-id="9f5d2-183">Nadat de query is voltooid, wordt u aankomt bij de `jdbc:hive2://headnodehost:10001/>` prompt.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-183">Once the query completes, you arrive at the `jdbc:hive2://headnodehost:10001/>` prompt.</span></span> <span data-ttu-id="9f5d2-184">U kunt ook uitvoeren voor een bestand met de `-f` parameter Beeline afgesloten nadat de query is voltooid.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-184">You can also run a file using the `-f` parameter, which exits Beeline after the query completes.</span></span>

5. <span data-ttu-id="9f5d2-185">Om te controleren of de **foutenlogboeken** tabel is gemaakt, met de volgende instructie retourneert alle rijen uit **foutenlogboeken**:</span><span class="sxs-lookup"><span data-stu-id="9f5d2-185">To verify that the **errorLogs** table was created, use the following statement to return all the rows from **errorLogs**:</span></span>

    ```hiveql
    SELECT * from errorLogs;
    ```

    <span data-ttu-id="9f5d2-186">Drie rijen met gegevens moeten worden geretourneerd, alle overkoepelende **[fout]** in kolom t4:</span><span class="sxs-lookup"><span data-stu-id="9f5d2-186">Three rows of data should be returned, all containing **[ERROR]** in column t4:</span></span>

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <span data-ttu-id="9f5d2-187"><a id="remote"></a>Beeline op afstand gebruiken</span><span class="sxs-lookup"><span data-stu-id="9f5d2-187"><a id="remote"></a>Use Beeline remotely</span></span>

<span data-ttu-id="9f5d2-188">Als u deze Beeline lokaal zijn geïnstalleerd, of wordt gebruikt door een Docker-installatiekopie, zoals [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), moet u de volgende parameters:</span><span class="sxs-lookup"><span data-stu-id="9f5d2-188">If you have Beeline installed locally, or are using it through a Docker image such as [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), you must use the following parameters:</span></span>

* <span data-ttu-id="9f5d2-189">__Verbindingsreeks__:`-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span><span class="sxs-lookup"><span data-stu-id="9f5d2-189">__Connection string__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span></span>

* <span data-ttu-id="9f5d2-190">__Aanmeldingsnaam van de cluster__:`-n admin`</span><span class="sxs-lookup"><span data-stu-id="9f5d2-190">__Cluster login name__: `-n admin`</span></span>

* <span data-ttu-id="9f5d2-191">__Aanmeldingswachtwoord cluster__`-p 'password'`</span><span class="sxs-lookup"><span data-stu-id="9f5d2-191">__Cluster login password__ `-p 'password'`</span></span>

<span data-ttu-id="9f5d2-192">Vervang de `clustername` in de verbindingstekenreeks met de naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-192">Replace the `clustername` in the connection string with the name of your HDInsight cluster.</span></span>

<span data-ttu-id="9f5d2-193">Vervang `admin` met de naam van uw cluster aanmelding en vervang `password` met het wachtwoord voor uw cluster-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-193">Replace `admin` with the name of your cluster login, and replace `password` with the password for your cluster login.</span></span>

## <span data-ttu-id="9f5d2-194"><a id="sparksql"></a>Beeline met Spark gebruiken</span><span class="sxs-lookup"><span data-stu-id="9f5d2-194"><a id="sparksql"></a>Use Beeline with Spark</span></span>

<span data-ttu-id="9f5d2-195">Spark biedt een eigen implementatie van HiveServer2, dit is vaak zoals als de Spark Thrift-server.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-195">Spark provides its own implementation of HiveServer2, which is often refered to as the Spark Thrift server.</span></span> <span data-ttu-id="9f5d2-196">Deze service wordt Spark SQL gebruikt voor query's in plaats van Hive omzetten en kan zorgen voor betere prestaties, afhankelijk van uw query.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-196">This service uses Spark SQL to resolve queries instead of Hive, and may provide better performance depending on your query.</span></span>

<span data-ttu-id="9f5d2-197">Poort gebruiken voor verbinding met de Spark Thrift-server van een Spark in HDInsight-cluster, `10002` in plaats van `10001`.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-197">To connect to the Spark Thrift server of a Spark on HDInsight cluster, use port `10002` instead of `10001`.</span></span> <span data-ttu-id="9f5d2-198">Bijvoorbeeld `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-198">For example, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f5d2-199">De Spark Thrift-server is niet rechtstreeks toegankelijk via het internet.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-199">The Spark Thrift server is not directly accessible over the internet.</span></span> <span data-ttu-id="9f5d2-200">U kunt alleen verbinding met deze van een SSH-sessie of in het hetzelfde virtuele Azure-netwerk als het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9f5d2-200">You can only connect to it from an SSH session or inside the same Azure Virtual Network as the HDInsight cluster.</span></span>

## <span data-ttu-id="9f5d2-201"><a id="summary"></a><a id="nextsteps"></a>De volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9f5d2-201"><a id="summary"></a><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="9f5d2-202">Zie het volgende document voor meer algemene informatie over Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9f5d2-202">For more general information on Hive in HDInsight, see the following document:</span></span>

* [<span data-ttu-id="9f5d2-203">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f5d2-203">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="9f5d2-204">Zie de volgende documenten voor meer informatie over andere manieren kunt u werken met Hadoop op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9f5d2-204">For more information on other ways you can work with Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="9f5d2-205">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f5d2-205">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="9f5d2-206">MapReduce gebruiken met Hadoop op HDInsight</span><span class="sxs-lookup"><span data-stu-id="9f5d2-206">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="9f5d2-207">Als u van Tez met Hive gebruikmaakt, raadpleegt u de volgende documenten:</span><span class="sxs-lookup"><span data-stu-id="9f5d2-207">If you are using Tez with Hive, see the following documents:</span></span>

* [<span data-ttu-id="9f5d2-208">De Tez-gebruikersinterface op HDInsight op basis van Windows gebruiken</span><span class="sxs-lookup"><span data-stu-id="9f5d2-208">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="9f5d2-209">De weergave Ambari Tez op Linux gebaseerde HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="9f5d2-209">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md

[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html


[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
