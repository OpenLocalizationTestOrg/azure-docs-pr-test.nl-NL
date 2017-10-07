---
title: aaaUse Pig met PowerShell in HDInsight - Azure Hadoop | Microsoft Docs
description: Meer informatie over hoe toosubmit Pig-taken tooa Hadoop-cluster in HDInsight met Azure PowerShell.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 737089c1-b494-4387-9def-7b4dac3be532
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 771617df203011eaec715a0dba6f5014a42877f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toorun-pig-jobs-with-hdinsight"></a><span data-ttu-id="48d8c-103">Azure PowerShell toorun Pig-taken gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="48d8c-103">Use Azure PowerShell toorun Pig jobs with HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="48d8c-104">Dit document bevat een voorbeeld van het gebruik van Azure PowerShell toosubmit Pig-taken tooa Hadoop op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="48d8c-104">This document provides an example of using Azure PowerShell toosubmit Pig jobs tooa Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="48d8c-105">Pig kunt u toowrite MapReduce-taken met behulp van een andere taal (Pig Latin) modellen gegevenstransformaties, in plaats van toewijzen en functies te beperken.</span><span class="sxs-lookup"><span data-stu-id="48d8c-105">Pig allows you toowrite MapReduce jobs by using a language (Pig Latin) that models data transformations, rather than map and reduce functions.</span></span>

> [!NOTE]
> <span data-ttu-id="48d8c-106">Dit document biedt geen een gedetailleerde beschrijving van wat Hallo Pig Latin-instructies gebruikt in de voorbeelden Hallo doen.</span><span class="sxs-lookup"><span data-stu-id="48d8c-106">This document does not provide a detailed description of what hello Pig Latin statements used in hello examples do.</span></span> <span data-ttu-id="48d8c-107">Zie voor meer informatie over Hallo Pig Latin in dit voorbeeld gebruikt [Pig gebruiken met Hadoop op HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="48d8c-107">For information about hello Pig Latin used in this example, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

## <span data-ttu-id="48d8c-108"><a id="prereq"></a>Vereisten</span><span class="sxs-lookup"><span data-stu-id="48d8c-108"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="48d8c-109">**Een Azure HDInsight-cluster**</span><span class="sxs-lookup"><span data-stu-id="48d8c-109">**An Azure HDInsight cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="48d8c-110">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="48d8c-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="48d8c-111">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="48d8c-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="48d8c-112">**Een werkstation met Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="48d8c-112">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <span data-ttu-id="48d8c-113"><a id="powershell"></a>Pig-taken met behulp van PowerShell uitgevoerd</span><span class="sxs-lookup"><span data-stu-id="48d8c-113"><a id="powershell"></a>Run Pig jobs using PowerShell</span></span>

<span data-ttu-id="48d8c-114">Azure PowerShell biedt *cmdlets* waarmee u kunt uitvoeren tooremotely Pig-taken in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="48d8c-114">Azure PowerShell provides *cmdlets* that allow you tooremotely run Pig jobs on HDInsight.</span></span> <span data-ttu-id="48d8c-115">Intern PowerShell REST-aanroepen te gebruikt[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) uitgevoerd op Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="48d8c-115">Internally, PowerShell uses REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) running on hello HDInsight cluster.</span></span>

<span data-ttu-id="48d8c-116">Hallo worden volgende cmdlets gebruikt bij het uitvoeren van Pig-taken op een externe HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="48d8c-116">hello following cmdlets are used when running Pig jobs on a remote HDInsight cluster:</span></span>

* <span data-ttu-id="48d8c-117">**Login-AzureRmAccount**: Azure PowerShell verifieert tooyour Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="48d8c-117">**Login-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure Subscription</span></span>
* <span data-ttu-id="48d8c-118">**Nieuwe AzureRmHDInsightPigJobDefinition**: maakt een *taak definitie* opgegeven met behulp van Hallo Pig Latin-instructies</span><span class="sxs-lookup"><span data-stu-id="48d8c-118">**New-AzureRmHDInsightPigJobDefinition**: Creates a *job definition* by using hello specified Pig Latin statements</span></span>
* <span data-ttu-id="48d8c-119">**Start AzureRmHDInsightJob**: Hallo taak definitie tooHDInsight verzendt, Hallo taak start en retourneert een *taak* -object dat gebruikt toocheck Hallo status van Hallo-taak worden kan</span><span class="sxs-lookup"><span data-stu-id="48d8c-119">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job</span></span>
* <span data-ttu-id="48d8c-120">**Wacht AzureRmHDInsightJob**: Hallo object toocheck Hallo taakstatus van Hallo taak gebruikt.</span><span class="sxs-lookup"><span data-stu-id="48d8c-120">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="48d8c-121">Wacht totdat het Hallo-taak is voltooid of Hallo wachttijd is overschreden.</span><span class="sxs-lookup"><span data-stu-id="48d8c-121">It waits until hello job has completed, or hello wait time has been exceeded.</span></span>
* <span data-ttu-id="48d8c-122">**Get-AzureRmHDInsightJobOutput**: tooretrieve Hallo uitvoer van Hallo taak gebruikt</span><span class="sxs-lookup"><span data-stu-id="48d8c-122">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job</span></span>

<span data-ttu-id="48d8c-123">Hallo volgende stappen laten zien hoe toouse deze cmdlets toorun een taak op uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="48d8c-123">hello following steps demonstrate how toouse these cmdlets toorun a job on your HDInsight cluster.</span></span>

1. <span data-ttu-id="48d8c-124">Hallo code als volgt met een editor opslaan **pigjob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="48d8c-124">Using an editor, save hello following code as **pigjob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]

1. <span data-ttu-id="48d8c-125">Open een nieuw Windows PowerShell-opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="48d8c-125">Open a new Windows PowerShell command prompt.</span></span> <span data-ttu-id="48d8c-126">Locatie van de mappen toohello Hallo wijzigen **pigjob.ps1** bestand en gebruik vervolgens Hallo opdrachtscript toorun hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="48d8c-126">Change directories toohello location of hello **pigjob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\pigjob.ps1

    <span data-ttu-id="48d8c-127">U bent na vragen aan gebruiker toolog in tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="48d8c-127">You are prompted toolog in tooyour Azure subscription.</span></span> <span data-ttu-id="48d8c-128">Vervolgens wordt u gevraagd om Hallo HTTPs/Admin-accountnaam en wachtwoord voor Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="48d8c-128">Then, you are asked for hello HTTPs/Admin account name and password for hello HDInsight cluster.</span></span>

2. <span data-ttu-id="48d8c-129">Het moet informatie vergelijkbare toohello tekst volgende retourneren wanneer op Hallo-taak is voltooid:</span><span class="sxs-lookup"><span data-stu-id="48d8c-129">When hello job completes, it should return information similar toohello following text:</span></span>

        Start hello Pig job ...
        Wait for hello Pig job toocomplete ...
        Display hello standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="48d8c-130"><a id="troubleshooting"></a>Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="48d8c-130"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="48d8c-131">Als er geen informatie wordt geretourneerd wanneer Hallo-taak is voltooid, is een fout kan zijn opgetreden tijdens de verwerking.</span><span class="sxs-lookup"><span data-stu-id="48d8c-131">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="48d8c-132">de foutgegevens tooview voor deze taak toevoegen na einde van de opdracht toohello Hallo Hallo **pigjob.ps1** bestand, opslaan en vervolgens opnieuw uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="48d8c-132">tooview error information for this job, add hello following command toohello end of hello **pigjob.ps1** file, save it, and then run it again.</span></span>

    # Print hello output of hello Pig job.
    Write-Host "Display hello standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

<span data-ttu-id="48d8c-133">Dit Hallo-informatie die is geschreven tooSTDERR terwijl u Hallo taak werd uitgevoerd op Hallo-server retourneert en mogelijk kunt u bepalen waarom de Hallo-taak is mislukt.</span><span class="sxs-lookup"><span data-stu-id="48d8c-133">This returns hello information that was written tooSTDERR on hello server when you ran hello job, and it may help determine why hello job is failing.</span></span>

## <span data-ttu-id="48d8c-134"><a id="summary"></a>Samenvatting</span><span class="sxs-lookup"><span data-stu-id="48d8c-134"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="48d8c-135">Zoals u ziet, Azure PowerShell biedt een eenvoudige manier toorun Pig-taken op een HDInsight-cluster, de status van de taak Hallo monitor en ophalen Hallo uitvoer.</span><span class="sxs-lookup"><span data-stu-id="48d8c-135">As you can see, Azure PowerShell provides an easy way toorun Pig jobs on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="48d8c-136"><a id="nextsteps"></a>Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="48d8c-136"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="48d8c-137">Voor algemene informatie over Pig in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="48d8c-137">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="48d8c-138">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="48d8c-138">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="48d8c-139">Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="48d8c-139">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="48d8c-140">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="48d8c-140">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="48d8c-141">MapReduce gebruiken met Hadoop op HDInsight</span><span class="sxs-lookup"><span data-stu-id="48d8c-141">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
