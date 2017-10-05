---
title: Met behulp van de opdrachtregel-Azure HDInsight Hadoop-clusters maken | Microsoft Docs
description: Informatie over het maken van HDInsight-clusters met behulp van de platformoverschrijdende Azure CLI 1.0.
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
ms.openlocfilehash: 8f2fcb46789d000cd66164508f1159338dcae5f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-hdinsight-clusters-using-the-azure-cli"></a><span data-ttu-id="ed269-103">Maken van HDInsight-clusters met de Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ed269-103">Create HDInsight clusters using the Azure CLI</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="ed269-104">De stappen in dit document procedure voor het maken van een 3.5 HDInsight-cluster met behulp van de Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="ed269-104">The steps in this document walk-through creating a HDInsight 3.5 cluster using the Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ed269-105">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="ed269-105">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ed269-106">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ed269-106">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="ed269-107">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ed269-107">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="ed269-108">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="ed269-108">**An Azure subscription**.</span></span> <span data-ttu-id="ed269-109">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="ed269-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="ed269-110">**Azure CLI**.</span><span class="sxs-lookup"><span data-stu-id="ed269-110">**Azure CLI**.</span></span> <span data-ttu-id="ed269-111">De stappen in dit document zijn laatste getest met Azure CLI versie 0.10.14.</span><span class="sxs-lookup"><span data-stu-id="ed269-111">The steps in this document were last tested with Azure CLI version 0.10.14.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="ed269-112">De stappen in dit document werken niet met Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="ed269-112">The steps in this document do not work with Azure CLI 2.0.</span></span> <span data-ttu-id="ed269-113">Azure CLI 2.0 biedt geen ondersteuning voor het maken van een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="ed269-113">Azure CLI 2.0 does not support creating an HDInsight cluster.</span></span>

## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="ed269-114">Aanmelden bij uw Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="ed269-114">Log in to your Azure subscription</span></span>

<span data-ttu-id="ed269-115">Volg de stappen die zijn beschreven in [Verbinding maken met een Azure-abonnement met de Azure-opdrachtregelinterface (Azure CLI)](../xplat-cli-connect.md) en maak verbinding met uw abonnement met behulp van de methode **login**.</span><span class="sxs-lookup"><span data-stu-id="ed269-115">Follow the steps documented in [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md) and connect to your subscription using the **login** method.</span></span>

## <a name="create-a-cluster"></a><span data-ttu-id="ed269-116">Een cluster maken</span><span class="sxs-lookup"><span data-stu-id="ed269-116">Create a cluster</span></span>

<span data-ttu-id="ed269-117">De volgende stappen moeten worden uitgevoerd vanaf een opdrachtregel zoals PowerShell of Bash.</span><span class="sxs-lookup"><span data-stu-id="ed269-117">The following steps should be performed from a command line, such as PowerShell or Bash.</span></span>

1. <span data-ttu-id="ed269-118">Gebruik de volgende opdracht om uw Azure-abonnement te verifiëren:</span><span class="sxs-lookup"><span data-stu-id="ed269-118">Use the following command to authenticate to your Azure subscription:</span></span>

        azure login

    <span data-ttu-id="ed269-119">U wordt gevraagd uw naam en wachtwoord opgeven.</span><span class="sxs-lookup"><span data-stu-id="ed269-119">You are prompted to provide your name and password.</span></span> <span data-ttu-id="ed269-120">Als u meerdere Azure-abonnementen hebt, gebruikt u `azure account set <subscriptionname>` instellen van het abonnement dat Azure CLI-opdrachten gebruiken.</span><span class="sxs-lookup"><span data-stu-id="ed269-120">If you have multiple Azure subscriptions, use `azure account set <subscriptionname>` to set the subscription that the Azure CLI commands use.</span></span>

2. <span data-ttu-id="ed269-121">Schakel over naar modus Azure Resource Manager met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="ed269-121">Switch to Azure Resource Manager mode using the following command:</span></span>

        azure config mode arm

3. <span data-ttu-id="ed269-122">Maak een resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ed269-122">Create a resource group.</span></span> <span data-ttu-id="ed269-123">Deze resourcegroep bevat het HDInsight-cluster en storage-account gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="ed269-123">This resource group contains the HDInsight cluster and associated storage account.</span></span>

        azure group create groupname location

    * <span data-ttu-id="ed269-124">Vervang `groupname` met een unieke naam voor de groep.</span><span class="sxs-lookup"><span data-stu-id="ed269-124">Replace `groupname` with a unique name for the group.</span></span>

    * <span data-ttu-id="ed269-125">Vervang `location` met de geografische regio die u wilt maken van de groep in.</span><span class="sxs-lookup"><span data-stu-id="ed269-125">Replace `location` with the geographic region that you want to create the group in.</span></span>

       <span data-ttu-id="ed269-126">Voor een lijst met geldige locaties, gebruikt u de `azure location list` opdracht en gebruik vervolgens een van de locaties van de `Name` kolom.</span><span class="sxs-lookup"><span data-stu-id="ed269-126">For a list of valid locations, use the `azure location list` command, and then use one of the locations from the `Name` column.</span></span>

4. <span data-ttu-id="ed269-127">Een opslagaccount maken.</span><span class="sxs-lookup"><span data-stu-id="ed269-127">Create a storage account.</span></span> <span data-ttu-id="ed269-128">Dit opslagaccount wordt gebruikt als de opslag van de standaard voor het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="ed269-128">This storage account is used as the default storage for the HDInsight cluster.</span></span>

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * <span data-ttu-id="ed269-129">Vervang `groupname` met de naam van de groep in de vorige stap hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ed269-129">Replace `groupname` with the name of the group created in the previous step.</span></span>

    * <span data-ttu-id="ed269-130">Vervang `location` met dezelfde locatie die wordt gebruikt in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="ed269-130">Replace `location` with the same location used in the previous step.</span></span>

    * <span data-ttu-id="ed269-131">Vervang `storagename` met een unieke naam voor het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="ed269-131">Replace `storagename` with a unique name for the storage account.</span></span>

        > [!NOTE]
        > <span data-ttu-id="ed269-132">Gebruik voor meer informatie over de parameters in deze opdracht gebruikt `azure storage account create -h` om help voor deze opdracht te geven.</span><span class="sxs-lookup"><span data-stu-id="ed269-132">For more information on the parameters used in this command, use `azure storage account create -h` to view help for this command.</span></span>

5. <span data-ttu-id="ed269-133">De sleutel die wordt gebruikt voor toegang tot het opslagaccount ophalen.</span><span class="sxs-lookup"><span data-stu-id="ed269-133">Retrieve the key used to access the storage account.</span></span>

        azure storage account keys list -g groupname storagename

    * <span data-ttu-id="ed269-134">Vervang `groupname` met de naam van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ed269-134">Replace `groupname` with the resource group name.</span></span>
    * <span data-ttu-id="ed269-135">Vervang `storagename` met de naam van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="ed269-135">Replace `storagename` with the name of the storage account.</span></span>

     <span data-ttu-id="ed269-136">Opslaan in de gegevens die wordt geretourneerd, de `key` waarde voor `key1`.</span><span class="sxs-lookup"><span data-stu-id="ed269-136">In the data that is returned, save the `key` value for `key1`.</span></span>

6. <span data-ttu-id="ed269-137">Maak een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="ed269-137">Create an HDInsight cluster.</span></span>

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * <span data-ttu-id="ed269-138">Vervang `groupname` met de naam van de resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="ed269-138">Replace `groupname` with the resource group name.</span></span>

    * <span data-ttu-id="ed269-139">Vervang `Hadoop` met het clustertype dat u wilt maken.</span><span class="sxs-lookup"><span data-stu-id="ed269-139">Replace `Hadoop` with the cluster type that you wish to create.</span></span> <span data-ttu-id="ed269-140">Bijvoorbeeld: `Hadoop`, `HBase`, `Kafka`, `Spark`, of `Storm`.</span><span class="sxs-lookup"><span data-stu-id="ed269-140">For example, `Hadoop`, `HBase`, `Kafka`, `Spark`, or `Storm`.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="ed269-141">HDInsight clusters worden geleverd in verschillende typen die met de werkbelasting of technologie die het cluster is afgestemd overeenkomen op.</span><span class="sxs-lookup"><span data-stu-id="ed269-141">HDInsight clusters come in various types, which correspond to the workload or technology that the cluster is tuned for.</span></span> <span data-ttu-id="ed269-142">Er is geen ondersteunde methode om een cluster waarin meerdere typen zoals Storm en HBase op één cluster te maken.</span><span class="sxs-lookup"><span data-stu-id="ed269-142">There is no supported method to create a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span>

    * <span data-ttu-id="ed269-143">Vervang `location` met dezelfde locatie gebruikt in de vorige stappen.</span><span class="sxs-lookup"><span data-stu-id="ed269-143">Replace `location` with the same location used in previous steps.</span></span>

    * <span data-ttu-id="ed269-144">Vervang `storagename` met de naam van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="ed269-144">Replace `storagename` with the storage account name.</span></span>

    * <span data-ttu-id="ed269-145">Vervang `storagekey` met de sleutel in de vorige stap hebt verkregen.</span><span class="sxs-lookup"><span data-stu-id="ed269-145">Replace `storagekey` with the key obtained in the previous step.</span></span>

    * <span data-ttu-id="ed269-146">Voor de `--defaultStorageContainer` parameter, gebruik dezelfde naam als u gebruikt voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="ed269-146">For the `--defaultStorageContainer` parameter, use the same name as you are using for the cluster.</span></span>

    * <span data-ttu-id="ed269-147">Vervang `admin` en `httppassword` met de naam en het wachtwoord dat u gebruiken wilt bij het openen van het cluster via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ed269-147">Replace `admin` and `httppassword` with the name and password you wish to use when accessing the cluster through HTTPS.</span></span>

    * <span data-ttu-id="ed269-148">Vervang `sshuser` en `sshuserpassword` met de gebruikersnaam en wachtwoord die u gebruiken wilt bij het openen van het cluster via SSH</span><span class="sxs-lookup"><span data-stu-id="ed269-148">Replace `sshuser` and `sshuserpassword` with the username and password you wish to use when accessing the cluster using SSH</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="ed269-149">In dit voorbeeld maakt een cluster met twee worker opmerkingen.</span><span class="sxs-lookup"><span data-stu-id="ed269-149">This example creates a cluster with two worker notes.</span></span> <span data-ttu-id="ed269-150">U kunt het aantal worker-knooppunten ook wijzigen nadat de cluster is gemaakt door het uitvoeren van bewerkingen voor vergroten/verkleinen.</span><span class="sxs-lookup"><span data-stu-id="ed269-150">You can also change the number of worker nodes after cluster creation by performing scaling operations.</span></span> <span data-ttu-id="ed269-151">Als u van plan bent over het gebruik van meer dan 32 worker-knooppunten, selecteert u een grootte van het hoofdknooppunt met ten minste 8 kerngeheugens en 14 GB RAM-geheugen.</span><span class="sxs-lookup"><span data-stu-id="ed269-151">If you plan on using more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14-GB RAM.</span></span> <span data-ttu-id="ed269-152">U kunt de grootte van het hoofdknooppunt instellen met behulp van de `--headNodeSize` parameter tijdens het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="ed269-152">You can set the head node size by using the `--headNodeSize` parameter during cluster creation.</span></span>
    >
    > <span data-ttu-id="ed269-153">Zie voor meer informatie over knooppuntgrootten en bijbehorende kosten [HDInsight prijzen](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="ed269-153">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

    <span data-ttu-id="ed269-154">Duurt enkele minuten voor het cluster maken van het proces te voltooien.</span><span class="sxs-lookup"><span data-stu-id="ed269-154">It may take several minutes for the cluster creation process to finish.</span></span> <span data-ttu-id="ed269-155">Meestal ongeveer 15.</span><span class="sxs-lookup"><span data-stu-id="ed269-155">Usually around 15.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="ed269-156">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="ed269-156">Troubleshoot</span></span>

<span data-ttu-id="ed269-157">Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) als u problemen ondervindt met het maken van HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="ed269-157">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed269-158">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ed269-158">Next steps</span></span>

<span data-ttu-id="ed269-159">Nu dat u een HDInsight-cluster met de Azure CLI hebt gemaakt, gebruikt u de volgende voor informatie over het werken met het cluster:</span><span class="sxs-lookup"><span data-stu-id="ed269-159">Now that you have successfully created an HDInsight cluster using the Azure CLI, use the following to learn how to work with your cluster:</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="ed269-160">Hadoop-clusters</span><span class="sxs-lookup"><span data-stu-id="ed269-160">Hadoop clusters</span></span>

* [<span data-ttu-id="ed269-161">Hive gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="ed269-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="ed269-162">Pig gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="ed269-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="ed269-163">MapReduce gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="ed269-163">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="ed269-164">HBase-clusters</span><span class="sxs-lookup"><span data-stu-id="ed269-164">HBase clusters</span></span>

* [<span data-ttu-id="ed269-165">Aan de slag met HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ed269-165">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="ed269-166">Ontwikkelen van Java-toepassingen voor HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="ed269-166">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="ed269-167">Storm-clusters</span><span class="sxs-lookup"><span data-stu-id="ed269-167">Storm clusters</span></span>

* [<span data-ttu-id="ed269-168">Java-topologieën ontwikkelen voor Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="ed269-168">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="ed269-169">Python-onderdelen in Storm op HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="ed269-169">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="ed269-170">Implementeren en bewaken topologieën met Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="ed269-170">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
