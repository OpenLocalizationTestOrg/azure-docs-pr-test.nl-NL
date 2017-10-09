---
title: aaaUse Beeline met Apache Hive - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse hello Beeline client toorun Hive query's met Hadoop op HDInsight. Beeline is een hulpprogramma voor het werken met HiveServer2 via JDBC vast.
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
ms.openlocfilehash: e788ff39f33d928808cfcb83a92f62ac9ae8ca09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-beeline-client-with-apache-hive"></a><span data-ttu-id="9d50e-105">Hallo Beeline client met Apache Hive gebruiken</span><span class="sxs-lookup"><span data-stu-id="9d50e-105">Use hello Beeline client with Apache Hive</span></span>

<span data-ttu-id="9d50e-106">Meer informatie over hoe toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) toorun Hive query's op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9d50e-106">Learn how toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) toorun Hive queries on HDInsight.</span></span>

<span data-ttu-id="9d50e-107">Beeline is een Hive-client die is opgenomen op Hallo hoofdknooppunten van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9d50e-107">Beeline is a Hive client that is included on hello head nodes of your HDInsight cluster.</span></span> <span data-ttu-id="9d50e-108">Beeline JDBC tooconnect tooHiveServer2, een service die wordt gehost op uw HDInsight-cluster gebruikt.</span><span class="sxs-lookup"><span data-stu-id="9d50e-108">Beeline uses JDBC tooconnect tooHiveServer2, a service hosted on your HDInsight cluster.</span></span> <span data-ttu-id="9d50e-109">U kunt ook gebruiken Beeline tooaccess Hive in HDInsight op afstand meer dan Hallo internet.</span><span class="sxs-lookup"><span data-stu-id="9d50e-109">You can also use Beeline tooaccess Hive on HDInsight remotely over hello internet.</span></span> <span data-ttu-id="9d50e-110">Hallo volgende tabel bevat de verbindingsreeksen voor gebruik met Beeline:</span><span class="sxs-lookup"><span data-stu-id="9d50e-110">hello following table provides connection strings for use with Beeline:</span></span>

| <span data-ttu-id="9d50e-111">Waar u Beeline van uitvoert</span><span class="sxs-lookup"><span data-stu-id="9d50e-111">Where you run Beeline from</span></span> | <span data-ttu-id="9d50e-112">Parameters</span><span class="sxs-lookup"><span data-stu-id="9d50e-112">Parameters</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9d50e-113">Een SSH-verbinding tooa headnode of edge-knooppunt</span><span class="sxs-lookup"><span data-stu-id="9d50e-113">An SSH connection tooa headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| <span data-ttu-id="9d50e-114">Externe Hallo-cluster</span><span class="sxs-lookup"><span data-stu-id="9d50e-114">Outside hello cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> <span data-ttu-id="9d50e-115">Vervang `admin` met Hallo cluster aanmeldingsaccount voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="9d50e-115">Replace `admin` with hello cluster login account for your cluster.</span></span>
>
> <span data-ttu-id="9d50e-116">Vervang `password` door Hallo wachtwoord voor aanmeldingsaccount Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="9d50e-116">Replace `password` with hello password for hello cluster login account.</span></span>
>
> <span data-ttu-id="9d50e-117">Vervang `clustername` met Hallo-naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9d50e-117">Replace `clustername` with hello name of your HDInsight cluster.</span></span>

## <span data-ttu-id="9d50e-118"><a id="prereq"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="9d50e-118"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="9d50e-119">Een op Linux gebaseerde Hadoop op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9d50e-119">A Linux-based Hadoop on HDInsight cluster.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="9d50e-120">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="9d50e-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9d50e-121">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9d50e-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="9d50e-122">Een SSH-client of een lokale Beeline-client.</span><span class="sxs-lookup"><span data-stu-id="9d50e-122">An SSH client or a local Beeline client.</span></span> <span data-ttu-id="9d50e-123">De meeste Hallo stappen in dit document wordt ervan uitgegaan dat u van Beeline van een SSH-sessie toohello cluster gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="9d50e-123">Most of hello steps in this document assume that you are using Beeline from an SSH session toohello cluster.</span></span> <span data-ttu-id="9d50e-124">Zie voor informatie over het uitvoeren van Beeline uit externe Hallo cluster Hallo [Beeline op afstand gebruiken](#remote) sectie.</span><span class="sxs-lookup"><span data-stu-id="9d50e-124">For information on running Beeline from outside hello cluster, see hello [use Beeline remotely](#remote) section.</span></span>

    <span data-ttu-id="9d50e-125">Zie voor meer informatie over het gebruik van SSH [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="9d50e-125">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="9d50e-126"><a id="beeline"></a>Gebruik Beeline</span><span class="sxs-lookup"><span data-stu-id="9d50e-126"><a id="beeline"></a>Use Beeline</span></span>

1. <span data-ttu-id="9d50e-127">Bij het starten van Beeline, moet u een verbindingsreeks opgeven voor HiveServer2 op uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9d50e-127">When starting Beeline, you must provide a connection string for HiveServer2 on your HDInsight cluster.</span></span> <span data-ttu-id="9d50e-128">toorun Hallo-opdracht uit externe Hallo-cluster, moet u ook Hallo cluster aanmeldingsnaam account opgeven (standaard `admin`) en het wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="9d50e-128">toorun hello command from outside hello cluster, you must also provide hello cluster login account name (default `admin`) and password.</span></span> <span data-ttu-id="9d50e-129">Hallo tabel toofind Hallo connection string indeling en parameters toouse volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="9d50e-129">Use hello following table toofind hello connection string format and parameters toouse:</span></span>

    | <span data-ttu-id="9d50e-130">Waar u Beeline van uitvoert</span><span class="sxs-lookup"><span data-stu-id="9d50e-130">Where you run Beeline from</span></span> | <span data-ttu-id="9d50e-131">Parameters</span><span class="sxs-lookup"><span data-stu-id="9d50e-131">Parameters</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="9d50e-132">Een SSH-verbinding tooa headnode of edge-knooppunt</span><span class="sxs-lookup"><span data-stu-id="9d50e-132">An SSH connection tooa headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | <span data-ttu-id="9d50e-133">Externe Hallo-cluster</span><span class="sxs-lookup"><span data-stu-id="9d50e-133">Outside hello cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    <span data-ttu-id="9d50e-134">Hallo na de opdracht kan bijvoorbeeld gebruikte toostart Beeline van een SSH-sessie toohello cluster:</span><span class="sxs-lookup"><span data-stu-id="9d50e-134">For example, hello following command can be used toostart Beeline from an SSH session toohello cluster:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    <span data-ttu-id="9d50e-135">Met deze opdracht Hallo Beeline client start en tooHiveServer2 Hallo hoofdknooppunt van cluster verbindt.</span><span class="sxs-lookup"><span data-stu-id="9d50e-135">This command starts hello Beeline client, and connects tooHiveServer2 on hello cluster head node.</span></span> <span data-ttu-id="9d50e-136">Zodra het Hallo-opdracht is voltooid, wordt u aankomt bij een `jdbc:hive2://headnodehost:10001/>` prompt.</span><span class="sxs-lookup"><span data-stu-id="9d50e-136">Once hello command completes, you arrive at a `jdbc:hive2://headnodehost:10001/>` prompt.</span></span>

2. <span data-ttu-id="9d50e-137">Beeline opdrachten beginnen met een `!` teken, bijvoorbeeld `!help` geeft help weer.</span><span class="sxs-lookup"><span data-stu-id="9d50e-137">Beeline commands begin with a `!` character, for example `!help` displays help.</span></span> <span data-ttu-id="9d50e-138">Hallo echter `!` voor bepaalde opdrachten kunnen worden weggelaten.</span><span class="sxs-lookup"><span data-stu-id="9d50e-138">However hello `!` can be omitted for some commands.</span></span> <span data-ttu-id="9d50e-139">Bijvoorbeeld: `help` werkt ook.</span><span class="sxs-lookup"><span data-stu-id="9d50e-139">For example, `help` also works.</span></span>

    <span data-ttu-id="9d50e-140">Er is een `!sql`, die is gebruikt tooexecute HiveQL-instructies.</span><span class="sxs-lookup"><span data-stu-id="9d50e-140">There is a `!sql`, which is used tooexecute HiveQL statements.</span></span> <span data-ttu-id="9d50e-141">HiveQL wordt echter zo vaak gebruikt dat kunt u de voorgaande Hallo weglaten `!sql`.</span><span class="sxs-lookup"><span data-stu-id="9d50e-141">However, HiveQL is so commonly used that you can omit hello preceding `!sql`.</span></span> <span data-ttu-id="9d50e-142">Hallo twee instructies te volgen zijn gelijkwaardig:</span><span class="sxs-lookup"><span data-stu-id="9d50e-142">hello following two statements are equivalent:</span></span>

    ```hiveql
    !sql show tables;
    show tables;
    ```

    <span data-ttu-id="9d50e-143">Op een nieuw cluster slechts één tabel wordt vermeld: **hivesampletable**.</span><span class="sxs-lookup"><span data-stu-id="9d50e-143">On a new cluster, only one table is listed: **hivesampletable**.</span></span>

3. <span data-ttu-id="9d50e-144">Hallo opdracht toodisplay Hallo schema voor Hallo hivesampletable volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="9d50e-144">Use hello following command toodisplay hello schema for hello hivesampletable:</span></span>

    ```hiveql
    describe hivesampletable;
    ```

    <span data-ttu-id="9d50e-145">Met deze opdracht retourneert Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="9d50e-145">This command returns hello following information:</span></span>

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

    <span data-ttu-id="9d50e-146">Deze informatie wordt Hallo kolommen in Hallo tabel beschreven.</span><span class="sxs-lookup"><span data-stu-id="9d50e-146">This information describes hello columns in hello table.</span></span> <span data-ttu-id="9d50e-147">Bij sommige query's op deze gegevens kan worden uitgevoerd, gaan we in plaats daarvan maakt een nieuwe tabel toodemonstrate hoe tooload gegevens in Hive en een schema hebt toegepast.</span><span class="sxs-lookup"><span data-stu-id="9d50e-147">While we could perform some queries against this data, let's instead create a brand new table toodemonstrate how tooload data into Hive and apply a schema.</span></span>

4. <span data-ttu-id="9d50e-148">Voer Hallo na instructies toocreate een tabel met de naam **log4jLogs** met behulp van voorbeeldgegevens voorzien Hallo HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="9d50e-148">Enter hello following statements toocreate a table named **log4jLogs** by using sample data provided with hello HDInsight cluster:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    <span data-ttu-id="9d50e-149">Deze instructies uitvoeren Hallo volgende acties:</span><span class="sxs-lookup"><span data-stu-id="9d50e-149">These statements perform hello following actions:</span></span>

    * <span data-ttu-id="9d50e-150">`DROP TABLE`-Als Hallo tabel bestaat, wordt deze verwijderd.</span><span class="sxs-lookup"><span data-stu-id="9d50e-150">`DROP TABLE` - If hello table exists, it is deleted.</span></span>

    * <span data-ttu-id="9d50e-151">`CREATE EXTERNAL TABLE`-Maakt een **externe** tabel in Hive.</span><span class="sxs-lookup"><span data-stu-id="9d50e-151">`CREATE EXTERNAL TABLE` - Creates an **external** table in Hive.</span></span> <span data-ttu-id="9d50e-152">De tabeldefinitie Hallo opslaan externe tabellen alleen in Hive.</span><span class="sxs-lookup"><span data-stu-id="9d50e-152">External tables only store hello table definition in Hive.</span></span> <span data-ttu-id="9d50e-153">Hallo-gegevens in de oorspronkelijke locatie Hallo gelaten.</span><span class="sxs-lookup"><span data-stu-id="9d50e-153">hello data is left in hello original location.</span></span>

    * <span data-ttu-id="9d50e-154">`ROW FORMAT`-Hoe Hallo gegevens zijn opgemaakt.</span><span class="sxs-lookup"><span data-stu-id="9d50e-154">`ROW FORMAT` - How hello data is formatted.</span></span> <span data-ttu-id="9d50e-155">In dit geval worden Hallo velden in elk logboek gescheiden door een spatie.</span><span class="sxs-lookup"><span data-stu-id="9d50e-155">In this case, hello fields in each log are separated by a space.</span></span>

    * <span data-ttu-id="9d50e-156">`STORED AS TEXTFILE LOCATION`-Waarin Hallo gegevens worden opgeslagen en in welke bestandsindeling.</span><span class="sxs-lookup"><span data-stu-id="9d50e-156">`STORED AS TEXTFILE LOCATION` - Where hello data is stored and in what file format.</span></span>

    * <span data-ttu-id="9d50e-157">`SELECT`: Hiermee kunt u een telling van alle rijen waarin kolom **t4** Hallo waarde bevat **[fout]**.</span><span class="sxs-lookup"><span data-stu-id="9d50e-157">`SELECT` - Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="9d50e-158">Deze query retourneert een waarde van **3** omdat er zijn drie rijen met deze waarde.</span><span class="sxs-lookup"><span data-stu-id="9d50e-158">This query returns a value of **3** as there are three rows that contain this value.</span></span>

    * <span data-ttu-id="9d50e-159">`INPUT__FILE__NAME LIKE '%.log'`-Hive probeert tooapply hello tooall schemabestanden in Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="9d50e-159">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts tooapply hello schema tooall files in hello directory.</span></span> <span data-ttu-id="9d50e-160">In dit geval bevat Hallo map bestanden die niet overeenkomen met de Hallo schema.</span><span class="sxs-lookup"><span data-stu-id="9d50e-160">In this case, hello directory contains files that do not match hello schema.</span></span> <span data-ttu-id="9d50e-161">tooprevent garbagecollection gegevens in de resultaten van de hello, deze instructie Hive vertelt dat we alleen gegevens uit bestanden eindigt op moet retourneren. log.</span><span class="sxs-lookup"><span data-stu-id="9d50e-161">tooprevent garbage data in hello results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

  > [!NOTE]
  > <span data-ttu-id="9d50e-162">Externe tabellen moeten worden gebruikt wanneer u van plan Hallo onderliggende gegevens toobe bijgewerkt door een externe bron bent.</span><span class="sxs-lookup"><span data-stu-id="9d50e-162">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="9d50e-163">Bijvoorbeeld, een uploadproces geautomatiseerde gegevens of een MapReduce-bewerking.</span><span class="sxs-lookup"><span data-stu-id="9d50e-163">For example, an automated data upload process or a MapReduce operation.</span></span>
  >
  > <span data-ttu-id="9d50e-164">Verwijderen van een externe tabel komt **niet** Hallo gegevens alleen Hallo tabeldefinitie kunt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9d50e-164">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

    <span data-ttu-id="9d50e-165">Hallo uitvoer van deze opdracht is vergelijkbaar toohello de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="9d50e-165">hello output of this command is similar toohello following text:</span></span>

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

5. <span data-ttu-id="9d50e-166">tooexit Beeline, gebruik `!exit`.</span><span class="sxs-lookup"><span data-stu-id="9d50e-166">tooexit Beeline, use `!exit`.</span></span>

## <span data-ttu-id="9d50e-167"><a id="file"></a>Beeline toorun een bestand HiveQL gebruiken</span><span class="sxs-lookup"><span data-stu-id="9d50e-167"><a id="file"></a>Use Beeline toorun a HiveQL file</span></span>

<span data-ttu-id="9d50e-168">Volgende stappen toocreate een bestand, voert u met behulp van Beeline hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9d50e-168">Use hello following steps toocreate a file, then run it using Beeline.</span></span>

1. <span data-ttu-id="9d50e-169">Gebruik Hallo volgende opdracht toocreate uit een bestand met de naam **query.hql**:</span><span class="sxs-lookup"><span data-stu-id="9d50e-169">Use hello following command toocreate a file named **query.hql**:</span></span>

    ```bash
    nano query.hql
    ```

2. <span data-ttu-id="9d50e-170">Gebruik hello tekst als Hallo inhoud van Hallo-bestand te volgen.</span><span class="sxs-lookup"><span data-stu-id="9d50e-170">Use hello following text as hello contents of hello file.</span></span> <span data-ttu-id="9d50e-171">Deze query maakt een nieuwe 'interne' tabel met de naam **foutenlogboeken**:</span><span class="sxs-lookup"><span data-stu-id="9d50e-171">This query creates a new 'internal' table named **errorLogs**:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    <span data-ttu-id="9d50e-172">Deze instructies uitvoeren Hallo volgende acties:</span><span class="sxs-lookup"><span data-stu-id="9d50e-172">These statements perform hello following actions:</span></span>

    * <span data-ttu-id="9d50e-173">**MAKEN van tabel als niet bestaat** -als Hallo tabel niet al bestaat, wordt deze gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9d50e-173">**CREATE TABLE IF NOT EXISTS** - If hello table does not already exist, it is created.</span></span> <span data-ttu-id="9d50e-174">Sinds Hallo **externe** trefwoord wordt niet gebruikt, wordt deze instructie maakt u een interne tabel.</span><span class="sxs-lookup"><span data-stu-id="9d50e-174">Since hello **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="9d50e-175">Interne tabellen worden opgeslagen in Hallo Hive-datawarehouse en volledig worden beheerd door Hive.</span><span class="sxs-lookup"><span data-stu-id="9d50e-175">Internal tables are stored in hello Hive data warehouse and are managed completely by Hive.</span></span>
    * <span data-ttu-id="9d50e-176">**OPGESLAGEN AS ORC** -Hallo-gegevens opslaat in geoptimaliseerd rij kolommen (ORC)-indeling.</span><span class="sxs-lookup"><span data-stu-id="9d50e-176">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="9d50e-177">ORC is een maximaal geoptimaliseerd en efficiënte indeling voor het opslaan van gegevens met Hive.</span><span class="sxs-lookup"><span data-stu-id="9d50e-177">ORC format is a highly optimized and efficient format for storing Hive data.</span></span>
    * <span data-ttu-id="9d50e-178">**INSERT OVERSCHRIJVEN... Selecteer** -rijen uit Hallo geselecteerd **log4jLogs** tabel met **[fout]**, en vervolgens voegt gegevens in Hallo Hallo **foutenlogboeken** tabel.</span><span class="sxs-lookup"><span data-stu-id="9d50e-178">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9d50e-179">In tegenstelling tot externe tabellen verwijdert de Hallo onderliggende gegevens ook een interne tabel verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9d50e-179">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

3. <span data-ttu-id="9d50e-180">Gebruik-bestand Hallo toosave **Ctrl**+**_X**, voert u **Y**, en tot slot **Enter**.</span><span class="sxs-lookup"><span data-stu-id="9d50e-180">toosave hello file, use **Ctrl**+**_X**, then enter **Y**, and finally **Enter**.</span></span>

4. <span data-ttu-id="9d50e-181">Hallo toorun Hallo bestand met behulp van Beeline volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="9d50e-181">Use hello following toorun hello file using Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > <span data-ttu-id="9d50e-182">Hallo `-i` parameter Beeline begint, voert Hallo instructies in Hallo query.hql bestand.</span><span class="sxs-lookup"><span data-stu-id="9d50e-182">hello `-i` parameter starts Beeline, runs hello statements in hello query.hql file.</span></span> <span data-ttu-id="9d50e-183">Zodra het Hallo-query is voltooid, wordt u aankomt bij Hallo `jdbc:hive2://headnodehost:10001/>` prompt.</span><span class="sxs-lookup"><span data-stu-id="9d50e-183">Once hello query completes, you arrive at hello `jdbc:hive2://headnodehost:10001/>` prompt.</span></span> <span data-ttu-id="9d50e-184">U kunt ook een bestand met de Hallo uitvoeren `-f` parameter Beeline afgesloten nadat Hallo-query is voltooid.</span><span class="sxs-lookup"><span data-stu-id="9d50e-184">You can also run a file using hello `-f` parameter, which exits Beeline after hello query completes.</span></span>

5. <span data-ttu-id="9d50e-185">tooverify die Hallo **foutenlogboeken** tabel is gemaakt, gebruikt u na de instructie tooreturn alle rijen uit Hallo Hallo **foutenlogboeken**:</span><span class="sxs-lookup"><span data-stu-id="9d50e-185">tooverify that hello **errorLogs** table was created, use hello following statement tooreturn all hello rows from **errorLogs**:</span></span>

    ```hiveql
    SELECT * from errorLogs;
    ```

    <span data-ttu-id="9d50e-186">Drie rijen met gegevens moeten worden geretourneerd, alle overkoepelende **[fout]** in kolom t4:</span><span class="sxs-lookup"><span data-stu-id="9d50e-186">Three rows of data should be returned, all containing **[ERROR]** in column t4:</span></span>

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <span data-ttu-id="9d50e-187"><a id="remote"></a>Beeline op afstand gebruiken</span><span class="sxs-lookup"><span data-stu-id="9d50e-187"><a id="remote"></a>Use Beeline remotely</span></span>

<span data-ttu-id="9d50e-188">Als u deze Beeline lokaal zijn geïnstalleerd, of wordt gebruikt door een Docker-installatiekopie, zoals [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), moet u de volgende parameters hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="9d50e-188">If you have Beeline installed locally, or are using it through a Docker image such as [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), you must use hello following parameters:</span></span>

* <span data-ttu-id="9d50e-189">__Verbindingsreeks__:`-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span><span class="sxs-lookup"><span data-stu-id="9d50e-189">__Connection string__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span></span>

* <span data-ttu-id="9d50e-190">__Aanmeldingsnaam van de cluster__:`-n admin`</span><span class="sxs-lookup"><span data-stu-id="9d50e-190">__Cluster login name__: `-n admin`</span></span>

* <span data-ttu-id="9d50e-191">__Aanmeldingswachtwoord cluster__`-p 'password'`</span><span class="sxs-lookup"><span data-stu-id="9d50e-191">__Cluster login password__ `-p 'password'`</span></span>

<span data-ttu-id="9d50e-192">Vervang Hallo `clustername` in de verbindingsreeks Hallo Hallo-naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9d50e-192">Replace hello `clustername` in hello connection string with hello name of your HDInsight cluster.</span></span>

<span data-ttu-id="9d50e-193">Vervang `admin` met de naam van uw cluster aanmelding en vervang Hallo `password` met Hallo wachtwoord voor uw cluster-aanmelding.</span><span class="sxs-lookup"><span data-stu-id="9d50e-193">Replace `admin` with hello name of your cluster login, and replace `password` with hello password for your cluster login.</span></span>

## <span data-ttu-id="9d50e-194"><a id="sparksql"></a>Beeline met Spark gebruiken</span><span class="sxs-lookup"><span data-stu-id="9d50e-194"><a id="sparksql"></a>Use Beeline with Spark</span></span>

<span data-ttu-id="9d50e-195">Spark biedt een eigen implementatie van HiveServer2, die vaak zoals tooas Hallo Spark Thrift-server.</span><span class="sxs-lookup"><span data-stu-id="9d50e-195">Spark provides its own implementation of HiveServer2, which is often refered tooas hello Spark Thrift server.</span></span> <span data-ttu-id="9d50e-196">Deze service Spark SQL tooresolve query's gebruikt in plaats van Hive en kan zorgen voor betere prestaties, afhankelijk van uw query.</span><span class="sxs-lookup"><span data-stu-id="9d50e-196">This service uses Spark SQL tooresolve queries instead of Hive, and may provide better performance depending on your query.</span></span>

<span data-ttu-id="9d50e-197">tooconnect toohello Spark Thrift-server van een Spark in HDInsight-cluster, gebruik poort `10002` in plaats van `10001`.</span><span class="sxs-lookup"><span data-stu-id="9d50e-197">tooconnect toohello Spark Thrift server of a Spark on HDInsight cluster, use port `10002` instead of `10001`.</span></span> <span data-ttu-id="9d50e-198">Bijvoorbeeld `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span><span class="sxs-lookup"><span data-stu-id="9d50e-198">For example, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9d50e-199">Hallo Spark Thrift-server is niet rechtstreeks toegankelijk via internet Hallo.</span><span class="sxs-lookup"><span data-stu-id="9d50e-199">hello Spark Thrift server is not directly accessible over hello internet.</span></span> <span data-ttu-id="9d50e-200">U kunt alleen tooit verbinding van een SSH-sessie of Hallo binnen hetzelfde virtuele Azure-netwerk zoals Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9d50e-200">You can only connect tooit from an SSH session or inside hello same Azure Virtual Network as hello HDInsight cluster.</span></span>

## <span data-ttu-id="9d50e-201"><a id="summary"></a><a id="nextsteps"></a>De volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9d50e-201"><a id="summary"></a><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="9d50e-202">Zie voor meer algemene informatie over Hive in HDInsight Hallo document te volgen:</span><span class="sxs-lookup"><span data-stu-id="9d50e-202">For more general information on Hive in HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="9d50e-203">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="9d50e-203">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="9d50e-204">Zie voor meer informatie over andere manieren kunt u werken met Hadoop op HDInsight Hallo documenten te volgen:</span><span class="sxs-lookup"><span data-stu-id="9d50e-204">For more information on other ways you can work with Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="9d50e-205">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="9d50e-205">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="9d50e-206">MapReduce gebruiken met Hadoop op HDInsight</span><span class="sxs-lookup"><span data-stu-id="9d50e-206">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="9d50e-207">Als u van Tez met Hive gebruikmaakt, raadpleegt u Hallo documenten te volgen:</span><span class="sxs-lookup"><span data-stu-id="9d50e-207">If you are using Tez with Hive, see hello following documents:</span></span>

* [<span data-ttu-id="9d50e-208">Hallo Tez UI op HDInsight op basis van Windows gebruiken</span><span class="sxs-lookup"><span data-stu-id="9d50e-208">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="9d50e-209">Hallo Ambari Tez weergave op Linux gebaseerde HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="9d50e-209">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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
