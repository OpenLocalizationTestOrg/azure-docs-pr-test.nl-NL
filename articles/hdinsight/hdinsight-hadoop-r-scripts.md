---
title: aaaUse R clusters in HDInsight toocustomize - Azure | Microsoft Docs
description: Meer informatie over hoe tooinstall R met behulp van scripts en gebruik R op HDInsight-clusters.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: be851270-afa5-4af0-a69e-2d343a4deeb7
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: bf5adf2e18dc43a743b29fd1567fad731b9c3ab7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-r-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="d4b94-103">R installeren en gebruiken op HDInsight Hadoop-clusters</span><span class="sxs-lookup"><span data-stu-id="d4b94-103">Install and use R on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="d4b94-104">Informatie over hoe Windows toocustomize op basis van HDInsight-cluster met R met behulp van de scriptactie en hoe toouse R op HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="d4b94-104">Learn how toocustomize Windows based HDInsight cluster with R using Script Action, and how toouse R on HDInsight clusters.</span></span> <span data-ttu-id="d4b94-105">Hallo [HDInsight aanbieding](https://azure.microsoft.com/pricing/details/hdinsight/) R Server als onderdeel van uw HDInsight-cluster bevat.</span><span class="sxs-lookup"><span data-stu-id="d4b94-105">hello [HDInsight offering](https://azure.microsoft.com/pricing/details/hdinsight/) includes R Server as part of your HDInsight cluster.</span></span> <span data-ttu-id="d4b94-106">Hierdoor kan R scripts toouse MapReduce en Spark toorun gedistribueerd berekeningen.</span><span class="sxs-lookup"><span data-stu-id="d4b94-106">This allows R scripts toouse MapReduce and Spark toorun distributed computations.</span></span> <span data-ttu-id="d4b94-107">Zie [Aan de slag met R Server in HDInsight](hdinsight-hadoop-r-server-get-started.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="d4b94-107">For more information, see [Get started using R Server on HDInsight](hdinsight-hadoop-r-server-get-started.md).</span></span> <span data-ttu-id="d4b94-108">Zie voor meer informatie over het gebruik van R met een cluster op basis van Linux [installeert en gebruikt R op HDinsight Hadoop-clusters (Linux)](hdinsight-hadoop-r-scripts-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d4b94-108">For information on using R with a Linux-based cluster, see [Install and use R on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-r-scripts-linux.md).</span></span>

<span data-ttu-id="d4b94-109">U kunt R installeren op elk type (Hadoop, Storm, HBase, Spark)-cluster in Azure HDInsight met behulp van *scriptactie*.</span><span class="sxs-lookup"><span data-stu-id="d4b94-109">You can install R on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="d4b94-110">Een voorbeeld script tooinstall R op een HDInsight-cluster is beschikbaar via een alleen-lezen Azure storage-blob op [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span><span class="sxs-lookup"><span data-stu-id="d4b94-110">A sample script tooinstall R on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

<span data-ttu-id="d4b94-111">**Verwante artikelen**</span><span class="sxs-lookup"><span data-stu-id="d4b94-111">**Related articles**</span></span>

* [<span data-ttu-id="d4b94-112">Installeren en gebruiken van R op HDinsight Hadoop-clusters (Linux)</span><span class="sxs-lookup"><span data-stu-id="d4b94-112">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="d4b94-113">[Hadoop-clusters maken in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): algemene informatie over het maken van HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="d4b94-113">[Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="d4b94-114">[HDInsight-cluster via scriptactie aanpassen][hdinsight-cluster-customize]: algemene informatie over het aanpassen van HDInsight-clusters met behulp van de scriptactie</span><span class="sxs-lookup"><span data-stu-id="d4b94-114">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="d4b94-115">Scriptactie-scripts ontwikkelen voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="d4b94-115">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)

## <a name="what-is-r"></a><span data-ttu-id="d4b94-116">Wat is R?</span><span class="sxs-lookup"><span data-stu-id="d4b94-116">What is R?</span></span>
<span data-ttu-id="d4b94-117">Hallo <a href="http://www.r-project.org/" target="_blank">R-Project voor statistische Computing</a> is een open source-taal en de omgeving voor statistische computing.</span><span class="sxs-lookup"><span data-stu-id="d4b94-117">hello <a href="http://www.r-project.org/" target="_blank">R Project for Statistical Computing</a> is an open source language and environment for statistical computing.</span></span> <span data-ttu-id="d4b94-118">R biedt honderden build in statistische functies en een eigen programmeertaal die aspecten van het functionele en objectgeoriënteerd programmeren combineert.</span><span class="sxs-lookup"><span data-stu-id="d4b94-118">R provides hundreds of build-in statistical functions and its own programming language that combines aspects of functional and object-oriented programming.</span></span> <span data-ttu-id="d4b94-119">Het bevat ook uitgebreide grafische mogelijkheden.</span><span class="sxs-lookup"><span data-stu-id="d4b94-119">It also provides extensive graphical capabilities.</span></span> <span data-ttu-id="d4b94-120">R is Hallo voorkeur programmeeromgeving voor de meeste professionele statistici en verzameld in een groot aantal velden.</span><span class="sxs-lookup"><span data-stu-id="d4b94-120">R is hello preferred programming environment for most professional statisticians and scientists in a wide variety of fields.</span></span>

<span data-ttu-id="d4b94-121">R is compatibel met Azure Blob Storage (WASB) zodat er opgeslagen gegevens kunnen worden verwerkt met behulp van R op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d4b94-121">R is compatible with Azure Blob Storage (WASB) so that data that is stored there can be processed using R on HDInsight.</span></span>  

## <a name="install-r"></a><span data-ttu-id="d4b94-122">R installeren</span><span class="sxs-lookup"><span data-stu-id="d4b94-122">Install R</span></span>
<span data-ttu-id="d4b94-123">Een [voorbeeldscript](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) tooinstall R op een HDInsight-cluster is beschikbaar via een alleen-lezen blob in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="d4b94-123">A [sample script](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1) tooinstall R on an HDInsight cluster is available from a read-only blob in Azure Storage.</span></span> <span data-ttu-id="d4b94-124">Deze sectie bevat instructies over hoe toouse voorbeeldscript Hallo tijdens het Hallo-cluster met behulp van hello Azure Portal maken.</span><span class="sxs-lookup"><span data-stu-id="d4b94-124">This section provides instructions about how toouse hello sample script while creating hello cluster using hello Azure Portal.</span></span>

> [!NOTE]
> <span data-ttu-id="d4b94-125">Hallo-voorbeeldscript is geïntroduceerd in HDInsight-cluster versie 3.1.</span><span class="sxs-lookup"><span data-stu-id="d4b94-125">hello sample script was introduced with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="d4b94-126">Zie voor meer informatie over de versies van HDInsight-cluster [versies van HDInsight-cluster](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="d4b94-126">For more information about  HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>
>
>

1. <span data-ttu-id="d4b94-127">Wanneer u een HDInsight-cluster van Hallo Portal maakt, klikt u op **optionele configuratie**, en klik vervolgens op **scriptacties**.</span><span class="sxs-lookup"><span data-stu-id="d4b94-127">When you create an HDInsight cluster from hello Portal, click **Optional Configuration**, and then click **Script Actions**.</span></span>
2. <span data-ttu-id="d4b94-128">Op Hallo **scriptacties** pagina, voert u Hallo volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="d4b94-128">On hello **Script Actions** page, enter hello following values:</span></span>

    <span data-ttu-id="d4b94-129">![Gebruik scriptactie toocustomize een cluster](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "toocustomize scriptactie gebruik een cluster")</span><span class="sxs-lookup"><span data-stu-id="d4b94-129">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-r-scripts/hdi-r-script-action.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="d4b94-130">Eigenschap</span><span class="sxs-lookup"><span data-stu-id="d4b94-130">Property</span></span></th><th><span data-ttu-id="d4b94-131">Waarde</span><span class="sxs-lookup"><span data-stu-id="d4b94-131">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="d4b94-132">Naam</span><span class="sxs-lookup"><span data-stu-id="d4b94-132">Name</span></span></td>
            <td><span data-ttu-id="d4b94-133">Geef een naam voor de scriptactie hello, bijvoorbeeld <b>R installeren</b>.</span><span class="sxs-lookup"><span data-stu-id="d4b94-133">Specify a name for hello script action, for example, <b>Install R</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="d4b94-134">Script-URI</span><span class="sxs-lookup"><span data-stu-id="d4b94-134">Script URI</span></span></td>
            <td><span data-ttu-id="d4b94-135">Geef Hallo URI toohello script op dat is aangeroepen toocustomize Hallo cluster, bijvoorbeeld <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></span><span class="sxs-lookup"><span data-stu-id="d4b94-135">Specify hello URI toohello script that is invoked toocustomize hello cluster, for example, <i>https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="d4b94-136">Soort knooppunt</span><span class="sxs-lookup"><span data-stu-id="d4b94-136">Node Type</span></span></td>
            <td><span data-ttu-id="d4b94-137">Geef Hallo knooppunten waarop Hallo aanpassing script wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="d4b94-137">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="d4b94-138">U kunt kiezen <b>alle knooppunten</b>, <b>hoofdknooppunten alleen</b>, of <b>Worker-knooppunten</b> alleen.</span><span class="sxs-lookup"><span data-stu-id="d4b94-138">You can choose <b>All Nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes</b> only.</span></span>
        <tr><td><span data-ttu-id="d4b94-139">Parameters</span><span class="sxs-lookup"><span data-stu-id="d4b94-139">Parameters</span></span></td>
            <td><span data-ttu-id="d4b94-140">Geef parameters op Hallo, indien vereist door het Hallo-script.</span><span class="sxs-lookup"><span data-stu-id="d4b94-140">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="d4b94-141">Hallo script tooinstall R is echter geen parameters, vereist zodat u kunt dit leeg laten.</span><span class="sxs-lookup"><span data-stu-id="d4b94-141">However, hello script tooinstall R does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="d4b94-142">U kunt meer dan één script actie tooinstall meerdere onderdelen toevoegen op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="d4b94-142">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="d4b94-143">Nadat u Hallo scripts hebt toegevoegd, klikt u op Hallo vinkje toostart crating Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="d4b94-143">After you have added hello scripts, click hello check mark toostart crating hello cluster.</span></span>

<span data-ttu-id="d4b94-144">U kunt ook Hallo script tooinstall R gebruiken in HDInsight met behulp van Azure PowerShell of Hallo HDInsight .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="d4b94-144">You can also use hello script tooinstall R on HDInsight by using Azure PowerShell or hello HDInsight .NET SDK.</span></span> <span data-ttu-id="d4b94-145">Instructies voor deze procedures vindt u verderop in dit artikel.</span><span class="sxs-lookup"><span data-stu-id="d4b94-145">Instructions for these procedures are provided later in this article.</span></span>

## <a name="run-r-scripts"></a><span data-ttu-id="d4b94-146">R-scripts uitvoeren</span><span class="sxs-lookup"><span data-stu-id="d4b94-146">Run R scripts</span></span>
<span data-ttu-id="d4b94-147">Deze sectie beschrijft hoe toorun een R-script op Hallo Hadoop-cluster met HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d4b94-147">This section describes how toorun an R script on hello Hadoop cluster with HDInsight.</span></span>

1. <span data-ttu-id="d4b94-148">**Een cluster toohello van extern bureaublad-verbinding tot stand brengen**: vanaf Hallo Portal, extern bureaublad inschakelen voor Hallo cluster die u hebt gemaakt met R is geïnstalleerd en vervolgens verbinding toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="d4b94-148">**Establish a Remote Desktop connection toohello cluster**: From hello Portal, enable Remote Desktop for hello cluster you created with R installed, and then connect toohello cluster.</span></span> <span data-ttu-id="d4b94-149">Zie voor instructies [tooHDInsight clusters met RDP verbinding](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="d4b94-149">For instructions, see [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="d4b94-150">**Open Hallo R console**: Hallo R-installatie plaatst u een koppeling toohello R-console op Hallo bureaublad van Hallo hoofdknooppunt.</span><span class="sxs-lookup"><span data-stu-id="d4b94-150">**Open hello R console**: hello R installation puts a link toohello R console on hello desktop of hello head node.</span></span> <span data-ttu-id="d4b94-151">Klik op het tooopen Hallo R-console.</span><span class="sxs-lookup"><span data-stu-id="d4b94-151">Click on it tooopen hello R console.</span></span>
3. <span data-ttu-id="d4b94-152">**Hallo R-script uitvoeren**: Hallo R-script rechtstreeks vanuit Hallo R-console kan worden uitgevoerd door plakken, te selecteren en op ENTER te drukken.</span><span class="sxs-lookup"><span data-stu-id="d4b94-152">**Run hello R script**: hello R script can be run directly from hello R console by pasting it, selecting it, and pressing ENTER.</span></span> <span data-ttu-id="d4b94-153">Hier volgt een eenvoudig voorbeeld-script dat Hallo getallen van 1 too100 genereert en vervolgens wordt vermenigvuldigd met 2.</span><span class="sxs-lookup"><span data-stu-id="d4b94-153">Here is a simple example script that generates hello numbers 1 too100 and then multiplies them by 2.</span></span>

        library(rmr2)
        library(rhdfs)
        ints = to.dfs(1:100)
        calc = mapreduce(input = ints, map = function(k, v) cbind(v, 2*v))
        from.dfs(calc)

<span data-ttu-id="d4b94-154">Hallo eerste twee regels aanroep Hallo RHadoop bibliotheken zijn geïnstalleerd met R. Hallo laatste regel afdrukken bestellen Hallo resultaten toohello console.</span><span class="sxs-lookup"><span data-stu-id="d4b94-154">hello first two lines call hello RHadoop libraries that are installed with R. hello final line prints hello results toohello console.</span></span> <span data-ttu-id="d4b94-155">Hallo-uitvoer ziet er als volgt:</span><span class="sxs-lookup"><span data-stu-id="d4b94-155">hello output should look like this:</span></span>

    [1,]  1 2
    [2,]  2 4
    .
    .
    .
    [98,]  98 196
    [99,]  99 198
    [100,] 100 200


## <a name="install-r-using-aure-powershell"></a><span data-ttu-id="d4b94-156">R met Aure PowerShell installeren</span><span class="sxs-lookup"><span data-stu-id="d4b94-156">Install R using Aure PowerShell</span></span>
<span data-ttu-id="d4b94-157">Zie [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="d4b94-157">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="d4b94-158">Hallo-voorbeeld laat zien hoe tooinstall Spark met Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d4b94-158">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="d4b94-159">U moet toocustomize Hallo script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span><span class="sxs-lookup"><span data-stu-id="d4b94-159">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1).</span></span>

## <a name="install-r-using-net-sdk"></a><span data-ttu-id="d4b94-160">R met .NET SDK installeren</span><span class="sxs-lookup"><span data-stu-id="d4b94-160">Install R using .NET SDK</span></span>
<span data-ttu-id="d4b94-161">Zie [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="d4b94-161">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="d4b94-162">Hallo-voorbeeld laat zien hoe tooinstall Spark met behulp van Hallo .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="d4b94-162">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="d4b94-163">U moet toocustomize Hallo script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).</span><span class="sxs-lookup"><span data-stu-id="d4b94-163">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps1](https://hdiconfigactions.blob.core.windows.net/rconfigactionv02/r-installer-v02.ps11).</span></span>

## <a name="see-also"></a><span data-ttu-id="d4b94-164">Zie ook</span><span class="sxs-lookup"><span data-stu-id="d4b94-164">See also</span></span>
* [<span data-ttu-id="d4b94-165">Installeren en gebruiken van R op HDinsight Hadoop-clusters (Linux)</span><span class="sxs-lookup"><span data-stu-id="d4b94-165">Install and use R on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-r-scripts-linux.md)
* <span data-ttu-id="d4b94-166">[Hadoop-clusters maken in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): algemene informatie over het maken van HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="d4b94-166">[Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): general information on creating HDInsight clusters</span></span>
* <span data-ttu-id="d4b94-167">[HDInsight-cluster via scriptactie aanpassen][hdinsight-cluster-customize]: algemene informatie over het aanpassen van HDInsight-clusters met behulp van de scriptactie</span><span class="sxs-lookup"><span data-stu-id="d4b94-167">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action</span></span>
* [<span data-ttu-id="d4b94-168">Scriptactie-scripts ontwikkelen voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="d4b94-168">Develop Script Action scripts for HDInsight</span></span>](hdinsight-hadoop-script-actions.md)
* <span data-ttu-id="d4b94-169">[Installeren en gebruiken van Spark in HDInsight-clusters][hdinsight-install-spark]: scriptactie voorbeeld over het installeren van Spark</span><span class="sxs-lookup"><span data-stu-id="d4b94-169">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark</span></span>
* <span data-ttu-id="d4b94-170">[Giraph installeren op HDInsight-clusters](hdinsight-hadoop-giraph-install.md): scriptactie voorbeeld over het installeren van Giraph</span><span class="sxs-lookup"><span data-stu-id="d4b94-170">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph</span></span>
* <span data-ttu-id="d4b94-171">[Solr installeren op HDInsight-clusters](hdinsight-hadoop-solr-install-linux.md): scriptactie voorbeeld over het installeren van Solr.</span><span class="sxs-lookup"><span data-stu-id="d4b94-171">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md): Script Action sample about installing Solr.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: ../hdinsight-provision-clusters/
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
[hdinsight-install-spark]: hdinsight-apache-spark-jupyter-spark-sql.md
