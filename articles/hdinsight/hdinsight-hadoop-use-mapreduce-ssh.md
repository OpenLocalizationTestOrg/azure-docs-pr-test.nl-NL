---
title: aaaMapReduce en SSH-verbinding met Hadoop in HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe toouse SSH toorun MapReduce taken met Hadoop op HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 844678ba-1e1f-4fda-b9ef-34df4035d547
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 9626577687fc5cc119a39d65a9c45298f57f81c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a><span data-ttu-id="5495e-103">MapReduce gebruiken met Hadoop op HDInsight met SSH</span><span class="sxs-lookup"><span data-stu-id="5495e-103">Use MapReduce with Hadoop on HDInsight with SSH</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="5495e-104">Meer informatie over hoe toosubmit MapReduce taken van een tooHDInsight Secure Shell (SSH)-verbinding.</span><span class="sxs-lookup"><span data-stu-id="5495e-104">Learn how toosubmit MapReduce jobs from a Secure Shell (SSH) connection tooHDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="5495e-105">Als u al bekend bent met het gebruik van Hadoop op basis van Linux-servers, maar u nieuwe tooHDInsight zijn, raadpleegt u [Linux gebaseerde HDInsight tips](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="5495e-105">If you are already familiar with using Linux-based Hadoop servers, but you are new tooHDInsight, see [Linux-based HDInsight tips](hdinsight-hadoop-linux-information.md).</span></span>

## <span data-ttu-id="5495e-106"><a id="prereq"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="5495e-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="5495e-107">Een cluster op basis van Linux HDInsight (Hadoop in HDInsight)</span><span class="sxs-lookup"><span data-stu-id="5495e-107">A Linux-based HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="5495e-108">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="5495e-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5495e-109">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5495e-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="5495e-110">Een SSH-client.</span><span class="sxs-lookup"><span data-stu-id="5495e-110">An SSH client.</span></span> <span data-ttu-id="5495e-111">Zie voor meer informatie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="5495e-111">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

## <span data-ttu-id="5495e-112"><a id="ssh"></a>Verbinding maken met SSH</span><span class="sxs-lookup"><span data-stu-id="5495e-112"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="5495e-113">Toohello-cluster via SSH verbinding.</span><span class="sxs-lookup"><span data-stu-id="5495e-113">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="5495e-114">Bijvoorbeeld, Hallo volgende opdracht maakt verbinding met tooa cluster met de naam **myhdinsight**:</span><span class="sxs-lookup"><span data-stu-id="5495e-114">For example, hello following command connects tooa cluster named **myhdinsight**:</span></span>

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="5495e-115">**Als u een certificaatsleutel voor SSH-verificatie**, moet u mogelijk toospecify Hallo locatie van de persoonlijke sleutel Hallo op uw clientsysteem, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5495e-115">**If you use a certificate key for SSH authentication**, you may need toospecify hello location of hello private key on your client system, for example:</span></span>

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

<span data-ttu-id="5495e-116">**Als u een wachtwoord voor de SSH-verificatie**, moet u tooprovide Hallo wachtwoord wanneer u wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="5495e-116">**If you use a password for SSH authentication**, you need tooprovide hello password when prompted.</span></span>

<span data-ttu-id="5495e-117">Zie voor meer informatie over het gebruik van SSH met HDInsight [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5495e-117">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="5495e-118"><a id="hadoop"></a>Hadoop-opdrachten gebruiken</span><span class="sxs-lookup"><span data-stu-id="5495e-118"><a id="hadoop"></a>Use Hadoop commands</span></span>

1. <span data-ttu-id="5495e-119">Nadat u verbonden toohello HDInsight-cluster bent, gebruikt u Hallo opdracht toostart een MapReduce-taak na:</span><span class="sxs-lookup"><span data-stu-id="5495e-119">After you are connected toohello HDInsight cluster, use hello following command toostart a MapReduce job:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    <span data-ttu-id="5495e-120">Deze opdracht start Hallo `wordcount` klasse, die is opgenomen in Hallo `hadoop-mapreduce-examples.jar` bestand.</span><span class="sxs-lookup"><span data-stu-id="5495e-120">This command starts hello `wordcount` class, which is contained in hello `hadoop-mapreduce-examples.jar` file.</span></span> <span data-ttu-id="5495e-121">Hierbij Hallo `/example/data/gutenberg/davinci.txt` document als invoer en uitvoer is opgeslagen op `/example/data/WordCountOutput`.</span><span class="sxs-lookup"><span data-stu-id="5495e-121">It uses hello `/example/data/gutenberg/davinci.txt` document as input, and output is stored at `/example/data/WordCountOutput`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5495e-122">Zie voor meer informatie over deze gegevens MapReduce-taak en Hallo voorbeeld [gebruik MapReduce in Hadoop op HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="5495e-122">For more information about this MapReduce job and hello example data, see [Use MapReduce in Hadoop on HDInsight](hdinsight-use-mapreduce.md).</span></span>

2. <span data-ttu-id="5495e-123">Hallo taak verzendt gegevens worden verwerkt en wordt informatie vergelijkbare toohello tekst volgen wanneer Hallo-taak is voltooid:</span><span class="sxs-lookup"><span data-stu-id="5495e-123">hello job emits details as it processes, and it returns information similar toohello following text when hello job completes:</span></span>

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. <span data-ttu-id="5495e-124">Wanneer Hallo-taak is voltooid, gebruikt u Hallo opdracht toolist Hallo uitvoerbestanden te volgen:</span><span class="sxs-lookup"><span data-stu-id="5495e-124">When hello job completes, use hello following command toolist hello output files:</span></span>

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    <span data-ttu-id="5495e-125">Deze opdracht weer twee bestanden: `_SUCCESS` en `part-r-00000`.</span><span class="sxs-lookup"><span data-stu-id="5495e-125">This command display two files, `_SUCCESS` and `part-r-00000`.</span></span> <span data-ttu-id="5495e-126">Hallo `part-r-00000` bestand bevat een Hallo uitvoer voor deze taak.</span><span class="sxs-lookup"><span data-stu-id="5495e-126">hello `part-r-00000` file contains hello output for this job.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5495e-127">Bepaalde MapReduce-taken kunnen Hallo resultaten gesplitst over meerdere **onderdeel-r-###** bestanden.</span><span class="sxs-lookup"><span data-stu-id="5495e-127">Some MapReduce jobs may split hello results across multiple **part-r-#####** files.</span></span> <span data-ttu-id="5495e-128">Als dit het geval is, gebruikt u Hallo ### achtervoegsel tooindicate Hallo volgorde van Hallo-bestanden.</span><span class="sxs-lookup"><span data-stu-id="5495e-128">If so, use hello ##### suffix tooindicate hello order of hello files.</span></span>

4. <span data-ttu-id="5495e-129">Hallo tooview uitvoer Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="5495e-129">tooview hello output, use hello following command:</span></span>

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    <span data-ttu-id="5495e-130">Deze opdracht geeft een lijst met Hallo woorden die zijn opgenomen in Hallo **wasb://example/data/gutenberg/davinci.txt** bestands- en Hallo aantal keren dat elk woord is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="5495e-130">This command displays a list of hello words that are contained in hello **wasb://example/data/gutenberg/davinci.txt** file and hello number of times each word occurred.</span></span> <span data-ttu-id="5495e-131">Hallo is volgende tekst een voorbeeld van Hallo-gegevens die zijn opgenomen in Hallo-bestand:</span><span class="sxs-lookup"><span data-stu-id="5495e-131">hello following text is an example of hello data that is contained in hello file:</span></span>

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <span data-ttu-id="5495e-132"><a id="summary"></a>Samenvatting</span><span class="sxs-lookup"><span data-stu-id="5495e-132"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="5495e-133">Zoals u ziet, Hadoop-opdrachten bieden een eenvoudige manier toorun MapReduce-taken in een HDInsight-cluster en weergave Hallo taakuitvoer.</span><span class="sxs-lookup"><span data-stu-id="5495e-133">As you can see, Hadoop commands provide an easy way toorun MapReduce jobs in an HDInsight cluster and then view hello job output.</span></span>

## <span data-ttu-id="5495e-134"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5495e-134"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="5495e-135">Voor algemene informatie over MapReduce-taken in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5495e-135">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="5495e-136">Gebruik MapReduce op HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="5495e-136">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="5495e-137">Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5495e-137">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="5495e-138">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5495e-138">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="5495e-139">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5495e-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
