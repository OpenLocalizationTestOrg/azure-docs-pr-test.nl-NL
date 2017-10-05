---
title: Wat is Apache Hive en HiveQL - Azure HDInsight | Microsoft Docs
description: Apache Hive is een systeem voor het datawarehouse van gegevens voor Hadoop. U kunt de gegevens die zijn opgeslagen in met behulp van HiveQL, Hive query die vergelijkbaar is met Transact-SQL. In dit document wordt beschreven hoe Hive en HiveQL gebruiken met Azure HDInsight.
keywords: hiveql, wat hive, hadoop hiveql, is het gebruik van hive, informatie over hive, wat is er hive
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2c10f989-7636-41bf-b7f7-c4b67ec0814f
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 6b3ee17141f773bec07cf40e0b6d63363e9b5164
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a><span data-ttu-id="ebbad-106">Wat is Apache Hive en HiveQL in Azure HDInsight?</span><span class="sxs-lookup"><span data-stu-id="ebbad-106">What is Apache Hive and HiveQL on Azure HDInsight?</span></span>

<span data-ttu-id="ebbad-107">[Apache Hive](http://hive.apache.org/) is een systeem voor het datawarehouse van gegevens voor Hadoop.</span><span class="sxs-lookup"><span data-stu-id="ebbad-107">[Apache Hive](http://hive.apache.org/) is a data warehouse system for Hadoop.</span></span> <span data-ttu-id="ebbad-108">Hive kunt gegevenssamenvatting, query's en analyse van gegevens.</span><span class="sxs-lookup"><span data-stu-id="ebbad-108">Hive enables data summarization, querying, and analysis of data.</span></span> <span data-ttu-id="ebbad-109">Hive-query's zijn geschreven in HiveQL, namelijk een querytaal die vergelijkbaar is met SQL.</span><span class="sxs-lookup"><span data-stu-id="ebbad-109">Hive queries are written in HiveQL, which is a query language similar to SQL.</span></span>

<span data-ttu-id="ebbad-110">Hive kunt u de projectstructuur van het op grotendeels ongestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="ebbad-110">Hive allows you to project structure on largely unstructured data.</span></span> <span data-ttu-id="ebbad-111">Nadat u de structuur gedefinieerd, kunt u HiveQL query uitvoeren op de gegevens zonder kennis van Java of MapReduce.</span><span class="sxs-lookup"><span data-stu-id="ebbad-111">After you define the structure, you can use HiveQL to query the data without knowledge of Java or MapReduce.</span></span>

<span data-ttu-id="ebbad-112">HDInsight biedt verschillende clustertypen die zijn afgestemd op specifieke werkbelasting in gedachten.</span><span class="sxs-lookup"><span data-stu-id="ebbad-112">HDInsight provides several cluster types, which are tuned for specific workloads.</span></span> <span data-ttu-id="ebbad-113">De volgende clustertypen worden meestal gebruikt voor Hive-query's:</span><span class="sxs-lookup"><span data-stu-id="ebbad-113">The following cluster types are most often used for Hive queries:</span></span>

* <span data-ttu-id="ebbad-114">__Interactieve Hive__: een Hadoop-cluster waarmee [lage latentie analytische verwerking (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) functionaliteit voor de reactietijd voor interactieve query's verbeteren.</span><span class="sxs-lookup"><span data-stu-id="ebbad-114">__Interactive Hive__: A Hadoop cluster that provides [Low Latency Analytical Processing (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) functionality to improve response times for interactive queries.</span></span> <span data-ttu-id="ebbad-115">Zie voor meer informatie de [beginnen met een interactieve Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md) document.</span><span class="sxs-lookup"><span data-stu-id="ebbad-115">For more information, see the [Start with Interactive Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

* <span data-ttu-id="ebbad-116">__Hadoop__: een Hadoop-cluster dat is afgestemd op batchverwerking werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="ebbad-116">__Hadoop__: A Hadoop cluster that is tuned for batch processing workloads.</span></span> <span data-ttu-id="ebbad-117">Zie voor meer informatie de [starten met Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="ebbad-117">For more information, see the [Start with Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) document.</span></span>

* <span data-ttu-id="ebbad-118">__Spark__: Apache Spark zijn ingebouwde functionaliteit voor het werken met Hive.</span><span class="sxs-lookup"><span data-stu-id="ebbad-118">__Spark__: Apache Spark has built-in functionality for working with Hive.</span></span> <span data-ttu-id="ebbad-119">Zie voor meer informatie de [beginnen met Spark in HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) document.</span><span class="sxs-lookup"><span data-stu-id="ebbad-119">For more information, see the [Start with Spark on HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) document.</span></span>

* <span data-ttu-id="ebbad-120">__HBase__: HiveQL kan worden gebruikt voor opgeslagen querygegevens in HBase.</span><span class="sxs-lookup"><span data-stu-id="ebbad-120">__HBase__: HiveQL can be used to query data stored in HBase.</span></span> <span data-ttu-id="ebbad-121">Zie voor meer informatie de [beginnen met HBase in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) document.</span><span class="sxs-lookup"><span data-stu-id="ebbad-121">For more information, see the [Start with HBase on HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) document.</span></span>

## <a name="how-to-use-hive"></a><span data-ttu-id="ebbad-122">Het gebruik van Hive</span><span class="sxs-lookup"><span data-stu-id="ebbad-122">How to use Hive</span></span>

<span data-ttu-id="ebbad-123">Gebruik de volgende tabel voor het detecteren van het gebruik van Hive met HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ebbad-123">Use the following table to discover how to use Hive with HDInsight:</span></span>

| <span data-ttu-id="ebbad-124">**Gebruik deze methode** als u wilt dat...</span><span class="sxs-lookup"><span data-stu-id="ebbad-124">**Use this method** if you want...</span></span> | <span data-ttu-id="ebbad-125">.. .an **interactieve** shell</span><span class="sxs-lookup"><span data-stu-id="ebbad-125">...an **interactive** shell</span></span> | <span data-ttu-id="ebbad-126">... **batch** verwerken</span><span class="sxs-lookup"><span data-stu-id="ebbad-126">...**batch** processing</span></span> | <span data-ttu-id="ebbad-127">.. .door dit **cluster-besturingssysteem**</span><span class="sxs-lookup"><span data-stu-id="ebbad-127">...with this **cluster operating system**</span></span> | <span data-ttu-id="ebbad-128">.. .from dit **clientbesturingssysteem**</span><span class="sxs-lookup"><span data-stu-id="ebbad-128">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="ebbad-129">Hive-weergave</span><span class="sxs-lookup"><span data-stu-id="ebbad-129">Hive View</span></span>](hdinsight-hadoop-use-hive-ambari-view.md) |<span data-ttu-id="ebbad-130">✔</span><span class="sxs-lookup"><span data-stu-id="ebbad-130">✔</span></span> |<span data-ttu-id="ebbad-131">✔</span><span class="sxs-lookup"><span data-stu-id="ebbad-131">✔</span></span> |<span data-ttu-id="ebbad-132">Linux</span><span class="sxs-lookup"><span data-stu-id="ebbad-132">Linux</span></span> |<span data-ttu-id="ebbad-133">(Browser gebaseerd)</span><span class="sxs-lookup"><span data-stu-id="ebbad-133">Any (browser based)</span></span> |
| [<span data-ttu-id="ebbad-134">Beeline client</span><span class="sxs-lookup"><span data-stu-id="ebbad-134">Beeline client</span></span>](hdinsight-hadoop-use-hive-beeline.md) |<span data-ttu-id="ebbad-135">✔</span><span class="sxs-lookup"><span data-stu-id="ebbad-135">✔</span></span> |<span data-ttu-id="ebbad-136">✔</span><span class="sxs-lookup"><span data-stu-id="ebbad-136">✔</span></span> |<span data-ttu-id="ebbad-137">Linux</span><span class="sxs-lookup"><span data-stu-id="ebbad-137">Linux</span></span> |<span data-ttu-id="ebbad-138">Linux, Unix, Mac OS X of Windows</span><span class="sxs-lookup"><span data-stu-id="ebbad-138">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="ebbad-139">REST API</span><span class="sxs-lookup"><span data-stu-id="ebbad-139">REST API</span></span>](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |<span data-ttu-id="ebbad-140">✔</span><span class="sxs-lookup"><span data-stu-id="ebbad-140">✔</span></span> |<span data-ttu-id="ebbad-141">Linux- of Windows *</span><span class="sxs-lookup"><span data-stu-id="ebbad-141">Linux or Windows*</span></span> |<span data-ttu-id="ebbad-142">Linux, Unix, Mac OS X of Windows</span><span class="sxs-lookup"><span data-stu-id="ebbad-142">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="ebbad-143">HDInsight tools voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ebbad-143">HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |<span data-ttu-id="ebbad-144">✔</span><span class="sxs-lookup"><span data-stu-id="ebbad-144">✔</span></span> |<span data-ttu-id="ebbad-145">Linux- of Windows *</span><span class="sxs-lookup"><span data-stu-id="ebbad-145">Linux or Windows*</span></span> |<span data-ttu-id="ebbad-146">Windows</span><span class="sxs-lookup"><span data-stu-id="ebbad-146">Windows</span></span> |
| [<span data-ttu-id="ebbad-147">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ebbad-147">Windows PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |<span data-ttu-id="ebbad-148">✔</span><span class="sxs-lookup"><span data-stu-id="ebbad-148">✔</span></span> |<span data-ttu-id="ebbad-149">Linux- of Windows *</span><span class="sxs-lookup"><span data-stu-id="ebbad-149">Linux or Windows*</span></span> |<span data-ttu-id="ebbad-150">Windows</span><span class="sxs-lookup"><span data-stu-id="ebbad-150">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="ebbad-151">\*Linux is het enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="ebbad-151">\* Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ebbad-152">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ebbad-152">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="ebbad-153">Als u een cluster met HDInsight op basis van Windows gebruikt, kunt u de [Query console](hdinsight-hadoop-use-hive-query-console.md) vanuit de browser of [extern bureaublad](hdinsight-hadoop-use-hive-remote-desktop.md) Hive-query's uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="ebbad-153">If you are using a Windows-based HDInsight cluster, you can use the [Query console](hdinsight-hadoop-use-hive-query-console.md) from your browser or [Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md) to run Hive queries.</span></span>

## <a name="hiveql-language-reference"></a><span data-ttu-id="ebbad-154">HiveQL-taalreferentie</span><span class="sxs-lookup"><span data-stu-id="ebbad-154">HiveQL language reference</span></span>

<span data-ttu-id="ebbad-155">Taalreferentie HiveQL is beschikbaar in de [taal handmatig (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span><span class="sxs-lookup"><span data-stu-id="ebbad-155">HiveQL language reference is available in the [language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span></span>

## <a name="hive-and-data-structure"></a><span data-ttu-id="ebbad-156">Structuur van hive en gegevens</span><span class="sxs-lookup"><span data-stu-id="ebbad-156">Hive and data structure</span></span>

<span data-ttu-id="ebbad-157">Hive begrijpt het werken met gestructureerde en semi-gestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="ebbad-157">Hive understands how to work with structured and semi-structured data.</span></span> <span data-ttu-id="ebbad-158">Bijvoorbeeld: tekstbestanden waarin de velden worden gescheiden door specifieke tekens.</span><span class="sxs-lookup"><span data-stu-id="ebbad-158">For example, text files where the fields are delimited by specific characters.</span></span> <span data-ttu-id="ebbad-159">De volgende instructie van HiveQL maakt een tabel door spaties gescheiden gegevens:</span><span class="sxs-lookup"><span data-stu-id="ebbad-159">The following HiveQL statement creates a table over space-delimited data:</span></span>

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

<span data-ttu-id="ebbad-160">Hive biedt ook ondersteuning voor aangepaste **serialisatiefunctie/deserializers (serde-schrijfbewerking)** voor complexe of onregelmatig gestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="ebbad-160">Hive also supports custom **serializer/deserializers (SerDe)** for complex or irregularly structured data.</span></span> <span data-ttu-id="ebbad-161">Zie voor meer informatie de [een aangepaste JSON serde-schrijfbewerking gebruiken met HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.</span><span class="sxs-lookup"><span data-stu-id="ebbad-161">For more information, see the [How to use a custom JSON SerDe with HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.</span></span>

<span data-ttu-id="ebbad-162">Zie voor meer informatie over ondersteunde bestandsindelingen in Hive, de [taal handmatig (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span><span class="sxs-lookup"><span data-stu-id="ebbad-162">For more information on file formats supported by Hive, see the [Language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span></span>

## <a name="hive-internal-tables-vs-external-tables"></a><span data-ttu-id="ebbad-163">Interne tabellen tegenover externe tabellen hive</span><span class="sxs-lookup"><span data-stu-id="ebbad-163">Hive internal tables vs external tables</span></span>

<span data-ttu-id="ebbad-164">Er zijn twee soorten tabellen die u met Hive maken kunt:</span><span class="sxs-lookup"><span data-stu-id="ebbad-164">There are two types of tables that you can create with Hive:</span></span>

* <span data-ttu-id="ebbad-165">__Interne__: gegevens worden opgeslagen in het datawarehouse Hive.</span><span class="sxs-lookup"><span data-stu-id="ebbad-165">__Internal__: Data is stored in the Hive data warehouse.</span></span> <span data-ttu-id="ebbad-166">Het datawarehouse bevindt zich op `/hive/warehouse/` op de standaard-opslag voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="ebbad-166">The data warehouse is located at `/hive/warehouse/` on the default storage for the cluster.</span></span>

    <span data-ttu-id="ebbad-167">Gebruik interne tabellen wanneer:</span><span class="sxs-lookup"><span data-stu-id="ebbad-167">Use internal tables when:</span></span>

    * <span data-ttu-id="ebbad-168">Gegevens is tijdelijk.</span><span class="sxs-lookup"><span data-stu-id="ebbad-168">Data is temporary.</span></span>
    * <span data-ttu-id="ebbad-169">Wilt u Hive voor het beheren van de levenscyclus van de tabel en de gegevens.</span><span class="sxs-lookup"><span data-stu-id="ebbad-169">You want Hive to manage the lifecycle of the table and data.</span></span>

* <span data-ttu-id="ebbad-170">__Externe__: gegevens worden opgeslagen buiten het datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="ebbad-170">__External__: Data is stored outside the data warehouse.</span></span> <span data-ttu-id="ebbad-171">De gegevens kunnen worden opgeslagen op opslag die toegankelijk is door het cluster.</span><span class="sxs-lookup"><span data-stu-id="ebbad-171">The data can be stored on any storage accessible by the cluster.</span></span>

    <span data-ttu-id="ebbad-172">Gebruik externe tabellen wanneer:</span><span class="sxs-lookup"><span data-stu-id="ebbad-172">Use external tables when:</span></span>

    * <span data-ttu-id="ebbad-173">De gegevens worden ook gebruikt buiten Hive.</span><span class="sxs-lookup"><span data-stu-id="ebbad-173">The data is also used outside of Hive.</span></span> <span data-ttu-id="ebbad-174">Bijvoorbeeld, worden de gegevensbestanden bijgewerkt door een ander proces (die wordt niet vergrendeld de bestanden.)</span><span class="sxs-lookup"><span data-stu-id="ebbad-174">For example, the data files are updated by another process (that does not lock the files.)</span></span>
    * <span data-ttu-id="ebbad-175">Gegevens moeten blijven in de onderliggende locatie, zelfs na het verwijderen van de tabel.</span><span class="sxs-lookup"><span data-stu-id="ebbad-175">Data needs to remain in the underlying location, even after dropping the table.</span></span>
    * <span data-ttu-id="ebbad-176">U moet een aangepaste locatie, zoals een niet-standaard opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="ebbad-176">You need a custom location, such as a non-default storage account.</span></span>
    * <span data-ttu-id="ebbad-177">Een ander programma dan hive beheert de indeling van gegevens, locatie, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="ebbad-177">A program other than hive manages the data format, location, etc.</span></span>

<span data-ttu-id="ebbad-178">Zie voor meer informatie de [Hive interne en externe tabellen Intro] [ cindygross-hive-tables] blogbericht.</span><span class="sxs-lookup"><span data-stu-id="ebbad-178">For more information, see the [Hive Internal and External Tables Intro][cindygross-hive-tables] blog post.</span></span>

## <a name="user-defined-functions-udf"></a><span data-ttu-id="ebbad-179">Gebruiker gedefinieerde functies (UDF)</span><span class="sxs-lookup"><span data-stu-id="ebbad-179">User-defined functions (UDF)</span></span>

<span data-ttu-id="ebbad-180">Hive kan verder worden uitgebreid via **gebruiker gedefinieerde functies (UDF)**.</span><span class="sxs-lookup"><span data-stu-id="ebbad-180">Hive can also be extended through **user-defined functions (UDF)**.</span></span> <span data-ttu-id="ebbad-181">Een UDF, kunt u functionaliteit of logica die eenvoudig niet is gemodelleerd in HiveQL implementeren.</span><span class="sxs-lookup"><span data-stu-id="ebbad-181">A UDF allows you to implement functionality or logic that isn't easily modeled in HiveQL.</span></span> <span data-ttu-id="ebbad-182">Zie de volgende documenten voor een voorbeeld van het gebruik van UDF's met Hive:</span><span class="sxs-lookup"><span data-stu-id="ebbad-182">For an example of using UDFs with Hive, see the following documents:</span></span>

* [<span data-ttu-id="ebbad-183">Een Java door de gebruiker gedefinieerde functie gebruiken met Hive</span><span class="sxs-lookup"><span data-stu-id="ebbad-183">Use a Java user-defined function with Hive</span></span>](hdinsight-hadoop-hive-java-udf.md)

* [<span data-ttu-id="ebbad-184">Een Python door de gebruiker gedefinieerde functie gebruiken met Hive en Pig</span><span class="sxs-lookup"><span data-stu-id="ebbad-184">Use a Python user-defined function with Hive and Pig</span></span>](hdinsight-python.md)

* [<span data-ttu-id="ebbad-185">Een C# gebruiker gedefinieerde functie gebruiken met Hive en Pig</span><span class="sxs-lookup"><span data-stu-id="ebbad-185">Use a C# user-defined function with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="ebbad-186">Het toevoegen van een aangepaste Hive gebruiker gedefinieerde functie aan HDInsight</span><span class="sxs-lookup"><span data-stu-id="ebbad-186">How to add a custom Hive user-defined function to HDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [<span data-ttu-id="ebbad-187">Een voorbeeld van de gebruiker gedefinieerde functie datum/tijd-indeling converteren naar Hive tijdstempel Hive</span><span class="sxs-lookup"><span data-stu-id="ebbad-187">An example Hive user-defined function to convert date/time formats to Hive timestamp</span></span>](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <span data-ttu-id="ebbad-188"><a id="data"></a>Voorbeeldgegevens</span><span class="sxs-lookup"><span data-stu-id="ebbad-188"><a id="data"></a>Example data</span></span>

<span data-ttu-id="ebbad-189">Hive in HDInsight wordt vooraf geladen geleverd met een interne tabel met de naam `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="ebbad-189">Hive on HDInsight comes pre-loaded with an internal table named `hivesampletable`.</span></span> <span data-ttu-id="ebbad-190">HDInsight biedt ook een voorbeeld van gegevenssets die kunnen worden gebruikt met Hive.</span><span class="sxs-lookup"><span data-stu-id="ebbad-190">HDInsight also provides example data sets that can be used with Hive.</span></span> <span data-ttu-id="ebbad-191">Deze gegevenssets worden opgeslagen in de `/example/data` en `/HdiSamples` mappen.</span><span class="sxs-lookup"><span data-stu-id="ebbad-191">These data sets are stored in the `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="ebbad-192">Deze mappen aanwezig zijn in de standaard-opslag voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="ebbad-192">These directories exist in the default storage for your cluster.</span></span>

## <span data-ttu-id="ebbad-193"><a id="job"></a>Voorbeeld van de Hive-query</span><span class="sxs-lookup"><span data-stu-id="ebbad-193"><a id="job"></a>Example Hive query</span></span>

<span data-ttu-id="ebbad-194">De volgende HiveQL-instructies project kolommen naar de `/example/data/sample.log` bestand:</span><span class="sxs-lookup"><span data-stu-id="ebbad-194">The following HiveQL statements project columns onto the `/example/data/sample.log` file:</span></span>

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

<span data-ttu-id="ebbad-195">In het vorige voorbeeld uitvoeren de HiveQL-instructies de volgende acties:</span><span class="sxs-lookup"><span data-stu-id="ebbad-195">In the previous example, the HiveQL statements perform the following actions:</span></span>

* <span data-ttu-id="ebbad-196">`set hive.execution.engine=tez;`: Hiermee stelt u de engine voor het uitvoeren Tez gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ebbad-196">`set hive.execution.engine=tez;`: Sets the execution engine to use Tez.</span></span> <span data-ttu-id="ebbad-197">Tez gebruik in plaats van MapReduce krijgt u een toename van de prestaties van query's.</span><span class="sxs-lookup"><span data-stu-id="ebbad-197">Using Tez instead of MapReduce can provide an increase in query performance.</span></span> <span data-ttu-id="ebbad-198">Zie voor meer informatie over Tez de [Apache Tez gebruiken voor betere prestaties](#usetez) sectie.</span><span class="sxs-lookup"><span data-stu-id="ebbad-198">For more information on Tez, see the [Use Apache Tez for improved performance](#usetez) section.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ebbad-199">Deze instructie is alleen vereist wanneer u een HDInsight op basis van Windows-cluster.</span><span class="sxs-lookup"><span data-stu-id="ebbad-199">This statement is only required when using a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="ebbad-200">Tez is de engine voor het uitvoeren van standaard voor HDInsight op basis van Linux.</span><span class="sxs-lookup"><span data-stu-id="ebbad-200">Tez is the default execution engine for Linux-based HDInsight.</span></span>

* <span data-ttu-id="ebbad-201">`DROP TABLE`: Als de tabel al bestaat, verwijderen.</span><span class="sxs-lookup"><span data-stu-id="ebbad-201">`DROP TABLE`: If the table already exists, delete it.</span></span>

* <span data-ttu-id="ebbad-202">`CREATE EXTERNAL TABLE`: Hiermee maakt u een nieuw **externe** tabel in Hive.</span><span class="sxs-lookup"><span data-stu-id="ebbad-202">`CREATE EXTERNAL TABLE`: Creates a new **external** table in Hive.</span></span> <span data-ttu-id="ebbad-203">De tabeldefinitie opslaan externe tabellen alleen in Hive.</span><span class="sxs-lookup"><span data-stu-id="ebbad-203">External tables only store the table definition in Hive.</span></span> <span data-ttu-id="ebbad-204">De gegevens blijft in de oorspronkelijke locatie en in de oorspronkelijke indeling.</span><span class="sxs-lookup"><span data-stu-id="ebbad-204">The data is left in the original location and in the original format.</span></span>

* <span data-ttu-id="ebbad-205">`ROW FORMAT`: Hiermee geeft u Hive hoe de gegevens wordt opgemaakt.</span><span class="sxs-lookup"><span data-stu-id="ebbad-205">`ROW FORMAT`: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="ebbad-206">In dit geval worden de velden in elk logboek gescheiden door een spatie.</span><span class="sxs-lookup"><span data-stu-id="ebbad-206">In this case, the fields in each log are separated by a space.</span></span>

* <span data-ttu-id="ebbad-207">`STORED AS TEXTFILE LOCATION`: Vertelt Hive waar de gegevens worden opgeslagen (de `example/data` directory) en dat deze is opgeslagen als tekst.</span><span class="sxs-lookup"><span data-stu-id="ebbad-207">`STORED AS TEXTFILE LOCATION`: Tells Hive where the data is stored (the `example/data` directory) and that it is stored as text.</span></span> <span data-ttu-id="ebbad-208">De gegevens worden in één bestand of worden verdeeld over meerdere bestanden in de map.</span><span class="sxs-lookup"><span data-stu-id="ebbad-208">The data can be in one file or spread across multiple files within the directory.</span></span>

* <span data-ttu-id="ebbad-209">`SELECT`: Hiermee selecteert u een telling van alle rijen waarin de kolom **t4** bevat de waarde **[fout]**.</span><span class="sxs-lookup"><span data-stu-id="ebbad-209">`SELECT`: Selects a count of all rows where the column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="ebbad-210">Deze instructie retourneert een waarde van **3** omdat er drie rijen met deze waarde.</span><span class="sxs-lookup"><span data-stu-id="ebbad-210">This statement returns a value of **3** because there are three rows that contain this value.</span></span>

* <span data-ttu-id="ebbad-211">`INPUT__FILE__NAME LIKE '%.log'`-Hive probeert het schema toepassen op alle bestanden in de map.</span><span class="sxs-lookup"><span data-stu-id="ebbad-211">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts to apply the schema to all files in the directory.</span></span> <span data-ttu-id="ebbad-212">In dit geval wordt bevat de map bestanden die niet overeenkomen met het schema.</span><span class="sxs-lookup"><span data-stu-id="ebbad-212">In this case, the directory contains files that do not match the schema.</span></span> <span data-ttu-id="ebbad-213">Om te voorkomen dat een garbagecollection-gegevens in de resultaten, deze instructie vertelt Hive dat we alleen gegevens uit bestanden eindigt op moet retourneren. log.</span><span class="sxs-lookup"><span data-stu-id="ebbad-213">To prevent garbage data in the results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

> [!NOTE]
> <span data-ttu-id="ebbad-214">Externe tabellen moeten worden gebruikt wanneer u de onderliggende gegevens wordt bijgewerkt door een externe bron verwacht.</span><span class="sxs-lookup"><span data-stu-id="ebbad-214">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="ebbad-215">Bijvoorbeeld, een geautomatiseerd proces of MapReduce-bewerking uploaden.</span><span class="sxs-lookup"><span data-stu-id="ebbad-215">For example, an automated data upload process, or MapReduce operation.</span></span>
>
> <span data-ttu-id="ebbad-216">Verwijderen van een externe tabel komt **niet** gegevens verwijderd, wordt de definitie van de tabel alleen verwijderd.</span><span class="sxs-lookup"><span data-stu-id="ebbad-216">Dropping an external table does **not** delete the data, it only deletes the table definition.</span></span>

<span data-ttu-id="ebbad-217">Maken van een **interne** in plaats van de externe tabel, gebruikt u de volgende HiveQL:</span><span class="sxs-lookup"><span data-stu-id="ebbad-217">To create an **internal** table instead of external, use the following HiveQL:</span></span>

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

<span data-ttu-id="ebbad-218">Deze instructies uitvoeren de volgende acties:</span><span class="sxs-lookup"><span data-stu-id="ebbad-218">These statements perform the following actions:</span></span>

* <span data-ttu-id="ebbad-219">`CREATE TABLE IF NOT EXISTS`: Als de tabel niet bestaat, maakt u dit.</span><span class="sxs-lookup"><span data-stu-id="ebbad-219">`CREATE TABLE IF NOT EXISTS`: If the table does not exist, create it.</span></span> <span data-ttu-id="ebbad-220">Omdat de **externe** trefwoord wordt niet gebruikt, wordt deze instructie maakt u een interne tabel.</span><span class="sxs-lookup"><span data-stu-id="ebbad-220">Because the **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="ebbad-221">De tabel wordt opgeslagen in het datawarehouse Hive en volledig wordt beheerd door Hive.</span><span class="sxs-lookup"><span data-stu-id="ebbad-221">The table is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

* <span data-ttu-id="ebbad-222">`STORED AS ORC`: De gegevens opslaat in geoptimaliseerd rij kolommen (ORC)-indeling.</span><span class="sxs-lookup"><span data-stu-id="ebbad-222">`STORED AS ORC`: Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="ebbad-223">ORC is een maximaal geoptimaliseerd en efficiënte indeling voor het opslaan van gegevens met Hive.</span><span class="sxs-lookup"><span data-stu-id="ebbad-223">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

* <span data-ttu-id="ebbad-224">`INSERT OVERWRITE ... SELECT`: Selecteert rijen uit de **log4jLogs** tabel met **[fout]**, en vervolgens voegt u de gegevens in de **foutenlogboeken** tabel.</span><span class="sxs-lookup"><span data-stu-id="ebbad-224">`INSERT OVERWRITE ... SELECT`: Selects rows from the **log4jLogs** table that contains **[ERROR]**, and then inserts the data into the **errorLogs** table.</span></span>

> [!NOTE]
> <span data-ttu-id="ebbad-225">In tegenstelling tot externe tabellen verwijdert voor het verwijderen van een interne tabel tevens de onderliggende gegevens.</span><span class="sxs-lookup"><span data-stu-id="ebbad-225">Unlike external tables, dropping an internal table also deletes the underlying data.</span></span>

## <a name="improve-hive-query-performance"></a><span data-ttu-id="ebbad-226">Hive-query's sneller</span><span class="sxs-lookup"><span data-stu-id="ebbad-226">Improve Hive query performance</span></span>

### <span data-ttu-id="ebbad-227"><a id="usetez"></a>Apache Tez</span><span class="sxs-lookup"><span data-stu-id="ebbad-227"><a id="usetez"></a>Apache Tez</span></span>

<span data-ttu-id="ebbad-228">[Apache Tez](http://tez.apache.org) ligt een framework dat kunt van gegevensintensieve toepassingen, zoals Hive, om u te veel efficiënter op schaal worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ebbad-228">[Apache Tez](http://tez.apache.org) is a framework that allows data intensive applications, such as Hive, to run much more efficiently at scale.</span></span> <span data-ttu-id="ebbad-229">Tez is standaard ingeschakeld voor Linux gebaseerde HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="ebbad-229">Tez is enabled by default for Linux-based HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="ebbad-230">Tez is momenteel uitgeschakeld voor Windows gebaseerde HDInsight-clusters standaard en moet zijn ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="ebbad-230">Tez is currently off by default for Windows-based HDInsight clusters and it must be enabled.</span></span> <span data-ttu-id="ebbad-231">Om te profiteren van Tez, moet de volgende waarde worden ingesteld voor een Hive-query:</span><span class="sxs-lookup"><span data-stu-id="ebbad-231">To take advantage of Tez, the following value must be set for a Hive query:</span></span>
>
> `set hive.execution.engine=tez;`
>
> <span data-ttu-id="ebbad-232">Tez is de standaard-engine voor Linux gebaseerde HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="ebbad-232">Tez is the default engine for Linux-based HDInsight clusters.</span></span>

<span data-ttu-id="ebbad-233">De [Hive op Tez-Ontwerpdocumenten](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) bevat details over de implementatie keuzen en afstemmen configuraties.</span><span class="sxs-lookup"><span data-stu-id="ebbad-233">The [Hive on Tez design documents](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contains details about the implementation choices and tuning configurations.</span></span>

<span data-ttu-id="ebbad-234">Om u te helpen bij foutopsporing taken uitgevoerd met Tez, HDInsight biedt de volgende web UI's waarmee u details wilt weergeven van Tez-taken:</span><span class="sxs-lookup"><span data-stu-id="ebbad-234">To aid in debugging jobs ran using Tez, HDInsight provides the following web UIs that allow you to view details of Tez jobs:</span></span>

* [<span data-ttu-id="ebbad-235">De weergave Ambari Tez op Linux gebaseerde HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="ebbad-235">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

* [<span data-ttu-id="ebbad-236">De Tez-gebruikersinterface op HDInsight op basis van Windows gebruiken</span><span class="sxs-lookup"><span data-stu-id="ebbad-236">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a><span data-ttu-id="ebbad-237">Lage latentie Analytical Processing (LLAP)</span><span class="sxs-lookup"><span data-stu-id="ebbad-237">Low Latency Analytical Processing (LLAP)</span></span>

<span data-ttu-id="ebbad-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (soms ook wel lange Live en proces) is een nieuwe functie in Hive 2.0 waarmee de caching van query's in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="ebbad-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (sometimes known as Live Long and Process) is a new feature in Hive 2.0 that allows in-memory caching of queries.</span></span> <span data-ttu-id="ebbad-239">LLAP maakt Hive-query's sneller tot [26 x sneller dan Hive 1.x in sommige gevallen](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span><span class="sxs-lookup"><span data-stu-id="ebbad-239">LLAP makes Hive queries much faster, up to [26x faster than Hive 1.x in some cases](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span></span>

<span data-ttu-id="ebbad-240">HDInsight biedt LLAP in het cluster interactieve Hive-type.</span><span class="sxs-lookup"><span data-stu-id="ebbad-240">HDInsight provides LLAP in the Interactive Hive cluster type.</span></span> <span data-ttu-id="ebbad-241">Zie voor meer informatie de [beginnen met een interactieve Hive](hdinsight-hadoop-use-interactive-hive.md) document.</span><span class="sxs-lookup"><span data-stu-id="ebbad-241">For more information, see the [Start with Interactive Hive](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

## <a name="hive-jobs-and-sql-server-integration-services"></a><span data-ttu-id="ebbad-242">Hive-taken en SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="ebbad-242">Hive jobs and SQL Server Integration Services</span></span>

<span data-ttu-id="ebbad-243">SQL Server Integration Services (SSIS) kunt u een Hive-taak uitvoert.</span><span class="sxs-lookup"><span data-stu-id="ebbad-243">You can use SQL Server Integration Services (SSIS) to run a Hive job.</span></span> <span data-ttu-id="ebbad-244">Het Azure-functiepakket voor SSIS biedt de volgende onderdelen die met Hive-taken in HDInsight werken.</span><span class="sxs-lookup"><span data-stu-id="ebbad-244">The Azure Feature Pack for SSIS provides the following components that work with Hive jobs on HDInsight.</span></span>

* <span data-ttu-id="ebbad-245">[Azure HDInsight Hive-taak][hivetask]</span><span class="sxs-lookup"><span data-stu-id="ebbad-245">[Azure HDInsight Hive Task][hivetask]</span></span>

* <span data-ttu-id="ebbad-246">[Azure abonnement Verbindingsbeheer][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="ebbad-246">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="ebbad-247">Meer informatie over het Azure Feature Pack voor SSIS [hier][ssispack].</span><span class="sxs-lookup"><span data-stu-id="ebbad-247">Learn more about the Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="ebbad-248"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ebbad-248"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="ebbad-249">Nu u weet wat Hive is en het gebruik ervan met Hadoop in HDInsight, gebruiken de volgende koppelingen om te verkennen andere manieren om te werken met Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ebbad-249">Now that you've learned what Hive is and how to use it with Hadoop in HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* <span data-ttu-id="ebbad-250">[Gegevens uploaden naar HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="ebbad-250">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="ebbad-251">[Pig gebruiken met HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="ebbad-251">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="ebbad-252">[MapReduce-taken gebruiken met HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="ebbad-252">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/
[hivetask]: http://msdn.microsoft.com/library/mt146771(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx

[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md


[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx
