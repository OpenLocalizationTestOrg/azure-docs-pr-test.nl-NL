---
title: Hadoop Hive gebruiken met PowerShell in HDInsight - Azure | Microsoft Docs
description: PowerShell gebruiken voor het uitvoeren van Hive-query's in Hadoop op HDInsight.
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
ms.openlocfilehash: e1cb2e4a1fc82fb43082e79a5feba71b81b3eaa8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-using-powershell"></a><span data-ttu-id="e9812-103">Uitvoeren van Hive-query's met behulp van PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9812-103">Run Hive queries using PowerShell</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="e9812-104">Dit document bevat een voorbeeld van het gebruik van Azure PowerShell in de modus Azure Resource Group Hive-query's uitvoeren in een Hadoop op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="e9812-104">This document provides an example of using Azure PowerShell in the Azure Resource Group mode to run Hive queries in a Hadoop on HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="e9812-105">Dit document biedt geen een gedetailleerde beschrijving van wat de HiveQL-instructies die worden gebruikt in de voorbeelden doen.</span><span class="sxs-lookup"><span data-stu-id="e9812-105">This document does not provide a detailed description of what the HiveQL statements that are used in the examples do.</span></span> <span data-ttu-id="e9812-106">Zie voor informatie over de HiveQL die wordt gebruikt in dit voorbeeld, [Hive gebruiken met Hadoop op HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="e9812-106">For information on the HiveQL that is used in this example, see [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="e9812-107">**Vereisten**</span><span class="sxs-lookup"><span data-stu-id="e9812-107">**Prerequisites**</span></span>

* <span data-ttu-id="e9812-108">**Een Azure HDInsight-cluster**: het maakt niet uit of het cluster Windows is of Linux-.</span><span class="sxs-lookup"><span data-stu-id="e9812-108">**An Azure HDInsight cluster**: It does not matter whether the cluster is Windows or Linux-based.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="e9812-109">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="e9812-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e9812-110">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="e9812-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="e9812-111">**Een werkstation met Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="e9812-111">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a><span data-ttu-id="e9812-112">Uitvoeren van Hive-query's met Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9812-112">Run Hive queries using Azure PowerShell</span></span>

<span data-ttu-id="e9812-113">Azure PowerShell biedt *cmdlets* waarmee u kunt op afstand Hive-query's uitvoeren op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e9812-113">Azure PowerShell provides *cmdlets* that allow you to remotely run Hive queries on HDInsight.</span></span> <span data-ttu-id="e9812-114">Intern, de REST-aanroepen naar voor het maken van de cmdlets [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) op het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="e9812-114">Internally, the cmdlets make REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) on the HDInsight cluster.</span></span>

<span data-ttu-id="e9812-115">De volgende cmdlets worden gebruikt bij het uitvoeren van Hive-query's in een externe HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="e9812-115">The following cmdlets are used when running Hive queries in a remote HDInsight cluster:</span></span>

* <span data-ttu-id="e9812-116">**Add-AzureRmAccount**: Azure PowerShell verifieert met uw Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="e9812-116">**Add-AzureRmAccount**: Authenticates Azure PowerShell to your Azure subscription</span></span>
* <span data-ttu-id="e9812-117">**Nieuwe AzureRmHDInsightHiveJobDefinition**: maakt een *taak definitie* met behulp van de opgegeven HiveQL-instructies</span><span class="sxs-lookup"><span data-stu-id="e9812-117">**New-AzureRmHDInsightHiveJobDefinition**: Creates a *job definition* by using the specified HiveQL statements</span></span>
* <span data-ttu-id="e9812-118">**Start AzureRmHDInsightJob**: de taakdefinitie verzendt naar HDInsight, wordt de taak wordt gestart en wordt een *taak* -object dat kan worden gebruikt om de status van de taak controleren</span><span class="sxs-lookup"><span data-stu-id="e9812-118">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job</span></span>
* <span data-ttu-id="e9812-119">**Wacht AzureRmHDInsightJob**: het taakobject gebruikt om te controleren van de status van de taak.</span><span class="sxs-lookup"><span data-stu-id="e9812-119">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="e9812-120">Wacht totdat de taak is voltooid of de wachttijd is overschreden.</span><span class="sxs-lookup"><span data-stu-id="e9812-120">It waits until the job completes or the wait time is exceeded.</span></span>
* <span data-ttu-id="e9812-121">**Get-AzureRmHDInsightJobOutput**: gebruikt voor het ophalen van de uitvoer van de taak</span><span class="sxs-lookup"><span data-stu-id="e9812-121">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job</span></span>
* <span data-ttu-id="e9812-122">**Aanroepen AzureRmHDInsightHiveJob**: gebruikt voor het uitvoeren van HiveQL-instructies.</span><span class="sxs-lookup"><span data-stu-id="e9812-122">**Invoke-AzureRmHDInsightHiveJob**: Used to run HiveQL statements.</span></span> <span data-ttu-id="e9812-123">Deze cmdlet-blokken de query is voltooid en vervolgens de resultaten geretourneerd</span><span class="sxs-lookup"><span data-stu-id="e9812-123">This cmdlet blocks the query completes, then returns the results</span></span>
* <span data-ttu-id="e9812-124">**Gebruik AzureRmHDInsightCluster**: Hiermee stelt u het huidige cluster moet worden gebruikt voor de **Invoke-AzureRmHDInsightHiveJob** opdracht</span><span class="sxs-lookup"><span data-stu-id="e9812-124">**Use-AzureRmHDInsightCluster**: Sets the current cluster to use for the **Invoke-AzureRmHDInsightHiveJob** command</span></span>

<span data-ttu-id="e9812-125">De volgende stappen laten zien hoe u deze cmdlets gebruiken om een taak uitvoert in uw HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="e9812-125">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster:</span></span>

1. <span data-ttu-id="e9812-126">De volgende code als met een editor opslaan **hivejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="e9812-126">Using an editor, save the following code as **hivejob.ps1**.</span></span>

    <span data-ttu-id="e9812-127">[!code-powershell[belangrijkste](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]</span><span class="sxs-lookup"><span data-stu-id="e9812-127">[!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]</span></span>

2. <span data-ttu-id="e9812-128">Open een nieuw **Azure PowerShell** opdrachtprompt.</span><span class="sxs-lookup"><span data-stu-id="e9812-128">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="e9812-129">Wijzig de mappen naar de locatie van de **hivejob.ps1** bestand en vervolgens voert u het script met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="e9812-129">Change directories to the location of the **hivejob.ps1** file, then use the following command to run the script:</span></span>

        .\hivejob.ps1

    <span data-ttu-id="e9812-130">Wanneer het script wordt uitgevoerd, wordt u gevraagd de clusternaam en referenties van het HTTPS/Admin-account invoeren voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="e9812-130">When the script runs, you are prompted to enter the cluster name and the HTTPS/Admin account credentials for the cluster.</span></span> <span data-ttu-id="e9812-131">U kunt ook gevraagd zich aanmelden bij uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="e9812-131">You may also be prompted to log in to your Azure subscription.</span></span>

3. <span data-ttu-id="e9812-132">Wanneer de taak is voltooid, wordt informatie vergelijkbaar met de volgende thext:</span><span class="sxs-lookup"><span data-stu-id="e9812-132">When the job completes, it returns information similar to the following thext:</span></span>

        Display the standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. <span data-ttu-id="e9812-133">Zoals eerder gezegd **Invoke-Hive** kan worden gebruikt voor een query uitvoeren en wacht tot het antwoord.</span><span class="sxs-lookup"><span data-stu-id="e9812-133">As mentioned earlier, **Invoke-Hive** can be used to run a query and wait for the response.</span></span> <span data-ttu-id="e9812-134">Het volgende script gebruiken om te zien hoe Invoke-Hive werkt:</span><span class="sxs-lookup"><span data-stu-id="e9812-134">Use the following script to see how Invoke-Hive works:</span></span>

    <span data-ttu-id="e9812-135">[!code-powershell[belangrijkste](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]</span><span class="sxs-lookup"><span data-stu-id="e9812-135">[!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]</span></span>

    <span data-ttu-id="e9812-136">De uitvoer ziet er de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="e9812-136">The output looks like the following text:</span></span>

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > <span data-ttu-id="e9812-137">Voor meer HiveQL-query's, kunt u Azure PowerShell **hier tekenreeksen** cmdlet of HiveQL scriptbestanden.</span><span class="sxs-lookup"><span data-stu-id="e9812-137">For longer HiveQL queries, you can use the Azure PowerShell **Here-Strings** cmdlet or HiveQL script files.</span></span> <span data-ttu-id="e9812-138">Het volgende fragment toont hoe u de **Invoke-Hive** cmdlet een bestand HiveQL-script uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="e9812-138">The following snippet shows how to use the **Invoke-Hive** cmdlet to run a HiveQL script file.</span></span> <span data-ttu-id="e9812-139">Het scriptbestand HiveQL moet worden geüpload naar wasb: / /.</span><span class="sxs-lookup"><span data-stu-id="e9812-139">The HiveQL script file must be uploaded to wasb://.</span></span>
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > <span data-ttu-id="e9812-140">Voor meer informatie over **hier tekenreeksen**, Zie <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">met behulp van Windows PowerShell hier-tekenreeksen</a>.</span><span class="sxs-lookup"><span data-stu-id="e9812-140">For more information about **Here-Strings**, see <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a>.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="e9812-141">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="e9812-141">Troubleshooting</span></span>

<span data-ttu-id="e9812-142">Als er geen gegevens worden geretourneerd als de taak is voltooid, is een fout kan zijn opgetreden tijdens de verwerking.</span><span class="sxs-lookup"><span data-stu-id="e9812-142">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="e9812-143">Als u wilt weergeven van informatie over de fout voor deze taak, Voeg het volgende toe aan het einde van de **hivejob.ps1** bestand, opslaan en vervolgens opnieuw uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="e9812-143">To view error information for this job, add the following to the end of the **hivejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print the output of the Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="e9812-144">Deze cmdlet retourneert de gegevens die in STDERR op de server worden geschreven wanneer u de taak is uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="e9812-144">This cmdlet returns the information that is written to STDERR on the server when you ran the job.</span></span>

## <a name="summary"></a><span data-ttu-id="e9812-145">Samenvatting</span><span class="sxs-lookup"><span data-stu-id="e9812-145">Summary</span></span>

<span data-ttu-id="e9812-146">Zoals u zien kunt, biedt Azure PowerShell een eenvoudige manier om Hive-query's uitvoeren in een HDInsight-cluster, de taakstatus te controleren en ophalen van de uitvoer.</span><span class="sxs-lookup"><span data-stu-id="e9812-146">As you can see, Azure PowerShell provides an easy way to run Hive queries in an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e9812-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e9812-147">Next steps</span></span>

<span data-ttu-id="e9812-148">Voor algemene informatie over Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e9812-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="e9812-149">Hive gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e9812-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="e9812-150">Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:</span><span class="sxs-lookup"><span data-stu-id="e9812-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="e9812-151">Pig gebruiken met Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e9812-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="e9812-152">MapReduce gebruiken met Hadoop op HDInsight</span><span class="sxs-lookup"><span data-stu-id="e9812-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
