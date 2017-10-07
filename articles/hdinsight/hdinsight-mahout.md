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
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-hadoop-in-hdinsight-powershell"></a><span data-ttu-id="e2036-103">Filmaanbevelingen genereren met behulp van Apache Mahout met Hadoop in HDInsight (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="e2036-103">Generate movie recommendations by using Apache Mahout with Hadoop in HDInsight (PowerShell)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="e2036-104">Meer informatie over hoe toouse hello [Apache Mahout](http://mahout.apache.org) machine learning-bibliotheek met Azure HDInsight toogenerate filmaanbevelingen.</span><span class="sxs-lookup"><span data-stu-id="e2036-104">Learn how toouse hello [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight toogenerate movie recommendations.</span></span> <span data-ttu-id="e2036-105">Hallo-voorbeeld in dit document wordt Azure PowerShell toorun Mahout taken.</span><span class="sxs-lookup"><span data-stu-id="e2036-105">hello example in this document uses Azure PowerShell toorun Mahout jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e2036-106">Vereisten</span><span class="sxs-lookup"><span data-stu-id="e2036-106">Prerequisites</span></span>

* <span data-ttu-id="e2036-107">Een Linux gebaseerde HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="e2036-107">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="e2036-108">Zie voor meer informatie over het maken van een [aan de slag met Hadoop op basis van Linux in HDInsight][getstarted].</span><span class="sxs-lookup"><span data-stu-id="e2036-108">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e2036-109">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="e2036-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e2036-110">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e2036-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="e2036-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2036-111">Azure PowerShell</span></span>](/powershell/azure/overview)

## <span data-ttu-id="e2036-112"><a name="recommendations"></a>Aanbevelingen genereren met behulp van Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2036-112"><a name="recommendations"></a>Generate recommendations by using Azure PowerShell</span></span>

> [!WARNING]
> <span data-ttu-id="e2036-113">Hallo-taak in deze sectie werkt met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e2036-113">hello job in this section works by using Azure PowerShell.</span></span> <span data-ttu-id="e2036-114">Veel van Hallo-klassen die zijn opgegeven met Mahout werkt momenteel niet met Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e2036-114">Many of hello classes provided with Mahout do not currently work with Azure PowerShell.</span></span> <span data-ttu-id="e2036-115">Zie voor een lijst met klassen die niet met Azure PowerShell werken, Hallo [probleemoplossing](#troubleshooting) sectie.</span><span class="sxs-lookup"><span data-stu-id="e2036-115">For a list of classes that do not work with Azure PowerShell, see hello [Troubleshooting](#troubleshooting) section.</span></span>
>
> <span data-ttu-id="e2036-116">Zie voor een voorbeeld van het gebruik van SSH tooconnect tooHDInsight en voer Mahout voorbeelden rechtstreeks op Hallo cluster [filmaanbevelingen genereren met Mahout en HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="e2036-116">For an example of using SSH tooconnect tooHDInsight and run Mahout examples directly on hello cluster, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

<span data-ttu-id="e2036-117">Een van Hallo-functies die wordt geleverd door Mahout is een aanbeveling-engine.</span><span class="sxs-lookup"><span data-stu-id="e2036-117">One of hello functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="e2036-118">Deze engine accepteert gegevens in de indeling van Hallo `userID`, `itemId`, en `prefValue` (Hallo gebruikers voorkeur voor Hallo item).</span><span class="sxs-lookup"><span data-stu-id="e2036-118">This engine accepts data in hello format of `userID`, `itemId`, and `prefValue` (hello users preference for hello item).</span></span> <span data-ttu-id="e2036-119">Mahout hello data toodetermine gebruikers like-item-voorkeuren gebruikte toomake aanbevelingen kunnen worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="e2036-119">Mahout uses hello data toodetermine users with like-item preferences, which can be used toomake recommendations.</span></span>

<span data-ttu-id="e2036-120">Hallo is volgende voorbeeld een eenvoudig overzicht van hoe Hallo aanbeveling proces werkt:</span><span class="sxs-lookup"><span data-stu-id="e2036-120">hello following example is a simplified walk-through of how hello recommendation process works:</span></span>

* <span data-ttu-id="e2036-121">**mede exemplaar**: Jan Els en Bob alle bevallen *Star Wars*, *Empire ontvangen terug Hallo*, en *Return Hallo Jedi*.</span><span class="sxs-lookup"><span data-stu-id="e2036-121">**co-occurrence**: Joe, Alice, and Bob all liked *Star Wars*, *hello Empire Strikes Back*, and *Return of hello Jedi*.</span></span> <span data-ttu-id="e2036-122">Mahout bepaalt dat gebruikers die als een van deze films ook graag twee andere Hallo.</span><span class="sxs-lookup"><span data-stu-id="e2036-122">Mahout determines that users who like any one of these movies also like hello other two.</span></span>

* <span data-ttu-id="e2036-123">**mede exemplaar**: Bob en Els ook bevallen *Hallo Phantom Menace*, *een aanval op Hallo klonen*, en *Revenge Hallo Sith*.</span><span class="sxs-lookup"><span data-stu-id="e2036-123">**co-occurrence**: Bob and Alice also liked *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span> <span data-ttu-id="e2036-124">Mahout bepaalt dat gebruikers die ook de vorige drie films Hallo bevallen, zoals deze films.</span><span class="sxs-lookup"><span data-stu-id="e2036-124">Mahout determines that users who liked hello previous three movies also like these movies.</span></span>

* <span data-ttu-id="e2036-125">**Gelijkenis aanbeveling**: omdat Jan bevallen Hallo eerste drie films, Mahout wordt bekeken films die anderen met vergelijkbare voorkeuren bevallen, maar Joe heeft geen gevolgde (bevallen/geclassificeerd).</span><span class="sxs-lookup"><span data-stu-id="e2036-125">**Similarity recommendation**: Because Joe liked hello first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="e2036-126">In dit geval Mahout raadt *Hallo Phantom Menace*, *een aanval op Hallo klonen*, en *Revenge Hallo Sith*.</span><span class="sxs-lookup"><span data-stu-id="e2036-126">In this case, Mahout recommends *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span>

### <a name="understanding-hello-data"></a><span data-ttu-id="e2036-127">Understanding Hallo gegevens</span><span class="sxs-lookup"><span data-stu-id="e2036-127">Understanding hello data</span></span>

<span data-ttu-id="e2036-128">[GroupLens Research] [ movielens] biedt classificatie gegevens voor films in een indeling die compatibel is met Mahout.</span><span class="sxs-lookup"><span data-stu-id="e2036-128">[GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="e2036-129">Deze gegevens zijn beschikbaar op Hallo standaard opslag voor uw cluster op `/HdiSamples//HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="e2036-129">This data is available on hello default storage for your cluster at `/HdiSamples//HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="e2036-130">Er zijn twee bestanden: `moviedb.txt` (informatie over Hallo films) en `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="e2036-130">There are two files, `moviedb.txt` (information about hello movies) and `user-ratings.txt`.</span></span> <span data-ttu-id="e2036-131">Hallo `user-ratings.txt` -bestand wordt gebruikt tijdens de analyse.</span><span class="sxs-lookup"><span data-stu-id="e2036-131">hello `user-ratings.txt` file is used during analysis.</span></span> <span data-ttu-id="e2036-132">Hallo `moviedb.txt` bestand is gebruikte tooprovide gebruiksvriendelijke tekst hello resultaten van Hallo analyse om weer te geven.</span><span class="sxs-lookup"><span data-stu-id="e2036-132">hello `moviedb.txt` file is used tooprovide user-friendly text when displaying hello results of hello analysis.</span></span>

<span data-ttu-id="e2036-133">Hallo gegevens in gebruiker ratings.txt heeft een structuur van `userID`, `movieID`, `userRating`, en `timestamp`, die vertellen hoe maximaal elke gebruiker een film beoordeeld.</span><span class="sxs-lookup"><span data-stu-id="e2036-133">hello data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="e2036-134">Hier volgt een voorbeeld van Hallo gegevens:</span><span class="sxs-lookup"><span data-stu-id="e2036-134">Here is an example of hello data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

### <a name="run-hello-job"></a><span data-ttu-id="e2036-135">Hallo-taak uitvoeren</span><span class="sxs-lookup"><span data-stu-id="e2036-135">Run hello job</span></span>

<span data-ttu-id="e2036-136">Gebruik Hallo Windows PowerShell-script toorun een taak die gebruikmaakt van Hallo Mahout aanbeveling engine met Hallo filmgegevens te volgen:</span><span class="sxs-lookup"><span data-stu-id="e2036-136">Use hello following Windows PowerShell script toorun a job that uses hello Mahout recommendation engine with hello movie data:</span></span>

> [!NOTE]
> <span data-ttu-id="e2036-137">Dit bestand wordt u gevraagd om informatie die is gebruikt tooconnect tooyour HDInsight-cluster en taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="e2036-137">This file prompts you for information that is used tooconnect tooyour HDInsight cluster and run jobs.</span></span> <span data-ttu-id="e2036-138">Het kan enkele minuten duren voordat Hallo taken toocomplete en Hallo uitvoer.txt bestand downloaden.</span><span class="sxs-lookup"><span data-stu-id="e2036-138">It may take several minutes for hello jobs toocomplete and download hello output.txt file.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]

> [!NOTE]
> <span data-ttu-id="e2036-139">Mahout taken verwijderd tijdelijke gegevens die zijn gemaakt tijdens het verwerken van Hallo-taak niet.</span><span class="sxs-lookup"><span data-stu-id="e2036-139">Mahout jobs do not remove temporary data that is created while processing hello job.</span></span> <span data-ttu-id="e2036-140">Hallo `--tempDir` parameter wordt opgegeven in Hallo voorbeeld taak tooisolate Hallo tijdelijke bestanden naar een specifieke map.</span><span class="sxs-lookup"><span data-stu-id="e2036-140">hello `--tempDir` parameter is specified in hello example job tooisolate hello temporary files into a specific directory.</span></span>

<span data-ttu-id="e2036-141">Hallo Mahout taak levert geen Hallo uitvoer tooSTDOUT.</span><span class="sxs-lookup"><span data-stu-id="e2036-141">hello Mahout job does not return hello output tooSTDOUT.</span></span> <span data-ttu-id="e2036-142">In plaats daarvan wordt deze opgeslagen in de opgegeven uitvoermap Hallo als **onderdeel-r-00000**.</span><span class="sxs-lookup"><span data-stu-id="e2036-142">Instead, it stores it in hello specified output directory as **part-r-00000**.</span></span> <span data-ttu-id="e2036-143">Hallo script downloadt u dit bestand te**uitvoer.txt** in de huidige map Hallo op uw werkstation.</span><span class="sxs-lookup"><span data-stu-id="e2036-143">hello script downloads this file too**output.txt** in hello current directory on your workstation.</span></span>

<span data-ttu-id="e2036-144">Hallo is volgende tekst een voorbeeld van Hallo inhoud van dit bestand:</span><span class="sxs-lookup"><span data-stu-id="e2036-144">hello following text is an example of hello content of this file:</span></span>

    1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
    2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
    3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
    4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

<span data-ttu-id="e2036-145">de eerste kolom Hallo is Hallo `userID`.</span><span class="sxs-lookup"><span data-stu-id="e2036-145">hello first column is hello `userID`.</span></span> <span data-ttu-id="e2036-146">waarden in Hallo ' [' en ']' zijn `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="e2036-146">hello values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

<span data-ttu-id="e2036-147">Hallo script ook gedownload Hallo `moviedb.txt` en `user-ratings.txt` bestanden, wat nodig tooformat Hallo uitvoer toobe beter leesbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="e2036-147">hello script also downloads hello `moviedb.txt` and `user-ratings.txt` files, which are needed tooformat hello output toobe more readable.</span></span>

### <a name="view-hello-output"></a><span data-ttu-id="e2036-148">Hallo-uitvoer weergeven</span><span class="sxs-lookup"><span data-stu-id="e2036-148">View hello output</span></span>

<span data-ttu-id="e2036-149">Hoewel hello gegenereerde uitvoer mogelijk OK voor gebruik in een toepassing, is het niet gebruiksvriendelijke.</span><span class="sxs-lookup"><span data-stu-id="e2036-149">Although hello generated output might be OK for use in an application, it's not user-friendly.</span></span> <span data-ttu-id="e2036-150">Hallo `moviedb.txt` van Hallo-server worden gebruikt tooresolve hello `movieId` tooa film naam.</span><span class="sxs-lookup"><span data-stu-id="e2036-150">hello `moviedb.txt` from hello server can be used tooresolve hello `movieId` tooa movie name.</span></span> <span data-ttu-id="e2036-151">Hallo PowerShell script toodisplay aanbevelingen met film namen gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e2036-151">Use hello following PowerShell script toodisplay recommendations with movie names:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]

<span data-ttu-id="e2036-152">Hallo opdracht toodisplay Hallo aanbevelingen in een gebruiksvriendelijke indeling gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e2036-152">Use hello following command toodisplay hello recommendations in a user-friendly format:</span></span> 

```powershell
.\show-recommendation.ps1 -userId 4 -userDataFile .\user-ratings.txt -movieFile .\moviedb.txt -recommendationFile .\output.txt
```

<span data-ttu-id="e2036-153">Hallo uitvoer is vergelijkbaar toohello de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="e2036-153">hello output is similar toohello following text:</span></span>

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

## <span data-ttu-id="e2036-154"><a name="troubleshooting"></a>Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="e2036-154"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="cannot-overwrite-files"></a><span data-ttu-id="e2036-155">Bestanden kan niet worden overschreven.</span><span class="sxs-lookup"><span data-stu-id="e2036-155">Cannot overwrite files</span></span>

<span data-ttu-id="e2036-156">Mahout taken komen niet opruimen van tijdelijke bestanden die zijn gemaakt tijdens de verwerking.</span><span class="sxs-lookup"><span data-stu-id="e2036-156">Mahout jobs do not clean up temporary files that were created during processing.</span></span> <span data-ttu-id="e2036-157">Bovendien overschrijven Hallo taken niet bestaande uitvoerbestand.</span><span class="sxs-lookup"><span data-stu-id="e2036-157">In addition, hello jobs do not overwrite existing output file.</span></span>

<span data-ttu-id="e2036-158">tooavoid fouten bij het uitvoeren van taken Mahout, verwijdert u tijdelijke- en uitvoergegevens bestanden tussen wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e2036-158">tooavoid errors when running Mahout jobs, delete temporary and output files between runs.</span></span> <span data-ttu-id="e2036-159">tooremove hello bestanden die zijn gemaakt door Hallo eerdere scripts in dit document Hallo volgende PowerShell-script gebruiken:</span><span class="sxs-lookup"><span data-stu-id="e2036-159">tooremove hello files created by hello earlier scripts in this document, use hello following PowerShell script:</span></span>

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

### <span data-ttu-id="e2036-160"><a name="nopowershell"></a>Klassen die niet met Azure PowerShell werken</span><span class="sxs-lookup"><span data-stu-id="e2036-160"><a name="nopowershell"></a>Classes that do not work with Azure PowerShell</span></span>

<span data-ttu-id="e2036-161">Mahout-functies die gebruikmaken van de volgende klassen Hallo retourneren verschillende foutberichten bij gebruik van Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="e2036-161">Mahout jobs that use hello following classes return various error messages when used from Windows PowerShell:</span></span>

* <span data-ttu-id="e2036-162">org.apache.mahout.utils.clustering.ClusterDumper</span><span class="sxs-lookup"><span data-stu-id="e2036-162">org.apache.mahout.utils.clustering.ClusterDumper</span></span>
* <span data-ttu-id="e2036-163">org.apache.mahout.utils.SequenceFileDumper</span><span class="sxs-lookup"><span data-stu-id="e2036-163">org.apache.mahout.utils.SequenceFileDumper</span></span>
* <span data-ttu-id="e2036-164">org.apache.mahout.utils.vectors.lucene.Driver</span><span class="sxs-lookup"><span data-stu-id="e2036-164">org.apache.mahout.utils.vectors.lucene.Driver</span></span>
* <span data-ttu-id="e2036-165">org.apache.mahout.utils.vectors.arff.Driver</span><span class="sxs-lookup"><span data-stu-id="e2036-165">org.apache.mahout.utils.vectors.arff.Driver</span></span>
* <span data-ttu-id="e2036-166">org.apache.mahout.text.WikipediaToSequenceFile</span><span class="sxs-lookup"><span data-stu-id="e2036-166">org.apache.mahout.text.WikipediaToSequenceFile</span></span>
* <span data-ttu-id="e2036-167">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span><span class="sxs-lookup"><span data-stu-id="e2036-167">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span></span>
* <span data-ttu-id="e2036-168">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span><span class="sxs-lookup"><span data-stu-id="e2036-168">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span></span>
* <span data-ttu-id="e2036-169">org.apache.mahout.classifier.sgd.TrainLogistic</span><span class="sxs-lookup"><span data-stu-id="e2036-169">org.apache.mahout.classifier.sgd.TrainLogistic</span></span>
* <span data-ttu-id="e2036-170">org.apache.mahout.classifier.sgd.RunLogistic</span><span class="sxs-lookup"><span data-stu-id="e2036-170">org.apache.mahout.classifier.sgd.RunLogistic</span></span>
* <span data-ttu-id="e2036-171">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="e2036-171">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span></span>
* <span data-ttu-id="e2036-172">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="e2036-172">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span></span>
* <span data-ttu-id="e2036-173">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="e2036-173">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span></span>
* <span data-ttu-id="e2036-174">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span><span class="sxs-lookup"><span data-stu-id="e2036-174">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span></span>
* <span data-ttu-id="e2036-175">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span><span class="sxs-lookup"><span data-stu-id="e2036-175">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span></span>
* <span data-ttu-id="e2036-176">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span><span class="sxs-lookup"><span data-stu-id="e2036-176">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span></span>
* <span data-ttu-id="e2036-177">org.apache.mahout.classifier.df.tools.Describe</span><span class="sxs-lookup"><span data-stu-id="e2036-177">org.apache.mahout.classifier.df.tools.Describe</span></span>

<span data-ttu-id="e2036-178">toorun-functies die gebruikmaken van deze klassen toohello HDInsight-cluster via SSH verbinding Hallo-taken en uitvoeren vanaf de opdrachtregel Hallo.</span><span class="sxs-lookup"><span data-stu-id="e2036-178">toorun jobs that use these classes, connect toohello HDInsight cluster using SSH and run hello jobs from hello command line.</span></span> <span data-ttu-id="e2036-179">Zie voor een voorbeeld van het gebruik van SSH toorun Mahout taken [filmaanbevelingen genereren met Mahout en HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="e2036-179">For an example of using SSH toorun Mahout jobs, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2036-180">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e2036-180">Next steps</span></span>

<span data-ttu-id="e2036-181">U hebt geleerd hoe toouse Mahout, andere manieren om te werken met gegevens in HDInsight detecteren:</span><span class="sxs-lookup"><span data-stu-id="e2036-181">Now that you have learned how toouse Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="e2036-182">Hive met HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2036-182">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="e2036-183">Pig met HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2036-183">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="e2036-184">MapReduce met HDInsight</span><span class="sxs-lookup"><span data-stu-id="e2036-184">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

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
