---
title: aaaUse Hadoop Pig in HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse varkens met Hadoop op HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: acfeb52b-4b81-4a7d-af77-3e9908407404
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 90850f2c742b8954c66ce277127e01b14fc3906f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a><span data-ttu-id="78469-103">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="78469-103">Use Pig with Hadoop on HDInsight</span></span>

<span data-ttu-id="78469-104">Meer informatie over hoe toouse [Apache Pig](http://pig.apache.org/) met HDInsight...</span><span class="sxs-lookup"><span data-stu-id="78469-104">Learn how toouse [Apache Pig](http://pig.apache.org/) with HDInsight...</span></span>

<span data-ttu-id="78469-105">Pig is een platform voor het maken van programma's voor Hadoop met behulp van een procedurele taal bekend als *Pig Latin*.</span><span class="sxs-lookup"><span data-stu-id="78469-105">Pig is a platform for creating programs for Hadoop by using a procedural language known as *Pig Latin*.</span></span> <span data-ttu-id="78469-106">Pig is een alternatieve tooJava voor het maken van *MapReduce* oplossingen en deze is opgenomen in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78469-106">Pig is an alternative tooJava for creating *MapReduce* solutions, and it is included with Azure HDInsight.</span></span> <span data-ttu-id="78469-107">Gebruik Hallo tabel toodiscover Hallo verschillende manieren waarop Pig kan worden gebruikt met HDInsight te volgen:</span><span class="sxs-lookup"><span data-stu-id="78469-107">Use hello following table toodiscover hello various ways that Pig can be used with HDInsight:</span></span>

| <span data-ttu-id="78469-108">**Gebruik deze** als u wilt dat...</span><span class="sxs-lookup"><span data-stu-id="78469-108">**Use this** if you want...</span></span> | <span data-ttu-id="78469-109">.. .an **interactieve** shell</span><span class="sxs-lookup"><span data-stu-id="78469-109">...an **interactive** shell</span></span> | <span data-ttu-id="78469-110">... **batch** verwerken</span><span class="sxs-lookup"><span data-stu-id="78469-110">...**batch** processing</span></span> | <span data-ttu-id="78469-111">.. .door dit **cluster-besturingssysteem**</span><span class="sxs-lookup"><span data-stu-id="78469-111">...with this **cluster operating system**</span></span> | <span data-ttu-id="78469-112">.. .from dit **clientbesturingssysteem**</span><span class="sxs-lookup"><span data-stu-id="78469-112">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="78469-113">SSH</span><span class="sxs-lookup"><span data-stu-id="78469-113">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="78469-114">✔</span><span class="sxs-lookup"><span data-stu-id="78469-114">✔</span></span> |<span data-ttu-id="78469-115">✔</span><span class="sxs-lookup"><span data-stu-id="78469-115">✔</span></span> |<span data-ttu-id="78469-116">Linux</span><span class="sxs-lookup"><span data-stu-id="78469-116">Linux</span></span> |<span data-ttu-id="78469-117">Linux, Unix, Mac OS X of Windows</span><span class="sxs-lookup"><span data-stu-id="78469-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="78469-118">REST API</span><span class="sxs-lookup"><span data-stu-id="78469-118">REST API</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="78469-119">✔</span><span class="sxs-lookup"><span data-stu-id="78469-119">✔</span></span> |<span data-ttu-id="78469-120">Linux- of Windows</span><span class="sxs-lookup"><span data-stu-id="78469-120">Linux or Windows</span></span> |<span data-ttu-id="78469-121">Linux, Unix, Mac OS X of Windows</span><span class="sxs-lookup"><span data-stu-id="78469-121">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="78469-122">.NET-SDK voor Hadoop</span><span class="sxs-lookup"><span data-stu-id="78469-122">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="78469-123">✔</span><span class="sxs-lookup"><span data-stu-id="78469-123">✔</span></span> |<span data-ttu-id="78469-124">Linux- of Windows</span><span class="sxs-lookup"><span data-stu-id="78469-124">Linux or Windows</span></span> |<span data-ttu-id="78469-125">Windows (voor nu)</span><span class="sxs-lookup"><span data-stu-id="78469-125">Windows (for now)</span></span> |
| [<span data-ttu-id="78469-126">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="78469-126">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="78469-127">✔</span><span class="sxs-lookup"><span data-stu-id="78469-127">✔</span></span> |<span data-ttu-id="78469-128">Linux- of Windows</span><span class="sxs-lookup"><span data-stu-id="78469-128">Linux or Windows</span></span> |<span data-ttu-id="78469-129">Windows</span><span class="sxs-lookup"><span data-stu-id="78469-129">Windows</span></span> |
| <span data-ttu-id="78469-130">[Extern bureaublad](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 en 3.3)</span><span class="sxs-lookup"><span data-stu-id="78469-130">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="78469-131">✔</span><span class="sxs-lookup"><span data-stu-id="78469-131">✔</span></span> |<span data-ttu-id="78469-132">✔</span><span class="sxs-lookup"><span data-stu-id="78469-132">✔</span></span> |<span data-ttu-id="78469-133">Windows</span><span class="sxs-lookup"><span data-stu-id="78469-133">Windows</span></span> |<span data-ttu-id="78469-134">Windows</span><span class="sxs-lookup"><span data-stu-id="78469-134">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="78469-135">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="78469-135">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="78469-136">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="78469-136">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="78469-137"><a id="why"></a>Waarom Pig gebruiken</span><span class="sxs-lookup"><span data-stu-id="78469-137"><a id="why"></a>Why use Pig</span></span>

<span data-ttu-id="78469-138">Een van Hallo uitdagingen bij het verwerken van gegevens met behulp van MapReduce in Hadoop is uw verwerking logica implementeren met behulp van alleen een kaart en een functie verminderen.</span><span class="sxs-lookup"><span data-stu-id="78469-138">One of hello challenges of processing data by using MapReduce in Hadoop is implementing your processing logic by using only a map and a reduce function.</span></span> <span data-ttu-id="78469-139">Voor complexe verwerking, u vaak keten toobreak verwerken in meerdere MapReduce-bewerkingen die zijn samengesteld tooachieve Hallo gewenst resultaat.</span><span class="sxs-lookup"><span data-stu-id="78469-139">For complex processing, you often have toobreak processing into multiple MapReduce operations that are chained together tooachieve hello desired result.</span></span>

<span data-ttu-id="78469-140">Pig kunt u toodefine verwerken als een reeks transformaties die Hallo gegevensoverdrachten via tooproduce Hallo gewenste uitvoer.</span><span class="sxs-lookup"><span data-stu-id="78469-140">Pig allows you toodefine processing as a series of transformations that hello data flows through tooproduce hello desired output.</span></span>

<span data-ttu-id="78469-141">Hallo Pig Latin taal kunt u toodescribe Hallo gegevensstroom uit onbewerkte invoer, via een of meer transformaties tooproduce Hallo gewenste uitvoer.</span><span class="sxs-lookup"><span data-stu-id="78469-141">hello Pig Latin language allows you toodescribe hello data flow from raw input, through one or more transformations, tooproduce hello desired output.</span></span> <span data-ttu-id="78469-142">Pig Latin-programma's volgen deze algemene patroon:</span><span class="sxs-lookup"><span data-stu-id="78469-142">Pig Latin programs follow this general pattern:</span></span>

* <span data-ttu-id="78469-143">**Load**: gegevens toobe ingesteld van het bestandssysteem Hallo lezen</span><span class="sxs-lookup"><span data-stu-id="78469-143">**Load**: Read data toobe manipulated from hello file system</span></span>

* <span data-ttu-id="78469-144">**Transformeren**: Hallo gegevens bewerken</span><span class="sxs-lookup"><span data-stu-id="78469-144">**Transform**: Manipulate hello data</span></span>

* <span data-ttu-id="78469-145">**Dump of opgeslagen**: gegevens toohello scherm uitvoer of opgeslagen voor verwerking</span><span class="sxs-lookup"><span data-stu-id="78469-145">**Dump or store**: Output data toohello screen or store it for processing</span></span>

### <a name="user-defined-functions"></a><span data-ttu-id="78469-146">Gebruiker gedefinieerde functies</span><span class="sxs-lookup"><span data-stu-id="78469-146">User-defined functions</span></span>

<span data-ttu-id="78469-147">Pig Latin ondersteunt ook gebruiker gedefinieerde functies (UDF), waarmee u tooinvoke externe onderdelen die logica die is moeilijk toomodel in Pig Latin implementeren.</span><span class="sxs-lookup"><span data-stu-id="78469-147">Pig Latin also supports user-defined functions (UDF), which allows you tooinvoke external components that implement logic that is difficult toomodel in Pig Latin.</span></span>

<span data-ttu-id="78469-148">Zie voor meer informatie over Pig Latin [Pig Latin verwijzing handmatige 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) en [Pig Latin verwijzing handmatige 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span><span class="sxs-lookup"><span data-stu-id="78469-148">For more information about Pig Latin, see [Pig Latin Reference Manual 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) and [Pig Latin Reference Manual 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span></span>

<span data-ttu-id="78469-149">Zie voor een voorbeeld van het gebruik van UDF's met Pig Hallo documenten te volgen:</span><span class="sxs-lookup"><span data-stu-id="78469-149">For an example of using UDFs with Pig, see hello following documents:</span></span>

* <span data-ttu-id="78469-150">[Gebruik DataFu met Pig in HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) -DataFu is een verzameling nuttig UDF's die worden beheerd door de Apache</span><span class="sxs-lookup"><span data-stu-id="78469-150">[Use DataFu with Pig in HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu is a collection of useful UDFs maintained by Apache</span></span>
* [<span data-ttu-id="78469-151">Gebruik van Python met Pig en Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="78469-151">Use Python with Pig and Hive in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="78469-152">Gebruik C# met Hive en Pig in HDInsight</span><span class="sxs-lookup"><span data-stu-id="78469-152">Use C# with Hive and Pig in HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <span data-ttu-id="78469-153"><a id="data"></a>Voorbeeldgegevens</span><span class="sxs-lookup"><span data-stu-id="78469-153"><a id="data"></a>Example data</span></span>

<span data-ttu-id="78469-154">HDInsight biedt verschillende voorbeeld gegevenssets die zijn opgeslagen in Hallo `/example/data` en `/HdiSamples` mappen.</span><span class="sxs-lookup"><span data-stu-id="78469-154">HDInsight provides various example data sets, which are stored in hello `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="78469-155">Deze mappen zich in Hallo standaard opslagruimte voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="78469-155">These directories are in hello default storage for your cluster.</span></span> <span data-ttu-id="78469-156">Hallo Pig voorbeeld in dit document wordt Hallo *log4j* bestand van `/example/data/sample.log`.</span><span class="sxs-lookup"><span data-stu-id="78469-156">hello Pig example in this document uses hello *log4j* file from `/example/data/sample.log`.</span></span>

<span data-ttu-id="78469-157">Elk logboek in Hallo-bestand bestaat uit een line-of velden met een `[LOG LEVEL]` veld tooshow Hallo type en Hallo ernst, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="78469-157">Each log inside hello file consists of a line of fields that contains a `[LOG LEVEL]` field tooshow hello type and hello severity, for example:</span></span>

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

<span data-ttu-id="78469-158">In het vorige voorbeeld Hallo is Hallo logboekniveau fout.</span><span class="sxs-lookup"><span data-stu-id="78469-158">In hello previous example, hello log level is ERROR.</span></span>

> [!NOTE]
> <span data-ttu-id="78469-159">U kunt ook een log4j-bestand genereren met behulp van Hallo [Apache-Log4j](http://en.wikipedia.org/wiki/Log4j) hulpprogramma logboekregistratie en vervolgens uploaden bestand tooyour blob.</span><span class="sxs-lookup"><span data-stu-id="78469-159">You can also generate a log4j file by using hello [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) logging tool and then upload that file tooyour blob.</span></span> <span data-ttu-id="78469-160">Zie [gegevens uploaden tooHDInsight](hdinsight-upload-data.md) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="78469-160">See [Upload Data tooHDInsight](hdinsight-upload-data.md) for instructions.</span></span> <span data-ttu-id="78469-161">Zie voor meer informatie over het gebruik van blobs in Azure storage met HDInsight [Azure Blob Storage gebruiken met HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="78469-161">For more information about how blobs in Azure storage are used with HDInsight, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>

## <span data-ttu-id="78469-162"><a id="job"></a>Voorbeeld van de taak</span><span class="sxs-lookup"><span data-stu-id="78469-162"><a id="job"></a>Example job</span></span>

<span data-ttu-id="78469-163">Hallo volgende Pig Latin-taak wordt geladen Hallo `sample.log` -bestand uit Hallo standaard opslag voor uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="78469-163">hello following Pig Latin job loads hello `sample.log` file from hello default storage for your HDInsight cluster.</span></span> <span data-ttu-id="78469-164">Vervolgens voert een reeks transformaties die in een aantal van hoe vaak elk logboek niveau opgetreden in Hallo-invoergegevens resulteren uit.</span><span class="sxs-lookup"><span data-stu-id="78469-164">Then it performs a series of transformations that result in a count of how many times each log level occurred in hello input data.</span></span> <span data-ttu-id="78469-165">Hallo resultaten worden tooSTDOUT geschreven.</span><span class="sxs-lookup"><span data-stu-id="78469-165">hello results are written tooSTDOUT.</span></span>

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

<span data-ttu-id="78469-166">Hallo toont volgende afbeelding een overzicht van wat elke transformatie toohello gegevens biedt.</span><span class="sxs-lookup"><span data-stu-id="78469-166">hello following image shows a summary of what each transformation does toohello data.</span></span>

![Grafische weergave van Hallo transformaties][image-hdi-pig-data-transformation]

## <span data-ttu-id="78469-168"><a id="run"></a>Hallo Pig Latin taak uitvoeren</span><span class="sxs-lookup"><span data-stu-id="78469-168"><a id="run"></a>Run hello Pig Latin job</span></span>

<span data-ttu-id="78469-169">HDInsight kunt Pig Latin taken uitvoeren met behulp van een aantal methoden.</span><span class="sxs-lookup"><span data-stu-id="78469-169">HDInsight can run Pig Latin jobs by using a variety of methods.</span></span> <span data-ttu-id="78469-170">Gebruik Hallo tabel toodecide methode die geschikt voor u is te volgen en Hallo-koppeling voor de procedure volgen.</span><span class="sxs-lookup"><span data-stu-id="78469-170">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="78469-171">**Gebruik deze** als u wilt dat...</span><span class="sxs-lookup"><span data-stu-id="78469-171">**Use this** if you want...</span></span> | <span data-ttu-id="78469-172">.. .an **interactieve** shell</span><span class="sxs-lookup"><span data-stu-id="78469-172">...an **interactive** shell</span></span> | <span data-ttu-id="78469-173">... **batch** verwerken</span><span class="sxs-lookup"><span data-stu-id="78469-173">...**batch** processing</span></span> | <span data-ttu-id="78469-174">.. .door dit **cluster-besturingssysteem**</span><span class="sxs-lookup"><span data-stu-id="78469-174">...with this **cluster operating system**</span></span> | <span data-ttu-id="78469-175">.. .from dit **client**</span><span class="sxs-lookup"><span data-stu-id="78469-175">...from this **client**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="78469-176">SSH</span><span class="sxs-lookup"><span data-stu-id="78469-176">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="78469-177">✔</span><span class="sxs-lookup"><span data-stu-id="78469-177">✔</span></span> |<span data-ttu-id="78469-178">✔</span><span class="sxs-lookup"><span data-stu-id="78469-178">✔</span></span> |<span data-ttu-id="78469-179">Linux</span><span class="sxs-lookup"><span data-stu-id="78469-179">Linux</span></span> |<span data-ttu-id="78469-180">Linux, Unix, Mac OS X of Windows</span><span class="sxs-lookup"><span data-stu-id="78469-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="78469-181">CURL</span><span class="sxs-lookup"><span data-stu-id="78469-181">Curl</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="78469-182">✔</span><span class="sxs-lookup"><span data-stu-id="78469-182">✔</span></span> |<span data-ttu-id="78469-183">Linux- of Windows</span><span class="sxs-lookup"><span data-stu-id="78469-183">Linux or Windows</span></span> |<span data-ttu-id="78469-184">Linux, Unix, Mac OS X of Windows</span><span class="sxs-lookup"><span data-stu-id="78469-184">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="78469-185">.NET-SDK voor Hadoop</span><span class="sxs-lookup"><span data-stu-id="78469-185">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="78469-186">✔</span><span class="sxs-lookup"><span data-stu-id="78469-186">✔</span></span> |<span data-ttu-id="78469-187">Linux- of Windows</span><span class="sxs-lookup"><span data-stu-id="78469-187">Linux or Windows</span></span> |<span data-ttu-id="78469-188">Windows (voor nu)</span><span class="sxs-lookup"><span data-stu-id="78469-188">Windows (for now)</span></span> |
| [<span data-ttu-id="78469-189">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="78469-189">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="78469-190">✔</span><span class="sxs-lookup"><span data-stu-id="78469-190">✔</span></span> |<span data-ttu-id="78469-191">Linux- of Windows</span><span class="sxs-lookup"><span data-stu-id="78469-191">Linux or Windows</span></span> |<span data-ttu-id="78469-192">Windows</span><span class="sxs-lookup"><span data-stu-id="78469-192">Windows</span></span> |
| <span data-ttu-id="78469-193">[Extern bureaublad](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 en 3.3)</span><span class="sxs-lookup"><span data-stu-id="78469-193">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="78469-194">✔</span><span class="sxs-lookup"><span data-stu-id="78469-194">✔</span></span> |<span data-ttu-id="78469-195">✔</span><span class="sxs-lookup"><span data-stu-id="78469-195">✔</span></span> |<span data-ttu-id="78469-196">Windows</span><span class="sxs-lookup"><span data-stu-id="78469-196">Windows</span></span> |<span data-ttu-id="78469-197">Windows</span><span class="sxs-lookup"><span data-stu-id="78469-197">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="78469-198">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="78469-198">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="78469-199">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="78469-199">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="pig-and-sql-server-integration-services"></a><span data-ttu-id="78469-200">Pig- en SQL Server integratieservices</span><span class="sxs-lookup"><span data-stu-id="78469-200">Pig and SQL Server Integration Services</span></span>

<span data-ttu-id="78469-201">U kunt SQL Server Integration Services (SSIS) toorun Pig-taak.</span><span class="sxs-lookup"><span data-stu-id="78469-201">You can use SQL Server Integration Services (SSIS) toorun a Pig job.</span></span> <span data-ttu-id="78469-202">Hello Azure Feature Pack voor SSIS biedt Hallo onderdelen die met Pig-taken in HDInsight werken te volgen.</span><span class="sxs-lookup"><span data-stu-id="78469-202">hello Azure Feature Pack for SSIS provides hello following components that work with Pig jobs on HDInsight.</span></span>

* <span data-ttu-id="78469-203">[Azure HDInsight Pig-taak][pigtask]</span><span class="sxs-lookup"><span data-stu-id="78469-203">[Azure HDInsight Pig Task][pigtask]</span></span>

* <span data-ttu-id="78469-204">[Azure abonnement Verbindingsbeheer][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="78469-204">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="78469-205">Meer informatie over Azure Feature Pack Hallo voor SSIS [hier][ssispack].</span><span class="sxs-lookup"><span data-stu-id="78469-205">Learn more about hello Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="78469-206"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="78469-206"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="78469-207">U hebt geleerd hoe toouse Pig met HDInsight, gebruik Hallo volgen koppelingen tooexplore andere manieren toowork met Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="78469-207">Now that you have learned how toouse Pig with HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* <span data-ttu-id="78469-208">[Uploaden van gegevens tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="78469-208">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="78469-209">[Hive gebruiken met HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="78469-209">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* [<span data-ttu-id="78469-210">Sqoop gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="78469-210">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop.md)
* [<span data-ttu-id="78469-211">Oozie gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="78469-211">Use Oozie with HDInsight</span></span>](hdinsight-use-oozie.md)
* <span data-ttu-id="78469-212">[MapReduce-taken gebruiken met HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="78469-212">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

[apachepig-home]: http://pig.apache.org/
[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
[curl]: http://curl.haxx.se/
[pigtask]: http://msdn.microsoft.com/library/mt146781(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx


[hdinsight-upload-data]: hdinsight-upload-data.md

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md#mapreduce-sdk

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx


[image-hdi-pig-data-transformation]: ./media/hdinsight-use-pig/HDI.DataTransformation.gif
