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
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a><span data-ttu-id="5f560-104">Python streaming MapReduce-programma's voor HDInsight ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="5f560-104">Develop Python streaming MapReduce programs for HDInsight</span></span>

<span data-ttu-id="5f560-105">Meer informatie over hoe toouse Python in de streaming MapReduce-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="5f560-105">Learn how toouse Python in streaming MapReduce operations.</span></span> <span data-ttu-id="5f560-106">Hadoop biedt een streaming-API voor MapReduce waarmee u toowrite kaart en functies in andere talen dan Java verminderen.</span><span class="sxs-lookup"><span data-stu-id="5f560-106">Hadoop provides a streaming API for MapReduce that enables you toowrite map and reduce functions in languages other than Java.</span></span> <span data-ttu-id="5f560-107">Hallo stappen in dit document Hallo kaart implementeren en verminderen het Python-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="5f560-107">hello steps in this document implement hello Map and Reduce components in Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f560-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5f560-108">Prerequisites</span></span>

* <span data-ttu-id="5f560-109">Een op Linux gebaseerde Hadoop op HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="5f560-109">A Linux-based Hadoop on HDInsight cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5f560-110">Hallo stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux.</span><span class="sxs-lookup"><span data-stu-id="5f560-110">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="5f560-111">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="5f560-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5f560-112">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5f560-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="5f560-113">Een teksteditor</span><span class="sxs-lookup"><span data-stu-id="5f560-113">A text editor</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5f560-114">Hallo teksteditor moet LF gebruiken als Hallo regel beëindigen.</span><span class="sxs-lookup"><span data-stu-id="5f560-114">hello text editor must use LF as hello line ending.</span></span> <span data-ttu-id="5f560-115">Met behulp van een regel beëindigen van CRLF zorgt ervoor dat fouten bij het uitvoeren van Hallo MapReduce-taak op Linux gebaseerde HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="5f560-115">Using a line ending of CRLF causes errors when running hello MapReduce job on Linux-based HDInsight clusters.</span></span>

* <span data-ttu-id="5f560-116">Hallo `ssh` en `scp` opdrachten, of [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span><span class="sxs-lookup"><span data-stu-id="5f560-116">hello `ssh` and `scp` commands, or [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span></span>

## <a name="word-count"></a><span data-ttu-id="5f560-117">Aantal woorden</span><span class="sxs-lookup"><span data-stu-id="5f560-117">Word count</span></span>

<span data-ttu-id="5f560-118">In dit voorbeeld is een aantal eenvoudige woorden die zijn geïmplementeerd in een python een toewijzen en reducer.</span><span class="sxs-lookup"><span data-stu-id="5f560-118">This example is a basic word count implemented in a python a mapper and reducer.</span></span> <span data-ttu-id="5f560-119">Hallo mapper zinnen opgesplitst in afzonderlijke woorden en Hallo reducer aggregeert Hallo woorden en tooproduce Hallo uitvoer telt.</span><span class="sxs-lookup"><span data-stu-id="5f560-119">hello mapper breaks sentences into individual words, and hello reducer aggregates hello words and counts tooproduce hello output.</span></span>

<span data-ttu-id="5f560-120">Hallo volgende stroomdiagram ziet u wat er gebeurt tijdens het Hallo-kaart en fasen te verminderen.</span><span class="sxs-lookup"><span data-stu-id="5f560-120">hello following flowchart illustrates what happens during hello map and reduce phases.</span></span>

![afbeelding van Hallo mapreduce-proces](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a><span data-ttu-id="5f560-122">Streaming MapReduce</span><span class="sxs-lookup"><span data-stu-id="5f560-122">Streaming MapReduce</span></span>

<span data-ttu-id="5f560-123">Hadoop kunt u toospecify een bestand dat Hallo toewijzing bevat en logica die wordt gebruikt door een taak te verminderen.</span><span class="sxs-lookup"><span data-stu-id="5f560-123">Hadoop allows you toospecify a file that contains hello map and reduce logic that is used by a job.</span></span> <span data-ttu-id="5f560-124">specifieke vereisten voor Hallo Hallo toewijzen en logica te verminderen zijn:</span><span class="sxs-lookup"><span data-stu-id="5f560-124">hello specific requirements for hello map and reduce logic are:</span></span>

* <span data-ttu-id="5f560-125">**Invoer**: Hallo kaart en verminderen onderdelen invoergegevens van STDIN moeten lezen.</span><span class="sxs-lookup"><span data-stu-id="5f560-125">**Input**: hello map and reduce components must read input data from STDIN.</span></span>
* <span data-ttu-id="5f560-126">**Uitvoer**: Hallo kaart en verminderen onderdelen uitvoer gegevens tooSTDOUT moeten schrijven.</span><span class="sxs-lookup"><span data-stu-id="5f560-126">**Output**: hello map and reduce components must write output data tooSTDOUT.</span></span>
* <span data-ttu-id="5f560-127">**Gegevensindeling**: Hallo gegevens verbruikt en geproduceerd moet een sleutel-waardepaar, gescheiden door een tab-teken.</span><span class="sxs-lookup"><span data-stu-id="5f560-127">**Data format**: hello data consumed and produced must be a key/value pair, separated by a tab character.</span></span>

<span data-ttu-id="5f560-128">Python eenvoudig deze vereisten kan verwerken met behulp van Hallo `sys` module tooread uit STDIN `print` tooprint tooSTDOUT.</span><span class="sxs-lookup"><span data-stu-id="5f560-128">Python can easily handle these requirements by using hello `sys` module tooread from STDIN and using `print` tooprint tooSTDOUT.</span></span> <span data-ttu-id="5f560-129">Hallo resterende taak is eenvoudig hello gegevens formatteren met een tabblad (`\t`) teken tussen Hallo-sleutel en waarde.</span><span class="sxs-lookup"><span data-stu-id="5f560-129">hello remaining task is simply formatting hello data with a tab (`\t`) character between hello key and value.</span></span>

## <a name="create-hello-mapper-and-reducer"></a><span data-ttu-id="5f560-130">Hallo toewijzen en reducer maken</span><span class="sxs-lookup"><span data-stu-id="5f560-130">Create hello mapper and reducer</span></span>

1. <span data-ttu-id="5f560-131">Maak een bestand met de naam `mapper.py` en Hallo gebruik de volgende code als Hallo inhoud:</span><span class="sxs-lookup"><span data-stu-id="5f560-131">Create a file named `mapper.py` and use hello following code as hello content:</span></span>

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

2. <span data-ttu-id="5f560-132">Maak een bestand met de naam **reducer.py** en Hallo gebruik de volgende code als Hallo inhoud:</span><span class="sxs-lookup"><span data-stu-id="5f560-132">Create a file named **reducer.py** and use hello following code as hello content:</span></span>

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

## <a name="run-using-powershell"></a><span data-ttu-id="5f560-133">Uitvoeren met PowerShell</span><span class="sxs-lookup"><span data-stu-id="5f560-133">Run using PowerShell</span></span>

<span data-ttu-id="5f560-134">tooensure dat uw bestanden hebben het juiste regeleinden hello, gebruik Hallo volgende PowerShell-script:</span><span class="sxs-lookup"><span data-stu-id="5f560-134">tooensure that your files have hello right line endings, use hello following PowerShell script:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]

<span data-ttu-id="5f560-135">Hallo volgende PowerShell-script tooupload Hallo bestanden gebruiken, Hallo taak uitvoeren en Hallo uitvoer weergeven:</span><span class="sxs-lookup"><span data-stu-id="5f560-135">Use hello following PowerShell script tooupload hello files, run hello job, and view hello output:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]

## <a name="run-from-an-ssh-session"></a><span data-ttu-id="5f560-136">Uitvoeren van een SSH-sessie</span><span class="sxs-lookup"><span data-stu-id="5f560-136">Run from an SSH session</span></span>

1. <span data-ttu-id="5f560-137">Van uw ontwikkelomgeving in Hallo dezelfde map als `mapper.py` en `reducer.py` bestanden, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5f560-137">From your development environment, in hello same directory as `mapper.py` and `reducer.py` files, use hello following command:</span></span>

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="5f560-138">Vervang `username` met Hallo SSH-gebruikersnaam voor uw cluster en `clustername` met Hallo-naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="5f560-138">Replace `username` with hello SSH user name for your cluster, and `clustername` with hello name of your cluster.</span></span>

    <span data-ttu-id="5f560-139">Met deze opdracht kopieert Hallo-bestanden van Hallo lokaal systeem toohello hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="5f560-139">This command copies hello files from hello local system toohello head node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5f560-140">Als u een wachtwoord toosecure uw SSH-account gebruikt, wordt u gevraagd Hallo wachtwoord op te geven.</span><span class="sxs-lookup"><span data-stu-id="5f560-140">If you used a password toosecure your SSH account, you are prompted for hello password.</span></span> <span data-ttu-id="5f560-141">Als u een SSH-sleutel gebruikt, hebt u mogelijk toouse hello `-i` parameter en Hallo pad toohello persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="5f560-141">If you used an SSH key, you may have toouse hello `-i` parameter and hello path toohello private key.</span></span> <span data-ttu-id="5f560-142">Bijvoorbeeld `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="5f560-142">For example, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="5f560-143">Verbinding toohello cluster via SSH:</span><span class="sxs-lookup"><span data-stu-id="5f560-143">Connect toohello cluster by using SSH:</span></span>

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    <span data-ttu-id="5f560-144">Zie voor meer informatie over [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5f560-144">For more information on, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="5f560-145">tooensure hello mapper.py en reducer.py hebben Hallo regeleinden corrigeren, gebruikt u Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="5f560-145">tooensure hello mapper.py and reducer.py have hello correct line endings, use hello following commands:</span></span>

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. <span data-ttu-id="5f560-146">Gebruik Hallo opdracht toostart hello MapReduce-taak te volgen.</span><span class="sxs-lookup"><span data-stu-id="5f560-146">Use hello following command toostart hello MapReduce job.</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    <span data-ttu-id="5f560-147">Deze opdracht heeft Hallo volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="5f560-147">This command has hello following parts:</span></span>

   * <span data-ttu-id="5f560-148">**hadoop-streaming.jar**: gebruikt bij het uitvoeren van streaming MapReduce-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="5f560-148">**hadoop-streaming.jar**: Used when performing streaming MapReduce operations.</span></span> <span data-ttu-id="5f560-149">Het Hadoop-interfaces met Hallo externe MapReduce code die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="5f560-149">It interfaces Hadoop with hello external MapReduce code you provide.</span></span>

   * <span data-ttu-id="5f560-150">**-bestanden**: voegt Hallo opgegeven bestanden toohello MapReduce-taak.</span><span class="sxs-lookup"><span data-stu-id="5f560-150">**-files**: Adds hello specified files toohello MapReduce job.</span></span>

   * <span data-ttu-id="5f560-151">**-toewijzer**: vertelt Hadoop die toouse bestand zoals Hallo toewijzen.</span><span class="sxs-lookup"><span data-stu-id="5f560-151">**-mapper**: Tells Hadoop which file toouse as hello mapper.</span></span>

   * <span data-ttu-id="5f560-152">**-reducer**: vertelt Hadoop die toouse bestand zoals Hallo reducer.</span><span class="sxs-lookup"><span data-stu-id="5f560-152">**-reducer**: Tells Hadoop which file toouse as hello reducer.</span></span>

   * <span data-ttu-id="5f560-153">**-invoer**: Hallo bestand voor invoer die moeten worden geteld woorden uit.</span><span class="sxs-lookup"><span data-stu-id="5f560-153">**-input**: hello input file that we should count words from.</span></span>

   * <span data-ttu-id="5f560-154">**-uitvoer**: Hallo-map die Hallo uitvoer naar worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="5f560-154">**-output**: hello directory that hello output is written to.</span></span>

    <span data-ttu-id="5f560-155">Hallo MapReduce-taak werkt, Hallo proces weergegeven als percentage.</span><span class="sxs-lookup"><span data-stu-id="5f560-155">As hello MapReduce job works, hello process is displayed as percentages.</span></span>

        <span data-ttu-id="5f560-156">15-02-05 19:01:04 INFO mapreduce. Taak: kaart 0% verminderen 0% 15-02-05 19:01:16 INFO mapreduce. Taak: kaart 100% verminderen 0% 15-02-05 19:01:27 INFO mapreduce. Taak: kaart 100% verminderen 100%</span><span class="sxs-lookup"><span data-stu-id="5f560-156">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span></span>


5. <span data-ttu-id="5f560-157">Hallo tooview uitvoer Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5f560-157">tooview hello output, use hello following command:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="5f560-158">Met deze opdracht geeft een lijst met woorden en hoe vaak Hallo word is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="5f560-158">This command displays a list of words and how many times hello word occurred.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5f560-159">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5f560-159">Next steps</span></span>

<span data-ttu-id="5f560-160">U hebt geleerd hoe toouse MapRedcue streaming taken met HDInsight, gebruik dan Hallo tooexplore koppelingen volgen andere manieren toowork met Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5f560-160">Now that you have learned how toouse streaming MapRedcue jobs with HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* [<span data-ttu-id="5f560-161">Hive gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f560-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="5f560-162">Pig gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f560-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="5f560-163">MapReduce-taken gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f560-163">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
