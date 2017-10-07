---
title: aaaUse C# met MapReduce van Hadoop in HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe toouse C# toocreate MapReduce-oplossingen met Hadoop in Azure HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.custom: hdinsightactive
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd8b684e74155bc1a37d4ab8d6f9033276ef5aa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a>Gebruik C# met MapReduce streaming van Hadoop in HDInsight

Meer informatie over hoe toouse C# toocreate een MapReduce-oplossing op HDInsight.

> [!IMPORTANT]
> Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie voor meer informatie [versiebeheer van HDInsight-onderdeel](hdinsight-component-versioning.md).

Hadoop-streaming is een hulpprogramma waarmee u toorun MapReduce-taken met een script of uitvoerbaar bestand. In dit voorbeeld is .NET gebruikte tooimplement Hallo toewijzen en reducer voor een word-count-oplossing.

## <a name="net-on-hdinsight"></a>.NET in HDInsight

__HDInsight op basis van Linux__ clusters gebruik [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET-toepassingen. Mono versie 4.2.1 is opgenomen in HDInsight versie 3.5. Zie voor meer informatie over Hallo-versie van Mono opgenomen met HDInsight [HDInsight onderdeel versies](hdinsight-component-versioning.md). toouse een specifieke versie van Mono, Zie Hallo [installeren of update Mono](hdinsight-hadoop-install-mono.md) document.

Zie voor meer informatie over de Mono compatibiliteit met versies van .NET Framework [Mono compatibiliteit](http://www.mono-project.com/docs/about-mono/compatibility/).

## <a name="how-hadoop-streaming-works"></a>Hadoop-streaming werking

Hallo basisproces gebruikt voor streaming in dit document is als volgt:

1. Hadoop geeft STDIN toohello toewijzer (mapper.exe in dit voorbeeld).
2. Hallo mapper Hallo gegevens verwerkt, en door tabs gescheiden sleutel/waarde-paren tooSTDOUT verzendt.
3. Hallo-uitvoer is gelezen door Hadoop en toohello reducer (reducer.exe in dit voorbeeld) en deze vervolgens STDIN doorgeven.
4. Hallo reducer Hallo door tabs gescheiden sleutel/waarde-paren leest, Hallo gegevens verwerkt en vervolgens verzendt Hallo resultaat als door tabs gescheiden sleutel-waardeparen op STDOUT.
5. Hallo-uitvoer is gelezen door Hadoop en toohello uitvoermap geschreven.

Zie voor meer informatie over het streaming- [Hadoop-Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).

## <a name="prerequisites"></a>Vereisten

* U moet bekend zijn met schrijven en het bouwen van C#-code die gericht is op .NET Framework 4.5. Hallo stappen in dit document Visual Studio 2017.

* Een manier tooupload .exe-bestanden toohello cluster. Hallo stappen in dit document gebruiken Hallo Data Lake Tools voor Visual Studio tooupload Hallo bestanden tooprimary opslagruimte voor Hallo-cluster.

* Azure PowerShell of een SSH-client.

* Een Hadoop op HDInsight-cluster. Zie voor meer informatie over het maken van een cluster [maken van een HDInsight-cluster](hdinsight-provision-clusters.md).

## <a name="create-hello-mapper"></a>Hallo mapper maken

Maak in Visual Studio een nieuw __consoletoepassing__ met de naam __mapper__. Hallo na de code voor de toepassing hello gebruiken:

```csharp
using System;
using System.Text.RegularExpressions;

namespace mapper
{
    class Program
    {
        static void Main(string[] args)
        {
            string line;
            //Hadoop passes data toohello mapper on STDIN
            while((line = Console.ReadLine()) != null)
            {
                // We only want words, so strip out punctuation, numbers, etc.
                var onlyText = Regex.Replace(line, @"\.|;|:|,|[0-9]|'", "");
                // Split at whitespace.
                var words = Regex.Matches(onlyText, @"[\w]+");
                // Loop over hello words
                foreach(var word in words)
                {
                    //Emit tab-delimited key/value pairs.
                    //In this case, a word and a count of 1.
                    Console.WriteLine("{0}\t1",word);
                }
            }
        }
    }
}
```

Na het maken van de toepassing hello samenstellen tooproduce hello `/bin/Debug/mapper.exe` bestand in de projectmap Hallo.

## <a name="create-hello-reducer"></a>Hallo reducer maken

Maak in Visual Studio een nieuw __consoletoepassing__ met de naam __reducer__. Hallo na de code voor de toepassing hello gebruiken:

```csharp
using System;
using System.Collections.Generic;

namespace reducer
{
    class Program
    {
        static void Main(string[] args)
        {
            //Dictionary for holding a count of words
            Dictionary<string, int> words = new Dictionary<string, int>();

            string line;
            //Read from STDIN
            while ((line = Console.ReadLine()) != null)
            {
                // Data from Hadoop is tab-delimited key/value pairs
                var sArr = line.Split('\t');
                // Get hello word
                string word = sArr[0];
                // Get hello count
                int count = Convert.ToInt32(sArr[1]);

                //Do we already have a count for hello word?
                if(words.ContainsKey(word))
                {
                    //If so, increment hello count
                    words[word] += count;
                } else
                {
                    //Add hello key toohello collection
                    words.Add(word, count);
                }
            }
            //Finally, emit each word and count
            foreach (var word in words)
            {
                //Emit tab-delimited key/value pairs.
                //In this case, a word and a count of 1.
                Console.WriteLine("{0}\t{1}", word.Key, word.Value);
            }
        }
    }
}
```

Na het maken van de toepassing hello samenstellen tooproduce hello `/bin/Debug/reducer.exe` bestand in de projectmap Hallo.

## <a name="upload-toostorage"></a>Toostorage uploaden

1. Open in Visual Studio **Server Explorer**.

2. Vouw **Azure** uit en vouw vervolgens **HDInsight** uit.

3. Als u wordt gevraagd, Voer uw referenties in Azure-abonnement en klik vervolgens op **aanmelden**.

4. Hallo HDInsight-cluster dat u deze toepassing toodeploy wilt uitbreiden. Een item met de tekst hello __(Default Storage Account)__ wordt vermeld.

    ![Server Explorer Hallo storage-account voor Hallo cluster weergeven](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * Als dit item kan worden uitgebreid, gebruikt u een __Azure Storage-Account__ als standaard opslag voor Hallo-cluster. tooview hello bestanden op Hallo standaard opslag voor Hallo-cluster, vouw Hallo vermelding en dubbelklik vervolgens op Hallo __(standaardcontainer)__.

    * Als dit item kan niet worden uitgebreid, gebruikt u __Azure Data Lake Store__ als Hallo standaard opslag voor Hallo-cluster. tooview hello bestanden op Hallo standaard opslag voor Hallo-cluster, dubbelklikt u op Hallo __(Standaardopslagaccount)__ vermelding.

5. tooupload hello .exe-bestanden, een van de volgende methoden hello gebruiken:

    * Als u een __Azure Storage-Account__op Hallo uploaden pictogram en blader vervolgens toohello **bin\debug** map voor Hallo **mapper** project. Tot slot selecteert Hallo **mapper.exe** -bestand en klik op **Ok**.

        ![pictogram uploaden](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * Als u __Azure Data Lake Store__, met de rechtermuisknop op een leeg gebied in Hallo bestand aanbieding en selecteer vervolgens __uploaden__. Tot slot selecteert Hallo **mapper.exe** -bestand en klik op **Open**.

    Eenmaal Hallo __mapper.exe__ uploaden is voltooid, herhaalt Hallo uploadproces voor Hallo __reducer.exe__ bestand.

## <a name="run-a-job-using-an-ssh-session"></a>Een taak uitvoeren: met behulp van een SSH-sessie

1. SSH tooconnect toohello HDInsight-cluster gebruiken. Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

2. Gebruik een van de volgende opdracht toostart hello MapReduce-taak Hallo:

    * Als u __Data Lake Store__ als standaard opslag:

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * Als u __Azure Storage__ als standaard opslag:

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    Hallo volgende lijst beschrijft wat elke parameter doet:

    * `hadoop-streaming.jar`: Hallo jar-bestand met de Hallo streaming MapReduce-functionaliteit.
    * `-files`: Hiermee voegt u Hallo `mapper.exe` en `reducer.exe` bestanden toothis taak. Hallo `adl:///` of `wasb:///` voordat elk bestand Hallo pad toohello hoofdmap van de standaard opslagruimte voor Hallo-cluster is.
    * `-mapper`: Hiermee geeft u op welk bestand implementeert Hallo toewijzen.
    * `-reducer`: Hiermee geeft u op welk bestand Hallo reducer implementeert.
    * `-input`: Hallo invoergegevens.
    * `-output`: de uitvoermap Hallo.

3. Zodra het Hallo MapReduce-taak is voltooid, gebruikt u Hallo tooview Hallo resultaten te volgen:

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    Hallo is volgende tekst een voorbeeld van Hallo-gegevens geretourneerd door deze opdracht:

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a>Een taak uitvoeren: met behulp van PowerShell

Gebruik Hallo volgende PowerShell-script toorun een MapReduce-taak en Hallo resultaten te downloaden.

[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]

Dit script wordt u gevraagd om Hallo cluster account aanmeldingsnaam en wachtwoord, samen met de naam van een Hallo HDInsight-cluster. Zodra het Hallo-taak is voltooid, Hallo uitvoer gedownloade toohello is `output.txt` vanaf bestand in Hallo directory Hallo script wordt uitgevoerd. Hallo volgende tekst is een voorbeeld van gegevens in Hallo Hallo `output.txt` bestand:

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over het gebruik van MapReduce met HDInsight [MapReduce gebruiken met HDInsight](hdinsight-use-mapreduce.md).

Zie voor meer informatie over het gebruik van C# met Hive en Pig [een C# door de gebruiker gedefinieerde functie gebruiken met Hive en Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).

Zie voor meer informatie over het gebruik van C# met Storm op HDInsight [C#-topologieën ontwikkelen voor Storm op HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).