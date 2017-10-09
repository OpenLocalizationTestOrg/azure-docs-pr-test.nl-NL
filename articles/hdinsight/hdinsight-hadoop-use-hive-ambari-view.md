---
title: aaaUse Ambari-weergaven toowork met Hive in HDInsight (Hadoop) - Azure | Microsoft Docs
description: Meer informatie over hoe toouse Hive-weergave Hallo van uw web browser toosubmit Hive-query's. Hallo Hive-weergave maakt deel uit van Hallo die ambari-Webgebruikersinterface is voorzien van uw Linux gebaseerde HDInsight-cluster.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 1abe9104-f4b2-41b9-9161-abbc43de8294
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: f9a77b652e70d34a0ff9165fbb8c2e16d3401ae0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-hive-view-with-hadoop-in-hdinsight"></a><span data-ttu-id="9dc23-104">Hallo Hive-weergave gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="9dc23-104">Use hello Hive View with Hadoop in HDInsight</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="9dc23-105">Meer informatie over hoe toorun Hive van query's met Ambari Hive-weergave.</span><span class="sxs-lookup"><span data-stu-id="9dc23-105">Learn how toorun Hive queries using Ambari Hive View.</span></span> <span data-ttu-id="9dc23-106">Ambari is een beheer en controle hulpprogramma met HDInsight op basis van Linux-clusters.</span><span class="sxs-lookup"><span data-stu-id="9dc23-106">Ambari is a management and monitoring utility provided with Linux-based HDInsight clusters.</span></span> <span data-ttu-id="9dc23-107">Een van de Hallo functies via Ambari is een Webgebruikersinterface die gebruikte toorun Hive-query's kunnen worden.</span><span class="sxs-lookup"><span data-stu-id="9dc23-107">One of hello features provided through Ambari is a Web UI that can be used toorun Hive queries.</span></span>

> [!NOTE]
> <span data-ttu-id="9dc23-108">Ambari heeft veel mogelijkheden die niet in dit document worden besproken.</span><span class="sxs-lookup"><span data-stu-id="9dc23-108">Ambari has many capabilities that are not discussed in this document.</span></span> <span data-ttu-id="9dc23-109">Zie voor meer informatie [HDInsight-clusters beheren met behulp van Hallo Ambari-Webgebruikersinterface](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="9dc23-109">For more information, see [Manage HDInsight clusters by using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9dc23-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="9dc23-110">Prerequisites</span></span>

* <span data-ttu-id="9dc23-111">Een Linux gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="9dc23-111">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="9dc23-112">Zie voor meer informatie over het maken van de cluster [aan de slag met HDInsight op basis van Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9dc23-112">For information on creating cluster, see [Get started with Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9dc23-113">Hallo stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux.</span><span class="sxs-lookup"><span data-stu-id="9dc23-113">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="9dc23-114">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="9dc23-114">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9dc23-115">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="9dc23-115">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="open-hello-hive-view"></a><span data-ttu-id="9dc23-116">Open Hallo Hive-weergave</span><span class="sxs-lookup"><span data-stu-id="9dc23-116">Open hello Hive view</span></span>

<span data-ttu-id="9dc23-117">U kunt Ambari-weergaven van hello Azure-portal; Selecteer uw HDInsight-cluster en selecteer vervolgens **Ambari-weergaven** van Hallo **snelkoppelingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="9dc23-117">You can Ambari Views from hello Azure portal; select your HDInsight cluster and then select **Ambari Views** from hello **Quick Links** section.</span></span>

![sectie Snelle koppelingen van Hallo-portal](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

<span data-ttu-id="9dc23-119">Selecteer in de lijst van de Hallo van weergaven, Hallo __Hive-weergave__.</span><span class="sxs-lookup"><span data-stu-id="9dc23-119">From hello list of views, select hello __Hive View__.</span></span>

![Hallo Hive-weergave geselecteerd](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> <span data-ttu-id="9dc23-121">Bij het openen van Ambari zijn na vragen aan gebruiker tooauthenticate toohello site.</span><span class="sxs-lookup"><span data-stu-id="9dc23-121">When accessing Ambari, you are prompted tooauthenticate toohello site.</span></span> <span data-ttu-id="9dc23-122">Hallo beheerder invoeren (standaard `admin`) en het wachtwoord die u hebt gebruikt bij het maken van de cluster Hallo account.</span><span class="sxs-lookup"><span data-stu-id="9dc23-122">Enter hello admin (default `admin`) account name and password you used when creating hello cluster.</span></span>

<span data-ttu-id="9dc23-123">Hier ziet u een pagina vergelijkbaar toohello installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="9dc23-123">You should see a page similar toohello following image:</span></span>

![Afbeelding van Hallo query werkblad voor Hallo Hive-weergave](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <span data-ttu-id="9dc23-125"><a name="hivequery"></a>Een query uitvoeren</span><span class="sxs-lookup"><span data-stu-id="9dc23-125"><a name="hivequery"></a>Run a query</span></span>

<span data-ttu-id="9dc23-126">een hive-query toorun gebruiken Hallo volgende stappen uit Hallo Hive-weergave.</span><span class="sxs-lookup"><span data-stu-id="9dc23-126">toorun a hive query, use hello following steps from hello Hive view.</span></span>

1. <span data-ttu-id="9dc23-127">Van Hallo __Query__ tabblad, Hallo HiveQL-instructies te volgen in Hallo werkblad plakken:</span><span class="sxs-lookup"><span data-stu-id="9dc23-127">From hello __Query__ tab, paste hello following HiveQL statements into hello worksheet:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    <span data-ttu-id="9dc23-128">Deze instructies uitvoeren Hallo volgende acties:</span><span class="sxs-lookup"><span data-stu-id="9dc23-128">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="9dc23-129">`DROP TABLE`-Verwijdert Hallo tabel en Hallo-gegevensbestand als Hallo tabel al bestaat.</span><span class="sxs-lookup"><span data-stu-id="9dc23-129">`DROP TABLE` - Deletes hello table and hello data file, in case hello table already exists.</span></span>

   * <span data-ttu-id="9dc23-130">`CREATE EXTERNAL TABLE`-Maakt een nieuwe tabel 'extern' in Hive.</span><span class="sxs-lookup"><span data-stu-id="9dc23-130">`CREATE EXTERNAL TABLE` - Creates a new "external" table in Hive.</span></span>
   <span data-ttu-id="9dc23-131">Alleen de tabeldefinitie Hallo opslaan externe tabellen in Hive.</span><span class="sxs-lookup"><span data-stu-id="9dc23-131">External tables store only hello table definition in Hive.</span></span> <span data-ttu-id="9dc23-132">Hallo-gegevens in de oorspronkelijke locatie Hallo gelaten.</span><span class="sxs-lookup"><span data-stu-id="9dc23-132">hello data is left in hello original location.</span></span>

   * <span data-ttu-id="9dc23-133">`ROW FORMAT`-Hoe Hallo gegevens zijn opgemaakt.</span><span class="sxs-lookup"><span data-stu-id="9dc23-133">`ROW FORMAT` - How hello data is formatted.</span></span> <span data-ttu-id="9dc23-134">In dit geval worden Hallo velden in elk logboek gescheiden door een spatie.</span><span class="sxs-lookup"><span data-stu-id="9dc23-134">In this case, hello fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="9dc23-135">`STORED AS TEXTFILE LOCATION`-Waar Hallo gegevens worden opgeslagen en dat deze is opgeslagen als tekst.</span><span class="sxs-lookup"><span data-stu-id="9dc23-135">`STORED AS TEXTFILE LOCATION` - Where hello data is stored, and that it is stored as text.</span></span>

   * <span data-ttu-id="9dc23-136">`SELECT`: Hiermee kunt u een telling van alle rijen waarin kolom t4 Hallo waarde [fout] bevat.</span><span class="sxs-lookup"><span data-stu-id="9dc23-136">`SELECT` - Selects a count of all rows where column t4 contains hello value [ERROR].</span></span>

     > [!NOTE]
     > <span data-ttu-id="9dc23-137">Externe tabellen moeten worden gebruikt wanneer u van plan Hallo onderliggende gegevens toobe bijgewerkt door een externe bron bent.</span><span class="sxs-lookup"><span data-stu-id="9dc23-137">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="9dc23-138">Bijvoorbeeld, een geautomatiseerde uploaden van gegevens verwerken, of door een andere MapReduce-bewerking.</span><span class="sxs-lookup"><span data-stu-id="9dc23-138">For example, an automated data upload process, or by another MapReduce operation.</span></span> <span data-ttu-id="9dc23-139">Verwijderen van een externe tabel komt *niet* Hallo gegevens alleen Hallo tabeldefinitie kunt verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9dc23-139">Dropping an external table does *not* delete hello data, only hello table definition.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="9dc23-140">Hallo laat __Database__ selectie __standaard__.</span><span class="sxs-lookup"><span data-stu-id="9dc23-140">Leave hello __Database__ selection at __default__.</span></span> <span data-ttu-id="9dc23-141">Hallo-voorbeelden in dit document Hallo-standaarddatabase die is opgenomen in HDInsight gebruiken.</span><span class="sxs-lookup"><span data-stu-id="9dc23-141">hello examples in this document use hello default database included with HDInsight.</span></span>

2. <span data-ttu-id="9dc23-142">toostart hello query, gebruik Hallo **Execute** knop onder Hallo werkblad.</span><span class="sxs-lookup"><span data-stu-id="9dc23-142">toostart hello query, use hello **Execute** button below hello worksheet.</span></span> <span data-ttu-id="9dc23-143">Tekstwijzigingen oranje en hello te wordt**stoppen**.</span><span class="sxs-lookup"><span data-stu-id="9dc23-143">It turns orange and hello text changes too**Stop**.</span></span>

3. <span data-ttu-id="9dc23-144">Zodra het Hallo-query is voltooid, Hallo **resultaten** tabblad Hallo resultaten van Hallo bewerking weer.</span><span class="sxs-lookup"><span data-stu-id="9dc23-144">Once hello query has finished, hello **Results** tab displays hello results of hello operation.</span></span> <span data-ttu-id="9dc23-145">na de tekst Hello is Hallo resultaat van het Hallo-query:</span><span class="sxs-lookup"><span data-stu-id="9dc23-145">hello following text is hello result of hello query:</span></span>

        sev       cnt
        [ERROR]   3

    <span data-ttu-id="9dc23-146">Hallo **logboeken** tabblad kan worden gemaakt door de taak Hallo Hallo-logboekgegevens voor gebruikte tooview.</span><span class="sxs-lookup"><span data-stu-id="9dc23-146">hello **Logs** tab can be used tooview hello logging information created by hello job.</span></span>

   > [!TIP]
   > <span data-ttu-id="9dc23-147">Hallo **resultaten opslaan** dialoogvenster vervolgkeuzelijst in het bovenste Hallo links van de Hallo **resultaten queryproces** sectie kunt u toodownload of resultaten opslaan.</span><span class="sxs-lookup"><span data-stu-id="9dc23-147">hello **Save results** drop-down dialog in hello upper left of hello **Query Process Results** section allows you toodownload or save results.</span></span>

4. <span data-ttu-id="9dc23-148">Selecteer de eerste vier regels Hallo van deze query Selecteer **Execute**.</span><span class="sxs-lookup"><span data-stu-id="9dc23-148">Select hello first four lines of this query, then select **Execute**.</span></span> <span data-ttu-id="9dc23-149">U ziet dat er geen resultaten zijn wanneer Hallo-taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="9dc23-149">Notice that there are no results when hello job completes.</span></span> <span data-ttu-id="9dc23-150">Met behulp van Hallo **Execute** knop indien deel van de query Hallo alleen wordt uitgevoerd Hallo geselecteerde instructies is geselecteerd.</span><span class="sxs-lookup"><span data-stu-id="9dc23-150">Using hello **Execute** button when part of hello query is selected only runs hello selected statements.</span></span> <span data-ttu-id="9dc23-151">Hallo selectie bevatten niet in dit geval Hallo laatste instructie waarmee rijen worden opgehaald uit de tabel Hallo.</span><span class="sxs-lookup"><span data-stu-id="9dc23-151">In this case, hello selection didn't include hello final statement that retrieves rows from hello table.</span></span> <span data-ttu-id="9dc23-152">Als u alleen die regel selecteren en gebruik **Execute**, ziet u resultaten Hallo verwacht.</span><span class="sxs-lookup"><span data-stu-id="9dc23-152">If you select just that line and use **Execute**, you should see hello expected results.</span></span>

5. <span data-ttu-id="9dc23-153">tooadd een werkblad gebruiken Hallo **nieuw werkblad** knop onderin Hallo Hallo **Query-Editor**.</span><span class="sxs-lookup"><span data-stu-id="9dc23-153">tooadd a worksheet, use hello **New Worksheet** button at hello bottom of hello **Query Editor**.</span></span> <span data-ttu-id="9dc23-154">Voer in nieuw werkblad Hallo Hallo HiveQL-instructies te volgen:</span><span class="sxs-lookup"><span data-stu-id="9dc23-154">In hello new worksheet, enter hello following HiveQL statements:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  <span data-ttu-id="9dc23-155">Deze instructies uitvoeren Hallo volgende acties:</span><span class="sxs-lookup"><span data-stu-id="9dc23-155">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="9dc23-156">**MAKEN van tabel als niet bestaat** -maakt een tabel, als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="9dc23-156">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="9dc23-157">Sinds Hallo **externe** trefwoord wordt niet gebruikt, een interne tabel is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="9dc23-157">Since hello **EXTERNAL** keyword is not used, an internal table is created.</span></span> <span data-ttu-id="9dc23-158">Een interne tabel wordt opgeslagen in Hallo Hive-datawarehouse en volledig wordt beheerd door Hive.</span><span class="sxs-lookup"><span data-stu-id="9dc23-158">An internal table is stored in hello Hive data warehouse and is managed completely by Hive.</span></span> <span data-ttu-id="9dc23-159">In tegenstelling tot externe tabellen verwijdert de Hallo onderliggende gegevens ook een interne tabel verwijderen.</span><span class="sxs-lookup"><span data-stu-id="9dc23-159">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

   * <span data-ttu-id="9dc23-160">**OPGESLAGEN AS ORC** -Hallo-gegevens opslaat in geoptimaliseerd rij kolommen (ORC)-indeling.</span><span class="sxs-lookup"><span data-stu-id="9dc23-160">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="9dc23-161">ORC is een maximaal geoptimaliseerd en efficiënte indeling voor het opslaan van gegevens met Hive.</span><span class="sxs-lookup"><span data-stu-id="9dc23-161">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="9dc23-162">**INSERT OVERSCHRIJVEN... Selecteer** -rijen uit Hallo geselecteerd **log4jLogs** tabel met `[ERROR]`, en vervolgens voegt de gegevens in Hallo Hallo **foutenlogboeken** tabel.</span><span class="sxs-lookup"><span data-stu-id="9dc23-162">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain `[ERROR]`, and then inserts hello data into hello **errorLogs** table.</span></span>

     <span data-ttu-id="9dc23-163">Gebruik Hallo **Execute** knop toorun deze query.</span><span class="sxs-lookup"><span data-stu-id="9dc23-163">Use hello **Execute** button toorun this query.</span></span> <span data-ttu-id="9dc23-164">Hallo **resultaten** tabblad bevat geen gegevens wanneer Hallo query nul rijen retourneert.</span><span class="sxs-lookup"><span data-stu-id="9dc23-164">hello **Results** tab does not contain any information when hello query returns zero rows.</span></span> <span data-ttu-id="9dc23-165">Hallo status moet worden weergegeven als **geslaagd** zodra Hallo-query is voltooid.</span><span class="sxs-lookup"><span data-stu-id="9dc23-165">hello status should show as **SUCCEEDED** once hello query completes.</span></span>

### <a name="visual-explain"></a><span data-ttu-id="9dc23-166">Visual wordt uitgelegd</span><span class="sxs-lookup"><span data-stu-id="9dc23-166">Visual explain</span></span>

<span data-ttu-id="9dc23-167">een visualisatie van queryplan hello, selecteer Hallo toodisplay **Visual uitgelegd** tabblad onder Hallo werkblad.</span><span class="sxs-lookup"><span data-stu-id="9dc23-167">toodisplay a visualization of hello query plan, select hello **Visual Explain** tab below hello worksheet.</span></span>

<span data-ttu-id="9dc23-168">Hallo **Visual uitgelegd** -weergave van Hallo query kan nuttig zijn bij het begrijpen van de stroom Hallo van complexe query's zijn.</span><span class="sxs-lookup"><span data-stu-id="9dc23-168">hello **Visual Explain** view of hello query can be helpful in understanding hello flow of complex queries.</span></span> <span data-ttu-id="9dc23-169">U kunt een tekstuele equivalent van deze weergave weergeven met behulp van Hallo **uitleg** knop in Hallo Query-Editor.</span><span class="sxs-lookup"><span data-stu-id="9dc23-169">You can view a textual equivalent of this view by using hello **Explain** button in hello Query Editor.</span></span>

### <a name="tez-ui"></a><span data-ttu-id="9dc23-170">Tez-gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="9dc23-170">Tez UI</span></span>

<span data-ttu-id="9dc23-171">toodisplay hello Tez UI voor Hallo query, selecteer Hallo **Tez** tabblad onder Hallo werkblad.</span><span class="sxs-lookup"><span data-stu-id="9dc23-171">toodisplay hello Tez UI for hello query, select hello **Tez** tab below hello worksheet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9dc23-172">Tez wordt niet gebruikt tooresolve alle query's.</span><span class="sxs-lookup"><span data-stu-id="9dc23-172">Tez is not used tooresolve all queries.</span></span> <span data-ttu-id="9dc23-173">Groot aantal query's kunnen worden opgelost zonder Tez.</span><span class="sxs-lookup"><span data-stu-id="9dc23-173">Many queries can be resolved without using Tez.</span></span> 

<span data-ttu-id="9dc23-174">Als Tez gebruikte tooresolve Hallo query, wordt Hallo gestuurde acyclische grafiek (DAG) weergegeven.</span><span class="sxs-lookup"><span data-stu-id="9dc23-174">If Tez was used tooresolve hello query, hello Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="9dc23-175">Als u tooview Hallo DAG wilt voor query's in de afgelopen Hallo hebt uitgevoerd, of fouten opsporen in Tez proces hello, gebruikt u Hallo [Tez weergave](hdinsight-debug-ambari-tez-view.md) in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="9dc23-175">If you want tooview hello DAG for queries you've ran in hello past, or debug hello Tez process, use hello [Tez View](hdinsight-debug-ambari-tez-view.md) instead.</span></span>

## <a name="view-job-history"></a><span data-ttu-id="9dc23-176">Taakgeschiedenis weergeven</span><span class="sxs-lookup"><span data-stu-id="9dc23-176">View job history</span></span>

<span data-ttu-id="9dc23-177">Hallo __taken__ tabblad geeft een geschiedenis van Hive-query's.</span><span class="sxs-lookup"><span data-stu-id="9dc23-177">hello __Jobs__ tab displays a history of Hive queries.</span></span>

![Afbeelding van de taakgeschiedenis Hallo](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a><span data-ttu-id="9dc23-179">Databasetabellen</span><span class="sxs-lookup"><span data-stu-id="9dc23-179">Database tables</span></span>

<span data-ttu-id="9dc23-180">U kunt Hallo __tabellen__ tabblad toowork met tabellen in een Hive-database.</span><span class="sxs-lookup"><span data-stu-id="9dc23-180">You can use hello __Tables__ tab toowork with tables within a Hive database.</span></span>

![Afbeelding van tabblad Hallo-tabellen](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a><span data-ttu-id="9dc23-182">Opgeslagen query 's</span><span class="sxs-lookup"><span data-stu-id="9dc23-182">Saved queries</span></span>

<span data-ttu-id="9dc23-183">Vanaf het tabblad Query hello, kunt u eventueel query's opslaan.</span><span class="sxs-lookup"><span data-stu-id="9dc23-183">From hello Query tab, you can optionally save queries.</span></span> <span data-ttu-id="9dc23-184">Wanneer opgeslagen, kunt u de query voor Hallo van Hallo hergebruiken __opgeslagen query's__ tabblad.</span><span class="sxs-lookup"><span data-stu-id="9dc23-184">Once saved, you can reuse hello query from hello __Saved Queries__ tab.</span></span>

![Afbeelding van tabblad opgeslagen query 's](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a><span data-ttu-id="9dc23-186">Gebruiker gedefinieerde functies</span><span class="sxs-lookup"><span data-stu-id="9dc23-186">User-defined functions</span></span>

<span data-ttu-id="9dc23-187">Hive kan ook worden uitgebreid door de gebruiker gedefinieerde functies (UDF).</span><span class="sxs-lookup"><span data-stu-id="9dc23-187">Hive can also be extended through user-defined functions (UDF).</span></span> <span data-ttu-id="9dc23-188">Een UDF kunt u de functionaliteit van tooimplement of logica die eenvoudig niet is gemodelleerd in HiveQL.</span><span class="sxs-lookup"><span data-stu-id="9dc23-188">A UDF allows you tooimplement functionality or logic that isn't easily modeled in HiveQL.</span></span>

<span data-ttu-id="9dc23-189">Hallo UDF-tabblad bovenaan Hallo Hallo Hive-weergave kunt u toodeclare en een set UDF's opslaan.</span><span class="sxs-lookup"><span data-stu-id="9dc23-189">hello UDF tab at hello top of hello Hive View allows you toodeclare and save a set of UDFs.</span></span> <span data-ttu-id="9dc23-190">Deze UDF's kunnen worden gebruikt met Hallo **Query-Editor**.</span><span class="sxs-lookup"><span data-stu-id="9dc23-190">These UDFs can be used with hello **Query Editor**.</span></span>

![Afbeelding van tabblad UDF](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

<span data-ttu-id="9dc23-192">Nadat u een UDF toohello Hive-weergave hebt toegevoegd een **invoegen UDF's** knop wordt weergegeven aan de onderkant Hallo Hallo **Query-Editor**.</span><span class="sxs-lookup"><span data-stu-id="9dc23-192">Once you have added a UDF toohello Hive View, an **Insert udfs** button appears at hello bottom of hello **Query Editor**.</span></span> <span data-ttu-id="9dc23-193">Als u dit item selecteert, geeft een lijst vervolgkeuzelijst Hallo UDF's die zijn gedefinieerd in Hallo Hive-weergave.</span><span class="sxs-lookup"><span data-stu-id="9dc23-193">Selecting this entry displays a drop-down list of hello UDFs defined in hello Hive View.</span></span> <span data-ttu-id="9dc23-194">Als u een UDF, voegt HiveQL-instructies tooyour query tooenable Hallo UDF.</span><span class="sxs-lookup"><span data-stu-id="9dc23-194">Selecting a UDF adds HiveQL statements tooyour query tooenable hello UDF.</span></span>

<span data-ttu-id="9dc23-195">Bijvoorbeeld, als u hebt een UDF gedefinieerd Hello volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="9dc23-195">For example, if you have defined a UDF with hello following properties:</span></span>

* <span data-ttu-id="9dc23-196">Naam van bron: myudfs</span><span class="sxs-lookup"><span data-stu-id="9dc23-196">Resource name: myudfs</span></span>

* <span data-ttu-id="9dc23-197">Bronpad: /myudfs.jar</span><span class="sxs-lookup"><span data-stu-id="9dc23-197">Resource path: /myudfs.jar</span></span>

* <span data-ttu-id="9dc23-198">{UDF-naam: myawesomeudf</span><span class="sxs-lookup"><span data-stu-id="9dc23-198">UDF name: myawesomeudf</span></span>

* <span data-ttu-id="9dc23-199">{UDF-klassenaam: com.myudfs.Awesome</span><span class="sxs-lookup"><span data-stu-id="9dc23-199">UDF class name: com.myudfs.Awesome</span></span>

<span data-ttu-id="9dc23-200">Met behulp van Hallo **invoegen UDF's** knop wordt weergegeven voor een item met de naam **myudfs**, met een andere vervolgkeuzelijst voor elke UDF gedefinieerd voor die bron.</span><span class="sxs-lookup"><span data-stu-id="9dc23-200">Using hello **Insert udfs** button displays an entry named **myudfs**, with another drop-down for each UDF defined for that resource.</span></span> <span data-ttu-id="9dc23-201">In dit geval **myawesomeudf**.</span><span class="sxs-lookup"><span data-stu-id="9dc23-201">In this case, **myawesomeudf**.</span></span> <span data-ttu-id="9dc23-202">Dit item te selecteren, wordt na toohello begin van de query Hallo Hallo toegevoegd:</span><span class="sxs-lookup"><span data-stu-id="9dc23-202">Selecting this entry adds hello following toohello beginning of hello query:</span></span>

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

<span data-ttu-id="9dc23-203">U kunt vervolgens Hallo UDF gebruiken in uw query.</span><span class="sxs-lookup"><span data-stu-id="9dc23-203">You can then use hello UDF in your query.</span></span> <span data-ttu-id="9dc23-204">Bijvoorbeeld `SELECT myawesomeudf(name) FROM people;`.</span><span class="sxs-lookup"><span data-stu-id="9dc23-204">For example, `SELECT myawesomeudf(name) FROM people;`.</span></span>

<span data-ttu-id="9dc23-205">Zie voor meer informatie over het gebruik van UDF's met Hive in HDInsight Hallo documenten te volgen:</span><span class="sxs-lookup"><span data-stu-id="9dc23-205">For more information on using UDFs with Hive on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="9dc23-206">Met behulp van Python met Hive en Pig in HDInsight</span><span class="sxs-lookup"><span data-stu-id="9dc23-206">Using Python with Hive and Pig in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="9dc23-207">Hoe een aangepaste Hive UDF-tooHDInsight tooadd</span><span class="sxs-lookup"><span data-stu-id="9dc23-207">How tooadd a custom Hive UDF tooHDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a><span data-ttu-id="9dc23-208">Hive-instellingen</span><span class="sxs-lookup"><span data-stu-id="9dc23-208">Hive settings</span></span>

<span data-ttu-id="9dc23-209">Instellingen kunnen worden gebruikt toochange diverse Hive-instellingen.</span><span class="sxs-lookup"><span data-stu-id="9dc23-209">Settings can be used toochange various Hive settings.</span></span> <span data-ttu-id="9dc23-210">Engine voor het uitvoeren van Hallo voor Hive bijvoorbeeld gewijzigd van tooMapReduce Tez (Hallo standaard).</span><span class="sxs-lookup"><span data-stu-id="9dc23-210">For example, changing hello execution engine for Hive from Tez (hello default) tooMapReduce.</span></span>

## <span data-ttu-id="9dc23-211"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="9dc23-211"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="9dc23-212">Voor algemene informatie over Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9dc23-212">For general information on Hive in HDInsight:</span></span>

* [<span data-ttu-id="9dc23-213">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="9dc23-213">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="9dc23-214">Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="9dc23-214">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="9dc23-215">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="9dc23-215">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="9dc23-216">MapReduce gebruiken met Hadoop op HDInsight</span><span class="sxs-lookup"><span data-stu-id="9dc23-216">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
