---
title: aaaDevelop Python streaming MapReduce-taken met HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe toouse Python in de streaming MapReduce-taken. Hadoop biedt een streaming-API voor MapReduce voor het schrijven in andere talen dan Java.
services: hdinsight
keyword: mapreduce python,python map reduce,python mapreduce
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 7631d8d9-98ae-42ec-b9ec-ee3cf7e57fb3
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: a6ae3ba650b665ecc5839a4ddf5282f8ccfb6bd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a>Python streaming MapReduce-programma's voor HDInsight ontwikkelen

Meer informatie over hoe toouse Python in de streaming MapReduce-bewerkingen. Hadoop biedt een streaming-API voor MapReduce waarmee u toowrite kaart en functies in andere talen dan Java verminderen. Hallo stappen in dit document Hallo kaart implementeren en verminderen het Python-onderdelen.

## <a name="prerequisites"></a>Vereisten

* Een op Linux gebaseerde Hadoop op HDInsight-cluster

  > [!IMPORTANT]
  > Hallo stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

* Een teksteditor

  > [!IMPORTANT]
  > Hallo teksteditor moet LF gebruiken als Hallo regel beëindigen. Met behulp van een regel beëindigen van CRLF zorgt ervoor dat fouten bij het uitvoeren van Hallo MapReduce-taak op Linux gebaseerde HDInsight-clusters.

* Hallo `ssh` en `scp` opdrachten, of [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)

## <a name="word-count"></a>Aantal woorden

In dit voorbeeld is een aantal eenvoudige woorden die zijn geïmplementeerd in een python een toewijzen en reducer. Hallo mapper zinnen opgesplitst in afzonderlijke woorden en Hallo reducer aggregeert Hallo woorden en tooproduce Hallo uitvoer telt.

Hallo volgende stroomdiagram ziet u wat er gebeurt tijdens het Hallo-kaart en fasen te verminderen.

![afbeelding van Hallo mapreduce-proces](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a>Streaming MapReduce

Hadoop kunt u toospecify een bestand dat Hallo toewijzing bevat en logica die wordt gebruikt door een taak te verminderen. specifieke vereisten voor Hallo Hallo toewijzen en logica te verminderen zijn:

* **Invoer**: Hallo kaart en verminderen onderdelen invoergegevens van STDIN moeten lezen.
* **Uitvoer**: Hallo kaart en verminderen onderdelen uitvoer gegevens tooSTDOUT moeten schrijven.
* **Gegevensindeling**: Hallo gegevens verbruikt en geproduceerd moet een sleutel-waardepaar, gescheiden door een tab-teken.

Python eenvoudig deze vereisten kan verwerken met behulp van Hallo `sys` module tooread uit STDIN `print` tooprint tooSTDOUT. Hallo resterende taak is eenvoudig hello gegevens formatteren met een tabblad (`\t`) teken tussen Hallo-sleutel en waarde.

## <a name="create-hello-mapper-and-reducer"></a>Hallo toewijzen en reducer maken

1. Maak een bestand met de naam `mapper.py` en Hallo gebruik de volgende code als Hallo inhoud:

   ```python
   #!/usr/bin/env python

   # Use hello sys module
   import sys

   # 'file' in this case is STDIN
   def read_input(file):
       # Split each line into words
       for line in file:
           yield line.split()

   def main(separator='\t'):
       # Read hello data using read_input
       data = read_input(sys.stdin)
       # Process each word returned from read_input
       for words in data:
           # Process each word
           for word in words:
               # Write tooSTDOUT
               print '%s%s%d' % (word, separator, 1)

   if __name__ == "__main__":
       main()
   ```

2. Maak een bestand met de naam **reducer.py** en Hallo gebruik de volgende code als Hallo inhoud:

   ```python
   #!/usr/bin/env python

   # import modules
   from itertools import groupby
   from operator import itemgetter
   import sys

   # 'file' in this case is STDIN
   def read_mapper_output(file, separator='\t'):
       # Go through each line
       for line in file:
           # Strip out hello separator character
           yield line.rstrip().split(separator, 1)

   def main(separator='\t'):
       # Read hello data using read_mapper_output
       data = read_mapper_output(sys.stdin, separator=separator)
       # Group words and counts into 'group'
       #   Since MapReduce is a distributed process, each word
       #   may have multiple counts. 'group' will have all counts
       #   which can be retrieved using hello word as hello key.
       for current_word, group in groupby(data, itemgetter(0)):
           try:
               # For each word, pull hello count(s) for hello word
               #   from 'group' and create a total count
               total_count = sum(int(count) for current_word, count in group)
               # Write toostdout
               print "%s%s%d" % (current_word, separator, total_count)
           except ValueError:
               # Count was not a number, so do nothing
               pass

   if __name__ == "__main__":
       main()
   ```

## <a name="run-using-powershell"></a>Uitvoeren met PowerShell

tooensure dat uw bestanden hebben het juiste regeleinden hello, gebruik Hallo volgende PowerShell-script:

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]

Hallo volgende PowerShell-script tooupload Hallo bestanden gebruiken, Hallo taak uitvoeren en Hallo uitvoer weergeven:

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]

## <a name="run-from-an-ssh-session"></a>Uitvoeren van een SSH-sessie

1. Van uw ontwikkelomgeving in Hallo dezelfde map als `mapper.py` en `reducer.py` bestanden, Hallo volgende opdracht gebruiken:

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    Vervang `username` met Hallo SSH-gebruikersnaam voor uw cluster en `clustername` met Hallo-naam van het cluster.

    Met deze opdracht kopieert Hallo-bestanden van Hallo lokaal systeem toohello hoofdknooppunt.

    > [!NOTE]
    > Als u een wachtwoord toosecure uw SSH-account gebruikt, wordt u gevraagd Hallo wachtwoord op te geven. Als u een SSH-sleutel gebruikt, hebt u mogelijk toouse hello `-i` parameter en Hallo pad toohello persoonlijke sleutel. Bijvoorbeeld `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.

2. Verbinding toohello cluster via SSH:

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    Zie voor meer informatie over [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. tooensure hello mapper.py en reducer.py hebben Hallo regeleinden corrigeren, gebruikt u Hallo volgende opdrachten:

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. Gebruik Hallo opdracht toostart hello MapReduce-taak te volgen.

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    Deze opdracht heeft Hallo volgende onderdelen:

   * **hadoop-streaming.jar**: gebruikt bij het uitvoeren van streaming MapReduce-bewerkingen. Het Hadoop-interfaces met Hallo externe MapReduce code die u opgeeft.

   * **-bestanden**: voegt Hallo opgegeven bestanden toohello MapReduce-taak.

   * **-toewijzer**: vertelt Hadoop die toouse bestand zoals Hallo toewijzen.

   * **-reducer**: vertelt Hadoop die toouse bestand zoals Hallo reducer.

   * **-invoer**: Hallo bestand voor invoer die moeten worden geteld woorden uit.

   * **-uitvoer**: Hallo-map die Hallo uitvoer naar worden geschreven.

    Hallo MapReduce-taak werkt, Hallo proces weergegeven als percentage.

        15-02-05 19:01:04 INFO mapreduce. Taak: kaart 0% verminderen 0% 15-02-05 19:01:16 INFO mapreduce. Taak: kaart 100% verminderen 0% 15-02-05 19:01:27 INFO mapreduce. Taak: kaart 100% verminderen 100%


5. Hallo tooview uitvoer Hallo volgende opdracht gebruiken:

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    Met deze opdracht geeft een lijst met woorden en hoe vaak Hallo word is opgetreden.

## <a name="next-steps"></a>Volgende stappen

U hebt geleerd hoe toouse MapRedcue streaming taken met HDInsight, gebruik dan Hallo tooexplore koppelingen volgen andere manieren toowork met Azure HDInsight.

* [Hive gebruiken met HDInsight](hdinsight-use-hive.md)
* [Pig gebruiken met HDInsight](hdinsight-use-pig.md)
* [MapReduce-taken gebruiken met HDInsight](hdinsight-use-mapreduce.md)
