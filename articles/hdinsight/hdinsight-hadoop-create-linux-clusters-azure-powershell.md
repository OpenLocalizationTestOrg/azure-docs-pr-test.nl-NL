---
title: aaaCreate Hadoop-clusters met behulp van PowerShell - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toocreate Hadoop, HBase, Storm of Spark-clusters op Linux voor HDInsight met behulp van Azure PowerShell.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4208deca-d64a-45e1-8948-2673d5d7678c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 53afe4702f6b61a0720ceda48a4a34d7fa8797d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a><span data-ttu-id="cab7f-103">Op basis van Linux-clusters maken in HDInsight met behulp van Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cab7f-103">Create Linux-based clusters in HDInsight using Azure PowerShell</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="cab7f-104">Azure PowerShell is een krachtige scriptomgeving toocontrol gebruiken en automatiseren Hallo-implementatie en beheer van uw werkbelastingen in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="cab7f-104">Azure PowerShell is a powerful scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Microsoft Azure.</span></span> <span data-ttu-id="cab7f-105">Dit document bevat informatie over hoe toocreate een op Linux gebaseerde HDInsight-cluster met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cab7f-105">This document provides information about how toocreate a Linux-based HDInsight cluster by using Azure PowerShell.</span></span> <span data-ttu-id="cab7f-106">Dit omvat ook een voorbeeldscript.</span><span class="sxs-lookup"><span data-stu-id="cab7f-106">It also includes an example script.</span></span>

> [!NOTE]
> <span data-ttu-id="cab7f-107">Azure PowerShell is alleen beschikbaar op Windows-clients.</span><span class="sxs-lookup"><span data-stu-id="cab7f-107">Azure PowerShell is only available on Windows clients.</span></span> <span data-ttu-id="cab7f-108">Als u van een Linux-, Unix- of Mac OS X-client gebruikmaakt, Zie [maken van een Linux gebaseerde HDInsight-cluster met Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) voor informatie over het gebruik van hello Azure CLI toocreate een cluster.</span><span class="sxs-lookup"><span data-stu-id="cab7f-108">If you are using a Linux, Unix, or Mac OS X client, see [Create a Linux-based HDInsight cluster using Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) for information about using hello Azure CLI toocreate a cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cab7f-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="cab7f-109">Prerequisites</span></span>
<span data-ttu-id="cab7f-110">Hallo volgende voordat u deze procedure begint, moet u hebben:</span><span class="sxs-lookup"><span data-stu-id="cab7f-110">You must have hello following before starting this procedure:</span></span>

* <span data-ttu-id="cab7f-111">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="cab7f-111">An Azure subscription.</span></span> <span data-ttu-id="cab7f-112">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="cab7f-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* [<span data-ttu-id="cab7f-113">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cab7f-113">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > <span data-ttu-id="cab7f-114">Azure PowerShell-ondersteuning voor het beheer van HDInsight-resources met behulp van Azure Service Manager is **afgeschaft** en per 1 januari 2017 verdwenen.</span><span class="sxs-lookup"><span data-stu-id="cab7f-114">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="cab7f-115">Hallo stappen in dit document gebruiken Hallo nieuwe HDInsight-cmdlets die met Azure Resource Manager werken.</span><span class="sxs-lookup"><span data-stu-id="cab7f-115">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="cab7f-116">Volg de stappen Hallo in [Azure PowerShell installeren](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall Hallo meest recente versie van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="cab7f-116">Please follow hello steps in [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="cab7f-117">Als u scripts hebt die moeten toobe toouse Hallo nieuwe cmdlets die met Azure Resource Manager werken gewijzigd, Zie [migreren tooAzure ontwikkeling Resource Manager gebaseerde hulpprogramma's voor HDInsight-clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="cab7f-117">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

## <a name="create-cluster"></a><span data-ttu-id="cab7f-118">Cluster maken</span><span class="sxs-lookup"><span data-stu-id="cab7f-118">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="cab7f-119">toocreate een HDInsight-cluster met behulp van Azure PowerShell, moet u Hallo procedures te volgen:</span><span class="sxs-lookup"><span data-stu-id="cab7f-119">toocreate an HDInsight cluster by using Azure PowerShell, you must complete hello following procedures:</span></span>

* <span data-ttu-id="cab7f-120">Een Azure-resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="cab7f-120">Create an Azure resource group</span></span>
* <span data-ttu-id="cab7f-121">Een Azure Storage-account maken</span><span class="sxs-lookup"><span data-stu-id="cab7f-121">Create an Azure Storage account</span></span>
* <span data-ttu-id="cab7f-122">Een Azure Blob-container maken</span><span class="sxs-lookup"><span data-stu-id="cab7f-122">Create an Azure Blob container</span></span>
* <span data-ttu-id="cab7f-123">Een HDInsight-cluster maken</span><span class="sxs-lookup"><span data-stu-id="cab7f-123">Create an HDInsight cluster</span></span>

<span data-ttu-id="cab7f-124">Hallo volgende script laat zien hoe een nieuw cluster toocreate:</span><span class="sxs-lookup"><span data-stu-id="cab7f-124">hello following script demonstrates how toocreate a new cluster:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]

<span data-ttu-id="cab7f-125">Hallo-waarden die u voor Hallo cluster aanmelding opgeeft zijn gebruikte toocreate hello Hadoop-gebruikersaccount voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="cab7f-125">hello values you specify for hello cluster login are used toocreate hello Hadoop user account for hello cluster.</span></span> <span data-ttu-id="cab7f-126">Gebruik dit account tooconnect tooservices gehost op Hallo cluster zoals web-UI of REST-API's.</span><span class="sxs-lookup"><span data-stu-id="cab7f-126">Use this account tooconnect tooservices hosted on hello cluster such as web UIs or REST APIs.</span></span>

<span data-ttu-id="cab7f-127">Hallo-waarden die u opgeeft voor de SSH-gebruiker Hallo zijn gebruikte toocreate Hallo SSH-gebruiker voor Hallo cluster.</span><span class="sxs-lookup"><span data-stu-id="cab7f-127">hello values you specify for hello SSH user are used toocreate hello SSH user for hello cluster.</span></span> <span data-ttu-id="cab7f-128">Gebruik dit account toostart een externe SSH-sessie op Hallo-cluster en taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="cab7f-128">Use this account toostart a remote SSH session on hello cluster and run jobs.</span></span> <span data-ttu-id="cab7f-129">Zie voor meer informatie, Hallo [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="cab7f-129">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cab7f-130">Als u van plan bent toouse meer dan 32 worker-knooppunten (bij het maken van een cluster maken of door vergroten/verkleinen Hallo cluster na aanmaak), moet u ook een hoofdknooppunt grootte opgeven met ten minste 8 kerngeheugens en 14 GB RAM-geheugen.</span><span class="sxs-lookup"><span data-stu-id="cab7f-130">If you plan toouse more than 32 worker nodes (either at cluster creation or by scaling hello cluster after creation), you must also specify a head node size with at least 8 cores and 14 GB of RAM.</span></span>
>
> <span data-ttu-id="cab7f-131">Zie voor meer informatie over knooppuntgrootten en bijbehorende kosten [HDInsight prijzen](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="cab7f-131">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="cab7f-132">Kan duren too20 minuten toocreate een cluster.</span><span class="sxs-lookup"><span data-stu-id="cab7f-132">It can take up too20 minutes toocreate a cluster.</span></span>

## <a name="create-cluster-configuration-object"></a><span data-ttu-id="cab7f-133">Cluster maken: Configuration-object</span><span class="sxs-lookup"><span data-stu-id="cab7f-133">Create cluster: Configuration object</span></span>

<span data-ttu-id="cab7f-134">U kunt ook maken voor een HDInsight configuration-object met behulp `New-AzureRmHDInsightClusterConfig` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="cab7f-134">You can also create an HDInsight configuration object using `New-AzureRmHDInsightClusterConfig` cmdlet.</span></span> <span data-ttu-id="cab7f-135">U kunt deze configuratie object tooenable extra configuratieopties voor uw cluster wijzigen.</span><span class="sxs-lookup"><span data-stu-id="cab7f-135">You can then modify this configuration object tooenable additional configuration options for your cluster.</span></span> <span data-ttu-id="cab7f-136">Gebruik tot slot Hallo `-Config` parameter Hallo `New-AzureRmHDInsightCluster` cmdlet toouse Hallo configuratie.</span><span class="sxs-lookup"><span data-stu-id="cab7f-136">Finally, use hello `-Config` parameter of hello `New-AzureRmHDInsightCluster` cmdlet toouse hello configuration.</span></span>

<span data-ttu-id="cab7f-137">Hallo volgende script maakt een object configuratie tooconfigure een R Server voor het type van HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="cab7f-137">hello following script creates a configuration object tooconfigure an R Server on HDInsight cluster type.</span></span> <span data-ttu-id="cab7f-138">Hallo-configuratie kan een edge-knooppunt, RStudio en een extra storage-account.</span><span class="sxs-lookup"><span data-stu-id="cab7f-138">hello configuration enables an edge node, RStudio, and an additional storage account.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]

> [!WARNING]
> <span data-ttu-id="cab7f-139">Met behulp van een opslagaccount in een andere locatie dan Hallo HDInsight-cluster wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="cab7f-139">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span> <span data-ttu-id="cab7f-140">Wanneer u in dit voorbeeld, Hallo aanvullende storage-account maken in Hallo dezelfde locatie als het Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="cab7f-140">When using this example, create hello additional storage account in hello same location as hello server.</span></span>

## <a name="customize-clusters"></a><span data-ttu-id="cab7f-141">Clusters aanpassen</span><span class="sxs-lookup"><span data-stu-id="cab7f-141">Customize clusters</span></span>

* <span data-ttu-id="cab7f-142">Zie [aanpassen HDInsight-clusters met behulp van de Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="cab7f-142">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span></span>
* <span data-ttu-id="cab7f-143">Zie [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="cab7f-143">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="cab7f-144">Hallo-cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="cab7f-144">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="cab7f-145">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="cab7f-145">Troubleshoot</span></span>

<span data-ttu-id="cab7f-146">Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) als u problemen ondervindt met het maken van HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="cab7f-146">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cab7f-147">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cab7f-147">Next steps</span></span>

<span data-ttu-id="cab7f-148">Nu u een HDInsight-cluster hebt gemaakt, gebruiken Hallo hoe resources toolearn na toowork met uw cluster.</span><span class="sxs-lookup"><span data-stu-id="cab7f-148">Now that you have successfully created an HDInsight cluster, use hello following resources toolearn how toowork with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="cab7f-149">Hadoop-clusters</span><span class="sxs-lookup"><span data-stu-id="cab7f-149">Hadoop clusters</span></span>

* [<span data-ttu-id="cab7f-150">Hive gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="cab7f-150">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="cab7f-151">Pig gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="cab7f-151">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="cab7f-152">MapReduce gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="cab7f-152">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="cab7f-153">HBase-clusters</span><span class="sxs-lookup"><span data-stu-id="cab7f-153">HBase clusters</span></span>

* [<span data-ttu-id="cab7f-154">Aan de slag met HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="cab7f-154">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="cab7f-155">Ontwikkelen van Java-toepassingen voor HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="cab7f-155">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="cab7f-156">Storm-clusters</span><span class="sxs-lookup"><span data-stu-id="cab7f-156">Storm clusters</span></span>

* [<span data-ttu-id="cab7f-157">Java-topologieën ontwikkelen voor Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="cab7f-157">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="cab7f-158">Python-onderdelen in Storm op HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="cab7f-158">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="cab7f-159">Implementeren en bewaken topologieën met Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="cab7f-159">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="cab7f-160">Spark-clusters</span><span class="sxs-lookup"><span data-stu-id="cab7f-160">Spark clusters</span></span>

* [<span data-ttu-id="cab7f-161">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="cab7f-161">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="cab7f-162">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="cab7f-162">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="cab7f-163">Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools</span><span class="sxs-lookup"><span data-stu-id="cab7f-163">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="cab7f-164">Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken</span><span class="sxs-lookup"><span data-stu-id="cab7f-164">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="cab7f-165">Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen</span><span class="sxs-lookup"><span data-stu-id="cab7f-165">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

