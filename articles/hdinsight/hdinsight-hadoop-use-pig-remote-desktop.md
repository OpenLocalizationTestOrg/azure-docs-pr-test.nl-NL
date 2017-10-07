---
title: aaaUse Hadoop Pig met extern bureaublad in HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe toouse Hallo Pig opdracht toorun Pig Latin-instructies uit een extern bureaublad verbinding tooa Hadoop op basis van Windows-cluster in HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e034a286-de0f-465f-8bf1-3d085ca6abed
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 2a4565fa827cd45fdbe6194b0486df93a6561084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a><span data-ttu-id="90b3f-103">Pig-taken uitvoeren vanaf een extern bureaublad-verbinding</span><span class="sxs-lookup"><span data-stu-id="90b3f-103">Run Pig jobs from a Remote Desktop connection</span></span>
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="90b3f-104">Dit document bevat een overzicht voor het gebruik van Hallo Pig opdracht toorun Pig Latin-instructies uit een extern bureaublad verbinding tooa HDInsight op basis van Windows-cluster.</span><span class="sxs-lookup"><span data-stu-id="90b3f-104">This document provides a walkthrough for using hello Pig command toorun Pig Latin statements from a Remote Desktop connection tooa Windows-based HDInsight cluster.</span></span> <span data-ttu-id="90b3f-105">Pig Latin kunt u toocreate MapReduce-toepassingen door te beschrijven gegevenstransformaties, in plaats van toewijzen en functies te beperken.</span><span class="sxs-lookup"><span data-stu-id="90b3f-105">Pig Latin allows you toocreate MapReduce applications by describing data transformations, rather than map and reduce functions.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="90b3f-106">Extern bureaublad is alleen beschikbaar op HDInsight-clusters die Windows hello besturingssysteem gebruiken.</span><span class="sxs-lookup"><span data-stu-id="90b3f-106">Remote Desktop is only available on HDInsight clusters that use Windows as hello operating system.</span></span> <span data-ttu-id="90b3f-107">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="90b3f-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="90b3f-108">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="90b3f-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="90b3f-109">Voor HDInsight 3.4 of hoger, Zie [Pig gebruiken met HDInsight en SSH](hdinsight-hadoop-use-pig-ssh.md) voor informatie over het interactief uitvoeren Pig-taken rechtstreeks op Hallo cluster van een opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="90b3f-109">For HDInsight 3.4 or greater, see [Use Pig with HDInsight and SSH](hdinsight-hadoop-use-pig-ssh.md) for information on interactively running Pig jobs directly on hello cluster from a command-line.</span></span>

## <span data-ttu-id="90b3f-110"><a id="prereq"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="90b3f-110"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="90b3f-111">toocomplete hello stappen in dit artikel, moet u de volgende Hallo.</span><span class="sxs-lookup"><span data-stu-id="90b3f-111">toocomplete hello steps in this article, you will need hello following.</span></span>

* <span data-ttu-id="90b3f-112">Een cluster op basis van Windows HDInsight (Hadoop in HDInsight)</span><span class="sxs-lookup"><span data-stu-id="90b3f-112">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="90b3f-113">Een clientcomputer met Windows 10, Windows 8 of Windows 7</span><span class="sxs-lookup"><span data-stu-id="90b3f-113">A client computer running Windows 10, Windows 8, or Windows 7</span></span>

## <span data-ttu-id="90b3f-114"><a id="connect"></a>Verbinding maken met extern bureaublad</span><span class="sxs-lookup"><span data-stu-id="90b3f-114"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="90b3f-115">Extern bureaublad inschakelen voor Hallo HDInsight-cluster en verbind tooit met behulp Hallo-instructies in de [tooHDInsight clusters met RDP verbinding](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="90b3f-115">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="90b3f-116"><a id="pig"></a>Hallo Pig-opdracht gebruiken</span><span class="sxs-lookup"><span data-stu-id="90b3f-116"><a id="pig"></a>Use hello Pig command</span></span>
1. <span data-ttu-id="90b3f-117">Nadat u een verbinding met extern bureaublad hebt, start u Hallo **Hadoop-opdrachtregel** met behulp van Hallo-pictogram op Hallo bureaublad.</span><span class="sxs-lookup"><span data-stu-id="90b3f-117">After you have a Remote Desktop connection, start hello **Hadoop Command Line** by using hello icon on hello desktop.</span></span>
2. <span data-ttu-id="90b3f-118">Hallo na toostart Hallo Pig-opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="90b3f-118">Use hello following toostart hello Pig command:</span></span>

        %pig_home%\bin\pig

    <span data-ttu-id="90b3f-119">U krijgt een `grunt>` prompt.</span><span class="sxs-lookup"><span data-stu-id="90b3f-119">You will be presented with a `grunt>` prompt.</span></span>
3. <span data-ttu-id="90b3f-120">Voer Hallo-instructie:</span><span class="sxs-lookup"><span data-stu-id="90b3f-120">Enter hello following statement:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';

    <span data-ttu-id="90b3f-121">Met deze opdracht laadt Hallo inhoud van Hallo sample.log bestand in het Hallo LOGBOEKEN-bestand.</span><span class="sxs-lookup"><span data-stu-id="90b3f-121">This command loads hello contents of hello sample.log file into hello LOGS file.</span></span> <span data-ttu-id="90b3f-122">U kunt inhoud Hallo van Hallo-bestand met behulp van de volgende opdracht Hallo bekijken:</span><span class="sxs-lookup"><span data-stu-id="90b3f-122">You can view hello contents of hello file by using hello following command:</span></span>

        DUMP LOGS;
4. <span data-ttu-id="90b3f-123">Hallo-gegevens door het toepassen van een reguliere expressie tooextract alleen Hallo registratieniveau uit elke record transformeren:</span><span class="sxs-lookup"><span data-stu-id="90b3f-123">Transform hello data by applying a regular expression tooextract only hello logging level from each record:</span></span>

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    <span data-ttu-id="90b3f-124">U kunt **DUMP** tooview Hallo gegevens na de transformatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="90b3f-124">You can use **DUMP** tooview hello data after hello transformation.</span></span> <span data-ttu-id="90b3f-125">In dit geval `DUMP LEVELS;`.</span><span class="sxs-lookup"><span data-stu-id="90b3f-125">In this case, `DUMP LEVELS;`.</span></span>
5. <span data-ttu-id="90b3f-126">Blijven transformaties toepassen met behulp van Hallo instructies te volgen.</span><span class="sxs-lookup"><span data-stu-id="90b3f-126">Continue applying transformations by using hello following statements.</span></span> <span data-ttu-id="90b3f-127">Gebruik `DUMP` tooview Hallo resultaat van Hallo transformatie na elke stap.</span><span class="sxs-lookup"><span data-stu-id="90b3f-127">Use `DUMP` tooview hello result of hello transformation after each step.</span></span>

    <table>
    <tr>
    <th><span data-ttu-id="90b3f-128">Instructie</span><span class="sxs-lookup"><span data-stu-id="90b3f-128">Statement</span></span></th><th><span data-ttu-id="90b3f-129">Wat het doet</span><span class="sxs-lookup"><span data-stu-id="90b3f-129">What it does</span></span></th>
    </tr>
    <tr>
    <td><span data-ttu-id="90b3f-130">FILTEREDLEVELS = FILTER TOEPASSINGSNIVEAU LOGLEVEL niet null is.</span><span class="sxs-lookup"><span data-stu-id="90b3f-130">FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</span></span></td><td><span data-ttu-id="90b3f-131">Hiermee verwijdert u de rijen met een null-waarde voor het logboekniveau Hallo en slaat Hallo resultaten in FILTEREDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="90b3f-131">Removes rows that contain a null value for hello log level and stores hello results into FILTEREDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="90b3f-132">GROUPEDLEVELS = groep FILTEREDLEVELS door LOGLEVEL;</span><span class="sxs-lookup"><span data-stu-id="90b3f-132">GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</span></span></td><td><span data-ttu-id="90b3f-133">Groepen Hallo rijen door logboekniveau en slaat Hallo resultaten in GROUPEDLEVELS.</span><span class="sxs-lookup"><span data-stu-id="90b3f-133">Groups hello rows by log level and stores hello results into GROUPEDLEVELS.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="90b3f-134">FREQUENTIES foreach = GROUPEDLEVELS groep genereren als LOGLEVEL, COUNT (FILTEREDLEVELS. LOGLEVEL) zoals tellen;</span><span class="sxs-lookup"><span data-stu-id="90b3f-134">FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</span></span></td><td><span data-ttu-id="90b3f-135">Maakt een nieuwe set van gegevens in elk logboek unieke waarde en hoe vaak het optreedt.</span><span class="sxs-lookup"><span data-stu-id="90b3f-135">Creates a new set of data that contains each unique log level value and how many times it occurs.</span></span> <span data-ttu-id="90b3f-136">Dit bestand bevindt zich in de FREQUENTIES</span><span class="sxs-lookup"><span data-stu-id="90b3f-136">This is stored into FREQUENCIES</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="90b3f-137">RESULTAAT = volgorde FREQUENTIES door aantal desc;</span><span class="sxs-lookup"><span data-stu-id="90b3f-137">RESULT = order FREQUENCIES by COUNT desc;</span></span></td><td><span data-ttu-id="90b3f-138">Hallo-logboekniveaus op aantal (aflopend) en slaat de orders in resultaat</span><span class="sxs-lookup"><span data-stu-id="90b3f-138">Orders hello log levels by count (descending,) and stores into RESULT</span></span></td>
    </tr>
    </table><span data-ttu-id="90b3f-139">
6.U kunt ook de resultaten van een transformatie Hallo opslaan met behulp van Hallo `STORE` instructie.</span><span class="sxs-lookup"><span data-stu-id="90b3f-139">
6. You can also save hello results of a transformation by using hello `STORE` statement.</span></span> <span data-ttu-id="90b3f-140">Bijvoorbeeld Hallo volgende opdracht slaat Hallo `RESULT` toohello **/example/data/pigout** map in Hallo standaardopslagcontainer voor uw cluster:</span><span class="sxs-lookup"><span data-stu-id="90b3f-140">For example, hello following command saves hello `RESULT` toohello **/example/data/pigout** directory in hello default storage container for your cluster:</span></span>

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > <span data-ttu-id="90b3f-141">Hallo-gegevens worden opgeslagen in de opgegeven map Hallo in bestanden met de naam **onderdeel nnnnn**.</span><span class="sxs-lookup"><span data-stu-id="90b3f-141">hello data is stored in hello specified directory in files named **part-nnnnn**.</span></span> <span data-ttu-id="90b3f-142">Als het Hallo-map al bestaat, ontvangt u een foutbericht weergegeven.</span><span class="sxs-lookup"><span data-stu-id="90b3f-142">If hello directory already exists, you will receive an error message.</span></span>
   >
   >
7. <span data-ttu-id="90b3f-143">tooexit hello knorvis vragen, Voer Hallo-instructie.</span><span class="sxs-lookup"><span data-stu-id="90b3f-143">tooexit hello grunt prompt, enter hello following statement.</span></span>

        QUIT;

### <a name="pig-latin-batch-files"></a><span data-ttu-id="90b3f-144">Pig Latin batch-bestanden</span><span class="sxs-lookup"><span data-stu-id="90b3f-144">Pig Latin batch files</span></span>
<span data-ttu-id="90b3f-145">U kunt ook Hallo Pig opdracht toorun Pig Latin die is opgenomen in een bestand.</span><span class="sxs-lookup"><span data-stu-id="90b3f-145">You can also use hello Pig command toorun Pig Latin that is contained in a file.</span></span>

1. <span data-ttu-id="90b3f-146">Open na het afsluiten van Hallo knorvis prompt **Kladblok** en maak een nieuw bestand met de naam **pigbatch.pig** in Hallo **% PIG_HOME %** directory.</span><span class="sxs-lookup"><span data-stu-id="90b3f-146">After exiting hello grunt prompt, open **Notepad** and create a new file named **pigbatch.pig** in hello **%PIG_HOME%** directory.</span></span>
2. <span data-ttu-id="90b3f-147">Type of plakken Hallo volgende regels in Hallo **pigbatch.pig** bestand en sla het:</span><span class="sxs-lookup"><span data-stu-id="90b3f-147">Type or paste hello following lines into hello **pigbatch.pig** file, and then save it:</span></span>

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. <span data-ttu-id="90b3f-148">Gebruik Hallo na toorun hello **pigbatch.pig** -bestand met Hallo pig-opdracht.</span><span class="sxs-lookup"><span data-stu-id="90b3f-148">Use hello following toorun hello **pigbatch.pig** file using hello pig command.</span></span>

        pig %PIG_HOME%\pigbatch.pig

    <span data-ttu-id="90b3f-149">Wanneer Hallo batch-job is voltooid, ziet u Hallo na uitvoer, die moet worden Hallo hetzelfde als wanneer u gebruikt `DUMP RESULT;` in de vorige stappen Hallo:</span><span class="sxs-lookup"><span data-stu-id="90b3f-149">When hello batch job completes, you should see hello following output, which should be hello same as when you used `DUMP RESULT;` in hello previous steps:</span></span>

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="90b3f-150"><a id="summary"></a>Samenvatting</span><span class="sxs-lookup"><span data-stu-id="90b3f-150"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="90b3f-151">Zoals u zien kunt, kunt u Hallo Pig opdracht toointeractively MapReduce-bewerkingen uitvoeren of Pig Latin taken uitvoeren die zijn opgeslagen in een batch-bestand.</span><span class="sxs-lookup"><span data-stu-id="90b3f-151">As you can see, hello Pig command allows you toointeractively run MapReduce operations, or run Pig Latin jobs that are stored in a batch file.</span></span>

## <span data-ttu-id="90b3f-152"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="90b3f-152"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="90b3f-153">Voor algemene informatie over Pig in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="90b3f-153">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="90b3f-154">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="90b3f-154">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="90b3f-155">Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="90b3f-155">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="90b3f-156">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="90b3f-156">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="90b3f-157">MapReduce gebruiken met Hadoop op HDInsight</span><span class="sxs-lookup"><span data-stu-id="90b3f-157">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
