---
title: aaaInstall en gebruik Giraph op Hadoop-clusters in HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe toocustomize HDInsight-cluster met Giraph en hoe toouse Giraph.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 77a1d0e0-55de-4e61-98a0-060914fb7ca0
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: bd473faca9d3c87c29d7566a18fc94211c50f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="800fd-103">Installeren en gebruiken van Giraph op Windows gebaseerde HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="800fd-103">Install and use Giraph on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="800fd-104">Meer informatie over hoe Windows toocustomize gebaseerd HDInsight-cluster met Giraph met behulp van de scriptactie en hoe toouse Giraph tooprocess grootschalige grafieken.</span><span class="sxs-lookup"><span data-stu-id="800fd-104">Learn how toocustomize Windows based HDInsight cluster with Giraph using Script Action, and how toouse Giraph tooprocess large-scale graphs.</span></span> <span data-ttu-id="800fd-105">Zie voor meer informatie over het gebruik van Giraph met een cluster op basis van Linux [Giraph installeren op HDInsight Hadoop-clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="800fd-105">For information on using Giraph with a Linux-based cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="800fd-106">Hallo stappen in dit document alleen werken met HDInsight op basis van Windows-clusters.</span><span class="sxs-lookup"><span data-stu-id="800fd-106">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="800fd-107">HDInsight is alleen beschikbaar in Windows voor versies lager is dan HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="800fd-107">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="800fd-108">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="800fd-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="800fd-109">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="800fd-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="800fd-110">Voor meer informatie over tooinstall Giraph op Linux gebaseerde HDInsight-cluster Zie [Giraph installeren op HDInsight Hadoop-clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="800fd-110">For information on how tooinstall Giraph on a Linux-based HDInsight cluster, see [Install Giraph on HDInsight Hadoop clusters (Linux)](hdinsight-hadoop-giraph-install-linux.md).</span></span>


<span data-ttu-id="800fd-111">U kunt Giraph installeren op elk type (Hadoop, Storm, HBase, Spark)-cluster in Azure HDInsight met behulp van *scriptactie*.</span><span class="sxs-lookup"><span data-stu-id="800fd-111">You can install Giraph on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="800fd-112">Een voorbeeld script tooinstall Giraph op een HDInsight-cluster is beschikbaar via een alleen-lezen Azure storage-blob op [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="800fd-112">A sample script tooinstall Giraph on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span> <span data-ttu-id="800fd-113">Hallo-voorbeeldscript werkt alleen met HDInsight-cluster versie 3.1.</span><span class="sxs-lookup"><span data-stu-id="800fd-113">hello sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="800fd-114">Zie voor meer informatie over de versies van HDInsight-cluster, [versies van HDInsight-cluster](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="800fd-114">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="800fd-115">**Verwante artikelen**</span><span class="sxs-lookup"><span data-stu-id="800fd-115">**Related articles**</span></span>

* [<span data-ttu-id="800fd-116">Giraph installeren op HDInsight Hadoop-clusters (Linux)</span><span class="sxs-lookup"><span data-stu-id="800fd-116">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="800fd-117">[Hadoop-clusters maken in HDInsight](hdinsight-provision-clusters.md): algemene informatie over het maken van HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="800fd-117">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="800fd-118">[HDInsight-cluster via scriptactie aanpassen][hdinsight-cluster-customize]: algemene informatie over het aanpassen van HDInsight-clusters met behulp van de scriptactie.</span><span class="sxs-lookup"><span data-stu-id="800fd-118">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="800fd-119">[Scriptactie-scripts ontwikkelen voor HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="800fd-119">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-giraph"></a><span data-ttu-id="800fd-120">Wat is Giraph?</span><span class="sxs-lookup"><span data-stu-id="800fd-120">What is Giraph?</span></span>
<span data-ttu-id="800fd-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> kunt u tooperform grafiek verwerken met behulp van Hadoop en kan worden gebruikt met Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="800fd-121"><a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="800fd-122">Grafieken model relaties tussen de objecten, zoals Hallo-verbindingen tussen routers op een grote netwerk, zoals Hallo Internet, of relaties tussen mensen op sociale netwerken (soms waarnaar wordt verwezen tooas sociale grafiek).</span><span class="sxs-lookup"><span data-stu-id="800fd-122">Graphs model relationships between objects, such as hello connections between routers on a large network like hello Internet, or relationships between people on social networks (sometimes referred tooas a social graph).</span></span> <span data-ttu-id="800fd-123">Grafiek verwerking kunt u tooreason over Hallo relaties tussen de objecten in een grafiek, zoals:</span><span class="sxs-lookup"><span data-stu-id="800fd-123">Graph processing allows you tooreason about hello relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="800fd-124">Identificeren van mogelijke vrienden op basis van uw huidige relaties.</span><span class="sxs-lookup"><span data-stu-id="800fd-124">Identifying potential friends based on your current relationships.</span></span>
* <span data-ttu-id="800fd-125">Identificerende Hallo kortste afstand tussen twee computers in een netwerk.</span><span class="sxs-lookup"><span data-stu-id="800fd-125">Identifying hello shortest route between two computers in a network.</span></span>
* <span data-ttu-id="800fd-126">Berekenen Hallo pagina positie van webpagina's.</span><span class="sxs-lookup"><span data-stu-id="800fd-126">Calculating hello page rank of webpages.</span></span>

## <a name="install-giraph-using-portal"></a><span data-ttu-id="800fd-127">Giraph met portal installeren</span><span class="sxs-lookup"><span data-stu-id="800fd-127">Install Giraph using portal</span></span>
1. <span data-ttu-id="800fd-128">Beginnen met het maken van een cluster met behulp van Hallo **aangepast maken** optie, zoals beschreven op [maken Hadoop-clusters in HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="800fd-128">Start creating a cluster by using hello **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="800fd-129">Op Hallo **scriptacties** pagina van wizard hello, klikt u op **toevoegen scriptactie** tooprovide om details over de scriptactie hello, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="800fd-129">On hello **Script Actions** page of hello wizard, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="800fd-130">![Gebruik scriptactie toocustomize een cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "toocustomize scriptactie gebruik een cluster")</span><span class="sxs-lookup"><span data-stu-id="800fd-130">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="800fd-131">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="800fd-131">Property</span></span></th><th><span data-ttu-id="800fd-132">Waarde</span><span class="sxs-lookup"><span data-stu-id="800fd-132">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="800fd-133">Naam</span><span class="sxs-lookup"><span data-stu-id="800fd-133">Name</span></span></td>
            <td><span data-ttu-id="800fd-134">Geef een naam voor de scriptactie Hallo.</span><span class="sxs-lookup"><span data-stu-id="800fd-134">Specify a name for hello script action.</span></span> <span data-ttu-id="800fd-135">Bijvoorbeeld: <b>installeren Giraph</b>.</span><span class="sxs-lookup"><span data-stu-id="800fd-135">For example, <b>Install Giraph</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="800fd-136">Script-URI</span><span class="sxs-lookup"><span data-stu-id="800fd-136">Script URI</span></span></td>
            <td><span data-ttu-id="800fd-137">Geef Hallo Uniform Resource Identifier (URI) toohello script is aangeroepen toocustomize Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="800fd-137">Specify hello Uniform Resource Identifier (URI) toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="800fd-138">Bijvoorbeeld: <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="800fd-138">For example, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="800fd-139">Soort knooppunt</span><span class="sxs-lookup"><span data-stu-id="800fd-139">Node Type</span></span></td>
            <td><span data-ttu-id="800fd-140">Geef Hallo knooppunten waarop Hallo aanpassing script wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="800fd-140">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="800fd-141">U kunt kiezen <b>alle knooppunten</b>, <b>hoofdknooppunten alleen</b>, of <b>Worker-knooppunten</b>.</span><span class="sxs-lookup"><span data-stu-id="800fd-141">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="800fd-142">Parameters</span><span class="sxs-lookup"><span data-stu-id="800fd-142">Parameters</span></span></td>
            <td><span data-ttu-id="800fd-143">Geef parameters op Hallo, indien vereist door het Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="800fd-143">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="800fd-144">Hallo script tooinstall Giraph vereist geen parameters, zodat u kunt dit leeg laten.</span><span class="sxs-lookup"><span data-stu-id="800fd-144">hello script tooinstall Giraph does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="800fd-145">U kunt meer dan één script actie tooinstall meerdere onderdelen toevoegen op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="800fd-145">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="800fd-146">Nadat u Hallo scripts hebt toegevoegd, klikt u op Hallo vinkje toostart Hallo cluster maken.</span><span class="sxs-lookup"><span data-stu-id="800fd-146">After you have added hello scripts, click hello checkmark toostart creating hello cluster.</span></span>

## <a name="use-giraph"></a><span data-ttu-id="800fd-147">Giraph gebruiken</span><span class="sxs-lookup"><span data-stu-id="800fd-147">Use Giraph</span></span>
<span data-ttu-id="800fd-148">We gebruiken Hallo SimpleShortestPathsComputation voorbeeld toodemonstrate Hallo basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementatie voor het vinden van Hallo kortste pad tussen de objecten in een grafiek.</span><span class="sxs-lookup"><span data-stu-id="800fd-148">We use hello SimpleShortestPathsComputation example toodemonstrate hello basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementation for finding hello shortest path between objects in a graph.</span></span> <span data-ttu-id="800fd-149">Gebruik hello te volgen stappen tooupload Hallo voorbeeld gegevens en Hallo voorbeeld jar, een taak uitvoert met behulp van Hallo SimpleShortestPathsComputation voorbeeld en Hallo-resultaten weergeven.</span><span class="sxs-lookup"><span data-stu-id="800fd-149">Use hello following steps tooupload hello sample data and hello sample jar, run a job by using hello SimpleShortestPathsComputation example, and then view hello results.</span></span>

1. <span data-ttu-id="800fd-150">Upload een sample data bestand tooAzure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="800fd-150">Upload a sample data file tooAzure Blob storage.</span></span> <span data-ttu-id="800fd-151">Maak een nieuw bestand met de naam op uw lokale werkstation **tiny_graph.txt**.</span><span class="sxs-lookup"><span data-stu-id="800fd-151">On your local workstation, create a new file named **tiny_graph.txt**.</span></span> <span data-ttu-id="800fd-152">Hallo volgende regels moet bevatten:</span><span class="sxs-lookup"><span data-stu-id="800fd-152">It should contain hello following lines:</span></span>

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    <span data-ttu-id="800fd-153">Upload Hallo tiny_graph.txt toohello primaire bestandsopslag voor uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="800fd-153">Upload hello tiny_graph.txt file toohello primary storage for your HDInsight cluster.</span></span> <span data-ttu-id="800fd-154">Voor instructies over het tooupload van gegevens, Zie [gegevens voor Hadoop-taken in HDInsight uploaden](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="800fd-154">For instructions on how tooupload data, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

    <span data-ttu-id="800fd-155">Deze gegevens beschrijft de relatie tussen de objecten in een gerichte grafiek, met behulp van notatie Hallo [bron\_-id, de bron\_waarde [[dest\_id], [rand\_waarde],...]]. Elke regel vertegenwoordigt een relatie tussen een **bron\_id** object en een of meer **dest\_id** objecten.</span><span class="sxs-lookup"><span data-stu-id="800fd-155">This data describes a relationship between objects in a directed graph, by using hello format [source\_id, source\_value,[[dest\_id], [edge\_value],...]]. Each line represents a relationship between a **source\_id** object and one or more **dest\_id** objects.</span></span> <span data-ttu-id="800fd-156">Hallo **rand\_waarde** (of gewicht) kunnen worden beschouwd als Hallo sterkte of de afstand van de verbinding tussen Hallo **source_id** en **dest\_id**.</span><span class="sxs-lookup"><span data-stu-id="800fd-156">hello **edge\_value** (or weight) can be thought of as hello strength or distance of hello connection between **source_id** and **dest\_id**.</span></span>

    <span data-ttu-id="800fd-157">Getekend, en het Hallo-waarde (of gewicht) gebruikt als Hallo afstand tussen de objecten, Hallo boven gegevens als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="800fd-157">Drawn out, and using hello value (or weight) as hello distance between objects, hello above data might look like this:</span></span>

    ![tiny_graph.txt getekend als cirkels met verschillende afstand tussen regels](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. <span data-ttu-id="800fd-159">Hallo SimpleShortestPathsComputation voorbeeld uitvoert.</span><span class="sxs-lookup"><span data-stu-id="800fd-159">Run hello SimpleShortestPathsComputation example.</span></span> <span data-ttu-id="800fd-160">Gebruik hello Azure PowerShell-cmdlets toorun Hallo voorbeeld te volgen met behulp van Hallo tiny_graph.txt bestand als invoer.</span><span class="sxs-lookup"><span data-stu-id="800fd-160">Use hello following Azure PowerShell cmdlets toorun hello example by using hello tiny_graph.txt file as input.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="800fd-161">Azure PowerShell-ondersteuning voor het beheer van HDInsight-resources met behulp van Azure Service Manager is **afgeschaft** en per 1 januari 2017 verdwenen.</span><span class="sxs-lookup"><span data-stu-id="800fd-161">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="800fd-162">Hallo stappen in dit document gebruiken Hallo nieuwe HDInsight-cmdlets die met Azure Resource Manager werken.</span><span class="sxs-lookup"><span data-stu-id="800fd-162">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="800fd-163">Volg de stappen Hallo in [installeren en configureren van Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall Hallo meest recente versie van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="800fd-163">Please follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="800fd-164">Als u scripts hebt die moeten toobe toouse Hallo nieuwe cmdlets die met Azure Resource Manager werken gewijzigd, Zie [migreren tooAzure ontwikkeling Resource Manager gebaseerde hulpprogramma's voor HDInsight-clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="800fd-164">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

    ```powershell
    $clusterName = "clustername"
    # Giraph examples jar
    $jarFile = "wasb:///example/jars/giraph-examples.jar"
    # Arguments for this job
    $jobArguments = "org.apache.giraph.examples.SimpleShortestPathsComputation",
                    "-ca", "mapred.job.tracker=headnodehost:9010",
                    "-vif", "org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat",
                    "-vip", "wasb:///example/data/tiny_graph.txt",
                    "-vof", "org.apache.giraph.io.formats.IdWithValueTextOutputFormat",
                    "-op",  "wasb:///example/output/shortestpaths",
                    "-w", "2"
    # Create hello definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run hello job, write output toohello Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    <span data-ttu-id="800fd-165">Vervang in Hallo hierboven voorbeeld **clustername** met Hallo-naam van uw HDInsight-cluster met Giraph geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="800fd-165">In hello above example, replace **clustername** with hello name of your HDInsight cluster that has Giraph installed.</span></span>
3. <span data-ttu-id="800fd-166">Hallo resultaten weergeven.</span><span class="sxs-lookup"><span data-stu-id="800fd-166">View hello results.</span></span> <span data-ttu-id="800fd-167">Zodra het Hallo-taak is voltooid, Hallo resultaten worden opgeslagen in twee uitvoerbestanden in Hallo **wasb: / / / voorbeeld/out/shotestpaths** map.</span><span class="sxs-lookup"><span data-stu-id="800fd-167">Once hello job has finished, hello results will be stored in two output files in hello **wasb:///example/out/shotestpaths** folder.</span></span> <span data-ttu-id="800fd-168">Hallo-bestanden worden genoemd **onderdeel-m-00001** en **onderdeel-m-00002**.</span><span class="sxs-lookup"><span data-stu-id="800fd-168">hello files are called **part-m-00001** and **part-m-00002**.</span></span> <span data-ttu-id="800fd-169">Volgende stappen toodownload en bekijkt hello uitvoer Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="800fd-169">Perform hello following steps toodownload and view hello output:</span></span>

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select hello current subscription
    Select-AzureSubscription $subscriptionName

    # Create hello Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download hello job output toohello workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    <span data-ttu-id="800fd-170">Hiermee maakt u Hallo **uitvoer-voorbeeld/shortestpaths** directorystructuur in de huidige map op uw werkstation en download Hallo twee bestanden toothat uitvoerlocatie Hallo.</span><span class="sxs-lookup"><span data-stu-id="800fd-170">This will create hello **example/output/shortestpaths** directory structure in hello current directory on your workstation, and download hello two output files toothat location.</span></span>

    <span data-ttu-id="800fd-171">Gebruik Hallo **Cat** cmdlet toodisplay Hallo inhoud van Hallo-bestanden:</span><span class="sxs-lookup"><span data-stu-id="800fd-171">Use hello **Cat** cmdlet toodisplay hello contents of hello files:</span></span>

        Cat example/output/shortestpaths/part*

    <span data-ttu-id="800fd-172">Hallo-uitvoer moet vergelijkbaar toohello volgende weergegeven:</span><span class="sxs-lookup"><span data-stu-id="800fd-172">hello output should appear similar toohello following:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="800fd-173">Hallo SimpleShortestPathComputation voorbeeld is vastgelegde toostart met object-ID 1 en Hallo kortste pad tooother objecten zoeken.</span><span class="sxs-lookup"><span data-stu-id="800fd-173">hello SimpleShortestPathComputation example is hard coded toostart with object ID 1 and find hello shortest path tooother objects.</span></span> <span data-ttu-id="800fd-174">Dus Hallo uitvoer moet worden gelezen als `destination_id distance`, waarbij afstand Hallo waarde (of gewicht) van Hallo randen afgelegd tussen object-ID 1 en Hallo doel-ID.</span><span class="sxs-lookup"><span data-stu-id="800fd-174">So hello output should be read as `destination_id distance`, where distance is hello value (or weight) of hello edges traveled between object ID 1 and hello target ID.</span></span>

    <span data-ttu-id="800fd-175">U kunt dit visualiseren, Hallo resultaten controleren door onderweg Hallo kortste paden tussen de 1-ID en alle andere objecten.</span><span class="sxs-lookup"><span data-stu-id="800fd-175">Visualizing this, you can verify hello results by traveling hello shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="800fd-176">Let op: Hallo kortste pad tussen ID 1 en 4-ID is 5.</span><span class="sxs-lookup"><span data-stu-id="800fd-176">Note that hello shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="800fd-177">Dit is de totale afstand Hallo tussen <span style="color:orange">ID 1 en 3</span>, en vervolgens <span style="color:red">ID 3 en 4</span>.</span><span class="sxs-lookup"><span data-stu-id="800fd-177">This is hello total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Tekenen van objecten als cirkels met de kortste paden tussen getekend](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a><span data-ttu-id="800fd-179">Giraph met Aure PowerShell installeren</span><span class="sxs-lookup"><span data-stu-id="800fd-179">Install Giraph using Aure PowerShell</span></span>
<span data-ttu-id="800fd-180">Zie [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="800fd-180">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="800fd-181">Hallo-voorbeeld laat zien hoe tooinstall Spark met Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="800fd-181">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="800fd-182">U moet toocustomize Hallo script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="800fd-182">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="install-giraph-using-net-sdk"></a><span data-ttu-id="800fd-183">Giraph met .NET SDK installeren</span><span class="sxs-lookup"><span data-stu-id="800fd-183">Install Giraph using .NET SDK</span></span>
<span data-ttu-id="800fd-184">Zie [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="800fd-184">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="800fd-185">Hallo-voorbeeld laat zien hoe tooinstall Spark met behulp van Hallo .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="800fd-185">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="800fd-186">U moet toocustomize Hallo script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="800fd-186">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="800fd-187">Zie ook</span><span class="sxs-lookup"><span data-stu-id="800fd-187">See also</span></span>
* [<span data-ttu-id="800fd-188">Giraph installeren op HDInsight Hadoop-clusters (Linux)</span><span class="sxs-lookup"><span data-stu-id="800fd-188">Install Giraph on HDInsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-giraph-install-linux.md)
* <span data-ttu-id="800fd-189">[Hadoop-clusters maken in HDInsight](hdinsight-provision-clusters.md): algemene informatie over het maken van HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="800fd-189">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="800fd-190">[HDInsight-cluster via scriptactie aanpassen][hdinsight-cluster-customize]: algemene informatie over het aanpassen van HDInsight-clusters met behulp van de scriptactie.</span><span class="sxs-lookup"><span data-stu-id="800fd-190">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="800fd-191">[Scriptactie-scripts ontwikkelen voor HDInsight](hdinsight-hadoop-script-actions.md).</span><span class="sxs-lookup"><span data-stu-id="800fd-191">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="800fd-192">[Installeren en gebruiken van Spark in HDInsight-clusters][hdinsight-install-spark]: scriptactie voorbeeld over het installeren van Spark.</span><span class="sxs-lookup"><span data-stu-id="800fd-192">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="800fd-193">[R installeren op HDInsight-clusters][hdinsight-install-r]: scriptactie voorbeeld over het installeren van R.</span><span class="sxs-lookup"><span data-stu-id="800fd-193">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="800fd-194">[Solr installeren op HDInsight-clusters](hdinsight-hadoop-solr-install.md): scriptactie voorbeeld over het installeren van Solr.</span><span class="sxs-lookup"><span data-stu-id="800fd-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install.md): Script Action sample about installing Solr.</span></span>

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
