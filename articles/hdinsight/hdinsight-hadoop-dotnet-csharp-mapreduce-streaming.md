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
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="02870-103">Gebruik C# met MapReduce streaming van Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="02870-103">Use C# with MapReduce streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="02870-104">Meer informatie over hoe toouse C# toocreate een MapReduce-oplossing op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="02870-104">Learn how toouse C# toocreate a MapReduce solution on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="02870-105">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="02870-105">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="02870-106">Zie voor meer informatie [versiebeheer van HDInsight-onderdeel](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="02870-106">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="02870-107">Hadoop-streaming is een hulpprogramma waarmee u toorun MapReduce-taken met een script of uitvoerbaar bestand.</span><span class="sxs-lookup"><span data-stu-id="02870-107">Hadoop streaming is a utility that allows you toorun MapReduce jobs using a script or executable.</span></span> <span data-ttu-id="02870-108">In dit voorbeeld is .NET gebruikte tooimplement Hallo toewijzen en reducer voor een word-count-oplossing.</span><span class="sxs-lookup"><span data-stu-id="02870-108">In this example, .NET is used tooimplement hello mapper and reducer for a word count solution.</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="02870-109">.NET in HDInsight</span><span class="sxs-lookup"><span data-stu-id="02870-109">.NET on HDInsight</span></span>

<span data-ttu-id="02870-110">__HDInsight op basis van Linux__ clusters gebruik [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET-toepassingen.</span><span class="sxs-lookup"><span data-stu-id="02870-110">__Linux-based HDInsight__ clusters use [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="02870-111">Mono versie 4.2.1 is opgenomen in HDInsight versie 3.5.</span><span class="sxs-lookup"><span data-stu-id="02870-111">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="02870-112">Zie voor meer informatie over Hallo-versie van Mono opgenomen met HDInsight [HDInsight onderdeel versies](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="02870-112">For more information on hello version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="02870-113">toouse een specifieke versie van Mono, Zie Hallo [installeren of update Mono](hdinsight-hadoop-install-mono.md) document.</span><span class="sxs-lookup"><span data-stu-id="02870-113">toouse a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="02870-114">Zie voor meer informatie over de Mono compatibiliteit met versies van .NET Framework [Mono compatibiliteit](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="02870-114">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

## <a name="how-hadoop-streaming-works"></a><span data-ttu-id="02870-115">Hadoop-streaming werking</span><span class="sxs-lookup"><span data-stu-id="02870-115">How Hadoop streaming works</span></span>

<span data-ttu-id="02870-116">Hallo basisproces gebruikt voor streaming in dit document is als volgt:</span><span class="sxs-lookup"><span data-stu-id="02870-116">hello basic process used for streaming in this document is as follows:</span></span>

1. <span data-ttu-id="02870-117">Hadoop geeft STDIN toohello toewijzer (mapper.exe in dit voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="02870-117">Hadoop passes data toohello mapper (mapper.exe in this example) on STDIN.</span></span>
2. <span data-ttu-id="02870-118">Hallo mapper Hallo gegevens verwerkt, en door tabs gescheiden sleutel/waarde-paren tooSTDOUT verzendt.</span><span class="sxs-lookup"><span data-stu-id="02870-118">hello mapper processes hello data, and emits tab-delimited key/value pairs tooSTDOUT.</span></span>
3. <span data-ttu-id="02870-119">Hallo-uitvoer is gelezen door Hadoop en toohello reducer (reducer.exe in dit voorbeeld) en deze vervolgens STDIN doorgeven.</span><span class="sxs-lookup"><span data-stu-id="02870-119">hello output is read by Hadoop, and then passed toohello reducer (reducer.exe in this example) on STDIN.</span></span>
4. <span data-ttu-id="02870-120">Hallo reducer Hallo door tabs gescheiden sleutel/waarde-paren leest, Hallo gegevens verwerkt en vervolgens verzendt Hallo resultaat als door tabs gescheiden sleutel-waardeparen op STDOUT.</span><span class="sxs-lookup"><span data-stu-id="02870-120">hello reducer reads hello tab-delimited key/value pairs, processes hello data, and then emits hello result as tab-delimited key/value pairs on STDOUT.</span></span>
5. <span data-ttu-id="02870-121">Hallo-uitvoer is gelezen door Hadoop en toohello uitvoermap geschreven.</span><span class="sxs-lookup"><span data-stu-id="02870-121">hello output is read by Hadoop and written toohello output directory.</span></span>

<span data-ttu-id="02870-122">Zie voor meer informatie over het streaming- [Hadoop-Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span><span class="sxs-lookup"><span data-stu-id="02870-122">For more information on streaming, see [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02870-123">Vereisten</span><span class="sxs-lookup"><span data-stu-id="02870-123">Prerequisites</span></span>

* <span data-ttu-id="02870-124">U moet bekend zijn met schrijven en het bouwen van C#-code die gericht is op .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="02870-124">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span> <span data-ttu-id="02870-125">Hallo stappen in dit document Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="02870-125">hello steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="02870-126">Een manier tooupload .exe-bestanden toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="02870-126">A way tooupload .exe files toohello cluster.</span></span> <span data-ttu-id="02870-127">Hallo stappen in dit document gebruiken Hallo Data Lake Tools voor Visual Studio tooupload Hallo bestanden tooprimary opslagruimte voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="02870-127">hello steps in this document use hello Data Lake Tools for Visual Studio tooupload hello files tooprimary storage for hello cluster.</span></span>

* <span data-ttu-id="02870-128">Azure PowerShell of een SSH-client.</span><span class="sxs-lookup"><span data-stu-id="02870-128">Azure PowerShell or a SSH client.</span></span>

* <span data-ttu-id="02870-129">Een Hadoop op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="02870-129">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="02870-130">Zie voor meer informatie over het maken van een cluster [maken van een HDInsight-cluster](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="02870-130">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="create-hello-mapper"></a><span data-ttu-id="02870-131">Hallo mapper maken</span><span class="sxs-lookup"><span data-stu-id="02870-131">Create hello mapper</span></span>

<span data-ttu-id="02870-132">Maak in Visual Studio een nieuw __consoletoepassing__ met de naam __mapper__.</span><span class="sxs-lookup"><span data-stu-id="02870-132">In Visual Studio, create a new __Console application__ named __mapper__.</span></span> <span data-ttu-id="02870-133">Hallo na de code voor de toepassing hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="02870-133">Use hello following code for hello application:</span></span>

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

<span data-ttu-id="02870-134">Na het maken van de toepassing hello samenstellen tooproduce hello `/bin/Debug/mapper.exe` bestand in de projectmap Hallo.</span><span class="sxs-lookup"><span data-stu-id="02870-134">After creating hello application, build it tooproduce hello `/bin/Debug/mapper.exe` file in hello project directory.</span></span>

## <a name="create-hello-reducer"></a><span data-ttu-id="02870-135">Hallo reducer maken</span><span class="sxs-lookup"><span data-stu-id="02870-135">Create hello reducer</span></span>

<span data-ttu-id="02870-136">Maak in Visual Studio een nieuw __consoletoepassing__ met de naam __reducer__.</span><span class="sxs-lookup"><span data-stu-id="02870-136">In Visual Studio, create a new __Console application__ named __reducer__.</span></span> <span data-ttu-id="02870-137">Hallo na de code voor de toepassing hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="02870-137">Use hello following code for hello application:</span></span>

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

<span data-ttu-id="02870-138">Na het maken van de toepassing hello samenstellen tooproduce hello `/bin/Debug/reducer.exe` bestand in de projectmap Hallo.</span><span class="sxs-lookup"><span data-stu-id="02870-138">After creating hello application, build it tooproduce hello `/bin/Debug/reducer.exe` file in hello project directory.</span></span>

## <a name="upload-toostorage"></a><span data-ttu-id="02870-139">Toostorage uploaden</span><span class="sxs-lookup"><span data-stu-id="02870-139">Upload toostorage</span></span>

1. <span data-ttu-id="02870-140">Open in Visual Studio **Server Explorer**.</span><span class="sxs-lookup"><span data-stu-id="02870-140">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="02870-141">Vouw **Azure** uit en vouw vervolgens **HDInsight** uit.</span><span class="sxs-lookup"><span data-stu-id="02870-141">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="02870-142">Als u wordt gevraagd, Voer uw referenties in Azure-abonnement en klik vervolgens op **aanmelden**.</span><span class="sxs-lookup"><span data-stu-id="02870-142">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="02870-143">Hallo HDInsight-cluster dat u deze toepassing toodeploy wilt uitbreiden.</span><span class="sxs-lookup"><span data-stu-id="02870-143">Expand hello HDInsight cluster that you wish toodeploy this application to.</span></span> <span data-ttu-id="02870-144">Een item met de tekst hello __(Default Storage Account)__ wordt vermeld.</span><span class="sxs-lookup"><span data-stu-id="02870-144">An entry with hello text __(Default Storage Account)__ is listed.</span></span>

    ![Server Explorer Hallo storage-account voor Hallo cluster weergeven](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="02870-146">Als dit item kan worden uitgebreid, gebruikt u een __Azure Storage-Account__ als standaard opslag voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="02870-146">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for hello cluster.</span></span> <span data-ttu-id="02870-147">tooview hello bestanden op Hallo standaard opslag voor Hallo-cluster, vouw Hallo vermelding en dubbelklik vervolgens op Hallo __(standaardcontainer)__.</span><span class="sxs-lookup"><span data-stu-id="02870-147">tooview hello files on hello default storage for hello cluster, expand hello entry and then double-click hello __(Default Container)__.</span></span>

    * <span data-ttu-id="02870-148">Als dit item kan niet worden uitgebreid, gebruikt u __Azure Data Lake Store__ als Hallo standaard opslag voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="02870-148">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as hello default storage for hello cluster.</span></span> <span data-ttu-id="02870-149">tooview hello bestanden op Hallo standaard opslag voor Hallo-cluster, dubbelklikt u op Hallo __(Standaardopslagaccount)__ vermelding.</span><span class="sxs-lookup"><span data-stu-id="02870-149">tooview hello files on hello default storage for hello cluster, double-click hello __(Default Storage Account)__ entry.</span></span>

5. <span data-ttu-id="02870-150">tooupload hello .exe-bestanden, een van de volgende methoden hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="02870-150">tooupload hello .exe files, use one of hello following methods:</span></span>

    * <span data-ttu-id="02870-151">Als u een __Azure Storage-Account__op Hallo uploaden pictogram en blader vervolgens toohello **bin\debug** map voor Hallo **mapper** project.</span><span class="sxs-lookup"><span data-stu-id="02870-151">If using an __Azure Storage Account__, click hello upload icon, and then browse toohello **bin\debug** folder for hello **mapper** project.</span></span> <span data-ttu-id="02870-152">Tot slot selecteert Hallo **mapper.exe** -bestand en klik op **Ok**.</span><span class="sxs-lookup"><span data-stu-id="02870-152">Finally, select hello **mapper.exe** file and click **Ok**.</span></span>

        ![pictogram uploaden](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="02870-154">Als u __Azure Data Lake Store__, met de rechtermuisknop op een leeg gebied in Hallo bestand aanbieding en selecteer vervolgens __uploaden__.</span><span class="sxs-lookup"><span data-stu-id="02870-154">If using __Azure Data Lake Store__, right-click an empty area in hello file listing, and then select __Upload__.</span></span> <span data-ttu-id="02870-155">Tot slot selecteert Hallo **mapper.exe** -bestand en klik op **Open**.</span><span class="sxs-lookup"><span data-stu-id="02870-155">Finally, select hello **mapper.exe** file and click **Open**.</span></span>

    <span data-ttu-id="02870-156">Eenmaal Hallo __mapper.exe__ uploaden is voltooid, herhaalt Hallo uploadproces voor Hallo __reducer.exe__ bestand.</span><span class="sxs-lookup"><span data-stu-id="02870-156">Once hello __mapper.exe__ upload has finished, repeat hello upload process for hello __reducer.exe__ file.</span></span>

## <a name="run-a-job-using-an-ssh-session"></a><span data-ttu-id="02870-157">Een taak uitvoeren: met behulp van een SSH-sessie</span><span class="sxs-lookup"><span data-stu-id="02870-157">Run a job: Using an SSH session</span></span>

1. <span data-ttu-id="02870-158">SSH tooconnect toohello HDInsight-cluster gebruiken.</span><span class="sxs-lookup"><span data-stu-id="02870-158">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="02870-159">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="02870-159">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="02870-160">Gebruik een van de volgende opdracht toostart hello MapReduce-taak Hallo:</span><span class="sxs-lookup"><span data-stu-id="02870-160">Use one of hello following command toostart hello MapReduce job:</span></span>

    * <span data-ttu-id="02870-161">Als u __Data Lake Store__ als standaard opslag:</span><span class="sxs-lookup"><span data-stu-id="02870-161">If using __Data Lake Store__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * <span data-ttu-id="02870-162">Als u __Azure Storage__ als standaard opslag:</span><span class="sxs-lookup"><span data-stu-id="02870-162">If using __Azure Storage__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    <span data-ttu-id="02870-163">Hallo volgende lijst beschrijft wat elke parameter doet:</span><span class="sxs-lookup"><span data-stu-id="02870-163">hello following list describes what each parameter does:</span></span>

    * <span data-ttu-id="02870-164">`hadoop-streaming.jar`: Hallo jar-bestand met de Hallo streaming MapReduce-functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="02870-164">`hadoop-streaming.jar`: hello jar file that contains hello streaming MapReduce functionality.</span></span>
    * <span data-ttu-id="02870-165">`-files`: Hiermee voegt u Hallo `mapper.exe` en `reducer.exe` bestanden toothis taak.</span><span class="sxs-lookup"><span data-stu-id="02870-165">`-files`: Adds hello `mapper.exe` and `reducer.exe` files toothis job.</span></span> <span data-ttu-id="02870-166">Hallo `adl:///` of `wasb:///` voordat elk bestand Hallo pad toohello hoofdmap van de standaard opslagruimte voor Hallo-cluster is.</span><span class="sxs-lookup"><span data-stu-id="02870-166">hello `adl:///` or `wasb:///` before each file is hello path toohello root of default storage for hello cluster.</span></span>
    * <span data-ttu-id="02870-167">`-mapper`: Hiermee geeft u op welk bestand implementeert Hallo toewijzen.</span><span class="sxs-lookup"><span data-stu-id="02870-167">`-mapper`: Specifies which file implements hello mapper.</span></span>
    * <span data-ttu-id="02870-168">`-reducer`: Hiermee geeft u op welk bestand Hallo reducer implementeert.</span><span class="sxs-lookup"><span data-stu-id="02870-168">`-reducer`: Specifies which file implements hello reducer.</span></span>
    * <span data-ttu-id="02870-169">`-input`: Hallo invoergegevens.</span><span class="sxs-lookup"><span data-stu-id="02870-169">`-input`: hello input data.</span></span>
    * <span data-ttu-id="02870-170">`-output`: de uitvoermap Hallo.</span><span class="sxs-lookup"><span data-stu-id="02870-170">`-output`: hello output directory.</span></span>

3. <span data-ttu-id="02870-171">Zodra het Hallo MapReduce-taak is voltooid, gebruikt u Hallo tooview Hallo resultaten te volgen:</span><span class="sxs-lookup"><span data-stu-id="02870-171">Once hello MapReduce job completes, use hello following tooview hello results:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="02870-172">Hallo is volgende tekst een voorbeeld van Hallo-gegevens geretourneerd door deze opdracht:</span><span class="sxs-lookup"><span data-stu-id="02870-172">hello following text is an example of hello data returned by this command:</span></span>

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a><span data-ttu-id="02870-173">Een taak uitvoeren: met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="02870-173">Run a job: Using PowerShell</span></span>

<span data-ttu-id="02870-174">Gebruik Hallo volgende PowerShell-script toorun een MapReduce-taak en Hallo resultaten te downloaden.</span><span class="sxs-lookup"><span data-stu-id="02870-174">Use hello following PowerShell script toorun a MapReduce job and download hello results.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]

<span data-ttu-id="02870-175">Dit script wordt u gevraagd om Hallo cluster account aanmeldingsnaam en wachtwoord, samen met de naam van een Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="02870-175">This script prompts you for hello cluster login account name and password, along with hello HDInsight cluster name.</span></span> <span data-ttu-id="02870-176">Zodra het Hallo-taak is voltooid, Hallo uitvoer gedownloade toohello is `output.txt` vanaf bestand in Hallo directory Hallo script wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="02870-176">Once hello job completes, hello output is downloaded toohello `output.txt` file in hello directory hello script is ran from.</span></span> <span data-ttu-id="02870-177">Hallo volgende tekst is een voorbeeld van gegevens in Hallo Hallo `output.txt` bestand:</span><span class="sxs-lookup"><span data-stu-id="02870-177">hello following text is an example of hello data in hello `output.txt` file:</span></span>

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a><span data-ttu-id="02870-178">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="02870-178">Next steps</span></span>

<span data-ttu-id="02870-179">Zie voor meer informatie over het gebruik van MapReduce met HDInsight [MapReduce gebruiken met HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="02870-179">For more information on using MapReduce with HDInsight, see [Use MapReduce with HDInsight](hdinsight-use-mapreduce.md).</span></span>

<span data-ttu-id="02870-180">Zie voor meer informatie over het gebruik van C# met Hive en Pig [een C# door de gebruiker gedefinieerde functie gebruiken met Hive en Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="02870-180">For information on using C# with Hive and Pig, see [Use a C# user defined function with Hive and Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span></span>

<span data-ttu-id="02870-181">Zie voor meer informatie over het gebruik van C# met Storm op HDInsight [C#-topologieën ontwikkelen voor Storm op HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="02870-181">For information on using C# with Storm on HDInsight, see [Develop C# topologies for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>