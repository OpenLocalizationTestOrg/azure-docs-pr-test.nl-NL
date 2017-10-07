---
title: aaaUse Hadoop Hive op Hallo Query-Console in de HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe toouse Hallo webgebaseerde Console Query toorun Hive-query's op een HDInsight Hadoop-cluster van uw browser.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5ae074b0-f55e-472d-94a7-005b0e79f779
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 621882082c9a07655d34b8dc980b8e47dd04b745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-query-console"></a><span data-ttu-id="97ffc-103">Uitvoeren van Hive-query's met behulp van Hallo Query-Console</span><span class="sxs-lookup"><span data-stu-id="97ffc-103">Run Hive queries using hello Query Console</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="97ffc-104">In dit artikel leert u hoe toouse hello HDInsight Query Console toorun Hive-query's op een HDInsight Hadoop-cluster van uw browser.</span><span class="sxs-lookup"><span data-stu-id="97ffc-104">In this article, you will learn how toouse hello HDInsight Query Console toorun Hive queries on an HDInsight Hadoop cluster from your browser.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="97ffc-105">Hallo HDInsight Query-Console is alleen beschikbaar op Windows gebaseerde HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="97ffc-105">hello HDInsight Query Console is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="97ffc-106">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="97ffc-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="97ffc-107">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="97ffc-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="97ffc-108">Voor HDInsight 3.4 of hoger, Zie [uitvoeren Hive-query's in de Ambari Hive-weergave](hdinsight-hadoop-use-hive-ambari-view.md) voor informatie over het uitvoeren van Hive-query's vanuit een webbrowser.</span><span class="sxs-lookup"><span data-stu-id="97ffc-108">For HDInsight 3.4 or greater, see [Run Hive queries in Ambari Hive View](hdinsight-hadoop-use-hive-ambari-view.md) for information on running Hive queries from a web browser.</span></span>

## <span data-ttu-id="97ffc-109"><a id="prereq"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="97ffc-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="97ffc-110">toocomplete hello stappen in dit artikel, moet u de volgende Hallo.</span><span class="sxs-lookup"><span data-stu-id="97ffc-110">toocomplete hello steps in this article, you will need hello following.</span></span>

* <span data-ttu-id="97ffc-111">Een HDInsight Hadoop op basis van Windows-cluster</span><span class="sxs-lookup"><span data-stu-id="97ffc-111">A Windows-based HDInsight Hadoop cluster</span></span>
* <span data-ttu-id="97ffc-112">Een moderne webbrowser</span><span class="sxs-lookup"><span data-stu-id="97ffc-112">A modern web browser</span></span>

## <span data-ttu-id="97ffc-113"><a id="run"></a>Uitvoeren van Hive-query's met behulp van Hallo Query-Console</span><span class="sxs-lookup"><span data-stu-id="97ffc-113"><a id="run"></a> Run Hive queries using hello Query Console</span></span>
1. <span data-ttu-id="97ffc-114">Open een webbrowser en navigeer te**https://CLUSTERNAME.azurehdinsight.net**, waarbij **CLUSTERNAME** Hallo-naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="97ffc-114">Open a web browser and navigate too**https://CLUSTERNAME.azurehdinsight.net**, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span> <span data-ttu-id="97ffc-115">Als u wordt gevraagd, voert u Hallo-gebruikersnaam en wachtwoord die u hebt gebruikt toen u Hallo cluster hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="97ffc-115">If prompted, enter hello user name and password that you used when you created hello cluster.</span></span>
2. <span data-ttu-id="97ffc-116">Hallo-koppelingen bovenaan Hallo Hallo pagina, selecteer **Hive-Editor**.</span><span class="sxs-lookup"><span data-stu-id="97ffc-116">From hello links at hello top of hello page, select **Hive Editor**.</span></span> <span data-ttu-id="97ffc-117">U ziet nu een formulier dat gebruikt tooenter hello HiveQL-instructies worden kan die u wilt dat toorun in Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="97ffc-117">This displays a form that can be used tooenter hello HiveQL statements that you want toorun in hello HDInsight cluster.</span></span>

    ![Hallo hive-editor](./media/hdinsight-hadoop-use-hive-query-console/queryconsole.png)

    <span data-ttu-id="97ffc-119">Vervang de tekst hello `Select * from hivesampletable` Hello HiveQL-instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="97ffc-119">Replace hello text `Select * from hivesampletable` with hello following HiveQL statements:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="97ffc-120">Deze instructies uitvoeren Hallo volgende acties:</span><span class="sxs-lookup"><span data-stu-id="97ffc-120">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="97ffc-121">**DROP TABLE**: Hiermee verwijdert u Hallo tabel en het Hallo-gegevensbestand als Hallo tabel al bestaat.</span><span class="sxs-lookup"><span data-stu-id="97ffc-121">**DROP TABLE**: Deletes hello table and hello data file if hello table already exists.</span></span>
   * <span data-ttu-id="97ffc-122">**EXTERNE tabel maken**: maakt een nieuwe 'extern' tabel in Hive.</span><span class="sxs-lookup"><span data-stu-id="97ffc-122">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="97ffc-123">Externe tabellen opslaan alleen Hallo tabeldefinitie in Hive; Hallo-gegevens in de oorspronkelijke locatie Hallo gelaten.</span><span class="sxs-lookup"><span data-stu-id="97ffc-123">External tables store only hello table definition in Hive; hello data is left in hello original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="97ffc-124">Externe tabellen moeten worden gebruikt wanneer u gegevens toobe worden bijgewerkt door een externe bron (zoals een uploadproces geautomatiseerde gegevens) of door een andere MapReduce-bewerking onderliggende hello verwacht, maar u wilt dat altijd Hive query toouse Hallo meest recente gegevens.</span><span class="sxs-lookup"><span data-stu-id="97ffc-124">External tables should be used when you expect hello underlying data toobe updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries toouse hello latest data.</span></span>
     >
     > <span data-ttu-id="97ffc-125">Verwijderen van een externe tabel komt **niet** Hallo gegevens alleen Hallo tabeldefinitie kunt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="97ffc-125">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>
     >
     >
   * <span data-ttu-id="97ffc-126">**INDELING van de rij**: Hive-wordt uitgelegd hoe Hallo gegevens wordt opgemaakt.</span><span class="sxs-lookup"><span data-stu-id="97ffc-126">**ROW FORMAT**: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="97ffc-127">In dit geval worden Hallo velden in elk logboek gescheiden door een spatie.</span><span class="sxs-lookup"><span data-stu-id="97ffc-127">In this case, hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="97ffc-128">**AS TEXTFILE locatie opgeslagen**: vertelt Hive waar Hallo gegevens zijn opgeslagen (directory Hallo bijvoorbeeld/gegevens) en deze is opgeslagen als tekst</span><span class="sxs-lookup"><span data-stu-id="97ffc-128">**STORED AS TEXTFILE LOCATION**: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text</span></span>
   * <span data-ttu-id="97ffc-129">**Selecteer**: Selecteer een telling van alle rijen waarin kolom **t4** Hallo waarde bevatten **[fout]**.</span><span class="sxs-lookup"><span data-stu-id="97ffc-129">**SELECT**: Select a count of all rows where column **t4** contain hello value **[ERROR]**.</span></span> <span data-ttu-id="97ffc-130">Dit moet een waarde van retourneren **3** omdat er drie rijen met deze waarde.</span><span class="sxs-lookup"><span data-stu-id="97ffc-130">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="97ffc-131">**INPUT__FILE__NAME zoals '%.log'** -vertelt Hive die we alleen gegevens uit bestanden eindigt op moet retourneren. log.</span><span class="sxs-lookup"><span data-stu-id="97ffc-131">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="97ffc-132">Hiermee beperkt u Hallo zoeken toohello sample.log-bestand dat Hallo gegevens bevat, en voorkomt dat het retourneren van gegevens uit andere voorbeeld gegevensbestanden die komen niet overeen met de Hallo-schema die is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="97ffc-132">This restricts hello search toohello sample.log file that contains hello data, and keeps it from returning data from other example data files that do not match hello schema we defined.</span></span>
3. <span data-ttu-id="97ffc-133">Klik op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="97ffc-133">Click **Submit**.</span></span> <span data-ttu-id="97ffc-134">Hallo **taak sessie** op Hallo onderaan Hallo pagina details voor Hallo-taak moet worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="97ffc-134">hello **Job Session** at hello bottom of hello page should display details for hello job.</span></span>
4. <span data-ttu-id="97ffc-135">Wanneer Hallo **Status** wijzigingen te veld**voltooid**, selecteer **Details weergeven** voor Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="97ffc-135">When hello **Status** field changes too**Completed**, select **View Details** for hello job.</span></span> <span data-ttu-id="97ffc-136">Op de pagina met details Hallo Hallo **Taakuitvoer** bevat `[ERROR]    3`.</span><span class="sxs-lookup"><span data-stu-id="97ffc-136">On hello details page, hello **Job Output** contains `[ERROR]    3`.</span></span> <span data-ttu-id="97ffc-137">U kunt Hallo **downloaden** knop onder deze toodownload veld van een bestand met de Hallo-uitvoer van Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="97ffc-137">You can use hello **Download** button under this field toodownload a file that contains hello output of hello job.</span></span>

## <span data-ttu-id="97ffc-138"><a id="summary"></a>Samenvatting</span><span class="sxs-lookup"><span data-stu-id="97ffc-138"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="97ffc-139">Zoals u ziet, Hive query's in een HDInsight-cluster Hallo Query-Console biedt een eenvoudige manier toorun Hallo taakstatus controleren en Hallo uitvoer ophalen.</span><span class="sxs-lookup"><span data-stu-id="97ffc-139">As you can see, hello Query Console provides an easy way toorun Hive queries in an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

<span data-ttu-id="97ffc-140">Selecteer toolearn meer over het gebruik van Hive-Query Console toorun Hive-taken **aan de slag** bovenaan Hallo Hallo Query-Console, gebruik vervolgens Hallo voorbeelden die worden geleverd.</span><span class="sxs-lookup"><span data-stu-id="97ffc-140">toolearn more about using Hive Query Console toorun Hive jobs, select **Getting Started** at hello top of hello Query Console, then use hello samples that are provided.</span></span> <span data-ttu-id="97ffc-141">Elke steekproef begeleidt bij Hallo proces van het gebruik van Hive tooanalyze gegevens, inclusief uitleg over Hallo HiveQL-instructies in het Hallo-voorbeeld gebruikt.</span><span class="sxs-lookup"><span data-stu-id="97ffc-141">Each sample walks through hello process of using Hive tooanalyze data, including explanations about hello HiveQL statements used in hello sample.</span></span>

## <span data-ttu-id="97ffc-142"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="97ffc-142"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="97ffc-143">Voor algemene informatie over Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="97ffc-143">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="97ffc-144">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="97ffc-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="97ffc-145">Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="97ffc-145">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="97ffc-146">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="97ffc-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="97ffc-147">MapReduce gebruiken met Hadoop op HDInsight</span><span class="sxs-lookup"><span data-stu-id="97ffc-147">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="97ffc-148">Als u van Tez met Hive gebruikmaakt, raadpleegt u Hallo volgende documenten voor het opsporen van informatie:</span><span class="sxs-lookup"><span data-stu-id="97ffc-148">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="97ffc-149">Hallo Tez UI op HDInsight op basis van Windows gebruiken</span><span class="sxs-lookup"><span data-stu-id="97ffc-149">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="97ffc-150">Hallo Ambari Tez weergave op Linux gebaseerde HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="97ffc-150">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
