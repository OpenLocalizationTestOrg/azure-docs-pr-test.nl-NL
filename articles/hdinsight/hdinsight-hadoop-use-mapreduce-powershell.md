---
title: MapReduce en PowerShell gebruiken met Hadoop - Azure HDInsight | Microsoft Docs
description: Informatie over het gebruiken van PowerShell op afstand MapReduce-taken uitvoeren met Hadoop op HDInsight.
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
ms.openlocfilehash: c3801573808709f29cb1e563ac803f225a28cafc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a><span data-ttu-id="ead70-103">MapReduce-taken uitvoeren met Hadoop in HDInsight met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="ead70-103">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="ead70-104">Dit document bevat een voorbeeld van een MapReduce-taak uitgevoerd in een Hadoop op HDInsight-cluster met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ead70-104">This document provides an example of using Azure PowerShell to run a MapReduce job in a Hadoop on HDInsight cluster.</span></span>

## <span data-ttu-id="ead70-105"><a id="prereq"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="ead70-105"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="ead70-106">**Een Azure HDInsight (Hadoop in HDInsight)-cluster**</span><span class="sxs-lookup"><span data-stu-id="ead70-106">**An Azure HDInsight (Hadoop on HDInsight) cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="ead70-107">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="ead70-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ead70-108">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ead70-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="ead70-109">**Een werkstation met Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="ead70-109">**A workstation with Azure PowerShell**.</span></span>

## <span data-ttu-id="ead70-110"><a id="powershell"></a>Voer een MapReduce-taak met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ead70-110"><a id="powershell"></a>Run a MapReduce job using Azure PowerShell</span></span>

<span data-ttu-id="ead70-111">Azure PowerShell biedt *cmdlets* waarmee u kunt op afstand MapReduce-taken uitvoeren op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ead70-111">Azure PowerShell provides *cmdlets* that allow you to remotely run MapReduce jobs on HDInsight.</span></span> <span data-ttu-id="ead70-112">Intern maakt u dit kunt doen met behulp van REST-aanroepen naar [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (voorheen Templeton) uitgevoerd op het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="ead70-112">Internally, this is accomplished by using REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (formerly called Templeton) running on the HDInsight cluster.</span></span>

<span data-ttu-id="ead70-113">De volgende cmdlets worden gebruikt bij het uitvoeren van MapReduce-taken in een externe HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="ead70-113">The following cmdlets are used when running MapReduce jobs in a remote HDInsight cluster.</span></span>

* <span data-ttu-id="ead70-114">**Login-AzureRmAccount**: Azure PowerShell verifieert met uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="ead70-114">**Login-AzureRmAccount**: Authenticates Azure PowerShell to your Azure subscription.</span></span>

* <span data-ttu-id="ead70-115">**Nieuwe AzureRmHDInsightMapReduceJobDefinition**: maakt een nieuw *taak definitie* met behulp van de opgegeven MapReduce-informatie.</span><span class="sxs-lookup"><span data-stu-id="ead70-115">**New-AzureRmHDInsightMapReduceJobDefinition**: Creates a new *job definition* by using the specified MapReduce information.</span></span>

* <span data-ttu-id="ead70-116">**Start AzureRmHDInsightJob**: de taakdefinitie verzendt naar HDInsight, wordt de taak wordt gestart en wordt een *taak* -object dat kan worden gebruikt om de status van de taak te controleren.</span><span class="sxs-lookup"><span data-stu-id="ead70-116">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job.</span></span>

* <span data-ttu-id="ead70-117">**Wacht AzureRmHDInsightJob**: het taakobject gebruikt om te controleren van de status van de taak.</span><span class="sxs-lookup"><span data-stu-id="ead70-117">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="ead70-118">Wacht totdat de taak is voltooid of de wachttijd is overschreden.</span><span class="sxs-lookup"><span data-stu-id="ead70-118">It waits until the job completes or the wait time is exceeded.</span></span>

* <span data-ttu-id="ead70-119">**Get-AzureRmHDInsightJobOutput**: gebruikt voor het ophalen van de uitvoer van de taak.</span><span class="sxs-lookup"><span data-stu-id="ead70-119">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job.</span></span>

<span data-ttu-id="ead70-120">De volgende stappen laten zien hoe u deze cmdlets gebruiken om een taak uitvoert in uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="ead70-120">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster.</span></span>

1. <span data-ttu-id="ead70-121">De volgende code als met een editor opslaan **mapreducejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="ead70-121">Using an editor, save the following code as **mapreducejob.ps1**.</span></span>

    <span data-ttu-id="ead70-122">[!code-powershell[belangrijkste](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]</span><span class="sxs-lookup"><span data-stu-id="ead70-122">[!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]</span></span>

2. <span data-ttu-id="ead70-123">Open een nieuw **Azure PowerShell** opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="ead70-123">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="ead70-124">Wijzig de mappen naar de locatie van de **mapreducejob.ps1** bestand en vervolgens voert u het script met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ead70-124">Change directories to the location of the **mapreducejob.ps1** file, then use the following command to run the script:</span></span>

        .\mapreducejob.ps1

    <span data-ttu-id="ead70-125">Wanneer u het script uitvoert, wordt u gevraagd om de naam van het HDInsight-cluster en de HTTPS/Admin-accountnaam en wachtwoord voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="ead70-125">When you run the script, you are prompted for the name of the HDInsight cluster and the HTTPS/Admin account name and password for the cluster.</span></span> <span data-ttu-id="ead70-126">U mogelijk ook gevraagd om uw Azure-abonnement te verifiëren.</span><span class="sxs-lookup"><span data-stu-id="ead70-126">You may also be prompted to authenticate to your Azure subscription.</span></span>

3. <span data-ttu-id="ead70-127">Wanneer de taak is voltooid, wordt de uitvoer is vergelijkbaar met de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="ead70-127">When the job completes, you receive output similar to the following text:</span></span>

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    <span data-ttu-id="ead70-128">Deze uitvoer geeft aan dat de taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="ead70-128">This output indicates that the job completed successfully.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ead70-129">Als de **ExitCode** is een waarde dan 0, Zie [probleemoplossing](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="ead70-129">If the **ExitCode** is a value other than 0, see [Troubleshooting](#troubleshooting).</span></span>

    <span data-ttu-id="ead70-130">In dit voorbeeld worden ook opgeslagen de gedownloade bestanden naar een **uitvoer.txt** bestand in de map met het script uit.</span><span class="sxs-lookup"><span data-stu-id="ead70-130">This example also stores the downloaded files to an **output.txt** file in the directory that you run the script from.</span></span>

### <a name="view-output"></a><span data-ttu-id="ead70-131">Uitvoer weergeven</span><span class="sxs-lookup"><span data-stu-id="ead70-131">View output</span></span>

<span data-ttu-id="ead70-132">Open de **uitvoer.txt** bestand in een teksteditor om de woorden en aantallen geproduceerd door de taak te zien.</span><span class="sxs-lookup"><span data-stu-id="ead70-132">Open the **output.txt** file in a text editor to see the words and counts produced by the job.</span></span>

> [!NOTE]
> <span data-ttu-id="ead70-133">De uitvoerbestanden van een MapReduce-taak zijn niet-wijzigbaar.</span><span class="sxs-lookup"><span data-stu-id="ead70-133">The output files of a MapReduce job are immutable.</span></span> <span data-ttu-id="ead70-134">Dus als u dit voorbeeld opnieuw uitvoeren, moet u de naam van het uitvoerbestand wijzigen.</span><span class="sxs-lookup"><span data-stu-id="ead70-134">So if you rerun this sample, you need to change the name of the output file.</span></span>

## <span data-ttu-id="ead70-135"><a id="troubleshooting"></a>Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="ead70-135"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="ead70-136">Als er geen gegevens worden geretourneerd als de taak is voltooid, is een fout kan zijn opgetreden tijdens de verwerking.</span><span class="sxs-lookup"><span data-stu-id="ead70-136">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="ead70-137">Om weer te geven informatie over de fout voor deze taak, kunt u de volgende opdracht toevoegen aan het einde van de **mapreducejob.ps1** bestand, opslaan en vervolgens opnieuw uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="ead70-137">To view error information for this job, add the following command to the end of the **mapreducejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print the output of the WordCount job.
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="ead70-138">Deze cmdlet retourneert de informatie die is geschreven naar STDERR op de server bij het uitvoeren van de taak en mogelijk kunt u bepalen waarom de taak is mislukt.</span><span class="sxs-lookup"><span data-stu-id="ead70-138">This cmdlet returns the information that was written to STDERR on the server when you ran the job, and it may help determine why the job is failing.</span></span>

## <span data-ttu-id="ead70-139"><a id="summary"></a>Samenvatting</span><span class="sxs-lookup"><span data-stu-id="ead70-139"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="ead70-140">Zoals u zien kunt, biedt Azure PowerShell een eenvoudige manier om MapReduce-taken uitvoeren op een HDInsight-cluster, de taakstatus te controleren en ophalen van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="ead70-140">As you can see, Azure PowerShell provides an easy way to run MapReduce jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="ead70-141"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ead70-141"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="ead70-142">Voor algemene informatie over MapReduce-taken in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ead70-142">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="ead70-143">Gebruik MapReduce op HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="ead70-143">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="ead70-144">Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ead70-144">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="ead70-145">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ead70-145">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="ead70-146">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ead70-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
