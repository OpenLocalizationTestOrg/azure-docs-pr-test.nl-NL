---
title: Met behulp van PowerShell - Azure HDInsight Hadoop-clusters maken | Microsoft Docs
description: Informatie over het maken van Hadoop, HBase, Storm of Spark-clusters op Linux voor HDInsight met behulp van Azure PowerShell.
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
ms.openlocfilehash: ca75974e6ec4f60739137d4cb5458bbfd735de3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a><span data-ttu-id="3aefb-103">Op basis van Linux-clusters maken in HDInsight met behulp van Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3aefb-103">Create Linux-based clusters in HDInsight using Azure PowerShell</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="3aefb-104">Azure PowerShell is een krachtige scriptomgeving op servers die u gebruiken kunt om te beheren en de implementatie en beheer van uw werkbelastingen in Microsoft Azure automatiseren.</span><span class="sxs-lookup"><span data-stu-id="3aefb-104">Azure PowerShell is a powerful scripting environment that you can use to control and automate the deployment and management of your workloads in Microsoft Azure.</span></span> <span data-ttu-id="3aefb-105">Dit document bevat informatie over het maken van een Linux gebaseerde HDInsight-cluster met behulp van Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3aefb-105">This document provides information about how to create a Linux-based HDInsight cluster by using Azure PowerShell.</span></span> <span data-ttu-id="3aefb-106">Dit omvat ook een voorbeeldscript.</span><span class="sxs-lookup"><span data-stu-id="3aefb-106">It also includes an example script.</span></span>

> [!NOTE]
> <span data-ttu-id="3aefb-107">Azure PowerShell is alleen beschikbaar op Windows-clients.</span><span class="sxs-lookup"><span data-stu-id="3aefb-107">Azure PowerShell is only available on Windows clients.</span></span> <span data-ttu-id="3aefb-108">Als u van een Linux-, Unix- of Mac OS X-client gebruikmaakt, Zie [maken van een Linux gebaseerde HDInsight-cluster met Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) voor informatie over het gebruik van de Azure CLI om een cluster te maken.</span><span class="sxs-lookup"><span data-stu-id="3aefb-108">If you are using a Linux, Unix, or Mac OS X client, see [Create a Linux-based HDInsight cluster using Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) for information about using the Azure CLI to create a cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3aefb-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3aefb-109">Prerequisites</span></span>
<span data-ttu-id="3aefb-110">Hiervoor hebt u het volgende voordat u deze procedure begint:</span><span class="sxs-lookup"><span data-stu-id="3aefb-110">You must have the following before starting this procedure:</span></span>

* <span data-ttu-id="3aefb-111">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="3aefb-111">An Azure subscription.</span></span> <span data-ttu-id="3aefb-112">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="3aefb-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* [<span data-ttu-id="3aefb-113">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3aefb-113">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > <span data-ttu-id="3aefb-114">Azure PowerShell-ondersteuning voor het beheer van HDInsight-resources met behulp van Azure Service Manager is **afgeschaft** en per 1 januari 2017 verdwenen.</span><span class="sxs-lookup"><span data-stu-id="3aefb-114">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="3aefb-115">In de stappen in dit document worden de nieuwe HDInsight-cmdlets gebruikt die met Azure Resource Manager werken.</span><span class="sxs-lookup"><span data-stu-id="3aefb-115">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="3aefb-116">Volg de stappen in [Azure PowerShell installeren](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) de meest recente versie van Azure PowerShell installeren.</span><span class="sxs-lookup"><span data-stu-id="3aefb-116">Please follow the steps in [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="3aefb-117">Als u scripts hebt die moeten worden gewijzigd om ze te kunnen gebruiken met de nieuwe cmdlets die werken met Azure Resource Manager, raadpleegt u [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) (Migreren naar op Azure Resource Manager gebaseerde hulpprogramma’s voor HDInsight-clusters) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3aefb-117">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

## <a name="create-cluster"></a><span data-ttu-id="3aefb-118">Cluster maken</span><span class="sxs-lookup"><span data-stu-id="3aefb-118">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="3aefb-119">Voor het maken van een HDInsight-cluster met behulp van Azure PowerShell, moet u de volgende procedures uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="3aefb-119">To create an HDInsight cluster by using Azure PowerShell, you must complete the following procedures:</span></span>

* <span data-ttu-id="3aefb-120">Een Azure-resourcegroep maken</span><span class="sxs-lookup"><span data-stu-id="3aefb-120">Create an Azure resource group</span></span>
* <span data-ttu-id="3aefb-121">Een Azure Storage-account maken</span><span class="sxs-lookup"><span data-stu-id="3aefb-121">Create an Azure Storage account</span></span>
* <span data-ttu-id="3aefb-122">Een Azure Blob-container maken</span><span class="sxs-lookup"><span data-stu-id="3aefb-122">Create an Azure Blob container</span></span>
* <span data-ttu-id="3aefb-123">Een HDInsight-cluster maken</span><span class="sxs-lookup"><span data-stu-id="3aefb-123">Create an HDInsight cluster</span></span>

<span data-ttu-id="3aefb-124">Het volgende script laat zien hoe u een nieuw cluster maken:</span><span class="sxs-lookup"><span data-stu-id="3aefb-124">The following script demonstrates how to create a new cluster:</span></span>

<span data-ttu-id="3aefb-125">[!code-powershell[belangrijkste](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]</span><span class="sxs-lookup"><span data-stu-id="3aefb-125">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]</span></span>

<span data-ttu-id="3aefb-126">De waarden die u voor de aanmelding van de cluster opgeeft worden gebruikt voor het maken van het Hadoop-gebruikersaccount voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="3aefb-126">The values you specify for the cluster login are used to create the Hadoop user account for the cluster.</span></span> <span data-ttu-id="3aefb-127">Dit account verbinding maken met services die worden gehost op het cluster, zoals web UI of REST-API's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3aefb-127">Use this account to connect to services hosted on the cluster such as web UIs or REST APIs.</span></span>

<span data-ttu-id="3aefb-128">De waarden die u voor de SSH-gebruiker opgeeft worden gebruikt voor het maken van de SSH-gebruiker voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="3aefb-128">The values you specify for the SSH user are used to create the SSH user for the cluster.</span></span> <span data-ttu-id="3aefb-129">Dit account wordt gebruikt voor een externe SSH-sessie starten op het cluster en taken uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3aefb-129">Use this account to start a remote SSH session on the cluster and run jobs.</span></span> <span data-ttu-id="3aefb-130">Zie het document [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3aefb-130">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3aefb-131">Als u meer dan 32 worker-knooppunten (op bij het maken van het cluster of wilt door het schalen van het cluster na aanmaak) gebruiken, moet u ook een hoofdknooppunt grootte opgeven met ten minste 8 kerngeheugens en 14 GB RAM-geheugen.</span><span class="sxs-lookup"><span data-stu-id="3aefb-131">If you plan to use more than 32 worker nodes (either at cluster creation or by scaling the cluster after creation), you must also specify a head node size with at least 8 cores and 14 GB of RAM.</span></span>
>
> <span data-ttu-id="3aefb-132">Zie voor meer informatie over knooppuntgrootten en bijbehorende kosten [HDInsight prijzen](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="3aefb-132">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="3aefb-133">Er kunnen maximaal 20 minuten om een cluster te maken.</span><span class="sxs-lookup"><span data-stu-id="3aefb-133">It can take up to 20 minutes to create a cluster.</span></span>

## <a name="create-cluster-configuration-object"></a><span data-ttu-id="3aefb-134">Cluster maken: Configuration-object</span><span class="sxs-lookup"><span data-stu-id="3aefb-134">Create cluster: Configuration object</span></span>

<span data-ttu-id="3aefb-135">U kunt ook maken voor een HDInsight configuration-object met behulp `New-AzureRmHDInsightClusterConfig` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3aefb-135">You can also create an HDInsight configuration object using `New-AzureRmHDInsightClusterConfig` cmdlet.</span></span> <span data-ttu-id="3aefb-136">U kunt dit configuratieobject zodat extra configuratieopties voor uw cluster wijzigen.</span><span class="sxs-lookup"><span data-stu-id="3aefb-136">You can then modify this configuration object to enable additional configuration options for your cluster.</span></span> <span data-ttu-id="3aefb-137">Gebruik tot slot de `-Config` parameter van de `New-AzureRmHDInsightCluster` cmdlet de configuratie te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3aefb-137">Finally, use the `-Config` parameter of the `New-AzureRmHDInsightCluster` cmdlet to use the configuration.</span></span>

<span data-ttu-id="3aefb-138">Het volgende script maakt een configuratieobject voor de configuratie van een R Server op type HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="3aefb-138">The following script creates a configuration object to configure an R Server on HDInsight cluster type.</span></span> <span data-ttu-id="3aefb-139">De configuratie maakt een edge-knooppunt, RStudio en een extra storage-account.</span><span class="sxs-lookup"><span data-stu-id="3aefb-139">The configuration enables an edge node, RStudio, and an additional storage account.</span></span>

<span data-ttu-id="3aefb-140">[!code-powershell[belangrijkste](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]</span><span class="sxs-lookup"><span data-stu-id="3aefb-140">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]</span></span>

> [!WARNING]
> <span data-ttu-id="3aefb-141">Met behulp van een opslagaccount in een andere locatie dan het HDInsight-cluster wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="3aefb-141">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span> <span data-ttu-id="3aefb-142">Wanneer u in dit voorbeeld gebruikt, moet u de aanvullende storage-account maken in dezelfde locatie als de server.</span><span class="sxs-lookup"><span data-stu-id="3aefb-142">When using this example, create the additional storage account in the same location as the server.</span></span>

## <a name="customize-clusters"></a><span data-ttu-id="3aefb-143">Clusters aanpassen</span><span class="sxs-lookup"><span data-stu-id="3aefb-143">Customize clusters</span></span>

* <span data-ttu-id="3aefb-144">Zie [aanpassen HDInsight-clusters met behulp van de Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="3aefb-144">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span></span>
* <span data-ttu-id="3aefb-145">Zie [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="3aefb-145">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="3aefb-146">Het cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="3aefb-146">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="3aefb-147">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="3aefb-147">Troubleshoot</span></span>

<span data-ttu-id="3aefb-148">Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) als u problemen ondervindt met het maken van HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="3aefb-148">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="3aefb-149">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3aefb-149">Next steps</span></span>

<span data-ttu-id="3aefb-150">Nu u een HDInsight-cluster hebt gemaakt, gebruiken de volgende bronnen voor meer informatie over het werken met uw cluster.</span><span class="sxs-lookup"><span data-stu-id="3aefb-150">Now that you have successfully created an HDInsight cluster, use the following resources to learn how to work with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="3aefb-151">Hadoop-clusters</span><span class="sxs-lookup"><span data-stu-id="3aefb-151">Hadoop clusters</span></span>

* [<span data-ttu-id="3aefb-152">Hive gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="3aefb-152">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="3aefb-153">Pig gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="3aefb-153">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="3aefb-154">MapReduce gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="3aefb-154">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="3aefb-155">HBase-clusters</span><span class="sxs-lookup"><span data-stu-id="3aefb-155">HBase clusters</span></span>

* [<span data-ttu-id="3aefb-156">Aan de slag met HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="3aefb-156">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="3aefb-157">Ontwikkelen van Java-toepassingen voor HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="3aefb-157">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="3aefb-158">Storm-clusters</span><span class="sxs-lookup"><span data-stu-id="3aefb-158">Storm clusters</span></span>

* [<span data-ttu-id="3aefb-159">Java-topologieën ontwikkelen voor Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="3aefb-159">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="3aefb-160">Python-onderdelen in Storm op HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="3aefb-160">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="3aefb-161">Implementeren en bewaken topologieën met Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="3aefb-161">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="3aefb-162">Spark-clusters</span><span class="sxs-lookup"><span data-stu-id="3aefb-162">Spark clusters</span></span>

* [<span data-ttu-id="3aefb-163">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="3aefb-163">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="3aefb-164">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="3aefb-164">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="3aefb-165">Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools</span><span class="sxs-lookup"><span data-stu-id="3aefb-165">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="3aefb-166">Spark met Machine Learning: Spark in HDInsight gebruiken om voedselinspectieresultaten te voorspellen</span><span class="sxs-lookup"><span data-stu-id="3aefb-166">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="3aefb-167">Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen</span><span class="sxs-lookup"><span data-stu-id="3aefb-167">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

