---
title: aaaUse Hadoop Pig met SSH op een HDInsight-cluster - Azure | Microsoft Docs
description: Meer informatie over hoe tooa Linux gebaseerde Hadoop-cluster verbinding te maken met SSH, en vervolgens gebruik Hallo Pig opdracht toorun Pig Latin instructies interactief of als een batch taken.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b646a93b-4c51-4ba4-84da-3275d9124ebe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 1da303e239b537e6b331b1d33010058582718c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-hello-pig-command-ssh"></a><span data-ttu-id="5f52a-103">Pig-taken uitvoeren op een cluster op basis van Linux met Hallo Pig-opdracht (SSH)</span><span class="sxs-lookup"><span data-stu-id="5f52a-103">Run Pig jobs on a Linux-based cluster with hello Pig command (SSH)</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="5f52a-104">Meer informatie over hoe toointeractively Pig-taken uitvoeren vanaf een SSH-verbinding tooyour HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="5f52a-104">Learn how toointeractively run Pig jobs from an SSH connection tooyour HDInsight cluster.</span></span> <span data-ttu-id="5f52a-105">Hallo Pig Latin programmeertaal kunt u toodescribe transformaties die toegepast toohello invoer gegevens tooproduce Hallo gewenst uitgevoerd worden.</span><span class="sxs-lookup"><span data-stu-id="5f52a-105">hello Pig Latin programming language allows you toodescribe transformations that are applied toohello input data tooproduce hello desired output.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5f52a-106">Hallo moet stappen in dit document een Linux gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="5f52a-106">hello steps in this document require a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="5f52a-107">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="5f52a-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5f52a-108">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="5f52a-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="5f52a-109"><a id="ssh"></a>Verbinding maken met SSH</span><span class="sxs-lookup"><span data-stu-id="5f52a-109"><a id="ssh"></a>Connect with SSH</span></span>

<span data-ttu-id="5f52a-110">SSH tooconnect tooyour HDInsight-cluster gebruiken.</span><span class="sxs-lookup"><span data-stu-id="5f52a-110">Use SSH tooconnect tooyour HDInsight cluster.</span></span> <span data-ttu-id="5f52a-111">Hallo volgende voorbeeld maakt verbinding met de naam tooa-cluster **myhdinsight** als Hallo rekening met de naam **sshuser**:</span><span class="sxs-lookup"><span data-stu-id="5f52a-111">hello following example connects tooa cluster named **myhdinsight** as hello account named **sshuser**:</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

<span data-ttu-id="5f52a-112">**Als u een certificaatsleutel voor SSH-verificatie hebt opgegeven** wanneer u Hallo HDInsight-cluster gemaakt, moet u wellicht toospecify Hallo locatie van de persoonlijke sleutel Hallo op uw clientsysteem.</span><span class="sxs-lookup"><span data-stu-id="5f52a-112">**If you provided a certificate key for SSH authentication** when you created hello HDInsight cluster, you may need toospecify hello location of hello private key on your client system.</span></span>

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

<span data-ttu-id="5f52a-113">**Als u een wachtwoord voor de SSH-verificatie opgegeven** tijdens het maken van HDInsight-cluster Hallo Hallo wachtwoord desgevraagd opgeven.</span><span class="sxs-lookup"><span data-stu-id="5f52a-113">**If you provided a password for SSH authentication** when you created hello HDInsight cluster, provide hello password when prompted.</span></span>

<span data-ttu-id="5f52a-114">Zie voor meer informatie over het gebruik van SSH met HDInsight [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5f52a-114">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="5f52a-115"><a id="pig"></a>Hallo Pig-opdracht gebruiken</span><span class="sxs-lookup"><span data-stu-id="5f52a-115"><a id="pig"></a>Use hello Pig command</span></span>

1. <span data-ttu-id="5f52a-116">Eenmaal zijn verbonden, start u met behulp van de volgende opdracht Hallo Hallo Pig-opdrachtregelinterface (CLI):</span><span class="sxs-lookup"><span data-stu-id="5f52a-116">Once connected, start hello Pig command-line interface (CLI) by using hello following command:</span></span>

        pig

    <span data-ttu-id="5f52a-117">Na korte tijd, ziet u een `grunt>` prompt.</span><span class="sxs-lookup"><span data-stu-id="5f52a-117">After a moment, you should see a `grunt>` prompt.</span></span>

2. <span data-ttu-id="5f52a-118">Voer Hallo-instructie:</span><span class="sxs-lookup"><span data-stu-id="5f52a-118">Enter hello following statement:</span></span>

        LOGS = LOAD '/example/data/sample.log';

    <span data-ttu-id="5f52a-119">Met deze opdracht laadt Hallo inhoud van Hallo sample.log bestand in LOGBOEKEN.</span><span class="sxs-lookup"><span data-stu-id="5f52a-119">This command loads hello contents of hello sample.log file into LOGS.</span></span> <span data-ttu-id="5f52a-120">U kunt inhoud Hallo van Hallo-bestand met behulp van de volgende instructie Hallo bekijken:</span><span class="sxs-lookup"><span data-stu-id="5f52a-120">You can view hello contents of hello file by using hello following statement:</span></span>

        DUMP LOGS;

3. <span data-ttu-id="5f52a-121">Vervolgens Hallo gegevens transformeren door het toepassen van een reguliere expressie tooextract alleen Hallo registratieniveau uit elke record met behulp van de volgende instructie Hallo:</span><span class="sxs-lookup"><span data-stu-id="5f52a-121">Next, transform hello data by applying a regular expression tooextract only hello logging level from each record by using hello following statement:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="5f52a-122">U kunt **DUMP** tooview Hallo gegevens na de transformatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="5f52a-122">You can use **DUMP** tooview hello data after hello transformation.</span></span> <span data-ttu-id="5f52a-123">In dit geval gebruiken `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="5f52a-123">In this case, use `DUMP LEVELS;`.</span></span>

4. <span data-ttu-id="5f52a-124">Doorgaan transformaties toepassen door middel van Hallo-instructies in de volgende tabel Hallo:</span><span class="sxs-lookup"><span data-stu-id="5f52a-124">Continue applying transformations by using hello statements in hello following table:</span></span>

    | <span data-ttu-id="5f52a-125">Pig Latin-instructie</span><span class="sxs-lookup"><span data-stu-id="5f52a-125">Pig Latin statement</span></span> | <span data-ttu-id="5f52a-126">Welke Hallo-instructie doet</span><span class="sxs-lookup"><span data-stu-id="5f52a-126">What hello statement does</span></span> |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | <span data-ttu-id="5f52a-127">Hiermee verwijdert u de rijen met een null-waarde voor het logboekniveau Hallo en slaat Hallo resultaten in `FILTEREDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="5f52a-127">Removes rows that contain a null value for hello log level and stores hello results into `FILTEREDLEVELS`.</span></span> |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | <span data-ttu-id="5f52a-128">Groepen Hallo rijen door logboekniveau en slaat Hallo resultaten in `GROUPEDLEVELS`.</span><span class="sxs-lookup"><span data-stu-id="5f52a-128">Groups hello rows by log level and stores hello results into `GROUPEDLEVELS`.</span></span> |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | <span data-ttu-id="5f52a-129">Hiermee maakt u een van de gegevens die elke unieke logboek bevat waarde en hoe vaak het optreedt.</span><span class="sxs-lookup"><span data-stu-id="5f52a-129">Creates a set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="5f52a-130">Hallo-gegevensset wordt opgeslagen in `FREQUENCIES`.</span><span class="sxs-lookup"><span data-stu-id="5f52a-130">hello data set is stored into `FREQUENCIES`.</span></span> |
    | `RESULT = order FREQUENCIES by COUNT desc;` | <span data-ttu-id="5f52a-131">Hallo-logboekniveaus orders op het aantal (aflopend) en opgeslagen in `RESULT`.</span><span class="sxs-lookup"><span data-stu-id="5f52a-131">Orders hello log levels by count (descending) and stores into `RESULT`.</span></span> |

    > [!TIP]
    > <span data-ttu-id="5f52a-132">Gebruik `DUMP` tooview Hallo resultaat van Hallo transformatie na elke stap.</span><span class="sxs-lookup"><span data-stu-id="5f52a-132">Use `DUMP` tooview hello result of hello transformation after each step.</span></span>

5. <span data-ttu-id="5f52a-133">U kunt ook de resultaten van een transformatie Hallo opslaan met behulp van Hallo `STORE` instructie.</span><span class="sxs-lookup"><span data-stu-id="5f52a-133">You can also save hello results of a transformation by using hello `STORE` statement.</span></span> <span data-ttu-id="5f52a-134">Bijvoorbeeld Hallo-instructie Hallo bespaart `RESULT` toohello `/example/data/pigout` directory op Hallo standaard opslagruimte voor uw cluster:</span><span class="sxs-lookup"><span data-stu-id="5f52a-134">For example, hello following statement saves hello `RESULT` toohello `/example/data/pigout` directory on hello default storage for your cluster:</span></span>

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > <span data-ttu-id="5f52a-135">Hallo-gegevens worden opgeslagen in de opgegeven map Hallo in bestanden met de naam `part-nnnnn`.</span><span class="sxs-lookup"><span data-stu-id="5f52a-135">hello data is stored in hello specified directory in files named `part-nnnnn`.</span></span> <span data-ttu-id="5f52a-136">Als het Hallo-map al bestaat, ontvangt u een fout opgetreden.</span><span class="sxs-lookup"><span data-stu-id="5f52a-136">If hello directory already exists, you receive an error.</span></span>

6. <span data-ttu-id="5f52a-137">tooexit hello knorvis vragen, Voer Hallo-instructie:</span><span class="sxs-lookup"><span data-stu-id="5f52a-137">tooexit hello grunt prompt, enter hello following statement:</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="5f52a-138">Pig Latin batch-bestanden</span><span class="sxs-lookup"><span data-stu-id="5f52a-138">Pig Latin batch files</span></span>

<span data-ttu-id="5f52a-139">U kunt ook Hallo Pig opdracht toorun Pig Latin opgenomen in een bestand.</span><span class="sxs-lookup"><span data-stu-id="5f52a-139">You can also use hello Pig command toorun Pig Latin contained in a file.</span></span>

1. <span data-ttu-id="5f52a-140">Na het afsluiten van Hallo knorvis prompt gebruik Hallo volgende toopipe STDIN naar een bestand met de naam opdracht `pigbatch.pig`.</span><span class="sxs-lookup"><span data-stu-id="5f52a-140">After exiting hello grunt prompt, use hello following command toopipe STDIN into a file named `pigbatch.pig`.</span></span> <span data-ttu-id="5f52a-141">Dit bestand is gemaakt in de basismap Hallo voor Hallo SSH gebruikersaccount.</span><span class="sxs-lookup"><span data-stu-id="5f52a-141">This file is created in hello home directory for hello SSH user account.</span></span>

        cat > ~/pigbatch.pig

2. <span data-ttu-id="5f52a-142">Typ of plak de volgende regels Hallo en gebruik vervolgens Ctrl + D na voltooiing.</span><span class="sxs-lookup"><span data-stu-id="5f52a-142">Type or paste hello following lines, and then use Ctrl+D when finished.</span></span>

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. <span data-ttu-id="5f52a-143">Gebruik Hallo volgende opdracht toorun hello `pigbatch.pig` bestand met behulp van Hallo Pig-opdracht.</span><span class="sxs-lookup"><span data-stu-id="5f52a-143">Use hello following command toorun hello `pigbatch.pig` file by using hello Pig command.</span></span>

        pig ~/pigbatch.pig

    <span data-ttu-id="5f52a-144">Nadat het Hallo batch-job is voltooid, ziet u Hallo volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="5f52a-144">Once hello batch job finishes, you see hello following output:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <span data-ttu-id="5f52a-145"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5f52a-145"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="5f52a-146">Raadpleeg voor algemene informatie over Pig in HDInsight Hallo document te volgen:</span><span class="sxs-lookup"><span data-stu-id="5f52a-146">For general information on Pig in HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="5f52a-147">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f52a-147">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="5f52a-148">Zie voor meer informatie over andere manieren toowork met Hadoop op HDInsight Hallo documenten te volgen:</span><span class="sxs-lookup"><span data-stu-id="5f52a-148">For more information on other ways toowork with Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="5f52a-149">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f52a-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="5f52a-150">MapReduce gebruiken met Hadoop op HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f52a-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
