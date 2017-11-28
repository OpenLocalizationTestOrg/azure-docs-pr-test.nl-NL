---
title: Interactieve Hive in HDInsight - Azure gebruiken | Microsoft Docs
description: Informatie over het gebruik van interactieve (Hive op LLAP) Hive in HDInsight.
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
ms.openlocfilehash: e7874b55fc72f14d8e2c801872359e823cb2ba34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a><span data-ttu-id="0ea3c-103">Interactieve Hive in HDInsight (Preview) gebruiken</span><span class="sxs-lookup"><span data-stu-id="0ea3c-103">Use Interactive Hive in HDInsight (Preview)</span></span>
<span data-ttu-id="0ea3c-104">Interactieve (ook Hive</span><span class="sxs-lookup"><span data-stu-id="0ea3c-104">Interactive Hive (A.K.A.</span></span> <span data-ttu-id="0ea3c-105">[Lange Live en proces](https://cwiki.apache.org/confluence/display/Hive/LLAP)) is een nieuwe HDInsight [type cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="0ea3c-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) is a new HDInsight [cluster type](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>  <span data-ttu-id="0ea3c-106">Interactieve Hive kan in het cachegeheugen die Hive-query's kunt u veel meer interactieve en sneller.</span><span class="sxs-lookup"><span data-stu-id="0ea3c-106">Interactive Hive allows in memory caching that makes Hive queries much more interactive and faster.</span></span> <span data-ttu-id="0ea3c-107">Deze nieuwe functie kunt HDInsight van de wereld meeste zodat, flexibele en open Big Data-oplossingen in de cloud met caches van in het geheugen (met Hive en Spark) en geavanceerde analyses via diepe integratie met R-Services.</span><span class="sxs-lookup"><span data-stu-id="0ea3c-107">This new feature makes HDInsight one of the world’s most performant, flexible, and open Big Data solutions on the cloud with in-memory caches (using Hive and Spark) and advanced analytics through deep integration with R Services.</span></span> 

<span data-ttu-id="0ea3c-108">Het cluster interactieve Hive wijkt af van het Hadoop-cluster.</span><span class="sxs-lookup"><span data-stu-id="0ea3c-108">The Interactive Hive cluster is different from the Hadoop cluster.</span></span> <span data-ttu-id="0ea3c-109">Het bevat alleen de Hive-service.</span><span class="sxs-lookup"><span data-stu-id="0ea3c-109">It only contains the Hive service.</span></span> 

> [!NOTE]
> <span data-ttu-id="0ea3c-110">MapReduce, Pig, Sqoop, Oozie en andere services wordt binnenkort van dit clustertype worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="0ea3c-110">MapReduce, Pig, Sqoop, Oozie, and other services will be removed from this cluster type soon.</span></span>
> <span data-ttu-id="0ea3c-111">Het Hive-service in het cluster interactieve Hive is alleen toegankelijk via de Ambari Hive-weergave, Beeline en Hive ODBC.</span><span class="sxs-lookup"><span data-stu-id="0ea3c-111">The Hive service in the Interactive Hive cluster is only accessible via the Ambari Hive view, Beeline, and Hive ODBC.</span></span> <span data-ttu-id="0ea3c-112">Deze niet toegankelijk is via Hive-console, Templeton, Azure CLI en Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0ea3c-112">It can’t be accessed via Hive console, Templeton, Azure CLI, and Azure PowerShell.</span></span> 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a><span data-ttu-id="0ea3c-113">Een interactieve Hive-cluster maken</span><span class="sxs-lookup"><span data-stu-id="0ea3c-113">Create an Interactive Hive cluster</span></span>
<span data-ttu-id="0ea3c-114">Interactieve Hive-cluster wordt alleen ondersteund op Linux gebaseerde clusters.</span><span class="sxs-lookup"><span data-stu-id="0ea3c-114">Interactive Hive cluster is only supported on Linux-based clusters.</span></span> <span data-ttu-id="0ea3c-115">Zie voor meer informatie over het maken van HDInsight-clusters [maken Linux gebaseerde Hadoop-clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="0ea3c-115">For information about creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="execute-hive-from-interactive-hive"></a><span data-ttu-id="0ea3c-116">Component van interactieve Hive uitvoeren</span><span class="sxs-lookup"><span data-stu-id="0ea3c-116">Execute Hive from Interactive Hive</span></span>
<span data-ttu-id="0ea3c-117">Er zijn verschillende opties voor het uitvoeren van Hive-query's:</span><span class="sxs-lookup"><span data-stu-id="0ea3c-117">There are different options how you can execute Hive queries:</span></span>

* <span data-ttu-id="0ea3c-118">Uitvoeren van Hive met behulp van de Ambari Hive-weergave</span><span class="sxs-lookup"><span data-stu-id="0ea3c-118">Run Hive using the Ambari Hive view</span></span>
  
    <span data-ttu-id="0ea3c-119">Zie voor informatie over het gebruik van de weergave Hive [de weergave Hive gebruiken met Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="0ea3c-119">For the information about using the Hive View, see [Use the Hive View with Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>
* <span data-ttu-id="0ea3c-120">Uitvoeren van Hive met Beeline</span><span class="sxs-lookup"><span data-stu-id="0ea3c-120">Run Hive using Beeline</span></span>
  
    <span data-ttu-id="0ea3c-121">Zie voor informatie over het gebruik van Beeline op HDInsight [Hive gebruiken met Hadoop in HDInsight met Beeline](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="0ea3c-121">For the information on using Beeline on HDInsight, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
  
    <span data-ttu-id="0ea3c-122">U Beeline gebruiken vanuit de headnode of een lege edge-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="0ea3c-122">You use Beeline from either the headnode or an empty edge node.</span></span>  <span data-ttu-id="0ea3c-123">Beeline gebruik van een leeg edge-knooppunt wordt aanbevolen.</span><span class="sxs-lookup"><span data-stu-id="0ea3c-123">Using Beeline from an empty edge node is recommended.</span></span>  <span data-ttu-id="0ea3c-124">Zie voor meer informatie over het maken van een HDInsight-cluster met een leeg edgenode [leeg edge-knooppunten gebruiken in HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="0ea3c-124">For information on creating an HDInsight cluster with an empty edgenode, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>
* <span data-ttu-id="0ea3c-125">Uitvoeren van Hive via Hive ODBC</span><span class="sxs-lookup"><span data-stu-id="0ea3c-125">Run Hive using Hive ODBC</span></span>
  
    <span data-ttu-id="0ea3c-126">Zie voor informatie over het gebruik van Hive ODBC [verbinding maken met Excel en Hadoop met het Microsoft Hive ODBC-stuurprogramma](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="0ea3c-126">For the information on using Hive ODBC, see [Connect Excel to Hadoop with the Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>

<span data-ttu-id="0ea3c-127">**De verbindingsreeks JDBC zoeken:**</span><span class="sxs-lookup"><span data-stu-id="0ea3c-127">**To find the JDBC connection string:**</span></span>

1. <span data-ttu-id="0ea3c-128">Meld u bij de Ambari met behulp van de volgende URL: https://<ClusterName>. AzureHDInsight.net.</span><span class="sxs-lookup"><span data-stu-id="0ea3c-128">Sign on to Ambari using the following URL: https://<ClusterName>.AzureHDInsight.net.</span></span>
2. <span data-ttu-id="0ea3c-129">Klik op **Hive** in het menu links.</span><span class="sxs-lookup"><span data-stu-id="0ea3c-129">Click **Hive** from the left menu.</span></span>
3. <span data-ttu-id="0ea3c-130">Klik op de gemarkeerde pictogram voor het kopiëren van de URL:</span><span class="sxs-lookup"><span data-stu-id="0ea3c-130">Click the highlighted icon to copy the URL:</span></span>
   
   ![HDInsight Hadoop Hive interactieve LLAP JDBC](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a><span data-ttu-id="0ea3c-132">Zie ook</span><span class="sxs-lookup"><span data-stu-id="0ea3c-132">See also</span></span>
* <span data-ttu-id="0ea3c-133">[Hadoop op basis van Linux-clusters maken in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): informatie over het maken van clusters interactieve Hive in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0ea3c-133">[Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Learn how to create Interactive Hive clusters in HDInsight.</span></span>
* <span data-ttu-id="0ea3c-134">[Hive gebruiken met Hadoop in HDInsight met Beeline](hdinsight-hadoop-use-hive-beeline.md): informatie over het gebruik van Beeline Hive-query's verzenden.</span><span class="sxs-lookup"><span data-stu-id="0ea3c-134">[Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md): Learn how to use Beeline to submit Hive queries.</span></span>
* <span data-ttu-id="0ea3c-135">[Excel en Hadoop koppelen met het stuurprogramma Microsoft Hive ODBC](hdinsight-connect-excel-hive-odbc-driver.md): meer informatie over hoe u Excel verbindt met Hive.</span><span class="sxs-lookup"><span data-stu-id="0ea3c-135">[Connect Excel to Hadoop with the Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md): learn how to connect Excel to Hive.</span></span>

