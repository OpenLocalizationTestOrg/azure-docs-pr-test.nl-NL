---
title: aaaCreate Hadoop-cluster met een veilige overdracht storage-accounts in Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe HDInsight-clusters met veilige overdracht toocreate ingeschakeld voor Azure storage-accounts.
keywords: aan de slag met hadoop, hadoop linux, hadoop Quick Start, veilige overdracht, azure opslagaccount
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: jgao
ms.openlocfilehash: 0acb8814ad0d5d5b5652d930b2e3da90f9d7978d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a><span data-ttu-id="aa4e4-104">Hadoop-cluster maken met opslagaccounts voor veilige overdracht in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="aa4e4-104">Create Hadoop cluster with secure transfer storage accounts in Azure HDInsight</span></span>

<span data-ttu-id="aa4e4-105">Hallo [vereiste gegevensoverdracht Secure](../storage/common/storage-require-secure-transfer.md) functie verhoogt Hallo beveiliging van uw Azure Storage-account door het afdwingen van alle aanvragen tooyour-account via een beveiligde verbinding.</span><span class="sxs-lookup"><span data-stu-id="aa4e4-105">hello [Secure transfer required](../storage/common/storage-require-secure-transfer.md) feature enhances hello security of your Azure Storage account by enforcing all requests tooyour account through a secure connection.</span></span> <span data-ttu-id="aa4e4-106">Deze functie en Hallo wasbs-schema worden alleen ondersteund door de HDInsight-cluster versie 3,6 of hoger.</span><span class="sxs-lookup"><span data-stu-id="aa4e4-106">This feature and hello wasbs scheme are only supported by HDInsight cluster version 3.6 or newer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="aa4e4-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="aa4e4-107">Prerequisites</span></span>
<span data-ttu-id="aa4e4-108">Voordat u met deze zelfstudie begint, moet u over de volgende onderdelen beschikken:</span><span class="sxs-lookup"><span data-stu-id="aa4e4-108">Before you begin this tutorial, you must have:</span></span>

* <span data-ttu-id="aa4e4-109">**Azure-abonnement**: toocreate een gratis één maand-proefaccount, te bladeren[azure.microsoft.com/free](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="aa4e4-109">**Azure subscription**: toocreate a free one-month trial account, browse too[azure.microsoft.com/free](https://azure.microsoft.com/free).</span></span>
* <span data-ttu-id="aa4e4-110">**Een Azure-opslagaccount met veilige overdracht**.</span><span class="sxs-lookup"><span data-stu-id="aa4e4-110">**An Azure Storage account with secure transfer enabled**.</span></span> <span data-ttu-id="aa4e4-111">Zie voor instructies Hallo [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) en [vereisen veilige overdracht](../storage/common/storage-require-secure-transfer.md).</span><span class="sxs-lookup"><span data-stu-id="aa4e4-111">For hello instructions, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) and [Require secure transfer](../storage/common/storage-require-secure-transfer.md).</span></span>
* <span data-ttu-id="aa4e4-112">**Een Blob-container op Hallo opslagaccount**.</span><span class="sxs-lookup"><span data-stu-id="aa4e4-112">**A Blob container on hello storage account**.</span></span> 
## <a name="create-cluster"></a><span data-ttu-id="aa4e4-113">Cluster maken</span><span class="sxs-lookup"><span data-stu-id="aa4e4-113">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


<span data-ttu-id="aa4e4-114">In deze sectie maakt u een Hadoop-cluster in HDInsight met behulp van een [Azure Resource Manager-sjabloon](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="aa4e4-114">In this section, you create a Hadoop cluster in HDInsight using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="aa4e4-115">Hallo-sjabloon bevindt zich in [Github](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span><span class="sxs-lookup"><span data-stu-id="aa4e4-115">hello template is located in [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span></span> <span data-ttu-id="aa4e4-116">Het maken van een Azure Resource Manager-sjabloon is niet vereist voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="aa4e4-116">Resource Manager template experience is not required for following this tutorial.</span></span> <span data-ttu-id="aa4e4-117">Voor andere methoden voor het maken van cluster en inzicht Hallo-eigenschappen die in deze zelfstudie gebruikt, Zie [HDInsight-clusters maken](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="aa4e4-117">For other cluster creation methods and understanding hello properties used in this tutorial, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="aa4e4-118">Klik op Hallo installatiekopie toosign in tooAzure en open Hallo Resource Manager-sjabloon in hello Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="aa4e4-118">Click hello following image toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="aa4e4-119">Ga als volgt Hallo instructies toocreate Hallo cluster Hello volgende specificaties:</span><span class="sxs-lookup"><span data-stu-id="aa4e4-119">Follow hello instructions toocreate hello cluster with hello following specifications:</span></span> 

    - <span data-ttu-id="aa4e4-120">Geef HDInsight versie 3.6 op.</span><span class="sxs-lookup"><span data-stu-id="aa4e4-120">Specify HDInsight version 3.6.</span></span>  <span data-ttu-id="aa4e4-121">Hallo standaardversie is 3.5.</span><span class="sxs-lookup"><span data-stu-id="aa4e4-121">hello default version is 3.5.</span></span> <span data-ttu-id="aa4e4-122">Versie 3.6 of hoger is vereist.</span><span class="sxs-lookup"><span data-stu-id="aa4e4-122">Version 3.6 or newer is required.</span></span>
    - <span data-ttu-id="aa4e4-123">Geef een opslagaccount met veilige overdracht op.</span><span class="sxs-lookup"><span data-stu-id="aa4e4-123">Specify a secure transfer enabled storage account.</span></span>
    - <span data-ttu-id="aa4e4-124">Korte naam voor het Hallo-opslagaccount gebruiken.</span><span class="sxs-lookup"><span data-stu-id="aa4e4-124">Use short name for hello storage account.</span></span>
    - <span data-ttu-id="aa4e4-125">Zowel Hallo storage-account en de blob-container Hallo moeten vooraf worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="aa4e4-125">Both hello storage account and hello blob container must be created beforehand.</span></span> 

    <span data-ttu-id="aa4e4-126">Zie voor instructies Hallo [cluster maken](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="aa4e4-126">For hello instructions, see [Create cluster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span> 

<span data-ttu-id="aa4e4-127">Als u uw eigen configuratiebestanden script actie tooprovide opgeeft, moet u wasbs in Hallo volgende instellingen:</span><span class="sxs-lookup"><span data-stu-id="aa4e4-127">If you use script action tooprovide your own configuration files, you must use wasbs in hello following settings:</span></span>

- <span data-ttu-id="aa4e4-128">fs.defaultFS (core-site)</span><span class="sxs-lookup"><span data-stu-id="aa4e4-128">fs.defaultFS (core-site)</span></span>
- <span data-ttu-id="aa4e4-129">spark.eventLog.dir</span><span class="sxs-lookup"><span data-stu-id="aa4e4-129">spark.eventLog.dir</span></span> 
- <span data-ttu-id="aa4e4-130">spark.history.fs.logDirectory</span><span class="sxs-lookup"><span data-stu-id="aa4e4-130">spark.history.fs.logDirectory</span></span>

## <a name="add-additional-storage-accounts"></a><span data-ttu-id="aa4e4-131">Extra opslagaccounts toevoegen</span><span class="sxs-lookup"><span data-stu-id="aa4e4-131">Add additional storage accounts</span></span>

<span data-ttu-id="aa4e4-132">Er zijn verschillende opties tooadd extra veilige overdracht ingeschakeld storage-accounts:</span><span class="sxs-lookup"><span data-stu-id="aa4e4-132">There are several options tooadd additional secure transfer enabled storage accounts:</span></span>

- <span data-ttu-id="aa4e4-133">Hello Azure Resource Manager-sjabloon in de laatste sectie Hallo wijzigen.</span><span class="sxs-lookup"><span data-stu-id="aa4e4-133">Modify hello Azure Resource Manager template in hello last section.</span></span>
- <span data-ttu-id="aa4e4-134">Maken van een cluster met de Hallo [Azure-portal](https://portal.azure.com) en gekoppelde storage-account opgeven.</span><span class="sxs-lookup"><span data-stu-id="aa4e4-134">Create a cluster using hello [Azure portal](https://portal.azure.com) and specify linked storage account.</span></span>
- <span data-ttu-id="aa4e4-135">Gebruik script actie tooadd extra veilige overdracht ingeschakeld storage accounts tooan bestaand HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="aa4e4-135">Use script action tooadd additional secure transfer enabled storage accounts tooan existing HDInsight cluster.</span></span>  <span data-ttu-id="aa4e4-136">Zie voor meer informatie [toevoegen van extra opslagruimte accounts tooHDInsight](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="aa4e4-136">For more information, see [Add additional storage accounts tooHDInsight](hdinsight-hadoop-add-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa4e4-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="aa4e4-137">Next steps</span></span>
<span data-ttu-id="aa4e4-138">In deze zelfstudie hebt u geleerd hoe toocreate een HDInsight-cluster, en schakel veilige transfer toohello storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="aa4e4-138">In this tutorial, you have learned how toocreate an HDInsight cluster, and enable secure transfer toohello storage accounts.</span></span>

<span data-ttu-id="aa4e4-139">toolearn meer informatie over het analyseren van gegevens met HDInsight, Zie Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="aa4e4-139">toolearn more about analyzing data with HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="aa4e4-140">toolearn meer informatie over het gebruik van Hive met HDInsight, met inbegrip van hoe tooperform Hive query's vanuit Visual Studio, Zie [Hive gebruiken met HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="aa4e4-140">toolearn more about using Hive with HDInsight, including how tooperform Hive queries from Visual Studio, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
* <span data-ttu-id="aa4e4-141">toolearn over Pig, een taal gebruikt tootransform gegevens, Zie [Pig gebruiken met HDInsight][hdinsight-use-pig].</span><span class="sxs-lookup"><span data-stu-id="aa4e4-141">toolearn about Pig, a language used tootransform data, see [Use Pig with HDInsight][hdinsight-use-pig].</span></span>
* <span data-ttu-id="aa4e4-142">Zie toolearn over MapReduce, een manier toowrite-programma's die gegevens op Hadoop, verwerken [MapReduce gebruiken met HDInsight][hdinsight-use-mapreduce].</span><span class="sxs-lookup"><span data-stu-id="aa4e4-142">toolearn about MapReduce, a way toowrite programs that process data on Hadoop, see [Use MapReduce with HDInsight][hdinsight-use-mapreduce].</span></span>
* <span data-ttu-id="aa4e4-143">toolearn over het gebruik van Hallo HDInsight Tools voor Visual Studio tooanalyze gegevens in HDInsight, Zie [aan de slag met Visual Studio Hadoop-hulpprogramma's voor HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="aa4e4-143">toolearn about using hello HDInsight Tools for Visual Studio tooanalyze data on HDInsight, see [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

<span data-ttu-id="aa4e4-144">toolearn meer informatie over hoe HDInsight gegevens opslaat of hoe tooget gegevens in HDInsight, raadpleegt u Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="aa4e4-144">toolearn more about how HDInsight stores data or how tooget data into HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="aa4e4-145">Zie [Azure Storage gebruiken met HDInsight](hdinsight-hadoop-use-blob-storage.md) voor meer informatie over hoe HDInsight Azure Storage gebruikt.</span><span class="sxs-lookup"><span data-stu-id="aa4e4-145">For information on how HDInsight uses Azure Storage, see [Use Azure Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>
* <span data-ttu-id="aa4e4-146">Voor meer informatie over tooupload gegevens tooHDInsight, Zie [uploaden van gegevens tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="aa4e4-146">For information on how tooupload data tooHDInsight, see [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

<span data-ttu-id="aa4e4-147">toolearn meer informatie over het maken of beheren van een HDInsight-cluster, Zie Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="aa4e4-147">toolearn more about creating or managing an HDInsight cluster, see hello following articles:</span></span>

* <span data-ttu-id="aa4e4-148">toolearn over het beheren van uw Linux gebaseerde HDInsight-cluster, Zie [HDInsight-clusters beheren met Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="aa4e4-148">toolearn about managing your Linux-based HDInsight cluster, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
* <span data-ttu-id="aa4e4-149">Zie toolearn meer informatie over het Hallo-opties die u selecteren kunt bij het maken van een HDInsight-cluster [HDInsight op Linux met aangepaste opties maken](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="aa4e4-149">toolearn more about hello options you can select when creating an HDInsight cluster, see [Creating HDInsight on Linux using custom options](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="aa4e4-150">Als u bekend met Linux en Hadoop bent, maar tooknow details over Hadoop op HDInsight hello wilt, Zie [werken met HDInsight op Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="aa4e4-150">If you are familiar with Linux, and Hadoop, but want tooknow specifics about Hadoop on hello HDInsight, see [Working with HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span> <span data-ttu-id="aa4e4-151">Dit artikel biedt informatie zoals:</span><span class="sxs-lookup"><span data-stu-id="aa4e4-151">This article provides information such as:</span></span>
  
  * <span data-ttu-id="aa4e4-152">URL's voor services die worden gehost op het Hallo-cluster, zoals Ambari en WebHCat</span><span class="sxs-lookup"><span data-stu-id="aa4e4-152">URLs for services hosted on hello cluster, such as Ambari and WebHCat</span></span>
  * <span data-ttu-id="aa4e4-153">Hallo-locatie van Hadoop-bestanden en voorbeelden op het lokale bestandssysteem Hallo</span><span class="sxs-lookup"><span data-stu-id="aa4e4-153">hello location of Hadoop files and examples on hello local file system</span></span>
  * <span data-ttu-id="aa4e4-154">Hallo gebruik van Azure Storage (WASB) in plaats van HDFS als Hallo standaard gegevensopslag</span><span class="sxs-lookup"><span data-stu-id="aa4e4-154">hello use of Azure Storage (WASB) instead of HDFS as hello default data store</span></span>

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


