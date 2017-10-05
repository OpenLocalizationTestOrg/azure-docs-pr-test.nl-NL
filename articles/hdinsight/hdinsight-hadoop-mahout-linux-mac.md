---
title: Genereren met Mahout en HDInsight (SSH) - Azure aanbevelingen | Microsoft Docs
description: Informatie over het gebruik van de Apache Mahout-machine learning-bibliotheek voor het genereren van filmaanbevelingen met HDInsight (Hadoop).
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
ms.openlocfilehash: 28450d72f19a5467d88bc787d11f6c37c5afbf9a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a><span data-ttu-id="4d795-103">Filmaanbevelingen genereren met behulp van Apache Mahout met Hadoop op basis van Linux in HDInsight (SSH)</span><span class="sxs-lookup"><span data-stu-id="4d795-103">Generate movie recommendations by using Apache Mahout with Linux-based Hadoop in HDInsight (SSH)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="4d795-104">Meer informatie over het gebruik van de [Apache Mahout](http://mahout.apache.org) machine learning-bibliotheek met Azure HDInsight filmaanbevelingen genereren.</span><span class="sxs-lookup"><span data-stu-id="4d795-104">Learn how to use the [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight to generate movie recommendations.</span></span>

<span data-ttu-id="4d795-105">Mahout is een [machine learning] [ ml] -bibliotheek voor Apache Hadoop.</span><span class="sxs-lookup"><span data-stu-id="4d795-105">Mahout is a [machine learning][ml] library for Apache Hadoop.</span></span> <span data-ttu-id="4d795-106">Mahout bevat algoritmen voor het verwerken van gegevens, zoals filteren, classificatie en clustering.</span><span class="sxs-lookup"><span data-stu-id="4d795-106">Mahout contains algorithms for processing data, such as filtering, classification, and clustering.</span></span> <span data-ttu-id="4d795-107">In dit artikel kunt u een aanbeveling engine filmaanbevelingen die zijn gebaseerd op je vrienden hebt gezien films genereren.</span><span class="sxs-lookup"><span data-stu-id="4d795-107">In this article, you use a recommendation engine to generate movie recommendations that are based on movies your friends have seen.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d795-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4d795-108">Prerequisites</span></span>

* <span data-ttu-id="4d795-109">Een Linux gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="4d795-109">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="4d795-110">Zie voor meer informatie over het maken van een [aan de slag met Hadoop op basis van Linux in HDInsight][getstarted].</span><span class="sxs-lookup"><span data-stu-id="4d795-110">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4d795-111">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="4d795-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4d795-112">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4d795-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="4d795-113">Een SSH-client.</span><span class="sxs-lookup"><span data-stu-id="4d795-113">An SSH client.</span></span> <span data-ttu-id="4d795-114">Zie het document [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4d795-114">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

## <a name="mahout-versioning"></a><span data-ttu-id="4d795-115">Mahout versiebeheer</span><span class="sxs-lookup"><span data-stu-id="4d795-115">Mahout versioning</span></span>

<span data-ttu-id="4d795-116">Zie voor meer informatie over de versie van Mahout in HDInsight [HDInsight versies en Hadoop-onderdelen](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="4d795-116">For more information about the version of Mahout in HDInsight, see [HDInsight versions and Hadoop components](hdinsight-component-versioning.md).</span></span>

## <span data-ttu-id="4d795-117"><a name="recommendations"></a>Understanding aanbevelingen</span><span class="sxs-lookup"><span data-stu-id="4d795-117"><a name="recommendations"></a>Understanding recommendations</span></span>

<span data-ttu-id="4d795-118">Een van de functies die wordt geleverd door Mahout is een aanbeveling-engine.</span><span class="sxs-lookup"><span data-stu-id="4d795-118">One of the functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="4d795-119">Deze engine accepteert gegevens in de indeling van `userID`, `itemId`, en `prefValue` (de voorkeur voor het item).</span><span class="sxs-lookup"><span data-stu-id="4d795-119">This engine accepts data in the format of `userID`, `itemId`, and `prefValue` (the preference for the item).</span></span> <span data-ttu-id="4d795-120">Mahout kunt uitvoeren, analyse van CO-exemplaar om te bepalen: *gebruikers die een voorkeur voor een item hebben ook een voorkeur voor deze andere items hebt*.</span><span class="sxs-lookup"><span data-stu-id="4d795-120">Mahout can then perform co-occurance analysis to determine: *users who have a preference for an item also have a preference for these other items*.</span></span> <span data-ttu-id="4d795-121">Mahout bepaalt vervolgens gebruikers met dergelijke-item voorkeuren, die kunnen worden gebruikt om aanbevelingen te doen.</span><span class="sxs-lookup"><span data-stu-id="4d795-121">Mahout then determines users with like-item preferences, which can be used to make recommendations.</span></span>

<span data-ttu-id="4d795-122">De volgende werkstroom is een voorbeeld van een vereenvoudigde die gebruikmaakt van filmgegevens:</span><span class="sxs-lookup"><span data-stu-id="4d795-122">The following workflow is a simplified example that uses movie data:</span></span>

* <span data-ttu-id="4d795-123">**Mede exemplaar**: Jan Els en Bob alle bevallen *Star Wars*, *terug ontvangen in de Empire*, en *Return van de Jedi*.</span><span class="sxs-lookup"><span data-stu-id="4d795-123">**Co-occurance**: Joe, Alice, and Bob all liked *Star Wars*, *The Empire Strikes Back*, and *Return of the Jedi*.</span></span> <span data-ttu-id="4d795-124">Mahout bepaalt dat gebruikers die een van deze films ook de andere twee zoals.</span><span class="sxs-lookup"><span data-stu-id="4d795-124">Mahout determines that users who like any one of these movies also like the other two.</span></span>

* <span data-ttu-id="4d795-125">**Mede exemplaar**: Bob en Els ook bevallen *de Phantom Menace*, *een aanval van de klonen*, en *Revenge van de Sith*.</span><span class="sxs-lookup"><span data-stu-id="4d795-125">**Co-occurance**: Bob and Alice also liked *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span> <span data-ttu-id="4d795-126">Mahout bepaalt dat gebruikers die de vorige drie films ook bevallen, zoals deze drie films.</span><span class="sxs-lookup"><span data-stu-id="4d795-126">Mahout determines that users who liked the previous three movies also like these three movies.</span></span>

* <span data-ttu-id="4d795-127">**Gelijkenis aanbeveling**: Jan omdat de eerste drie films bevallen, Mahout wordt bekeken films die anderen met vergelijkbare voorkeuren bevallen, maar Joe heeft geen gevolgde (bevallen/geclassificeerd).</span><span class="sxs-lookup"><span data-stu-id="4d795-127">**Similarity recommendation**: Because Joe liked the first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="4d795-128">In dit geval Mahout raadt *de Phantom Menace*, *een aanval van de klonen*, en *Revenge van de Sith*.</span><span class="sxs-lookup"><span data-stu-id="4d795-128">In this case, Mahout recommends *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span>

### <a name="understanding-the-data"></a><span data-ttu-id="4d795-129">Wat zijn de gegevens?</span><span class="sxs-lookup"><span data-stu-id="4d795-129">Understanding the data</span></span>

<span data-ttu-id="4d795-130">Gemakkelijk [GroupLens Research] [ movielens] biedt classificatie gegevens voor films in een indeling die compatibel is met Mahout.</span><span class="sxs-lookup"><span data-stu-id="4d795-130">Conveniently, [GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="4d795-131">Deze gegevens zijn beschikbaar op het cluster standaard opslag op `/HdiSamples/HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="4d795-131">This data is available on your cluster's default storage at `/HdiSamples/HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="4d795-132">Er zijn twee bestanden: `moviedb.txt` en `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="4d795-132">There are two files, `moviedb.txt` and `user-ratings.txt`.</span></span> <span data-ttu-id="4d795-133">De gebruiker ratings.txt-bestand wordt gebruikt tijdens de analyse, terwijl moviedb.txt gebruiksvriendelijke om tekstinformatie te geven bij het weergeven van de resultaten van de analyse wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4d795-133">The user-ratings.txt file is used during analysis, while moviedb.txt is used to provide user-friendly text information when displaying the results of the analysis.</span></span>

<span data-ttu-id="4d795-134">De gegevens in gebruiker ratings.txt heeft een structuur van `userID`, `movieID`, `userRating`, en `timestamp`, die vertellen hoe maximaal elke gebruiker een film beoordeeld.</span><span class="sxs-lookup"><span data-stu-id="4d795-134">The data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="4d795-135">Hier volgt een voorbeeld van de gegevens:</span><span class="sxs-lookup"><span data-stu-id="4d795-135">Here is an example of the data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-the-analysis"></a><span data-ttu-id="4d795-136">De analyse uitvoeren</span><span class="sxs-lookup"><span data-stu-id="4d795-136">Run the analysis</span></span>

<span data-ttu-id="4d795-137">Gebruik de volgende opdracht om uit te voeren de aanbeveling van een SSH-verbinding met het cluster:</span><span class="sxs-lookup"><span data-stu-id="4d795-137">From an SSH connection to the cluster, use the following command to run the recommendation job:</span></span>

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> <span data-ttu-id="4d795-138">De taak duurt enkele minuten in beslag, en mogelijk meerdere MapReduce-taken worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4d795-138">The job may take several minutes to complete, and may run multiple MapReduce jobs.</span></span>

## <a name="view-the-output"></a><span data-ttu-id="4d795-139">De uitvoer weergeven</span><span class="sxs-lookup"><span data-stu-id="4d795-139">View the output</span></span>

1. <span data-ttu-id="4d795-140">Zodra de taak is voltooid, gebruikt u de volgende opdracht om weer te geven van de gegenereerde uitvoer:</span><span class="sxs-lookup"><span data-stu-id="4d795-140">Once the job completes, use the following command to view the generated output:</span></span>

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    <span data-ttu-id="4d795-141">De uitvoer ziet er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="4d795-141">The output appears as follows:</span></span>

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    <span data-ttu-id="4d795-142">De eerste kolom is de `userID`.</span><span class="sxs-lookup"><span data-stu-id="4d795-142">The first column is the `userID`.</span></span> <span data-ttu-id="4d795-143">De waarden in ' [' en ']' zijn `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="4d795-143">The values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

2. <span data-ttu-id="4d795-144">U kunt de uitvoer, samen met de moviedb.txt bieden meer informatie over de aanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="4d795-144">You can use the output, along with the moviedb.txt, to provide more information on the recommendations.</span></span> <span data-ttu-id="4d795-145">Eerst moet de bestanden kopiëren lokaal met de volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="4d795-145">First, we need to copy the files locally using the following commands:</span></span>

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    <span data-ttu-id="4d795-146">Met deze opdracht wordt de uitvoergegevens gekopieerd naar een bestand met de naam **recommendations.txt** in de huidige map, samen met de gegevensbestanden film.</span><span class="sxs-lookup"><span data-stu-id="4d795-146">This command copies the output data to a file named **recommendations.txt** in the current directory, along with the movie data files.</span></span>

3. <span data-ttu-id="4d795-147">Gebruik de volgende opdracht voor het maken van een pythonscript dat Hiermee u film namen voor de gegevens in de uitvoer van de aanbevelingen zoekt:</span><span class="sxs-lookup"><span data-stu-id="4d795-147">Use the following command to create a Python script that looks up movie names for the data in the recommendations output:</span></span>

    ```bash
    nano show_recommendations.py
    ```

    <span data-ttu-id="4d795-148">Wanneer de editor wordt geopend, gebruikt u de volgende tekst als de inhoud van het bestand:</span><span class="sxs-lookup"><span data-stu-id="4d795-148">When the editor opens, use the following text as the contents of the file:</span></span>

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

    <span data-ttu-id="4d795-149">Druk op **Ctrl X**, **Y**, en tot slot **Enter** gegevens opslaan.</span><span class="sxs-lookup"><span data-stu-id="4d795-149">Press **Ctrl-X**, **Y**, and finally **Enter** to save the data.</span></span>

4. <span data-ttu-id="4d795-150">Het Python-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="4d795-150">Run the Python script.</span></span> <span data-ttu-id="4d795-151">De volgende opdracht wordt ervan uitgegaan dat u in de map waar alle bestanden zijn gedownload:</span><span class="sxs-lookup"><span data-stu-id="4d795-151">The following command assumes you are in the directory where all the files were downloaded:</span></span>

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    <span data-ttu-id="4d795-152">Met deze opdracht wordt de aanbevelingen die worden gegenereerd voor de gebruiker-ID 4 bekeken.</span><span class="sxs-lookup"><span data-stu-id="4d795-152">This command looks at the recommendations generated for user ID 4.</span></span>

    * <span data-ttu-id="4d795-153">De **gebruiker ratings.txt** bestand wordt gebruikt voor het ophalen van films die zijn beoordeeld.</span><span class="sxs-lookup"><span data-stu-id="4d795-153">The **user-ratings.txt** file is used to retrieve movies that have been rated.</span></span>

    * <span data-ttu-id="4d795-154">De **moviedb.txt** bestand wordt gebruikt voor het ophalen van de namen van de films.</span><span class="sxs-lookup"><span data-stu-id="4d795-154">The **moviedb.txt** file is used to retrieve the names of the movies.</span></span>

    * <span data-ttu-id="4d795-155">De **recommendations.txt** wordt gebruikt voor het ophalen van de filmaanbevelingen voor deze gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4d795-155">The **recommendations.txt** is used to retrieve the movie recommendations for this user.</span></span>

     <span data-ttu-id="4d795-156">De uitvoer van deze opdracht is vergelijkbaar met de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="4d795-156">The output from this command is similar to the following text:</span></span>

        <span data-ttu-id="4d795-157">Fraudewaarschuwing in Tibet (1997), beoordelen 5.0 = Indiana Jones en de laatste Crusade (1989) score = 5.0 Jaws (1975) score = 5.0 zin en mee (1995) score = 5.0 onafhankelijkheid dag (ID4) (1996) score = 5.0 mijn beste vriend Wedding (1997), beoordelen 5.0 = Jerry Maguire (1996) score 5.0 = Scream 2 (1997) score = 5.0 tijd Kill, een (1996) score = 5.0</span><span class="sxs-lookup"><span data-stu-id="4d795-157">Seven Years in Tibet (1997), score=5.0   Indiana Jones and the Last Crusade (1989), score=5.0   Jaws (1975), score=5.0   Sense and Sensibility (1995), score=5.0   Independence Day (ID4) (1996), score=5.0   My Best Friend's Wedding (1997), score=5.0   Jerry Maguire (1996), score=5.0   Scream 2 (1997), score=5.0   Time to Kill, A (1996), score=5.0</span></span>

## <a name="delete-temporary-data"></a><span data-ttu-id="4d795-158">Tijdelijke gegevens verwijderen</span><span class="sxs-lookup"><span data-stu-id="4d795-158">Delete temporary data</span></span>

<span data-ttu-id="4d795-159">Mahout taken verwijderd tijdelijke gegevens die zijn gemaakt tijdens het verwerken van de taak niet.</span><span class="sxs-lookup"><span data-stu-id="4d795-159">Mahout jobs do not remove temporary data that is created while processing the job.</span></span> <span data-ttu-id="4d795-160">De `--tempDir` parameter wordt opgegeven in de voorbeeld-taak voor het isoleren van de tijdelijke bestanden in een specifiek pad voor eenvoudig verwijderen.</span><span class="sxs-lookup"><span data-stu-id="4d795-160">The `--tempDir` parameter is specified in the example job to isolate the temporary files into a specific path for easy deletion.</span></span> <span data-ttu-id="4d795-161">Gebruik de volgende opdracht voor het verwijderen van de tijdelijke bestanden:</span><span class="sxs-lookup"><span data-stu-id="4d795-161">To remove the temp files, use the following command:</span></span>

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> <span data-ttu-id="4d795-162">Als u de opdracht opnieuw uitvoeren wilt, moet u ook de uitvoermap verwijderen.</span><span class="sxs-lookup"><span data-stu-id="4d795-162">If you want to run the command again, you must also delete the output directory.</span></span> <span data-ttu-id="4d795-163">Gebruik de volgende om deze map te verwijderen:</span><span class="sxs-lookup"><span data-stu-id="4d795-163">Use the following to delete this directory:</span></span>
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a><span data-ttu-id="4d795-164">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4d795-164">Next steps</span></span>

<span data-ttu-id="4d795-165">U hebt geleerd hoe u Mahout, detectie van andere manieren van het werken met gegevens in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="4d795-165">Now that you have learned how to use Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="4d795-166">Hive met HDInsight</span><span class="sxs-lookup"><span data-stu-id="4d795-166">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="4d795-167">Pig met HDInsight</span><span class="sxs-lookup"><span data-stu-id="4d795-167">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="4d795-168">MapReduce met HDInsight</span><span class="sxs-lookup"><span data-stu-id="4d795-168">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

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
