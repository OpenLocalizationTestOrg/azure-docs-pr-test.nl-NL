---
title: MapReduce en extern bureaublad met Hadoop in HDInsight - Azure | Microsoft Docs
description: Informatie over het gebruik van extern bureaublad verbinding maken met Hadoop op HDInsight en MapReduce-taken uitvoeren.
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
ms.openlocfilehash: b56674857b013f9bb3d4dd4b6e97b34e0a97b1b2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="476c3-103">MapReduce in Hadoop in HDInsight met extern bureaublad gebruiken</span><span class="sxs-lookup"><span data-stu-id="476c3-103">Use MapReduce in Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="476c3-104">In dit artikel leert u hoe u verbinding met een Hadoop op HDInsight-cluster met behulp van extern bureaublad en voer vervolgens MapReduce-taken via de Hadoop-opdracht.</span><span class="sxs-lookup"><span data-stu-id="476c3-104">In this article, you will learn how to connect to a Hadoop on HDInsight cluster by using Remote Desktop and then run MapReduce jobs by using the Hadoop command.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="476c3-105">Extern bureaublad is alleen beschikbaar op Windows gebaseerde HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="476c3-105">Remote Desktop is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="476c3-106">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="476c3-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="476c3-107">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="476c3-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="476c3-108">Voor HDInsight 3.4 of hoger, Zie [MapReduce gebruikt met SSH](hdinsight-hadoop-use-mapreduce-ssh.md) voor meer informatie over verbinding maken met het HDInsight-cluster en MapReduce-taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="476c3-108">For HDInsight 3.4 or greater, see [Use MapReduce with SSH](hdinsight-hadoop-use-mapreduce-ssh.md) for information on connecting to the HDInsight cluster and running MapReduce jobs.</span></span>

## <span data-ttu-id="476c3-109"><a id="prereq"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="476c3-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="476c3-110">Voor het voltooien van de stappen in dit artikel, moet u het volgende:</span><span class="sxs-lookup"><span data-stu-id="476c3-110">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="476c3-111">Een cluster op basis van Windows HDInsight (Hadoop in HDInsight)</span><span class="sxs-lookup"><span data-stu-id="476c3-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="476c3-112">Een clientcomputer met Windows 10, Windows 8 of Windows 7</span><span class="sxs-lookup"><span data-stu-id="476c3-112">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="476c3-113"><a id="connect"></a>Verbinding maken met extern bureaublad</span><span class="sxs-lookup"><span data-stu-id="476c3-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="476c3-114">Extern bureaublad inschakelen voor het HDInsight-cluster en vervolgens verbinding maken met het door de instructies op [verbinding maken met HDInsight-clusters met RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="476c3-114">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="476c3-115"><a id="hadoop"></a>Gebruik de opdracht Hadoop</span><span class="sxs-lookup"><span data-stu-id="476c3-115"><a id="hadoop"></a>Use the Hadoop command</span></span>
<span data-ttu-id="476c3-116">Wanneer u met het bureaublad van het HDInsight-cluster verbonden bent, gebruikt u de volgende stappen uit een MapReduce-taak uitvoeren met behulp van de Hadoop-opdracht:</span><span class="sxs-lookup"><span data-stu-id="476c3-116">When you are connected to the desktop for the HDInsight cluster, use the following steps to run a MapReduce job by using the Hadoop command:</span></span>

1. <span data-ttu-id="476c3-117">Start vanaf het bureaublad HDInsight de **Hadoop-opdrachtregel**.</span><span class="sxs-lookup"><span data-stu-id="476c3-117">From the HDInsight desktop, start the **Hadoop Command Line**.</span></span> <span data-ttu-id="476c3-118">Hiermee opent u een nieuwe opdrachtprompt in de **c:\apps\dist\hadoop-&lt;versienummer >** directory.</span><span class="sxs-lookup"><span data-stu-id="476c3-118">This opens a new command prompt in the **c:\apps\dist\hadoop-&lt;version number>** directory.</span></span>

   > [!NOTE]
   > <span data-ttu-id="476c3-119">Het versienummer verandert als Hadoop wordt bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="476c3-119">The version number changes as Hadoop is updated.</span></span> <span data-ttu-id="476c3-120">De **HADOOP_HOME** omgevingsvariabele kan worden gebruikt om het pad niet vinden.</span><span class="sxs-lookup"><span data-stu-id="476c3-120">The **HADOOP_HOME** environment variable can be used to find the path.</span></span> <span data-ttu-id="476c3-121">Bijvoorbeeld: `cd %HADOOP_HOME%` mappen naar de map Hadoop, zonder u te weten het versienummer wordt gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="476c3-121">For example, `cd %HADOOP_HOME%` changes directories to the Hadoop directory, without requiring you to know the version number.</span></span>
   >
   >
2. <span data-ttu-id="476c3-122">Gebruik de **Hadoop** opdracht voor het uitvoeren van een voorbeeld van de MapReduce-taak, gebruik de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="476c3-122">To use the **Hadoop** command to run an example MapReduce job, use the following command:</span></span>

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    <span data-ttu-id="476c3-123">Hiermee start u de **wordcount** klasse, die is opgenomen in de **hadoop-mapreduce-examples.jar** bestand in de huidige map.</span><span class="sxs-lookup"><span data-stu-id="476c3-123">This starts the **wordcount** class, which is contained in the **hadoop-mapreduce-examples.jar** file in the current directory.</span></span> <span data-ttu-id="476c3-124">Als invoer, gebruikt de **wasb://example/data/gutenberg/davinci.txt** document en uitvoer is opgeslagen in: **wasb: / / / voorbeeld/data/WordCountOutput**.</span><span class="sxs-lookup"><span data-stu-id="476c3-124">As input, it uses the **wasb://example/data/gutenberg/davinci.txt** document, and output is stored at: **wasb:///example/data/WordCountOutput**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="476c3-125">Zie voor meer informatie over deze MapReduce-taak en de bijvoorbeeld gegevens <a href="hdinsight-use-mapreduce.md">gebruik MapReduce in HDInsight Hadoop</a>.</span><span class="sxs-lookup"><span data-stu-id="476c3-125">for more information about this MapReduce job and the example data, see <a href="hdinsight-use-mapreduce.md">Use MapReduce in HDInsight Hadoop</a>.</span></span>
   >
   >
3. <span data-ttu-id="476c3-126">De taak verzendt details, zoals deze wordt verwerkt en gegevens worden geretourneerd met de volgende strekking wanneer de taak voltooid is:</span><span class="sxs-lookup"><span data-stu-id="476c3-126">The job emits details as it is processed, and it returns information similar to the following when the job is complete:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. <span data-ttu-id="476c3-127">Wanneer de taak voltooid is, gebruik de volgende opdracht voor het weergeven van de uitvoerbestanden die is opgeslagen op **wasb://example/data/WordCountOutput**:</span><span class="sxs-lookup"><span data-stu-id="476c3-127">When the job is complete, use the following command to list the output files stored at **wasb://example/data/WordCountOutput**:</span></span>

        hadoop fs -ls wasb:///example/data/WordCountOutput

    <span data-ttu-id="476c3-128">Dit moet worden weergegeven in twee bestanden: **_SUCCESS** en **onderdeel-r-00000**.</span><span class="sxs-lookup"><span data-stu-id="476c3-128">This should display two files, **_SUCCESS** and **part-r-00000**.</span></span> <span data-ttu-id="476c3-129">De **onderdeel-r-00000** bestand bevat de uitvoer voor deze taak.</span><span class="sxs-lookup"><span data-stu-id="476c3-129">The **part-r-00000** file contains the output for this job.</span></span>

   > [!NOTE]
   > <span data-ttu-id="476c3-130">Bepaalde MapReduce-taken kunnen de resultaten worden gesplitst over meerdere **onderdeel-r-###** bestanden.</span><span class="sxs-lookup"><span data-stu-id="476c3-130">Some MapReduce jobs may split the results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="476c3-131">Als dit het geval is, gebruiken de ### achtervoegsel om aan te geven van de volgorde van de bestanden.</span><span class="sxs-lookup"><span data-stu-id="476c3-131">If so, use the ##### suffix to indicate the order of the files.</span></span>
   >
   >
5. <span data-ttu-id="476c3-132">Gebruik de volgende opdracht om de weergave van de uitvoer:</span><span class="sxs-lookup"><span data-stu-id="476c3-132">To view the output, use the following command:</span></span>

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    <span data-ttu-id="476c3-133">Dit geeft een lijst met de woorden die zijn opgenomen in de **wasb://example/data/gutenberg/davinci.txt** bestand samen met het aantal keren dat elk woord is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="476c3-133">This displays a list of the words that are contained in the **wasb://example/data/gutenberg/davinci.txt** file, along with the number of times each word occured.</span></span> <span data-ttu-id="476c3-134">Hier volgt een voorbeeld van de gegevens die worden opgenomen in het bestand:</span><span class="sxs-lookup"><span data-stu-id="476c3-134">The following is an example of the data that will be contained in the file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="476c3-135"><a id="summary"></a>Samenvatting</span><span class="sxs-lookup"><span data-stu-id="476c3-135"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="476c3-136">Zoals u ziet Hiermee de opdracht Hadoop kunt u eenvoudig MapReduce-taken uitvoeren op een HDInsight-cluster en bekijk vervolgens de taakuitvoer van de.</span><span class="sxs-lookup"><span data-stu-id="476c3-136">As you can see, the Hadoop command provides an easy way to run MapReduce jobs on an HDInsight cluster and then view the job output.</span></span>

## <span data-ttu-id="476c3-137"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="476c3-137"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="476c3-138">Voor algemene informatie over MapReduce-taken in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="476c3-138">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="476c3-139">Gebruik MapReduce op HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="476c3-139">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="476c3-140">Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="476c3-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="476c3-141">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="476c3-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="476c3-142">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="476c3-142">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
