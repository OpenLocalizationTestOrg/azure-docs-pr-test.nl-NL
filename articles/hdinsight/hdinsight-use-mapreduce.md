---
title: aaaMapReduce met Hadoop op HDInsight | Microsoft Docs
description: Meer informatie over hoe toorun MapReduce taken op Hadoop in HDInsight-clusters.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7f321501-d62c-4ffc-b5d6-102ecba6dd76
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 0cf7ad0e6769e678be64f9e4ec8ed7a214ab7af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a><span data-ttu-id="ae44e-103">MapReduce in Hadoop in HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="ae44e-103">Use MapReduce in Hadoop on HDInsight</span></span>

<span data-ttu-id="ae44e-104">Meer informatie over hoe toorun MapReduce taken op HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="ae44e-104">Learn how toorun MapReduce jobs on HDInsight clusters.</span></span> <span data-ttu-id="ae44e-105">Gebruik Hallo tabel toodiscover Hallo verschillende manieren waarop MapReduce kan worden gebruikt met HDInsight te volgen:</span><span class="sxs-lookup"><span data-stu-id="ae44e-105">Use hello following table toodiscover hello various ways that MapReduce can be used with HDInsight:</span></span>

| <span data-ttu-id="ae44e-106">**Gebruik deze**...</span><span class="sxs-lookup"><span data-stu-id="ae44e-106">**Use this**...</span></span> | <span data-ttu-id="ae44e-107">**.. .toodo dit**</span><span class="sxs-lookup"><span data-stu-id="ae44e-107">**...toodo this**</span></span> | <span data-ttu-id="ae44e-108">.. .door dit **cluster-besturingssysteem**</span><span class="sxs-lookup"><span data-stu-id="ae44e-108">...with this **cluster operating system**</span></span> | <span data-ttu-id="ae44e-109">.. .from dit **clientbesturingssysteem**</span><span class="sxs-lookup"><span data-stu-id="ae44e-109">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="ae44e-110">SSH</span><span class="sxs-lookup"><span data-stu-id="ae44e-110">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="ae44e-111">Gebruik Hallo Hadoop opdracht via **SSH**</span><span class="sxs-lookup"><span data-stu-id="ae44e-111">Use hello Hadoop command through **SSH**</span></span> |<span data-ttu-id="ae44e-112">Linux</span><span class="sxs-lookup"><span data-stu-id="ae44e-112">Linux</span></span> |<span data-ttu-id="ae44e-113">Linux, Unix, Mac OS X of Windows</span><span class="sxs-lookup"><span data-stu-id="ae44e-113">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="ae44e-114">REST</span><span class="sxs-lookup"><span data-stu-id="ae44e-114">REST</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="ae44e-115">Hallo-taak op afstand verzenden met behulp van **REST** (voorbeelden gebruiken cURL)</span><span class="sxs-lookup"><span data-stu-id="ae44e-115">Submit hello job remotely by using **REST** (examples use cURL)</span></span> |<span data-ttu-id="ae44e-116">Linux- of Windows</span><span class="sxs-lookup"><span data-stu-id="ae44e-116">Linux or Windows</span></span> |<span data-ttu-id="ae44e-117">Linux, Unix, Mac OS X of Windows</span><span class="sxs-lookup"><span data-stu-id="ae44e-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="ae44e-118">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae44e-118">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="ae44e-119">Hallo-taak op afstand verzenden met behulp van **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="ae44e-119">Submit hello job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="ae44e-120">Linux- of Windows</span><span class="sxs-lookup"><span data-stu-id="ae44e-120">Linux or Windows</span></span> |<span data-ttu-id="ae44e-121">Windows</span><span class="sxs-lookup"><span data-stu-id="ae44e-121">Windows</span></span> |
| <span data-ttu-id="ae44e-122">[Extern bureaublad](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 en 3.3)</span><span class="sxs-lookup"><span data-stu-id="ae44e-122">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="ae44e-123">Gebruik Hallo Hadoop opdracht via **extern bureaublad**</span><span class="sxs-lookup"><span data-stu-id="ae44e-123">Use hello Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="ae44e-124">Windows</span><span class="sxs-lookup"><span data-stu-id="ae44e-124">Windows</span></span> |<span data-ttu-id="ae44e-125">Windows</span><span class="sxs-lookup"><span data-stu-id="ae44e-125">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="ae44e-126">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="ae44e-126">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ae44e-127">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ae44e-127">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="ae44e-128"><a id="whatis"></a>Wat is MapReduce</span><span class="sxs-lookup"><span data-stu-id="ae44e-128"><a id="whatis"></a>What is MapReduce</span></span>

<span data-ttu-id="ae44e-129">Hadoop-MapReduce is een softwareframework voor het schrijven van taken die enorme hoeveelheden gegevens verwerken.</span><span class="sxs-lookup"><span data-stu-id="ae44e-129">Hadoop MapReduce is a software framework for writing jobs that process vast amounts of data.</span></span> <span data-ttu-id="ae44e-130">Invoergegevens opgesplitst onafhankelijke chunks op Hallo knooppunten in het cluster vervolgens parallel worden verwerkt.</span><span class="sxs-lookup"><span data-stu-id="ae44e-130">Input data is split into independent chunks, which are then processed in parallel across hello nodes in your cluster.</span></span> <span data-ttu-id="ae44e-131">Een MapReduce-taak bestaat uit twee functies:</span><span class="sxs-lookup"><span data-stu-id="ae44e-131">A MapReduce job consists of two functions:</span></span>

* <span data-ttu-id="ae44e-132">**Toewijzer**: invoergegevens verbruikt, analyseert ze (meestal met filteren en sorteren operations) en verzendt tuples (sleutel / waarde-paren)</span><span class="sxs-lookup"><span data-stu-id="ae44e-132">**Mapper**: Consumes input data, analyzes it (usually with filter and sorting operations), and emits tuples (key-value pairs)</span></span>

* <span data-ttu-id="ae44e-133">**Reducer**: tuples die door Hallo Mapper verbruikt en wordt een samenvatting uitgevoerd waarmee een kleinere, gecombineerde resultaat van Hallo Mapper-gegevens maakt</span><span class="sxs-lookup"><span data-stu-id="ae44e-133">**Reducer**: Consumes tuples emitted by hello Mapper and performs a summary operation that creates a smaller, combined result from hello Mapper data</span></span>

<span data-ttu-id="ae44e-134">Een voorbeeld van een eenvoudige word aantal MapReduce-taak wordt weergegeven in het volgende diagram Hallo:</span><span class="sxs-lookup"><span data-stu-id="ae44e-134">A basic word count MapReduce job example is illustrated in hello following diagram:</span></span>

![HDI. WordCountDiagram][image-hdi-wordcountdiagram]

<span data-ttu-id="ae44e-136">Hallo-uitvoer van deze taak is een telling van het aantal keren dat elk woord is opgetreden in de tekst hello die is geanalyseerd.</span><span class="sxs-lookup"><span data-stu-id="ae44e-136">hello output of this job is a count of how many times each word occurred in hello text that was analyzed.</span></span>

* <span data-ttu-id="ae44e-137">Hallo mapper wordt elke regel van de ingevoerde tekst hello als invoer en splitst deze in woorden.</span><span class="sxs-lookup"><span data-stu-id="ae44e-137">hello mapper takes each line from hello input text as an input and breaks it into words.</span></span> <span data-ttu-id="ae44e-138">Het verzendt een sleutelwaarde paar telkens wanneer een woord van Hallo woord plaatsvindt wordt gevolgd door een 1.</span><span class="sxs-lookup"><span data-stu-id="ae44e-138">It emits a key/value pair each time a word occurs of hello word is followed by a 1.</span></span> <span data-ttu-id="ae44e-139">Hallo-uitvoer is gesorteerd voordat het tooreducer wordt verzonden.</span><span class="sxs-lookup"><span data-stu-id="ae44e-139">hello output is sorted before sending it tooreducer.</span></span>
* <span data-ttu-id="ae44e-140">Hallo reducer de som van de afzonderlijke aantallen voor elk woord en verzendt een één sleutel/waarde-paar die Hallo woord, gevolgd door Hallo som van de instanties bevat.</span><span class="sxs-lookup"><span data-stu-id="ae44e-140">hello reducer sums these individual counts for each word and emits a single key/value pair that contains hello word followed by hello sum of its occurrences.</span></span>

<span data-ttu-id="ae44e-141">MapReduce kan worden geïmplementeerd in diverse talen.</span><span class="sxs-lookup"><span data-stu-id="ae44e-141">MapReduce can be implemented in various languages.</span></span> <span data-ttu-id="ae44e-142">Java is de meest voorkomende implementatie Hallo en wordt gebruikt voor demonstratiedoeleinden in dit document.</span><span class="sxs-lookup"><span data-stu-id="ae44e-142">Java is hello most common implementation, and is used for demonstration purposes in this document.</span></span>

## <a name="development-languages"></a><span data-ttu-id="ae44e-143">Ontwikkelingstalen</span><span class="sxs-lookup"><span data-stu-id="ae44e-143">Development languages</span></span>

<span data-ttu-id="ae44e-144">Talen of frameworks die zijn gebaseerd op Java en de virtuele Java-Machine Hallo kan rechtstreeks als een MapReduce-taak worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ae44e-144">Languages or frameworks that are based on Java and hello Java Virtual Machine can be ran directly as a MapReduce job.</span></span> <span data-ttu-id="ae44e-145">Hallo-voorbeeld gebruikt in dit document is een MapReduce Java-toepassing.</span><span class="sxs-lookup"><span data-stu-id="ae44e-145">hello example used in this document is a Java MapReduce application.</span></span> <span data-ttu-id="ae44e-146">Niet-Java-talen, zoals C#, Python of zelfstandige uitvoerbare bestanden, moeten het Hadoop-streaming gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ae44e-146">Non-Java languages, such as C#, Python, or standalone executables, must use Hadoop streaming.</span></span>

<span data-ttu-id="ae44e-147">Hadoop-streaming communiceert met Hallo toewijzen en reducer via STDIN en STDOUT.</span><span class="sxs-lookup"><span data-stu-id="ae44e-147">Hadoop streaming communicates with hello mapper and reducer over STDIN and STDOUT.</span></span> <span data-ttu-id="ae44e-148">Hallo mapper reducer gegevens van een regel op een tijdstip van STDIN lezen en schrijven Hallo uitvoer tooSTDOUT.</span><span class="sxs-lookup"><span data-stu-id="ae44e-148">hello mapper and reducer read data a line at a time from STDIN, and write hello output tooSTDOUT.</span></span> <span data-ttu-id="ae44e-149">Elke regel lezen of verzonden door Hallo toewijzen en reducer moet Hallo-indeling van een sleutel-waardepaar, gescheiden door een tab-teken zijn:</span><span class="sxs-lookup"><span data-stu-id="ae44e-149">Each line read or emitted by hello mapper and reducer must be in hello format of a key/value pair, delimited by a tab character:</span></span>

    [key]/t[value]

<span data-ttu-id="ae44e-150">Zie voor meer informatie [Hadoop-Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span><span class="sxs-lookup"><span data-stu-id="ae44e-150">For more information, see [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span></span>

<span data-ttu-id="ae44e-151">Zie voor voorbeelden van het gebruik van Hadoop-streaming met HDInsight Hallo documenten te volgen:</span><span class="sxs-lookup"><span data-stu-id="ae44e-151">For examples of using Hadoop streaming with HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="ae44e-152">C# MapReduce-taken ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="ae44e-152">Develop C# MapReduce jobs</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="ae44e-153">Python-MapReduce-taken ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="ae44e-153">Develop Python MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="ae44e-154"><a id="data"></a>Voorbeeldgegevens</span><span class="sxs-lookup"><span data-stu-id="ae44e-154"><a id="data"></a>Example data</span></span>

<span data-ttu-id="ae44e-155">HDInsight biedt verschillende voorbeeld gegevenssets die zijn opgeslagen in Hallo `/example/data` en `/HdiSamples` directory.</span><span class="sxs-lookup"><span data-stu-id="ae44e-155">HDInsight provides various example data sets, which are stored in hello `/example/data` and `/HdiSamples` directory.</span></span> <span data-ttu-id="ae44e-156">Deze mappen zich in Hallo standaard opslagruimte voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="ae44e-156">These directories are in hello default storage for your cluster.</span></span> <span data-ttu-id="ae44e-157">In dit document, gebruiken we Hallo `/example/data/gutenberg/davinci.txt` bestand.</span><span class="sxs-lookup"><span data-stu-id="ae44e-157">In this document, we use hello `/example/data/gutenberg/davinci.txt` file.</span></span> <span data-ttu-id="ae44e-158">Dit bestand bevat Hallo notitieblokken van Leonardo Da Vinci.</span><span class="sxs-lookup"><span data-stu-id="ae44e-158">This file contains hello notebooks of Leonardo Da Vinci.</span></span>

## <span data-ttu-id="ae44e-159"><a id="job"></a>Voorbeeld MapReduce</span><span class="sxs-lookup"><span data-stu-id="ae44e-159"><a id="job"></a>Example MapReduce</span></span>

<span data-ttu-id="ae44e-160">Een voorbeeld MapReduce word-count-toepassing is opgenomen in uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="ae44e-160">An example MapReduce word count application is included with your HDInsight cluster.</span></span> <span data-ttu-id="ae44e-161">In dit voorbeeld bevindt zich op `/example/jars/hadoop-mapreduce-examples.jar` op Hallo standaard opslag voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="ae44e-161">This example is located at `/example/jars/hadoop-mapreduce-examples.jar` on hello default storage for your cluster.</span></span>

<span data-ttu-id="ae44e-162">Hallo volgende Java-code is Hallo bron van Hallo MapReduce-toepassing die zijn opgenomen in Hallo `hadoop-mapreduce-examples.jar` bestand:</span><span class="sxs-lookup"><span data-stu-id="ae44e-162">hello following Java code is hello source of hello MapReduce application contained in hello `hadoop-mapreduce-examples.jar` file:</span></span>

```java
package org.apache.hadoop.examples;

import java.io.IOException;
import java.util.StringTokenizer;

import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.util.GenericOptionsParser;

public class WordCount {

    public static class TokenizerMapper
        extends Mapper<Object, Text, Text, IntWritable>{

    private final static IntWritable one = new IntWritable(1);
    private Text word = new Text();

    public void map(Object key, Text value, Context context
                    ) throws IOException, InterruptedException {
        StringTokenizer itr = new StringTokenizer(value.toString());
        while (itr.hasMoreTokens()) {
        word.set(itr.nextToken());
        context.write(word, one);
        }
    }
    }

    public static class IntSumReducer
        extends Reducer<Text,IntWritable,Text,IntWritable> {
    private IntWritable result = new IntWritable();

    public void reduce(Text key, Iterable<IntWritable> values,
                        Context context
                        ) throws IOException, InterruptedException {
        int sum = 0;
        for (IntWritable val : values) {
        sum += val.get();
        }
        result.set(sum);
        context.write(key, result);
    }
    }

    public static void main(String[] args) throws Exception {
    Configuration conf = new Configuration();
    String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
    if (otherArgs.length != 2) {
        System.err.println("Usage: wordcount <in> <out>");
        System.exit(2);
    }
    Job job = new Job(conf, "word count");
    job.setJarByClass(WordCount.class);
    job.setMapperClass(TokenizerMapper.class);
    job.setCombinerClass(IntSumReducer.class);
    job.setReducerClass(IntSumReducer.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(IntWritable.class);
    FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
    FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
    System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
}
```

<span data-ttu-id="ae44e-163">Uw eigen toepassingen MapReduce, Zie voor instructies toowrite Hallo documenten te volgen:</span><span class="sxs-lookup"><span data-stu-id="ae44e-163">For instructions toowrite your own MapReduce applications, see hello following documents:</span></span>

* [<span data-ttu-id="ae44e-164">Ontwikkelen van Java-MapReduce-toepassingen voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="ae44e-164">Develop Java MapReduce applications for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="ae44e-165">Python-MapReduce-toepassingen voor HDInsight ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="ae44e-165">Develop Python MapReduce applications for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="ae44e-166"><a id="run"></a>Hallo MapReduce uitvoeren</span><span class="sxs-lookup"><span data-stu-id="ae44e-166"><a id="run"></a>Run hello MapReduce</span></span>

<span data-ttu-id="ae44e-167">HDInsight kunt HiveQL taken uitvoeren met behulp van verschillende methoden.</span><span class="sxs-lookup"><span data-stu-id="ae44e-167">HDInsight can run HiveQL jobs by using various methods.</span></span> <span data-ttu-id="ae44e-168">Gebruik Hallo tabel toodecide methode die geschikt voor u is te volgen en Hallo-koppeling voor de procedure volgen.</span><span class="sxs-lookup"><span data-stu-id="ae44e-168">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="ae44e-169">**Gebruik deze**...</span><span class="sxs-lookup"><span data-stu-id="ae44e-169">**Use this**...</span></span> | <span data-ttu-id="ae44e-170">**.. .toodo dit**</span><span class="sxs-lookup"><span data-stu-id="ae44e-170">**...toodo this**</span></span> | <span data-ttu-id="ae44e-171">.. .door dit **cluster-besturingssysteem**</span><span class="sxs-lookup"><span data-stu-id="ae44e-171">...with this **cluster operating system**</span></span> | <span data-ttu-id="ae44e-172">.. .from dit **clientbesturingssysteem**</span><span class="sxs-lookup"><span data-stu-id="ae44e-172">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="ae44e-173">SSH</span><span class="sxs-lookup"><span data-stu-id="ae44e-173">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="ae44e-174">Gebruik Hallo Hadoop opdracht via **SSH**</span><span class="sxs-lookup"><span data-stu-id="ae44e-174">Use hello Hadoop command through **SSH**</span></span> |<span data-ttu-id="ae44e-175">Linux</span><span class="sxs-lookup"><span data-stu-id="ae44e-175">Linux</span></span> |<span data-ttu-id="ae44e-176">Linux, Unix, Mac OS X of Windows</span><span class="sxs-lookup"><span data-stu-id="ae44e-176">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="ae44e-177">CURL</span><span class="sxs-lookup"><span data-stu-id="ae44e-177">Curl</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="ae44e-178">Hallo-taak op afstand verzenden met behulp van **REST**</span><span class="sxs-lookup"><span data-stu-id="ae44e-178">Submit hello job remotely by using **REST**</span></span> |<span data-ttu-id="ae44e-179">Linux- of Windows</span><span class="sxs-lookup"><span data-stu-id="ae44e-179">Linux or Windows</span></span> |<span data-ttu-id="ae44e-180">Linux, Unix, Mac OS X of Windows</span><span class="sxs-lookup"><span data-stu-id="ae44e-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="ae44e-181">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae44e-181">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="ae44e-182">Hallo-taak op afstand verzenden met behulp van **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="ae44e-182">Submit hello job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="ae44e-183">Linux- of Windows</span><span class="sxs-lookup"><span data-stu-id="ae44e-183">Linux or Windows</span></span> |<span data-ttu-id="ae44e-184">Windows</span><span class="sxs-lookup"><span data-stu-id="ae44e-184">Windows</span></span> |
| <span data-ttu-id="ae44e-185">[Extern bureaublad](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 en 3.3)</span><span class="sxs-lookup"><span data-stu-id="ae44e-185">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="ae44e-186">Gebruik Hallo Hadoop opdracht via **extern bureaublad**</span><span class="sxs-lookup"><span data-stu-id="ae44e-186">Use hello Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="ae44e-187">Windows</span><span class="sxs-lookup"><span data-stu-id="ae44e-187">Windows</span></span> |<span data-ttu-id="ae44e-188">Windows</span><span class="sxs-lookup"><span data-stu-id="ae44e-188">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="ae44e-189">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="ae44e-189">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ae44e-190">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ae44e-190">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="ae44e-191"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ae44e-191"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="ae44e-192">toolearn meer informatie over het werken met gegevens in HDInsight, Zie Hallo documenten te volgen:</span><span class="sxs-lookup"><span data-stu-id="ae44e-192">toolearn more about working with data in HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="ae44e-193">Het ontwikkelen van Java-MapReduce-programma's voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="ae44e-193">Develop Java MapReduce programs for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="ae44e-194">Python streaming MapReduce-programma's voor HDInsight ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="ae44e-194">Develop Python streaming MapReduce programs for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

* [<span data-ttu-id="ae44e-195">Gebruiker MapReduce-taken met Apache Hadoop op HDInsight ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="ae44e-195">Develop Scalding MapReduce jobs with Apache Hadoop on HDInsight</span></span>](hdinsight-hadoop-mapreduce-scalding.md)

* <span data-ttu-id="ae44e-196">[Hive gebruiken met HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="ae44e-196">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>

* <span data-ttu-id="ae44e-197">[Pig gebruiken met HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="ae44e-197">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
