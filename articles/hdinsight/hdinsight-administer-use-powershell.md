---
title: aaaManage Hadoop-clusters in HDInsight met PowerShell - Azure | Microsoft Docs
description: Meer informatie over hoe tooperform administratieve taken voor het Hallo Hadoop-clusters in HDInsight met behulp van Azure PowerShell.
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
ms.openlocfilehash: 3df082d752fa8c703db82a54b82b740290af6729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a><span data-ttu-id="a6373-103">Hadoop-clusters in HDInsight met behulp van Azure PowerShell beheren</span><span class="sxs-lookup"><span data-stu-id="a6373-103">Manage Hadoop clusters in HDInsight by using Azure PowerShell</span></span>
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

<span data-ttu-id="a6373-104">Azure PowerShell is een krachtige scriptomgeving toocontrol gebruiken en automatiseren Hallo-implementatie en beheer van uw workloads in Azure.</span><span class="sxs-lookup"><span data-stu-id="a6373-104">Azure PowerShell is a powerful scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="a6373-105">In dit artikel leert u hoe toomanage Hadoop-clusters in Azure HDInsight met behulp van een lokale Azure PowerShell-console via Hallo van Windows PowerShell gebruiken.</span><span class="sxs-lookup"><span data-stu-id="a6373-105">In this article, you will learn how toomanage Hadoop clusters in Azure HDInsight by using a local Azure PowerShell console through hello use of Windows PowerShell.</span></span> <span data-ttu-id="a6373-106">Zie voor lijst Hallo Hallo HDInsight PowerShell-cmdlets [HDInsight cmdlet-verwijzing][hdinsight-powershell-reference].</span><span class="sxs-lookup"><span data-stu-id="a6373-106">For hello list of hello HDInsight PowerShell cmdlets, see [HDInsight cmdlet reference][hdinsight-powershell-reference].</span></span>

<span data-ttu-id="a6373-107">**Vereisten**</span><span class="sxs-lookup"><span data-stu-id="a6373-107">**Prerequisites**</span></span>

<span data-ttu-id="a6373-108">Voordat u dit artikel, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="a6373-108">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="a6373-109">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="a6373-109">**An Azure subscription**.</span></span> <span data-ttu-id="a6373-110">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="a6373-110">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="install-azure-powershell"></a><span data-ttu-id="a6373-111">Azure PowerShell installeren</span><span class="sxs-lookup"><span data-stu-id="a6373-111">Install Azure PowerShell</span></span>
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="a6373-112">Als u Azure PowerShell versie 0,9 hebt geïnstalleerd x, moet u deze verwijderen voordat u een nieuwere versie installeert.</span><span class="sxs-lookup"><span data-stu-id="a6373-112">If you have installed Azure PowerShell version 0.9x, you must uninstall it before installing a newer version.</span></span>

<span data-ttu-id="a6373-113">toocheck versie Hallo Hallo PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a6373-113">toocheck hello version of hello installed PowerShell:</span></span>

    Get-Module *azure*

<span data-ttu-id="a6373-114">toouninstall hello oudere versie, programma's en onderdelen in Configuratiescherm Hallo uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a6373-114">toouninstall hello older version, run Programs and Features in hello control panel.</span></span>

## <a name="create-clusters"></a><span data-ttu-id="a6373-115">Clusters maken</span><span class="sxs-lookup"><span data-stu-id="a6373-115">Create clusters</span></span>
<span data-ttu-id="a6373-116">Zie [maken Linux gebaseerde clusters in HDInsight met behulp van Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="a6373-116">See [Create Linux-based clusters in HDInsight using Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)</span></span>

## <a name="list-clusters"></a><span data-ttu-id="a6373-117">Lijst met clusters</span><span class="sxs-lookup"><span data-stu-id="a6373-117">List clusters</span></span>
<span data-ttu-id="a6373-118">Hallo opdracht toolist na alle clusters in het huidige abonnement hello gebruiken:</span><span class="sxs-lookup"><span data-stu-id="a6373-118">Use hello following command toolist all clusters in hello current subscription:</span></span>

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a><span data-ttu-id="a6373-119">Cluster weergeven</span><span class="sxs-lookup"><span data-stu-id="a6373-119">Show cluster</span></span>
<span data-ttu-id="a6373-120">Gebruik onderstaande opdracht tooshow gegevens van een specifieke cluster in het huidige abonnement Hallo Hallo:</span><span class="sxs-lookup"><span data-stu-id="a6373-120">Use hello following command tooshow details of a specific cluster in hello current subscription:</span></span>

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a><span data-ttu-id="a6373-121">Clusters verwijderen</span><span class="sxs-lookup"><span data-stu-id="a6373-121">Delete clusters</span></span>
<span data-ttu-id="a6373-122">Gebruik Hallo opdracht toodelete een cluster te volgen:</span><span class="sxs-lookup"><span data-stu-id="a6373-122">Use hello following command toodelete a cluster:</span></span>

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

<span data-ttu-id="a6373-123">U kunt ook een cluster verwijderen door het verwijderen van resourcegroep Hallo die Hallo cluster bevat.</span><span class="sxs-lookup"><span data-stu-id="a6373-123">You can also delete a cluster by removing hello resource group that contains hello cluster.</span></span> <span data-ttu-id="a6373-124">Let op: Hiermee verwijdert u alle Hallo bronnen in Hallo-groep met inbegrip van Hallo storage-standaardaccount.</span><span class="sxs-lookup"><span data-stu-id="a6373-124">Please note, this will delete all hello resources in hello group including hello default storage account.</span></span>

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a><span data-ttu-id="a6373-125">Clusters schalen</span><span class="sxs-lookup"><span data-stu-id="a6373-125">Scale clusters</span></span>
<span data-ttu-id="a6373-126">Hallo-cluster schalen van functie kunt u toochange Hallo aantal worker-knooppunten gebruikt door een cluster dat wordt uitgevoerd in Azure HDInsight zonder toore-Hallo cluster maken.</span><span class="sxs-lookup"><span data-stu-id="a6373-126">hello cluster scaling feature allows you toochange hello number of worker nodes used by a cluster that is running in Azure HDInsight without having toore-create hello cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="a6373-127">Alleen clusters met HDInsight versie 3.1.3 of hoger worden ondersteund.</span><span class="sxs-lookup"><span data-stu-id="a6373-127">Only clusters with HDInsight version 3.1.3 or higher are supported.</span></span> <span data-ttu-id="a6373-128">Als u niet zeker Hallo versie van het cluster weet, kunt u de eigenschappenpagina Hallo controleren.</span><span class="sxs-lookup"><span data-stu-id="a6373-128">If you are unsure of hello version of your cluster, you can check hello Properties page.</span></span>  <span data-ttu-id="a6373-129">Zie [lijst en geeft weer clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span><span class="sxs-lookup"><span data-stu-id="a6373-129">See [List and show clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).</span></span>
>
>

<span data-ttu-id="a6373-130">Hallo gevolgen van het aantal gegevensknooppunten voor elk type ondersteund door HDInsight cluster Hallo wijzigen:</span><span class="sxs-lookup"><span data-stu-id="a6373-130">hello impact of changing hello number of data nodes for each type of cluster supported by HDInsight:</span></span>

* <span data-ttu-id="a6373-131">Hadoop</span><span class="sxs-lookup"><span data-stu-id="a6373-131">Hadoop</span></span>

    <span data-ttu-id="a6373-132">Hallo aantal worker-knooppunten van een Hadoop-cluster dat wordt uitgevoerd zonder enige impact op alle taken die in behandeling of wordt uitgevoerd, kunt u naadloos verhogen.</span><span class="sxs-lookup"><span data-stu-id="a6373-132">You can seamlessly increase hello number of worker nodes in a Hadoop cluster that is running without impacting any pending or running jobs.</span></span> <span data-ttu-id="a6373-133">Nieuwe taken kunnen ook worden verzonden tijdens het Hallo-bewerking wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a6373-133">New jobs can also be submitted while hello operation is in progress.</span></span> <span data-ttu-id="a6373-134">Fouten in een bewerking voor schaal worden probleemloos verwerkt zodat hello cluster altijd functioneel is overblijft.</span><span class="sxs-lookup"><span data-stu-id="a6373-134">Failures in a scaling operation are gracefully handled so that hello cluster is always left in a functional state.</span></span>

    <span data-ttu-id="a6373-135">Wanneer een Hadoop-cluster wordt verkleind door het aantal gegevensknooppunten hello te verminderen, worden sommige services in de cluster Hallo Hallo opnieuw gestart.</span><span class="sxs-lookup"><span data-stu-id="a6373-135">When a Hadoop cluster is scaled down by reducing hello number of data nodes, some of hello services in hello cluster are restarted.</span></span> <span data-ttu-id="a6373-136">Dit zorgt ervoor dat alle actieve en in behandeling zijnde taken toofail op Hallo Hallo schalen van de bewerking is voltooid.</span><span class="sxs-lookup"><span data-stu-id="a6373-136">This causes all running and pending jobs toofail at hello completion of hello scaling operation.</span></span> <span data-ttu-id="a6373-137">U kunt echter Hallo taken verzenden zodra Hallo-bewerking voltooid is.</span><span class="sxs-lookup"><span data-stu-id="a6373-137">You can, however, resubmit hello jobs once hello operation is complete.</span></span>
* <span data-ttu-id="a6373-138">HBase</span><span class="sxs-lookup"><span data-stu-id="a6373-138">HBase</span></span>

    <span data-ttu-id="a6373-139">U kunt naadloos toevoegen of verwijderen van knooppunten tooyour HBase-cluster, terwijl deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a6373-139">You can seamlessly add or remove nodes tooyour HBase cluster while it is running.</span></span> <span data-ttu-id="a6373-140">Regionale Servers worden automatisch verdeeld binnen een paar minuten na voltooiing van Hallo bewerking schalen.</span><span class="sxs-lookup"><span data-stu-id="a6373-140">Regional Servers are automatically balanced within a few minutes of completing hello scaling operation.</span></span> <span data-ttu-id="a6373-141">U kunt echter ook handmatig Hallo regionale servers verdelen door logboekregistratie in toohello headnode van het cluster en actieve Hallo volgende opdrachten uit een opdrachtpromptvenster:</span><span class="sxs-lookup"><span data-stu-id="a6373-141">However, you can also manually balance hello regional servers by logging in toohello headnode of cluster and running hello following commands from a command prompt window:</span></span>

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* <span data-ttu-id="a6373-142">Storm</span><span class="sxs-lookup"><span data-stu-id="a6373-142">Storm</span></span>

    <span data-ttu-id="a6373-143">U kunt naadloos toevoegen of verwijderen van gegevens knooppunten tooyour Storm-cluster, terwijl deze wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="a6373-143">You can seamlessly add or remove data nodes tooyour Storm cluster while it is running.</span></span> <span data-ttu-id="a6373-144">Maar nadat de bewerking schalen Hallo installatie is voltooid, moet u toorebalance Hallo topologie.</span><span class="sxs-lookup"><span data-stu-id="a6373-144">But after a successful completion of hello scaling operation, you will need toorebalance hello topology.</span></span>

    <span data-ttu-id="a6373-145">Herverdeling kan worden uitgevoerd op twee manieren:</span><span class="sxs-lookup"><span data-stu-id="a6373-145">Rebalancing can be accomplished in two ways:</span></span>

  * <span data-ttu-id="a6373-146">Storm-webgebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="a6373-146">Storm web UI</span></span>
  * <span data-ttu-id="a6373-147">Hulpprogramma voor opdrachtregelinterface (CLI)</span><span class="sxs-lookup"><span data-stu-id="a6373-147">Command-line interface (CLI) tool</span></span>

    <span data-ttu-id="a6373-148">Raadpleeg toohello [Apache Storm documentatie](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="a6373-148">Please refer toohello [Apache Storm documentation](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) for more details.</span></span>

    <span data-ttu-id="a6373-149">Hallo Storm-webgebruikersinterface is beschikbaar op Hallo HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="a6373-149">hello Storm web UI is available on hello HDInsight cluster:</span></span>

    ![HDInsight storm scale deel opnieuw](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    <span data-ttu-id="a6373-151">Hier volgt een voorbeeld hoe toouse Hallo CLI toorebalance Hallo Storm-topologie opdracht:</span><span class="sxs-lookup"><span data-stu-id="a6373-151">Here is an example how toouse hello CLI command toorebalance hello Storm topology:</span></span>

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

<span data-ttu-id="a6373-152">toochange hello Hadoop-clusters met behulp van Azure PowerShell, uitvoeren van de volgende opdracht vanaf een clientcomputer Hallo:</span><span class="sxs-lookup"><span data-stu-id="a6373-152">toochange hello Hadoop cluster size by using Azure PowerShell, run hello following command from a client machine:</span></span>

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a><span data-ttu-id="a6373-153">Toegang verlenen of in te trekken</span><span class="sxs-lookup"><span data-stu-id="a6373-153">Grant/revoke access</span></span>
<span data-ttu-id="a6373-154">HDInsight-clusters hebben Hallo HTTP-webservices (al deze services hebt RESTful eindpunten) te volgen:</span><span class="sxs-lookup"><span data-stu-id="a6373-154">HDInsight clusters have hello following HTTP web services (all of these services have RESTful endpoints):</span></span>

* <span data-ttu-id="a6373-155">ODBC</span><span class="sxs-lookup"><span data-stu-id="a6373-155">ODBC</span></span>
* <span data-ttu-id="a6373-156">JDBC</span><span class="sxs-lookup"><span data-stu-id="a6373-156">JDBC</span></span>
* <span data-ttu-id="a6373-157">Ambari</span><span class="sxs-lookup"><span data-stu-id="a6373-157">Ambari</span></span>
* <span data-ttu-id="a6373-158">Oozie</span><span class="sxs-lookup"><span data-stu-id="a6373-158">Oozie</span></span>
* <span data-ttu-id="a6373-159">Templeton</span><span class="sxs-lookup"><span data-stu-id="a6373-159">Templeton</span></span>

<span data-ttu-id="a6373-160">Standaard worden deze services verleend om toegang te krijgen.</span><span class="sxs-lookup"><span data-stu-id="a6373-160">By default, these services are granted for access.</span></span> <span data-ttu-id="a6373-161">U kunt in te trekken/grant Hallo toegang.</span><span class="sxs-lookup"><span data-stu-id="a6373-161">You can revoke/grant hello access.</span></span> <span data-ttu-id="a6373-162">toorevoke:</span><span class="sxs-lookup"><span data-stu-id="a6373-162">toorevoke:</span></span>

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

<span data-ttu-id="a6373-163">toogrant:</span><span class="sxs-lookup"><span data-stu-id="a6373-163">toogrant:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    # Credential option 1
    $hadoopUserName = "admin"
    $hadoopUserPassword = "<Enter hello Password>"
    $hadoopUserPW = ConvertTo-SecureString -String $hadoopUserPassword -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential($hadoopUserName,$hadoopUserPW)

    # Credential option 2
    #$credential = Get-Credential -Message "Enter hello HTTP username and password:" -UserName "admin"

    Grant-AzureRmHDInsightHttpServicesAccess -ClusterName $clusterName -HttpCredential $credential

> [!NOTE]
> <span data-ttu-id="a6373-164">Door het Hallo toegang verlenen/intrekken, wordt u opnieuw ingesteld Hallo cluster-gebruikersnaam en wachtwoord.</span><span class="sxs-lookup"><span data-stu-id="a6373-164">By granting/revoking hello access, you will reset hello cluster user name and password.</span></span>
>
>

<span data-ttu-id="a6373-165">Dit kan ook worden gedaan via Hallo Portal.</span><span class="sxs-lookup"><span data-stu-id="a6373-165">This can also be done via hello Portal.</span></span> <span data-ttu-id="a6373-166">Zie [HDInsight beheren met behulp van Azure-portal Hallo][hdinsight-admin-portal].</span><span class="sxs-lookup"><span data-stu-id="a6373-166">See [Administer HDInsight by using hello Azure portal][hdinsight-admin-portal].</span></span>

## <a name="update-http-user-credentials"></a><span data-ttu-id="a6373-167">HTTP-gebruikersreferenties updaten</span><span class="sxs-lookup"><span data-stu-id="a6373-167">Update HTTP user credentials</span></span>
<span data-ttu-id="a6373-168">Is Hallo dezelfde procedure als [Grant/revoke HTTP toegang](#grant/revoke-access). Als het cluster Hallo Hallo HTTP-toegang is verleend, moet u het eerst intrekken.</span><span class="sxs-lookup"><span data-stu-id="a6373-168">It is hello same procedure as [Grant/revoke HTTP access](#grant/revoke-access).If hello cluster has been granted hello HTTP access, you must first revoke it.</span></span>  <span data-ttu-id="a6373-169">Vervolgens toegang verlenen en Hallo met nieuwe HTTP gebruikersgegevens.</span><span class="sxs-lookup"><span data-stu-id="a6373-169">And then grant hello access with new HTTP user credentials.</span></span>

## <a name="find-hello-default-storage-account"></a><span data-ttu-id="a6373-170">Hallo standaardopslagaccount vinden</span><span class="sxs-lookup"><span data-stu-id="a6373-170">Find hello default storage account</span></span>
<span data-ttu-id="a6373-171">Hallo volgende Powershell-script laat zien hoe tooget Hallo naam van het standaardopslagaccount en Hallo standaard opslagaccountsleutel voor een cluster.</span><span class="sxs-lookup"><span data-stu-id="a6373-171">hello following Powershell script demonstrates how tooget hello default storage account name and hello default storage account key for a cluster.</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-hello-resource-group"></a><span data-ttu-id="a6373-172">Hallo resourcegroep vinden</span><span class="sxs-lookup"><span data-stu-id="a6373-172">Find hello resource group</span></span>
<span data-ttu-id="a6373-173">In de modus Resource Manager hello hoort elk HDInsight-cluster tooan Azure-resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="a6373-173">In hello Resource Manager mode, each HDInsight cluster belongs tooan Azure resource group.</span></span>  <span data-ttu-id="a6373-174">toofind hello resourcegroep:</span><span class="sxs-lookup"><span data-stu-id="a6373-174">toofind hello resource group:</span></span>

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a><span data-ttu-id="a6373-175">Verzenden van taken</span><span class="sxs-lookup"><span data-stu-id="a6373-175">Submit jobs</span></span>
<span data-ttu-id="a6373-176">**toosubmit MapReduce-taken**</span><span class="sxs-lookup"><span data-stu-id="a6373-176">**toosubmit MapReduce jobs**</span></span>

<span data-ttu-id="a6373-177">Zie [uitvoeren Hadoop-MapReduce-voorbeelden in HDInsight op basis van Windows](hdinsight-run-samples.md).</span><span class="sxs-lookup"><span data-stu-id="a6373-177">See [Run Hadoop MapReduce samples in Windows-based HDInsight](hdinsight-run-samples.md).</span></span>

<span data-ttu-id="a6373-178">**toosubmit Hive-taken**</span><span class="sxs-lookup"><span data-stu-id="a6373-178">**toosubmit Hive jobs**</span></span>

<span data-ttu-id="a6373-179">Zie [uitvoeren Hive-query's met behulp van PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a6373-179">See [Run Hive queries using PowerShell](hdinsight-hadoop-use-hive-powershell.md).</span></span>

<span data-ttu-id="a6373-180">**toosubmit Pig-taken**</span><span class="sxs-lookup"><span data-stu-id="a6373-180">**toosubmit Pig jobs**</span></span>

<span data-ttu-id="a6373-181">Zie [uitvoeren Pig-taken met behulp van PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="a6373-181">See [Run Pig jobs using PowerShell](hdinsight-hadoop-use-pig-powershell.md).</span></span>

<span data-ttu-id="a6373-182">**toosubmit Sqoop taken**</span><span class="sxs-lookup"><span data-stu-id="a6373-182">**toosubmit Sqoop jobs**</span></span>

<span data-ttu-id="a6373-183">Zie [Sqoop gebruiken met HDInsight](hdinsight-use-sqoop.md).</span><span class="sxs-lookup"><span data-stu-id="a6373-183">See [Use Sqoop with HDInsight](hdinsight-use-sqoop.md).</span></span>

<span data-ttu-id="a6373-184">**toosubmit Oozie taken**</span><span class="sxs-lookup"><span data-stu-id="a6373-184">**toosubmit Oozie jobs**</span></span>

<span data-ttu-id="a6373-185">Zie [Oozie gebruiken met Hadoop toodefine en voer een werkstroom in HDInsight](hdinsight-use-oozie.md).</span><span class="sxs-lookup"><span data-stu-id="a6373-185">See [Use Oozie with Hadoop toodefine and run a workflow in HDInsight](hdinsight-use-oozie.md).</span></span>

## <a name="upload-data-tooazure-blob-storage"></a><span data-ttu-id="a6373-186">Uploaden van gegevens tooAzure Blob-opslag</span><span class="sxs-lookup"><span data-stu-id="a6373-186">Upload data tooAzure Blob storage</span></span>
<span data-ttu-id="a6373-187">Zie [uploaden van gegevens tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="a6373-187">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

## <a name="see-also"></a><span data-ttu-id="a6373-188">Zie ook</span><span class="sxs-lookup"><span data-stu-id="a6373-188">See Also</span></span>
* <span data-ttu-id="a6373-189">[HDInsight-cmdlet-naslagdocumentatie][hdinsight-powershell-reference]</span><span class="sxs-lookup"><span data-stu-id="a6373-189">[HDInsight cmdlet reference documentation][hdinsight-powershell-reference]</span></span>
* <span data-ttu-id="a6373-190">[HDInsight beheren met behulp van hello Azure-portal][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="a6373-190">[Administer HDInsight by using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="a6373-191">[HDInsight met behulp van een opdrachtregelinterface beheren][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="a6373-191">[Administer HDInsight using a command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="a6373-192">[HDInsight-clusters maken][hdinsight-provision]</span><span class="sxs-lookup"><span data-stu-id="a6373-192">[Create HDInsight clusters][hdinsight-provision]</span></span>
* <span data-ttu-id="a6373-193">[Uploaden van gegevens tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="a6373-193">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="a6373-194">[Hadoop-taken programmatisch verzenden][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="a6373-194">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="a6373-195">[Aan de slag met Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="a6373-195">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>

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
