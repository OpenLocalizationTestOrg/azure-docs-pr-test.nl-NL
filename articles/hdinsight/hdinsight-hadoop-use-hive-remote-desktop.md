---
title: Hadoop Hive en extern bureaublad gebruiken in HDInsight - Azure | Microsoft Docs
description: Informatie over het verbinden met Hadoop-cluster in HDInsight met behulp van extern bureaublad en voer de Hive-query's via de opdrachtregelinterface Hive.
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
ms.openlocfilehash: 187c7cb413b3707e58eea387857375053d267189
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="79e3e-103">Hive gebruiken met Hadoop op HDInsight met extern bureaublad</span><span class="sxs-lookup"><span data-stu-id="79e3e-103">Use Hive with Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="79e3e-104">In dit artikel hebt u meer informatie over het verbinding maken met een HDInsight-cluster met behulp van extern bureaublad, en vervolgens Hive-query's uitvoeren met Hive-opdrachtregelinterface (CLI).</span><span class="sxs-lookup"><span data-stu-id="79e3e-104">In this article, you will learn how to connect to an HDInsight cluster by using Remote Desktop, and then run Hive queries by using the Hive Command-Line Interface (CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="79e3e-105">Extern bureaublad is alleen beschikbaar op HDInsight-clusters die Windows als het besturingssysteem gebruiken.</span><span class="sxs-lookup"><span data-stu-id="79e3e-105">Remote Desktop is only available on HDInsight clusters that use Windows as the operating system.</span></span> <span data-ttu-id="79e3e-106">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="79e3e-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="79e3e-107">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="79e3e-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="79e3e-108">Voor HDInsight 3.4 of hoger, Zie [Hive gebruiken met HDInsight en Beeline](hdinsight-hadoop-use-hive-beeline.md) voor informatie over het uitvoeren van Hive-query's op het cluster rechtstreeks vanaf een opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="79e3e-108">For HDInsight 3.4 or greater, see [Use Hive with HDInsight and Beeline](hdinsight-hadoop-use-hive-beeline.md) for information on running Hive queries directly on the cluster from a command-line.</span></span>

## <span data-ttu-id="79e3e-109"><a id="prereq"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="79e3e-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="79e3e-110">Voor het voltooien van de stappen in dit artikel, moet u het volgende:</span><span class="sxs-lookup"><span data-stu-id="79e3e-110">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="79e3e-111">Een cluster op basis van Windows HDInsight (Hadoop in HDInsight)</span><span class="sxs-lookup"><span data-stu-id="79e3e-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="79e3e-112">Een clientcomputer met Windows 10, Windows 8 of Windows 7</span><span class="sxs-lookup"><span data-stu-id="79e3e-112">A client computer running Windows 10, Window 8, or Windows 7</span></span>

## <span data-ttu-id="79e3e-113"><a id="connect"></a>Verbinding maken met extern bureaublad</span><span class="sxs-lookup"><span data-stu-id="79e3e-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="79e3e-114">Extern bureaublad inschakelen voor het HDInsight-cluster en vervolgens verbinding maken met het door de instructies op [verbinding maken met HDInsight-clusters met RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="79e3e-114">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="79e3e-115"><a id="hive"></a>Gebruik de opdracht Hive</span><span class="sxs-lookup"><span data-stu-id="79e3e-115"><a id="hive"></a>Use the Hive command</span></span>
<span data-ttu-id="79e3e-116">Wanneer u verbinding hebt met het bureaublad voor het HDInsight-cluster, gebruik de volgende stappen uit om te werken met Hive:</span><span class="sxs-lookup"><span data-stu-id="79e3e-116">When you have connected to the desktop for the HDInsight cluster, use the following steps to work with Hive:</span></span>

1. <span data-ttu-id="79e3e-117">Start vanaf het bureaublad HDInsight de **Hadoop-opdrachtregel**.</span><span class="sxs-lookup"><span data-stu-id="79e3e-117">From the HDInsight desktop, start the **Hadoop Command Line**.</span></span>
2. <span data-ttu-id="79e3e-118">Voer de volgende opdracht om de CLI Hive starten:</span><span class="sxs-lookup"><span data-stu-id="79e3e-118">Enter the following command to start the Hive CLI:</span></span>

        %hive_home%\bin\hive

    <span data-ttu-id="79e3e-119">Als de CLI is gestart, ziet u de CLI Hive-prompt: `hive>`.</span><span class="sxs-lookup"><span data-stu-id="79e3e-119">When the CLI has started, you will see the Hive CLI prompt: `hive>`.</span></span>
3. <span data-ttu-id="79e3e-120">De volgende instructies om een nieuwe tabel met de naam te maken met behulp van de CLI Voer **log4jLogs** voorbeeldgegevens gebruikt:</span><span class="sxs-lookup"><span data-stu-id="79e3e-120">Using the CLI, enter the following statements to create a new table named **log4jLogs** using sample data:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="79e3e-121">Deze instructies uitvoeren de volgende acties:</span><span class="sxs-lookup"><span data-stu-id="79e3e-121">These statements perform the following actions:</span></span>

   * <span data-ttu-id="79e3e-122">**DROP TABLE**: Hiermee verwijdert u de tabel en het gegevensbestand als de tabel al bestaat.</span><span class="sxs-lookup"><span data-stu-id="79e3e-122">**DROP TABLE**: Deletes the table and the data file if the table already exists.</span></span>
   * <span data-ttu-id="79e3e-123">**EXTERNE tabel maken**: maakt een nieuwe 'extern' tabel in Hive.</span><span class="sxs-lookup"><span data-stu-id="79e3e-123">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="79e3e-124">De definitie van de tabel opslaan externe tabellen in Hive (de gegevens links op de oorspronkelijke locatie).</span><span class="sxs-lookup"><span data-stu-id="79e3e-124">External tables store only the table definition in Hive (the data is left in the original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="79e3e-125">Externe tabellen moeten worden gebruikt wanneer u de onderliggende gegevens worden bijgewerkt door een externe bron (zoals een uploadproces geautomatiseerde gegevens) of door een andere MapReduce-bewerking verwacht, maar u wilt dat altijd de meest recente gegevens gebruiken voor Hive-query's.</span><span class="sxs-lookup"><span data-stu-id="79e3e-125">External tables should be used when you expect the underlying data to be updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries to use the latest data.</span></span>
     >
     > <span data-ttu-id="79e3e-126">Verwijderen van een externe tabel komt **niet** de gegevens, de definitie van de tabel verwijderen.</span><span class="sxs-lookup"><span data-stu-id="79e3e-126">Dropping an external table does **not** delete the data, only the table definition.</span></span>
     >
     >
   * <span data-ttu-id="79e3e-127">**INDELING van de rij**: Hive-wordt uitgelegd hoe de gegevens wordt opgemaakt.</span><span class="sxs-lookup"><span data-stu-id="79e3e-127">**ROW FORMAT**: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="79e3e-128">In dit geval worden de velden in elk logboek gescheiden door een spatie.</span><span class="sxs-lookup"><span data-stu-id="79e3e-128">In this case, the fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="79e3e-129">**AS TEXTFILE locatie opgeslagen**: vertelt Hive waar de gegevens zijn opgeslagen (de map met de voorbeeldgegevens /) en deze is opgeslagen als tekst.</span><span class="sxs-lookup"><span data-stu-id="79e3e-129">**STORED AS TEXTFILE LOCATION**: Tells Hive where the data is stored (the example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="79e3e-130">**Selecteer**: selecteert een telling van alle rijen waarin kolom **t4** bevat de waarde **[fout]**.</span><span class="sxs-lookup"><span data-stu-id="79e3e-130">**SELECT**: Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="79e3e-131">Dit moet een waarde van retourneren **3** omdat er drie rijen met deze waarde.</span><span class="sxs-lookup"><span data-stu-id="79e3e-131">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="79e3e-132">**INPUT__FILE__NAME zoals '%.log'** -vertelt Hive die we alleen gegevens uit bestanden eindigt op moet retourneren. log.</span><span class="sxs-lookup"><span data-stu-id="79e3e-132">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="79e3e-133">Dit beperkt de zoekopdracht tot het sample.log-bestand dat de gegevens bevat, en voorkomt dat het retourneren van gegevens uit andere voorbeeld gegevensbestanden die komen niet overeen met het schema dat is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="79e3e-133">This restricts the search to the sample.log file that contains the data, and keeps it from returning data from other example data files that do not match the schema we defined.</span></span>
4. <span data-ttu-id="79e3e-134">Gebruik de volgende instructies voor het maken van een nieuwe 'interne' tabel met de naam **foutenlogboeken**:</span><span class="sxs-lookup"><span data-stu-id="79e3e-134">Use the following statements to create a new 'internal' table named **errorLogs**:</span></span>

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    <span data-ttu-id="79e3e-135">Deze instructies uitvoeren de volgende acties:</span><span class="sxs-lookup"><span data-stu-id="79e3e-135">These statements perform the following actions:</span></span>

   * <span data-ttu-id="79e3e-136">**MAKEN van tabel als niet bestaat**: maakt een tabel als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="79e3e-136">**CREATE TABLE IF NOT EXISTS**: Creates a table if it does not already exist.</span></span> <span data-ttu-id="79e3e-137">Omdat de **externe** trefwoord wordt niet gebruikt, is dit een interne tabel die is opgeslagen in het datawarehouse Hive en volledig wordt beheerd door Hive.</span><span class="sxs-lookup"><span data-stu-id="79e3e-137">Because the **EXTERNAL** keyword is not used, this is an internal table, which is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="79e3e-138">In tegenstelling tot **externe** tabellen, ook verwijderen van een interne tabel worden de onderliggende gegevens verwijderd.</span><span class="sxs-lookup"><span data-stu-id="79e3e-138">Unlike **EXTERNAL** tables, dropping an internal table also deletes the underlying data.</span></span>
     >
     >
   * <span data-ttu-id="79e3e-139">**OPGESLAGEN AS ORC**: de gegevens opslaat in geoptimaliseerde rij kolomindeling (ORC).</span><span class="sxs-lookup"><span data-stu-id="79e3e-139">**STORED AS ORC**: Stores the data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="79e3e-140">Dit is een maximaal geoptimaliseerd en efficiënte indeling voor het opslaan van gegevens met Hive.</span><span class="sxs-lookup"><span data-stu-id="79e3e-140">This is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="79e3e-141">**INSERT OVERSCHRIJVEN... Selecteer**: selecteert rijen uit de **log4jLogs** tabel met **[fout]**, voegt u vervolgens de gegevens in de **foutenlogboeken** tabel.</span><span class="sxs-lookup"><span data-stu-id="79e3e-141">**INSERT OVERWRITE ... SELECT**: Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span></span>

     <span data-ttu-id="79e3e-142">Om te controleren dat die bevatten alleen rijen **[fout]** in kolom t4 zijn opgeslagen op de **foutenlogboeken** tabel, met de volgende instructie retourneert alle rijen uit **foutenlogboeken**:</span><span class="sxs-lookup"><span data-stu-id="79e3e-142">To verify that only rows that contain **[ERROR]** in column t4 were stored to the **errorLogs** table, use the following statement to return all the rows from **errorLogs**:</span></span>

       <span data-ttu-id="79e3e-143">Selecteer * uit foutenlogboeken;</span><span class="sxs-lookup"><span data-stu-id="79e3e-143">SELECT * from errorLogs;</span></span>

     <span data-ttu-id="79e3e-144">Drie rijen met gegevens moeten worden geretourneerd, alle overkoepelende **[fout]** in kolom t4.</span><span class="sxs-lookup"><span data-stu-id="79e3e-144">Three rows of data should be returned, all containing **[ERROR]** in column t4.</span></span>

## <span data-ttu-id="79e3e-145"><a id="summary"></a>Samenvatting</span><span class="sxs-lookup"><span data-stu-id="79e3e-145"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="79e3e-146">Zoals u ziet de de Hive-opdracht biedt een eenvoudige manier om interactief Hive-query's uitvoeren op een HDInsight-cluster, de taakstatus te controleren en ophalen van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="79e3e-146">As you can see, the the Hive command provides an easy way to interactively run Hive queries on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="79e3e-147"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="79e3e-147"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="79e3e-148">Voor algemene informatie over Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="79e3e-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="79e3e-149">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="79e3e-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="79e3e-150">Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="79e3e-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="79e3e-151">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="79e3e-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="79e3e-152">MapReduce gebruiken met Hadoop op HDInsight</span><span class="sxs-lookup"><span data-stu-id="79e3e-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="79e3e-153">Als u van Tez met Hive gebruikmaakt, raadpleegt u de volgende documenten voor het opsporen van informatie:</span><span class="sxs-lookup"><span data-stu-id="79e3e-153">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="79e3e-154">De Tez-gebruikersinterface op HDInsight op basis van Windows gebruiken</span><span class="sxs-lookup"><span data-stu-id="79e3e-154">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="79e3e-155">De weergave Ambari Tez op Linux gebaseerde HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="79e3e-155">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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
