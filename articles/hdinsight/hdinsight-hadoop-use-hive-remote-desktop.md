---
title: aaaUse Hadoop Hive en extern bureaublad in HDInsight - Azure | Microsoft Docs
description: Informatie over hoe tooconnect tooHadoop-cluster in HDInsight met behulp van extern bureaublad en vervolgens Hive-query's uitvoeren met behulp van Hallo opdrachtregelinterface Hive.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c228e35-d58a-4f22-917a-1d20c9da89b4
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: f86ffc1be33a8b0b2346d1a1388e5dfa6d0f8777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="55a91-103">Hive gebruiken met Hadoop op HDInsight met extern bureaublad</span><span class="sxs-lookup"><span data-stu-id="55a91-103">Use Hive with Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="55a91-104">In dit artikel leert u hoe tooconnect tooan HDInsight-cluster met behulp van extern bureaublad en voer vervolgens Hive query's met behulp van Hallo Hive-opdrachtregelinterface (CLI).</span><span class="sxs-lookup"><span data-stu-id="55a91-104">In this article, you will learn how tooconnect tooan HDInsight cluster by using Remote Desktop, and then run Hive queries by using hello Hive Command-Line Interface (CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="55a91-105">Extern bureaublad is alleen beschikbaar op HDInsight-clusters die Windows hello besturingssysteem gebruiken.</span><span class="sxs-lookup"><span data-stu-id="55a91-105">Remote Desktop is only available on HDInsight clusters that use Windows as hello operating system.</span></span> <span data-ttu-id="55a91-106">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="55a91-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="55a91-107">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="55a91-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="55a91-108">Voor HDInsight 3.4 of hoger, Zie [Hive gebruiken met HDInsight en Beeline](hdinsight-hadoop-use-hive-beeline.md) voor informatie over het uitvoeren van Hive-query rechtstreeks op Hallo-cluster vanaf een opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="55a91-108">For HDInsight 3.4 or greater, see [Use Hive with HDInsight and Beeline](hdinsight-hadoop-use-hive-beeline.md) for information on running Hive queries directly on hello cluster from a command-line.</span></span>

## <span data-ttu-id="55a91-109"><a id="prereq"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="55a91-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="55a91-110">toocomplete hello stappen in dit artikel, moet u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="55a91-110">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="55a91-111">Een cluster op basis van Windows HDInsight (Hadoop in HDInsight)</span><span class="sxs-lookup"><span data-stu-id="55a91-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="55a91-112">Een clientcomputer met Windows 10, Windows 8 of Windows 7</span><span class="sxs-lookup"><span data-stu-id="55a91-112">A client computer running Windows 10, Window 8, or Windows 7</span></span>

## <span data-ttu-id="55a91-113"><a id="connect"></a>Verbinding maken met extern bureaublad</span><span class="sxs-lookup"><span data-stu-id="55a91-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="55a91-114">Extern bureaublad inschakelen voor Hallo HDInsight-cluster en verbind tooit met behulp Hallo-instructies in de [tooHDInsight clusters met RDP verbinding](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="55a91-114">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="55a91-115"><a id="hive"></a>Hallo Hive-opdracht gebruiken</span><span class="sxs-lookup"><span data-stu-id="55a91-115"><a id="hive"></a>Use hello Hive command</span></span>
<span data-ttu-id="55a91-116">Wanneer u verbinding hebt met het bureaublad toohello voor Hallo HDInsight-cluster gebruiken Hallo toowork met Hive stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="55a91-116">When you have connected toohello desktop for hello HDInsight cluster, use hello following steps toowork with Hive:</span></span>

1. <span data-ttu-id="55a91-117">Hallo HDInsight bureaublad starten Hallo **Hadoop-opdrachtregel**.</span><span class="sxs-lookup"><span data-stu-id="55a91-117">From hello HDInsight desktop, start hello **Hadoop Command Line**.</span></span>
2. <span data-ttu-id="55a91-118">Voer Hallo opdracht toostart Hallo Hive CLI te volgen:</span><span class="sxs-lookup"><span data-stu-id="55a91-118">Enter hello following command toostart hello Hive CLI:</span></span>

        %hive_home%\bin\hive

    <span data-ttu-id="55a91-119">Als Hallo CLI is gestart, ziet u Hallo CLI Hive-prompt: `hive>`.</span><span class="sxs-lookup"><span data-stu-id="55a91-119">When hello CLI has started, you will see hello Hive CLI prompt: `hive>`.</span></span>
3. <span data-ttu-id="55a91-120">Gebruik Hallo CLI Hallo na toocreate instructies een nieuwe tabel met de naam te geven **log4jLogs** voorbeeldgegevens gebruikt:</span><span class="sxs-lookup"><span data-stu-id="55a91-120">Using hello CLI, enter hello following statements toocreate a new table named **log4jLogs** using sample data:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="55a91-121">Deze instructies uitvoeren Hallo volgende acties:</span><span class="sxs-lookup"><span data-stu-id="55a91-121">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="55a91-122">**DROP TABLE**: Hiermee verwijdert u Hallo tabel en het Hallo-gegevensbestand als Hallo tabel al bestaat.</span><span class="sxs-lookup"><span data-stu-id="55a91-122">**DROP TABLE**: Deletes hello table and hello data file if hello table already exists.</span></span>
   * <span data-ttu-id="55a91-123">**EXTERNE tabel maken**: maakt een nieuwe 'extern' tabel in Hive.</span><span class="sxs-lookup"><span data-stu-id="55a91-123">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="55a91-124">Externe tabellen opslaan alleen Hallo tabeldefinitie in Hive (hello gegevens in de oorspronkelijke locatie Hallo blijft).</span><span class="sxs-lookup"><span data-stu-id="55a91-124">External tables store only hello table definition in Hive (hello data is left in hello original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="55a91-125">Externe tabellen moeten worden gebruikt wanneer u gegevens toobe worden bijgewerkt door een externe bron (zoals een uploadproces geautomatiseerde gegevens) of door een andere MapReduce-bewerking onderliggende hello verwacht, maar u wilt dat altijd Hive query toouse Hallo meest recente gegevens.</span><span class="sxs-lookup"><span data-stu-id="55a91-125">External tables should be used when you expect hello underlying data toobe updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries toouse hello latest data.</span></span>
     >
     > <span data-ttu-id="55a91-126">Verwijderen van een externe tabel komt **niet** Hallo gegevens alleen Hallo tabeldefinitie kunt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="55a91-126">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>
     >
     >
   * <span data-ttu-id="55a91-127">**INDELING van de rij**: Hive-wordt uitgelegd hoe Hallo gegevens wordt opgemaakt.</span><span class="sxs-lookup"><span data-stu-id="55a91-127">**ROW FORMAT**: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="55a91-128">In dit geval worden Hallo velden in elk logboek gescheiden door een spatie.</span><span class="sxs-lookup"><span data-stu-id="55a91-128">In this case, hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="55a91-129">**AS TEXTFILE locatie opgeslagen**: vertelt Hive waar Hallo gegevens zijn opgeslagen (directory Hallo bijvoorbeeld/gegevens) en deze is opgeslagen als tekst.</span><span class="sxs-lookup"><span data-stu-id="55a91-129">**STORED AS TEXTFILE LOCATION**: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="55a91-130">**Selecteer**: selecteert een telling van alle rijen waarin kolom **t4** Hallo waarde bevat **[fout]**.</span><span class="sxs-lookup"><span data-stu-id="55a91-130">**SELECT**: Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="55a91-131">Dit moet een waarde van retourneren **3** omdat er drie rijen met deze waarde.</span><span class="sxs-lookup"><span data-stu-id="55a91-131">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="55a91-132">**INPUT__FILE__NAME zoals '%.log'** -vertelt Hive die we alleen gegevens uit bestanden eindigt op moet retourneren. log.</span><span class="sxs-lookup"><span data-stu-id="55a91-132">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="55a91-133">Hiermee beperkt u Hallo zoeken toohello sample.log-bestand dat Hallo gegevens bevat, en voorkomt dat het retourneren van gegevens uit andere voorbeeld gegevensbestanden die komen niet overeen met de Hallo-schema die is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="55a91-133">This restricts hello search toohello sample.log file that contains hello data, and keeps it from returning data from other example data files that do not match hello schema we defined.</span></span>
4. <span data-ttu-id="55a91-134">Gebruik Hallo na toocreate instructies een nieuwe 'interne' tabel met de naam **foutenlogboeken**:</span><span class="sxs-lookup"><span data-stu-id="55a91-134">Use hello following statements toocreate a new 'internal' table named **errorLogs**:</span></span>

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    <span data-ttu-id="55a91-135">Deze instructies uitvoeren Hallo volgende acties:</span><span class="sxs-lookup"><span data-stu-id="55a91-135">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="55a91-136">**MAKEN van tabel als niet bestaat**: maakt een tabel als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="55a91-136">**CREATE TABLE IF NOT EXISTS**: Creates a table if it does not already exist.</span></span> <span data-ttu-id="55a91-137">Omdat Hallo **externe** trefwoord wordt niet gebruikt, is dit een interne tabel die is opgeslagen in Hallo Hive-datawarehouse en volledig wordt beheerd door Hive.</span><span class="sxs-lookup"><span data-stu-id="55a91-137">Because hello **EXTERNAL** keyword is not used, this is an internal table, which is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="55a91-138">In tegenstelling tot **externe** tabellen, verwijderen van een interne tabel ook Hallo onderliggende gegevens worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="55a91-138">Unlike **EXTERNAL** tables, dropping an internal table also deletes hello underlying data.</span></span>
     >
     >
   * <span data-ttu-id="55a91-139">**OPGESLAGEN AS ORC**: Hallo-gegevens opslaat in geoptimaliseerde rij kolomindeling (ORC).</span><span class="sxs-lookup"><span data-stu-id="55a91-139">**STORED AS ORC**: Stores hello data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="55a91-140">Dit is een maximaal geoptimaliseerd en efficiënte indeling voor het opslaan van gegevens met Hive.</span><span class="sxs-lookup"><span data-stu-id="55a91-140">This is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="55a91-141">**INSERT OVERSCHRIJVEN... Selecteer**: rijen uit Hallo geselecteerd **log4jLogs** tabel met **[fout]**, en vervolgens voegt gegevens in Hallo Hallo **foutenlogboeken** tabel.</span><span class="sxs-lookup"><span data-stu-id="55a91-141">**INSERT OVERWRITE ... SELECT**: Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>

     <span data-ttu-id="55a91-142">tooverify die alleen rijen die bevatten **[fout]** in kolom t4 waren opgeslagen toohello **foutenlogboeken** tabel, gebruikt u na de instructie tooreturn alle rijen uit Hallo Hallo **foutenlogboeken**:</span><span class="sxs-lookup"><span data-stu-id="55a91-142">tooverify that only rows that contain **[ERROR]** in column t4 were stored toohello **errorLogs** table, use hello following statement tooreturn all hello rows from **errorLogs**:</span></span>

       <span data-ttu-id="55a91-143">Selecteer * uit foutenlogboeken;</span><span class="sxs-lookup"><span data-stu-id="55a91-143">SELECT * from errorLogs;</span></span>

     <span data-ttu-id="55a91-144">Drie rijen met gegevens moeten worden geretourneerd, alle overkoepelende **[fout]** in kolom t4.</span><span class="sxs-lookup"><span data-stu-id="55a91-144">Three rows of data should be returned, all containing **[ERROR]** in column t4.</span></span>

## <span data-ttu-id="55a91-145"><a id="summary"></a>Samenvatting</span><span class="sxs-lookup"><span data-stu-id="55a91-145"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="55a91-146">Zoals u ziet, Hallo Hallo Hive opdracht biedt een eenvoudige manier toointeractively Hive-query's uitvoeren op een HDInsight-cluster, Hallo monitor status van taken en Hallo uitvoer ophalen.</span><span class="sxs-lookup"><span data-stu-id="55a91-146">As you can see, hello hello Hive command provides an easy way toointeractively run Hive queries on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="55a91-147"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="55a91-147"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="55a91-148">Voor algemene informatie over Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="55a91-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="55a91-149">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="55a91-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="55a91-150">Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="55a91-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="55a91-151">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="55a91-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="55a91-152">MapReduce gebruiken met Hadoop op HDInsight</span><span class="sxs-lookup"><span data-stu-id="55a91-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="55a91-153">Als u van Tez met Hive gebruikmaakt, raadpleegt u Hallo volgende documenten voor het opsporen van informatie:</span><span class="sxs-lookup"><span data-stu-id="55a91-153">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="55a91-154">Hallo Tez UI op HDInsight op basis van Windows gebruiken</span><span class="sxs-lookup"><span data-stu-id="55a91-154">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="55a91-155">Hallo Ambari Tez weergave op Linux gebaseerde HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="55a91-155">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

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





[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
