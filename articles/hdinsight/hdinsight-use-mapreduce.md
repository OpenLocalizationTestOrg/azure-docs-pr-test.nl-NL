---
title: MapReduce met Hadoop op HDInsight | Microsoft Docs
description: Informatie over het uitvoeren van MapReduce-taken op Hadoop in HDInsight-clusters.
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
ms.openlocfilehash: df8ac578a56de72df667b1fa7f90f981c79d9999
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a><span data-ttu-id="e253d-103">MapReduce in Hadoop in HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="e253d-103">Use MapReduce in Hadoop on HDInsight</span></span>

<span data-ttu-id="e253d-104">Informatie over het uitvoeren van MapReduce-taken op HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="e253d-104">Learn how to run MapReduce jobs on HDInsight clusters.</span></span> <span data-ttu-id="e253d-105">Gebruik de volgende tabel voor het detecteren van de verschillende manieren waarop MapReduce kan worden gebruikt met HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e253d-105">Use the following table to discover the various ways that MapReduce can be used with HDInsight:</span></span>

| <span data-ttu-id="e253d-106">**Gebruik deze**...</span><span class="sxs-lookup"><span data-stu-id="e253d-106">**Use this**...</span></span> | <span data-ttu-id="e253d-107">**.. .om hiervoor**</span><span class="sxs-lookup"><span data-stu-id="e253d-107">**...to do this**</span></span> | <span data-ttu-id="e253d-108">.. .door dit **cluster-besturingssysteem**</span><span class="sxs-lookup"><span data-stu-id="e253d-108">...with this **cluster operating system**</span></span> | <span data-ttu-id="e253d-109">.. .from dit **clientbesturingssysteem**</span><span class="sxs-lookup"><span data-stu-id="e253d-109">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="e253d-110">SSH</span><span class="sxs-lookup"><span data-stu-id="e253d-110">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="e253d-111">Gebruik de opdracht Hadoop via **SSH**</span><span class="sxs-lookup"><span data-stu-id="e253d-111">Use the Hadoop command through **SSH**</span></span> |<span data-ttu-id="e253d-112">Linux</span><span class="sxs-lookup"><span data-stu-id="e253d-112">Linux</span></span> |<span data-ttu-id="e253d-113">Linux, Unix, Mac OS X of Windows</span><span class="sxs-lookup"><span data-stu-id="e253d-113">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="e253d-114">REST</span><span class="sxs-lookup"><span data-stu-id="e253d-114">REST</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="e253d-115">Verzenden van de taak op afstand via **REST** (voorbeelden gebruiken cURL)</span><span class="sxs-lookup"><span data-stu-id="e253d-115">Submit the job remotely by using **REST** (examples use cURL)</span></span> |<span data-ttu-id="e253d-116">Linux- of Windows</span><span class="sxs-lookup"><span data-stu-id="e253d-116">Linux or Windows</span></span> |<span data-ttu-id="e253d-117">Linux, Unix, Mac OS X of Windows</span><span class="sxs-lookup"><span data-stu-id="e253d-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="e253d-118">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e253d-118">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="e253d-119">Verzenden van de taak op afstand via **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="e253d-119">Submit the job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="e253d-120">Linux- of Windows</span><span class="sxs-lookup"><span data-stu-id="e253d-120">Linux or Windows</span></span> |<span data-ttu-id="e253d-121">Windows</span><span class="sxs-lookup"><span data-stu-id="e253d-121">Windows</span></span> |
| <span data-ttu-id="e253d-122">[Extern bureaublad](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 en 3.3)</span><span class="sxs-lookup"><span data-stu-id="e253d-122">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="e253d-123">Gebruik de opdracht Hadoop via **extern bureaublad**</span><span class="sxs-lookup"><span data-stu-id="e253d-123">Use the Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="e253d-124">Windows</span><span class="sxs-lookup"><span data-stu-id="e253d-124">Windows</span></span> |<span data-ttu-id="e253d-125">Windows</span><span class="sxs-lookup"><span data-stu-id="e253d-125">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="e253d-126">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="e253d-126">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e253d-127">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e253d-127">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="e253d-128"><a id="whatis"></a>Wat is MapReduce</span><span class="sxs-lookup"><span data-stu-id="e253d-128"><a id="whatis"></a>What is MapReduce</span></span>

<span data-ttu-id="e253d-129">Hadoop-MapReduce is een softwareframework voor het schrijven van taken die enorme hoeveelheden gegevens verwerken.</span><span class="sxs-lookup"><span data-stu-id="e253d-129">Hadoop MapReduce is a software framework for writing jobs that process vast amounts of data.</span></span> <span data-ttu-id="e253d-130">Invoergegevens opgesplitst onafhankelijke segmenten, die vervolgens parallel worden verwerkt op de knooppunten in het cluster.</span><span class="sxs-lookup"><span data-stu-id="e253d-130">Input data is split into independent chunks, which are then processed in parallel across the nodes in your cluster.</span></span> <span data-ttu-id="e253d-131">Een MapReduce-taak bestaat uit twee functies:</span><span class="sxs-lookup"><span data-stu-id="e253d-131">A MapReduce job consists of two functions:</span></span>

* <span data-ttu-id="e253d-132">**Toewijzer**: invoergegevens verbruikt, analyseert ze (meestal met filteren en sorteren operations) en verzendt tuples (sleutel / waarde-paren)</span><span class="sxs-lookup"><span data-stu-id="e253d-132">**Mapper**: Consumes input data, analyzes it (usually with filter and sorting operations), and emits tuples (key-value pairs)</span></span>

* <span data-ttu-id="e253d-133">**Reducer**: tuples die door de Mapper verbruikt en wordt een samenvatting uitgevoerd waarmee een kleinere, gecombineerde resultaat van de gegevens toewijzen maakt</span><span class="sxs-lookup"><span data-stu-id="e253d-133">**Reducer**: Consumes tuples emitted by the Mapper and performs a summary operation that creates a smaller, combined result from the Mapper data</span></span>

<span data-ttu-id="e253d-134">Een voorbeeld van een eenvoudige word aantal MapReduce-taak wordt weergegeven in het volgende diagram:</span><span class="sxs-lookup"><span data-stu-id="e253d-134">A basic word count MapReduce job example is illustrated in the following diagram:</span></span>

![HDI. WordCountDiagram][image-hdi-wordcountdiagram]

<span data-ttu-id="e253d-136">De uitvoer van deze taak is een telling van het aantal keren dat elk woord is opgetreden in de tekst die is geanalyseerd.</span><span class="sxs-lookup"><span data-stu-id="e253d-136">The output of this job is a count of how many times each word occurred in the text that was analyzed.</span></span>

* <span data-ttu-id="e253d-137">De toewijzing wordt elke regel van de ingevoerde tekst als invoer en splitst deze in woorden.</span><span class="sxs-lookup"><span data-stu-id="e253d-137">The mapper takes each line from the input text as an input and breaks it into words.</span></span> <span data-ttu-id="e253d-138">Het verzendt een sleutelwaarde paar telkens wanneer een woord van het woord plaatsvindt wordt gevolgd door een 1.</span><span class="sxs-lookup"><span data-stu-id="e253d-138">It emits a key/value pair each time a word occurs of the word is followed by a 1.</span></span> <span data-ttu-id="e253d-139">De uitvoer is gesorteerd voordat deze naar reducer verzonden.</span><span class="sxs-lookup"><span data-stu-id="e253d-139">The output is sorted before sending it to reducer.</span></span>
* <span data-ttu-id="e253d-140">De reducer deze afzonderlijke tellingen voor elk woord elkaar worden opgeteld en verzendt een één sleutel/waarde-paar die het woord gevolgd door de som van de instanties bevat.</span><span class="sxs-lookup"><span data-stu-id="e253d-140">The reducer sums these individual counts for each word and emits a single key/value pair that contains the word followed by the sum of its occurrences.</span></span>

<span data-ttu-id="e253d-141">MapReduce kan worden geïmplementeerd in diverse talen.</span><span class="sxs-lookup"><span data-stu-id="e253d-141">MapReduce can be implemented in various languages.</span></span> <span data-ttu-id="e253d-142">Java is de meest voorkomende implementatie en wordt gebruikt voor demonstratiedoeleinden in dit document.</span><span class="sxs-lookup"><span data-stu-id="e253d-142">Java is the most common implementation, and is used for demonstration purposes in this document.</span></span>

## <a name="development-languages"></a><span data-ttu-id="e253d-143">Ontwikkelingstalen</span><span class="sxs-lookup"><span data-stu-id="e253d-143">Development languages</span></span>

<span data-ttu-id="e253d-144">Talen of frameworks die zijn gebaseerd op Java en de virtuele Java-Machine kan rechtstreeks als een MapReduce-taak worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e253d-144">Languages or frameworks that are based on Java and the Java Virtual Machine can be ran directly as a MapReduce job.</span></span> <span data-ttu-id="e253d-145">Het voorbeeld gebruikt in dit document is een MapReduce Java-toepassing.</span><span class="sxs-lookup"><span data-stu-id="e253d-145">The example used in this document is a Java MapReduce application.</span></span> <span data-ttu-id="e253d-146">Niet-Java-talen, zoals C#, Python of zelfstandige uitvoerbare bestanden, moeten het Hadoop-streaming gebruiken.</span><span class="sxs-lookup"><span data-stu-id="e253d-146">Non-Java languages, such as C#, Python, or standalone executables, must use Hadoop streaming.</span></span>

<span data-ttu-id="e253d-147">Hadoop-streaming communiceert met de toewijzen en reducer via STDIN en STDOUT.</span><span class="sxs-lookup"><span data-stu-id="e253d-147">Hadoop streaming communicates with the mapper and reducer over STDIN and STDOUT.</span></span> <span data-ttu-id="e253d-148">De toewijzen en reducer gegevens van een regel op een tijdstip van STDIN lezen en schrijven van de uitvoer naar STDOUT.</span><span class="sxs-lookup"><span data-stu-id="e253d-148">The mapper and reducer read data a line at a time from STDIN, and write the output to STDOUT.</span></span> <span data-ttu-id="e253d-149">Elke regel lezen of verzonden door de toewijzen en reducer moet de indeling van een sleutel-waardepaar, gescheiden door een tab-teken zijn:</span><span class="sxs-lookup"><span data-stu-id="e253d-149">Each line read or emitted by the mapper and reducer must be in the format of a key/value pair, delimited by a tab character:</span></span>

    [key]/t[value]

<span data-ttu-id="e253d-150">Zie voor meer informatie [Hadoop-Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span><span class="sxs-lookup"><span data-stu-id="e253d-150">For more information, see [Hadoop Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).</span></span>

<span data-ttu-id="e253d-151">Zie de volgende documenten voor voorbeelden van het gebruik van Hadoop-streaming met HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e253d-151">For examples of using Hadoop streaming with HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="e253d-152">C# MapReduce-taken ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="e253d-152">Develop C# MapReduce jobs</span></span>](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [<span data-ttu-id="e253d-153">Python-MapReduce-taken ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="e253d-153">Develop Python MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="e253d-154"><a id="data"></a>Voorbeeldgegevens</span><span class="sxs-lookup"><span data-stu-id="e253d-154"><a id="data"></a>Example data</span></span>

<span data-ttu-id="e253d-155">HDInsight biedt verschillende voorbeeld gegevenssets die zijn opgeslagen in de `/example/data` en `/HdiSamples` directory.</span><span class="sxs-lookup"><span data-stu-id="e253d-155">HDInsight provides various example data sets, which are stored in the `/example/data` and `/HdiSamples` directory.</span></span> <span data-ttu-id="e253d-156">Deze mappen zich in de standaard-opslag voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="e253d-156">These directories are in the default storage for your cluster.</span></span> <span data-ttu-id="e253d-157">In dit document, gebruiken we de `/example/data/gutenberg/davinci.txt` bestand.</span><span class="sxs-lookup"><span data-stu-id="e253d-157">In this document, we use the `/example/data/gutenberg/davinci.txt` file.</span></span> <span data-ttu-id="e253d-158">Dit bestand bevat de laptops van Leonardo Da Vinci.</span><span class="sxs-lookup"><span data-stu-id="e253d-158">This file contains the notebooks of Leonardo Da Vinci.</span></span>

## <span data-ttu-id="e253d-159"><a id="job"></a>Voorbeeld MapReduce</span><span class="sxs-lookup"><span data-stu-id="e253d-159"><a id="job"></a>Example MapReduce</span></span>

<span data-ttu-id="e253d-160">Een voorbeeld MapReduce word-count-toepassing is opgenomen in uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="e253d-160">An example MapReduce word count application is included with your HDInsight cluster.</span></span> <span data-ttu-id="e253d-161">In dit voorbeeld bevindt zich op `/example/jars/hadoop-mapreduce-examples.jar` op de standaard-opslag voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="e253d-161">This example is located at `/example/jars/hadoop-mapreduce-examples.jar` on the default storage for your cluster.</span></span>

<span data-ttu-id="e253d-162">De volgende Java-code is de bron van de MapReduce-toepassing die is opgenomen in de `hadoop-mapreduce-examples.jar` bestand:</span><span class="sxs-lookup"><span data-stu-id="e253d-162">The following Java code is the source of the MapReduce application contained in the `hadoop-mapreduce-examples.jar` file:</span></span>

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

<span data-ttu-id="e253d-163">Zie de volgende documenten voor instructies om uw eigen MapReduce-toepassingen te schrijven:</span><span class="sxs-lookup"><span data-stu-id="e253d-163">For instructions to write your own MapReduce applications, see the following documents:</span></span>

* [<span data-ttu-id="e253d-164">Ontwikkelen van Java-MapReduce-toepassingen voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="e253d-164">Develop Java MapReduce applications for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="e253d-165">Python-MapReduce-toepassingen voor HDInsight ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="e253d-165">Develop Python MapReduce applications for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

## <span data-ttu-id="e253d-166"><a id="run"></a>De MapReduce uitvoeren</span><span class="sxs-lookup"><span data-stu-id="e253d-166"><a id="run"></a>Run the MapReduce</span></span>

<span data-ttu-id="e253d-167">HDInsight kunt HiveQL taken uitvoeren met behulp van verschillende methoden.</span><span class="sxs-lookup"><span data-stu-id="e253d-167">HDInsight can run HiveQL jobs by using various methods.</span></span> <span data-ttu-id="e253d-168">Gebruik de volgende tabel om te bepalen welke methode is geschikt voor u en volg de koppeling voor een overzicht.</span><span class="sxs-lookup"><span data-stu-id="e253d-168">Use the following table to decide which method is right for you, then follow the link for a walkthrough.</span></span>

| <span data-ttu-id="e253d-169">**Gebruik deze**...</span><span class="sxs-lookup"><span data-stu-id="e253d-169">**Use this**...</span></span> | <span data-ttu-id="e253d-170">**.. .om hiervoor**</span><span class="sxs-lookup"><span data-stu-id="e253d-170">**...to do this**</span></span> | <span data-ttu-id="e253d-171">.. .door dit **cluster-besturingssysteem**</span><span class="sxs-lookup"><span data-stu-id="e253d-171">...with this **cluster operating system**</span></span> | <span data-ttu-id="e253d-172">.. .from dit **clientbesturingssysteem**</span><span class="sxs-lookup"><span data-stu-id="e253d-172">...from this **client operating system**</span></span> |
|:--- |:--- |:--- |:--- |
| [<span data-ttu-id="e253d-173">SSH</span><span class="sxs-lookup"><span data-stu-id="e253d-173">SSH</span></span>](hdinsight-hadoop-use-mapreduce-ssh.md) |<span data-ttu-id="e253d-174">Gebruik de opdracht Hadoop via **SSH**</span><span class="sxs-lookup"><span data-stu-id="e253d-174">Use the Hadoop command through **SSH**</span></span> |<span data-ttu-id="e253d-175">Linux</span><span class="sxs-lookup"><span data-stu-id="e253d-175">Linux</span></span> |<span data-ttu-id="e253d-176">Linux, Unix, Mac OS X of Windows</span><span class="sxs-lookup"><span data-stu-id="e253d-176">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="e253d-177">CURL</span><span class="sxs-lookup"><span data-stu-id="e253d-177">Curl</span></span>](hdinsight-hadoop-use-mapreduce-curl.md) |<span data-ttu-id="e253d-178">Verzenden van de taak op afstand via **REST**</span><span class="sxs-lookup"><span data-stu-id="e253d-178">Submit the job remotely by using **REST**</span></span> |<span data-ttu-id="e253d-179">Linux- of Windows</span><span class="sxs-lookup"><span data-stu-id="e253d-179">Linux or Windows</span></span> |<span data-ttu-id="e253d-180">Linux, Unix, Mac OS X of Windows</span><span class="sxs-lookup"><span data-stu-id="e253d-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="e253d-181">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e253d-181">Windows PowerShell</span></span>](hdinsight-hadoop-use-mapreduce-powershell.md) |<span data-ttu-id="e253d-182">Verzenden van de taak op afstand via **Windows PowerShell**</span><span class="sxs-lookup"><span data-stu-id="e253d-182">Submit the job remotely by using **Windows PowerShell**</span></span> |<span data-ttu-id="e253d-183">Linux- of Windows</span><span class="sxs-lookup"><span data-stu-id="e253d-183">Linux or Windows</span></span> |<span data-ttu-id="e253d-184">Windows</span><span class="sxs-lookup"><span data-stu-id="e253d-184">Windows</span></span> |
| <span data-ttu-id="e253d-185">[Extern bureaublad](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 en 3.3)</span><span class="sxs-lookup"><span data-stu-id="e253d-185">[Remote Desktop](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="e253d-186">Gebruik de opdracht Hadoop via **extern bureaublad**</span><span class="sxs-lookup"><span data-stu-id="e253d-186">Use the Hadoop command through **Remote Desktop**</span></span> |<span data-ttu-id="e253d-187">Windows</span><span class="sxs-lookup"><span data-stu-id="e253d-187">Windows</span></span> |<span data-ttu-id="e253d-188">Windows</span><span class="sxs-lookup"><span data-stu-id="e253d-188">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="e253d-189">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="e253d-189">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e253d-190">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e253d-190">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="e253d-191"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e253d-191"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="e253d-192">Zie de volgende documenten voor meer informatie over het werken met gegevens in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e253d-192">To learn more about working with data in HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="e253d-193">Het ontwikkelen van Java-MapReduce-programma's voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="e253d-193">Develop Java MapReduce programs for HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [<span data-ttu-id="e253d-194">Python streaming MapReduce-programma's voor HDInsight ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="e253d-194">Develop Python streaming MapReduce programs for HDInsight</span></span>](hdinsight-hadoop-streaming-python.md)

* [<span data-ttu-id="e253d-195">Gebruiker MapReduce-taken met Apache Hadoop op HDInsight ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="e253d-195">Develop Scalding MapReduce jobs with Apache Hadoop on HDInsight</span></span>](hdinsight-hadoop-mapreduce-scalding.md)

* <span data-ttu-id="e253d-196">[Hive gebruiken met HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="e253d-196">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>

* <span data-ttu-id="e253d-197">[Pig gebruiken met HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="e253d-197">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
