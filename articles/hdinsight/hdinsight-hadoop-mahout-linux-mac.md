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
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-linux-based-hadoop-in-hdinsight-ssh"></a>Filmaanbevelingen genereren met behulp van Apache Mahout met Hadoop op basis van Linux in HDInsight (SSH)

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

Meer informatie over hoe toouse hello [Apache Mahout](http://mahout.apache.org) machine learning-bibliotheek met Azure HDInsight toogenerate filmaanbevelingen.

Mahout is een [machine learning] [ ml] -bibliotheek voor Apache Hadoop. Mahout bevat algoritmen voor het verwerken van gegevens, zoals filteren, classificatie en clustering. In dit artikel gebruikt u een aanbeveling engine toogenerate filmaanbevelingen die zijn gebaseerd op films je vrienden hebt gezien.

## <a name="prerequisites"></a>Vereisten

* Een Linux gebaseerde HDInsight-cluster. Zie voor meer informatie over het maken van een [aan de slag met Hadoop op basis van Linux in HDInsight][getstarted].

> [!IMPORTANT]
> Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

* Een SSH-client. Zie voor meer informatie, Hallo [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.

## <a name="mahout-versioning"></a>Mahout versiebeheer

Zie voor meer informatie over het Hallo-versie van Mahout in HDInsight [HDInsight versies en Hadoop-onderdelen](hdinsight-component-versioning.md).

## <a name="recommendations"></a>Understanding aanbevelingen

Een van Hallo-functies die wordt geleverd door Mahout is een aanbeveling-engine. Deze engine accepteert gegevens in de indeling van Hallo `userID`, `itemId`, en `prefValue` (Hallo voorkeur voor Hallo item). Mahout kunt uitvoeren, mede exemplaar analysis toodetermine: *gebruikers die een voorkeur voor een item hebben ook een voorkeur voor deze andere items hebt*. Mahout vervolgens gebruikers met dergelijke-item-voorkeuren gebruikte toomake aanbevelingen kunnen worden bepaald.

Hallo is volgende werkstroom een voorbeeld van een vereenvoudigde die gebruikmaakt van filmgegevens:

* **Mede exemplaar**: Jan Els en Bob alle bevallen *Star Wars*, *Empire ontvangen terug Hallo*, en *Return Hallo Jedi*. Mahout bepaalt dat gebruikers die als een van deze films ook graag twee andere Hallo.

* **Mede exemplaar**: Bob en Els ook bevallen *Hallo Phantom Menace*, *een aanval op Hallo klonen*, en *Revenge Hallo Sith*. Mahout bepaalt dat gebruikers die ook de vorige drie films Hallo bevallen, zoals deze drie films.

* **Gelijkenis aanbeveling**: omdat Jan bevallen Hallo eerste drie films, Mahout wordt bekeken films die anderen met vergelijkbare voorkeuren bevallen, maar Joe heeft geen gevolgde (bevallen/geclassificeerd). In dit geval Mahout raadt *Hallo Phantom Menace*, *een aanval op Hallo klonen*, en *Revenge Hallo Sith*.

### <a name="understanding-hello-data"></a>Understanding Hallo gegevens

Gemakkelijk [GroupLens Research] [ movielens] biedt classificatie gegevens voor films in een indeling die compatibel is met Mahout. Deze gegevens zijn beschikbaar op het cluster standaard opslag op `/HdiSamples/HdiSamples/MahoutMovieData`.

Er zijn twee bestanden: `moviedb.txt` en `user-ratings.txt`. Hallo gebruiker ratings.txt bestand wordt gebruikt tijdens de analyse, terwijl moviedb.txt gebruikte tooprovide gebruiksvriendelijke tekstinformatie Hallo resultaten van Hallo analyse om weer te geven.

Hallo gegevens in gebruiker ratings.txt heeft een structuur van `userID`, `movieID`, `userRating`, en `timestamp`, die vertellen hoe maximaal elke gebruiker een film beoordeeld. Hier volgt een voorbeeld van Hallo gegevens:

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

## <a name="run-hello-analysis"></a>Hallo-analyse uitvoeren

Gebruik van een SSH-verbinding toohello-cluster Hallo opdracht toorun Hallo aanbeveling taak te volgen:

```bash
mahout recommenditembased -s SIMILARITY_COOCCURRENCE -i /HdiSamples/HdiSamples/MahoutMovieData/user-ratings.txt -o /example/data/mahoutout --tempDir /temp/mahouttemp
```

> [!NOTE]
> Hallo taak duurt enkele minuten toocomplete, en mogelijk meerdere MapReduce-taken worden uitgevoerd.

## <a name="view-hello-output"></a>Hallo-uitvoer weergeven

1. Zodra het Hallo-taak is voltooid, gebruikt u Hallo opdrachtuitvoer tooview Hallo gegenereerd na:

    ```bash
    hdfs dfs -text /example/data/mahoutout/part-r-00000
    ```

    Hallo-uitvoer ziet er als volgt uit:

        1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
        2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
        3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
        4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

    de eerste kolom Hallo is Hallo `userID`. waarden in Hallo ' [' en ']' zijn `movieId`:`recommendationScore`.

2. U kunt Hallo-uitvoer, samen met de Hallo moviedb.txt, tooprovide meer informatie op Hallo aanbevelingen. We moeten eerst toocopy Hallo bestanden lokaal via Hallo volgende opdrachten:

    ```bash
    hdfs dfs -get /example/data/mahoutout/part-r-00000 recommendations.txt
    hdfs dfs -get /HdiSamples/HdiSamples/MahoutMovieData/* .
    ```

    Met deze opdracht kopieën Hallo tooa uitvoergegevensbestand met de naam **recommendations.txt** in de huidige map Hallo samen met de Hallo film gegevensbestanden worden opgeslagen.

3. Hallo opdracht toocreate een pythonscript dat Hiermee u film namen voor gegevens in de uitvoer van de aanbevelingen Hallo Hallo zoekt volgende gebruiken:

    ```bash
    nano show_recommendations.py
    ```

    Wanneer Hallo editor wordt geopend, gebruikt u Hallo tekst als Hallo inhoud van Hallo-bestand te volgen:

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

    Druk op **Ctrl X**, **Y**, en tot slot **Enter** toosave Hallo gegevens.

4. Hallo pythonscript uitvoeren. Hallo volgende opdracht wordt ervan uitgegaan dat u in het Hallo-directory waar alle Hallo-bestanden zijn gedownload:

    ```bash
    python show_recommendations.py 4 user-ratings.txt moviedb.txt recommendations.txt
    ```

    Met deze opdracht wordt bekeken Hallo aanbevelingen gegenereerd voor de gebruiker-ID 4.

    * Hallo **gebruiker ratings.txt** bestand is gebruikte tooretrieve films die zijn beoordeeld.

    * Hallo **moviedb.txt** bestand gebruikte tooretrieve Hallo namen van Hallo films is.

    * Hallo **recommendations.txt** gebruikte tooretrieve hello filmaanbevelingen voor deze gebruiker is.

     Hallo uitvoer van deze opdracht is vergelijkbaar toohello de volgende tekst:

        Fraudewaarschuwing in Tibet (1997) score = 5.0 Indiana Jones en Hallo laatste Crusade (1989) score = 5.0 Jaws (1975) score 5.0 = zin en mee (1995) score 5.0 = onafhankelijkheid dag (ID4) (1996) score = 5.0 mijn beste vriend Wedding (1997), beoordelen 5.0 = Jerry Maguire (1996 ), score 5.0 = Scream 2 (1997) score = 5.0 tijd tooKill, een (1996) score = 5.0

## <a name="delete-temporary-data"></a>Tijdelijke gegevens verwijderen

Mahout taken verwijderd tijdelijke gegevens die zijn gemaakt tijdens het verwerken van Hallo-taak niet. Hallo `--tempDir` parameter wordt opgegeven in Hallo voorbeeld taak tooisolate Hallo tijdelijke bestanden naar een specifiek pad voor eenvoudig verwijderen. tooremove hello tijdelijke bestanden, Hallo volgende opdracht gebruiken:

```bash
hdfs dfs -rm -f -r /temp/mahouttemp
```

> [!WARNING]
> Als u opnieuw toorun Hallo opdracht wilt, moet u ook Hallo uitvoermap verwijderen. Deze map Hallo toodelete volgende gebruiken:
>
> `hdfs dfs -rm -f -r /example/data/mahoutout`


## <a name="next-steps"></a>Volgende stappen

U hebt geleerd hoe toouse Mahout, andere manieren om te werken met gegevens in HDInsight detecteren:

* [Hive met HDInsight](hdinsight-use-hive.md)
* [Pig met HDInsight](hdinsight-use-pig.md)
* [MapReduce met HDInsight](hdinsight-use-mapreduce.md)

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
