---
title: aaaUse Hadoop Hive met PowerShell in HDInsight - Azure | Microsoft Docs
description: Gebruik PowerShell toorun Hive-query's in Hadoop op HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cb795b7c-bcd0-497a-a7f0-8ed18ef49195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 9e0b72a25c5b12431f837b1a34a63ecc06223528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-powershell"></a><span data-ttu-id="4fcb1-103">Uitvoeren van Hive-query's met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="4fcb1-103">Run Hive queries using PowerShell</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="4fcb1-104">Dit document bevat een voorbeeld van het gebruik van Azure PowerShell in hello Azure-resourcegroep modus toorun Hive-query's in een Hadoop op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="4fcb1-104">This document provides an example of using Azure PowerShell in hello Azure Resource Group mode toorun Hive queries in a Hadoop on HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="4fcb1-105">Dit document biedt geen een gedetailleerde beschrijving van wat Hallo HiveQL-instructies die worden gebruikt in de voorbeelden Hallo doen.</span><span class="sxs-lookup"><span data-stu-id="4fcb1-105">This document does not provide a detailed description of what hello HiveQL statements that are used in hello examples do.</span></span> <span data-ttu-id="4fcb1-106">Zie voor informatie over Hallo HiveQL die wordt gebruikt in dit voorbeeld, [Hive gebruiken met Hadoop op HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="4fcb1-106">For information on hello HiveQL that is used in this example, see [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="4fcb1-107">**Vereisten**</span><span class="sxs-lookup"><span data-stu-id="4fcb1-107">**Prerequisites**</span></span>

* <span data-ttu-id="4fcb1-108">**Een Azure HDInsight-cluster**: het maakt niet uit of Windows hello cluster of op basis van Linux.</span><span class="sxs-lookup"><span data-stu-id="4fcb1-108">**An Azure HDInsight cluster**: It does not matter whether hello cluster is Windows or Linux-based.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="4fcb1-109">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="4fcb1-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4fcb1-110">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4fcb1-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="4fcb1-111">**Een werkstation met Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="4fcb1-111">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a><span data-ttu-id="4fcb1-112">Uitvoeren van Hive-query's met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="4fcb1-112">Run Hive queries using Azure PowerShell</span></span>

<span data-ttu-id="4fcb1-113">Azure PowerShell biedt *cmdlets* waarmee u kunt uitvoeren tooremotely Hive-query's op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4fcb1-113">Azure PowerShell provides *cmdlets* that allow you tooremotely run Hive queries on HDInsight.</span></span> <span data-ttu-id="4fcb1-114">Intern maakt u Hallo cmdlets REST-aanroepen te[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) op Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="4fcb1-114">Internally, hello cmdlets make REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) on hello HDInsight cluster.</span></span>

<span data-ttu-id="4fcb1-115">Hallo worden volgende cmdlets gebruikt bij het uitvoeren van Hive-query's in een externe HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="4fcb1-115">hello following cmdlets are used when running Hive queries in a remote HDInsight cluster:</span></span>

* <span data-ttu-id="4fcb1-116">**Add-AzureRmAccount**: Azure PowerShell verifieert tooyour Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="4fcb1-116">**Add-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure subscription</span></span>
* <span data-ttu-id="4fcb1-117">**Nieuwe AzureRmHDInsightHiveJobDefinition**: maakt een *taak definitie* opgegeven met behulp van Hallo HiveQL-instructies</span><span class="sxs-lookup"><span data-stu-id="4fcb1-117">**New-AzureRmHDInsightHiveJobDefinition**: Creates a *job definition* by using hello specified HiveQL statements</span></span>
* <span data-ttu-id="4fcb1-118">**Start AzureRmHDInsightJob**: Hallo taak definitie tooHDInsight verzendt, Hallo taak start en retourneert een *taak* -object dat gebruikt toocheck Hallo status van Hallo-taak worden kan</span><span class="sxs-lookup"><span data-stu-id="4fcb1-118">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job</span></span>
* <span data-ttu-id="4fcb1-119">**Wacht AzureRmHDInsightJob**: Hallo object toocheck Hallo taakstatus van Hallo taak gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4fcb1-119">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="4fcb1-120">Wacht totdat het Hallo-taak is voltooid of Hallo wachttijd is overschreden.</span><span class="sxs-lookup"><span data-stu-id="4fcb1-120">It waits until hello job completes or hello wait time is exceeded.</span></span>
* <span data-ttu-id="4fcb1-121">**Get-AzureRmHDInsightJobOutput**: tooretrieve Hallo uitvoer van Hallo taak gebruikt</span><span class="sxs-lookup"><span data-stu-id="4fcb1-121">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job</span></span>
* <span data-ttu-id="4fcb1-122">**Aanroepen AzureRmHDInsightHiveJob**: toorun HiveQL-instructies gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4fcb1-122">**Invoke-AzureRmHDInsightHiveJob**: Used toorun HiveQL statements.</span></span> <span data-ttu-id="4fcb1-123">Deze cmdlet blokken Hallo-query is voltooid en geeft vervolgens Hallo resultaten</span><span class="sxs-lookup"><span data-stu-id="4fcb1-123">This cmdlet blocks hello query completes, then returns hello results</span></span>
* <span data-ttu-id="4fcb1-124">**Gebruik AzureRmHDInsightCluster**: Sets Hallo huidige cluster toouse voor Hallo **Invoke-AzureRmHDInsightHiveJob** opdracht</span><span class="sxs-lookup"><span data-stu-id="4fcb1-124">**Use-AzureRmHDInsightCluster**: Sets hello current cluster toouse for hello **Invoke-AzureRmHDInsightHiveJob** command</span></span>

<span data-ttu-id="4fcb1-125">Hallo volgende stappen laten zien hoe toouse deze cmdlets toorun een taak in uw HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="4fcb1-125">hello following steps demonstrate how toouse these cmdlets toorun a job in your HDInsight cluster:</span></span>

1. <span data-ttu-id="4fcb1-126">Hallo code als volgt met een editor opslaan **hivejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="4fcb1-126">Using an editor, save hello following code as **hivejob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. <span data-ttu-id="4fcb1-127">Open een nieuw **Azure PowerShell** opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="4fcb1-127">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="4fcb1-128">Locatie van de mappen toohello Hallo wijzigen **hivejob.ps1** bestand en gebruik vervolgens Hallo opdrachtscript toorun hello te volgen:</span><span class="sxs-lookup"><span data-stu-id="4fcb1-128">Change directories toohello location of hello **hivejob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\hivejob.ps1

    <span data-ttu-id="4fcb1-129">Wanneer het Hallo-script wordt uitgevoerd, bent u na vragen aan gebruiker tooenter Hallo cluster naam en het Hallo HTTPS/Admin accountreferenties voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="4fcb1-129">When hello script runs, you are prompted tooenter hello cluster name and hello HTTPS/Admin account credentials for hello cluster.</span></span> <span data-ttu-id="4fcb1-130">Hebt u mogelijk ook na vragen aan gebruiker toolog in tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="4fcb1-130">You may also be prompted toolog in tooyour Azure subscription.</span></span>

3. <span data-ttu-id="4fcb1-131">Wanneer het Hallo-taak is voltooid, wordt informatie vergelijkbare toohello thext te volgen:</span><span class="sxs-lookup"><span data-stu-id="4fcb1-131">When hello job completes, it returns information similar toohello following thext:</span></span>

        Display hello standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. <span data-ttu-id="4fcb1-132">Zoals eerder gezegd **Invoke-Hive** kan worden gebruikt toorun een query en wachten op antwoord Hallo.</span><span class="sxs-lookup"><span data-stu-id="4fcb1-132">As mentioned earlier, **Invoke-Hive** can be used toorun a query and wait for hello response.</span></span> <span data-ttu-id="4fcb1-133">Hallo script toosee de werking van Invoke-Hive volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="4fcb1-133">Use hello following script toosee how Invoke-Hive works:</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    <span data-ttu-id="4fcb1-134">Hallo-uitvoer ziet er Hallo volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="4fcb1-134">hello output looks like hello following text:</span></span>

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > <span data-ttu-id="4fcb1-135">Voor meer HiveQL-query's, kunt u hello Azure PowerShell **hier tekenreeksen** cmdlet of HiveQL scriptbestanden.</span><span class="sxs-lookup"><span data-stu-id="4fcb1-135">For longer HiveQL queries, you can use hello Azure PowerShell **Here-Strings** cmdlet or HiveQL script files.</span></span> <span data-ttu-id="4fcb1-136">Hallo volgende codefragment bevat hoe toouse hello **Invoke-Hive** cmdlet toorun een scriptbestand HiveQL.</span><span class="sxs-lookup"><span data-stu-id="4fcb1-136">hello following snippet shows how toouse hello **Invoke-Hive** cmdlet toorun a HiveQL script file.</span></span> <span data-ttu-id="4fcb1-137">Hallo HiveQL scriptbestand moet worden geüpload toowasb: / /.</span><span class="sxs-lookup"><span data-stu-id="4fcb1-137">hello HiveQL script file must be uploaded toowasb://.</span></span>
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > <span data-ttu-id="4fcb1-138">Voor meer informatie over **hier tekenreeksen**, Zie <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">met behulp van Windows PowerShell hier-tekenreeksen</a>.</span><span class="sxs-lookup"><span data-stu-id="4fcb1-138">For more information about **Here-Strings**, see <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a>.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="4fcb1-139">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="4fcb1-139">Troubleshooting</span></span>

<span data-ttu-id="4fcb1-140">Als er geen informatie wordt geretourneerd wanneer Hallo-taak is voltooid, is een fout kan zijn opgetreden tijdens de verwerking.</span><span class="sxs-lookup"><span data-stu-id="4fcb1-140">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="4fcb1-141">Foutgegevens tooview voor deze taak toevoegen na einde toohello Hallo Hallo **hivejob.ps1** bestand, opslaan en vervolgens opnieuw uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="4fcb1-141">tooview error information for this job, add hello following toohello end of hello **hivejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print hello output of hello Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="4fcb1-142">Deze cmdlet retourneert Hallo-informatie die is geschreven tooSTDERR terwijl u Hallo taak werd uitgevoerd op Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="4fcb1-142">This cmdlet returns hello information that is written tooSTDERR on hello server when you ran hello job.</span></span>

## <a name="summary"></a><span data-ttu-id="4fcb1-143">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="4fcb1-143">Summary</span></span>

<span data-ttu-id="4fcb1-144">Zoals u ziet, Azure PowerShell biedt een eenvoudige manier toorun Hive-query's in een HDInsight-cluster, Hallo monitor status van taken en Hallo uitvoer ophalen.</span><span class="sxs-lookup"><span data-stu-id="4fcb1-144">As you can see, Azure PowerShell provides an easy way toorun Hive queries in an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fcb1-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4fcb1-145">Next steps</span></span>

<span data-ttu-id="4fcb1-146">Voor algemene informatie over Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="4fcb1-146">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="4fcb1-147">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4fcb1-147">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="4fcb1-148">Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="4fcb1-148">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="4fcb1-149">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4fcb1-149">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="4fcb1-150">MapReduce gebruiken met Hadoop op HDInsight</span><span class="sxs-lookup"><span data-stu-id="4fcb1-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
