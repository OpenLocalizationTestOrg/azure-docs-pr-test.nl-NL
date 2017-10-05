---
title: Hadoop-cluster maken met opslagaccounts voor veilige overdracht in Azure HDInsight | Microsoft Docs
description: Informatie over het maken van HDInsight-clusters met Azure-opslag-accounts voor veilige overdracht.
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
ms.openlocfilehash: 370b2f081930fe88527436a1a127309aed6681f0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a><span data-ttu-id="204a6-104">Hadoop-cluster maken met opslagaccounts voor veilige overdracht in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="204a6-104">Create Hadoop cluster with secure transfer storage accounts in Azure HDInsight</span></span>

<span data-ttu-id="204a6-105">De functie [Veilige overdracht vereist](../storage/common/storage-require-secure-transfer.md) verhoogt de beveiliging van uw Azure-opslagaccount door alle aanvragen naar uw account af te dwingen via een beveiligde verbinding.</span><span class="sxs-lookup"><span data-stu-id="204a6-105">The [Secure transfer required](../storage/common/storage-require-secure-transfer.md) feature enhances the security of your Azure Storage account by enforcing all requests to your account through a secure connection.</span></span> <span data-ttu-id="204a6-106">Deze functie en het wasbs-schema worden alleen ondersteund door HDInsight-clusterversie 3.6 of nieuwer.</span><span class="sxs-lookup"><span data-stu-id="204a6-106">This feature and the wasbs scheme are only supported by HDInsight cluster version 3.6 or newer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="204a6-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="204a6-107">Prerequisites</span></span>
<span data-ttu-id="204a6-108">Voordat u met deze zelfstudie begint, moet u over de volgende onderdelen beschikken:</span><span class="sxs-lookup"><span data-stu-id="204a6-108">Before you begin this tutorial, you must have:</span></span>

* <span data-ttu-id="204a6-109">**Azure-abonnement**: voor het maken van een gratis proefaccount van één maand, bezoekt u [azure.microsoft.com/free](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="204a6-109">**Azure subscription**: To create a free one-month trial account, browse to [azure.microsoft.com/free](https://azure.microsoft.com/free).</span></span>
* <span data-ttu-id="204a6-110">**Een Azure-opslagaccount met veilige overdracht**.</span><span class="sxs-lookup"><span data-stu-id="204a6-110">**An Azure Storage account with secure transfer enabled**.</span></span> <span data-ttu-id="204a6-111">Zie [Een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) en [Veilige overdracht vereisen](../storage/common/storage-require-secure-transfer.md) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="204a6-111">For the instructions, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) and [Require secure transfer](../storage/common/storage-require-secure-transfer.md).</span></span>
* <span data-ttu-id="204a6-112">**Een Blob-container in het opslagaccount**.</span><span class="sxs-lookup"><span data-stu-id="204a6-112">**A Blob container on the storage account**.</span></span> 
## <a name="create-cluster"></a><span data-ttu-id="204a6-113">Cluster maken</span><span class="sxs-lookup"><span data-stu-id="204a6-113">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


<span data-ttu-id="204a6-114">In deze sectie maakt u een Hadoop-cluster in HDInsight met behulp van een [Azure Resource Manager-sjabloon](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="204a6-114">In this section, you create a Hadoop cluster in HDInsight using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="204a6-115">De sjabloon bevindt zich in [GitHub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span><span class="sxs-lookup"><span data-stu-id="204a6-115">The template is located in [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span></span> <span data-ttu-id="204a6-116">Het maken van een Azure Resource Manager-sjabloon is niet vereist voor deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="204a6-116">Resource Manager template experience is not required for following this tutorial.</span></span> <span data-ttu-id="204a6-117">Zie [HDInsight-clusters maken](hdinsight-hadoop-provision-linux-clusters.md) voor andere methoden om clusters te maken en inzicht te krijgen in de eigenschappen die worden gebruikt in deze zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="204a6-117">For other cluster creation methods and understanding the properties used in this tutorial, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="204a6-118">Klik op de volgende afbeelding om u aan te melden bij Azure en de Resource Manager-sjabloon in Azure Portal te openen.</span><span class="sxs-lookup"><span data-stu-id="204a6-118">Click the following image to sign in to Azure and open the Resource Manager template in the Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. <span data-ttu-id="204a6-119">Volg de instructies voor het maken van het cluster met de volgende specificaties:</span><span class="sxs-lookup"><span data-stu-id="204a6-119">Follow the instructions to create the cluster with the following specifications:</span></span> 

    - <span data-ttu-id="204a6-120">Geef HDInsight versie 3.6 op.</span><span class="sxs-lookup"><span data-stu-id="204a6-120">Specify HDInsight version 3.6.</span></span>  <span data-ttu-id="204a6-121">De standaardversie is 3.5.</span><span class="sxs-lookup"><span data-stu-id="204a6-121">The default version is 3.5.</span></span> <span data-ttu-id="204a6-122">Versie 3.6 of hoger is vereist.</span><span class="sxs-lookup"><span data-stu-id="204a6-122">Version 3.6 or newer is required.</span></span>
    - <span data-ttu-id="204a6-123">Geef een opslagaccount met veilige overdracht op.</span><span class="sxs-lookup"><span data-stu-id="204a6-123">Specify a secure transfer enabled storage account.</span></span>
    - <span data-ttu-id="204a6-124">Gebruik de korte naam voor het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="204a6-124">Use short name for the storage account.</span></span>
    - <span data-ttu-id="204a6-125">Zowel het opslagaccount als de blob-container moeten vooraf zijn gemaakt.</span><span class="sxs-lookup"><span data-stu-id="204a6-125">Both the storage account and the blob container must be created beforehand.</span></span> 

    <span data-ttu-id="204a6-126">Zie [Cluster maken](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster) voor instructies.</span><span class="sxs-lookup"><span data-stu-id="204a6-126">For the instructions, see [Create cluster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span> 

<span data-ttu-id="204a6-127">Als u een scriptactie gebruikt om uw eigen configuratiebestanden te verstrekken, moet u wasbs gebruiken in de volgende instellingen:</span><span class="sxs-lookup"><span data-stu-id="204a6-127">If you use script action to provide your own configuration files, you must use wasbs in the following settings:</span></span>

- <span data-ttu-id="204a6-128">fs.defaultFS (core-site)</span><span class="sxs-lookup"><span data-stu-id="204a6-128">fs.defaultFS (core-site)</span></span>
- <span data-ttu-id="204a6-129">spark.eventLog.dir</span><span class="sxs-lookup"><span data-stu-id="204a6-129">spark.eventLog.dir</span></span> 
- <span data-ttu-id="204a6-130">spark.history.fs.logDirectory</span><span class="sxs-lookup"><span data-stu-id="204a6-130">spark.history.fs.logDirectory</span></span>

## <a name="add-additional-storage-accounts"></a><span data-ttu-id="204a6-131">Extra opslagaccounts toevoegen</span><span class="sxs-lookup"><span data-stu-id="204a6-131">Add additional storage accounts</span></span>

<span data-ttu-id="204a6-132">Er zijn verschillende opties om extra opslagaccounts met veilige overdracht toe te voegen:</span><span class="sxs-lookup"><span data-stu-id="204a6-132">There are several options to add additional secure transfer enabled storage accounts:</span></span>

- <span data-ttu-id="204a6-133">De Azure Resource Manager-sjabloon in de laatste sectie wijzigen.</span><span class="sxs-lookup"><span data-stu-id="204a6-133">Modify the Azure Resource Manager template in the last section.</span></span>
- <span data-ttu-id="204a6-134">Een cluster maken met [Azure Portal](https://portal.azure.com) en een gekoppelde opslagaccount opgeven.</span><span class="sxs-lookup"><span data-stu-id="204a6-134">Create a cluster using the [Azure portal](https://portal.azure.com) and specify linked storage account.</span></span>
- <span data-ttu-id="204a6-135">Een scriptactie gebruiken om extra opslagaccounts met veilige overdracht toe te voegen aan een bestaand HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="204a6-135">Use script action to add additional secure transfer enabled storage accounts to an existing HDInsight cluster.</span></span>  <span data-ttu-id="204a6-136">Zie [Extra opslagaccounts toevoegen aan HDInsight](hdinsight-hadoop-add-storage.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="204a6-136">For more information, see [Add additional storage accounts to HDInsight](hdinsight-hadoop-add-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="204a6-137">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="204a6-137">Next steps</span></span>
<span data-ttu-id="204a6-138">In deze zelfstudie hebt u geleerd hoe een HDInsight-cluster kunt maken en veilige overdracht kunt inschakelen voor de opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="204a6-138">In this tutorial, you have learned how to create an HDInsight cluster, and enable secure transfer to the storage accounts.</span></span>

<span data-ttu-id="204a6-139">Zie de volgende artikelen voor meer informatie over het analyseren van gegevens met HDInsight:</span><span class="sxs-lookup"><span data-stu-id="204a6-139">To learn more about analyzing data with HDInsight, see the following articles:</span></span>

* <span data-ttu-id="204a6-140">Zie [Hive gebruiken met HDInsight][hdinsight-use-hive] voor meer informatie over het gebruik van Hive met HDInsight, waaronder over het uitvoeren van Hive-query's vanuit Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="204a6-140">To learn more about using Hive with HDInsight, including how to perform Hive queries from Visual Studio, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
* <span data-ttu-id="204a6-141">Zie [Pig gebruiken met HDInsight][hdinsight-use-pig] voor meer informatie over Pig, een taal die wordt gebruikt voor het omzetten van gegevens.</span><span class="sxs-lookup"><span data-stu-id="204a6-141">To learn about Pig, a language used to transform data, see [Use Pig with HDInsight][hdinsight-use-pig].</span></span>
* <span data-ttu-id="204a6-142">Zie [MapReduce gebruiken met HDInsight][hdinsight-use-mapreduce] voor meer informatie over MapReduce, een middel om programma's te schrijven die gegevens verwerken op Hadoop.</span><span class="sxs-lookup"><span data-stu-id="204a6-142">To learn about MapReduce, a way to write programs that process data on Hadoop, see [Use MapReduce with HDInsight][hdinsight-use-mapreduce].</span></span>
* <span data-ttu-id="204a6-143">Zie voor meer informatie over het gebruik van de HDInsight-hulpprogramma's voor Visual Studio om gegevens op HDInsight te analyseren [Aan de slag met Visual Studio Hadoop-hulpprogramma's voor HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="204a6-143">To learn about using the HDInsight Tools for Visual Studio to analyze data on HDInsight, see [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

<span data-ttu-id="204a6-144">Zie de volgende artikelen voor meer informatie over hoe HDInsight gegevens opslaat en over het ophalen van gegevens in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="204a6-144">To learn more about how HDInsight stores data or how to get data into HDInsight, see the following articles:</span></span>

* <span data-ttu-id="204a6-145">Zie [Azure Storage gebruiken met HDInsight](hdinsight-hadoop-use-blob-storage.md) voor meer informatie over hoe HDInsight Azure Storage gebruikt.</span><span class="sxs-lookup"><span data-stu-id="204a6-145">For information on how HDInsight uses Azure Storage, see [Use Azure Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>
* <span data-ttu-id="204a6-146">Zie [Gegevens uploaden naar HDInsight][hdinsight-upload-data] voor meer informatie over het uploaden van gegevens naar HDInsight.</span><span class="sxs-lookup"><span data-stu-id="204a6-146">For information on how to upload data to HDInsight, see [Upload data to HDInsight][hdinsight-upload-data].</span></span>

<span data-ttu-id="204a6-147">Zie de volgende artikelen voor meer informatie over het maken of beheren van een HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="204a6-147">To learn more about creating or managing an HDInsight cluster, see the following articles:</span></span>

* <span data-ttu-id="204a6-148">Zie voor meer informatie over het beheren van uw HDInsight-cluster op basis van Linux [HDInsight-clusters beheren met Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="204a6-148">To learn about managing your Linux-based HDInsight cluster, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
* <span data-ttu-id="204a6-149">Zie voor meer informatie over de opties die u kunt selecteren bij het maken van een HDInsight-cluster [HDInsight op Linux maken met aangepaste opties](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="204a6-149">To learn more about the options you can select when creating an HDInsight cluster, see [Creating HDInsight on Linux using custom options](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="204a6-150">Als u bekend bent met Linux en Hadoop, maar u meer details wilt weten over Hadoop op HDInsight, raadpleegt u [Werken met HDInsight op Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="204a6-150">If you are familiar with Linux, and Hadoop, but want to know specifics about Hadoop on the HDInsight, see [Working with HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span> <span data-ttu-id="204a6-151">Dit artikel biedt informatie zoals:</span><span class="sxs-lookup"><span data-stu-id="204a6-151">This article provides information such as:</span></span>
  
  * <span data-ttu-id="204a6-152">URL's voor services die worden gehost op het cluster, zoals Ambari en WebHCat</span><span class="sxs-lookup"><span data-stu-id="204a6-152">URLs for services hosted on the cluster, such as Ambari and WebHCat</span></span>
  * <span data-ttu-id="204a6-153">De locatie van Hadoop-bestanden en voorbeelden op het lokale bestandssysteem</span><span class="sxs-lookup"><span data-stu-id="204a6-153">The location of Hadoop files and examples on the local file system</span></span>
  * <span data-ttu-id="204a6-154">Het gebruik van Azure Storage (WASB) in plaats van HDFS als de standaard gegevensopslag</span><span class="sxs-lookup"><span data-stu-id="204a6-154">The use of Azure Storage (WASB) instead of HDFS as the default data store</span></span>

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


