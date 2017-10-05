---
title: Streaming-MapReduce-taken met HDInsight - Azure Python ontwikkelen | Microsoft Docs
description: Informatie over het gebruik van Python in streaming MapReduce-taken. Hadoop biedt een streaming-API voor MapReduce voor het schrijven in andere talen dan Java.
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
ms.openlocfilehash: b86605c49291a99f49c4b2841d46324cfd0db56d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="develop-python-streaming-mapreduce-programs-for-hdinsight"></a><span data-ttu-id="d9a83-104">Python streaming MapReduce-programma's voor HDInsight ontwikkelen</span><span class="sxs-lookup"><span data-stu-id="d9a83-104">Develop Python streaming MapReduce programs for HDInsight</span></span>

<span data-ttu-id="d9a83-105">Informatie over het gebruik van Python in streaming MapReduce-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="d9a83-105">Learn how to use Python in streaming MapReduce operations.</span></span> <span data-ttu-id="d9a83-106">Hadoop biedt een streaming-API voor MapReduce waarmee u kunt schrijven kaart en functies in andere talen dan Java te verminderen.</span><span class="sxs-lookup"><span data-stu-id="d9a83-106">Hadoop provides a streaming API for MapReduce that enables you to write map and reduce functions in languages other than Java.</span></span> <span data-ttu-id="d9a83-107">De stappen in dit document implementeren van de kaart en onderdelen in Python verminderen.</span><span class="sxs-lookup"><span data-stu-id="d9a83-107">The steps in this document implement the Map and Reduce components in Python.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9a83-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d9a83-108">Prerequisites</span></span>

* <span data-ttu-id="d9a83-109">Een op Linux gebaseerde Hadoop op HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="d9a83-109">A Linux-based Hadoop on HDInsight cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d9a83-110">De stappen in dit document moet een HDInsight-cluster dat gebruik maakt van Linux.</span><span class="sxs-lookup"><span data-stu-id="d9a83-110">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="d9a83-111">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="d9a83-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d9a83-112">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d9a83-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="d9a83-113">Een teksteditor</span><span class="sxs-lookup"><span data-stu-id="d9a83-113">A text editor</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d9a83-114">De teksteditor moet LF gebruiken als het beëindigen van de regel.</span><span class="sxs-lookup"><span data-stu-id="d9a83-114">The text editor must use LF as the line ending.</span></span> <span data-ttu-id="d9a83-115">Met behulp van een regel beëindigen van CRLF zorgt ervoor dat fouten bij het uitvoeren van de MapReduce-taak op Linux gebaseerde HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="d9a83-115">Using a line ending of CRLF causes errors when running the MapReduce job on Linux-based HDInsight clusters.</span></span>

* <span data-ttu-id="d9a83-116">De `ssh` en `scp` opdrachten, of [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span><span class="sxs-lookup"><span data-stu-id="d9a83-116">The `ssh` and `scp` commands, or [Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-3.8.0)</span></span>

## <a name="word-count"></a><span data-ttu-id="d9a83-117">Aantal woorden</span><span class="sxs-lookup"><span data-stu-id="d9a83-117">Word count</span></span>

<span data-ttu-id="d9a83-118">In dit voorbeeld is een aantal eenvoudige woorden die zijn geïmplementeerd in een python een toewijzen en reducer.</span><span class="sxs-lookup"><span data-stu-id="d9a83-118">This example is a basic word count implemented in a python a mapper and reducer.</span></span> <span data-ttu-id="d9a83-119">De mapper zinnen opgesplitst in afzonderlijke woorden en de reducer de woorden samenvoegt en telt de uitvoer te produceren.</span><span class="sxs-lookup"><span data-stu-id="d9a83-119">The mapper breaks sentences into individual words, and the reducer aggregates the words and counts to produce the output.</span></span>

<span data-ttu-id="d9a83-120">Het volgende stroomdiagram ziet u wat er gebeurt tijdens de kaart en fasen te verminderen.</span><span class="sxs-lookup"><span data-stu-id="d9a83-120">The following flowchart illustrates what happens during the map and reduce phases.</span></span>

![afbeelding van het mapreduce-proces](./media/hdinsight-hadoop-streaming-python/HDI.WordCountDiagram.png)

## <a name="streaming-mapreduce"></a><span data-ttu-id="d9a83-122">Streaming MapReduce</span><span class="sxs-lookup"><span data-stu-id="d9a83-122">Streaming MapReduce</span></span>

<span data-ttu-id="d9a83-123">Hadoop kunt u een bestand opgeeft dat de kaart bevat en logica die wordt gebruikt door een taak te verminderen.</span><span class="sxs-lookup"><span data-stu-id="d9a83-123">Hadoop allows you to specify a file that contains the map and reduce logic that is used by a job.</span></span> <span data-ttu-id="d9a83-124">De specifieke vereisten voor de kaart en logica te verminderen zijn:</span><span class="sxs-lookup"><span data-stu-id="d9a83-124">The specific requirements for the map and reduce logic are:</span></span>

* <span data-ttu-id="d9a83-125">**Invoer**: de kaart en verminderen onderdelen invoergegevens van STDIN moeten lezen.</span><span class="sxs-lookup"><span data-stu-id="d9a83-125">**Input**: The map and reduce components must read input data from STDIN.</span></span>
* <span data-ttu-id="d9a83-126">**Uitvoer**: de kaart en de onderdelen moeten uitvoergegevens naar STDOUT schrijven.</span><span class="sxs-lookup"><span data-stu-id="d9a83-126">**Output**: The map and reduce components must write output data to STDOUT.</span></span>
* <span data-ttu-id="d9a83-127">**Gegevensindeling**: de gegevens die worden gebruikt en die wordt geproduceerd moet een sleutel-waardepaar, gescheiden door een tab-teken.</span><span class="sxs-lookup"><span data-stu-id="d9a83-127">**Data format**: The data consumed and produced must be a key/value pair, separated by a tab character.</span></span>

<span data-ttu-id="d9a83-128">Python eenvoudig deze vereisten kan verwerken met behulp van de `sys` module die u wilt lezen uit STDIN en het gebruik van `print` af te drukken op STDOUT.</span><span class="sxs-lookup"><span data-stu-id="d9a83-128">Python can easily handle these requirements by using the `sys` module to read from STDIN and using `print` to print to STDOUT.</span></span> <span data-ttu-id="d9a83-129">De resterende taak is gewoon de gegevens op een tabblad formatteren (`\t`) tussen de sleutel en waarde teken.</span><span class="sxs-lookup"><span data-stu-id="d9a83-129">The remaining task is simply formatting the data with a tab (`\t`) character between the key and value.</span></span>

## <a name="create-the-mapper-and-reducer"></a><span data-ttu-id="d9a83-130">De toewijzen en reducer maken</span><span class="sxs-lookup"><span data-stu-id="d9a83-130">Create the mapper and reducer</span></span>

1. <span data-ttu-id="d9a83-131">Maak een bestand met de naam `mapper.py` en de volgende code gebruiken als de inhoud:</span><span class="sxs-lookup"><span data-stu-id="d9a83-131">Create a file named `mapper.py` and use the following code as the content:</span></span>

   ```python
   #!/usr/bin/env python

   # Use the sys module
   import sys

   # 'file' in this case is STDIN
   def read_input(file):
       # Split each line into words
       for line in file:
           yield line.split()

   def main(separator='\t'):
       # Read the data using read_input
       data = read_input(sys.stdin)
       # Process each word returned from read_input
       for words in data:
           # Process each word
           for word in words:
               # Write to STDOUT
               print '%s%s%d' % (word, separator, 1)

   if __name__ == "__main__":
       main()
   ```

2. <span data-ttu-id="d9a83-132">Maak een bestand met de naam **reducer.py** en de volgende code gebruiken als de inhoud:</span><span class="sxs-lookup"><span data-stu-id="d9a83-132">Create a file named **reducer.py** and use the following code as the content:</span></span>

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
           # Strip out the separator character
           yield line.rstrip().split(separator, 1)

   def main(separator='\t'):
       # Read the data using read_mapper_output
       data = read_mapper_output(sys.stdin, separator=separator)
       # Group words and counts into 'group'
       #   Since MapReduce is a distributed process, each word
       #   may have multiple counts. 'group' will have all counts
       #   which can be retrieved using the word as the key.
       for current_word, group in groupby(data, itemgetter(0)):
           try:
               # For each word, pull the count(s) for the word
               #   from 'group' and create a total count
               total_count = sum(int(count) for current_word, count in group)
               # Write to stdout
               print "%s%s%d" % (current_word, separator, total_count)
           except ValueError:
               # Count was not a number, so do nothing
               pass

   if __name__ == "__main__":
       main()
   ```

## <a name="run-using-powershell"></a><span data-ttu-id="d9a83-133">Uitvoeren met PowerShell</span><span class="sxs-lookup"><span data-stu-id="d9a83-133">Run using PowerShell</span></span>

<span data-ttu-id="d9a83-134">Om ervoor te zorgen dat uw bestanden rechts regeleinden, gebruikt u de volgende PowerShell-script:</span><span class="sxs-lookup"><span data-stu-id="d9a83-134">To ensure that your files have the right line endings, use the following PowerShell script:</span></span>

<span data-ttu-id="d9a83-135">[!code-powershell[belangrijkste](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]</span><span class="sxs-lookup"><span data-stu-id="d9a83-135">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=138-140)]</span></span>

<span data-ttu-id="d9a83-136">Gebruik de volgende PowerShell-script de bestanden uploaden, voer de taak en de uitvoer weergeven:</span><span class="sxs-lookup"><span data-stu-id="d9a83-136">Use the following PowerShell script to upload the files, run the job, and view the output:</span></span>

<span data-ttu-id="d9a83-137">[!code-powershell[belangrijkste](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]</span><span class="sxs-lookup"><span data-stu-id="d9a83-137">[!code-powershell[main](../../powershell_scripts/hdinsight/streaming-python/streaming-python.ps1?range=5-134)]</span></span>

## <a name="run-from-an-ssh-session"></a><span data-ttu-id="d9a83-138">Uitvoeren van een SSH-sessie</span><span class="sxs-lookup"><span data-stu-id="d9a83-138">Run from an SSH session</span></span>

1. <span data-ttu-id="d9a83-139">Van uw ontwikkelomgeving in dezelfde map als `mapper.py` en `reducer.py` bestanden, gebruik de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d9a83-139">From your development environment, in the same directory as `mapper.py` and `reducer.py` files, use the following command:</span></span>

    ```bash
    scp mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:
    ```

    <span data-ttu-id="d9a83-140">Vervang `username` met de SSH-gebruikersnaam voor uw cluster en `clustername` met de naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="d9a83-140">Replace `username` with the SSH user name for your cluster, and `clustername` with the name of your cluster.</span></span>

    <span data-ttu-id="d9a83-141">Met deze opdracht kopieert de bestanden van het lokale systeem met het hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="d9a83-141">This command copies the files from the local system to the head node.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d9a83-142">Als u een wachtwoord gebruikt om uw SSH-account te beveiligen, wordt u gevraagd het wachtwoord op te geven.</span><span class="sxs-lookup"><span data-stu-id="d9a83-142">If you used a password to secure your SSH account, you are prompted for the password.</span></span> <span data-ttu-id="d9a83-143">Als u een SSH-sleutel gebruikt, moet u mogelijk gebruiken de `-i` parameter en het pad naar de persoonlijke sleutel.</span><span class="sxs-lookup"><span data-stu-id="d9a83-143">If you used an SSH key, you may have to use the `-i` parameter and the path to the private key.</span></span> <span data-ttu-id="d9a83-144">Bijvoorbeeld `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span><span class="sxs-lookup"><span data-stu-id="d9a83-144">For example, `scp -i /path/to/private/key mapper.py reducer.py username@clustername-ssh.azurehdinsight.net:`.</span></span>

2. <span data-ttu-id="d9a83-145">Verbinding maken met het cluster via SSH:</span><span class="sxs-lookup"><span data-stu-id="d9a83-145">Connect to the cluster by using SSH:</span></span>

    ```bash
    ssh username@clustername-ssh.azurehdinsight.net`
    ```

    <span data-ttu-id="d9a83-146">Zie voor meer informatie over [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d9a83-146">For more information on, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

3. <span data-ttu-id="d9a83-147">De mapper.py en reducer.py hebt de juiste regeleinden, gebruik de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="d9a83-147">To ensure the mapper.py and reducer.py have the correct line endings, use the following commands:</span></span>

    ```bash
    perl -pi -e 's/\r\n/\n/g' mapper.py
    perl -pi -e 's/\r\n/\n/g' reducer.py
    ```

4. <span data-ttu-id="d9a83-148">Gebruik de volgende opdracht de MapReduce-taak starten.</span><span class="sxs-lookup"><span data-stu-id="d9a83-148">Use the following command to start the MapReduce job.</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files mapper.py,reducer.py -mapper mapper.py -reducer reducer.py -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
    ```

    <span data-ttu-id="d9a83-149">Deze opdracht heeft de volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="d9a83-149">This command has the following parts:</span></span>

   * <span data-ttu-id="d9a83-150">**hadoop-streaming.jar**: gebruikt bij het uitvoeren van streaming MapReduce-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="d9a83-150">**hadoop-streaming.jar**: Used when performing streaming MapReduce operations.</span></span> <span data-ttu-id="d9a83-151">Het Hadoop-interfaces met de externe MapReduce-code die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="d9a83-151">It interfaces Hadoop with the external MapReduce code you provide.</span></span>

   * <span data-ttu-id="d9a83-152">**-bestanden**: de opgegeven bestanden toevoegt aan de MapReduce-taak.</span><span class="sxs-lookup"><span data-stu-id="d9a83-152">**-files**: Adds the specified files to the MapReduce job.</span></span>

   * <span data-ttu-id="d9a83-153">**-toewijzer**: vertelt Hadoop welk bestand moet worden gebruikt als de toewijzen.</span><span class="sxs-lookup"><span data-stu-id="d9a83-153">**-mapper**: Tells Hadoop which file to use as the mapper.</span></span>

   * <span data-ttu-id="d9a83-154">**-reducer**: vertelt Hadoop welk bestand moet worden gebruikt als de reducer.</span><span class="sxs-lookup"><span data-stu-id="d9a83-154">**-reducer**: Tells Hadoop which file to use as the reducer.</span></span>

   * <span data-ttu-id="d9a83-155">**-invoer**: het bestand voor invoer die moeten worden geteld woorden uit.</span><span class="sxs-lookup"><span data-stu-id="d9a83-155">**-input**: The input file that we should count words from.</span></span>

   * <span data-ttu-id="d9a83-156">**-uitvoer**: de map die de uitvoer naar worden geschreven.</span><span class="sxs-lookup"><span data-stu-id="d9a83-156">**-output**: The directory that the output is written to.</span></span>

    <span data-ttu-id="d9a83-157">Als de MapReduce-taak werkt, wordt het proces weergegeven als percentage.</span><span class="sxs-lookup"><span data-stu-id="d9a83-157">As the MapReduce job works, the process is displayed as percentages.</span></span>

        <span data-ttu-id="d9a83-158">15-02-05 19:01:04 INFO mapreduce. Taak: kaart 0% verminderen 0% 15-02-05 19:01:16 INFO mapreduce. Taak: kaart 100% verminderen 0% 15-02-05 19:01:27 INFO mapreduce. Taak: kaart 100% verminderen 100%</span><span class="sxs-lookup"><span data-stu-id="d9a83-158">15/02/05 19:01:04 INFO mapreduce.Job:  map 0% reduce 0%    15/02/05 19:01:16 INFO mapreduce.Job:  map 100% reduce 0%    15/02/05 19:01:27 INFO mapreduce.Job:  map 100% reduce 100%</span></span>


5. <span data-ttu-id="d9a83-159">Gebruik de volgende opdracht om de weergave van de uitvoer:</span><span class="sxs-lookup"><span data-stu-id="d9a83-159">To view the output, use the following command:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="d9a83-160">Met deze opdracht geeft een lijst met woorden en hoe vaak het woord is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="d9a83-160">This command displays a list of words and how many times the word occurred.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9a83-161">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d9a83-161">Next steps</span></span>

<span data-ttu-id="d9a83-162">U hebt geleerd hoe u streaming MapRedcue taken gebruiken met HDInsight, gebruik de volgende koppelingen om te verkennen andere manieren om te werken met Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d9a83-162">Now that you have learned how to use streaming MapRedcue jobs with HDInsight, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* [<span data-ttu-id="d9a83-163">Hive gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="d9a83-163">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="d9a83-164">Pig gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="d9a83-164">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="d9a83-165">MapReduce-taken gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="d9a83-165">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
