---
title: Hadoop-clusters in HDInsight met PowerShell - Azure beheren | Microsoft Docs
description: Informatie over het uitvoeren van beheertaken voor het Hadoop-clusters in HDInsight met behulp van Azure PowerShell.
services: hdinsight
editor: cgronlun
manager: jhubbard
tags: azure-portal
author: mumian
documentationcenter: 
ms.assetid: bfdfa754-18e5-4ef9-b0d6-2dbdcebc0283
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: c47dabd7c4aa4ba0be08c419989e536711f03677
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a><span data-ttu-id="c18cd-103">Hadoop-clusters in HDInsight met behulp van Azure PowerShell beheren</span><span class="sxs-lookup"><span data-stu-id="c18cd-103">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="c18cd-104">Azure PowerShell is een krachtige scriptomgeving op servers die u gebruiken kunt om te beheren en de implementatie en beheer van uw workloads in Azure automatiseren.</span><span class="sxs-lookup"><span data-stu-id="c18cd-104">Azure PowerShell is a powerful scripting environment that you can use to control and automate the deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="c18cd-105">In dit artikel leert u hoe u in Azure HDInsight Hadoop-clusters beheren met behulp van een lokale Azure PowerShell-console door het gebruik van Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c18cd-105">In this article, you will learn how to manage Hadoop clusters in Azure HDInsight by using a local Azure PowerShell console through the use of Windows PowerShell.</span></span> <span data-ttu-id="c18cd-106">Zie voor een overzicht van de HDInsight-PowerShell-cmdlets [HDInsight cmdlet-verwijzing][hdinsight-powershell-reference].</span><span class="sxs-lookup"><span data-stu-id="c18cd-106">For the list of the HDInsight PowerShell cmdlets, see [HDInsight cmdlet reference][hdinsight-powershell-reference].</span></span>

<span data-ttu-id="c18cd-107">**Vereisten**</span><span class="sxs-lookup"><span data-stu-id="c18cd-107">**Prerequisites**</span></span>

<span data-ttu-id="c18cd-108">Voordat u dit artikel gaat lezen, moet u beschikken over het volgende:</span><span class="sxs-lookup"><span data-stu-id="c18cd-108">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="c18cd-109">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="c18cd-109">**An Azure subscription**.</span></span> <span data-ttu-id="c18cd-110">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="c18cd-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="c18cd-111">Azure PowerShell installeren</span><span class="sxs-lookup"><span data-stu-id="c18cd-111">Install Azure PowerShell</span></span>
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="c18cd-112">Als u Azure PowerShell versie 0,9 hebt geïnstalleerd x, moet u deze verwijderen voordat u een nieuwere versie installeert.</span><span class="sxs-lookup"><span data-stu-id="c18cd-112">If you have installed Azure PowerShell version 0.9x, you must uninstall it before installing a newer version.</span></span>

<span data-ttu-id="c18cd-113">De versie van de geïnstalleerde PowerShell controleren:</span><span class="sxs-lookup"><span data-stu-id="c18cd-113">To check the version of the installed PowerShell:</span></span>

    Get-Module *azure*

<span data-ttu-id="c18cd-114">Voer voor het verwijderen van de oudere versie, programma's en onderdelen in het Configuratiescherm.</span><span class="sxs-lookup"><span data-stu-id="c18cd-114">To uninstall the older version, run Programs and Features in the control panel.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="c18cd-115">Clusters maken</span><span class="sxs-lookup"><span data-stu-id="c18cd-115">Create clusters</span></span>
<span data-ttu-id="c18cd-116">Zie [maken Linux gebaseerde clusters in HDInsight met behulp van Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="c18cd-116">See [Create Linux-based clusters in HDInsight using Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="c18cd-117">Lijst met clusters</span><span class="sxs-lookup"><span data-stu-id="c18cd-117">List clusters</span></span>
<span data-ttu-id="c18cd-118">Gebruik de volgende opdracht voor een lijst met alle clusters in het huidige abonnement:</span><span class="sxs-lookup"><span data-stu-id="c18cd-118">Use the following command to list all clusters in the current subscription:</span></span>

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a><span data-ttu-id="c18cd-119">Cluster weergeven</span><span class="sxs-lookup"><span data-stu-id="c18cd-119">Show cluster</span></span>
<span data-ttu-id="c18cd-120">Gebruik de volgende opdracht om details van een specifiek cluster in het huidige abonnement weer te geven:</span><span class="sxs-lookup"><span data-stu-id="c18cd-120">Use the following command to show details of a specific cluster in the current subscription:</span></span>

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a><span data-ttu-id="c18cd-121">Clusters verwijderen</span><span class="sxs-lookup"><span data-stu-id="c18cd-121">Delete clusters</span></span>
<span data-ttu-id="c18cd-122">Gebruik de volgende opdracht om te verwijderen van een cluster:</span><span class="sxs-lookup"><span data-stu-id="c18cd-122">Use the following command to delete a cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

<span data-ttu-id="c18cd-123">U kunt ook een cluster verwijderen door het verwijderen van de resourcegroep waarin het cluster.</span><span class="sxs-lookup"><span data-stu-id="c18cd-123">You can also delete a cluster by removing the resource group that contains the cluster.</span></span> <span data-ttu-id="c18cd-124">Let op: Hiermee verwijdert u alle resources in de groep met inbegrip van het standaardopslagaccount.</span><span class="sxs-lookup"><span data-stu-id="c18cd-124">Please note, this will delete all the resources in the group including the default storage account.</span></span>

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="c18cd-125">Clusters schalen</span><span class="sxs-lookup"><span data-stu-id="c18cd-125">Scale clusters</span></span>
<span data-ttu-id="c18cd-126">Het schalen van de functie cluster kunt u het aantal worker-knooppunten gebruikt door een cluster dat wordt uitgevoerd in Azure HDInsight zonder te hoeven maken van het cluster opnieuw wijzigen.</span><span class="sxs-lookup"><span data-stu-id="c18cd-126">The cluster scaling feature allows you to change the number of worker nodes used by a cluster that is running in Azure HDInsight without having to re-create the cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="c18cd-127">Alleen clusters met HDInsight versie 3.1.3 of hoger worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="c18cd-127">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="c18cd-128">Als u de versie van het cluster niet zeker weet, kunt u de pagina eigenschappen controleren.</span><span class="sxs-lookup"><span data-stu-id="c18cd-128">If you are unsure of the version of your cluster, you can check the Properties page.</span></span>  <span data-ttu-id="c18cd-129">Zie [lijst en geeft weer clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="c18cd-129">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="c18cd-130">De gevolgen van het wijzigen van het aantal gegevensknooppunten voor elk type van ondersteund door de HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="c18cd-130">The impact of changing the number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="c18cd-131">Hadoop</span><span class="sxs-lookup"><span data-stu-id="c18cd-131">Hadoop</span></span>

    <span data-ttu-id="c18cd-132">U kunt naadloos Verhoog het aantal worker-knooppunten van een Hadoop-cluster dat wordt uitgevoerd zonder enige impact op alle taken die in behandeling of wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c18cd-132">You can seamlessly increase the number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="c18cd-133">Nieuwe taken kunnen ook worden verzonden terwijl de bewerking uitgevoerd wordt.</span><span class="sxs-lookup"><span data-stu-id="c18cd-133">New jobs can also be submitted while the operation is in progress.</span></span> <span data-ttu-id="c18cd-134">Fouten in een bewerking voor schaal worden probleemloos verwerkt zodat het cluster altijd in een functionele staat blijft.</span><span class="sxs-lookup"><span data-stu-id="c18cd-134">Failures in a scaling operation are gracefully handled so that the cluster is always left in a functional state.</span></span>

    <span data-ttu-id="c18cd-135">Wanneer een Hadoop-cluster wordt verkleind door het aantal gegevensknooppunten te verminderen, zijn sommige van de services in het cluster opnieuw gestart.</span><span class="sxs-lookup"><span data-stu-id="c18cd-135">When a Hadoop cluster is scaled down by reducing the number of data nodes, some of the services in the cluster are restarted.</span></span> <span data-ttu-id="c18cd-136">Dit zorgt ervoor dat alle actieve en in behandeling zijnde taken mislukken na het voltooien van de bewerking uit te schalen.</span><span class="sxs-lookup"><span data-stu-id="c18cd-136">This causes all running and pending jobs to fail at the completion of the scaling operation.</span></span> <span data-ttu-id="c18cd-137">U kunt echter de taken verzenden zodra de bewerking voltooid is.</span><span class="sxs-lookup"><span data-stu-id="c18cd-137">You can, however, resubmit the jobs once the operation is complete.</span></span>
* <span data-ttu-id="c18cd-138">HBase</span><span class="sxs-lookup"><span data-stu-id="c18cd-138">HBase</span></span>

    <span data-ttu-id="c18cd-139">U kunt naadloos toevoegen of verwijderen van knooppunten in uw HBase-cluster, terwijl deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c18cd-139">You can seamlessly add or remove nodes to your HBase cluster while it is running.</span></span> <span data-ttu-id="c18cd-140">Regionale Servers worden automatisch verdeeld binnen een paar minuten na voltooiing van de bewerking uit te schalen.</span><span class="sxs-lookup"><span data-stu-id="c18cd-140">Regional Servers are automatically balanced within a few minutes of completing the scaling operation.</span></span> <span data-ttu-id="c18cd-141">U kunt echter ook handmatig de regionale servers verdelen door aanmelden bij de headnode van cluster en het gebruik van de volgende opdrachten vanuit een opdrachtpromptvenster:</span><span class="sxs-lookup"><span data-stu-id="c18cd-141">However, you can also manually balance the regional servers by logging in to the headnode of cluster and running the following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="c18cd-142">Storm</span><span class="sxs-lookup"><span data-stu-id="c18cd-142">Storm</span></span>

    <span data-ttu-id="c18cd-143">U kunt naadloos toevoegen of verwijderen van gegevensknooppunten naar uw Storm-cluster, terwijl deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="c18cd-143">You can seamlessly add or remove data nodes to your Storm cluster while it is running.</span></span> <span data-ttu-id="c18cd-144">Maar na een geslaagde voltooiing van de bewerking uit te schalen, moet u de topologie opnieuw verdelen.</span><span class="sxs-lookup"><span data-stu-id="c18cd-144">But after a successful completion of the scaling operation, you will need to rebalance the topology.</span></span>

    <span data-ttu-id="c18cd-145">Herverdeling kan worden uitgevoerd op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="c18cd-145">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="c18cd-146">Storm-webgebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="c18cd-146">Storm web UI</span></span>
  * <span data-ttu-id="c18cd-147">Hulpprogramma voor opdrachtregelinterface (CLI)</span><span class="sxs-lookup"><span data-stu-id="c18cd-147">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="c18cd-148">Raadpleeg de [Apache Storm documentatie](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="c18cd-148">Please refer to the [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="c18cd-149">De Storm-webgebruikersinterface is beschikbaar op het HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="c18cd-149">The Storm web UI is available on the HDInsight cluster:</span></span>

    ![HDInsight storm scale deel opnieuw](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    <span data-ttu-id="c18cd-151">Hier volgt een voorbeeld van hoe u met de opdracht CLI opnieuw verdelen van de Storm-topologie:</span><span class="sxs-lookup"><span data-stu-id="c18cd-151">Here is an example how to use the CLI command to rebalance the Storm topology:</span></span>

        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="c18cd-152">Als u wilt de grootte van Hadoop-cluster wijzigen met behulp van Azure PowerShell, voer de volgende opdracht vanaf een clientcomputer:</span><span class="sxs-lookup"><span data-stu-id="c18cd-152">To change the Hadoop cluster size by using Azure PowerShell, run the following command from a client machine:</span></span>

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a><span data-ttu-id="c18cd-153">Toegang verlenen of in te trekken</span><span class="sxs-lookup"><span data-stu-id="c18cd-153">Grant/revoke access</span></span>
<span data-ttu-id="c18cd-154">HDInsight-clusters hebben de volgende HTTP-webservices (al deze services hebt RESTful eindpunten):</span><span class="sxs-lookup"><span data-stu-id="c18cd-154">HDInsight clusters have the following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="c18cd-155">ODBC</span><span class="sxs-lookup"><span data-stu-id="c18cd-155">ODBC</span></span>
* <span data-ttu-id="c18cd-156">JDBC</span><span class="sxs-lookup"><span data-stu-id="c18cd-156">JDBC</span></span>
* <span data-ttu-id="c18cd-157">Ambari</span><span class="sxs-lookup"><span data-stu-id="c18cd-157">Ambari</span></span>
* <span data-ttu-id="c18cd-158">Oozie</span><span class="sxs-lookup"><span data-stu-id="c18cd-158">Oozie</span></span>
* <span data-ttu-id="c18cd-159">Templeton</span><span class="sxs-lookup"><span data-stu-id="c18cd-159">Templeton</span></span>

<span data-ttu-id="c18cd-160">Standaard worden deze services verleend om toegang te krijgen.</span><span class="sxs-lookup"><span data-stu-id="c18cd-160">By default, these services are granted for access.</span></span> <span data-ttu-id="c18cd-161">U kunt in te trekken/verlenen toegang.</span><span class="sxs-lookup"><span data-stu-id="c18cd-161">You can revoke/grant the access.</span></span> <span data-ttu-id="c18cd-162">Voor het intrekken van:</span><span class="sxs-lookup"><span data-stu-id="c18cd-162">To revoke:</span></span>

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

<span data-ttu-id="c18cd-163">Om toegang te verlenen:</span><span class="sxs-lookup"><span data-stu-id="c18cd-163">To grant:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter the Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter the HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> <span data-ttu-id="c18cd-164">Door de toegang verlenen/intrekken, stelt u de cluster-gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="c18cd-164">By granting/revoking the access, you will reset the cluster user name and password.</span></span>
>
>

<span data-ttu-id="c18cd-165">Dit kan ook worden gedaan via de Portal.</span><span class="sxs-lookup"><span data-stu-id="c18cd-165">This can also be done via the Portal.</span></span> <span data-ttu-id="c18cd-166">Zie [HDInsight beheren met behulp van de Azure-portal][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="c18cd-166">See [Administer HDInsight by using the Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="c18cd-167">HTTP-gebruikersreferenties updaten</span><span class="sxs-lookup"><span data-stu-id="c18cd-167">Update HTTP user credentials</span></span>
<span data-ttu-id="c18cd-168">Dit is dezelfde procedure als [Grant/revoke HTTP toegang](#grant/revoke-access). Als het cluster heeft de HTTP-toegang is verleend, moet u het eerst intrekken.</span><span class="sxs-lookup"><span data-stu-id="c18cd-168">It is the same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If the cluster has been granted the HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="c18cd-169">Vervolgens toegang verlenen en de met nieuwe HTTP gebruikersgegevens.</span><span class="sxs-lookup"><span data-stu-id="c18cd-169">And then grant the access with new HTTP user credentials.</span></span>

## <a name="find-the-default-storage-account"></a><span data-ttu-id="c18cd-170">Het standaardopslagaccount vinden</span><span class="sxs-lookup"><span data-stu-id="c18cd-170">Find the default storage account</span></span>
<span data-ttu-id="c18cd-171">De volgende Powershell-script laat zien hoe de naam van het standaardopslagaccount en de standaard opslagaccountsleutel voor een cluster.</span><span class="sxs-lookup"><span data-stu-id="c18cd-171">The following Powershell script demonstrates how to get the default storage account name and the default storage account key for a cluster.</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-the-resource-group"></a><span data-ttu-id="c18cd-172">De resourcegroep niet vinden</span><span class="sxs-lookup"><span data-stu-id="c18cd-172">Find the resource group</span></span>
<span data-ttu-id="c18cd-173">In de modus Resource Manager behoort elk HDInsight-cluster tot een Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c18cd-173">In the Resource Manager mode, each HDInsight cluster belongs to an Azure resource group.</span></span>  <span data-ttu-id="c18cd-174">Zoek de resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="c18cd-174">To find the resource group:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a><span data-ttu-id="c18cd-175">Verzenden van taken</span><span class="sxs-lookup"><span data-stu-id="c18cd-175">Submit jobs</span></span>
<span data-ttu-id="c18cd-176">**MapReduce-taken verzenden**</span><span class="sxs-lookup"><span data-stu-id="c18cd-176">**To submit MapReduce jobs**</span></span>

<span data-ttu-id="c18cd-177">Zie [uitvoeren Hadoop-MapReduce-voorbeelden in HDInsight op basis van Windows](hdinsight-run-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c18cd-177">See [Run Hadoop MapReduce samples in Windows-based HDInsight](hdinsight-run-samples.md).</span></span>

<span data-ttu-id="c18cd-178">**Hive-taken verzenden**</span><span class="sxs-lookup"><span data-stu-id="c18cd-178">**To submit Hive jobs**</span></span>

<span data-ttu-id="c18cd-179">Zie [uitvoeren Hive-query's met behulp van PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c18cd-179">See [Run Hive queries using PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span></span>

<span data-ttu-id="c18cd-180">**Pig-taken verzenden**</span><span class="sxs-lookup"><span data-stu-id="c18cd-180">**To submit Pig jobs**</span></span>

<span data-ttu-id="c18cd-181">Zie [uitvoeren Pig-taken met behulp van PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c18cd-181">See [Run Pig jobs using PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span></span>

<span data-ttu-id="c18cd-182">**Om Sqoop taken te verzenden**</span><span class="sxs-lookup"><span data-stu-id="c18cd-182">**To submit Sqoop jobs**</span></span>

<span data-ttu-id="c18cd-183">Zie [Sqoop gebruiken met HDInsight](hdinsight-use-sqoop.md).</span><span class="sxs-lookup"><span data-stu-id="c18cd-183">See [Use Sqoop with HDInsight](hdinsight-use-sqoop.md).</span></span>

<span data-ttu-id="c18cd-184">**Oozie-taken verzenden**</span><span class="sxs-lookup"><span data-stu-id="c18cd-184">**To submit Oozie jobs**</span></span>

<span data-ttu-id="c18cd-185">Zie [Oozie gebruiken met Hadoop om te definiëren en uitvoeren van een werkstroom in HDInsight](hdinsight-use-oozie.md).</span><span class="sxs-lookup"><span data-stu-id="c18cd-185">See [Use Oozie with Hadoop to define and run a workflow in HDInsight](hdinsight-use-oozie.md).</span></span>

## <a name="upload-data-to-azure-blob-storage"></a><span data-ttu-id="c18cd-186">Gegevens uploaden naar Azure Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="c18cd-186">Upload data to Azure Blob storage</span></span>
<span data-ttu-id="c18cd-187">Zie [Gegevens uploaden naar HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="c18cd-187">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="c18cd-188">Zie ook</span><span class="sxs-lookup"><span data-stu-id="c18cd-188">See Also</span></span>
* <span data-ttu-id="c18cd-189">[HDInsight-cmdlet-naslagdocumentatie][hdinsight-powershell-reference]</span><span class="sxs-lookup"><span data-stu-id="c18cd-189">[HDInsight cmdlet reference documentation][hdinsight-powershell-reference]</span></span>
* <span data-ttu-id="c18cd-190">[HDInsight beheren met behulp van de Azure-portal][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="c18cd-190">[Administer HDInsight by using the Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="c18cd-191">[HDInsight met behulp van een opdrachtregelinterface beheren][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="c18cd-191">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="c18cd-192">[HDInsight-clusters maken][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="c18cd-192">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="c18cd-193">[Gegevens uploaden naar HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="c18cd-193">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="c18cd-194">[Hadoop-taken programmatisch verzenden][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="c18cd-194">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="c18cd-195">[Aan de slag met Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="c18cd-195">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-provision-custom-options]: hdinsight-hadoop-provision-linux-clusters.md#configuration
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-flight]: hdinsight-analyze-flight-delay-data.md

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[image-hdi-ps-provision]: ./media/hdinsight-administer-use-powershell/HDI.PS.Provision.png
