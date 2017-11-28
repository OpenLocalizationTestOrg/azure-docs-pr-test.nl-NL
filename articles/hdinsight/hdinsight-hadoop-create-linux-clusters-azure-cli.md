---
title: aaaCreate Hadoop-clusters met behulp van de opdrachtregel - hello Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toocreate HDInsight-clusters met meerdere platforms Azure CLI 1.0 Hallo.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 50b01483-455c-4d87-b754-2229005a8ab9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 5295b01054b8c23df0e3b75a3e0e8c933ac48b3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-using-hello-azure-cli"></a><span data-ttu-id="54115-103">Maken van HDInsight-clusters met hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="54115-103">Create HDInsight clusters using hello Azure CLI</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="54115-104">Hallo stappen in dit document procedure voor het maken van een 3.5 HDInsight-cluster met behulp van hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="54115-104">hello steps in this document walk-through creating a HDInsight 3.5 cluster using hello Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="54115-105">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="54115-105">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="54115-106">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="54115-106">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="54115-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="54115-107">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="54115-108">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="54115-108">**An Azure subscription**.</span></span> <span data-ttu-id="54115-109">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="54115-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="54115-110">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="54115-110">**Azure CLI**.</span></span> <span data-ttu-id="54115-111">Hallo stappen in dit document zijn laatste getest met Azure CLI versie 0.10.14.</span><span class="sxs-lookup"><span data-stu-id="54115-111">hello steps in this document were last tested with Azure CLI version 0.10.14.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="54115-112">Hallo stappen in dit document werken niet met Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="54115-112">hello steps in this document do not work with Azure CLI 2.0.</span></span> <span data-ttu-id="54115-113">Azure CLI 2.0 biedt geen ondersteuning voor het maken van een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="54115-113">Azure CLI 2.0 does not support creating an HDInsight cluster.</span></span>

## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="54115-114">Meld u bij tooyour Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="54115-114">Log in tooyour Azure subscription</span></span>

<span data-ttu-id="54115-115">Hallo stappen beschreven in [tooan Azure-abonnement van hello Azure-opdrachtregelinterface (Azure CLI) verbinding](../xplat-cli-connect.md) en maak verbinding met Hallo tooyour-abonnement **aanmelding** methode.</span><span class="sxs-lookup"><span data-stu-id="54115-115">Follow hello steps documented in [Connect tooan Azure subscription from hello Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md) and connect tooyour subscription using hello **login** method.</span></span>

## <a name="create-a-cluster"></a><span data-ttu-id="54115-116">Een cluster maken</span><span class="sxs-lookup"><span data-stu-id="54115-116">Create a cluster</span></span>

<span data-ttu-id="54115-117">Hallo stappen moet worden uitgevoerd vanaf een opdrachtregel zoals PowerShell of Bash.</span><span class="sxs-lookup"><span data-stu-id="54115-117">hello following steps should be performed from a command line, such as PowerShell or Bash.</span></span>

1. <span data-ttu-id="54115-118">Gebruik Hallo opdracht tooauthenticate tooyour Azure-abonnement te volgen:</span><span class="sxs-lookup"><span data-stu-id="54115-118">Use hello following command tooauthenticate tooyour Azure subscription:</span></span>

        azure login

    <span data-ttu-id="54115-119">U na vragen aan gebruiker tooprovide zijn uw naam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="54115-119">You are prompted tooprovide your name and password.</span></span> <span data-ttu-id="54115-120">Als u meerdere Azure-abonnementen hebt, gebruikt u `azure account set <subscriptionname>` tooset Hallo abonnement dat hello Azure CLI-opdrachten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="54115-120">If you have multiple Azure subscriptions, use `azure account set <subscriptionname>` tooset hello subscription that hello Azure CLI commands use.</span></span>

2. <span data-ttu-id="54115-121">De modus Resource Manager tooAzure met behulp van de volgende opdracht Hallo switch:</span><span class="sxs-lookup"><span data-stu-id="54115-121">Switch tooAzure Resource Manager mode using hello following command:</span></span>

        azure config mode arm

3. <span data-ttu-id="54115-122">Maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="54115-122">Create a resource group.</span></span> <span data-ttu-id="54115-123">Deze resourcegroep bevat Hallo HDInsight-cluster en storage-account gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="54115-123">This resource group contains hello HDInsight cluster and associated storage account.</span></span>

        azure group create groupname location

    * <span data-ttu-id="54115-124">Vervang `groupname` met een unieke naam voor de groep Hallo.</span><span class="sxs-lookup"><span data-stu-id="54115-124">Replace `groupname` with a unique name for hello group.</span></span>

    * <span data-ttu-id="54115-125">Vervang `location` met Hallo geografische regio die u wilt dat toocreate Hallo groep in.</span><span class="sxs-lookup"><span data-stu-id="54115-125">Replace `location` with hello geographic region that you want toocreate hello group in.</span></span>

       <span data-ttu-id="54115-126">Gebruik voor een lijst met geldige locaties, Hallo `azure location list` opdracht en gebruik vervolgens een van de locaties van Hallo Hallo `Name` kolom.</span><span class="sxs-lookup"><span data-stu-id="54115-126">For a list of valid locations, use hello `azure location list` command, and then use one of hello locations from hello `Name` column.</span></span>

4. <span data-ttu-id="54115-127">Een opslagaccount maken.</span><span class="sxs-lookup"><span data-stu-id="54115-127">Create a storage account.</span></span> <span data-ttu-id="54115-128">Dit opslagaccount wordt gebruikt als Hallo standaard opslag voor Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="54115-128">This storage account is used as hello default storage for hello HDInsight cluster.</span></span>

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * <span data-ttu-id="54115-129">Vervang `groupname` met de naam van Hallo groep gemaakt in de vorige stap Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="54115-129">Replace `groupname` with hello name of hello group created in hello previous step.</span></span>

    * <span data-ttu-id="54115-130">Vervang `location` met dezelfde locatie worden gebruikt in de vorige stap Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="54115-130">Replace `location` with hello same location used in hello previous step.</span></span>

    * <span data-ttu-id="54115-131">Vervang `storagename` met een unieke naam voor het Hallo-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="54115-131">Replace `storagename` with a unique name for hello storage account.</span></span>

        > [!NOTE]
        > <span data-ttu-id="54115-132">Voor meer informatie over Hallo-parameters die worden gebruikt in deze opdracht gebruiken `azure storage account create -h` tooview help voor deze opdracht.</span><span class="sxs-lookup"><span data-stu-id="54115-132">For more information on hello parameters used in this command, use `azure storage account create -h` tooview help for this command.</span></span>

5. <span data-ttu-id="54115-133">Hallo-sleutel ophalen tooaccess Hallo storage-account gebruikt.</span><span class="sxs-lookup"><span data-stu-id="54115-133">Retrieve hello key used tooaccess hello storage account.</span></span>

        azure storage account keys list -g groupname storagename

    * <span data-ttu-id="54115-134">Vervang `groupname` met de naam van resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="54115-134">Replace `groupname` with hello resource group name.</span></span>
    * <span data-ttu-id="54115-135">Vervang `storagename` met de naam van het opslagaccount Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="54115-135">Replace `storagename` with hello name of hello storage account.</span></span>

     <span data-ttu-id="54115-136">Hallo-gegevens die wordt geretourneerd, opslaan Hallo `key` waarde voor `key1`.</span><span class="sxs-lookup"><span data-stu-id="54115-136">In hello data that is returned, save hello `key` value for `key1`.</span></span>

6. <span data-ttu-id="54115-137">Maak een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="54115-137">Create an HDInsight cluster.</span></span>

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * <span data-ttu-id="54115-138">Vervang `groupname` met de naam van resourcegroep Hallo.</span><span class="sxs-lookup"><span data-stu-id="54115-138">Replace `groupname` with hello resource group name.</span></span>

    * <span data-ttu-id="54115-139">Vervang `Hadoop` met type Hallo-cluster dat u wenst dat toocreate.</span><span class="sxs-lookup"><span data-stu-id="54115-139">Replace `Hadoop` with hello cluster type that you wish toocreate.</span></span> <span data-ttu-id="54115-140">Bijvoorbeeld: `Hadoop`, `HBase`, `Kafka`, `Spark`, of `Storm`.</span><span class="sxs-lookup"><span data-stu-id="54115-140">For example, `Hadoop`, `HBase`, `Kafka`, `Spark`, or `Storm`.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="54115-141">HDInsight clusters worden geleverd in verschillende typen die overeenkomen met de werkbelasting toohello of technologie voor het cluster Hallo is afgestemd op.</span><span class="sxs-lookup"><span data-stu-id="54115-141">HDInsight clusters come in various types, which correspond toohello workload or technology that hello cluster is tuned for.</span></span> <span data-ttu-id="54115-142">Er is geen ondersteunde methode toocreate van een cluster waarin meerdere typen zoals Storm en HBase op één cluster.</span><span class="sxs-lookup"><span data-stu-id="54115-142">There is no supported method toocreate a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span>

    * <span data-ttu-id="54115-143">Vervang `location` Hello dezelfde locatie worden gebruikt in de vorige stappen.</span><span class="sxs-lookup"><span data-stu-id="54115-143">Replace `location` with hello same location used in previous steps.</span></span>

    * <span data-ttu-id="54115-144">Vervang `storagename` met Hallo opslagaccountnaam.</span><span class="sxs-lookup"><span data-stu-id="54115-144">Replace `storagename` with hello storage account name.</span></span>

    * <span data-ttu-id="54115-145">Vervang `storagekey` met Hallo-sleutel in de vorige stap Hallo verkregen.</span><span class="sxs-lookup"><span data-stu-id="54115-145">Replace `storagekey` with hello key obtained in hello previous step.</span></span>

    * <span data-ttu-id="54115-146">Voor Hallo `--defaultStorageContainer` parameter, gebruik Hallo dezelfde naam als u voor het Hallo-cluster gebruikt.</span><span class="sxs-lookup"><span data-stu-id="54115-146">For hello `--defaultStorageContainer` parameter, use hello same name as you are using for hello cluster.</span></span>

    * <span data-ttu-id="54115-147">Vervang `admin` en `httppassword` met Hallo naam en het wachtwoord u wenst dat toouse bij het openen van Hallo-cluster via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="54115-147">Replace `admin` and `httppassword` with hello name and password you wish toouse when accessing hello cluster through HTTPS.</span></span>

    * <span data-ttu-id="54115-148">Vervang `sshuser` en `sshuserpassword` met Hallo gebruikersnaam en wachtwoord desgewenst toouse bij het openen van Hallo-cluster via SSH</span><span class="sxs-lookup"><span data-stu-id="54115-148">Replace `sshuser` and `sshuserpassword` with hello username and password you wish toouse when accessing hello cluster using SSH</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="54115-149">In dit voorbeeld maakt een cluster met twee worker opmerkingen.</span><span class="sxs-lookup"><span data-stu-id="54115-149">This example creates a cluster with two worker notes.</span></span> <span data-ttu-id="54115-150">U kunt ook het aantal worker-knooppunten Hallo na het maken van het cluster wijzigen door het vergroten/verkleinen bewerkingen uitvoert.</span><span class="sxs-lookup"><span data-stu-id="54115-150">You can also change hello number of worker nodes after cluster creation by performing scaling operations.</span></span> <span data-ttu-id="54115-151">Als u van plan bent over het gebruik van meer dan 32 worker-knooppunten, selecteert u een grootte van het hoofdknooppunt met ten minste 8 kerngeheugens en 14 GB RAM-geheugen.</span><span class="sxs-lookup"><span data-stu-id="54115-151">If you plan on using more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14-GB RAM.</span></span> <span data-ttu-id="54115-152">U kunt Hallo hoofdknooppunt grootte instellen met behulp van Hallo `--headNodeSize` parameter tijdens het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="54115-152">You can set hello head node size by using hello `--headNodeSize` parameter during cluster creation.</span></span>
    >
    > <span data-ttu-id="54115-153">Zie voor meer informatie over knooppuntgrootten en bijbehorende kosten [HDInsight prijzen](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="54115-153">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

    <span data-ttu-id="54115-154">Het kan enkele minuten duren voordat Hallo cluster maken van het proces toofinish.</span><span class="sxs-lookup"><span data-stu-id="54115-154">It may take several minutes for hello cluster creation process toofinish.</span></span> <span data-ttu-id="54115-155">Meestal ongeveer 15.</span><span class="sxs-lookup"><span data-stu-id="54115-155">Usually around 15.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="54115-156">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="54115-156">Troubleshoot</span></span>

<span data-ttu-id="54115-157">Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) als u problemen ondervindt met het maken van HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="54115-157">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="54115-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="54115-158">Next steps</span></span>

<span data-ttu-id="54115-159">Nu u een HDInsight-cluster met behulp van hello Azure CLI hebt gemaakt, gebruiken Hallo toolearn hoe na toowork met het cluster:</span><span class="sxs-lookup"><span data-stu-id="54115-159">Now that you have successfully created an HDInsight cluster using hello Azure CLI, use hello following toolearn how toowork with your cluster:</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="54115-160">Hadoop-clusters</span><span class="sxs-lookup"><span data-stu-id="54115-160">Hadoop clusters</span></span>

* [<span data-ttu-id="54115-161">Hive gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="54115-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="54115-162">Pig gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="54115-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="54115-163">MapReduce gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="54115-163">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="54115-164">HBase-clusters</span><span class="sxs-lookup"><span data-stu-id="54115-164">HBase clusters</span></span>

* [<span data-ttu-id="54115-165">Aan de slag met HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="54115-165">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="54115-166">Ontwikkelen van Java-toepassingen voor HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="54115-166">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="54115-167">Storm-clusters</span><span class="sxs-lookup"><span data-stu-id="54115-167">Storm clusters</span></span>

* [<span data-ttu-id="54115-168">Java-topologieën ontwikkelen voor Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="54115-168">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="54115-169">Python-onderdelen in Storm op HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="54115-169">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="54115-170">Implementeren en bewaken topologieën met Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="54115-170">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
