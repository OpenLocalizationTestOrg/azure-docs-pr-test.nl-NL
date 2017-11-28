---
title: Hadoop Pig gebruiken in HDInsight | Microsoft Docs
description: Informatie over het Pig gebruiken met Hadoop op HDInsight.
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
ms.openlocfilehash: 474f901ffdaf1ed372ace19076ef723b8b10cb9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a><span data-ttu-id="ee1af-103">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ee1af-103">Use Pig with Hadoop on HDInsight</span></span>

<span data-ttu-id="ee1af-104">Informatie over het gebruik [Apache Pig](http://pig.apache.org/) met HDInsight...</span><span class="sxs-lookup"><span data-stu-id="ee1af-104">Learn how to use [Apache Pig](http://pig.apache.org/) with HDInsight...</span></span>

<span data-ttu-id="ee1af-105">Pig is een platform voor het maken van programma's voor Hadoop met behulp van een procedurele taal bekend als *Pig Latin*.</span><span class="sxs-lookup"><span data-stu-id="ee1af-105">Pig is a platform for creating programs for Hadoop by using a procedural language known as *Pig Latin*.</span></span> <span data-ttu-id="ee1af-106">Pig vormt een alternatief voor Java voor het maken van *MapReduce* oplossingen en deze is opgenomen in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ee1af-106">Pig is an alternative to Java for creating *MapReduce* solutions, and it is included with Azure HDInsight.</span></span> <span data-ttu-id="ee1af-107">Gebruik de volgende tabel voor het detecteren van de verschillende manieren waarop varkens kan worden gebruikt met HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ee1af-107">Use the following table to discover the various ways that Pig can be used with HDInsight:</span></span>

| <span data-ttu-id="ee1af-108">**Gebruik deze** als u wilt dat...</span><span class="sxs-lookup"><span data-stu-id="ee1af-108">**Use this** if you want...</span></span> | <span data-ttu-id="ee1af-109">.. .an **interactieve** shell</span><span class="sxs-lookup"><span data-stu-id="ee1af-109">...an **interactive** shell</span></span> | <span data-ttu-id="ee1af-110">... **batch** verwerken</span><span class="sxs-lookup"><span data-stu-id="ee1af-110">...**batch** processing</span></span> | <span data-ttu-id="ee1af-111">.. .door dit **cluster-besturingssysteem**</span><span class="sxs-lookup"><span data-stu-id="ee1af-111">...with this **cluster operating system**</span></span> | <span data-ttu-id="ee1af-112">.. .from dit **clientbesturingssysteem**</span><span class="sxs-lookup"><span data-stu-id="ee1af-112">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="ee1af-113">SSH</span><span class="sxs-lookup"><span data-stu-id="ee1af-113">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="ee1af-114">✔</span><span class="sxs-lookup"><span data-stu-id="ee1af-114">✔</span></span> |<span data-ttu-id="ee1af-115">✔</span><span class="sxs-lookup"><span data-stu-id="ee1af-115">✔</span></span> |<span data-ttu-id="ee1af-116">Linux</span><span class="sxs-lookup"><span data-stu-id="ee1af-116">Linux</span></span> |<span data-ttu-id="ee1af-117">Linux, Unix, Mac OS X of Windows</span><span class="sxs-lookup"><span data-stu-id="ee1af-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="ee1af-118">REST API</span><span class="sxs-lookup"><span data-stu-id="ee1af-118">REST API</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="ee1af-119">✔</span><span class="sxs-lookup"><span data-stu-id="ee1af-119">✔</span></span> |<span data-ttu-id="ee1af-120">Linux- of Windows</span><span class="sxs-lookup"><span data-stu-id="ee1af-120">Linux or Windows</span></span> |<span data-ttu-id="ee1af-121">Linux, Unix, Mac OS X of Windows</span><span class="sxs-lookup"><span data-stu-id="ee1af-121">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="ee1af-122">.NET-SDK voor Hadoop</span><span class="sxs-lookup"><span data-stu-id="ee1af-122">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="ee1af-123">✔</span><span class="sxs-lookup"><span data-stu-id="ee1af-123">✔</span></span> |<span data-ttu-id="ee1af-124">Linux- of Windows</span><span class="sxs-lookup"><span data-stu-id="ee1af-124">Linux or Windows</span></span> |<span data-ttu-id="ee1af-125">Windows (voor nu)</span><span class="sxs-lookup"><span data-stu-id="ee1af-125">Windows (for now)</span></span> |
| [<span data-ttu-id="ee1af-126">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee1af-126">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="ee1af-127">✔</span><span class="sxs-lookup"><span data-stu-id="ee1af-127">✔</span></span> |<span data-ttu-id="ee1af-128">Linux- of Windows</span><span class="sxs-lookup"><span data-stu-id="ee1af-128">Linux or Windows</span></span> |<span data-ttu-id="ee1af-129">Windows</span><span class="sxs-lookup"><span data-stu-id="ee1af-129">Windows</span></span> |
| <span data-ttu-id="ee1af-130">[Extern bureaublad](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 en 3.3)</span><span class="sxs-lookup"><span data-stu-id="ee1af-130">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="ee1af-131">✔</span><span class="sxs-lookup"><span data-stu-id="ee1af-131">✔</span></span> |<span data-ttu-id="ee1af-132">✔</span><span class="sxs-lookup"><span data-stu-id="ee1af-132">✔</span></span> |<span data-ttu-id="ee1af-133">Windows</span><span class="sxs-lookup"><span data-stu-id="ee1af-133">Windows</span></span> |<span data-ttu-id="ee1af-134">Windows</span><span class="sxs-lookup"><span data-stu-id="ee1af-134">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="ee1af-135">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="ee1af-135">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ee1af-136">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ee1af-136">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="ee1af-137"><a id="why"></a>Waarom Pig gebruiken</span><span class="sxs-lookup"><span data-stu-id="ee1af-137"><a id="why"></a>Why use Pig</span></span>

<span data-ttu-id="ee1af-138">Een van de uitdagingen bij het verwerken van gegevens met behulp van MapReduce in Hadoop is uw verwerking logica implementeren met behulp van alleen een kaart en een functie verminderen.</span><span class="sxs-lookup"><span data-stu-id="ee1af-138">One of the challenges of processing data by using MapReduce in Hadoop is implementing your processing logic by using only a map and a reduce function.</span></span> <span data-ttu-id="ee1af-139">Voor complexe verwerking, hebt u vaak verwerking opdelen in meerdere MapReduce-bewerkingen die zijn gekoppeld samen om te bewerkstelligen het gewenste resultaat oplevert.</span><span class="sxs-lookup"><span data-stu-id="ee1af-139">For complex processing, you often have to break processing into multiple MapReduce operations that are chained together to achieve the desired result.</span></span>

<span data-ttu-id="ee1af-140">Pig kunt u verwerking definiëren als een reeks transformaties dat de gegevens via loopt om de gewenste uitvoer te produceren.</span><span class="sxs-lookup"><span data-stu-id="ee1af-140">Pig allows you to define processing as a series of transformations that the data flows through to produce the desired output.</span></span>

<span data-ttu-id="ee1af-141">De taal Pig Latin kunt u beschrijven de gegevensstroom van onbewerkte invoer, via een of meer transformaties, om de gewenste uitvoer te produceren.</span><span class="sxs-lookup"><span data-stu-id="ee1af-141">The Pig Latin language allows you to describe the data flow from raw input, through one or more transformations, to produce the desired output.</span></span> <span data-ttu-id="ee1af-142">Pig Latin-programma's volgen deze algemene patroon:</span><span class="sxs-lookup"><span data-stu-id="ee1af-142">Pig Latin programs follow this general pattern:</span></span>

* <span data-ttu-id="ee1af-143">**Load**: gegevens van het bestandssysteem worden gemanipuleerd lezen</span><span class="sxs-lookup"><span data-stu-id="ee1af-143">**Load**: Read data to be manipulated from the file system</span></span>

* <span data-ttu-id="ee1af-144">**Transformeren**: de gegevens bewerken</span><span class="sxs-lookup"><span data-stu-id="ee1af-144">**Transform**: Manipulate the data</span></span>

* <span data-ttu-id="ee1af-145">**Dump of opgeslagen**: uitvoergegevens naar het scherm of opgeslagen voor verwerking</span><span class="sxs-lookup"><span data-stu-id="ee1af-145">**Dump or store**: Output data to the screen or store it for processing</span></span>

### <a name="user-defined-functions"></a><span data-ttu-id="ee1af-146">Gebruiker gedefinieerde functies</span><span class="sxs-lookup"><span data-stu-id="ee1af-146">User-defined functions</span></span>

<span data-ttu-id="ee1af-147">Pig Latin ondersteunt ook gebruiker gedefinieerde functies (UDF), zodat u kunt het aanroepen van externe onderdelen die logica die is moeilijk om Pig Latin-model te implementeren.</span><span class="sxs-lookup"><span data-stu-id="ee1af-147">Pig Latin also supports user-defined functions (UDF), which allows you to invoke external components that implement logic that is difficult to model in Pig Latin.</span></span>

<span data-ttu-id="ee1af-148">Zie voor meer informatie over Pig Latin [Pig Latin verwijzing handmatige 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) en [Pig Latin verwijzing handmatige 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span><span class="sxs-lookup"><span data-stu-id="ee1af-148">For more information about Pig Latin, see [Pig Latin Reference Manual 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) and [Pig Latin Reference Manual 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span></span>

<span data-ttu-id="ee1af-149">Zie de volgende documenten voor een voorbeeld van het gebruik van UDF's met Pig:</span><span class="sxs-lookup"><span data-stu-id="ee1af-149">For an example of using UDFs with Pig, see the following documents:</span></span>

* <span data-ttu-id="ee1af-150">[Gebruik DataFu met Pig in HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) -DataFu is een verzameling nuttig UDF's die worden beheerd door de Apache</span><span class="sxs-lookup"><span data-stu-id="ee1af-150">[Use DataFu with Pig in HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu is a collection of useful UDFs maintained by Apache</span></span>
* [<span data-ttu-id="ee1af-151">Gebruik van Python met Pig en Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ee1af-151">Use Python with Pig and Hive in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="ee1af-152">Gebruik C# met Hive en Pig in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ee1af-152">Use C# with Hive and Pig in HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <span data-ttu-id="ee1af-153"><a id="data"></a>Voorbeeldgegevens</span><span class="sxs-lookup"><span data-stu-id="ee1af-153"><a id="data"></a>Example data</span></span>

<span data-ttu-id="ee1af-154">HDInsight biedt verschillende voorbeeld gegevenssets die zijn opgeslagen in de `/example/data` en `/HdiSamples` mappen.</span><span class="sxs-lookup"><span data-stu-id="ee1af-154">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="ee1af-155">Deze mappen zich in de standaard-opslag voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="ee1af-155">These directories are in the default storage for your cluster.</span></span> <span data-ttu-id="ee1af-156">In het voorbeeld Pig in dit document wordt de *log4j* bestand van `/example/data/sample.log`.</span><span class="sxs-lookup"><span data-stu-id="ee1af-156">The Pig example in this document uses the *log4j* file from `/example/data/sample.log`.</span></span>

<span data-ttu-id="ee1af-157">Elk logboek in het bestand bestaat uit een line-of velden met een `[LOG LEVEL]` om weer te geven van het type en de ernst, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ee1af-157">Each log inside the file consists of a line of fields that contains a `[LOG LEVEL]` field to show the type and the severity, for example:</span></span>

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

<span data-ttu-id="ee1af-158">In het vorige voorbeeld is het Logniveau fout.</span><span class="sxs-lookup"><span data-stu-id="ee1af-158">In the previous example, the log level is ERROR.</span></span>

> [!NOTE]
> <span data-ttu-id="ee1af-159">U kunt ook een log4j-bestand genereren met behulp van de [Apache-Log4j](http://en.wikipedia.org/wiki/Log4j) hulpprogramma logboekregistratie en uploadt u dit bestand vervolgens naar de blob.</span><span class="sxs-lookup"><span data-stu-id="ee1af-159">You can also generate a log4j file by using the [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) logging tool and then upload that file to your blob.</span></span> <span data-ttu-id="ee1af-160">Zie [gegevens uploaden naar HDInsight](hdinsight-upload-data.md) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="ee1af-160">See [Upload Data to HDInsight](hdinsight-upload-data.md) for instructions.</span></span> <span data-ttu-id="ee1af-161">Zie voor meer informatie over het gebruik van blobs in Azure storage met HDInsight [Azure Blob Storage gebruiken met HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="ee1af-161">For more information about how blobs in Azure storage are used with HDInsight, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>

## <span data-ttu-id="ee1af-162"><a id="job"></a>Voorbeeld van de taak</span><span class="sxs-lookup"><span data-stu-id="ee1af-162"><a id="job"></a>Example job</span></span>

<span data-ttu-id="ee1af-163">De volgende taak voor Pig Latin laadt de `sample.log` -bestand van de standaard-opslag voor uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="ee1af-163">The following Pig Latin job loads the `sample.log` file from the default storage for your HDInsight cluster.</span></span> <span data-ttu-id="ee1af-164">Vervolgens voert een reeks transformaties die resulteren in een telling van het aantal keren dat elke logboekniveau is opgetreden in de invoergegevens uit.</span><span class="sxs-lookup"><span data-stu-id="ee1af-164">Then it performs a series of transformations that result in a count of how many times each log level occurred in the input data.</span></span> <span data-ttu-id="ee1af-165">De resultaten worden geschreven naar STDOUT.</span><span class="sxs-lookup"><span data-stu-id="ee1af-165">The results are written to STDOUT.</span></span>

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

<span data-ttu-id="ee1af-166">De volgende afbeelding toont een overzicht van de werking van elke transformatie op de gegevens.</span><span class="sxs-lookup"><span data-stu-id="ee1af-166">The following image shows a summary of what each transformation does to the data.</span></span>

![Grafische weergave van de transformaties][image-hdi-pig-data-transformation]

## <span data-ttu-id="ee1af-168"><a id="run"></a>Voer de taak Pig Latin</span><span class="sxs-lookup"><span data-stu-id="ee1af-168"><a id="run"></a>Run the Pig Latin job</span></span>

<span data-ttu-id="ee1af-169">HDInsight kunt Pig Latin taken uitvoeren met behulp van een aantal methoden.</span><span class="sxs-lookup"><span data-stu-id="ee1af-169">HDInsight can run Pig Latin jobs by using a variety of methods.</span></span> <span data-ttu-id="ee1af-170">Gebruik de volgende tabel om te bepalen welke methode is geschikt voor u en volg de koppeling voor een overzicht.</span><span class="sxs-lookup"><span data-stu-id="ee1af-170">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="ee1af-171">**Gebruik deze** als u wilt dat...</span><span class="sxs-lookup"><span data-stu-id="ee1af-171">**Use this** if you want...</span></span> | <span data-ttu-id="ee1af-172">.. .an **interactieve** shell</span><span class="sxs-lookup"><span data-stu-id="ee1af-172">...an **interactive** shell</span></span> | <span data-ttu-id="ee1af-173">... **batch** verwerken</span><span class="sxs-lookup"><span data-stu-id="ee1af-173">...**batch** processing</span></span> | <span data-ttu-id="ee1af-174">.. .door dit **cluster-besturingssysteem**</span><span class="sxs-lookup"><span data-stu-id="ee1af-174">...with this **cluster operating system**</span></span> | <span data-ttu-id="ee1af-175">.. .from dit **client**</span><span class="sxs-lookup"><span data-stu-id="ee1af-175">...from this **client**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="ee1af-176">SSH</span><span class="sxs-lookup"><span data-stu-id="ee1af-176">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="ee1af-177">✔</span><span class="sxs-lookup"><span data-stu-id="ee1af-177">✔</span></span> |<span data-ttu-id="ee1af-178">✔</span><span class="sxs-lookup"><span data-stu-id="ee1af-178">✔</span></span> |<span data-ttu-id="ee1af-179">Linux</span><span class="sxs-lookup"><span data-stu-id="ee1af-179">Linux</span></span> |<span data-ttu-id="ee1af-180">Linux, Unix, Mac OS X of Windows</span><span class="sxs-lookup"><span data-stu-id="ee1af-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="ee1af-181">CURL</span><span class="sxs-lookup"><span data-stu-id="ee1af-181">Curl</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="ee1af-182">✔</span><span class="sxs-lookup"><span data-stu-id="ee1af-182">✔</span></span> |<span data-ttu-id="ee1af-183">Linux- of Windows</span><span class="sxs-lookup"><span data-stu-id="ee1af-183">Linux or Windows</span></span> |<span data-ttu-id="ee1af-184">Linux, Unix, Mac OS X of Windows</span><span class="sxs-lookup"><span data-stu-id="ee1af-184">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="ee1af-185">.NET-SDK voor Hadoop</span><span class="sxs-lookup"><span data-stu-id="ee1af-185">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="ee1af-186">✔</span><span class="sxs-lookup"><span data-stu-id="ee1af-186">✔</span></span> |<span data-ttu-id="ee1af-187">Linux- of Windows</span><span class="sxs-lookup"><span data-stu-id="ee1af-187">Linux or Windows</span></span> |<span data-ttu-id="ee1af-188">Windows (voor nu)</span><span class="sxs-lookup"><span data-stu-id="ee1af-188">Windows (for now)</span></span> |
| [<span data-ttu-id="ee1af-189">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee1af-189">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="ee1af-190">✔</span><span class="sxs-lookup"><span data-stu-id="ee1af-190">✔</span></span> |<span data-ttu-id="ee1af-191">Linux- of Windows</span><span class="sxs-lookup"><span data-stu-id="ee1af-191">Linux or Windows</span></span> |<span data-ttu-id="ee1af-192">Windows</span><span class="sxs-lookup"><span data-stu-id="ee1af-192">Windows</span></span> |
| <span data-ttu-id="ee1af-193">[Extern bureaublad](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 en 3.3)</span><span class="sxs-lookup"><span data-stu-id="ee1af-193">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="ee1af-194">✔</span><span class="sxs-lookup"><span data-stu-id="ee1af-194">✔</span></span> |<span data-ttu-id="ee1af-195">✔</span><span class="sxs-lookup"><span data-stu-id="ee1af-195">✔</span></span> |<span data-ttu-id="ee1af-196">Windows</span><span class="sxs-lookup"><span data-stu-id="ee1af-196">Windows</span></span> |<span data-ttu-id="ee1af-197">Windows</span><span class="sxs-lookup"><span data-stu-id="ee1af-197">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="ee1af-198">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="ee1af-198">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ee1af-199">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ee1af-199">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="pig-and-sql-server-integration-services"></a><span data-ttu-id="ee1af-200">Pig- en SQL Server integratieservices</span><span class="sxs-lookup"><span data-stu-id="ee1af-200">Pig and SQL Server Integration Services</span></span>

<span data-ttu-id="ee1af-201">SQL Server Integration Services (SSIS) kunt u een Pig-taak uitvoert.</span><span class="sxs-lookup"><span data-stu-id="ee1af-201">You can use SQL Server Integration Services (SSIS) to run a Pig job.</span></span> <span data-ttu-id="ee1af-202">Het Azure-functiepakket voor SSIS biedt de volgende onderdelen die met Pig-taken in HDInsight werken.</span><span class="sxs-lookup"><span data-stu-id="ee1af-202">The Azure Feature Pack for SSIS provides the following components that work with Pig jobs on HDInsight.</span></span>

* <span data-ttu-id="ee1af-203">[Azure HDInsight Pig-taak][pigtask]</span><span class="sxs-lookup"><span data-stu-id="ee1af-203">[Azure HDInsight Pig Task][pigtask]</span></span>

* <span data-ttu-id="ee1af-204">[Azure abonnement Verbindingsbeheer][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="ee1af-204">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="ee1af-205">Meer informatie over het Azure Feature Pack voor SSIS [hier][ssispack].</span><span class="sxs-lookup"><span data-stu-id="ee1af-205">Learn more about the Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="ee1af-206"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ee1af-206"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="ee1af-207">U hebt geleerd hoe u Pig gebruiken met HDInsight, gebruik de volgende koppelingen om te verkennen andere manieren om te werken met Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ee1af-207">Now that you have learned how to use Pig with HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* <span data-ttu-id="ee1af-208">[Gegevens uploaden naar HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="ee1af-208">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="ee1af-209">[Hive gebruiken met HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="ee1af-209">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* [<span data-ttu-id="ee1af-210">Sqoop gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="ee1af-210">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop.md)
* [<span data-ttu-id="ee1af-211">Oozie gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="ee1af-211">Use Oozie with HDInsight</span></span>](hdinsight-use-oozie.md)
* <span data-ttu-id="ee1af-212">[MapReduce-taken gebruiken met HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="ee1af-212">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

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
