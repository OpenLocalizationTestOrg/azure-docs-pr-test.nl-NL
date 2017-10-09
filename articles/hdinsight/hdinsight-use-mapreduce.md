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
# <a name="use-mapreduce-in-hadoop-on-hdinsight"></a>MapReduce in Hadoop in HDInsight gebruiken

Meer informatie over hoe toorun MapReduce taken op HDInsight-clusters. Gebruik Hallo tabel toodiscover Hallo verschillende manieren waarop MapReduce kan worden gebruikt met HDInsight te volgen:

| **Gebruik deze**... | **.. .toodo dit** | .. .door dit **cluster-besturingssysteem** | .. .from dit **clientbesturingssysteem** |
|:--- |:--- |:--- |:--- |
| [SSH](hdinsight-hadoop-use-mapreduce-ssh.md) |Gebruik Hallo Hadoop opdracht via **SSH** |Linux |Linux, Unix, Mac OS X of Windows |
| [REST](hdinsight-hadoop-use-mapreduce-curl.md) |Hallo-taak op afstand verzenden met behulp van **REST** (voorbeelden gebruiken cURL) |Linux- of Windows |Linux, Unix, Mac OS X of Windows |
| [Windows PowerShell](hdinsight-hadoop-use-mapreduce-powershell.md) |Hallo-taak op afstand verzenden met behulp van **Windows PowerShell** |Linux- of Windows |Windows |
| [Extern bureaublad](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 en 3.3) |Gebruik Hallo Hadoop opdracht via **extern bureaublad** |Windows |Windows |

> [!IMPORTANT]
> Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

## <a id="whatis"></a>Wat is MapReduce

Hadoop-MapReduce is een softwareframework voor het schrijven van taken die enorme hoeveelheden gegevens verwerken. Invoergegevens opgesplitst onafhankelijke chunks op Hallo knooppunten in het cluster vervolgens parallel worden verwerkt. Een MapReduce-taak bestaat uit twee functies:

* **Toewijzer**: invoergegevens verbruikt, analyseert ze (meestal met filteren en sorteren operations) en verzendt tuples (sleutel / waarde-paren)

* **Reducer**: tuples die door Hallo Mapper verbruikt en wordt een samenvatting uitgevoerd waarmee een kleinere, gecombineerde resultaat van Hallo Mapper-gegevens maakt

Een voorbeeld van een eenvoudige word aantal MapReduce-taak wordt weergegeven in het volgende diagram Hallo:

![HDI. WordCountDiagram][image-hdi-wordcountdiagram]

Hallo-uitvoer van deze taak is een telling van het aantal keren dat elk woord is opgetreden in de tekst hello die is geanalyseerd.

* Hallo mapper wordt elke regel van de ingevoerde tekst hello als invoer en splitst deze in woorden. Het verzendt een sleutelwaarde paar telkens wanneer een woord van Hallo woord plaatsvindt wordt gevolgd door een 1. Hallo-uitvoer is gesorteerd voordat het tooreducer wordt verzonden.
* Hallo reducer de som van de afzonderlijke aantallen voor elk woord en verzendt een één sleutel/waarde-paar die Hallo woord, gevolgd door Hallo som van de instanties bevat.

MapReduce kan worden geïmplementeerd in diverse talen. Java is de meest voorkomende implementatie Hallo en wordt gebruikt voor demonstratiedoeleinden in dit document.

## <a name="development-languages"></a>Ontwikkelingstalen

Talen of frameworks die zijn gebaseerd op Java en de virtuele Java-Machine Hallo kan rechtstreeks als een MapReduce-taak worden uitgevoerd. Hallo-voorbeeld gebruikt in dit document is een MapReduce Java-toepassing. Niet-Java-talen, zoals C#, Python of zelfstandige uitvoerbare bestanden, moeten het Hadoop-streaming gebruiken.

Hadoop-streaming communiceert met Hallo toewijzen en reducer via STDIN en STDOUT. Hallo mapper reducer gegevens van een regel op een tijdstip van STDIN lezen en schrijven Hallo uitvoer tooSTDOUT. Elke regel lezen of verzonden door Hallo toewijzen en reducer moet Hallo-indeling van een sleutel-waardepaar, gescheiden door een tab-teken zijn:

    [key]/t[value]

Zie voor meer informatie [Hadoop-Streaming](http://hadoop.apache.org/docs/r1.2.1/streaming.html).

Zie voor voorbeelden van het gebruik van Hadoop-streaming met HDInsight Hallo documenten te volgen:

* [C# MapReduce-taken ontwikkelen](hdinsight-hadoop-dotnet-csharp-mapreduce-streaming.md)

* [Python-MapReduce-taken ontwikkelen](hdinsight-hadoop-streaming-python.md)

## <a id="data"></a>Voorbeeldgegevens

HDInsight biedt verschillende voorbeeld gegevenssets die zijn opgeslagen in Hallo `/example/data` en `/HdiSamples` directory. Deze mappen zich in Hallo standaard opslagruimte voor uw cluster. In dit document, gebruiken we Hallo `/example/data/gutenberg/davinci.txt` bestand. Dit bestand bevat Hallo notitieblokken van Leonardo Da Vinci.

## <a id="job"></a>Voorbeeld MapReduce

Een voorbeeld MapReduce word-count-toepassing is opgenomen in uw HDInsight-cluster. In dit voorbeeld bevindt zich op `/example/jars/hadoop-mapreduce-examples.jar` op Hallo standaard opslag voor uw cluster.

Hallo volgende Java-code is Hallo bron van Hallo MapReduce-toepassing die zijn opgenomen in Hallo `hadoop-mapreduce-examples.jar` bestand:

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

Uw eigen toepassingen MapReduce, Zie voor instructies toowrite Hallo documenten te volgen:

* [Ontwikkelen van Java-MapReduce-toepassingen voor HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [Python-MapReduce-toepassingen voor HDInsight ontwikkelen](hdinsight-hadoop-streaming-python.md)

## <a id="run"></a>Hallo MapReduce uitvoeren

HDInsight kunt HiveQL taken uitvoeren met behulp van verschillende methoden. Gebruik Hallo tabel toodecide methode die geschikt voor u is te volgen en Hallo-koppeling voor de procedure volgen.

| **Gebruik deze**... | **.. .toodo dit** | .. .door dit **cluster-besturingssysteem** | .. .from dit **clientbesturingssysteem** |
|:--- |:--- |:--- |:--- |
| [SSH](hdinsight-hadoop-use-mapreduce-ssh.md) |Gebruik Hallo Hadoop opdracht via **SSH** |Linux |Linux, Unix, Mac OS X of Windows |
| [CURL](hdinsight-hadoop-use-mapreduce-curl.md) |Hallo-taak op afstand verzenden met behulp van **REST** |Linux- of Windows |Linux, Unix, Mac OS X of Windows |
| [Windows PowerShell](hdinsight-hadoop-use-mapreduce-powershell.md) |Hallo-taak op afstand verzenden met behulp van **Windows PowerShell** |Linux- of Windows |Windows |
| [Extern bureaublad](hdinsight-hadoop-use-mapreduce-remote-desktop.md) (HDInsight 3.2 en 3.3) |Gebruik Hallo Hadoop opdracht via **extern bureaublad** |Windows |Windows |

> [!IMPORTANT]
> Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

## <a id="nextsteps"></a>Volgende stappen

toolearn meer informatie over het werken met gegevens in HDInsight, Zie Hallo documenten te volgen:

* [Het ontwikkelen van Java-MapReduce-programma's voor HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)

* [Python streaming MapReduce-programma's voor HDInsight ontwikkelen](hdinsight-hadoop-streaming-python.md)

* [Gebruiker MapReduce-taken met Apache Hadoop op HDInsight ontwikkelen](hdinsight-hadoop-mapreduce-scalding.md)

* [Hive gebruiken met HDInsight][hdinsight-use-hive]

* [Pig gebruiken met HDInsight][hdinsight-use-pig]


[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-develop-mapreduce-jobs]: hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-wordcountdiagram]: ./media/hdinsight-use-mapreduce/HDI.WordCountDiagram.gif
