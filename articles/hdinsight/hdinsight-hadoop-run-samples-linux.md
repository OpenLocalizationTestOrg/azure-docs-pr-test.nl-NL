---
title: aaaRun Hadoop-MapReduce-voorbeelden op HDInsight - Azure | Microsoft Docs
description: Aan de slag met MapReduce-voorbeelden in jar-bestanden die zijn opgenomen in HDInsight. Gebruik van SSH tooconnect toohello cluster en gebruik vervolgens Hallo Hadoop opdracht toorun voorbeeld-taken.
keywords: hadoop voorbeeld jar, hadoop voorbeelden jar, voorbeelden van hadoop-mapreduce, mapreduce-voorbeelden
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e1d2a0b9-1659-4fab-921e-4a8990cbb30a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 7a16bbd51eb17570fcaa3b1e0f5990fa889c106a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hello-mapreduce-examples-included-in-hdinsight"></a><span data-ttu-id="d5233-105">Hallo MapReduce voorbeelden is opgenomen in HDInsight uitvoeren</span><span class="sxs-lookup"><span data-stu-id="d5233-105">Run hello MapReduce examples included in HDInsight</span></span>

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="d5233-106">Meer informatie over hoe toorun hello MapReduce voorbeelden opgenomen met Hadoop op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d5233-106">Learn how toorun hello MapReduce examples included with Hadoop on HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5233-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d5233-107">Prerequisites</span></span>

* <span data-ttu-id="d5233-108">**Een HDInsight-cluster**: Zie [aan de slag met Hadoop met Hive in HDInsight op Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="d5233-108">**An HDInsight cluster**: See [Get started using Hadoop with Hive in HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d5233-109">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="d5233-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d5233-110">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d5233-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="d5233-111">**Een SSH-client**: Zie voor meer informatie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d5233-111">**An SSH client**: For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <a name="hello-mapreduce-examples"></a><span data-ttu-id="d5233-112">Hallo MapReduce-voorbeelden</span><span class="sxs-lookup"><span data-stu-id="d5233-112">hello MapReduce examples</span></span>

<span data-ttu-id="d5233-113">**Locatie**: Hallo voorbeelden bevinden zich op HDInsight-cluster op Hallo `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="d5233-113">**Location**: hello samples are located on hello HDInsight cluster at `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.</span></span>

<span data-ttu-id="d5233-114">**Inhoud**: Hallo volgen voorbeelden zijn opgenomen in dit archief:</span><span class="sxs-lookup"><span data-stu-id="d5233-114">**Contents**: hello following samples are contained in this archive:</span></span>

* <span data-ttu-id="d5233-115">`aggregatewordcount`: Er is een statistische functie gebaseerd mapreduce-programma dat Hallo woorden in Hallo invoerbestanden geteld.</span><span class="sxs-lookup"><span data-stu-id="d5233-115">`aggregatewordcount`: An Aggregate based mapreduce program that counts hello words in hello input files.</span></span>
* <span data-ttu-id="d5233-116">`aggregatewordhist`: Er is een statistische functie gebaseerd mapreduce-programma dat wordt berekend Hallo histogram Hallo woorden in Hallo invoerbestanden.</span><span class="sxs-lookup"><span data-stu-id="d5233-116">`aggregatewordhist`: An Aggregate based mapreduce program that computes hello histogram of hello words in hello input files.</span></span>
* <span data-ttu-id="d5233-117">`bbp`: Een mapreduce-programma dat gebruikmaakt van Bailey-Borwein-Plouffe toocompute exacte cijfers van Pi.</span><span class="sxs-lookup"><span data-stu-id="d5233-117">`bbp`: A mapreduce program that uses Bailey-Borwein-Plouffe toocompute exact digits of Pi.</span></span>
* <span data-ttu-id="d5233-118">`dbcount`: Er is een voorbeeld van de taak die Hallo pageview logboeken opgeslagen in een database telt.</span><span class="sxs-lookup"><span data-stu-id="d5233-118">`dbcount`: An example job that counts hello pageview logs stored in a database.</span></span>
* <span data-ttu-id="d5233-119">`distbbp`: Een mapreduce-programma dat gebruikmaakt van een formule toocompute BBP type bits exacte van Pi.</span><span class="sxs-lookup"><span data-stu-id="d5233-119">`distbbp`: A mapreduce program that uses a BBP-type formula toocompute exact bits of Pi.</span></span>
* <span data-ttu-id="d5233-120">`grep`: Een mapreduce-programma dat wordt geteld Hallo komt overeen met van een reguliere expressie in de Hallo-invoer.</span><span class="sxs-lookup"><span data-stu-id="d5233-120">`grep`: A mapreduce program that counts hello matches of a regex in hello input.</span></span>
* <span data-ttu-id="d5233-121">`join`: Een taak die een join uitvoert via gesorteerd, evenveel gepartitioneerd gegevenssets.</span><span class="sxs-lookup"><span data-stu-id="d5233-121">`join`: A job that performs a join over sorted, equally partitioned datasets.</span></span>
* <span data-ttu-id="d5233-122">`multifilewc`: Een taak die woorden uit verschillende bestanden telt.</span><span class="sxs-lookup"><span data-stu-id="d5233-122">`multifilewc`: A job that counts words from several files.</span></span>
* <span data-ttu-id="d5233-123">`pentomino`: Een mapreduce-tegel elementlay programma toofind oplossingen toopentomino problemen.</span><span class="sxs-lookup"><span data-stu-id="d5233-123">`pentomino`: A mapreduce tile laying program toofind solutions toopentomino problems.</span></span>
* <span data-ttu-id="d5233-124">`pi`: Een mapreduce-programma dat u maakt een schatting van Pi met behulp van een quasi Monte Carlo-methode.</span><span class="sxs-lookup"><span data-stu-id="d5233-124">`pi`: A mapreduce program that estimates Pi using a quasi-Monte Carlo method.</span></span>
* <span data-ttu-id="d5233-125">`randomtextwriter`: Een mapreduce-programma dat 10 GB met willekeurige tekstgegevens per knooppunt schrijft.</span><span class="sxs-lookup"><span data-stu-id="d5233-125">`randomtextwriter`: A mapreduce program that writes 10 GB of random textual data per node.</span></span>
* <span data-ttu-id="d5233-126">`randomwriter`: Een mapreduce-programma dat 10 GB willekeurige gegevens per knooppunt schrijft.</span><span class="sxs-lookup"><span data-stu-id="d5233-126">`randomwriter`: A mapreduce program that writes 10 GB of random data per node.</span></span>
* <span data-ttu-id="d5233-127">`secondarysort`: Er is een voorbeeld van een secundaire sorteren toohello definiëren verminderen fase.</span><span class="sxs-lookup"><span data-stu-id="d5233-127">`secondarysort`: An example defining a secondary sort toohello reduce phase.</span></span>
* <span data-ttu-id="d5233-128">`sort`: Een mapreduce-programma dat Hallo gegevens geschreven door Hallo willekeurige writer gesorteerd.</span><span class="sxs-lookup"><span data-stu-id="d5233-128">`sort`: A mapreduce program that sorts hello data written by hello random writer.</span></span>
* <span data-ttu-id="d5233-129">`sudoku`: Een sudoku Solver '.</span><span class="sxs-lookup"><span data-stu-id="d5233-129">`sudoku`: A sudoku solver.</span></span>
* <span data-ttu-id="d5233-130">`teragen`: De gegevens voor Hallo terasort genereren.</span><span class="sxs-lookup"><span data-stu-id="d5233-130">`teragen`: Generate data for hello terasort.</span></span>
* <span data-ttu-id="d5233-131">`terasort`: Hallo terasort worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d5233-131">`terasort`: Run hello terasort.</span></span>
* <span data-ttu-id="d5233-132">`teravalidate`: De resultaten van terasort controleren.</span><span class="sxs-lookup"><span data-stu-id="d5233-132">`teravalidate`: Checking results of terasort.</span></span>
* <span data-ttu-id="d5233-133">`wordcount`: Een mapreduce-programma dat Hallo woorden in Hallo invoerbestanden geteld.</span><span class="sxs-lookup"><span data-stu-id="d5233-133">`wordcount`: A mapreduce program that counts hello words in hello input files.</span></span>
* <span data-ttu-id="d5233-134">`wordmean`: Een mapreduce-programma dat Hallo gemiddelde duur van Hallo woorden in Hallo invoerbestanden telt.</span><span class="sxs-lookup"><span data-stu-id="d5233-134">`wordmean`: A mapreduce program that counts hello average length of hello words in hello input files.</span></span>
* <span data-ttu-id="d5233-135">`wordmedian`: Een mapreduce-programma dat Hallo mediaan lengte van Hallo woorden in Hallo invoerbestanden telt.</span><span class="sxs-lookup"><span data-stu-id="d5233-135">`wordmedian`: A mapreduce program that counts hello median length of hello words in hello input files.</span></span>
* <span data-ttu-id="d5233-136">`wordstandarddeviation`: Een mapreduce-programma dat Hallo standaardafwijking van Hallo lengte van Hallo woorden in Hallo invoerbestanden telt.</span><span class="sxs-lookup"><span data-stu-id="d5233-136">`wordstandarddeviation`: A mapreduce program that counts hello standard deviation of hello length of hello words in hello input files.</span></span>

<span data-ttu-id="d5233-137">**Broncode**: broncode voor deze voorbeelden is opgenomen op HDInsight-cluster op Hallo `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span><span class="sxs-lookup"><span data-stu-id="d5233-137">**Source code**: Source code for these samples is included on hello HDInsight cluster at `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.</span></span>

> [!NOTE]
> <span data-ttu-id="d5233-138">Hallo `2.2.4.9-1` in Hallo pad Hallo-versie van Hallo Hortonworks Data Platform voor Hallo HDInsight-cluster is en kunnen afwijken voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="d5233-138">hello `2.2.4.9-1` in hello path is hello version of hello Hortonworks Data Platform for hello HDInsight cluster, and may be different for your cluster.</span></span>

## <a name="run-hello-wordcount-example"></a><span data-ttu-id="d5233-139">Hallo wordcount-voorbeeld uitvoeren</span><span class="sxs-lookup"><span data-stu-id="d5233-139">Run hello wordcount example</span></span>

1. <span data-ttu-id="d5233-140">Verbinding maken via SSH tooHDInsight.</span><span class="sxs-lookup"><span data-stu-id="d5233-140">Connect tooHDInsight using SSH.</span></span> <span data-ttu-id="d5233-141">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d5233-141">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="d5233-142">Van Hallo `username@#######:~$` gevraagd, gebruikt u Hallo Voorbeeldopdrachten toolist hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="d5233-142">From hello `username@#######:~$` prompt, use hello following command toolist hello samples:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    <span data-ttu-id="d5233-143">Met deze opdracht genereert Hallo-lijst van voorbeeld van de vorige sectie Hallo van dit document.</span><span class="sxs-lookup"><span data-stu-id="d5233-143">This command generates hello list of sample from hello previous section of this document.</span></span>

3. <span data-ttu-id="d5233-144">Gebruik hello opdracht tooget help op een specifieke voorbeeld te volgen.</span><span class="sxs-lookup"><span data-stu-id="d5233-144">Use hello following command tooget help on a specific sample.</span></span> <span data-ttu-id="d5233-145">In dit geval Hallo **wordcount** voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="d5233-145">In this case, hello **wordcount** sample:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    <span data-ttu-id="d5233-146">U ontvangt Hallo volgende bericht:</span><span class="sxs-lookup"><span data-stu-id="d5233-146">You receive hello following message:</span></span>

        Usage: wordcount <in> [<in>...] <out>

    <span data-ttu-id="d5233-147">Dit bericht geeft aan dat u verschillende invoerpaden voor Hallo brondocumenten bieden kunt.</span><span class="sxs-lookup"><span data-stu-id="d5233-147">This message indicates that you can provide several input paths for hello source documents.</span></span> <span data-ttu-id="d5233-148">Hallo uiteindelijke pad is waar Hallo uitvoer (aantal woorden in Hallo brondocumenten) wordt opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="d5233-148">hello final path is where hello output (count of words in hello source documents) is stored.</span></span>

4. <span data-ttu-id="d5233-149">Hallo toocount na alle woorden in Hallo notitieblokken van Leonardo Da Vinci, die beschikbaar worden gesteld als voorbeeldgegevens met uw cluster gebruiken:</span><span class="sxs-lookup"><span data-stu-id="d5233-149">Use hello following toocount all words in hello Notebooks of Leonardo Da Vinci, which are provided as sample data with your cluster:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    <span data-ttu-id="d5233-150">Invoer voor deze taak wordt gelezen uit `/example/data/gutenberg/davinci.txt`.</span><span class="sxs-lookup"><span data-stu-id="d5233-150">Input for this job is read from `/example/data/gutenberg/davinci.txt`.</span></span> <span data-ttu-id="d5233-151">Uitvoer voor dit voorbeeld wordt opgeslagen in `/example/data/davinciwordcount`.</span><span class="sxs-lookup"><span data-stu-id="d5233-151">Output for this example is stored in `/example/data/davinciwordcount`.</span></span> <span data-ttu-id="d5233-152">Beide paden bevinden zich op standaard opslag voor Hallo-cluster niet Hallo het lokale bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="d5233-152">Both paths are located on default storage for hello cluster, not hello local file system.</span></span>

   > [!NOTE]
   > <span data-ttu-id="d5233-153">Zoals beschreven in de help van Hallo voor Hallo wordcount-voorbeeld, kunt u ook meerdere invoerbestanden opgeven.</span><span class="sxs-lookup"><span data-stu-id="d5233-153">As noted in hello help for hello wordcount sample, you could also specify multiple input files.</span></span> <span data-ttu-id="d5233-154">Bijvoorbeeld: `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` woorden in zowel davinci.txt en ulysses.txt geteld.</span><span class="sxs-lookup"><span data-stu-id="d5233-154">For example, `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` would count words in both davinci.txt and ulysses.txt.</span></span>

5. <span data-ttu-id="d5233-155">Zodra het Hallo-taak is voltooid, gebruikt u Hallo opdrachtuitvoer tooview hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="d5233-155">Once hello job completes, use hello following command tooview hello output:</span></span>

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    <span data-ttu-id="d5233-156">Met deze opdracht worden alle bestanden met Hallo uitvoer geproduceerd door Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="d5233-156">This command concatenates all hello output files produced by hello job.</span></span> <span data-ttu-id="d5233-157">Hallo uitvoer toohello console worden weergegeven.</span><span class="sxs-lookup"><span data-stu-id="d5233-157">It displays hello output toohello console.</span></span> <span data-ttu-id="d5233-158">Hallo uitvoer is vergelijkbaar toohello de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="d5233-158">hello output is similar toohello following text:</span></span>

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    <span data-ttu-id="d5233-159">Elke regel vertegenwoordigt een woord en hoe vaak het is opgetreden in Hallo invoergegevens.</span><span class="sxs-lookup"><span data-stu-id="d5233-159">Each line represents a word and how many times it occurred in hello input data.</span></span>

## <a name="hello-sudoku-example"></a><span data-ttu-id="d5233-160">Hallo Sudoku voorbeeld</span><span class="sxs-lookup"><span data-stu-id="d5233-160">hello Sudoku example</span></span>

<span data-ttu-id="d5233-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) is een logische puzzel bestaat uit negen 3 x 3 rasters.</span><span class="sxs-lookup"><span data-stu-id="d5233-161">[Sudoku](https://en.wikipedia.org/wiki/Sudoku) is a logic puzzle made up of nine 3x3 grids.</span></span> <span data-ttu-id="d5233-162">Sommige cellen in het raster Hallo hebben aantallen, terwijl andere gebruikers leeg zijn en Hallo doel toosolve voor Hallo lege cellen is.</span><span class="sxs-lookup"><span data-stu-id="d5233-162">Some cells in hello grid have numbers, while others are blank, and hello goal is toosolve for hello blank cells.</span></span> <span data-ttu-id="d5233-163">Hallo vorige koppeling meer informatie over het Hallo puzzel heeft, maar Hallo doel van dit voorbeeld is toosolve voor Hallo lege cellen.</span><span class="sxs-lookup"><span data-stu-id="d5233-163">hello previous link has more information on hello puzzle, but hello purpose of this sample is toosolve for hello blank cells.</span></span> <span data-ttu-id="d5233-164">De invoer moet dus een bestand dat zich in de volgende indeling Hallo:</span><span class="sxs-lookup"><span data-stu-id="d5233-164">So our input should be a file that is in hello following format:</span></span>

* <span data-ttu-id="d5233-165">Negen rijen van de negen kolommen</span><span class="sxs-lookup"><span data-stu-id="d5233-165">Nine rows of nine columns</span></span>
* <span data-ttu-id="d5233-166">Elke kolom mag een getal of `?` (geeft een lege cel)</span><span class="sxs-lookup"><span data-stu-id="d5233-166">Each column can contain either a number or `?` (which indicates a blank cell)</span></span>
* <span data-ttu-id="d5233-167">Cellen zijn gescheiden door een spatie</span><span class="sxs-lookup"><span data-stu-id="d5233-167">Cells are separated by a space</span></span>

<span data-ttu-id="d5233-168">Er is een bepaalde manier tooconstruct Sudoku puzzels; een getal in een kolom of de rij kan niet worden herhaald.</span><span class="sxs-lookup"><span data-stu-id="d5233-168">There is a certain way tooconstruct Sudoku puzzles; you can't repeat a number in a column or row.</span></span> <span data-ttu-id="d5233-169">Er is een voorbeeld op Hallo HDInsight-cluster die correct is samengesteld.</span><span class="sxs-lookup"><span data-stu-id="d5233-169">There's an example on hello HDInsight cluster that is properly constructed.</span></span> <span data-ttu-id="d5233-170">Deze bevindt zich op `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` en bevat de volgende tekst hello:</span><span class="sxs-lookup"><span data-stu-id="d5233-170">It is located at `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` and contains hello following text:</span></span>

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

<span data-ttu-id="d5233-171">toorun dit probleem voorbeeld Hallo Sudoku bijvoorbeeld gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="d5233-171">toorun this example problem through hello Sudoku example, use hello following command:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

<span data-ttu-id="d5233-172">Hallo-resultaten verschijnen vergelijkbare toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="d5233-172">hello results appear similar toohello following text:</span></span>

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a><span data-ttu-id="d5233-173">Voorbeeld van pi (π)</span><span class="sxs-lookup"><span data-stu-id="d5233-173">Pi (π) example</span></span>

<span data-ttu-id="d5233-174">Hallo pi voorbeeld maakt gebruik van een statistische (quasi Monte Carlo) methode tooestimate Hallo waarde van pi.</span><span class="sxs-lookup"><span data-stu-id="d5233-174">hello pi sample uses a statistical (quasi-Monte Carlo) method tooestimate hello value of pi.</span></span> <span data-ttu-id="d5233-175">Punten worden in willekeurige volgorde in een vierkant eenheid geplaatst.</span><span class="sxs-lookup"><span data-stu-id="d5233-175">Points are placed at random in a unit square.</span></span> <span data-ttu-id="d5233-176">Hallo vierkante bevat ook een cirkel.</span><span class="sxs-lookup"><span data-stu-id="d5233-176">hello square also contains a circle.</span></span> <span data-ttu-id="d5233-177">Hallo kans dat Hallo punten Hallo cirkel vallen zijn gelijk toohello gebied Hallo cirkel-, pi/4.</span><span class="sxs-lookup"><span data-stu-id="d5233-177">hello probability that hello points fall within hello circle are equal toohello area of hello circle, pi/4.</span></span> <span data-ttu-id="d5233-178">Hallo-waarde van pi kan worden geschat van Hallo-waarde van 4R.</span><span class="sxs-lookup"><span data-stu-id="d5233-178">hello value of pi can be estimated from hello value of 4R.</span></span> <span data-ttu-id="d5233-179">R is Hallo verhouding tussen aantal punten in Hallo cirkel toohello totaal aantal punten die binnen Hallo vierkante Hallo.</span><span class="sxs-lookup"><span data-stu-id="d5233-179">R is hello ratio of hello number of points that are inside hello circle toohello total number of points that are within hello square.</span></span> <span data-ttu-id="d5233-180">Hallo groter Hallo voorbeeld van punten gebruikt, Hallo beter Hallo inschatten is.</span><span class="sxs-lookup"><span data-stu-id="d5233-180">hello larger hello sample of points used, hello better hello estimate is.</span></span>

<span data-ttu-id="d5233-181">Hallo opdracht toorun volgende dit voorbeeld gebruiken.</span><span class="sxs-lookup"><span data-stu-id="d5233-181">Use hello following command toorun this sample.</span></span> <span data-ttu-id="d5233-182">Met deze opdracht gebruikt 16-kaarten met 10.000.000 voorbeelden tooestimate Hallo waarde van pi:</span><span class="sxs-lookup"><span data-stu-id="d5233-182">This command uses 16 maps with 10,000,000 samples each tooestimate hello value of pi:</span></span>

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

<span data-ttu-id="d5233-183">Hallo waarde geretourneerd door deze opdracht is vergelijkbaar te**3.14159155000000000000**.</span><span class="sxs-lookup"><span data-stu-id="d5233-183">hello value returned by this command is similar too**3.14159155000000000000**.</span></span> <span data-ttu-id="d5233-184">Voor verwijzingen zijn hello eerste 10 decimalen van pi 3.1415926535.</span><span class="sxs-lookup"><span data-stu-id="d5233-184">For references, hello first 10 decimal places of pi are 3.1415926535.</span></span>

## <a name="10-gb-greysort-example"></a><span data-ttu-id="d5233-185">Voorbeeld van 10 GB-Greysort</span><span class="sxs-lookup"><span data-stu-id="d5233-185">10 GB Greysort example</span></span>

<span data-ttu-id="d5233-186">GraySort is een benchmark-sortering.</span><span class="sxs-lookup"><span data-stu-id="d5233-186">GraySort is a benchmark sort.</span></span> <span data-ttu-id="d5233-187">Hallo-metriek is Hallo sorteren snelheid (TB per minuut) die tijdens het sorteren van grote hoeveelheden gegevens, meestal een 100 TB minimale wordt bereikt.</span><span class="sxs-lookup"><span data-stu-id="d5233-187">hello metric is hello sort rate (TB/minute) that is achieved while sorting large amounts of data, usually a 100 TB minimum.</span></span>

<span data-ttu-id="d5233-188">Dit voorbeeld wordt een matige 10 GB aan gegevens gebruikt, zodat deze kan relatief snel kan worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d5233-188">This sample uses a modest 10 GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="d5233-189">Hallo MapReduce-toepassingen die zijn ontwikkeld door Owen O'Malley en Arun Murthy wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="d5233-189">It uses hello MapReduce applications developed by Owen O'Malley and Arun Murthy.</span></span> <span data-ttu-id="d5233-190">Deze toepassingen gewonnen Hallo jaarlijkse Algemeen ('daytona') terabyte sorteren benchmark in 2009, met een snelheid van 0.578 TB/min (100 TB in 173 minuten).</span><span class="sxs-lookup"><span data-stu-id="d5233-190">These applications won hello annual general-purpose ("daytona") terabyte sort benchmark in 2009, with a rate of 0.578 TB/min (100 TB in 173 minutes).</span></span> <span data-ttu-id="d5233-191">Zie voor meer informatie over deze en andere sorteren benchmarks Hallo [Sortbenchmark](http://sortbenchmark.org/) site.</span><span class="sxs-lookup"><span data-stu-id="d5233-191">For more information on this and other sorting benchmarks, see hello [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="d5233-192">Dit voorbeeld worden drie sets van MapReduce-programma's gebruikt:</span><span class="sxs-lookup"><span data-stu-id="d5233-192">This sample uses three sets of MapReduce programs:</span></span>

* <span data-ttu-id="d5233-193">**TeraGen**: een MapReduce-programma die rijen met gegevens toosort genereert</span><span class="sxs-lookup"><span data-stu-id="d5233-193">**TeraGen**: A MapReduce program that generates rows of data toosort</span></span>

* <span data-ttu-id="d5233-194">**TeraSort**: Hallo invoergegevens voorbeelden en MapReduce toosort Hallo gegevens worden gebruikt in een totale volgorde</span><span class="sxs-lookup"><span data-stu-id="d5233-194">**TeraSort**: Samples hello input data and uses MapReduce toosort hello data into a total order</span></span>

    <span data-ttu-id="d5233-195">TeraSort is een standaard sortering MapReduce, met uitzondering van een aangepaste partitioner.</span><span class="sxs-lookup"><span data-stu-id="d5233-195">TeraSort is a standard MapReduce sort, except for a custom partitioner.</span></span> <span data-ttu-id="d5233-196">Hallo partitioner maakt gebruik van een gesorteerde lijst met actieve N-1 sleutels die Hallo sleutel bereik voor elke verminderen definiëren.</span><span class="sxs-lookup"><span data-stu-id="d5233-196">hello partitioner uses a sorted list of N-1 sampled keys that define hello key range for each reduce.</span></span> <span data-ttu-id="d5233-197">In het bijzonder alle sleutels dergelijke waarvan de steekproef [i-1] < sleutel = < voorbeeld [i] tooreduce worden verzonden ik.</span><span class="sxs-lookup"><span data-stu-id="d5233-197">In particular, all keys such that sample[i-1] <= key < sample[i] are sent tooreduce i.</span></span> <span data-ttu-id="d5233-198">Deze partitioner garanties dat Hallo uitvoerwaarden van ik beperken zijn alle kleiner is dan Hallo-uitvoer van verminderen i + 1.</span><span class="sxs-lookup"><span data-stu-id="d5233-198">This partitioner guarantees that hello outputs of reduce i are all less than hello output of reduce i+1.</span></span>

* <span data-ttu-id="d5233-199">**TeraValidate**: een MapReduce-programma te valideren die uitvoer Hallo globaal wordt gesorteerd</span><span class="sxs-lookup"><span data-stu-id="d5233-199">**TeraValidate**: A MapReduce program that validates that hello output is globally sorted</span></span>

    <span data-ttu-id="d5233-200">Een kaart per bestand wordt gemaakt in de uitvoermap Hallo en elke toewijzing zorgt ervoor dat elke sleutel kleiner dan of gelijk is toohello vorige.</span><span class="sxs-lookup"><span data-stu-id="d5233-200">It creates one map per file in hello output directory, and each map ensures that each key is less than or equal toohello previous one.</span></span> <span data-ttu-id="d5233-201">Hallo kaart functie records Hallo eerst genereert en laatste sleutels van elk bestand.</span><span class="sxs-lookup"><span data-stu-id="d5233-201">hello map function generates records of hello first and last keys of each file.</span></span> <span data-ttu-id="d5233-202">Hallo functie verminderen zorgt ervoor dat Hallo eerste sleutel van i-bestand is groter dan de laatste sleutel Hallo van bestand i-1.</span><span class="sxs-lookup"><span data-stu-id="d5233-202">hello reduce function ensures that hello first key of file i is greater than hello last key of file i-1.</span></span> <span data-ttu-id="d5233-203">Eventuele problemen worden gerapporteerd als uitvoer voor Hallo fase verminderen met Hallo sleutels die zijn geplaatst.</span><span class="sxs-lookup"><span data-stu-id="d5233-203">Any problems are reported as an output of hello reduce phase, with hello keys that are out of order.</span></span>

<span data-ttu-id="d5233-204">Gebruik Hallo volgende stappen uit toogenerate gegevens, sorteren en vervolgens te valideren Hallo uitvoer:</span><span class="sxs-lookup"><span data-stu-id="d5233-204">Use hello following steps toogenerate data, sort, and then validate hello output:</span></span>

1. <span data-ttu-id="d5233-205">Genereren van 10 GB aan gegevens, die opgeslagen toohello HDInsight cluster standaard opslag is op `/example/data/10GB-sort-input`:</span><span class="sxs-lookup"><span data-stu-id="d5233-205">Generate 10 GB of data, which is stored toohello HDInsight cluster's default storage at `/example/data/10GB-sort-input`:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    <span data-ttu-id="d5233-206">Hallo `-Dmapred.map.tasks` vertelt Hadoop hoeveel kaart taken toouse voor deze taak.</span><span class="sxs-lookup"><span data-stu-id="d5233-206">hello `-Dmapred.map.tasks` tells Hadoop how many map tasks toouse for this job.</span></span> <span data-ttu-id="d5233-207">Hallo laatste twee parameters instrueren Hallo taak toocreate 10 GB aan gegevens en toostore op `/example/data/10GB-sort-input`.</span><span class="sxs-lookup"><span data-stu-id="d5233-207">hello final two parameters instruct hello job toocreate 10 GB of data and toostore it at `/example/data/10GB-sort-input`.</span></span>

2. <span data-ttu-id="d5233-208">Gebruik Hallo opdracht toosort Hallo gegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="d5233-208">Use hello following command toosort hello data:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    <span data-ttu-id="d5233-209">Hallo `-Dmapred.reduce.tasks` Hadoop geeft aan hoeveel taken toouse voor Hallo taak verminderen.</span><span class="sxs-lookup"><span data-stu-id="d5233-209">hello `-Dmapred.reduce.tasks` tells Hadoop how many reduce tasks toouse for hello job.</span></span> <span data-ttu-id="d5233-210">Hallo laatste twee parameters zijn alleen Hallo invoer en uitvoer van de locaties voor gegevens.</span><span class="sxs-lookup"><span data-stu-id="d5233-210">hello final two parameters are just hello input and output locations for data.</span></span>

3. <span data-ttu-id="d5233-211">Hallo volgt toovalidate Hallo gegevens die worden gegenereerd door Hallo sorteren gebruiken:</span><span class="sxs-lookup"><span data-stu-id="d5233-211">Use hello following toovalidate hello data generated by hello sort:</span></span>

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a><span data-ttu-id="d5233-212">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d5233-212">Next steps</span></span>

<span data-ttu-id="d5233-213">In dit artikel hebt u geleerd hoe toorun Hallo voorbeelden opgenomen Hello Linux gebaseerde HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="d5233-213">From this article, you learned how toorun hello samples included with hello Linux-based HDInsight clusters.</span></span> <span data-ttu-id="d5233-214">Zie voor de zelfstudies over het gebruik van Pig, Hive en MapReduce met HDInsight, Hallo volgende onderwerpen:</span><span class="sxs-lookup"><span data-stu-id="d5233-214">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see hello following topics:</span></span>

* <span data-ttu-id="d5233-215">[Pig gebruiken met Hadoop in HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="d5233-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="d5233-216">[Hive gebruiken met Hadoop in HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="d5233-216">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="d5233-217">[MapReduce gebruiken met Hadoop op HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="d5233-217">[Use MapReduce with Hadoop on HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
