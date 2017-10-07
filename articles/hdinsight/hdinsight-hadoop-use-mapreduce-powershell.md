---
title: aaaUse MapReduce en PowerShell gebruiken met Hadoop - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse PowerShell tooremotely MapReduce-taken uitvoeren met Hadoop op HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21b56d32-1785-4d44-8ae8-94467c12cfba
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 59524f0e8813d4c017f92bccb2e50d4c018acf71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a><span data-ttu-id="b3cc7-103">MapReduce-taken uitvoeren met Hadoop in HDInsight met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3cc7-103">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="b3cc7-104">Dit document bevat een voorbeeld van het gebruik van Azure PowerShell toorun een MapReduce-taak in een Hadoop op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-104">This document provides an example of using Azure PowerShell toorun a MapReduce job in a Hadoop on HDInsight cluster.</span></span>

## <span data-ttu-id="b3cc7-105"><a id="prereq"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="b3cc7-105"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="b3cc7-106">**Een Azure HDInsight (Hadoop in HDInsight)-cluster**</span><span class="sxs-lookup"><span data-stu-id="b3cc7-106">**An Azure HDInsight (Hadoop on HDInsight) cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="b3cc7-107">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b3cc7-108">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="b3cc7-109">**Een werkstation met Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-109">**A workstation with Azure PowerShell**.</span></span>

## <span data-ttu-id="b3cc7-110"><a id="powershell"></a>Voer een MapReduce-taak met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3cc7-110"><a id="powershell"></a>Run a MapReduce job using Azure PowerShell</span></span>

<span data-ttu-id="b3cc7-111">Azure PowerShell biedt *cmdlets* waarmee u kunt uitvoeren tooremotely MapReduce-taken in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-111">Azure PowerShell provides *cmdlets* that allow you tooremotely run MapReduce jobs on HDInsight.</span></span> <span data-ttu-id="b3cc7-112">Intern, dit wordt gerealiseerd met behulp van REST-aanroepen te[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (voorheen Templeton) uitgevoerd op Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-112">Internally, this is accomplished by using REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (formerly called Templeton) running on hello HDInsight cluster.</span></span>

<span data-ttu-id="b3cc7-113">Hallo worden volgende cmdlets gebruikt bij het uitvoeren van MapReduce-taken in een externe HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-113">hello following cmdlets are used when running MapReduce jobs in a remote HDInsight cluster.</span></span>

* <span data-ttu-id="b3cc7-114">**Login-AzureRmAccount**: Azure PowerShell verifieert tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-114">**Login-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure subscription.</span></span>

* <span data-ttu-id="b3cc7-115">**Nieuwe AzureRmHDInsightMapReduceJobDefinition**: maakt een nieuw *taak definitie* opgegeven met behulp van Hallo MapReduce-informatie.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-115">**New-AzureRmHDInsightMapReduceJobDefinition**: Creates a new *job definition* by using hello specified MapReduce information.</span></span>

* <span data-ttu-id="b3cc7-116">**Start AzureRmHDInsightJob**: Hallo taak definitie tooHDInsight verzendt, Hallo taak start en retourneert een *taak* -object dat gebruikt toocheck Hallo status van Hallo-taak worden kan.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-116">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job.</span></span>

* <span data-ttu-id="b3cc7-117">**Wacht AzureRmHDInsightJob**: Hallo object toocheck Hallo taakstatus van Hallo taak gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-117">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="b3cc7-118">Wacht totdat het Hallo-taak is voltooid of Hallo wachttijd is overschreden.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-118">It waits until hello job completes or hello wait time is exceeded.</span></span>

* <span data-ttu-id="b3cc7-119">**Get-AzureRmHDInsightJobOutput**: tooretrieve Hallo uitvoer van Hallo taak gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-119">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job.</span></span>

<span data-ttu-id="b3cc7-120">Hallo volgende stappen laten zien hoe toouse deze cmdlets toorun een taak in uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-120">hello following steps demonstrate how toouse these cmdlets toorun a job in your HDInsight cluster.</span></span>

1. <span data-ttu-id="b3cc7-121">Hallo code als volgt met een editor opslaan **mapreducejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-121">Using an editor, save hello following code as **mapreducejob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]

2. <span data-ttu-id="b3cc7-122">Open een nieuw **Azure PowerShell** opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-122">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="b3cc7-123">Locatie van de mappen toohello Hallo wijzigen **mapreducejob.ps1** bestand en gebruik vervolgens Hallo opdrachtscript toorun hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="b3cc7-123">Change directories toohello location of hello **mapreducejob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\mapreducejob.ps1

    <span data-ttu-id="b3cc7-124">Wanneer u Hallo script uitvoert, wordt u gevraagd Hallo-naam van Hallo HDInsight-cluster en Hallo HTTPS/Admin-accountnaam en wachtwoord voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-124">When you run hello script, you are prompted for hello name of hello HDInsight cluster and hello HTTPS/Admin account name and password for hello cluster.</span></span> <span data-ttu-id="b3cc7-125">Hebt u mogelijk ook na vragen aan gebruiker tooauthenticate tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-125">You may also be prompted tooauthenticate tooyour Azure subscription.</span></span>

3. <span data-ttu-id="b3cc7-126">Wanneer het Hallo-taak is voltooid, wordt uitvoer vergelijkbare toohello tekst te volgen:</span><span class="sxs-lookup"><span data-stu-id="b3cc7-126">When hello job completes, you receive output similar toohello following text:</span></span>

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    <span data-ttu-id="b3cc7-127">Deze uitvoer geeft aan dat Hallo-taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-127">This output indicates that hello job completed successfully.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b3cc7-128">Als hello **ExitCode** is een waarde dan 0, Zie [probleemoplossing](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="b3cc7-128">If hello **ExitCode** is a value other than 0, see [Troubleshooting](#troubleshooting).</span></span>

    <span data-ttu-id="b3cc7-129">In dit voorbeeld worden ook opgeslagen Hallo gedownloade bestanden tooan **uitvoer.txt** bestand in map Hallo met Hallo-script uit.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-129">This example also stores hello downloaded files tooan **output.txt** file in hello directory that you run hello script from.</span></span>

### <a name="view-output"></a><span data-ttu-id="b3cc7-130">Uitvoer weergeven</span><span class="sxs-lookup"><span data-stu-id="b3cc7-130">View output</span></span>

<span data-ttu-id="b3cc7-131">Open Hallo **uitvoer.txt** bestand in een tekst-editor toosee Hallo woorden en telt geproduceerd door Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-131">Open hello **output.txt** file in a text editor toosee hello words and counts produced by hello job.</span></span>

> [!NOTE]
> <span data-ttu-id="b3cc7-132">Hallo uitvoerbestanden van een MapReduce-taak zijn niet-wijzigbaar.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-132">hello output files of a MapReduce job are immutable.</span></span> <span data-ttu-id="b3cc7-133">Als u dit voorbeeld opnieuw uitvoeren, moet u dus toochange Hallo-naam van het uitvoerbestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-133">So if you rerun this sample, you need toochange hello name of hello output file.</span></span>

## <span data-ttu-id="b3cc7-134"><a id="troubleshooting"></a>Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="b3cc7-134"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="b3cc7-135">Als er geen informatie wordt geretourneerd wanneer Hallo-taak is voltooid, is een fout kan zijn opgetreden tijdens de verwerking.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-135">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="b3cc7-136">de foutgegevens tooview voor deze taak toevoegen na einde van de opdracht toohello Hallo Hallo **mapreducejob.ps1** bestand, opslaan en vervolgens opnieuw uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-136">tooview error information for this job, add hello following command toohello end of hello **mapreducejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print hello output of hello WordCount job.
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="b3cc7-137">Deze cmdlet retourneert Hallo-informatie die is geschreven tooSTDERR terwijl u Hallo taak werd uitgevoerd op de server Hallo en mogelijk kunt u bepalen waarom de Hallo-taak is mislukt.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-137">This cmdlet returns hello information that was written tooSTDERR on hello server when you ran hello job, and it may help determine why hello job is failing.</span></span>

## <span data-ttu-id="b3cc7-138"><a id="summary"></a>Samenvatting</span><span class="sxs-lookup"><span data-stu-id="b3cc7-138"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="b3cc7-139">Zoals u ziet, Azure PowerShell biedt een eenvoudige manier toorun MapReduce-taken op een HDInsight-cluster, de status van de taak Hallo monitor en ophalen Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="b3cc7-139">As you can see, Azure PowerShell provides an easy way toorun MapReduce jobs on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="b3cc7-140"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b3cc7-140"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="b3cc7-141">Voor algemene informatie over MapReduce-taken in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b3cc7-141">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="b3cc7-142">Gebruik MapReduce op HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="b3cc7-142">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="b3cc7-143">Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b3cc7-143">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="b3cc7-144">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b3cc7-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="b3cc7-145">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b3cc7-145">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
