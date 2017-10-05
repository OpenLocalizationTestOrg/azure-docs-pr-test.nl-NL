---
title: Ambari-weergaven gebruiken om te werken met Hive in HDInsight (Hadoop) - Azure | Microsoft Docs
description: Informatie over het gebruik van de Hive-weergave van uw webbrowser Hive-query's verzenden. Het Hive-weergave maakt deel uit van de Ambari-Webgebruikersinterface voorzien van uw Linux gebaseerde HDInsight-cluster.
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
ms.openlocfilehash: 80df3da4d62feb814ea2dd97c96e57954093c5c5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-hive-view-with-hadoop-in-hdinsight"></a><span data-ttu-id="b06ae-104">De weergave Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b06ae-104">Use the Hive View with Hadoop in HDInsight</span></span>

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="b06ae-105">Informatie over het uitvoeren van Hive-query's met Ambari Hive-weergave.</span><span class="sxs-lookup"><span data-stu-id="b06ae-105">Learn how to run Hive queries using Ambari Hive View.</span></span> <span data-ttu-id="b06ae-106">Ambari is een beheer en controle hulpprogramma met HDInsight op basis van Linux-clusters.</span><span class="sxs-lookup"><span data-stu-id="b06ae-106">Ambari is a management and monitoring utility provided with Linux-based HDInsight clusters.</span></span> <span data-ttu-id="b06ae-107">Een van de functies die worden geleverd via Ambari is een Web-UI die kan worden gebruikt voor het uitvoeren van Hive-query's.</span><span class="sxs-lookup"><span data-stu-id="b06ae-107">One of the features provided through Ambari is a Web UI that can be used to run Hive queries.</span></span>

> [!NOTE]
> <span data-ttu-id="b06ae-108">Ambari heeft veel mogelijkheden die niet in dit document worden besproken.</span><span class="sxs-lookup"><span data-stu-id="b06ae-108">Ambari has many capabilities that are not discussed in this document.</span></span> <span data-ttu-id="b06ae-109">Zie voor meer informatie [HDInsight-clusters beheren met behulp van de Ambari-Webgebruikersinterface](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="b06ae-109">For more information, see [Manage HDInsight clusters by using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b06ae-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="b06ae-110">Prerequisites</span></span>

* <span data-ttu-id="b06ae-111">Een Linux gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="b06ae-111">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="b06ae-112">Zie voor meer informatie over het maken van de cluster [aan de slag met HDInsight op basis van Linux](hdinsight-hadoop-linux-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b06ae-112">For information on creating cluster, see [Get started with Linux-based HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b06ae-113">De stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux.</span><span class="sxs-lookup"><span data-stu-id="b06ae-113">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="b06ae-114">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="b06ae-114">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b06ae-115">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b06ae-115">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="open-the-hive-view"></a><span data-ttu-id="b06ae-116">Open de Hive-weergave</span><span class="sxs-lookup"><span data-stu-id="b06ae-116">Open the Hive view</span></span>

<span data-ttu-id="b06ae-117">Kunt u Ambari-weergaven uit de Azure portal; Selecteer uw HDInsight-cluster en selecteer vervolgens **Ambari-weergaven** van de **snelkoppelingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="b06ae-117">You can Ambari Views from the Azure portal; select your HDInsight cluster and then select **Ambari Views** from the **Quick Links** section.</span></span>

![Snelle koppelingen sectie van de portal](./media/hdinsight-hadoop-use-hive-ambari-view/quicklinks.png)

<span data-ttu-id="b06ae-119">Selecteer in de lijst met weergaven, de __Hive-weergave__.</span><span class="sxs-lookup"><span data-stu-id="b06ae-119">From the list of views, select the __Hive View__.</span></span>

![De Hive-weergave geselecteerd](./media/hdinsight-hadoop-use-hive-ambari-view/select-hive-view.png)

> [!NOTE]
> <span data-ttu-id="b06ae-121">Bij het openen van Ambari, wordt u gevraagd om de site te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="b06ae-121">When accessing Ambari, you are prompted to authenticate to the site.</span></span> <span data-ttu-id="b06ae-122">Voer de beheerder (standaard `admin`) account naam en het wachtwoord die u hebt gebruikt bij het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="b06ae-122">Enter the admin (default `admin`) account name and password you used when creating the cluster.</span></span>

<span data-ttu-id="b06ae-123">Hier ziet u een pagina zoals in de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="b06ae-123">You should see a page similar to the following image:</span></span>

![Afbeelding van het werkblad query voor de Hive-weergave](./media/hdinsight-hadoop-use-hive-ambari-view/ambari-hive-view.png)

## <span data-ttu-id="b06ae-125"><a name="hivequery"></a>Een query uitvoeren</span><span class="sxs-lookup"><span data-stu-id="b06ae-125"><a name="hivequery"></a>Run a query</span></span>

<span data-ttu-id="b06ae-126">Als u wilt een hive-query uitvoert, gebruik de volgende stappen uit de Hive-weergave.</span><span class="sxs-lookup"><span data-stu-id="b06ae-126">To run a hive query, use the following steps from the Hive view.</span></span>

1. <span data-ttu-id="b06ae-127">Van de __Query__ tabblad, plak de volgende HiveQL-instructies in het werkblad:</span><span class="sxs-lookup"><span data-stu-id="b06ae-127">From the __Query__ tab, paste the following HiveQL statements into the worksheet:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS cnt FROM log4jLogs WHERE t4 = '[ERROR]' GROUP BY t4;
    ```

    <span data-ttu-id="b06ae-128">Deze instructies uitvoeren de volgende acties:</span><span class="sxs-lookup"><span data-stu-id="b06ae-128">These statements perform the following actions:</span></span>

   * <span data-ttu-id="b06ae-129">`DROP TABLE`-Hiermee verwijdert u de tabel en het gegevensbestand als de tabel al bestaat.</span><span class="sxs-lookup"><span data-stu-id="b06ae-129">`DROP TABLE` - Deletes the table and the data file, in case the table already exists.</span></span>

   * <span data-ttu-id="b06ae-130">`CREATE EXTERNAL TABLE`-Maakt een nieuwe tabel 'extern' in Hive.</span><span class="sxs-lookup"><span data-stu-id="b06ae-130">`CREATE EXTERNAL TABLE` - Creates a new "external" table in Hive.</span></span>
   <span data-ttu-id="b06ae-131">Externe tabellen worden de definitie van de tabel in Hive opslaan.</span><span class="sxs-lookup"><span data-stu-id="b06ae-131">External tables store only the table definition in Hive.</span></span> <span data-ttu-id="b06ae-132">De gegevens blijft op de oorspronkelijke locatie.</span><span class="sxs-lookup"><span data-stu-id="b06ae-132">The data is left in the original location.</span></span>

   * <span data-ttu-id="b06ae-133">`ROW FORMAT`-Hoe de gegevens zijn ingedeeld.</span><span class="sxs-lookup"><span data-stu-id="b06ae-133">`ROW FORMAT` - How the data is formatted.</span></span> <span data-ttu-id="b06ae-134">In dit geval worden de velden in elk logboek gescheiden door een spatie.</span><span class="sxs-lookup"><span data-stu-id="b06ae-134">In this case, the fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="b06ae-135">`STORED AS TEXTFILE LOCATION`-Waar de gegevens worden opgeslagen en dat deze is opgeslagen als tekst.</span><span class="sxs-lookup"><span data-stu-id="b06ae-135">`STORED AS TEXTFILE LOCATION` - Where the data is stored, and that it is stored as text.</span></span>

   * <span data-ttu-id="b06ae-136">`SELECT`: Hiermee kunt u een telling van alle rijen waarin t4 kolom de waarde [fout bevat].</span><span class="sxs-lookup"><span data-stu-id="b06ae-136">`SELECT` - Selects a count of all rows where column t4 contains the value [ERROR].</span></span>

     > [!NOTE]
     > <span data-ttu-id="b06ae-137">Externe tabellen moeten worden gebruikt wanneer u de onderliggende gegevens wordt bijgewerkt door een externe bron verwacht.</span><span class="sxs-lookup"><span data-stu-id="b06ae-137">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="b06ae-138">Bijvoorbeeld, een geautomatiseerde uploaden van gegevens verwerken, of door een andere MapReduce-bewerking.</span><span class="sxs-lookup"><span data-stu-id="b06ae-138">For example, an automated data upload process, or by another MapReduce operation.</span></span> <span data-ttu-id="b06ae-139">Verwijderen van een externe tabel komt *niet* de gegevens, de definitie van de tabel verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b06ae-139">Dropping an external table does *not* delete the data, only the table definition.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="b06ae-140">Laat de __Database__ selectie __standaard__.</span><span class="sxs-lookup"><span data-stu-id="b06ae-140">Leave the __Database__ selection at __default__.</span></span> <span data-ttu-id="b06ae-141">De voorbeelden in dit document gebruikt de standaarddatabase die is opgenomen in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b06ae-141">The examples in this document use the default database included with HDInsight.</span></span>

2. <span data-ttu-id="b06ae-142">Voor het starten van de query gebruikt de **Execute** knop onder het werkblad.</span><span class="sxs-lookup"><span data-stu-id="b06ae-142">To start the query, use the **Execute** button below the worksheet.</span></span> <span data-ttu-id="b06ae-143">Het oranje verandert en verandert de tekst in **stoppen**.</span><span class="sxs-lookup"><span data-stu-id="b06ae-143">It turns orange and the text changes to **Stop**.</span></span>

3. <span data-ttu-id="b06ae-144">Nadat de query is voltooid, de **resultaten** tabblad geeft de resultaten van de bewerking.</span><span class="sxs-lookup"><span data-stu-id="b06ae-144">Once the query has finished, The **Results** tab displays the results of the operation.</span></span> <span data-ttu-id="b06ae-145">De volgende tekst is het resultaat van de query:</span><span class="sxs-lookup"><span data-stu-id="b06ae-145">The following text is the result of the query:</span></span>

        sev       cnt
        [ERROR]   3

    <span data-ttu-id="b06ae-146">De **logboeken** tabblad kan worden gebruikt om gegevens in het logboek wordt gemaakt door de taak weer te geven.</span><span class="sxs-lookup"><span data-stu-id="b06ae-146">The **Logs** tab can be used to view the logging information created by the job.</span></span>

   > [!TIP]
   > <span data-ttu-id="b06ae-147">De **resultaten opslaan** dialoogvenster van de vervolgkeuzelijst in de linkerbovenhoek links van de **resultaten queryproces** sectie kunt u downloaden of het opslaan van resultaten.</span><span class="sxs-lookup"><span data-stu-id="b06ae-147">The **Save results** drop-down dialog in the upper left of the **Query Process Results** section allows you to download or save results.</span></span>

4. <span data-ttu-id="b06ae-148">Selecteer de eerste vier regels van deze query en vervolgens **Execute**.</span><span class="sxs-lookup"><span data-stu-id="b06ae-148">Select the first four lines of this query, then select **Execute**.</span></span> <span data-ttu-id="b06ae-149">U ziet dat er geen resultaten zijn wanneer de taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="b06ae-149">Notice that there are no results when the job completes.</span></span> <span data-ttu-id="b06ae-150">Met behulp van de **Execute** knop als deel van de query is geselecteerd. alleen de geselecteerde instructies wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="b06ae-150">Using the **Execute** button when part of the query is selected only runs the selected statements.</span></span> <span data-ttu-id="b06ae-151">De selectie bevatten niet in dit geval wordt de laatste instructie die rijen opgehaald uit de tabel.</span><span class="sxs-lookup"><span data-stu-id="b06ae-151">In this case, the selection didn't include the final statement that retrieves rows from the table.</span></span> <span data-ttu-id="b06ae-152">Als u alleen die regel selecteren en gebruik **Execute**, ziet u de verwachte resultaten.</span><span class="sxs-lookup"><span data-stu-id="b06ae-152">If you select just that line and use **Execute**, you should see the expected results.</span></span>

5. <span data-ttu-id="b06ae-153">U kunt een werkblad toevoegen met de **nieuw werkblad** knop aan de onderkant van de **Query-Editor**.</span><span class="sxs-lookup"><span data-stu-id="b06ae-153">To add a worksheet, use the **New Worksheet** button at the bottom of the **Query Editor**.</span></span> <span data-ttu-id="b06ae-154">Voer de volgende HiveQL-instructies in het nieuwe werkblad:</span><span class="sxs-lookup"><span data-stu-id="b06ae-154">In the new worksheet, enter the following HiveQL statements:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';
    ```

  <span data-ttu-id="b06ae-155">Deze instructies uitvoeren de volgende acties:</span><span class="sxs-lookup"><span data-stu-id="b06ae-155">These statements perform the following actions:</span></span>

   * <span data-ttu-id="b06ae-156">**MAKEN van tabel als niet bestaat** -maakt een tabel, als deze niet al bestaat.</span><span class="sxs-lookup"><span data-stu-id="b06ae-156">**CREATE TABLE IF NOT EXISTS** - Creates a table, if it does not already exist.</span></span> <span data-ttu-id="b06ae-157">Aangezien de **externe** trefwoord wordt niet gebruikt, een interne tabel is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b06ae-157">Since the **EXTERNAL** keyword is not used, an internal table is created.</span></span> <span data-ttu-id="b06ae-158">Een interne tabel wordt opgeslagen in het datawarehouse Hive en volledig wordt beheerd door Hive.</span><span class="sxs-lookup"><span data-stu-id="b06ae-158">An internal table is stored in the Hive data warehouse and is managed completely by Hive.</span></span> <span data-ttu-id="b06ae-159">In tegenstelling tot externe tabellen voor het verwijderen van een interne tabel worden verwijderd en de onderliggende gegevens.</span><span class="sxs-lookup"><span data-stu-id="b06ae-159">Unlike external tables, dropping an internal table deletes the underlying data as well.</span></span>

   * <span data-ttu-id="b06ae-160">**OPGESLAGEN AS ORC** -slaat de gegevens geoptimaliseerd rij kolommen (ORC)-indeling.</span><span class="sxs-lookup"><span data-stu-id="b06ae-160">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="b06ae-161">ORC is een maximaal geoptimaliseerd en efficiënte indeling voor het opslaan van gegevens met Hive.</span><span class="sxs-lookup"><span data-stu-id="b06ae-161">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="b06ae-162">**INSERT OVERSCHRIJVEN... Selecteer** -selecteert rijen uit de **log4jLogs** tabel met `[ERROR]`, en vervolgens voegt u de gegevens in de **foutenlogboeken** tabel.</span><span class="sxs-lookup"><span data-stu-id="b06ae-162">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain `[ERROR]`, and then inserts the data into the **errorLogs** table.</span></span>

     <span data-ttu-id="b06ae-163">Gebruik de **Execute** knop deze query uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="b06ae-163">Use the **Execute** button to run this query.</span></span> <span data-ttu-id="b06ae-164">De **resultaten** tabblad bevat geen gegevens wanneer de query nul rijen retourneert.</span><span class="sxs-lookup"><span data-stu-id="b06ae-164">The **Results** tab does not contain any information when the query returns zero rows.</span></span> <span data-ttu-id="b06ae-165">De status moet worden weergegeven als **geslaagd** zodra de query is voltooid.</span><span class="sxs-lookup"><span data-stu-id="b06ae-165">The status should show as **SUCCEEDED** once the query completes.</span></span>

### <a name="visual-explain"></a><span data-ttu-id="b06ae-166">Visual wordt uitgelegd</span><span class="sxs-lookup"><span data-stu-id="b06ae-166">Visual explain</span></span>

<span data-ttu-id="b06ae-167">Als u wilt een visualisatie van het queryplan weergeven, selecteert u de **Visual uitgelegd** tabblad onder het werkblad.</span><span class="sxs-lookup"><span data-stu-id="b06ae-167">To display a visualization of the query plan, select the **Visual Explain** tab below the worksheet.</span></span>

<span data-ttu-id="b06ae-168">De **Visual uitgelegd** weergave van de query kan nuttig zijn bij het begrijpen van de stroom van complexe query's zijn.</span><span class="sxs-lookup"><span data-stu-id="b06ae-168">The **Visual Explain** view of the query can be helpful in understanding the flow of complex queries.</span></span> <span data-ttu-id="b06ae-169">U kunt een tekstuele equivalent van deze weergave weergeven met behulp van de **uitleg** knop in de Query-Editor.</span><span class="sxs-lookup"><span data-stu-id="b06ae-169">You can view a textual equivalent of this view by using the **Explain** button in the Query Editor.</span></span>

### <a name="tez-ui"></a><span data-ttu-id="b06ae-170">Tez-gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="b06ae-170">Tez UI</span></span>

<span data-ttu-id="b06ae-171">Als u wilt de Tez UI voor de query weergeven, selecteert u de **Tez** tabblad onder het werkblad.</span><span class="sxs-lookup"><span data-stu-id="b06ae-171">To display the Tez UI for the query, select the **Tez** tab below the worksheet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b06ae-172">Tez wordt niet gebruikt voor het omzetten van alle query's.</span><span class="sxs-lookup"><span data-stu-id="b06ae-172">Tez is not used to resolve all queries.</span></span> <span data-ttu-id="b06ae-173">Groot aantal query's kunnen worden opgelost zonder Tez.</span><span class="sxs-lookup"><span data-stu-id="b06ae-173">Many queries can be resolved without using Tez.</span></span> 

<span data-ttu-id="b06ae-174">Als Tez is gebruikt voor het omzetten van de query, wordt de omgeleid acyclische grafiek (DAG) weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b06ae-174">If Tez was used to resolve the query, the Directed Acyclic Graph (DAG) is displayed.</span></span> <span data-ttu-id="b06ae-175">Als u weergeven van de DAG wilt voor query's in het verleden hebt uitgevoerd, of het proces Tez voor foutopsporing gebruiken de [Tez weergave](hdinsight-debug-ambari-tez-view.md) in plaats daarvan.</span><span class="sxs-lookup"><span data-stu-id="b06ae-175">If you want to view the DAG for queries you've ran in the past, or debug the Tez process, use the [Tez View](hdinsight-debug-ambari-tez-view.md) instead.</span></span>

## <a name="view-job-history"></a><span data-ttu-id="b06ae-176">Taakgeschiedenis weergeven</span><span class="sxs-lookup"><span data-stu-id="b06ae-176">View job history</span></span>

<span data-ttu-id="b06ae-177">De __taken__ tabblad geeft een geschiedenis van Hive-query's.</span><span class="sxs-lookup"><span data-stu-id="b06ae-177">The __Jobs__ tab displays a history of Hive queries.</span></span>

![Afbeelding van de taakgeschiedenis](./media/hdinsight-hadoop-use-hive-ambari-view/job-history.png)

## <a name="database-tables"></a><span data-ttu-id="b06ae-179">Databasetabellen</span><span class="sxs-lookup"><span data-stu-id="b06ae-179">Database tables</span></span>

<span data-ttu-id="b06ae-180">U kunt de __tabellen__ tabblad om te werken met tabellen in een Hive-database.</span><span class="sxs-lookup"><span data-stu-id="b06ae-180">You can use the __Tables__ tab to work with tables within a Hive database.</span></span>

![Afbeelding van het tabblad tabellen](./media/hdinsight-hadoop-use-hive-ambari-view/tables.png)

## <a name="saved-queries"></a><span data-ttu-id="b06ae-182">Opgeslagen query 's</span><span class="sxs-lookup"><span data-stu-id="b06ae-182">Saved queries</span></span>

<span data-ttu-id="b06ae-183">U kunt eventueel query's opslaan op het tabblad Query.</span><span class="sxs-lookup"><span data-stu-id="b06ae-183">From the Query tab, you can optionally save queries.</span></span> <span data-ttu-id="b06ae-184">Wanneer opgeslagen, kunt u de query van hergebruiken de __opgeslagen query's__ tabblad.</span><span class="sxs-lookup"><span data-stu-id="b06ae-184">Once saved, you can reuse the query from the __Saved Queries__ tab.</span></span>

![Afbeelding van tabblad opgeslagen query 's](./media/hdinsight-hadoop-use-hive-ambari-view/saved-queries.png)

## <a name="user-defined-functions"></a><span data-ttu-id="b06ae-186">Gebruiker gedefinieerde functies</span><span class="sxs-lookup"><span data-stu-id="b06ae-186">User-defined functions</span></span>

<span data-ttu-id="b06ae-187">Hive kan ook worden uitgebreid door de gebruiker gedefinieerde functies (UDF).</span><span class="sxs-lookup"><span data-stu-id="b06ae-187">Hive can also be extended through user-defined functions (UDF).</span></span> <span data-ttu-id="b06ae-188">Een UDF, kunt u functionaliteit of logica die eenvoudig niet is gemodelleerd in HiveQL implementeren.</span><span class="sxs-lookup"><span data-stu-id="b06ae-188">A UDF allows you to implement functionality or logic that isn't easily modeled in HiveQL.</span></span>

<span data-ttu-id="b06ae-189">De UDF boven op het tabblad van de weergave Hive kunt u declareren en een reeks UDF's op te slaan.</span><span class="sxs-lookup"><span data-stu-id="b06ae-189">The UDF tab at the top of the Hive View allows you to declare and save a set of UDFs.</span></span> <span data-ttu-id="b06ae-190">Deze UDF's kunnen worden gebruikt met de **Query-Editor**.</span><span class="sxs-lookup"><span data-stu-id="b06ae-190">These UDFs can be used with the **Query Editor**.</span></span>

![Afbeelding van tabblad UDF](./media/hdinsight-hadoop-use-hive-ambari-view/user-defined-functions.png)

<span data-ttu-id="b06ae-192">Nadat u hebt een UDF toegevoegd aan de weergave Hive, een **invoegen UDF's** knop wordt weergegeven aan de onderkant van de **Query-Editor**.</span><span class="sxs-lookup"><span data-stu-id="b06ae-192">Once you have added a UDF to the Hive View, an **Insert udfs** button appears at the bottom of the **Query Editor**.</span></span> <span data-ttu-id="b06ae-193">Als u deze vermelding geeft een vervolgkeuzelijst van de UDF's gedefinieerd in de weergave Hive weer.</span><span class="sxs-lookup"><span data-stu-id="b06ae-193">Selecting this entry displays a drop-down list of the UDFs defined in the Hive View.</span></span> <span data-ttu-id="b06ae-194">Als u een UDF, voegt HiveQL-instructies toe aan uw query voor het inschakelen van de UDF.</span><span class="sxs-lookup"><span data-stu-id="b06ae-194">Selecting a UDF adds HiveQL statements to your query to enable the UDF.</span></span>

<span data-ttu-id="b06ae-195">Bijvoorbeeld, als u hebt gedefinieerd een UDF met de volgende eigenschappen:</span><span class="sxs-lookup"><span data-stu-id="b06ae-195">For example, if you have defined a UDF with the following properties:</span></span>

* <span data-ttu-id="b06ae-196">Naam van bron: myudfs</span><span class="sxs-lookup"><span data-stu-id="b06ae-196">Resource name: myudfs</span></span>

* <span data-ttu-id="b06ae-197">Bronpad: /myudfs.jar</span><span class="sxs-lookup"><span data-stu-id="b06ae-197">Resource path: /myudfs.jar</span></span>

* <span data-ttu-id="b06ae-198">{UDF-naam: myawesomeudf</span><span class="sxs-lookup"><span data-stu-id="b06ae-198">UDF name: myawesomeudf</span></span>

* <span data-ttu-id="b06ae-199">{UDF-klassenaam: com.myudfs.Awesome</span><span class="sxs-lookup"><span data-stu-id="b06ae-199">UDF class name: com.myudfs.Awesome</span></span>

<span data-ttu-id="b06ae-200">Met behulp van de **invoegen UDF's** knop wordt weergegeven voor een item met de naam **myudfs**, met een andere vervolgkeuzelijst voor elke UDF gedefinieerd voor die bron.</span><span class="sxs-lookup"><span data-stu-id="b06ae-200">Using the **Insert udfs** button displays an entry named **myudfs**, with another drop-down for each UDF defined for that resource.</span></span> <span data-ttu-id="b06ae-201">In dit geval **myawesomeudf**.</span><span class="sxs-lookup"><span data-stu-id="b06ae-201">In this case, **myawesomeudf**.</span></span> <span data-ttu-id="b06ae-202">Dit item te selecteren, worden de volgende toegevoegd aan het begin van de query:</span><span class="sxs-lookup"><span data-stu-id="b06ae-202">Selecting this entry adds the following to the beginning of the query:</span></span>

```hiveql
add jar /myudfs.jar;
create temporary function myawesomeudf as 'com.myudfs.Awesome';
```

<span data-ttu-id="b06ae-203">U kunt vervolgens de UDF gebruiken in uw query.</span><span class="sxs-lookup"><span data-stu-id="b06ae-203">You can then use the UDF in your query.</span></span> <span data-ttu-id="b06ae-204">Bijvoorbeeld `SELECT myawesomeudf(name) FROM people;`.</span><span class="sxs-lookup"><span data-stu-id="b06ae-204">For example, `SELECT myawesomeudf(name) FROM people;`.</span></span>

<span data-ttu-id="b06ae-205">Zie de volgende documenten voor meer informatie over het gebruik van UDF's met Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b06ae-205">For more information on using UDFs with Hive on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="b06ae-206">Met behulp van Python met Hive en Pig in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b06ae-206">Using Python with Hive and Pig in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="b06ae-207">Het toevoegen van een aangepaste Hive UDF naar HDInsight</span><span class="sxs-lookup"><span data-stu-id="b06ae-207">How to add a custom Hive UDF to HDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

## <a name="hive-settings"></a><span data-ttu-id="b06ae-208">Hive-instellingen</span><span class="sxs-lookup"><span data-stu-id="b06ae-208">Hive settings</span></span>

<span data-ttu-id="b06ae-209">Instellingen kunnen worden gebruikt om verschillende Hive-instellingen te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b06ae-209">Settings can be used to change various Hive settings.</span></span> <span data-ttu-id="b06ae-210">Bijvoorbeeld wijzigen van de engine voor het uitvoeren voor MapReduce onderdeel van Tez (de standaardinstelling).</span><span class="sxs-lookup"><span data-stu-id="b06ae-210">For example, changing the execution engine for Hive from Tez (the default) to MapReduce.</span></span>

## <span data-ttu-id="b06ae-211"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b06ae-211"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="b06ae-212">Voor algemene informatie over Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b06ae-212">For general information on Hive in HDInsight:</span></span>

* [<span data-ttu-id="b06ae-213">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b06ae-213">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="b06ae-214">Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b06ae-214">For information on other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="b06ae-215">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b06ae-215">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="b06ae-216">MapReduce gebruiken met Hadoop op HDInsight</span><span class="sxs-lookup"><span data-stu-id="b06ae-216">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
