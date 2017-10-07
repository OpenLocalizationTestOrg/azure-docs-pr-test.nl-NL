---
title: aaaGenerate aanbevelingen met Mahout HDInsight vanuit PowerShell - Azure | Microsoft Docs
description: Meer informatie over hoe toouse Hallo Apache Mahout machine learning-bibliotheek toogenerate filmaanbevelingen met HDInsight (Hadoop) vanuit een PowerShell-script uitgevoerd op de client.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 07b57208-32aa-4e59-900a-6c934fa1b7a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 675a2cd8ecaf7fc797d6cd094e4e58f9aca7ed92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-hadoop-in-hdinsight-powershell"></a>Filmaanbevelingen genereren met behulp van Apache Mahout met Hadoop in HDInsight (PowerShell)

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

Meer informatie over hoe toouse hello [Apache Mahout](http://mahout.apache.org) machine learning-bibliotheek met Azure HDInsight toogenerate filmaanbevelingen. Hallo-voorbeeld in dit document wordt Azure PowerShell toorun Mahout taken.

## <a name="prerequisites"></a>Vereisten

* Een Linux gebaseerde HDInsight-cluster. Zie voor meer informatie over het maken van een [aan de slag met Hadoop op basis van Linux in HDInsight][getstarted].

> [!IMPORTANT]
> Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

* [Azure PowerShell](/powershell/azure/overview)

## <a name="recommendations"></a>Aanbevelingen genereren met behulp van Azure PowerShell

> [!WARNING]
> Hallo-taak in deze sectie werkt met behulp van Azure PowerShell. Veel van Hallo-klassen die zijn opgegeven met Mahout werkt momenteel niet met Azure PowerShell. Zie voor een lijst met klassen die niet met Azure PowerShell werken, Hallo [probleemoplossing](#troubleshooting) sectie.
>
> Zie voor een voorbeeld van het gebruik van SSH tooconnect tooHDInsight en voer Mahout voorbeelden rechtstreeks op Hallo cluster [filmaanbevelingen genereren met Mahout en HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).

Een van Hallo-functies die wordt geleverd door Mahout is een aanbeveling-engine. Deze engine accepteert gegevens in de indeling van Hallo `userID`, `itemId`, en `prefValue` (Hallo gebruikers voorkeur voor Hallo item). Mahout hello data toodetermine gebruikers like-item-voorkeuren gebruikte toomake aanbevelingen kunnen worden gebruikt.

Hallo is volgende voorbeeld een eenvoudig overzicht van hoe Hallo aanbeveling proces werkt:

* **mede exemplaar**: Jan Els en Bob alle bevallen *Star Wars*, *Empire ontvangen terug Hallo*, en *Return Hallo Jedi*. Mahout bepaalt dat gebruikers die als een van deze films ook graag twee andere Hallo.

* **mede exemplaar**: Bob en Els ook bevallen *Hallo Phantom Menace*, *een aanval op Hallo klonen*, en *Revenge Hallo Sith*. Mahout bepaalt dat gebruikers die ook de vorige drie films Hallo bevallen, zoals deze films.

* **Gelijkenis aanbeveling**: omdat Jan bevallen Hallo eerste drie films, Mahout wordt bekeken films die anderen met vergelijkbare voorkeuren bevallen, maar Joe heeft geen gevolgde (bevallen/geclassificeerd). In dit geval Mahout raadt *Hallo Phantom Menace*, *een aanval op Hallo klonen*, en *Revenge Hallo Sith*.

### <a name="understanding-hello-data"></a>Understanding Hallo gegevens

[GroupLens Research] [ movielens] biedt classificatie gegevens voor films in een indeling die compatibel is met Mahout. Deze gegevens zijn beschikbaar op Hallo standaard opslag voor uw cluster op `/HdiSamples//HdiSamples/MahoutMovieData`.

Er zijn twee bestanden: `moviedb.txt` (informatie over Hallo films) en `user-ratings.txt`. Hallo `user-ratings.txt` -bestand wordt gebruikt tijdens de analyse. Hallo `moviedb.txt` bestand is gebruikte tooprovide gebruiksvriendelijke tekst hello resultaten van Hallo analyse om weer te geven.

Hallo gegevens in gebruiker ratings.txt heeft een structuur van `userID`, `movieID`, `userRating`, en `timestamp`, die vertellen hoe maximaal elke gebruiker een film beoordeeld. Hier volgt een voorbeeld van Hallo gegevens:

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

### <a name="run-hello-job"></a>Hallo-taak uitvoeren

Gebruik Hallo Windows PowerShell-script toorun een taak die gebruikmaakt van Hallo Mahout aanbeveling engine met Hallo filmgegevens te volgen:

> [!NOTE]
> Dit bestand wordt u gevraagd om informatie die is gebruikt tooconnect tooyour HDInsight-cluster en taken uitvoeren. Het kan enkele minuten duren voordat Hallo taken toocomplete en Hallo uitvoer.txt bestand downloaden.

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]

> [!NOTE]
> Mahout taken verwijderd tijdelijke gegevens die zijn gemaakt tijdens het verwerken van Hallo-taak niet. Hallo `--tempDir` parameter wordt opgegeven in Hallo voorbeeld taak tooisolate Hallo tijdelijke bestanden naar een specifieke map.

Hallo Mahout taak levert geen Hallo uitvoer tooSTDOUT. In plaats daarvan wordt deze opgeslagen in de opgegeven uitvoermap Hallo als **onderdeel-r-00000**. Hallo script downloadt u dit bestand te**uitvoer.txt** in de huidige map Hallo op uw werkstation.

Hallo is volgende tekst een voorbeeld van Hallo inhoud van dit bestand:

    1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
    2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
    3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
    4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

de eerste kolom Hallo is Hallo `userID`. waarden in Hallo ' [' en ']' zijn `movieId`:`recommendationScore`.

Hallo script ook gedownload Hallo `moviedb.txt` en `user-ratings.txt` bestanden, wat nodig tooformat Hallo uitvoer toobe beter leesbaar zijn.

### <a name="view-hello-output"></a>Hallo-uitvoer weergeven

Hoewel hello gegenereerde uitvoer mogelijk OK voor gebruik in een toepassing, is het niet gebruiksvriendelijke. Hallo `moviedb.txt` van Hallo-server worden gebruikt tooresolve hello `movieId` tooa film naam. Hallo PowerShell script toodisplay aanbevelingen met film namen gebruiken:

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]

Hallo opdracht toodisplay Hallo aanbevelingen in een gebruiksvriendelijke indeling gebruiken: 

```powershell
.\show-recommendation.ps1 -userId 4 -userDataFile .\user-ratings.txt -movieFile .\moviedb.txt -recommendationFile .\output.txt
```

Hallo uitvoer is vergelijkbaar toohello de volgende tekst:

    Reading movies descriptions
    Reading rated movies
    Reading recommendations
    Rated movies
    ---------------------------
    Movie                                    Rating
    -----                                    ------
    Devil's Own, hello (1997)                  1
    Alien: Resurrection (1997)               3
    187 (1997)                               2
    (lines ommitted)

    ---------------------------
    Recommended movies
    ---------------------------

    Movie                                    Score
    -----                                    -----
    Good Will Hunting (1997)                 4.6504064
    Swingers (1996)                          4.6862745
    Wings of hello Dove, hello (1997)            4.6666665
    People vs. Larry Flynt, hello (1996)       4.834559
    Everyone Says I Love You (1996)          4.707071
    Secrets & Lies (1996)                    4.818182
    That Thing You Do! (1996)                4.75
    Grosse Pointe Blank (1997)               4.8235292
    Donnie Brasco (1997)                     4.6792455
    Lone Star (1996)                         4.7099237

## <a name="troubleshooting"></a>Problemen oplossen

### <a name="cannot-overwrite-files"></a>Bestanden kan niet worden overschreven.

Mahout taken komen niet opruimen van tijdelijke bestanden die zijn gemaakt tijdens de verwerking. Bovendien overschrijven Hallo taken niet bestaande uitvoerbestand.

tooavoid fouten bij het uitvoeren van taken Mahout, verwijdert u tijdelijke- en uitvoergegevens bestanden tussen wordt uitgevoerd. tooremove hello bestanden die zijn gemaakt door Hallo eerdere scripts in dit document Hallo volgende PowerShell-script gebruiken:

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

#Get hello cluster info so we can get hello resource group, storage, etc.
$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName = $clusterInfo.DefaultStorageAccount.split('.')[0]
$container = $clusterInfo.DefaultStorageContainer
$storageAccountKey = (Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage context and upload hello file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

#Azure PowerShell can't delete blobs using wildcard,
#so have tooget a list and delete one at a time
# Start with hello output
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/out"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
# Next hello temp files
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/temp"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
```

### <a name="nopowershell"></a>Klassen die niet met Azure PowerShell werken

Mahout-functies die gebruikmaken van de volgende klassen Hallo retourneren verschillende foutberichten bij gebruik van Windows PowerShell:

* org.apache.mahout.utils.clustering.ClusterDumper
* org.apache.mahout.utils.SequenceFileDumper
* org.apache.mahout.utils.vectors.lucene.Driver
* org.apache.mahout.utils.vectors.arff.Driver
* org.apache.mahout.text.WikipediaToSequenceFile
* org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles
* org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer
* org.apache.mahout.classifier.sgd.TrainLogistic
* org.apache.mahout.classifier.sgd.RunLogistic
* org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic
* org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic
* org.apache.mahout.classifier.sgd.RunAdaptiveLogistic
* org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer
* org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator
* org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator
* org.apache.mahout.classifier.df.tools.Describe

toorun-functies die gebruikmaken van deze klassen toohello HDInsight-cluster via SSH verbinding Hallo-taken en uitvoeren vanaf de opdrachtregel Hallo. Zie voor een voorbeeld van het gebruik van SSH toorun Mahout taken [filmaanbevelingen genereren met Mahout en HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).

## <a name="next-steps"></a>Volgende stappen

U hebt geleerd hoe toouse Mahout, andere manieren om te werken met gegevens in HDInsight detecteren:

* [Hive met HDInsight](hdinsight-use-hive.md)
* [Pig met HDInsight](hdinsight-use-pig.md)
* [MapReduce met HDInsight](hdinsight-use-mapreduce.md)

[build]: http://mahout.apache.org/developers/buildingmahout.html
[aps]: /powershell/azureps-cmdlets-docs
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
