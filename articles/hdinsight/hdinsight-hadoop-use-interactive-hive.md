---
title: Interactieve Hive in HDInsight - Azure aaaUse | Microsoft Docs
description: Meer informatie over hoe toouse interactieve (Hive op LLAP) Hive in HDInsight.
keywords: 
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0957643c-4936-48a3-84a3-5dc83db4ab1a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 9e751a08091d18bc1b3d070468feef87f6828c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a><span data-ttu-id="5105c-103">Interactieve Hive in HDInsight (Preview) gebruiken</span><span class="sxs-lookup"><span data-stu-id="5105c-103">Use Interactive Hive in HDInsight (Preview)</span></span>
<span data-ttu-id="5105c-104">Interactieve (ook Hive</span><span class="sxs-lookup"><span data-stu-id="5105c-104">Interactive Hive (A.K.A.</span></span> <span data-ttu-id="5105c-105">[Lange Live en proces](https://cwiki.apache.org/confluence/display/Hive/LLAP)) is een nieuwe HDInsight [type cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="5105c-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) is a new HDInsight [cluster type](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>  <span data-ttu-id="5105c-106">Interactieve Hive kan in het cachegeheugen die Hive-query's kunt u veel meer interactieve en sneller.</span><span class="sxs-lookup"><span data-stu-id="5105c-106">Interactive Hive allows in memory caching that makes Hive queries much more interactive and faster.</span></span> <span data-ttu-id="5105c-107">Deze nieuwe functie kunt HDInsight een Hallo wereld meeste zodat, flexibele en open Big Data-oplossingen op Hallo cloud met caches van in het geheugen (met Hive en Spark) en geavanceerde analyses via diepe integratie met R-Services.</span><span class="sxs-lookup"><span data-stu-id="5105c-107">This new feature makes HDInsight one of hello world’s most performant, flexible, and open Big Data solutions on hello cloud with in-memory caches (using Hive and Spark) and advanced analytics through deep integration with R Services.</span></span> 

<span data-ttu-id="5105c-108">Hallo interactieve Hive cluster wijkt af van Hallo Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="5105c-108">hello Interactive Hive cluster is different from hello Hadoop cluster.</span></span> <span data-ttu-id="5105c-109">Het bevat alleen Hallo Hive-service.</span><span class="sxs-lookup"><span data-stu-id="5105c-109">It only contains hello Hive service.</span></span> 

> [!NOTE]
> <span data-ttu-id="5105c-110">MapReduce, Pig, Sqoop, Oozie en andere services wordt binnenkort van dit clustertype worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="5105c-110">MapReduce, Pig, Sqoop, Oozie, and other services will be removed from this cluster type soon.</span></span>
> <span data-ttu-id="5105c-111">Hallo Hive-service in Hallo interactieve Hive-cluster is alleen toegankelijk via Hallo Ambari Hive-weergave, Beeline en Hive ODBC.</span><span class="sxs-lookup"><span data-stu-id="5105c-111">hello Hive service in hello Interactive Hive cluster is only accessible via hello Ambari Hive view, Beeline, and Hive ODBC.</span></span> <span data-ttu-id="5105c-112">Deze niet toegankelijk is via Hive-console, Templeton, Azure CLI en Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5105c-112">It can’t be accessed via Hive console, Templeton, Azure CLI, and Azure PowerShell.</span></span> 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a><span data-ttu-id="5105c-113">Een interactieve Hive-cluster maken</span><span class="sxs-lookup"><span data-stu-id="5105c-113">Create an Interactive Hive cluster</span></span>
<span data-ttu-id="5105c-114">Interactieve Hive-cluster wordt alleen ondersteund op Linux gebaseerde clusters.</span><span class="sxs-lookup"><span data-stu-id="5105c-114">Interactive Hive cluster is only supported on Linux-based clusters.</span></span> <span data-ttu-id="5105c-115">Zie voor meer informatie over het maken van HDInsight-clusters [maken Linux gebaseerde Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="5105c-115">For information about creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="execute-hive-from-interactive-hive"></a><span data-ttu-id="5105c-116">Component van interactieve Hive uitvoeren</span><span class="sxs-lookup"><span data-stu-id="5105c-116">Execute Hive from Interactive Hive</span></span>
<span data-ttu-id="5105c-117">Er zijn verschillende opties voor het uitvoeren van Hive-query's:</span><span class="sxs-lookup"><span data-stu-id="5105c-117">There are different options how you can execute Hive queries:</span></span>

* <span data-ttu-id="5105c-118">Uitvoeren van Hive met Hallo Ambari Hive-weergave</span><span class="sxs-lookup"><span data-stu-id="5105c-118">Run Hive using hello Ambari Hive view</span></span>
  
    <span data-ttu-id="5105c-119">Zie voor informatie over het gebruik van Hive-weergave Hallo Hallo [gebruik Hallo Hive-weergave met Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="5105c-119">For hello information about using hello Hive View, see [Use hello Hive View with Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>
* <span data-ttu-id="5105c-120">Uitvoeren van Hive met Beeline</span><span class="sxs-lookup"><span data-stu-id="5105c-120">Run Hive using Beeline</span></span>
  
    <span data-ttu-id="5105c-121">Zie voor informatie over het gebruik van Beeline op HDInsight hello [Hive gebruiken met Hadoop in HDInsight met Beeline](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="5105c-121">For hello information on using Beeline on HDInsight, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
  
    <span data-ttu-id="5105c-122">U Beeline van headnode hello of een lege edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="5105c-122">You use Beeline from either hello headnode or an empty edge node.</span></span>  <span data-ttu-id="5105c-123">Beeline gebruik van een leeg edge-knooppunt wordt aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="5105c-123">Using Beeline from an empty edge node is recommended.</span></span>  <span data-ttu-id="5105c-124">Zie voor meer informatie over het maken van een HDInsight-cluster met een leeg edgenode [leeg edge-knooppunten gebruiken in HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="5105c-124">For information on creating an HDInsight cluster with an empty edgenode, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>
* <span data-ttu-id="5105c-125">Uitvoeren van Hive via Hive ODBC</span><span class="sxs-lookup"><span data-stu-id="5105c-125">Run Hive using Hive ODBC</span></span>
  
    <span data-ttu-id="5105c-126">Zie voor informatie over het gebruik van Hive ODBC Hallo [tooHadoop Excel verbinding maken met de Hallo Microsoft Hive ODBC-stuurprogramma](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="5105c-126">For hello information on using Hive ODBC, see [Connect Excel tooHadoop with hello Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>

<span data-ttu-id="5105c-127">**toofind hello JDBC-verbindingsreeks:**</span><span class="sxs-lookup"><span data-stu-id="5105c-127">**toofind hello JDBC connection string:**</span></span>

1. <span data-ttu-id="5105c-128">Meld u aan met behulp van de URL na Hallo tooAmbari: https://<ClusterName>. AzureHDInsight.net.</span><span class="sxs-lookup"><span data-stu-id="5105c-128">Sign on tooAmbari using hello following URL: https://<ClusterName>.AzureHDInsight.net.</span></span>
2. <span data-ttu-id="5105c-129">Klik op **Hive** in het linkermenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="5105c-129">Click **Hive** from hello left menu.</span></span>
3. <span data-ttu-id="5105c-130">Klik op Hallo gemarkeerd pictogram toocopy Hallo URL:</span><span class="sxs-lookup"><span data-stu-id="5105c-130">Click hello highlighted icon toocopy hello URL:</span></span>
   
   ![HDInsight Hadoop Hive interactieve LLAP JDBC](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a><span data-ttu-id="5105c-132">Zie ook</span><span class="sxs-lookup"><span data-stu-id="5105c-132">See also</span></span>
* <span data-ttu-id="5105c-133">[Hadoop op basis van Linux-clusters maken in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): meer informatie over hoe toocreate interactieve Hive-clusters in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5105c-133">[Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Learn how toocreate Interactive Hive clusters in HDInsight.</span></span>
* <span data-ttu-id="5105c-134">[Hive gebruiken met Hadoop in HDInsight met Beeline](hdinsight-hadoop-use-hive-beeline.md): meer informatie over hoe toouse Beeline toosubmit Hive-query's.</span><span class="sxs-lookup"><span data-stu-id="5105c-134">[Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md): Learn how toouse Beeline toosubmit Hive queries.</span></span>
* <span data-ttu-id="5105c-135">[Verbinding maken met Excel tooHadoop met Hallo Microsoft Hive ODBC-stuurprogramma](hdinsight-connect-excel-hive-odbc-driver.md): meer informatie over hoe tooconnect Excel tooHive.</span><span class="sxs-lookup"><span data-stu-id="5105c-135">[Connect Excel tooHadoop with hello Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md): learn how tooconnect Excel tooHive.</span></span>

