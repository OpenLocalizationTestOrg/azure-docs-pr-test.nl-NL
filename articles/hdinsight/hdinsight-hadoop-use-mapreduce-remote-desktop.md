---
title: aaaMapReduce en extern bureaublad met Hadoop in HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe toouse extern bureaublad tooconnect tooHadoop op HDInsight en MapReduce-taken uitvoeren.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9d3a7b34-7def-4c2e-bb6c-52682d30dee8
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: bdbbcf59ca86dd1b170471aa9e12334a04c23667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="6c880-103">MapReduce in Hadoop in HDInsight met extern bureaublad gebruiken</span><span class="sxs-lookup"><span data-stu-id="6c880-103">Use MapReduce in Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="6c880-104">In dit artikel leert u leert hoe tooconnect tooa Hadoop op HDInsight-cluster met behulp van extern bureaublad en vervolgens MapReduce-taken uitvoeren met behulp van Hallo Hadoop-opdracht.</span><span class="sxs-lookup"><span data-stu-id="6c880-104">In this article, you will learn how tooconnect tooa Hadoop on HDInsight cluster by using Remote Desktop and then run MapReduce jobs by using hello Hadoop command.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6c880-105">Extern bureaublad is alleen beschikbaar op Windows gebaseerde HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="6c880-105">Remote Desktop is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="6c880-106">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="6c880-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="6c880-107">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6c880-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="6c880-108">Voor HDInsight 3.4 of hoger, Zie [MapReduce gebruikt met SSH](hdinsight-hadoop-use-mapreduce-ssh.md) voor informatie over het verbinden van toohello HDInsight-cluster en het MapReduce-taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6c880-108">For HDInsight 3.4 or greater, see [Use MapReduce with SSH](hdinsight-hadoop-use-mapreduce-ssh.md) for information on connecting toohello HDInsight cluster and running MapReduce jobs.</span></span>

## <span data-ttu-id="6c880-109"><a id="prereq"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="6c880-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="6c880-110">toocomplete hello stappen in dit artikel, moet u de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="6c880-110">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="6c880-111">Een cluster op basis van Windows HDInsight (Hadoop in HDInsight)</span><span class="sxs-lookup"><span data-stu-id="6c880-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="6c880-112">Een clientcomputer met Windows 10, Windows 8 of Windows 7</span><span class="sxs-lookup"><span data-stu-id="6c880-112">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="6c880-113"><a id="connect"></a>Verbinding maken met extern bureaublad</span><span class="sxs-lookup"><span data-stu-id="6c880-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="6c880-114">Extern bureaublad inschakelen voor Hallo HDInsight-cluster en verbind tooit met behulp Hallo-instructies in de [tooHDInsight clusters met RDP verbinding](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="6c880-114">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="6c880-115"><a id="hadoop"></a>Hallo Hadoop-opdracht gebruiken</span><span class="sxs-lookup"><span data-stu-id="6c880-115"><a id="hadoop"></a>Use hello Hadoop command</span></span>
<span data-ttu-id="6c880-116">Wanneer u verbonden toohello bureaublad voor Hallo HDInsight-cluster bent, gebruik Hallo volgende stappen toorun een MapReduce-taak met behulp van Hallo Hadoop-opdracht:</span><span class="sxs-lookup"><span data-stu-id="6c880-116">When you are connected toohello desktop for hello HDInsight cluster, use hello following steps toorun a MapReduce job by using hello Hadoop command:</span></span>

1. <span data-ttu-id="6c880-117">Hallo HDInsight bureaublad starten Hallo **Hadoop-opdrachtregel**.</span><span class="sxs-lookup"><span data-stu-id="6c880-117">From hello HDInsight desktop, start hello **Hadoop Command Line**.</span></span> <span data-ttu-id="6c880-118">Hiermee opent u een nieuwe prompt in Hallo **c:\apps\dist\hadoop-&lt;versienummer >** directory.</span><span class="sxs-lookup"><span data-stu-id="6c880-118">This opens a new command prompt in hello **c:\apps\dist\hadoop-&lt;version number>** directory.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6c880-119">Hallo-versienummer verandert als Hadoop wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="6c880-119">hello version number changes as Hadoop is updated.</span></span> <span data-ttu-id="6c880-120">Hallo **HADOOP_HOME** omgevingsvariabele kan worden gebruikt toofind Hallo pad.</span><span class="sxs-lookup"><span data-stu-id="6c880-120">hello **HADOOP_HOME** environment variable can be used toofind hello path.</span></span> <span data-ttu-id="6c880-121">Bijvoorbeeld: `cd %HADOOP_HOME%` wijzigingen mappen toohello Hadoop directory, zonder dat u tooknow Hallo versienummer.</span><span class="sxs-lookup"><span data-stu-id="6c880-121">For example, `cd %HADOOP_HOME%` changes directories toohello Hadoop directory, without requiring you tooknow hello version number.</span></span>
   >
   >
2. <span data-ttu-id="6c880-122">Hallo toouse **Hadoop** toorun MapReduce-taak van een voorbeeld van de opdracht, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="6c880-122">toouse hello **Hadoop** command toorun an example MapReduce job, use hello following command:</span></span>

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    <span data-ttu-id="6c880-123">Hiermee start u Hallo **wordcount** klasse, die is opgenomen in Hallo **hadoop-mapreduce-examples.jar** bestanden in de huidige map Hallo.</span><span class="sxs-lookup"><span data-stu-id="6c880-123">This starts hello **wordcount** class, which is contained in hello **hadoop-mapreduce-examples.jar** file in hello current directory.</span></span> <span data-ttu-id="6c880-124">Als invoer, hierbij Hallo **wasb://example/data/gutenberg/davinci.txt** document en uitvoer is opgeslagen in: **wasb: / / / voorbeeld/data/WordCountOutput**.</span><span class="sxs-lookup"><span data-stu-id="6c880-124">As input, it uses hello **wasb://example/data/gutenberg/davinci.txt** document, and output is stored at: **wasb:///example/data/WordCountOutput**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6c880-125">Zie voor meer informatie over deze gegevens MapReduce-taak en Hallo voorbeeld <a href="hdinsight-use-mapreduce.md">gebruik MapReduce in HDInsight Hadoop</a>.</span><span class="sxs-lookup"><span data-stu-id="6c880-125">for more information about this MapReduce job and hello example data, see <a href="hdinsight-use-mapreduce.md">Use MapReduce in HDInsight Hadoop</a>.</span></span>
   >
   >
3. <span data-ttu-id="6c880-126">Hallo taak verzendt details, zoals deze wordt verwerkt en informatie vergelijkbare toohello volgende retourneert bij het Hallo-taak is voltooid:</span><span class="sxs-lookup"><span data-stu-id="6c880-126">hello job emits details as it is processed, and it returns information similar toohello following when hello job is complete:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. <span data-ttu-id="6c880-127">Wanneer het Hallo-taak is voltooid, gebruiken Hallo volgende opdracht toolist Hallo uitvoerbestanden opgeslagen in **wasb://example/data/WordCountOutput**:</span><span class="sxs-lookup"><span data-stu-id="6c880-127">When hello job is complete, use hello following command toolist hello output files stored at **wasb://example/data/WordCountOutput**:</span></span>

        hadoop fs -ls wasb:///example/data/WordCountOutput

    <span data-ttu-id="6c880-128">Dit moet worden weergegeven in twee bestanden: **_SUCCESS** en **onderdeel-r-00000**.</span><span class="sxs-lookup"><span data-stu-id="6c880-128">This should display two files, **_SUCCESS** and **part-r-00000**.</span></span> <span data-ttu-id="6c880-129">Hallo **onderdeel-r-00000** bestand bevat een Hallo uitvoer voor deze taak.</span><span class="sxs-lookup"><span data-stu-id="6c880-129">hello **part-r-00000** file contains hello output for this job.</span></span>

   > [!NOTE]
   > <span data-ttu-id="6c880-130">Bepaalde MapReduce-taken kunnen Hallo resultaten gesplitst over meerdere **onderdeel-r-###** bestanden.</span><span class="sxs-lookup"><span data-stu-id="6c880-130">Some MapReduce jobs may split hello results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="6c880-131">Als dit het geval is, gebruikt u Hallo ### achtervoegsel tooindicate Hallo volgorde van Hallo-bestanden.</span><span class="sxs-lookup"><span data-stu-id="6c880-131">If so, use hello ##### suffix tooindicate hello order of hello files.</span></span>
   >
   >
5. <span data-ttu-id="6c880-132">Hallo tooview uitvoer Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="6c880-132">tooview hello output, use hello following command:</span></span>

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    <span data-ttu-id="6c880-133">Hiermee wordt een lijst met Hallo woorden die zijn opgenomen in Hallo **wasb://example/data/gutenberg/davinci.txt** bestand samen met de Hallo aantal malen dat elk woord heeft plaatsgevonden.</span><span class="sxs-lookup"><span data-stu-id="6c880-133">This displays a list of hello words that are contained in hello **wasb://example/data/gutenberg/davinci.txt** file, along with hello number of times each word occured.</span></span> <span data-ttu-id="6c880-134">Hallo Hieronder volgt een voorbeeld van Hallo-gegevens die worden opgenomen in het Hallo-bestand:</span><span class="sxs-lookup"><span data-stu-id="6c880-134">hello following is an example of hello data that will be contained in hello file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="6c880-135"><a id="summary"></a>Samenvatting</span><span class="sxs-lookup"><span data-stu-id="6c880-135"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="6c880-136">Zoals u ziet, biedt Hallo Hadoop opdracht een eenvoudige manier toorun MapReduce-taken op een HDInsight-cluster en klik vervolgens op weergave Hallo taakuitvoer.</span><span class="sxs-lookup"><span data-stu-id="6c880-136">As you can see, hello Hadoop command provides an easy way toorun MapReduce jobs on an HDInsight cluster and then view hello job output.</span></span>

## <span data-ttu-id="6c880-137"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6c880-137"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="6c880-138">Voor algemene informatie over MapReduce-taken in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="6c880-138">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="6c880-139">Gebruik MapReduce op HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="6c880-139">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="6c880-140">Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="6c880-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="6c880-141">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="6c880-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="6c880-142">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="6c880-142">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
