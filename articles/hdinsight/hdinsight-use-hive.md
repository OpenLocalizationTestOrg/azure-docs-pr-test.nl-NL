---
title: aaaWhat is Apache Hive en HiveQL - Azure HDInsight | Microsoft Docs
description: Apache Hive is een systeem voor het datawarehouse van gegevens voor Hadoop. U kunt de gegevens die zijn opgeslagen in HiveQL, welke vergelijkbaar tooTransact-SQL met Hive query. In dit document leest u hoe toouse Hive en HiveQL met Azure HDInsight.
keywords: hiveql, wat is er hive, hadoop hiveql, hoe toouse hive, informatie over hive, wat is er hive
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
ms.openlocfilehash: a2772312263895ff99b499898264c2e6d5e816e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a><span data-ttu-id="142b4-106">Wat is Apache Hive en HiveQL in Azure HDInsight?</span><span class="sxs-lookup"><span data-stu-id="142b4-106">What is Apache Hive and HiveQL on Azure HDInsight?</span></span>

<span data-ttu-id="142b4-107">[Apache Hive](http://hive.apache.org/) is een systeem voor het datawarehouse van gegevens voor Hadoop.</span><span class="sxs-lookup"><span data-stu-id="142b4-107">[Apache Hive](http://hive.apache.org/) is a data warehouse system for Hadoop.</span></span> <span data-ttu-id="142b4-108">Hive kunt gegevenssamenvatting, query's en analyse van gegevens.</span><span class="sxs-lookup"><span data-stu-id="142b4-108">Hive enables data summarization, querying, and analysis of data.</span></span> <span data-ttu-id="142b4-109">Hive-query's zijn geschreven in HiveQL die een vergelijkbare tooSQL voor query-taal.</span><span class="sxs-lookup"><span data-stu-id="142b4-109">Hive queries are written in HiveQL, which is a query language similar tooSQL.</span></span>

<span data-ttu-id="142b4-110">Hive kunt u tooproject structuur op grotendeels ongestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="142b4-110">Hive allows you tooproject structure on largely unstructured data.</span></span> <span data-ttu-id="142b4-111">Nadat u de structuur Hallo gedefinieerd, kunt u HiveQL tooquery Hallo gegevens zonder kennis van Java of MapReduce.</span><span class="sxs-lookup"><span data-stu-id="142b4-111">After you define hello structure, you can use HiveQL tooquery hello data without knowledge of Java or MapReduce.</span></span>

<span data-ttu-id="142b4-112">HDInsight biedt verschillende clustertypen die zijn afgestemd op specifieke werkbelasting in gedachten.</span><span class="sxs-lookup"><span data-stu-id="142b4-112">HDInsight provides several cluster types, which are tuned for specific workloads.</span></span> <span data-ttu-id="142b4-113">Hallo na clustertypen worden meestal gebruikt voor Hive-query's:</span><span class="sxs-lookup"><span data-stu-id="142b4-113">hello following cluster types are most often used for Hive queries:</span></span>

* <span data-ttu-id="142b4-114">__Interactieve Hive__: een Hadoop-cluster waarmee [lage latentie analytische verwerking (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) functionaliteit tooimprove responstijden voor interactieve query's.</span><span class="sxs-lookup"><span data-stu-id="142b4-114">__Interactive Hive__: A Hadoop cluster that provides [Low Latency Analytical Processing (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) functionality tooimprove response times for interactive queries.</span></span> <span data-ttu-id="142b4-115">Zie voor meer informatie, Hallo [beginnen met een interactieve Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md) document.</span><span class="sxs-lookup"><span data-stu-id="142b4-115">For more information, see hello [Start with Interactive Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

* <span data-ttu-id="142b4-116">__Hadoop__: een Hadoop-cluster dat is afgestemd op batchverwerking werkbelastingen.</span><span class="sxs-lookup"><span data-stu-id="142b4-116">__Hadoop__: A Hadoop cluster that is tuned for batch processing workloads.</span></span> <span data-ttu-id="142b4-117">Zie voor meer informatie, Hallo [starten met Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) document.</span><span class="sxs-lookup"><span data-stu-id="142b4-117">For more information, see hello [Start with Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) document.</span></span>

* <span data-ttu-id="142b4-118">__Spark__: Apache Spark zijn ingebouwde functionaliteit voor het werken met Hive.</span><span class="sxs-lookup"><span data-stu-id="142b4-118">__Spark__: Apache Spark has built-in functionality for working with Hive.</span></span> <span data-ttu-id="142b4-119">Zie voor meer informatie, Hallo [beginnen met Spark in HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) document.</span><span class="sxs-lookup"><span data-stu-id="142b4-119">For more information, see hello [Start with Spark on HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) document.</span></span>

* <span data-ttu-id="142b4-120">__HBase__: HiveQL gebruikte tooquery opgeslagen gegevens in HBase kan worden.</span><span class="sxs-lookup"><span data-stu-id="142b4-120">__HBase__: HiveQL can be used tooquery data stored in HBase.</span></span> <span data-ttu-id="142b4-121">Zie voor meer informatie, Hallo [beginnen met HBase in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) document.</span><span class="sxs-lookup"><span data-stu-id="142b4-121">For more information, see hello [Start with HBase on HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) document.</span></span>

## <a name="how-toouse-hive"></a><span data-ttu-id="142b4-122">Hoe toouse Hive</span><span class="sxs-lookup"><span data-stu-id="142b4-122">How toouse Hive</span></span>

<span data-ttu-id="142b4-123">Gebruik Hallo tabel toodiscover hoe toouse Hive met HDInsight te volgen:</span><span class="sxs-lookup"><span data-stu-id="142b4-123">Use hello following table toodiscover how toouse Hive with HDInsight:</span></span>

| <span data-ttu-id="142b4-124">**Gebruik deze methode** als u wilt dat...</span><span class="sxs-lookup"><span data-stu-id="142b4-124">**Use this method** if you want...</span></span> | <span data-ttu-id="142b4-125">.. .an **interactieve** shell</span><span class="sxs-lookup"><span data-stu-id="142b4-125">...an **interactive** shell</span></span> | <span data-ttu-id="142b4-126">... **batch** verwerken</span><span class="sxs-lookup"><span data-stu-id="142b4-126">...**batch** processing</span></span> | <span data-ttu-id="142b4-127">.. .door dit **cluster-besturingssysteem**</span><span class="sxs-lookup"><span data-stu-id="142b4-127">...with this **cluster operating system**</span></span> | <span data-ttu-id="142b4-128">.. .from dit **clientbesturingssysteem**</span><span class="sxs-lookup"><span data-stu-id="142b4-128">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="142b4-129">Hive-weergave</span><span class="sxs-lookup"><span data-stu-id="142b4-129">Hive View</span></span>](hdinsight-hadoop-use-hive-ambari-view.md) |<span data-ttu-id="142b4-130">✔</span><span class="sxs-lookup"><span data-stu-id="142b4-130">✔</span></span> |<span data-ttu-id="142b4-131">✔</span><span class="sxs-lookup"><span data-stu-id="142b4-131">✔</span></span> |<span data-ttu-id="142b4-132">Linux</span><span class="sxs-lookup"><span data-stu-id="142b4-132">Linux</span></span> |<span data-ttu-id="142b4-133">(Browser gebaseerd)</span><span class="sxs-lookup"><span data-stu-id="142b4-133">Any (browser based)</span></span> |
| [<span data-ttu-id="142b4-134">Beeline client</span><span class="sxs-lookup"><span data-stu-id="142b4-134">Beeline client</span></span>](hdinsight-hadoop-use-hive-beeline.md) |<span data-ttu-id="142b4-135">✔</span><span class="sxs-lookup"><span data-stu-id="142b4-135">✔</span></span> |<span data-ttu-id="142b4-136">✔</span><span class="sxs-lookup"><span data-stu-id="142b4-136">✔</span></span> |<span data-ttu-id="142b4-137">Linux</span><span class="sxs-lookup"><span data-stu-id="142b4-137">Linux</span></span> |<span data-ttu-id="142b4-138">Linux, Unix, Mac OS X of Windows</span><span class="sxs-lookup"><span data-stu-id="142b4-138">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="142b4-139">REST API</span><span class="sxs-lookup"><span data-stu-id="142b4-139">REST API</span></span>](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |<span data-ttu-id="142b4-140">✔</span><span class="sxs-lookup"><span data-stu-id="142b4-140">✔</span></span> |<span data-ttu-id="142b4-141">Linux- of Windows *</span><span class="sxs-lookup"><span data-stu-id="142b4-141">Linux or Windows*</span></span> |<span data-ttu-id="142b4-142">Linux, Unix, Mac OS X of Windows</span><span class="sxs-lookup"><span data-stu-id="142b4-142">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="142b4-143">HDInsight tools voor Visual Studio</span><span class="sxs-lookup"><span data-stu-id="142b4-143">HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |<span data-ttu-id="142b4-144">✔</span><span class="sxs-lookup"><span data-stu-id="142b4-144">✔</span></span> |<span data-ttu-id="142b4-145">Linux- of Windows *</span><span class="sxs-lookup"><span data-stu-id="142b4-145">Linux or Windows*</span></span> |<span data-ttu-id="142b4-146">Windows</span><span class="sxs-lookup"><span data-stu-id="142b4-146">Windows</span></span> |
| [<span data-ttu-id="142b4-147">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="142b4-147">Windows PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |<span data-ttu-id="142b4-148">✔</span><span class="sxs-lookup"><span data-stu-id="142b4-148">✔</span></span> |<span data-ttu-id="142b4-149">Linux- of Windows *</span><span class="sxs-lookup"><span data-stu-id="142b4-149">Linux or Windows*</span></span> |<span data-ttu-id="142b4-150">Windows</span><span class="sxs-lookup"><span data-stu-id="142b4-150">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="142b4-151">\*Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="142b4-151">\* Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="142b4-152">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="142b4-152">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="142b4-153">Als u een cluster met HDInsight op basis van Windows gebruikt, kunt u Hallo [Query console](hdinsight-hadoop-use-hive-query-console.md) vanuit de browser of [extern bureaublad](hdinsight-hadoop-use-hive-remote-desktop.md) toorun Hive-query's.</span><span class="sxs-lookup"><span data-stu-id="142b4-153">If you are using a Windows-based HDInsight cluster, you can use hello [Query console](hdinsight-hadoop-use-hive-query-console.md) from your browser or [Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md) toorun Hive queries.</span></span>

## <a name="hiveql-language-reference"></a><span data-ttu-id="142b4-154">HiveQL-taalreferentie</span><span class="sxs-lookup"><span data-stu-id="142b4-154">HiveQL language reference</span></span>

<span data-ttu-id="142b4-155">Taalreferentie HiveQL is beschikbaar in Hallo [taal handmatig (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span><span class="sxs-lookup"><span data-stu-id="142b4-155">HiveQL language reference is available in hello [language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span></span>

## <a name="hive-and-data-structure"></a><span data-ttu-id="142b4-156">Structuur van hive en gegevens</span><span class="sxs-lookup"><span data-stu-id="142b4-156">Hive and data structure</span></span>

<span data-ttu-id="142b4-157">Hive begrijpt hoe toowork met gestructureerd en semi-gestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="142b4-157">Hive understands how toowork with structured and semi-structured data.</span></span> <span data-ttu-id="142b4-158">Bijvoorbeeld: tekstbestanden waar Hallo velden worden gescheiden door specifieke tekens.</span><span class="sxs-lookup"><span data-stu-id="142b4-158">For example, text files where hello fields are delimited by specific characters.</span></span> <span data-ttu-id="142b4-159">Hallo volgende HiveQL-instructie maakt een tabel door spaties gescheiden gegevens:</span><span class="sxs-lookup"><span data-stu-id="142b4-159">hello following HiveQL statement creates a table over space-delimited data:</span></span>

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

<span data-ttu-id="142b4-160">Hive biedt ook ondersteuning voor aangepaste **serialisatiefunctie/deserializers (serde-schrijfbewerking)** voor complexe of onregelmatig gestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="142b4-160">Hive also supports custom **serializer/deserializers (SerDe)** for complex or irregularly structured data.</span></span> <span data-ttu-id="142b4-161">Zie voor meer informatie, Hallo [hoe een aangepaste JSON serde-schrijfbewerking met HDInsight toouse](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.</span><span class="sxs-lookup"><span data-stu-id="142b4-161">For more information, see hello [How toouse a custom JSON SerDe with HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.</span></span>

<span data-ttu-id="142b4-162">Zie voor meer informatie over ondersteunde bestandsindelingen in Hive Hallo [taal handmatig (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span><span class="sxs-lookup"><span data-stu-id="142b4-162">For more information on file formats supported by Hive, see hello [Language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span></span>

## <a name="hive-internal-tables-vs-external-tables"></a><span data-ttu-id="142b4-163">Interne tabellen tegenover externe tabellen hive</span><span class="sxs-lookup"><span data-stu-id="142b4-163">Hive internal tables vs external tables</span></span>

<span data-ttu-id="142b4-164">Er zijn twee soorten tabellen die u met Hive maken kunt:</span><span class="sxs-lookup"><span data-stu-id="142b4-164">There are two types of tables that you can create with Hive:</span></span>

* <span data-ttu-id="142b4-165">__Interne__: gegevens worden opgeslagen in Hallo Hive-datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="142b4-165">__Internal__: Data is stored in hello Hive data warehouse.</span></span> <span data-ttu-id="142b4-166">Hallo datawarehouse bevindt zich op `/hive/warehouse/` op Hallo standaard opslag voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="142b4-166">hello data warehouse is located at `/hive/warehouse/` on hello default storage for hello cluster.</span></span>

    <span data-ttu-id="142b4-167">Gebruik interne tabellen wanneer:</span><span class="sxs-lookup"><span data-stu-id="142b4-167">Use internal tables when:</span></span>

    * <span data-ttu-id="142b4-168">Gegevens is tijdelijk.</span><span class="sxs-lookup"><span data-stu-id="142b4-168">Data is temporary.</span></span>
    * <span data-ttu-id="142b4-169">Wilt u Hive toomanage Hallo levenscyclus van Hallo tabel en gegevens.</span><span class="sxs-lookup"><span data-stu-id="142b4-169">You want Hive toomanage hello lifecycle of hello table and data.</span></span>

* <span data-ttu-id="142b4-170">__Externe__: gegevens worden opgeslagen buiten het Hallo-datawarehouse.</span><span class="sxs-lookup"><span data-stu-id="142b4-170">__External__: Data is stored outside hello data warehouse.</span></span> <span data-ttu-id="142b4-171">Hallo-gegevens kunnen worden opgeslagen op opslag die toegankelijk is door Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="142b4-171">hello data can be stored on any storage accessible by hello cluster.</span></span>

    <span data-ttu-id="142b4-172">Gebruik externe tabellen wanneer:</span><span class="sxs-lookup"><span data-stu-id="142b4-172">Use external tables when:</span></span>

    * <span data-ttu-id="142b4-173">Hallo-gegevens worden ook gebruikt buiten Hive.</span><span class="sxs-lookup"><span data-stu-id="142b4-173">hello data is also used outside of Hive.</span></span> <span data-ttu-id="142b4-174">Bijvoorbeeld zijn Hallo-gegevensbestanden bijgewerkt door een ander proces (die wordt niet vergrendeld Hallo-bestanden.)</span><span class="sxs-lookup"><span data-stu-id="142b4-174">For example, hello data files are updated by another process (that does not lock hello files.)</span></span>
    * <span data-ttu-id="142b4-175">Gegevens moeten tooremain in Hallo onderliggende locatie, zelfs na het Hallo-tabel verwijderen.</span><span class="sxs-lookup"><span data-stu-id="142b4-175">Data needs tooremain in hello underlying location, even after dropping hello table.</span></span>
    * <span data-ttu-id="142b4-176">U moet een aangepaste locatie, zoals een niet-standaard opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="142b4-176">You need a custom location, such as a non-default storage account.</span></span>
    * <span data-ttu-id="142b4-177">Een ander programma dan hive beheert gegevensindeling hello, locatie, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="142b4-177">A program other than hive manages hello data format, location, etc.</span></span>

<span data-ttu-id="142b4-178">Zie voor meer informatie, Hallo [Hive interne en externe tabellen Intro] [ cindygross-hive-tables] blogbericht.</span><span class="sxs-lookup"><span data-stu-id="142b4-178">For more information, see hello [Hive Internal and External Tables Intro][cindygross-hive-tables] blog post.</span></span>

## <a name="user-defined-functions-udf"></a><span data-ttu-id="142b4-179">Gebruiker gedefinieerde functies (UDF)</span><span class="sxs-lookup"><span data-stu-id="142b4-179">User-defined functions (UDF)</span></span>

<span data-ttu-id="142b4-180">Hive kan verder worden uitgebreid via **gebruiker gedefinieerde functies (UDF)**.</span><span class="sxs-lookup"><span data-stu-id="142b4-180">Hive can also be extended through **user-defined functions (UDF)**.</span></span> <span data-ttu-id="142b4-181">Een UDF kunt u de functionaliteit van tooimplement of logica die eenvoudig niet is gemodelleerd in HiveQL.</span><span class="sxs-lookup"><span data-stu-id="142b4-181">A UDF allows you tooimplement functionality or logic that isn't easily modeled in HiveQL.</span></span> <span data-ttu-id="142b4-182">Zie voor een voorbeeld van het gebruik van UDF's met Hive Hallo documenten te volgen:</span><span class="sxs-lookup"><span data-stu-id="142b4-182">For an example of using UDFs with Hive, see hello following documents:</span></span>

* [<span data-ttu-id="142b4-183">Een Java door de gebruiker gedefinieerde functie gebruiken met Hive</span><span class="sxs-lookup"><span data-stu-id="142b4-183">Use a Java user-defined function with Hive</span></span>](hdinsight-hadoop-hive-java-udf.md)

* [<span data-ttu-id="142b4-184">Een Python door de gebruiker gedefinieerde functie gebruiken met Hive en Pig</span><span class="sxs-lookup"><span data-stu-id="142b4-184">Use a Python user-defined function with Hive and Pig</span></span>](hdinsight-python.md)

* [<span data-ttu-id="142b4-185">Een C# gebruiker gedefinieerde functie gebruiken met Hive en Pig</span><span class="sxs-lookup"><span data-stu-id="142b4-185">Use a C# user-defined function with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="142b4-186">Hoe de gebruiker gedefinieerde aangepaste component tooadd tooHDInsight functioneren</span><span class="sxs-lookup"><span data-stu-id="142b4-186">How tooadd a custom Hive user-defined function tooHDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [<span data-ttu-id="142b4-187">Een voorbeeld Hive gebruiker gedefinieerde functie tooconvert datum-/ tijdnotaties tooHive tijdstempel</span><span class="sxs-lookup"><span data-stu-id="142b4-187">An example Hive user-defined function tooconvert date/time formats tooHive timestamp</span></span>](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <span data-ttu-id="142b4-188"><a id="data"></a>Voorbeeldgegevens</span><span class="sxs-lookup"><span data-stu-id="142b4-188"><a id="data"></a>Example data</span></span>

<span data-ttu-id="142b4-189">Hive in HDInsight wordt vooraf geladen geleverd met een interne tabel met de naam `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="142b4-189">Hive on HDInsight comes pre-loaded with an internal table named `hivesampletable`.</span></span> <span data-ttu-id="142b4-190">HDInsight biedt ook een voorbeeld van gegevenssets die kunnen worden gebruikt met Hive.</span><span class="sxs-lookup"><span data-stu-id="142b4-190">HDInsight also provides example data sets that can be used with Hive.</span></span> <span data-ttu-id="142b4-191">Deze gegevenssets worden opgeslagen in Hallo `/example/data` en `/HdiSamples` mappen.</span><span class="sxs-lookup"><span data-stu-id="142b4-191">These data sets are stored in hello `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="142b4-192">Deze mappen aanwezig zijn in Hallo standaard opslagruimte voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="142b4-192">These directories exist in hello default storage for your cluster.</span></span>

## <span data-ttu-id="142b4-193"><a id="job"></a>Voorbeeld van de Hive-query</span><span class="sxs-lookup"><span data-stu-id="142b4-193"><a id="job"></a>Example Hive query</span></span>

<span data-ttu-id="142b4-194">Hallo volgende HiveQL-instructies projectkolommen op Hallo `/example/data/sample.log` bestand:</span><span class="sxs-lookup"><span data-stu-id="142b4-194">hello following HiveQL statements project columns onto hello `/example/data/sample.log` file:</span></span>

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

<span data-ttu-id="142b4-195">In het vorige voorbeeld hello Voer Hallo HiveQL-instructies Hallo van de volgende activiteiten:</span><span class="sxs-lookup"><span data-stu-id="142b4-195">In hello previous example, hello HiveQL statements perform hello following actions:</span></span>

* <span data-ttu-id="142b4-196">`set hive.execution.engine=tez;`: Sets Hallo uitvoering engine toouse Tez.</span><span class="sxs-lookup"><span data-stu-id="142b4-196">`set hive.execution.engine=tez;`: Sets hello execution engine toouse Tez.</span></span> <span data-ttu-id="142b4-197">Tez gebruik in plaats van MapReduce krijgt u een toename van de prestaties van query's.</span><span class="sxs-lookup"><span data-stu-id="142b4-197">Using Tez instead of MapReduce can provide an increase in query performance.</span></span> <span data-ttu-id="142b4-198">Zie voor meer informatie over Tez hello [Apache Tez gebruiken voor betere prestaties](#usetez) sectie.</span><span class="sxs-lookup"><span data-stu-id="142b4-198">For more information on Tez, see hello [Use Apache Tez for improved performance](#usetez) section.</span></span>

    > [!NOTE]
    > <span data-ttu-id="142b4-199">Deze instructie is alleen vereist wanneer u een HDInsight op basis van Windows-cluster.</span><span class="sxs-lookup"><span data-stu-id="142b4-199">This statement is only required when using a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="142b4-200">Tez is Hallo standaard engine voor het uitvoeren voor HDInsight op basis van Linux.</span><span class="sxs-lookup"><span data-stu-id="142b4-200">Tez is hello default execution engine for Linux-based HDInsight.</span></span>

* <span data-ttu-id="142b4-201">`DROP TABLE`: Als Hallo tabel al bestaat, verwijderen.</span><span class="sxs-lookup"><span data-stu-id="142b4-201">`DROP TABLE`: If hello table already exists, delete it.</span></span>

* <span data-ttu-id="142b4-202">`CREATE EXTERNAL TABLE`: Hiermee maakt u een nieuw **externe** tabel in Hive.</span><span class="sxs-lookup"><span data-stu-id="142b4-202">`CREATE EXTERNAL TABLE`: Creates a new **external** table in Hive.</span></span> <span data-ttu-id="142b4-203">De tabeldefinitie Hallo opslaan externe tabellen alleen in Hive.</span><span class="sxs-lookup"><span data-stu-id="142b4-203">External tables only store hello table definition in Hive.</span></span> <span data-ttu-id="142b4-204">in de oorspronkelijke locatie hello en in de oorspronkelijke indeling Hallo Hallo gegevens blijft.</span><span class="sxs-lookup"><span data-stu-id="142b4-204">hello data is left in hello original location and in hello original format.</span></span>

* <span data-ttu-id="142b4-205">`ROW FORMAT`: Hiermee geeft u Hive hoe Hallo gegevens wordt opgemaakt.</span><span class="sxs-lookup"><span data-stu-id="142b4-205">`ROW FORMAT`: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="142b4-206">In dit geval worden Hallo velden in elk logboek gescheiden door een spatie.</span><span class="sxs-lookup"><span data-stu-id="142b4-206">In this case, hello fields in each log are separated by a space.</span></span>

* <span data-ttu-id="142b4-207">`STORED AS TEXTFILE LOCATION`: Vertelt Hive waar hello gegevens worden opgeslagen (Hallo `example/data` directory) en dat deze is opgeslagen als tekst.</span><span class="sxs-lookup"><span data-stu-id="142b4-207">`STORED AS TEXTFILE LOCATION`: Tells Hive where hello data is stored (hello `example/data` directory) and that it is stored as text.</span></span> <span data-ttu-id="142b4-208">Hallo-gegevens worden in één bestand of verdeeld over meerdere bestanden binnen Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="142b4-208">hello data can be in one file or spread across multiple files within hello directory.</span></span>

* <span data-ttu-id="142b4-209">`SELECT`: Hiermee selecteert u een telling van alle rijen waarin hello kolom **t4** Hallo waarde bevat **[fout]**.</span><span class="sxs-lookup"><span data-stu-id="142b4-209">`SELECT`: Selects a count of all rows where hello column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="142b4-210">Deze instructie retourneert een waarde van **3** omdat er drie rijen met deze waarde.</span><span class="sxs-lookup"><span data-stu-id="142b4-210">This statement returns a value of **3** because there are three rows that contain this value.</span></span>

* <span data-ttu-id="142b4-211">`INPUT__FILE__NAME LIKE '%.log'`-Hive probeert tooapply hello tooall schemabestanden in Hallo-directory.</span><span class="sxs-lookup"><span data-stu-id="142b4-211">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts tooapply hello schema tooall files in hello directory.</span></span> <span data-ttu-id="142b4-212">In dit geval bevat Hallo map bestanden die niet overeenkomen met de Hallo schema.</span><span class="sxs-lookup"><span data-stu-id="142b4-212">In this case, hello directory contains files that do not match hello schema.</span></span> <span data-ttu-id="142b4-213">tooprevent garbagecollection gegevens in de resultaten van de hello, deze instructie Hive vertelt dat we alleen gegevens uit bestanden eindigt op moet retourneren. log.</span><span class="sxs-lookup"><span data-stu-id="142b4-213">tooprevent garbage data in hello results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

> [!NOTE]
> <span data-ttu-id="142b4-214">Externe tabellen moeten worden gebruikt wanneer u van plan Hallo onderliggende gegevens toobe bijgewerkt door een externe bron bent.</span><span class="sxs-lookup"><span data-stu-id="142b4-214">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="142b4-215">Bijvoorbeeld, een geautomatiseerd proces of MapReduce-bewerking uploaden.</span><span class="sxs-lookup"><span data-stu-id="142b4-215">For example, an automated data upload process, or MapReduce operation.</span></span>
>
> <span data-ttu-id="142b4-216">Verwijderen van een externe tabel komt **niet** Hallo-gegevens verwijderen Hallo tabeldefinitie alleen worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="142b4-216">Dropping an external table does **not** delete hello data, it only deletes hello table definition.</span></span>

<span data-ttu-id="142b4-217">toocreate een **interne** in plaats van de externe tabel, gebruikt u Hallo HiveQL te volgen:</span><span class="sxs-lookup"><span data-stu-id="142b4-217">toocreate an **internal** table instead of external, use hello following HiveQL:</span></span>

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

<span data-ttu-id="142b4-218">Deze instructies uitvoeren Hallo volgende acties:</span><span class="sxs-lookup"><span data-stu-id="142b4-218">These statements perform hello following actions:</span></span>

* <span data-ttu-id="142b4-219">`CREATE TABLE IF NOT EXISTS`: Als Hallo tabel niet bestaat, maken.</span><span class="sxs-lookup"><span data-stu-id="142b4-219">`CREATE TABLE IF NOT EXISTS`: If hello table does not exist, create it.</span></span> <span data-ttu-id="142b4-220">Omdat Hallo **externe** trefwoord wordt niet gebruikt, wordt deze instructie maakt u een interne tabel.</span><span class="sxs-lookup"><span data-stu-id="142b4-220">Because hello **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="142b4-221">Hallo-tabel is opgeslagen in Hallo Hive-datawarehouse en volledig wordt beheerd door Hive.</span><span class="sxs-lookup"><span data-stu-id="142b4-221">hello table is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

* <span data-ttu-id="142b4-222">`STORED AS ORC`: Het Hallo-gegevens opslaat in geoptimaliseerd rij kolommen (ORC)-indeling.</span><span class="sxs-lookup"><span data-stu-id="142b4-222">`STORED AS ORC`: Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="142b4-223">ORC is een maximaal geoptimaliseerd en efficiënte indeling voor het opslaan van gegevens met Hive.</span><span class="sxs-lookup"><span data-stu-id="142b4-223">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

* <span data-ttu-id="142b4-224">`INSERT OVERWRITE ... SELECT`: Rijen uit Hallo geselecteerd **log4jLogs** tabel met **[fout]**, en vervolgens voegt de gegevens in Hallo Hallo **foutenlogboeken** tabel.</span><span class="sxs-lookup"><span data-stu-id="142b4-224">`INSERT OVERWRITE ... SELECT`: Selects rows from hello **log4jLogs** table that contains **[ERROR]**, and then inserts hello data into hello **errorLogs** table.</span></span>

> [!NOTE]
> <span data-ttu-id="142b4-225">In tegenstelling tot externe tabellen verwijderd voor het verwijderen van een interne tabel ook Hallo onderliggende gegevens.</span><span class="sxs-lookup"><span data-stu-id="142b4-225">Unlike external tables, dropping an internal table also deletes hello underlying data.</span></span>

## <a name="improve-hive-query-performance"></a><span data-ttu-id="142b4-226">Hive-query's sneller</span><span class="sxs-lookup"><span data-stu-id="142b4-226">Improve Hive query performance</span></span>

### <span data-ttu-id="142b4-227"><a id="usetez"></a>Apache Tez</span><span class="sxs-lookup"><span data-stu-id="142b4-227"><a id="usetez"></a>Apache Tez</span></span>

<span data-ttu-id="142b4-228">[Apache Tez](http://tez.apache.org) ligt een framework dat kunt van gegevensintensieve toepassingen, zoals Hive, toorun veel efficiënter op schaal.</span><span class="sxs-lookup"><span data-stu-id="142b4-228">[Apache Tez](http://tez.apache.org) is a framework that allows data intensive applications, such as Hive, toorun much more efficiently at scale.</span></span> <span data-ttu-id="142b4-229">Tez is standaard ingeschakeld voor Linux gebaseerde HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="142b4-229">Tez is enabled by default for Linux-based HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="142b4-230">Tez is momenteel uitgeschakeld voor Windows gebaseerde HDInsight-clusters standaard en moet zijn ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="142b4-230">Tez is currently off by default for Windows-based HDInsight clusters and it must be enabled.</span></span> <span data-ttu-id="142b4-231">tootake profiteren van Tez, Hallo na de waarde moet worden ingesteld voor een Hive-query:</span><span class="sxs-lookup"><span data-stu-id="142b4-231">tootake advantage of Tez, hello following value must be set for a Hive query:</span></span>
>
> `set hive.execution.engine=tez;`
>
> <span data-ttu-id="142b4-232">Tez is Hallo standaard engine voor Linux gebaseerde HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="142b4-232">Tez is hello default engine for Linux-based HDInsight clusters.</span></span>

<span data-ttu-id="142b4-233">Hallo [Hive op Tez-Ontwerpdocumenten](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) bevat details over Hallo implementatie keuzen en afstemmen configuraties.</span><span class="sxs-lookup"><span data-stu-id="142b4-233">hello [Hive on Tez design documents](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contains details about hello implementation choices and tuning configurations.</span></span>

<span data-ttu-id="142b4-234">tooaid bij foutopsporing taken uitgevoerd met Tez, HDInsight biedt Hallo web UI's waarmee u tooview details van Tez-taken te volgen:</span><span class="sxs-lookup"><span data-stu-id="142b4-234">tooaid in debugging jobs ran using Tez, HDInsight provides hello following web UIs that allow you tooview details of Tez jobs:</span></span>

* [<span data-ttu-id="142b4-235">Hallo Ambari Tez weergave op Linux gebaseerde HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="142b4-235">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

* [<span data-ttu-id="142b4-236">Hallo Tez UI op HDInsight op basis van Windows gebruiken</span><span class="sxs-lookup"><span data-stu-id="142b4-236">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a><span data-ttu-id="142b4-237">Lage latentie Analytical Processing (LLAP)</span><span class="sxs-lookup"><span data-stu-id="142b4-237">Low Latency Analytical Processing (LLAP)</span></span>

<span data-ttu-id="142b4-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (soms ook wel lange Live en proces) is een nieuwe functie in Hive 2.0 waarmee de caching van query's in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="142b4-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (sometimes known as Live Long and Process) is a new feature in Hive 2.0 that allows in-memory caching of queries.</span></span> <span data-ttu-id="142b4-239">LLAP maakt Hive-query's sneller up te[26 x sneller dan Hive 1.x in sommige gevallen](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span><span class="sxs-lookup"><span data-stu-id="142b4-239">LLAP makes Hive queries much faster, up too[26x faster than Hive 1.x in some cases](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span></span>

<span data-ttu-id="142b4-240">HDInsight biedt LLAP Hallo clustertype interactieve Hive.</span><span class="sxs-lookup"><span data-stu-id="142b4-240">HDInsight provides LLAP in hello Interactive Hive cluster type.</span></span> <span data-ttu-id="142b4-241">Zie voor meer informatie, Hallo [beginnen met een interactieve Hive](hdinsight-hadoop-use-interactive-hive.md) document.</span><span class="sxs-lookup"><span data-stu-id="142b4-241">For more information, see hello [Start with Interactive Hive](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

## <a name="hive-jobs-and-sql-server-integration-services"></a><span data-ttu-id="142b4-242">Hive-taken en SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="142b4-242">Hive jobs and SQL Server Integration Services</span></span>

<span data-ttu-id="142b4-243">U kunt SQL Server Integration Services (SSIS) toorun een Hive-taak.</span><span class="sxs-lookup"><span data-stu-id="142b4-243">You can use SQL Server Integration Services (SSIS) toorun a Hive job.</span></span> <span data-ttu-id="142b4-244">Hello Azure Feature Pack voor SSIS biedt Hallo onderdelen die met Hive-taken in HDInsight werken te volgen.</span><span class="sxs-lookup"><span data-stu-id="142b4-244">hello Azure Feature Pack for SSIS provides hello following components that work with Hive jobs on HDInsight.</span></span>

* <span data-ttu-id="142b4-245">[Azure HDInsight Hive-taak][hivetask]</span><span class="sxs-lookup"><span data-stu-id="142b4-245">[Azure HDInsight Hive Task][hivetask]</span></span>

* <span data-ttu-id="142b4-246">[Azure abonnement Verbindingsbeheer][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="142b4-246">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="142b4-247">Meer informatie over Azure Feature Pack Hallo voor SSIS [hier][ssispack].</span><span class="sxs-lookup"><span data-stu-id="142b4-247">Learn more about hello Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="142b4-248"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="142b4-248"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="142b4-249">Nu dat u hebt geleerd wat Hive is en hoe toouse met Hadoop in HDInsight, gebruik Hallo volgen koppelingen tooexplore andere manieren toowork met Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="142b4-249">Now that you've learned what Hive is and how toouse it with Hadoop in HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* <span data-ttu-id="142b4-250">[Uploaden van gegevens tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="142b4-250">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="142b4-251">[Pig gebruiken met HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="142b4-251">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="142b4-252">[MapReduce-taken gebruiken met HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="142b4-252">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

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
