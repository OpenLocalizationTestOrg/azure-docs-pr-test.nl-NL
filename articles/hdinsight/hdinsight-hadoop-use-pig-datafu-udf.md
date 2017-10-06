---
title: aaaUse DataFu met Pig op HDInsight - Azure | Microsoft Docs
description: DataFu is een verzameling van bibliotheken voor gebruik met Hadoop. Meer informatie over hoe u DataFu kunt gebruiken met Pig op uw HDInsight-cluster.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 0016721a-82be-4773-88ad-91e6b2c21cbb
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 357ad8f9694cc590115289877e752bdd242bdadc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-datafu-with-pig-on-hdinsight"></a><span data-ttu-id="8b69a-104">DataFu met pig in HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="8b69a-104">Use DataFu with pig on HDInsight</span></span>

<span data-ttu-id="8b69a-105">Meer informatie over hoe toouse DataFu met HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8b69a-105">Learn how toouse DataFu with HDInsight.</span></span> <span data-ttu-id="8b69a-106">DataFu is een verzameling van Open-Source bibliotheken voor gebruik met Pig op Hadoop.</span><span class="sxs-lookup"><span data-stu-id="8b69a-106">DataFu is a collection of Open Source libraries for use with Pig on Hadoop.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8b69a-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="8b69a-107">Prerequisites</span></span>

* <span data-ttu-id="8b69a-108">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="8b69a-108">An Azure subscription.</span></span>

* <span data-ttu-id="8b69a-109">Een Azure HDInsight-cluster (Linux of op basis van Windows)</span><span class="sxs-lookup"><span data-stu-id="8b69a-109">An Azure HDInsight cluster (Linux or Windows based)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="8b69a-110">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="8b69a-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="8b69a-111">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8b69a-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="8b69a-112">Een enigszins bekend bent met [Pig gebruiken in HDInsight](hdinsight-use-pig.md)</span><span class="sxs-lookup"><span data-stu-id="8b69a-112">A basic familiarity with [using Pig on HDInsight](hdinsight-use-pig.md)</span></span>

## <a name="install-datafu-on-linux-based-hdinsight"></a><span data-ttu-id="8b69a-113">DataFu installeren op Linux gebaseerde HDInsight</span><span class="sxs-lookup"><span data-stu-id="8b69a-113">Install DataFu on Linux-based HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b69a-114">DataFu is geïnstalleerd op Linux gebaseerde clusters versie 3.3 en hoger, en op Windows gebaseerde clusters.</span><span class="sxs-lookup"><span data-stu-id="8b69a-114">DataFu is installed on Linux-based clusters version 3.3 and higher, and on Windows-based clusters.</span></span> <span data-ttu-id="8b69a-115">Het is niet geïnstalleerd op Linux gebaseerde clusters ouder is dan 3.3.</span><span class="sxs-lookup"><span data-stu-id="8b69a-115">It is not installed on Linux-based clusters earlier than 3.3.</span></span>
>
> <span data-ttu-id="8b69a-116">Als u een cluster met Windows of een cluster op basis van Linux hoger dan versie 3.3 gebruikt, moet u deze sectie overslaan.</span><span class="sxs-lookup"><span data-stu-id="8b69a-116">If you are using a Windows-based cluster, or a Linux-based cluster higher than version 3.3, skip this section.</span></span>

<span data-ttu-id="8b69a-117">DataFu kan worden gedownload en geïnstalleerd vanuit de opslagplaats met Maven Hallo.</span><span class="sxs-lookup"><span data-stu-id="8b69a-117">DataFu can be downloaded and installed from hello Maven repository.</span></span> <span data-ttu-id="8b69a-118">Gebruik Hallo stappen tooadd DataFu tooyour HDInsight-cluster te volgen:</span><span class="sxs-lookup"><span data-stu-id="8b69a-118">Use hello following steps tooadd DataFu tooyour HDInsight cluster:</span></span>

1. <span data-ttu-id="8b69a-119">Tooyour Linux gebaseerde HDInsight-cluster via SSH verbinding.</span><span class="sxs-lookup"><span data-stu-id="8b69a-119">Connect tooyour Linux-based HDInsight cluster using SSH.</span></span> <span data-ttu-id="8b69a-120">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="8b69a-120">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="8b69a-121">Hallo na de opdracht toodownload hello DataFu jar-bestand met het hulpprogramma wget hello gebruiken of kopieer en plak Hallo-koppeling in uw browser toobegin Hallo download.</span><span class="sxs-lookup"><span data-stu-id="8b69a-121">Use hello following command toodownload hello DataFu jar file using hello wget utility, or copy and paste hello link into your browser toobegin hello download.</span></span>

    ```
    wget http://central.maven.org/maven2/com/linkedin/datafu/datafu/1.2.0/datafu-1.2.0.jar
    ```

3. <span data-ttu-id="8b69a-122">Vervolgens uploaden Hallo toodefault opslagruimte voor uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="8b69a-122">Next, upload hello file toodefault storage for your HDInsight cluster.</span></span> <span data-ttu-id="8b69a-123">Hallo-bestand in standaard plaatst kunt opslag beschikbaar tooall knooppunten in het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="8b69a-123">Placing hello file in default storage makes it available tooall nodes in hello cluster.</span></span>

    ```
    hdfs dfs -put datafu-1.2.0.jar /example/jars
    ```

    > [!NOTE]
    > <span data-ttu-id="8b69a-124">vorige opdracht Hallo slaat Hallo jar in `/example/jars` omdat deze map al in de clusteropslag Hallo bestaat.</span><span class="sxs-lookup"><span data-stu-id="8b69a-124">hello previous command stores hello jar in `/example/jars` since this directory already exists on hello cluster storage.</span></span> <span data-ttu-id="8b69a-125">U kunt een locatie die u wilt dat op de opslag van HDInsight-cluster gebruiken.</span><span class="sxs-lookup"><span data-stu-id="8b69a-125">You can use any location you wish on HDInsight cluster storage.</span></span>

## <a name="use-datafu-with-pig"></a><span data-ttu-id="8b69a-126">DataFu met Pig gebruiken</span><span class="sxs-lookup"><span data-stu-id="8b69a-126">Use DataFu With Pig</span></span>

<span data-ttu-id="8b69a-127">Hallo stappen in deze sectie wordt ervan uitgegaan dat u bekend bent met Pig gebruiken in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8b69a-127">hello steps in this section assume that you are familiar with using Pig on HDInsight.</span></span> <span data-ttu-id="8b69a-128">Zie voor meer informatie over het gebruik van Pig met HDInsight [Pig gebruiken met HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="8b69a-128">For more information on using Pig with HDInsight, see [Use Pig with HDInsight](hdinsight-use-pig.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b69a-129">Als u handmatig DataFu met Hallo stappen in de vorige sectie Hallo hebt geïnstalleerd, moet u het registreren voordat u deze gebruikt.</span><span class="sxs-lookup"><span data-stu-id="8b69a-129">If you manually installed DataFu using hello steps in hello previous section, you must register it before using it.</span></span>
>
> * <span data-ttu-id="8b69a-130">Als uw cluster Azure Storage gebruikt, gebruikt u een `wasb://` pad.</span><span class="sxs-lookup"><span data-stu-id="8b69a-130">If your cluster uses Azure Storage, use a `wasb://` path.</span></span> <span data-ttu-id="8b69a-131">Bijvoorbeeld `register wasb:///example/jars/datafu-1.2.0.jar`.</span><span class="sxs-lookup"><span data-stu-id="8b69a-131">For example, `register wasb:///example/jars/datafu-1.2.0.jar`.</span></span>
>
> * <span data-ttu-id="8b69a-132">Als uw cluster gebruikmaakt van Azure Data Lake Store, gebruikt u een `adl://` pad.</span><span class="sxs-lookup"><span data-stu-id="8b69a-132">If your cluster uses Azure Data Lake Store, use an `adl://` path.</span></span> <span data-ttu-id="8b69a-133">Bijvoorbeeld `register adl://home/example/jars/datafu-1.2.0.jar`.</span><span class="sxs-lookup"><span data-stu-id="8b69a-133">For example, `register adl://home/example/jars/datafu-1.2.0.jar`.</span></span>

<span data-ttu-id="8b69a-134">U definiëren vaak een alias voor DataFu functies.</span><span class="sxs-lookup"><span data-stu-id="8b69a-134">You often define an alias for DataFu functions.</span></span> <span data-ttu-id="8b69a-135">Hallo volgende voorbeeld definieert een alias van `SHA`:</span><span class="sxs-lookup"><span data-stu-id="8b69a-135">hello following example defines an alias of `SHA`:</span></span>

```piglatin
DEFINE SHA datafu.pig.hash.SHA();
```

<span data-ttu-id="8b69a-136">Vervolgens kunt u deze alias in een Pig Latin script toogenerate een hash voor Hallo invoergegevens.</span><span class="sxs-lookup"><span data-stu-id="8b69a-136">You can then use this alias in a Pig Latin script toogenerate a hash for hello input data.</span></span> <span data-ttu-id="8b69a-137">Bijvoorbeeld: hello volgende Hallo locatie in de invoergegevens hello wordt vervangen door een hash-waarde:</span><span class="sxs-lookup"><span data-stu-id="8b69a-137">For example, hello following code replaces hello location in hello input data with a hash value:</span></span>

```piglatin
raw = LOAD '/HdiSamples/HdiSamples/SensorSampleData/building/building.csv' USING
    org.apache.pig.piggybank.storage.CSVExcelStorage(',', 'NO_MULTILINE', 'UNIX', 'SKIP_INPUT_HEADER') AS
    (int1:int,
     id1:chararray,
     int2:int,
     id2:chararray,
     location:chararray);
mask = FOREACH raw GENERATE int1, id1, int2, id2, SHA(location);
DUMP mask;
```

<span data-ttu-id="8b69a-138">Er wordt een Hallo volgende uitvoer gegenereerd:</span><span class="sxs-lookup"><span data-stu-id="8b69a-138">It generates hello following output:</span></span>

    (1,M1,25,AC1000,aa5ab35a9174c2062b7f7697b33fafe5ce404cf5fecf6bfbbf0dc96ba0d90046)
    (2,M2,27,FN39TG,7a1ca4ef7515f7276bae7230545829c27810c9d9e98ab2c06066bee6270d5153)
    (3,M3,28,JDNS77,07f62b021771d3cf67e2e1faf18769cc5e5c119ad7d4d1847a11e11d6d5a7ecb)
    (4,M4,17,GG1919,aed8f531aa7e785be255bc435e2582e74c58defedebcb629eeabf365b809bd6f)
    (5,M5,3,ACMAX22,1ed8c7e56c947bebc0cfcf88c4ea0f02c944568f71df893a99970e4f0c78cddc)
    (6,M6,9,AC1000,c96dd81db196cca5f57bd4270bbb9d9e9d1b242d67f9364005ee1dfdc2632523)
    (7,M7,13,FN39TG,3e049d78d958038ac6bd5dcf038075cc73362b4956aaf7308c3a69c8eca76297)
    (8,M8,25,JDNS77,c1ef40ce0484c698eb4bd27fe56c1e7b68d74f9780ed674210d0e5013dae45e9)
    (9,M9,11,GG1919,a7d355b26bda6bf1196ccffead0b2cf2b81f0a9de5b4876b44407f1dc07e51e6)
    (10,M10,23,ACMAX22,10436829032f361a3de50048de41755140e581467bc1895e6c1a17f423e42d10)
    (11,M11,14,AC1000,348841ef53dbd5a64008a86be432973db790774fb28b59b0d99702a3188b3705)
    (12,M12,26,FN39TG,aed8f531aa7e785be255bc435e2582e74c58defedebcb629eeabf365b809bd6f)
    (13,M13,25,JDNS77,ed9ad13611d7164839dd3feaf9a7f6a75a4138f389e0d45f8e07fa38da1116a2)
    (14,M14,17,GG1919,80db4ccdca106d37b920206331fcfe3e9e50a9e763d89b54ce3ad5ac8cf30f03)
    (15,M15,19,ACMAX22,3552ac0c032467fbf592cb4d10c5c9267800c01e343ad8ca557256d882ae9327)
    (16,M16,23,AC1000,07c67d76ef92ac9853588e098983fefba4ba5965f8fec95f42ab0d04c27865ba)
    (17,M17,11,FN39TG,557c1599d9a04895d3817d293e0806a4419a14de31958386182798d0d2ed3a56)
    (18,M18,25,JDNS77,dbc74a36d8e7439c45c64d856388506cc9b1218619cef979c3d605115a7a4546)
    (19,M19,14,GG1919,be55ef3f4c4e6c2d9c2afe2a33ac90ad0f50d4de7f9163999877e2a9ca5a54f8)
    (20,M20,19,ACMAX22,ea0b937ea317101ee2c26b03a4843a19ceced8a2b9673c3cf409a726ca2b0fd8)

## <a name="next-steps"></a><span data-ttu-id="8b69a-139">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="8b69a-139">Next steps</span></span>

<span data-ttu-id="8b69a-140">Zie voor meer informatie over DataFu of Pig Hallo documenten te volgen:</span><span class="sxs-lookup"><span data-stu-id="8b69a-140">For more information on DataFu or Pig, see hello following documents:</span></span>

* <span data-ttu-id="8b69a-141">[Apache Pig DataFu handleiding](http://datafu.incubator.apache.org/docs/datafu/guide.html).</span><span class="sxs-lookup"><span data-stu-id="8b69a-141">[Apache DataFu Pig Guide](http://datafu.incubator.apache.org/docs/datafu/guide.html).</span></span>
* [<span data-ttu-id="8b69a-142">Pig gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="8b69a-142">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
