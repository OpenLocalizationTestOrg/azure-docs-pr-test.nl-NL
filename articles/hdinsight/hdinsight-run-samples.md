---
title: aaaRun hello Hadoop in HDInsight - Azure-voorbeelden | Microsoft Docs
description: Aan de slag met hello Azure HDInsight-service met Hallo voorbeelden. PowerShell-scripts die MapReduce-programma's op gegevens clusters uitvoeren gebruiken.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: bf76d452-abb4-4210-87bd-a2067778c6ed
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 544856a2cdfe5154cbd9bf1fb05db081af86cd46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hadoop-mapreduce-samples-in-windows-based-hdinsight"></a>Voorbeelden van Hadoop MapReduce uitvoeren in HDInsight op basis van Windows
[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

Een reeks voorbeelden vindt u aan de slag met Azure HDInsight Hadoop-clusters van MapReduce-taken waarop toohelp. Deze voorbeelden worden beschikbaar gesteld op elk Hallo HDInsight beheerde clusters die u maakt. Deze voorbeelden wordt uitgevoerd, raakt u vertrouwd met het gebruik van Azure PowerShell-cmdlets toorun taken op Hadoop-clusters.

* [**Word-count**][hdinsight-sample-wordcount]: telt word-exemplaren in een tekstbestand.
* [**C#-streaming aantal woorden**][hdinsight-sample-csharp-streaming]: aantallen word voorvallen in een tekst-bestand met Hallo Hadoop-streaming interface.
* [**PI estimator**][hdinsight-sample-pi-estimator]: maakt gebruik van een statistische (quasi Monte Carlo) methode tooestimate Hallo waarde van pi.
* [**10 GB Graysort**][hdinsight-sample-10gb-graysort]: een algemeen GraySort uitvoeren op een 10 GB-bestand met behulp van HDInsight. Er zijn drie taken toorun: Teragen toogenerate Hallo gegevens, Terasort toosort Hallo gegevens en Teravalidate tooconfirm dat Hallo gegevens correct zijn gesorteerd.

> [!NOTE]
> Hallo broncode vindt u in Hallo bijlage.

Veel aanvullende documentatie bestaat op Hallo web voor Hadoop-gerelateerde technologieën, zoals Java gebaseerde MapReduce programmering en streaming en documentatie over Hallo-cmdlets die worden gebruikt in Windows PowerShell-scripts. Zie voor meer informatie over deze resources:

* [Het ontwikkelen van Java-MapReduce-programma's voor Hadoop in HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)
* [Hadoop-taken opgeven in HDInsight](hdinsight-submit-hadoop-jobs-programmatically.md)
* [Inleiding tooAzure HDInsight][hdinsight-introduction]

Veel mensen kiezen tegenwoordig Hive en Pig via MapReduce.  Zie voor meer informatie:

* [Hive in HDInsight gebruiken](hdinsight-use-hive.md)
* [Pig gebruiken in HDInsight](hdinsight-use-pig.md)

**Vereisten**:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **een HDInsight-cluster**. Zie voor instructies over Hallo verschillende manieren waarin dergelijke clusters kunnen worden gemaakt, [maken Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
* **Een werkstation met Azure PowerShell**.

    > [!IMPORTANT]
    > Azure PowerShell-ondersteuning voor het beheer van HDInsight-resources met behulp van Azure Service Manager is **afgeschaft** en verdwijnt per 1 januari 2017. Hallo stappen in dit document gebruiken Hallo nieuwe HDInsight-cmdlets die met Azure Resource Manager werken.
    >
    > Volg de stappen Hallo in [installeren en configureren van Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall Hallo meest recente versie van Azure PowerShell. Als u scripts hebt die moeten toobe toouse Hallo nieuwe cmdlets die met Azure Resource Manager werken gewijzigd, Zie [migreren tooAzure ontwikkeling Resource Manager gebaseerde hulpprogramma's voor HDInsight-clusters](hdinsight-hadoop-development-using-azure-resource-manager.md).

## <a name="hdinsight-sample-wordcount"></a>Word-count - Java
toosubmit een MapReduce-project, maakt u eerst de definitie van een MapReduce-taak. In de taakdefinitie Hallo, u Hallo MapReduce programma jar-bestand en Hallo-locatie van de jar-bestand hello, die is opgeven **wasb:///example/jars/hadoop-mapreduce-examples.jar**Hallo klassenaam en Hallo argumenten.  Hallo wordcount MapReduce programma twee argumenten aanneemt: Hallo-bronbestand die gebruikte toocount woorden en Hallo locatie voor uitvoer.

Hallo broncode vindt u in Hallo [bijlage A](#apendix-a---the-word-count-MapReduce-program-in-java).

Programma voor Hallo procedure van het ontwikkelen van een Java-MapReduce, Zie - [ontwikkelen van Java-MapReduce-programma's voor Hadoop in HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)

**toosubmit een word-count-MapReduce-taak**

1. Open **Windows PowerShell ISE**. Zie voor instructies [installeren en configureren van Azure PowerShell][powershell-install-configure].
2. Plak de volgende PowerShell-script Hallo:

    ```powershell
    $subscriptionName = "<Azure Subscription Name>"
    $resourceGroupName = "<Resource Group Name>"
    $clusterName = "<HDInsight cluster name>"             # HDInsight cluster name

    Select-AzureRmSubscription -SubscriptionName $subscriptionName

    # Define hello MapReduce job
    $mrJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "wordcount" `
                                -Arguments "wasb:///example/data/gutenberg/davinci.txt", "wasb:///example/data/WordCountOutput"

    # Submit hello job and wait for job completion
    $cred = Get-Credential -Message "Enter hello HDInsight cluster HTTP user credential:"
    $mrJob = Start-AzureRmHDInsightJob `
                        -ResourceGroupName $resourceGroupName `
                        -ClusterName $clusterName `
                        -HttpCredential $cred `
                        -JobDefinition $mrJobDefinition

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -JobId $mrJob.JobId

    # Get hello job output
    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -DefaultStorageAccountName $defaultStorageAccount `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultStorageContainer  `
        -JobId $mrJob.JobId `
        -DisplayOutputType StandardError

    # Download hello job output toohello workstation
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob example/data/WordCountOutput/part-r-00000 -Context $storageContext -Force

    # Display hello output file
    cat ./example/data/WordCountOutput/part-r-00000 | findstr "there"
    ```

    Hallo MapReduce-taak wordt een bestand met de naam *onderdeel-r-00000*, die woorden bevat en Hallo telt. Hallo-script gebruikt Hallo **findstr** toolist alle Hallo woorden die opdracht bevat *"there"*.
3. Hallo eerste drie variabelen instellen en Hallo-script uitvoeren.

## <a name="hdinsight-sample-csharp-streaming"></a>Word-count - C#-streaming
Hadoop biedt een streaming API tooMapReduce die kunt u toowrite kaart en functies in andere talen dan Java te verminderen.

> [!NOTE]
> Hallo stappen in deze zelfstudie gelden alleen tooWindows gebaseerde HDInsight-clusters. Zie voor een voorbeeld van streaming voor Linux gebaseerde HDInsight-clusters [ontwikkelen Python streaming-programma's voor HDInsight](hdinsight-hadoop-streaming-python.md).

In voorbeeld Hallo Hallo toewijzen en Hallo reducer zijn uitvoerbare bestanden die Hallo invoer van gelezen [stdin] [ stdin-stdout-stderr] (door regel) en de uitvoer van de Hallo te verzenden[stdout] [stdin-stdout-stderr]. Hallo programma telt alle Hallo woorden in Hallo tekst.

Als een uitvoerbaar bestand is opgegeven voor **mappers**, elke taak mapper Hallo uitvoerbare als een afzonderlijk proces wordt gestart wanneer Hallo toewijzen is geïnitialiseerd. Hallo mapper-taak wordt uitgevoerd, wordt de invoer in lijnen geconverteerd en feeds Hallo regels toohello [stdin] [ stdin-stdout-stderr] van Hallo-proces.

In Hallo tussentijd verzamelt Hallo mapper Hallo regel gerichte uitvoer van stdout Hallo van Hallo-proces. Elke regel worden geconverteerd naar een sleutel/waarde-paar wordt verzameld als uitvoer Hallo van Hallo toewijzen. Standaard Hallo-voorvoegsel van een regel van het eerste tabblad teken toohello is Hallo-sleutel en Hallo overige Hallo-regel (met uitzondering van Hallo Tab-teken) is Hallo-waarde. Volledige regel als Hallo-sleutel wordt beschouwd als er geen Tab-teken in de regel hello, en Hallo-waarde is null.

Als een uitvoerbaar bestand is opgegeven voor **verkleiningstoestellen**, elke taak reducer Hallo uitvoerbare als een afzonderlijk proces wordt gestart wanneer Hallo reducer is geïnitialiseerd. Hallo reducer taak wordt uitgevoerd, het waardeparen invoer sleutelwaarden worden geconverteerd in regels en het Hallo regels toohello feeds [stdin] [ stdin-stdout-stderr] van Hallo-proces.

In Hallo tussentijd Hallo reducer verzamelt Hallo regel gerichte uitvoer van Hallo [stdout] [ stdin-stdout-stderr] van Hallo-proces. Elke regel tooa sleutel-waardepaar, die worden verzameld als uitvoer van Hallo reducer hello wordt geconverteerd. Standaard Hallo-voorvoegsel van een regel van het eerste tabblad teken toohello is Hallo-sleutel en Hallo overige Hallo-regel (met uitzondering van Hallo Tab-teken) is Hallo-waarde.

**toosubmit een C# streaming de word-count-taak**

* Volg de procedure Hallo in [Word-count - Java](#word-count-java), en vervang de taakdefinitie Hallo door Hallo volgt regel:

    ```powershell
    $mrJobDefinition = New-AzureRmHDInsightStreamingMapReduceJobDefinition `
                            -Files "/example/apps/cat.exe","/example/apps/wc.exe" `
                            -Mapper "cat.exe" `
                            -Reducer "wc.exe" `
                            -InputPath "/example/data/gutenberg/davinci.txt" `
                            -OutputPath "/example/data/StreamingOutput/wc.txt"
    ```

    Hallo-uitvoerbestand zijn:

        example/data/StreamingOutput/wc.txt/part-00000

## <a name="hdinsight-sample-pi-estimator"></a>PI estimator
Hallo pi estimator maakt gebruik van een statistische (quasi Monte Carlo) methode tooestimate Hallo waarde van pi. Punten geplaatst willekeurig binnen een eenheid vierkante ook vallen binnen een cirkel met een kans gelijk toohello gebied van de cirkel hello, zijn aangebracht in vierkant pi/4. Hallo-waarde van pi kan worden geschat van Hallo-waarde van 4R, waarbij R Hallo verhouding van het aantal punten in Hallo cirkel toohello totaal aantal punten die binnen Hallo vierkante Hallo is. Hallo groter Hallo voorbeeld van punten gebruikt, Hallo beter Hallo inschatten is.

Hallo-script is opgegeven voor dit voorbeeld verzendt een taak van de jar Hadoop en is ingesteld toorun met een waarde met 16 maps, die vereist toocompute 10 miljoen voorbeeldpunten door Hallo parameterwaarden is. Deze parameter waarden kunnen worden gewijzigd tooimprove Hallo geschatte waarde van pi. Ter referentie: hello eerste 10 decimalen van pi zijn 3.1415926535.

**toosubmit een pi estimator taak**

* Volg de procedure Hallo in [Word-count - Java](#word-count-java), en vervang de taakdefinitie Hallo door Hallo volgt regel:

    ```powershell
    $mrJobJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "pi" `
                                -Arguments "16", "10000000"
    ```

## <a name="hdinsight-sample-10gb-graysort"></a>10 GB Graysort
Dit voorbeeld wordt een matige 10GB aan gegevens gebruikt, zodat deze kan relatief snel kan worden uitgevoerd. Hallo MapReduce-toepassingen die zijn ontwikkeld door Owen O'Malley en Arun Murthy die Hallo jaarlijkse Algemeen ('daytona') terabyte sorteren benchmark 2009 met een snelheid van 0.578 TB/min (100 TB in 173 minuten gewonnen) wordt gebruikt. Zie voor meer informatie over deze en andere sorteren benchmarks Hallo [Sortbenchmark](http://sortbenchmark.org/) site.

Dit voorbeeld worden drie sets van MapReduce-programma's gebruikt:

1. **TeraGen** is een MapReduce-programma waarmee u gegevens toosort toogenerate Hallo rijen kunt.
2. **TeraSort** Hallo invoergegevens voorbeelden en MapReduce toosort Hallo gegevens worden gebruikt in een totale volgorde. TeraSort is een standaard soort MapReduce-functies, met uitzondering van een aangepaste partitioner die gebruikmaakt van een gesorteerde lijst met actieve N-1 sleutels die Hallo sleutel bereik voor elke verminderen definiëren. In het bijzonder alle sleutels dergelijke waarvan de steekproef [i-1] < sleutel = < voorbeeld [i] tooreduce worden verzonden ik. Dit garandeert dat Hallo uitvoerwaarden van ik beperken zijn alle kleiner is dan Hallo-uitvoer van verminderen i + 1.
3. **TeraValidate** is een MapReduce-programma te valideren die uitvoer Hallo globaal wordt gesorteerd. Een kaart per bestand wordt gemaakt in de uitvoermap Hallo en elke toewijzing zorgt ervoor dat elke sleutel kleiner dan of gelijk is toohello vorige. Hallo kaart functie wordt ook gegenereerd records Hallo eerst en laatste sleutels van elk bestand en Hallo functie verminderen zorgt ervoor dat Hallo eerste sleutel van i-bestand is groter dan de laatste sleutel Hallo van bestand i-1. Eventuele problemen worden gerapporteerd als uitvoer Hallo verminderen met Hallo sleutels die geplaatst zijn.

Hallo invoer en uitvoerindeling, die wordt gebruikt door alle drie de toepassingen, leest en schrijft tekstbestanden Hallo Hallo juiste indeling. Hallo-uitvoer van Hallo verminderen is replicatie ingesteld too1 in plaats van Hallo standaard 3, omdat Hallo benchmark wedstrijd niet vereist dat de uitvoergegevens Hallo op toomultiple knooppunten worden gerepliceerd.

Drie taken vereist zijn voor elke overeenkomende tooone hello MapReduce-programma's die worden beschreven in Hallo inleiding Hallo voorbeeld:

1. Hallo-gegevens voor het sorteren door te voeren Hallo genereren **TeraGen** MapReduce-taak.
2. Hallo gegevens sorteren door te voeren Hallo **TeraSort** MapReduce-taak.
3. Bevestig dat Hallo gegevens correct zijn gesorteerd door te voeren Hallo **TeraValidate** MapReduce-taak.

**toosubmit hello taken**

* Volg de procedure Hallo in [Word-count - Java](#word-count-java), en gebruik Hallo taakdefinities te volgen:

    ```powershell
    $teragen = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teragen" `
                                -Arguments "-Dmapred.map.tasks=50", "100000000", "/example/data/10GB-sort-input"

    $terasort = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "terasort" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-input", "/example/data/10GB-sort-output"

    $teravalidate = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teravalidate" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-output", "/example/data/10GB-sort-validate"
    ```

## <a name="next-steps"></a>Volgende stappen
Van dit artikel en Hallo artikelen in elk Hallo voorbeelden hebt u geleerd hoe toorun Hallo voorbeelden opgenomen Hello HDInsight-clusters met behulp van Azure PowerShell. Zie voor de zelfstudies over het gebruik van Pig, Hive en MapReduce met HDInsight, Hallo volgende onderwerpen:

* [Aan de slag met Hadoop Hive in HDInsight tooanalyze mobiele telefoon gebruiken][hdinsight-get-started]
* [Pig gebruiken met Hadoop in HDInsight][hdinsight-use-pig]
* [Hive gebruiken met Hadoop in HDInsight][hdinsight-use-hive]
* [Hadoop-taken in HDInsight verzenden][hdinsight-submit-jobs]
* [Azure HDInsight SDK-documentatie][hdinsight-sdk-documentation]

## <a name="appendix-a---hello-word-count-source-code"></a>Bijlage A - Hallo Word-count broncode

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

## <a name="appendix-b---hello-word-count-streaming-source-code"></a>Bijlage B – Hallo woorden tellen broncode streaming
Hallo wordt MapReduce Hallo cat.exe toepassing als een toewijzing interface toostream Hallo tekst in de console Hallo Hallo wc.exe toepassing hello interface toocount Hallo aantal woorden die worden gestreamd uit een document worden verminderd. Zowel Hallo toewijzen als reducer hello Standaardinvoerstroom (stdin) tekens, regel voor regel lezen en schrijven van toohello standaard uitvoerstroom (stdout).

```csharp
// hello source code for hello cat.exe (Mapper).

using System;
using System.IO;

namespace cat
{
    class cat
    {
        static void Main(string[] args)
        {
            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            string line;
            char[] separators = { ' ', '\n'};
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split(separators);
                foreach (var word in words)
                {
                    Console.WriteLine("{0}\t1", word);
                }
            }
        }
    }
}
```

Hallo mapper-code in Hallo cat.cs bestand gebruikt een [StreamReader] [ streamreader] tooread Hallo tekens van Hallo binnenkomende stroom toohello console, schrijft vervolgens Hallo stroom toohello Standaarduitvoerstroom object met statische Hallo [Console.Writeline] [ console-writeline] methode.

```csharp
// hello source code for wc.exe (Reducer) is:

using System;
using System.IO;
using System.Linq;
using System.Collections;

namespace wc
{
    class wc
    {
        static void Main(string[] args)
        {
            string line;

            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            Hashtable wordCount = new Hashtable();
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split('\t');

                string key = words[0];

                if (wordCount.ContainsKey(key) == true)
                {
                    int n = Convert.ToInt32(wordCount[key]);
                    wordCount[key] = Convert.ToString(n + 1);
                }
                else
                {
                    wordCount[key] = words[1];
                }
            }
            foreach (var key in wordCount.Keys)
            {
                Console.WriteLine("{0} {1}", key, wordCount[key]);
            }
        }
    }
}
```

Hallo reducer code in Hallo wc.cs bestand gebruikt een [StreamReader] [ streamreader] object tooread tekens uit Hallo Standaardinvoerstroom die zijn uitgevoerd door Hallo cat.exe toewijzen. Als deze tekens met Hallo Hallo leest [Console.Writeline] [ console-writeline] methode, wordt dit geteld Hallo woorden door spaties en einde van regel tekens aan Hallo einde van elk woord tellen. Het Hallo totale toohello Standaarduitvoerstroom Hello hierna schrijft [Console.Writeline] [ console-writeline] methode.

## <a name="appendix-c---hello-pi-estimator-source-code"></a>Bijlage C - Hallo Pi estimator broncode
Hallo pi estimator Java-code die Hallo toewijzen en reducer functies bevat, is beschikbaar voor inspectie hieronder. Hallo mapper-programma genereert een opgegeven aantal punten op willekeurige binnen een vierkant eenheid geplaatst en vervolgens telt Hallo aantal die punten die in Hallo cirkel. Hallo reducer programma stelt punten door Hallo mappers geteld samen en vervolgens maakt een schatting van Hallo-waarde van pi van Hallo formule 4R, waarbij R Hallo verhouding van het aantal punten geteld binnen Hallo cirkel toohello totaal aantal punten die binnen Hallo vierkante Hallo is.

```java
/**
* Licensed toohello Apache Software Foundation (ASF) under one
* or more contributor license agreements. See hello NOTICE file
* distributed with this work for additional information
* regarding copyright ownership. hello ASF licenses this file
* tooyou under hello Apache License, Version 2.0 (the
* "License"); you may not use this file except in compliance
* with hello License. You may obtain a copy of hello License at
*
* http://www.apache.org/licenses/LICENSE-2.0
*
* Unless required by applicable law or agreed tooin writing, software
* distributed under hello License is distributed on an "AS IS" BASIS,
* WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or     implied.
* See hello License for hello specific language governing permissions and
* limitations under hello License.
*/

package org.apache.hadoop.examples;

import java.io.IOException;
import java.math.BigDecimal;
import java.util.Iterator;

import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.BooleanWritable;
import org.apache.hadoop.io.LongWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Writable;
import org.apache.hadoop.io.WritableComparable;
import org.apache.hadoop.io.SequenceFile.CompressionType;
import org.apache.hadoop.mapred.FileInputFormat;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.MapReduceBase;
import org.apache.hadoop.mapred.Mapper;
import org.apache.hadoop.mapred.OutputCollector;
import org.apache.hadoop.mapred.Reducer;
import org.apache.hadoop.mapred.Reporter;
import org.apache.hadoop.mapred.SequenceFileInputFormat;
import org.apache.hadoop.mapred.SequenceFileOutputFormat;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

//A Map-reduce program tooestimate hello value of Pi
//using quasi-Monte Carlo method.
//
//Mapper:
//Generate points in a unit square
//and then count points inside/outside of hello inscribed circle of hello square.
//
//Reducer:
//Accumulate points inside/outside results from hello mappers.
//Let numTotal = numInside + numOutside.
//hello fraction numInside/numTotal is a rational approximation of
//hello value (Area of hello circle)/(Area of hello square),
//where hello area of hello inscribed circle is Pi/4
//and hello area of unit square is 1.
//Then, Pi is estimated value toobe 4(numInside/numTotal).
//

public class PiEstimator extends Configured implements Tool {
//tmp directory for input/output
static private final Path TMP_DIR = new Path(
PiEstimator.class.getSimpleName() + "_TMP_3_141592654");

//2-dimensional Halton sequence {H(i)},
//where H(i) is a 2-dimensional point and i >= 1 is hello index.
//Halton sequence is used toogenerate sample points for Pi estimation.
private static class HaltonSequence {
// Bases
static final int[] P = {2, 3};
//Maximum number of digits allowed
static final int[] K = {63, 40};

private long index;
private double[] x;
private double[][] q;
private int[][] d;

//Initialize tooH(startindex),
//so hello sequence begins with H(startindex+1).
HaltonSequence(long startindex) {
index = startindex;
x = new double[K.length];
q = new double[K.length][];
d = new int[K.length][];
for(int i = 0; i < K.length; i++) {
q[i] = new double[K[i]];
d[i] = new int[K[i]];
}

for(int i = 0; i < K.length; i++) {
long k = index;
x[i] = 0;

for(int j = 0; j < K[i]; j++) {
q[i][j] = (j == 0? 1.0: q[i][j-1])/P[i];
d[i][j] = (int)(k % P[i]);
k = (k - d[i][j])/P[i];
x[i] += d[i][j] * q[i][j];
}
}
}

//Compute next point.
//Assume hello current point is H(index).
//Compute H(index+1).
//@return a 2-dimensional point with coordinates in [0,1)^2
double[] nextPoint() {
index++;
for(int i = 0; i < K.length; i++) {
for(int j = 0; j < K[i]; j++) {
d[i][j]++;
x[i] += q[i][j];
if (d[i][j] < P[i]) {
break;
}
d[i][j] = 0;
x[i] -= (j == 0? 1.0: q[i][j-1]);
}
}
return x;
}
}

//Mapper class for Pi estimation.
//Generate points in a unit square and then
//count points inside/outside of hello inscribed circle of hello square.
public static class PiMapper extends MapReduceBase
implements Mapper<LongWritable, LongWritable, BooleanWritable, LongWritable> {

//Map method.
//@param offset samples starting from hello (offset+1)th sample.
//@param size hello number of samples for this map
//@param out output {ture->numInside, false->numOutside}
//@param reporter
public void map(LongWritable offset,
LongWritable size,
OutputCollector<BooleanWritable, LongWritable> out,
Reporter reporter) throws IOException {

final HaltonSequence haltonsequence = new HaltonSequence(offset.get());
long numInside = 0L;
long numOutside = 0L;

for(long i = 0; i < size.get(); ) {
//generate points in a unit square
final double[] point = haltonsequence.nextPoint();

//count points inside/outside of hello inscribed circle of hello square
final double x = point[0] - 0.5;
final double y = point[1] - 0.5;
if (x*x + y*y > 0.25) {
numOutside++;
} else {
numInside++;
}

//report status
i++;
if (i % 1000 == 0) {
reporter.setStatus("Generated " + i + " samples.");
}
}

//output map results
out.collect(new BooleanWritable(true), new LongWritable(numInside));
out.collect(new BooleanWritable(false), new LongWritable(numOutside));
}
}

//Reducer class for Pi estimation.
//Accumulate points inside/outside results from hello mappers.
public static class PiReducer extends MapReduceBase
implements Reducer<BooleanWritable, LongWritable, WritableComparable<?>, Writable> {

private long numInside = 0;
private long numOutside = 0;
private JobConf conf; //configuration for accessing hello file system

//Store job configuration.
@Override
public void configure(JobConf job) {
conf = job;
}

// Accumulate number of points inside/outside results from hello mappers.
// @param isInside Is hello points inside?
// @param values An iterator tooa list of point counts
// @param output dummy, not used here.
// @param reporter

public void reduce(BooleanWritable isInside,
Iterator<LongWritable> values,
OutputCollector<WritableComparable<?>, Writable> output,
Reporter reporter) throws IOException {
if (isInside.get()) {
for(; values.hasNext(); numInside += values.next().get());
} else {
for(; values.hasNext(); numOutside += values.next().get());
}
}

//Reduce task done, write output tooa file.
@Override
public void close() throws IOException {
//write output tooa file
Path outDir = new Path(TMP_DIR, "out");
Path outFile = new Path(outDir, "reduce-out");
FileSystem fileSys = FileSystem.get(conf);
SequenceFile.Writer writer = SequenceFile.createWriter(fileSys, conf,
outFile, LongWritable.class, LongWritable.class,
CompressionType.NONE);
writer.append(new LongWritable(numInside), new LongWritable(numOutside));
writer.close();
}
}

//Run a map/reduce job for estimating Pi.
//@return hello estimated value of Pi.
public static BigDecimal estimate(int numMaps, long numPoints, JobConf jobConf
)
throws IOException {
//setup job conf
jobConf.setJobName(PiEstimator.class.getSimpleName());

jobConf.setInputFormat(SequenceFileInputFormat.class);

jobConf.setOutputKeyClass(BooleanWritable.class);
jobConf.setOutputValueClass(LongWritable.class);
jobConf.setOutputFormat(SequenceFileOutputFormat.class);

jobConf.setMapperClass(PiMapper.class);
jobConf.setNumMapTasks(numMaps);

jobConf.setReducerClass(PiReducer.class);
jobConf.setNumReduceTasks(1);

// turn off speculative execution, because DFS doesn't handle
// multiple writers toohello same file.
jobConf.setSpeculativeExecution(false);

//setup input/output directories
final Path inDir = new Path(TMP_DIR, "in");
final Path outDir = new Path(TMP_DIR, "out");
FileInputFormat.setInputPaths(jobConf, inDir);
FileOutputFormat.setOutputPath(jobConf, outDir);

final FileSystem fs = FileSystem.get(jobConf);
if (fs.exists(TMP_DIR)) {
throw new IOException("Tmp directory " + fs.makeQualified(TMP_DIR)
+ " already exists. Remove it first.");
}
if (!fs.mkdirs(inDir)) {
throw new IOException("Cannot create input directory " + inDir);
}

//generate an input file for each map task
try {
for(int i=0; i < numMaps; ++i) {
final Path file = new Path(inDir, "part"+i);
final LongWritable offset = new LongWritable(i * numPoints);
final LongWritable size = new LongWritable(numPoints);
final SequenceFile.Writer writer = SequenceFile.createWriter(
fs, jobConf, file,
LongWritable.class, LongWritable.class, CompressionType.NONE);
try {
writer.append(offset, size);
} finally {
writer.close();
}
System.out.println("Wrote input for Map #"+i);
}

//start a map/reduce job
System.out.println("Starting Job");
final long startTime = System.currentTimeMillis();
JobClient.runJob(jobConf);
final double duration = (System.currentTimeMillis() - startTime)/1000.0;
System.out.println("Job Finished in " + duration + " seconds");

//read outputs
Path inFile = new Path(outDir, "reduce-out");
LongWritable numInside = new LongWritable();
LongWritable numOutside = new LongWritable();
SequenceFile.Reader reader = new SequenceFile.Reader(fs, inFile, jobConf);
try {
reader.next(numInside, numOutside);
} finally {
reader.close();
}

//compute estimated value
return BigDecimal.valueOf(4).setScale(20)
.multiply(BigDecimal.valueOf(numInside.get()))
.divide(BigDecimal.valueOf(numMaps))
.divide(BigDecimal.valueOf(numPoints));
} finally {
fs.delete(TMP_DIR, true);
}
}

//Parse arguments and then runs a map/reduce job.
//Print output in standard out.
//@return a non-zero if there is an error. Otherwise, return 0.
public int run(String[] args) throws Exception {
if (args.length != 2) {
System.err.println("Usage: "+getClass().getName()+" <nMaps> <nSamples>");
ToolRunner.printGenericCommandUsage(System.err);
return -1;
}

final int nMaps = Integer.parseInt(args[0]);
final long nSamples = Long.parseLong(args[1]);

System.out.println("Number of Maps = " + nMaps);
System.out.println("Samples per Map = " + nSamples);

final JobConf jobConf = new JobConf(getConf(), getClass());
System.out.println("Estimated value of Pi is "
+ estimate(nMaps, nSamples, jobConf));
return 0;
}

//main method for running it as a stand alone command.
public static void main(String[] argv) throws Exception {
System.exit(ToolRunner.run(null, new PiEstimator(), argv));
}
}
```

## <a name="appendix-d---hello-10gb-graysort-source-code"></a>Bijlage D - Hallo 10gb graysort broncode
Hallo-code voor Hallo TeraSort MapReduce-programma wordt voor inspectie in deze sectie weergegeven.

```java
/**
    * Licensed toohello Apache Software Foundation (ASF) under one
    * or more contributor license agreements.  See hello NOTICE file
    * distributed with this work for additional information
    * regarding copyright ownership.  hello ASF licenses this file
    * tooyou under hello Apache License, Version 2.0 (the
    * "License"); you may not use this file except in compliance
    * with hello License.  You may obtain a copy of hello License at
    *
    *     http://www.apache.org/licenses/LICENSE-2.0
    *
    * Unless required by applicable law or agreed tooin writing, software
    * distributed under hello License is distributed on an "AS IS" BASIS,
    * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    * See hello License for hello specific language governing permissions and
    * limitations under hello License.
    */

package org.apache.hadoop.examples.terasort;

import java.io.IOException;
import java.io.PrintStream;
import java.net.URI;
import java.util.ArrayList;
import java.util.List;

import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.filecache.DistributedCache;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.NullWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.Partitioner;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

/**
    * Generates hello sampled split points, launches hello job,
    * and waits for it toofinish.
    * <p>
    * toorun hello program:
    * <b>bin/hadoop jar hadoop-examples-*.jar terasort in-dir out-dir</b>
    */

public class TeraSort extends Configured implements Tool {
    private static final Log LOG = LogFactory.getLog(TeraSort.class);

    /**
    * A partitioner that splits text keys into roughly equal
    * partitions in a global sorted order.
    */

    static class TotalOrderPartitioner implements Partitioner<Text,Text>{
    private TrieNode trie;
    private Text[] splitPoints;

    /**
        * A generic trie node
        */
    static abstract class TrieNode {
        private int level;
        TrieNode(int level) {
        this.level = level;
        }
        abstract int findPartition(Text key);
        abstract void print(PrintStream strm) throws IOException;
        int getLevel() {
        return level;
        }
    }

    /**
        * An inner trie node that contains 256 children based on hello next
        * character.
        */
    static class InnerTrieNode extends TrieNode {
        private TrieNode[] child = new TrieNode[256];

        InnerTrieNode(int level) {
        super(level);
        }
        int findPartition(Text key) {
        int level = getLevel();
        if (key.getLength() <= level) {
            return child[0].findPartition(key);
        }
        return child[key.getBytes()[level]].findPartition(key);
        }
        void setChild(int idx, TrieNode child) {
        this.child[idx] = child;
        }
        void print(PrintStream strm) throws IOException {
        for(int ch=0; ch < 255; ++ch) {
            for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
            }
            strm.print(ch);
            strm.println(" ->");
            if (child[ch] != null) {
            child[ch].print(strm);
            }
        }
        }
    }

    /**
        * A leaf trie node that does string compares toofigure out where hello given
        * key belongs between lower..upper.
        */
    static class LeafTrieNode extends TrieNode {
        int lower;
        int upper;
        Text[] splitPoints;
        LeafTrieNode(int level, Text[] splitPoints, int lower, int upper) {
        super(level);
        this.splitPoints = splitPoints;
        this.lower = lower;
        this.upper = upper;
        }
        int findPartition(Text key) {
        for(int i=lower; i<upper; ++i) {
            if (splitPoints[i].compareTo(key) >= 0) {
            return i;
            }
        }
        return upper;
        }
        void print(PrintStream strm) throws IOException {
        for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
        }
        strm.print(lower);
        strm.print(", ");
        strm.println(upper);
        }
    }

    /**
        * Read hello cut points from hello given sequence file.
        * @param fs hello file system
        * @param p hello path tooread
        * @param job hello job config
        * @return hello strings toosplit hello partitions on
        * @throws IOException
        */
    private static Text[] readPartitions(FileSystem fs, Path p,
                                            JobConf job) throws IOException {
        SequenceFile.Reader reader = new SequenceFile.Reader(fs, p, job);
        List<Text> parts = new ArrayList<Text>();
        Text key = new Text();
        NullWritable value = NullWritable.get();
        while (reader.next(key, value)) {
        parts.add(key);
        key = new Text();
        }
        reader.close();
        return parts.toArray(new Text[parts.size()]);
    }

    /**
        * Given a sorted set of cut points, build a trie that will find hello correct
        * partition quickly.
        * @param splits hello list of cut points
        * @param lower hello lower bound of partitions 0..numPartitions-1
        * @param upper hello upper bound of partitions 0..numPartitions-1
        * @param prefix hello prefix that we have already checked against
        * @param maxDepth hello maximum depth we will build a trie for
        * @return hello trie node that will divide hello splits correctly
        */
    private static TrieNode buildTrie(Text[] splits, int lower, int upper,
                                        Text prefix, int maxDepth) {
        int depth = prefix.getLength();
        if (depth >= maxDepth || lower == upper) {
        return new LeafTrieNode(depth, splits, lower, upper);
        }
        InnerTrieNode result = new InnerTrieNode(depth);
        Text trial = new Text(prefix);
        // append an extra byte on toohello prefix
        trial.append(new byte[1], 0, 1);
        int currentBound = lower;
        for(int ch = 0; ch < 255; ++ch) {
        trial.getBytes()[depth] = (byte) (ch + 1);
        lower = currentBound;
        while (currentBound < upper) {
            if (splits[currentBound].compareTo(trial) >= 0) {
            break;
            }
            currentBound += 1;
        }
        trial.getBytes()[depth] = (byte) ch;
        result.child[ch] = buildTrie(splits, lower, currentBound, trial,
                                        maxDepth);
        }
        // pick up hello rest
        trial.getBytes()[depth] = 127;
        result.child[255] = buildTrie(splits, currentBound, upper, trial,
                                    maxDepth);
        return result;
    }

    public void configure(JobConf job) {
        try {
        FileSystem fs = FileSystem.getLocal(job);
        Path partFile = new Path(TeraInputFormat.PARTITION_FILENAME);
        splitPoints = readPartitions(fs, partFile, job);
        trie = buildTrie(splitPoints, 0, splitPoints.length, new Text(), 2);
        } catch (IOException ie) {
        throw new IllegalArgumentException("can't read paritions file", ie);
        }
    }

    public TotalOrderPartitioner() {
    }

    public int getPartition(Text key, Text value, int numPartitions) {
        return trie.findPartition(key);
    }

    }

    public int run(String[] args) throws Exception {
    LOG.info("starting");
    JobConf job = (JobConf) getConf();
    Path inputDir = new Path(args[0]);
    inputDir = inputDir.makeQualified(inputDir.getFileSystem(job));
    Path partitionFile = new Path(inputDir, TeraInputFormat.PARTITION_FILENAME);
    URI partitionUri = new URI(partitionFile.toString() +
                                "#" + TeraInputFormat.PARTITION_FILENAME);
    TeraInputFormat.setInputPaths(job, new Path(args[0]));
    FileOutputFormat.setOutputPath(job, new Path(args[1]));
    job.setJobName("TeraSort");
    job.setJarByClass(TeraSort.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(Text.class);
    job.setInputFormat(TeraInputFormat.class);
    job.setOutputFormat(TeraOutputFormat.class);
    job.setPartitionerClass(TotalOrderPartitioner.class);
    TeraInputFormat.writePartitionFile(job, partitionFile);
    DistributedCache.addCacheFile(partitionUri, job);
    DistributedCache.createSymlink(job);
    job.setInt("dfs.replication", 1);
    TeraOutputFormat.setFinalSync(job, true);
    JobClient.runJob(job);
    LOG.info("done");
    return 0;
    }

    /**
    * @param args
    */

    public static void main(String[] args) throws Exception {
    int res = ToolRunner.run(new JobConf(), new TeraSort(), args);
    System.exit(res);
    }
}
```

[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-samples]: hdinsight-run-samples.md
[hdinsight-sample-10gb-graysort]: #hdinsight-sample-10gb-graysort
[hdinsight-sample-csharp-streaming]: #hdinsight-sample-csharp-streaming
[hdinsight-sample-pi-estimator]: #hdinsight-sample-pi-estimator
[hdinsight-sample-wordcount]: #hdinsight-sample-wordcount

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[streamreader]: http://msdn.microsoft.com/library/system.io.streamreader.aspx
[console-writeline]: http://msdn.microsoft.com/library/system.console.writeline
[stdin-stdout-stderr]: https://msdn.microsoft.com/library/3x292kth.aspx
