---
title: aaaGenerate aanbevelingen met Mahout en HDInsight (SSH) - Azure | Microsoft Docs
description: Meer informatie over hoe toouse Hallo Apache Mahout machine learning-bibliotheek toogenerate filmaanbevelingen met HDInsight (Hadoop).
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c78ec37c-9a8c-4bb6-9e38-0bdb9e89fbd7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: fedac9ceb4268f8421bce4623a5ad271041b8b3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a><span data-ttu-id="95097-103">Filmaanbevelingen genereren met behulp van Apache Mahout met Hadoop op basis van Linux in HDInsight (SSH)</span><span class="sxs-lookup"><span data-stu-id="95097-103">Generate movie recommendations by using Apache Mahout with Linux-based Hadoop in HDInsight (SSH)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="95097-104">Meer informatie over hoe toouse hello [Apache Mahout](http://mahout.apache.org) machine learning-bibliotheek met Azure HDInsight toogenerate filmaanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="95097-104">Learn how toouse hello [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight toogenerate movie recommendations.</span></span>

<span data-ttu-id="95097-105">Mahout is een [machine learning] [ ml] -bibliotheek voor Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="95097-105">Mahout is a [machine learning][ml] library for Apache Hadoop.</span></span> <span data-ttu-id="95097-106">Mahout bevat algoritmen voor het verwerken van gegevens, zoals filteren, classificatie en clustering.</span><span class="sxs-lookup"><span data-stu-id="95097-106">Mahout contains algorithms for processing data, such as filtering, classification, and clustering.</span></span> <span data-ttu-id="95097-107">In dit artikel gebruikt u een aanbeveling engine toogenerate filmaanbevelingen die zijn gebaseerd op films je vrienden hebt gezien.</span><span class="sxs-lookup"><span data-stu-id="95097-107">In this article, you use a recommendation engine toogenerate movie recommendations that are based on movies your friends have seen.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="95097-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="95097-108">Prerequisites</span></span>

* <span data-ttu-id="95097-109">Een Linux gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="95097-109">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="95097-110">Zie voor meer informatie over het maken van een [aan de slag met Hadoop op basis van Linux in HDInsight][getstarted].</span><span class="sxs-lookup"><span data-stu-id="95097-110">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="95097-111">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="95097-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="95097-112">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="95097-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="95097-113">Een SSH-client.</span><span class="sxs-lookup"><span data-stu-id="95097-113">An SSH client.</span></span> <span data-ttu-id="95097-114">Zie voor meer informatie, Hallo [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="95097-114">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="mahout-versioning"></a><span data-ttu-id="95097-115">Mahout versiebeheer</span><span class="sxs-lookup"><span data-stu-id="95097-115">Mahout versioning</span></span>

<span data-ttu-id="95097-116">Zie voor meer informatie over het Hallo-versie van Mahout in HDInsight [HDInsight versies en Hadoop-onderdelen](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="95097-116">For more information about hello version of Mahout in HDInsight, see [HDInsight versions and Hadoop components](hdinsight-component-versioning.md).</span></span>

## <span data-ttu-id="95097-117"><a name="recommendations"></a>Understanding aanbevelingen</span><span class="sxs-lookup"><span data-stu-id="95097-117"><a name="recommendations"></a>Understanding recommendations</span></span>

<span data-ttu-id="95097-118">Een van Hallo-functies die wordt geleverd door Mahout is een aanbeveling-engine.</span><span class="sxs-lookup"><span data-stu-id="95097-118">One of hello functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="95097-119">Deze engine accepteert gegevens in de indeling van Hallo `userID`, `itemId`, en `prefValue` (Hallo voorkeur voor Hallo item).</span><span class="sxs-lookup"><span data-stu-id="95097-119">This engine accepts data in hello format of `userID`, `itemId`, and `prefValue` (hello preference for hello item).</span></span> <span data-ttu-id="95097-120">Mahout kunt uitvoeren, mede exemplaar analysis toodetermine: *gebruikers die een voorkeur voor een item hebben ook een voorkeur voor deze andere items hebt*.</span><span class="sxs-lookup"><span data-stu-id="95097-120">Mahout can then perform co-occurance analysis toodetermine: *users who have a preference for an item also have a preference for these other items*.</span></span> <span data-ttu-id="95097-121">Mahout vervolgens gebruikers met dergelijke-item-voorkeuren gebruikte toomake aanbevelingen kunnen worden bepaald.</span><span class="sxs-lookup"><span data-stu-id="95097-121">Mahout then determines users with like-item preferences, which can be used toomake recommendations.</span></span>

<span data-ttu-id="95097-122">Hallo is volgende werkstroom een voorbeeld van een vereenvoudigde die gebruikmaakt van filmgegevens:</span><span class="sxs-lookup"><span data-stu-id="95097-122">hello following workflow is a simplified example that uses movie data:</span></span>

* <span data-ttu-id="95097-123">**Mede exemplaar**: Jan Els en Bob alle bevallen *Star Wars*, *Empire ontvangen terug Hallo*, en *Return Hallo Jedi*.</span><span class="sxs-lookup"><span data-stu-id="95097-123">**Co-occurance**: Joe, Alice, and Bob all liked *Star Wars*, *hello Empire Strikes Back*, and *Return of hello Jedi*.</span></span> <span data-ttu-id="95097-124">Mahout bepaalt dat gebruikers die als een van deze films ook graag twee andere Hallo.</span><span class="sxs-lookup"><span data-stu-id="95097-124">Mahout determines that users who like any one of these movies also like hello other two.</span></span>

* <span data-ttu-id="95097-125">**Mede exemplaar**: Bob en Els ook bevallen *Hallo Phantom Menace*, *een aanval op Hallo klonen*, en *Revenge Hallo Sith*.</span><span class="sxs-lookup"><span data-stu-id="95097-125">**Co-occurance**: Bob and Alice also liked *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span> <span data-ttu-id="95097-126">Mahout bepaalt dat gebruikers die ook de vorige drie films Hallo bevallen, zoals deze drie films.</span><span class="sxs-lookup"><span data-stu-id="95097-126">Mahout determines that users who liked hello previous three movies also like these three movies.</span></span>

* <span data-ttu-id="95097-127">**Gelijkenis aanbeveling**: omdat Jan bevallen Hallo eerste drie films, Mahout wordt bekeken films die anderen met vergelijkbare voorkeuren bevallen, maar Joe heeft geen gevolgde (bevallen/geclassificeerd).</span><span class="sxs-lookup"><span data-stu-id="95097-127">**Similarity recommendation**: Because Joe liked hello first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="95097-128">In dit geval Mahout raadt *Hallo Phantom Menace*, *een aanval op Hallo klonen*, en *Revenge Hallo Sith*.</span><span class="sxs-lookup"><span data-stu-id="95097-128">In this case, Mahout recommends *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span>

### <a name="understanding-hello-data"></a><span data-ttu-id="95097-129">Understanding Hallo gegevens</span><span class="sxs-lookup"><span data-stu-id="95097-129">Understanding hello data</span></span>

<span data-ttu-id="95097-130">Gemakkelijk [GroupLens Research] [ movielens] biedt classificatie gegevens voor films in een indeling die compatibel is met Mahout.</span><span class="sxs-lookup"><span data-stu-id="95097-130">Conveniently, [GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="95097-131">Deze gegevens zijn beschikbaar op het cluster standaard opslag op `/HdiSamples/HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="95097-131">This data is available on your cluster's default storage at `/HdiSamples/HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="95097-132">Er zijn twee bestanden: `moviedb.txt` en `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="95097-132">There are two files, `moviedb.txt` and `user-ratings.txt`.</span></span> <span data-ttu-id="95097-133">Hallo gebruiker ratings.txt bestand wordt gebruikt tijdens de analyse, terwijl moviedb.txt gebruikte tooprovide gebruiksvriendelijke tekstinformatie Hallo resultaten van Hallo analyse om weer te geven.</span><span class="sxs-lookup"><span data-stu-id="95097-133">hello user-ratings.txt file is used during analysis, while moviedb.txt is used tooprovide user-friendly text information when displaying hello results of hello analysis.</span></span>

<span data-ttu-id="95097-134">Hallo gegevens in gebruiker ratings.txt heeft een structuur van `userID`, `movieID`, `userRating`, en `timestamp`, die vertellen hoe maximaal elke gebruiker een film beoordeeld.</span><span class="sxs-lookup"><span data-stu-id="95097-134">hello data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="95097-135">Hier volgt een voorbeeld van Hallo gegevens:</span><span class="sxs-lookup"><span data-stu-id="95097-135">Here is an example of hello data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-hello-analysis"></a><span data-ttu-id="95097-136">Hallo-analyse uitvoeren</span><span class="sxs-lookup"><span data-stu-id="95097-136">Run hello analysis</span></span>

<span data-ttu-id="95097-137">Gebruik van een SSH-verbinding toohello-cluster Hallo opdracht toorun Hallo aanbeveling taak te volgen:</span><span class="sxs-lookup"><span data-stu-id="95097-137">From an SSH connection toohello cluster, use hello following command toorun hello recommendation job:</span></span>

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> <span data-ttu-id="95097-138">Hallo taak duurt enkele minuten toocomplete, en mogelijk meerdere MapReduce-taken worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="95097-138">hello job may take several minutes toocomplete, and may run multiple MapReduce jobs.</span></span>

## <a name="view-hello-output"></a><span data-ttu-id="95097-139">Hallo-uitvoer weergeven</span><span class="sxs-lookup"><span data-stu-id="95097-139">View hello output</span></span>

1. <span data-ttu-id="95097-140">Zodra het Hallo-taak is voltooid, gebruikt u Hallo opdrachtuitvoer tooview Hallo gegenereerd na:</span><span class="sxs-lookup"><span data-stu-id="95097-140">Once hello job completes, use hello following command tooview hello generated output:</span></span>

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    <span data-ttu-id="95097-141">Hallo-uitvoer ziet er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="95097-141">hello output appears as follows:</span></span>

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    <span data-ttu-id="95097-142">de eerste kolom Hallo is Hallo `userID`.</span><span class="sxs-lookup"><span data-stu-id="95097-142">hello first column is hello `userID`.</span></span> <span data-ttu-id="95097-143">waarden in Hallo ' [' en ']' zijn `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="95097-143">hello values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

2. <span data-ttu-id="95097-144">U kunt Hallo-uitvoer, samen met de Hallo moviedb.txt, tooprovide meer informatie op Hallo aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="95097-144">You can use hello output, along with hello moviedb.txt, tooprovide more information on hello recommendations.</span></span> <span data-ttu-id="95097-145">We moeten eerst toocopy Hallo bestanden lokaal via Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="95097-145">First, we need toocopy hello files locally using hello following commands:</span></span>

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    <span data-ttu-id="95097-146">Met deze opdracht kopieën Hallo tooa uitvoergegevensbestand met de naam **recommendations.txt** in de huidige map Hallo samen met de Hallo film gegevensbestanden worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="95097-146">This command copies hello output data tooa file named **recommendations.txt** in hello current directory, along with hello movie data files.</span></span>

3. <span data-ttu-id="95097-147">Hallo opdracht toocreate een pythonscript dat Hiermee u film namen voor gegevens in de uitvoer van de aanbevelingen Hallo Hallo zoekt volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="95097-147">Use hello following command toocreate a Python script that looks up movie names for hello data in hello recommendations output:</span></span>

    ```bash
    nano show_recommendations.py
    ```

    <span data-ttu-id="95097-148">Wanneer Hallo editor wordt geopend, gebruikt u Hallo tekst als Hallo inhoud van Hallo-bestand te volgen:</span><span class="sxs-lookup"><span data-stu-id="95097-148">When hello editor opens, use hello following text as hello contents of hello file:</span></span>

   ```python
   #!/usr/bin/env python

   import sys

   if len(sys.argv) != 5:
        print "Arguments: userId userDataFilename movieFilename recommendationFilename"
        sys.exit(1)

   userId, userDataFilename, movieFilename, recommendationFilename = sys.argv[1:]

   print "Reading Movies Descriptions"
   movieFile = open(movieFilename)
   movieById = {}
   for line in movieFile:
       tokens = line.split("|")
       movieById[tokens[0]] = tokens[1:]
   movieFile.close()

   print "Reading Rated Movies"
   userDataFile = open(userDataFilename)
   ratedMovieIds = []
   for line in userDataFile:
       tokens = line.split("\t")
       if tokens[0] == userId:
           ratedMovieIds.append((tokens[1],tokens[2]))
   userDataFile.close()

   print "Reading Recommendations"
   recommendationFile = open(recommendationFilename)
   recommendations = []
   for line in recommendationFile:
       tokens = line.split("\t")
       if tokens[0] == userId:
           movieIdAndScores = tokens[1].strip("[]\n").split(",")
           recommendations = [ movieIdAndScore.split(":") for movieIdAndScore in movieIdAndScores ]
           break
   recommendationFile.close()

   print "Rated Movies"
   print "------------------------"
   for movieId, rating in ratedMovieIds:
       print "%s, rating=%s" % (movieById[movieId][0], rating)
   print "------------------------"

   print "Recommended Movies"
   print "------------------------"
   for movieId, score in recommendations:
       print "%s, score=%s" % (movieById[movieId][0], score)
   print "------------------------"
   ```

    <span data-ttu-id="95097-149">Druk op **Ctrl X**, **Y**, en tot slot **Enter** toosave Hallo gegevens.</span><span class="sxs-lookup"><span data-stu-id="95097-149">Press **Ctrl-X**, **Y**, and finally **Enter** toosave hello data.</span></span>

4. <span data-ttu-id="95097-150">Hallo pythonscript uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="95097-150">Run hello Python script.</span></span> <span data-ttu-id="95097-151">Hallo volgende opdracht wordt ervan uitgegaan dat u in het Hallo-directory waar alle Hallo-bestanden zijn gedownload:</span><span class="sxs-lookup"><span data-stu-id="95097-151">hello following command assumes you are in hello directory where all hello files were downloaded:</span></span>

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    <span data-ttu-id="95097-152">Met deze opdracht wordt bekeken Hallo aanbevelingen gegenereerd voor de gebruiker-ID 4.</span><span class="sxs-lookup"><span data-stu-id="95097-152">This command looks at hello recommendations generated for user ID 4.</span></span>

    * <span data-ttu-id="95097-153">Hallo **gebruiker ratings.txt** bestand is gebruikte tooretrieve films die zijn beoordeeld.</span><span class="sxs-lookup"><span data-stu-id="95097-153">hello **user-ratings.txt** file is used tooretrieve movies that have been rated.</span></span>

    * <span data-ttu-id="95097-154">Hallo **moviedb.txt** bestand gebruikte tooretrieve Hallo namen van Hallo films is.</span><span class="sxs-lookup"><span data-stu-id="95097-154">hello **moviedb.txt** file is used tooretrieve hello names of hello movies.</span></span>

    * <span data-ttu-id="95097-155">Hallo **recommendations.txt** gebruikte tooretrieve hello filmaanbevelingen voor deze gebruiker is.</span><span class="sxs-lookup"><span data-stu-id="95097-155">hello **recommendations.txt** is used tooretrieve hello movie recommendations for this user.</span></span>

     <span data-ttu-id="95097-156">Hallo uitvoer van deze opdracht is vergelijkbaar toohello de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="95097-156">hello output from this command is similar toohello following text:</span></span>

        <span data-ttu-id="95097-157">Fraudewaarschuwing in Tibet (1997) score = 5.0 Indiana Jones en Hallo laatste Crusade (1989) score = 5.0 Jaws (1975) score 5.0 = zin en mee (1995) score 5.0 = onafhankelijkheid dag (ID4) (1996) score = 5.0 mijn beste vriend Wedding (1997), beoordelen 5.0 = Jerry Maguire (1996 ), score 5.0 = Scream 2 (1997) score = 5.0 tijd tooKill, een (1996) score = 5.0</span><span class="sxs-lookup"><span data-stu-id="95097-157">Seven Years in Tibet (1997), score=5.0   Indiana Jones and hello Last Crusade (1989), score=5.0   Jaws (1975), score=5.0   Sense and Sensibility (1995), score=5.0   Independence Day (ID4) (1996), score=5.0   My Best Friend's Wedding (1997), score=5.0   Jerry Maguire (1996), score=5.0   Scream 2 (1997), score=5.0   Time tooKill, A (1996), score=5.0</span></span>

## <a name="delete-temporary-data"></a><span data-ttu-id="95097-158">Tijdelijke gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="95097-158">Delete temporary data</span></span>

<span data-ttu-id="95097-159">Mahout taken verwijderd tijdelijke gegevens die zijn gemaakt tijdens het verwerken van Hallo-taak niet.</span><span class="sxs-lookup"><span data-stu-id="95097-159">Mahout jobs do not remove temporary data that is created while processing hello job.</span></span> <span data-ttu-id="95097-160">Hallo `--tempDir` parameter wordt opgegeven in Hallo voorbeeld taak tooisolate Hallo tijdelijke bestanden naar een specifiek pad voor eenvoudig verwijderen.</span><span class="sxs-lookup"><span data-stu-id="95097-160">hello `--tempDir` parameter is specified in hello example job tooisolate hello temporary files into a specific path for easy deletion.</span></span> <span data-ttu-id="95097-161">tooremove hello tijdelijke bestanden, Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="95097-161">tooremove hello temp files, use hello following command:</span></span>

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> <span data-ttu-id="95097-162">Als u opnieuw toorun Hallo opdracht wilt, moet u ook Hallo uitvoermap verwijderen.</span><span class="sxs-lookup"><span data-stu-id="95097-162">If you want toorun hello command again, you must also delete hello output directory.</span></span> <span data-ttu-id="95097-163">Deze map Hallo toodelete volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="95097-163">Use hello following toodelete this directory:</span></span>
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a><span data-ttu-id="95097-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="95097-164">Next steps</span></span>

<span data-ttu-id="95097-165">U hebt geleerd hoe toouse Mahout, andere manieren om te werken met gegevens in HDInsight detecteren:</span><span class="sxs-lookup"><span data-stu-id="95097-165">Now that you have learned how toouse Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="95097-166">Hive met HDInsight</span><span class="sxs-lookup"><span data-stu-id="95097-166">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="95097-167">Pig met HDInsight</span><span class="sxs-lookup"><span data-stu-id="95097-167">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="95097-168">MapReduce met HDInsight</span><span class="sxs-lookup"><span data-stu-id="95097-168">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[build]: http://mahout.apache.org/developers/buildingmahout.html
[movielens]: http://grouplens.org/datasets/movielens/
[100k]: http://files.grouplens.org/datasets/movielens/ml-100k.zip
[getstarted]: hdinsight-hadoop-linux-tutorial-get-started.md
[upload]: hdinsight-upload-data.md
[ml]: http://en.wikipedia.org/wiki/Machine_learning
[forest]: http://en.wikipedia.org/wiki/Random_forest
[enableremote]: ./media/hdinsight-mahout/enableremote.png
[connect]: ./media/hdinsight-mahout/connect.png
[hadoopcli]: ./media/hdinsight-mahout/hadoopcli.png
[tools]: https://github.com/Blackmist/hdinsight-tools
