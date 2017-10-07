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
# <a name="run-hello-mapreduce-examples-included-in-hdinsight"></a>Hallo MapReduce voorbeelden is opgenomen in HDInsight uitvoeren

[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

Meer informatie over hoe toorun hello MapReduce voorbeelden opgenomen met Hadoop op HDInsight.

## <a name="prerequisites"></a>Vereisten

* **Een HDInsight-cluster**: Zie [aan de slag met Hadoop met Hive in HDInsight op Linux](hdinsight-hadoop-linux-tutorial-get-started.md)

    > [!IMPORTANT]
    > Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

* **Een SSH-client**: Zie voor meer informatie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a name="hello-mapreduce-examples"></a>Hallo MapReduce-voorbeelden

**Locatie**: Hallo voorbeelden bevinden zich op HDInsight-cluster op Hallo `/usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar`.

**Inhoud**: Hallo volgen voorbeelden zijn opgenomen in dit archief:

* `aggregatewordcount`: Er is een statistische functie gebaseerd mapreduce-programma dat Hallo woorden in Hallo invoerbestanden geteld.
* `aggregatewordhist`: Er is een statistische functie gebaseerd mapreduce-programma dat wordt berekend Hallo histogram Hallo woorden in Hallo invoerbestanden.
* `bbp`: Een mapreduce-programma dat gebruikmaakt van Bailey-Borwein-Plouffe toocompute exacte cijfers van Pi.
* `dbcount`: Er is een voorbeeld van de taak die Hallo pageview logboeken opgeslagen in een database telt.
* `distbbp`: Een mapreduce-programma dat gebruikmaakt van een formule toocompute BBP type bits exacte van Pi.
* `grep`: Een mapreduce-programma dat wordt geteld Hallo komt overeen met van een reguliere expressie in de Hallo-invoer.
* `join`: Een taak die een join uitvoert via gesorteerd, evenveel gepartitioneerd gegevenssets.
* `multifilewc`: Een taak die woorden uit verschillende bestanden telt.
* `pentomino`: Een mapreduce-tegel elementlay programma toofind oplossingen toopentomino problemen.
* `pi`: Een mapreduce-programma dat u maakt een schatting van Pi met behulp van een quasi Monte Carlo-methode.
* `randomtextwriter`: Een mapreduce-programma dat 10 GB met willekeurige tekstgegevens per knooppunt schrijft.
* `randomwriter`: Een mapreduce-programma dat 10 GB willekeurige gegevens per knooppunt schrijft.
* `secondarysort`: Er is een voorbeeld van een secundaire sorteren toohello definiëren verminderen fase.
* `sort`: Een mapreduce-programma dat Hallo gegevens geschreven door Hallo willekeurige writer gesorteerd.
* `sudoku`: Een sudoku Solver '.
* `teragen`: De gegevens voor Hallo terasort genereren.
* `terasort`: Hallo terasort worden uitgevoerd.
* `teravalidate`: De resultaten van terasort controleren.
* `wordcount`: Een mapreduce-programma dat Hallo woorden in Hallo invoerbestanden geteld.
* `wordmean`: Een mapreduce-programma dat Hallo gemiddelde duur van Hallo woorden in Hallo invoerbestanden telt.
* `wordmedian`: Een mapreduce-programma dat Hallo mediaan lengte van Hallo woorden in Hallo invoerbestanden telt.
* `wordstandarddeviation`: Een mapreduce-programma dat Hallo standaardafwijking van Hallo lengte van Hallo woorden in Hallo invoerbestanden telt.

**Broncode**: broncode voor deze voorbeelden is opgenomen op HDInsight-cluster op Hallo `/usr/hdp/2.2.4.9-1/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples`.

> [!NOTE]
> Hallo `2.2.4.9-1` in Hallo pad Hallo-versie van Hallo Hortonworks Data Platform voor Hallo HDInsight-cluster is en kunnen afwijken voor uw cluster.

## <a name="run-hello-wordcount-example"></a>Hallo wordcount-voorbeeld uitvoeren

1. Verbinding maken via SSH tooHDInsight. Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

2. Van Hallo `username@#######:~$` gevraagd, gebruikt u Hallo Voorbeeldopdrachten toolist hello te volgen:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar
    ```

    Met deze opdracht genereert Hallo-lijst van voorbeeld van de vorige sectie Hallo van dit document.

3. Gebruik hello opdracht tooget help op een specifieke voorbeeld te volgen. In dit geval Hallo **wordcount** voorbeeld:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount
    ```

    U ontvangt Hallo volgende bericht:

        Usage: wordcount <in> [<in>...] <out>

    Dit bericht geeft aan dat u verschillende invoerpaden voor Hallo brondocumenten bieden kunt. Hallo uiteindelijke pad is waar Hallo uitvoer (aantal woorden in Hallo brondocumenten) wordt opgeslagen.

4. Hallo toocount na alle woorden in Hallo notitieblokken van Leonardo Da Vinci, die beschikbaar worden gesteld als voorbeeldgegevens met uw cluster gebruiken:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/davinciwordcount
    ```

    Invoer voor deze taak wordt gelezen uit `/example/data/gutenberg/davinci.txt`. Uitvoer voor dit voorbeeld wordt opgeslagen in `/example/data/davinciwordcount`. Beide paden bevinden zich op standaard opslag voor Hallo-cluster niet Hallo het lokale bestandssysteem.

   > [!NOTE]
   > Zoals beschreven in de help van Hallo voor Hallo wordcount-voorbeeld, kunt u ook meerdere invoerbestanden opgeven. Bijvoorbeeld: `hadoop jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/gutenberg/ulysses.txt /example/data/twowordcount` woorden in zowel davinci.txt en ulysses.txt geteld.

5. Zodra het Hallo-taak is voltooid, gebruikt u Hallo opdrachtuitvoer tooview hello te volgen:

    ```bash
    hdfs dfs -cat /example/data/davinciwordcount/*
    ```

    Met deze opdracht worden alle bestanden met Hallo uitvoer geproduceerd door Hallo-taak. Hallo uitvoer toohello console worden weergegeven. Hallo uitvoer is vergelijkbaar toohello de volgende tekst:

        zum     1
        zur     1
        zwanzig 1
        zweite  1

    Elke regel vertegenwoordigt een woord en hoe vaak het is opgetreden in Hallo invoergegevens.

## <a name="hello-sudoku-example"></a>Hallo Sudoku voorbeeld

[Sudoku](https://en.wikipedia.org/wiki/Sudoku) is een logische puzzel bestaat uit negen 3 x 3 rasters. Sommige cellen in het raster Hallo hebben aantallen, terwijl andere gebruikers leeg zijn en Hallo doel toosolve voor Hallo lege cellen is. Hallo vorige koppeling meer informatie over het Hallo puzzel heeft, maar Hallo doel van dit voorbeeld is toosolve voor Hallo lege cellen. De invoer moet dus een bestand dat zich in de volgende indeling Hallo:

* Negen rijen van de negen kolommen
* Elke kolom mag een getal of `?` (geeft een lege cel)
* Cellen zijn gescheiden door een spatie

Er is een bepaalde manier tooconstruct Sudoku puzzels; een getal in een kolom of de rij kan niet worden herhaald. Er is een voorbeeld op Hallo HDInsight-cluster die correct is samengesteld. Deze bevindt zich op `/usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta` en bevat de volgende tekst hello:

    8 5 ? 3 9 ? ? ? ?
    ? ? 2 ? ? ? ? ? ?
    ? ? 6 ? 1 ? ? ? 2
    ? ? 4 ? ? 3 ? 5 9
    ? ? 8 9 ? 1 4 ? ?
    3 2 ? 4 ? ? 8 ? ?
    9 ? ? ? 8 ? 5 ? ?
    ? ? ? ? ? ? 2 ? ?
    ? ? ? ? 4 5 ? 7 8

toorun dit probleem voorbeeld Hallo Sudoku bijvoorbeeld gebruik Hallo volgende opdracht:

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar sudoku /usr/hdp/*/hadoop/src/hadoop-mapreduce-project/hadoop-mapreduce-examples/src/main/java/org/apache/hadoop/examples/dancing/puzzle1.dta
```

Hallo-resultaten verschijnen vergelijkbare toohello volgende tekst:

    8 5 1 3 9 2 6 4 7
    4 3 2 6 7 8 1 9 5
    7 9 6 5 1 4 3 8 2
    6 1 4 8 2 3 7 5 9
    5 7 8 9 6 1 4 2 3
    3 2 9 4 5 7 8 1 6
    9 4 7 2 8 6 5 3 1
    1 8 5 7 3 9 2 6 4
    2 6 3 1 4 5 9 7 8

## <a name="pi--example"></a>Voorbeeld van pi (π)

Hallo pi voorbeeld maakt gebruik van een statistische (quasi Monte Carlo) methode tooestimate Hallo waarde van pi. Punten worden in willekeurige volgorde in een vierkant eenheid geplaatst. Hallo vierkante bevat ook een cirkel. Hallo kans dat Hallo punten Hallo cirkel vallen zijn gelijk toohello gebied Hallo cirkel-, pi/4. Hallo-waarde van pi kan worden geschat van Hallo-waarde van 4R. R is Hallo verhouding tussen aantal punten in Hallo cirkel toohello totaal aantal punten die binnen Hallo vierkante Hallo. Hallo groter Hallo voorbeeld van punten gebruikt, Hallo beter Hallo inschatten is.

Hallo opdracht toorun volgende dit voorbeeld gebruiken. Met deze opdracht gebruikt 16-kaarten met 10.000.000 voorbeelden tooestimate Hallo waarde van pi:

```bash
yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar pi 16 10000000
```

Hallo waarde geretourneerd door deze opdracht is vergelijkbaar te**3.14159155000000000000**. Voor verwijzingen zijn hello eerste 10 decimalen van pi 3.1415926535.

## <a name="10-gb-greysort-example"></a>Voorbeeld van 10 GB-Greysort

GraySort is een benchmark-sortering. Hallo-metriek is Hallo sorteren snelheid (TB per minuut) die tijdens het sorteren van grote hoeveelheden gegevens, meestal een 100 TB minimale wordt bereikt.

Dit voorbeeld wordt een matige 10 GB aan gegevens gebruikt, zodat deze kan relatief snel kan worden uitgevoerd. Hallo MapReduce-toepassingen die zijn ontwikkeld door Owen O'Malley en Arun Murthy wordt gebruikt. Deze toepassingen gewonnen Hallo jaarlijkse Algemeen ('daytona') terabyte sorteren benchmark in 2009, met een snelheid van 0.578 TB/min (100 TB in 173 minuten). Zie voor meer informatie over deze en andere sorteren benchmarks Hallo [Sortbenchmark](http://sortbenchmark.org/) site.

Dit voorbeeld worden drie sets van MapReduce-programma's gebruikt:

* **TeraGen**: een MapReduce-programma die rijen met gegevens toosort genereert

* **TeraSort**: Hallo invoergegevens voorbeelden en MapReduce toosort Hallo gegevens worden gebruikt in een totale volgorde

    TeraSort is een standaard sortering MapReduce, met uitzondering van een aangepaste partitioner. Hallo partitioner maakt gebruik van een gesorteerde lijst met actieve N-1 sleutels die Hallo sleutel bereik voor elke verminderen definiëren. In het bijzonder alle sleutels dergelijke waarvan de steekproef [i-1] < sleutel = < voorbeeld [i] tooreduce worden verzonden ik. Deze partitioner garanties dat Hallo uitvoerwaarden van ik beperken zijn alle kleiner is dan Hallo-uitvoer van verminderen i + 1.

* **TeraValidate**: een MapReduce-programma te valideren die uitvoer Hallo globaal wordt gesorteerd

    Een kaart per bestand wordt gemaakt in de uitvoermap Hallo en elke toewijzing zorgt ervoor dat elke sleutel kleiner dan of gelijk is toohello vorige. Hallo kaart functie records Hallo eerst genereert en laatste sleutels van elk bestand. Hallo functie verminderen zorgt ervoor dat Hallo eerste sleutel van i-bestand is groter dan de laatste sleutel Hallo van bestand i-1. Eventuele problemen worden gerapporteerd als uitvoer voor Hallo fase verminderen met Hallo sleutels die zijn geplaatst.

Gebruik Hallo volgende stappen uit toogenerate gegevens, sorteren en vervolgens te valideren Hallo uitvoer:

1. Genereren van 10 GB aan gegevens, die opgeslagen toohello HDInsight cluster standaard opslag is op `/example/data/10GB-sort-input`:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapred.map.tasks=50 100000000 /example/data/10GB-sort-input
    ```

    Hallo `-Dmapred.map.tasks` vertelt Hadoop hoeveel kaart taken toouse voor deze taak. Hallo laatste twee parameters instrueren Hallo taak toocreate 10 GB aan gegevens en toostore op `/example/data/10GB-sort-input`.

2. Gebruik Hallo opdracht toosort Hallo gegevens te volgen:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-input /example/data/10GB-sort-output
    ```

    Hallo `-Dmapred.reduce.tasks` Hadoop geeft aan hoeveel taken toouse voor Hallo taak verminderen. Hallo laatste twee parameters zijn alleen Hallo invoer en uitvoer van de locaties voor gegevens.

3. Hallo volgt toovalidate Hallo gegevens die worden gegenereerd door Hallo sorteren gebruiken:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapred.map.tasks=50 -Dmapred.reduce.tasks=25 /example/data/10GB-sort-output /example/data/10GB-sort-validate
    ```

## <a name="next-steps"></a>Volgende stappen

In dit artikel hebt u geleerd hoe toorun Hallo voorbeelden opgenomen Hello Linux gebaseerde HDInsight-clusters. Zie voor de zelfstudies over het gebruik van Pig, Hive en MapReduce met HDInsight, Hallo volgende onderwerpen:

* [Pig gebruiken met Hadoop in HDInsight][hdinsight-use-pig]
* [Hive gebruiken met Hadoop in HDInsight][hdinsight-use-hive]
* [MapReduce gebruiken met Hadoop op HDInsight][hdinsight-use-mapreduce]

[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md



[hdinsight-samples]: hdinsight-run-samples.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
