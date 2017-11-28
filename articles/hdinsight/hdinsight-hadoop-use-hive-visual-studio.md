---
title: aaaHive met (Hadoop) van Data Lake tools voor Visual Studio - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse Hallo Data Lake tools voor Visual Studio toorun Apache Hive-query's met Apache Hadoop op Azure HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2b3e672a-1195-4fa5-afb7-b7b73937bfbe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: dc76974c02cf68bcf701b2b155842c9e9c5cb988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-data-lake-tools-for-visual-studio"></a><span data-ttu-id="8810a-103">Uitvoeren van Hive-query's met Hallo Data Lake tools voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8810a-103">Run Hive queries using hello Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="8810a-104">Meer informatie over hoe toouse Hallo Data Lake tools voor Visual Studio tooquery Apache Hive.</span><span class="sxs-lookup"><span data-stu-id="8810a-104">Learn how toouse hello Data Lake tools for Visual Studio tooquery Apache Hive.</span></span> <span data-ttu-id="8810a-105">Hallo Data Lake-hulpprogramma's kunt u tooeasily maken, te verzenden en te bewaken tooHadoop voor Hive-query's in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8810a-105">hello Data Lake tools allow you tooeasily create, submit, and monitor Hive queries tooHadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="8810a-106"><a id="prereq"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="8810a-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="8810a-107">Een Azure HDInsight (Hadoop in HDInsight)-cluster</span><span class="sxs-lookup"><span data-stu-id="8810a-107">An Azure HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="8810a-108">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="8810a-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="8810a-109">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8810a-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="8810a-110">Visual Studio (een van de volgende versies Hallo):</span><span class="sxs-lookup"><span data-stu-id="8810a-110">Visual Studio (one of hello following versions):</span></span>

    * <span data-ttu-id="8810a-111">Visual Studio 2013 Community/Professional/Premium/Ultimate met Update 4</span><span class="sxs-lookup"><span data-stu-id="8810a-111">Visual Studio 2013 Community/Professional/Premium/Ultimate with Update 4</span></span>

    * <span data-ttu-id="8810a-112">Visual Studio 2015 (alle versies)</span><span class="sxs-lookup"><span data-stu-id="8810a-112">Visual Studio 2015 (any edition)</span></span>

    * <span data-ttu-id="8810a-113">Visual Studio 2017 (alle versies)</span><span class="sxs-lookup"><span data-stu-id="8810a-113">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="8810a-114">HDInsight tools voor Visual Studio of Azure Data Lake tools voor Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8810a-114">HDInsight tools for Visual Studio or Azure Data Lake tools for Visual Studio.</span></span> <span data-ttu-id="8810a-115">Zie [aan de slag met Visual Studio Hadoop-hulpprogramma's voor HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) voor informatie over het installeren en configureren van Hallo's.</span><span class="sxs-lookup"><span data-stu-id="8810a-115">See [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installing and configuring hello tools.</span></span>

## <span data-ttu-id="8810a-116"><a id="run"></a>Uitvoeren van Hive-query's met behulp van Visual Studio Hallo</span><span class="sxs-lookup"><span data-stu-id="8810a-116"><a id="run"></a> Run Hive queries using hello Visual Studio</span></span>

1. <span data-ttu-id="8810a-117">Open **Visual Studio** en selecteer **nieuw** > **Project** > **Azure Data Lake** > **HIVE** > **Hive-toepassing**.</span><span class="sxs-lookup"><span data-stu-id="8810a-117">Open **Visual Studio** and select **New** > **Project** > **Azure Data Lake** > **HIVE** > **Hive Application**.</span></span> <span data-ttu-id="8810a-118">Geef een naam voor dit project.</span><span class="sxs-lookup"><span data-stu-id="8810a-118">Provide a name for this project.</span></span>

2. <span data-ttu-id="8810a-119">Open Hallo **Script.hql** -bestand dat is gemaakt met dit project en plakken in Hallo HiveQL-instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="8810a-119">Open hello **Script.hql** file that is created with this project, and paste in hello following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    <span data-ttu-id="8810a-120">Deze instructies uitvoeren Hallo volgende acties:</span><span class="sxs-lookup"><span data-stu-id="8810a-120">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="8810a-121">`DROP TABLE`: Als Hallo tabel bestaat, wordt het door deze instructie verwijdert.</span><span class="sxs-lookup"><span data-stu-id="8810a-121">`DROP TABLE`: If hello table exists, this statement deletes it.</span></span>

   * <span data-ttu-id="8810a-122">`CREATE EXTERNAL TABLE`: Maakt een nieuwe tabel 'extern' in Hive.</span><span class="sxs-lookup"><span data-stu-id="8810a-122">`CREATE EXTERNAL TABLE`: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="8810a-123">De tabeldefinitie Hallo opslaan externe tabellen alleen in Hive (hello gegevens in de oorspronkelijke locatie Hallo blijft).</span><span class="sxs-lookup"><span data-stu-id="8810a-123">External tables only store hello table definition in Hive (hello data is left in hello original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="8810a-124">Externe tabellen moeten worden gebruikt wanneer u van plan Hallo onderliggende gegevens toobe bijgewerkt door een externe bron bent.</span><span class="sxs-lookup"><span data-stu-id="8810a-124">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="8810a-125">Bijvoorbeeld, een MapReduce-taak of een Azure-service.</span><span class="sxs-lookup"><span data-stu-id="8810a-125">For example, a MapReduce job or Azure service.</span></span>
     >
     > <span data-ttu-id="8810a-126">Verwijderen van een externe tabel komt **niet** Hallo gegevens alleen Hallo tabeldefinitie kunt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="8810a-126">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

   * <span data-ttu-id="8810a-127">`ROW FORMAT`: Hiermee geeft u Hive hoe Hallo gegevens wordt opgemaakt.</span><span class="sxs-lookup"><span data-stu-id="8810a-127">`ROW FORMAT`: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="8810a-128">In dit geval worden Hallo velden in elk logboek gescheiden door een spatie.</span><span class="sxs-lookup"><span data-stu-id="8810a-128">In this case, hello fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="8810a-129">`STORED AS TEXTFILE LOCATION`: Vertelt Hive waar hello gegevens worden opgeslagen (directory Hallo bijvoorbeeld/gegevens) en dat deze is opgeslagen als tekst.</span><span class="sxs-lookup"><span data-stu-id="8810a-129">`STORED AS TEXTFILE LOCATION`: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>

   * <span data-ttu-id="8810a-130">`SELECT`: Selecteer een telling van alle rijen waarin kolom `t4` Hallo waarde bevat `[ERROR]`.</span><span class="sxs-lookup"><span data-stu-id="8810a-130">`SELECT`: Select a count of all rows where column `t4` contains hello value `[ERROR]`.</span></span> <span data-ttu-id="8810a-131">Deze instructie retourneert een waarde van `3` omdat er drie rijen met deze waarde.</span><span class="sxs-lookup"><span data-stu-id="8810a-131">This statement returns a value of `3` because there are three rows that contain this value.</span></span>

   * <span data-ttu-id="8810a-132">`INPUT__FILE__NAME LIKE '%.log'`-Vertelt Hive dat we alleen gegevens uit bestanden eindigt op moet retourneren. log.</span><span class="sxs-lookup"><span data-stu-id="8810a-132">`INPUT__FILE__NAME LIKE '%.log'` - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="8810a-133">Deze component beperkt Hallo search toohello sample.log bestand die Hallo gegevens bevat.</span><span class="sxs-lookup"><span data-stu-id="8810a-133">This clause restricts hello search toohello sample.log file that contains hello data.</span></span>

3. <span data-ttu-id="8810a-134">Selecteer in de werkbalk Hallo Hallo **HDInsight-Cluster** wilt u toouse voor deze query.</span><span class="sxs-lookup"><span data-stu-id="8810a-134">From hello toolbar, select hello **HDInsight Cluster** that you want toouse for this query.</span></span> <span data-ttu-id="8810a-135">Selecteer **indienen** toorun Hallo instructies als een Hive-taak.</span><span class="sxs-lookup"><span data-stu-id="8810a-135">Select **Submit** toorun hello statements as a Hive job.</span></span>

   ![Indienings-balk](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. <span data-ttu-id="8810a-137">Hallo **taakoverzicht Hive** wordt weergegeven en geeft informatie weer over Hallo taak uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="8810a-137">hello **Hive Job Summary** appears and displays information about hello running job.</span></span> <span data-ttu-id="8810a-138">Gebruik Hallo **vernieuwen** toorefresh Hallo taakgegevens tot Hallo koppelen **taakstatus** wijzigingen te**voltooid**.</span><span class="sxs-lookup"><span data-stu-id="8810a-138">Use hello **Refresh** link toorefresh hello job information, until hello **Job Status** changes too**Completed**.</span></span>

   ![Taakoverzicht een voltooide taak weergeven](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. <span data-ttu-id="8810a-140">Gebruik Hallo **Taakuitvoer** tooview Hallo uitvoer van deze taak te koppelen.</span><span class="sxs-lookup"><span data-stu-id="8810a-140">Use hello **Job Output** link tooview hello output of this job.</span></span> <span data-ttu-id="8810a-141">Hiermee wordt weergegeven `[ERROR] 3`, dit is Hallo-waarde geretourneerd door deze query.</span><span class="sxs-lookup"><span data-stu-id="8810a-141">It displays `[ERROR] 3`, which is hello value returned by this query.</span></span>

6. <span data-ttu-id="8810a-142">U kunt ook Hive-query's uitvoeren zonder een project maken.</span><span class="sxs-lookup"><span data-stu-id="8810a-142">You can also run Hive queries without creating a project.</span></span> <span data-ttu-id="8810a-143">Met behulp van **Server Explorer**, vouw **Azure** > **HDInsight**, met de rechtermuisknop op uw HDInsight-server en selecteer vervolgens **een Hive-Query schrijven**.</span><span class="sxs-lookup"><span data-stu-id="8810a-143">Using **Server Explorer**, expand **Azure** > **HDInsight**, right-click your HDInsight server, and then select **Write a Hive Query**.</span></span>

7. <span data-ttu-id="8810a-144">In Hallo **temp.hql** document dat wordt weergegeven, toevoegen Hallo HiveQL-instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="8810a-144">In hello **temp.hql** document that appears, add hello following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    <span data-ttu-id="8810a-145">Deze instructies uitvoeren Hallo volgende acties:</span><span class="sxs-lookup"><span data-stu-id="8810a-145">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="8810a-146">`CREATE TABLE IF NOT EXISTS`: Een tabel gemaakt als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="8810a-146">`CREATE TABLE IF NOT EXISTS`: Creates a table if it does not already exist.</span></span> <span data-ttu-id="8810a-147">Omdat Hallo `EXTERNAL` trefwoord wordt niet gebruikt, wordt deze instructie maakt u een interne tabel.</span><span class="sxs-lookup"><span data-stu-id="8810a-147">Because hello `EXTERNAL` keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="8810a-148">Interne tabellen worden opgeslagen in Hallo Hive-datawarehouse en worden beheerd door Hive.</span><span class="sxs-lookup"><span data-stu-id="8810a-148">Internal tables are stored in hello Hive data warehouse and are managed by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="8810a-149">In tegenstelling tot `EXTERNAL` tabellen, verwijderen van een interne tabel ook Hallo onderliggende gegevens worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="8810a-149">Unlike `EXTERNAL` tables, dropping an internal table also deletes hello underlying data.</span></span>

   * <span data-ttu-id="8810a-150">`STORED AS ORC`: Winkels Hallo gegevens in geoptimaliseerde rij kolomindeling (ORC).</span><span class="sxs-lookup"><span data-stu-id="8810a-150">`STORED AS ORC`: Stores hello data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="8810a-151">ORC is een maximaal geoptimaliseerd en efficiënte indeling voor het opslaan van gegevens met Hive.</span><span class="sxs-lookup"><span data-stu-id="8810a-151">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="8810a-152">`INSERT OVERWRITE ... SELECT`: Rijen uit Hallo geselecteerd `log4jLogs` tabel met `[ERROR]`, en vervolgens voegt gegevens in Hallo Hallo `errorLogs` tabel.</span><span class="sxs-lookup"><span data-stu-id="8810a-152">`INSERT OVERWRITE ... SELECT`: Selects rows from hello `log4jLogs` table that contain `[ERROR]`, then inserts hello data into hello `errorLogs` table.</span></span>

8. <span data-ttu-id="8810a-153">Selecteer in de werkbalk Hallo **indienen** toorun Hallo taak.</span><span class="sxs-lookup"><span data-stu-id="8810a-153">From hello toolbar, select **Submit** toorun hello job.</span></span> <span data-ttu-id="8810a-154">Gebruik Hallo **taakstatus** toodetermine die Hallo-taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="8810a-154">Use hello **Job Status** toodetermine that hello job has completed successfully.</span></span>

9. <span data-ttu-id="8810a-155">tooverify die Hallo Hallo tabel, gebruik gemaakte taak **Server Explorer** en vouw **Azure** > **HDInsight** > uw HDInsight-cluster > **Hive-Databases** > **standaard**.</span><span class="sxs-lookup"><span data-stu-id="8810a-155">tooverify that hello job created hello table, use **Server Explorer** and expand **Azure** > **HDInsight** > your HDInsight cluster > **Hive Databases** > **default**.</span></span> <span data-ttu-id="8810a-156">Hallo **foutenlogboeken** tabel en Hallo **log4jLogs** tabel worden vermeld.</span><span class="sxs-lookup"><span data-stu-id="8810a-156">hello **errorLogs** table and hello **log4jLogs** table are listed.</span></span>

## <span data-ttu-id="8810a-157"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8810a-157"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="8810a-158">Zoals u ziet, bieden Hallo HDInsight tools voor Visual Studio een eenvoudige manier toowork met Hive-query's op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8810a-158">As you can see, hello HDInsight tools for Visual Studio provide an easy way toowork with Hive queries on HDInsight.</span></span>

<span data-ttu-id="8810a-159">Voor algemene informatie over Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="8810a-159">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="8810a-160">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="8810a-160">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="8810a-161">Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="8810a-161">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="8810a-162">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="8810a-162">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

* [<span data-ttu-id="8810a-163">MapReduce gebruiken met Hadoop op HDInsight</span><span class="sxs-lookup"><span data-stu-id="8810a-163">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="8810a-164">Voor meer informatie over Hallo HDInsight tools voor Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="8810a-164">For more information about hello HDInsight tools for Visual Studio:</span></span>

* [<span data-ttu-id="8810a-165">Aan de slag met HDInsight tools voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8810a-165">Getting started with HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md)

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

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx

[image-hdi-hive-powershell]: ./media/hdinsight-use-hive/HDI.HIVE.PowerShell.png
[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
[image-hdi-hive-architecture]: ./media/hdinsight-use-hive/HDI.Hive.Architecture.png
