---
title: Hadoop-clusters in HDInsight met behulp aaaMonitor Ambari-API - hello Azure | Microsoft Docs
description: "Hallo Apache Ambari APIs gebruiken voor het maken, beheren en bewaken van Hadoop-clusters. API's en hulpprogramma's voor intuïtieve operators verbergen Hallo complexiteit van Hadoop"
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
editor: cgronlun
manager: jhubbard
ms.assetid: 052135b3-d497-4acc-92ff-71cee49356ff
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: d61a8aae5ddfcd7d44f2e4cc899e0a4da5e5fdcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-hadoop-clusters-in-hdinsight-using-hello-ambari-api"></a><span data-ttu-id="cd126-104">Monitor voor Hadoop-clusters in HDInsight met behulp van Hallo Ambari-API</span><span class="sxs-lookup"><span data-stu-id="cd126-104">Monitor Hadoop clusters in HDInsight using hello Ambari API</span></span>
<span data-ttu-id="cd126-105">Meer informatie over hoe toomonitor HDInsight-clusters met behulp van Ambari APIs.</span><span class="sxs-lookup"><span data-stu-id="cd126-105">Learn how toomonitor HDInsight clusters by using Ambari APIs.</span></span>

> [!NOTE]
> <span data-ttu-id="cd126-106">Hallo-informatie in dit artikel is hoofdzakelijk voor HDInsight op basis van Windows-clusters, die geen alleen-lezen-versie van Hallo Ambari REST-API.</span><span class="sxs-lookup"><span data-stu-id="cd126-106">hello information in this article is primarily for Windows-based HDInsight clusters, which provide a read-only version of hello Ambari REST API.</span></span> <span data-ttu-id="cd126-107">Zie voor Linux gebaseerde clusters [beheren Hadoop-clusters met Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="cd126-107">For Linux-based clusters, see [Manage Hadoop clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
> 
> 

## <a name="what-is-ambari"></a><span data-ttu-id="cd126-108">Wat is Ambari?</span><span class="sxs-lookup"><span data-stu-id="cd126-108">What is Ambari?</span></span>
<span data-ttu-id="cd126-109">[Apache Ambari] [ ambari-home] wordt gebruikt voor het inrichten, beheren en controleren van Apache Hadoop-clusters.</span><span class="sxs-lookup"><span data-stu-id="cd126-109">[Apache Ambari][ambari-home] is used for provisioning, managing, and monitoring Apache Hadoop clusters.</span></span> <span data-ttu-id="cd126-110">Bevat een intuïtieve verzameling hulpprogramma's voor operators en een krachtige reeks API's die verbergen Hallo complexiteit van Hadoop Hallo werking van clusters vereenvoudigen.</span><span class="sxs-lookup"><span data-stu-id="cd126-110">It includes an intuitive collection of operator tools and a robust set of APIs that hide hello complexity of Hadoop, simplifying hello operation of clusters.</span></span> <span data-ttu-id="cd126-111">Zie voor meer informatie over Hallo API's, [Ambari-API-referentiemateriaal][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="cd126-111">For more information about hello APIs, see [Ambari API Reference][ambari-api-reference].</span></span> 

<span data-ttu-id="cd126-112">HDInsight ondersteunt momenteel alleen Hallo Ambari bewakingsfunctie.</span><span class="sxs-lookup"><span data-stu-id="cd126-112">HDInsight currently supports only hello Ambari monitoring feature.</span></span> <span data-ttu-id="cd126-113">Ambari-API 1.0 wordt ondersteund door clusters van HDInsight versie 3.0 en 2.1.</span><span class="sxs-lookup"><span data-stu-id="cd126-113">Ambari API 1.0 is supported by HDInsight version 3.0 and 2.1 clusters.</span></span> <span data-ttu-id="cd126-114">In dit artikel bevat informatie over toegang tot Ambari APIs HDInsight versie 3.1 of 2.1-clusters.</span><span class="sxs-lookup"><span data-stu-id="cd126-114">This article covers accessing Ambari APIs on HDInsight version 3.1 and 2.1 clusters.</span></span> <span data-ttu-id="cd126-115">Hallo belangrijkste verschil tussen Hallo twee is dat sommige onderdelen Hallo Hallo introductie van nieuwe mogelijkheden (zoals Hallo taakserver geschiedenis) zijn gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="cd126-115">hello key difference between hello two is that some of hello components have changed with hello introduction of new capabilities (such as hello Job History Server).</span></span> 

<span data-ttu-id="cd126-116">**Vereisten**</span><span class="sxs-lookup"><span data-stu-id="cd126-116">**Prerequisites**</span></span>

<span data-ttu-id="cd126-117">Voordat u deze zelfstudie begint, moet u de volgende items Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="cd126-117">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="cd126-118">**Een werkstation met Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="cd126-118">**A workstation with Azure PowerShell**.</span></span>
* <span data-ttu-id="cd126-119">(Optioneel) [cURL][curl].</span><span class="sxs-lookup"><span data-stu-id="cd126-119">(Optional) [cURL][curl].</span></span> <span data-ttu-id="cd126-120">tooinstall, Zie [cURL Releases en Downloads][curl-download].</span><span class="sxs-lookup"><span data-stu-id="cd126-120">tooinstall it, see [cURL Releases and Downloads][curl-download].</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="cd126-121">Wanneer Hallo cURL-opdracht in Windows, gebruik dubbele aanhalingstekens in plaats van enkele aanhalingstekens voor optiewaarden hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cd126-121">When use hello cURL command in Windows, use double-quotation marks instead of single-quotation marks for hello option values.</span></span>
  > 
  > 
* <span data-ttu-id="cd126-122">**Een Azure HDInsight-cluster**.</span><span class="sxs-lookup"><span data-stu-id="cd126-122">**An Azure HDInsight cluster**.</span></span> <span data-ttu-id="cd126-123">Zie voor instructies over het cluster inrichten [aan de slag met HDInsight] [ hdinsight-get-started] of [HDInsight-clusters inrichten][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="cd126-123">For instructions about cluster provisioning, see [Get started using HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span> <span data-ttu-id="cd126-124">U moet Hallo gegevens toogo Hallo-zelfstudie te volgen:</span><span class="sxs-lookup"><span data-stu-id="cd126-124">You need hello following data toogo through hello tutorial:</span></span>
  
  | <span data-ttu-id="cd126-125">Cluster-eigenschap</span><span class="sxs-lookup"><span data-stu-id="cd126-125">Cluster property</span></span> | <span data-ttu-id="cd126-126">Azure PowerShell de naam van variabele</span><span class="sxs-lookup"><span data-stu-id="cd126-126">Azure PowerShell variable name</span></span> | <span data-ttu-id="cd126-127">Waarde</span><span class="sxs-lookup"><span data-stu-id="cd126-127">Value</span></span> | <span data-ttu-id="cd126-128">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="cd126-128">Description</span></span> |
  | --- | --- | --- | --- |
  |   <span data-ttu-id="cd126-129">De naam van de HDInsight-cluster</span><span class="sxs-lookup"><span data-stu-id="cd126-129">HDInsight cluster name</span></span> |<span data-ttu-id="cd126-130">$clusterName</span><span class="sxs-lookup"><span data-stu-id="cd126-130">$clusterName</span></span> | |<span data-ttu-id="cd126-131">Hallo-naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="cd126-131">hello name of your HDInsight cluster.</span></span> |
  |   <span data-ttu-id="cd126-132">Cluster-gebruikersnaam</span><span class="sxs-lookup"><span data-stu-id="cd126-132">Cluster username</span></span> |<span data-ttu-id="cd126-133">$clusterUsername</span><span class="sxs-lookup"><span data-stu-id="cd126-133">$clusterUsername</span></span> | |<span data-ttu-id="cd126-134">Clusternaam van de gebruiker opgegeven waarop het Hallo-cluster is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="cd126-134">Cluster user name specified when hello cluster was created.</span></span> |
  |   <span data-ttu-id="cd126-135">Het wachtwoord van cluster</span><span class="sxs-lookup"><span data-stu-id="cd126-135">Cluster password</span></span> |<span data-ttu-id="cd126-136">$clusterPassword</span><span class="sxs-lookup"><span data-stu-id="cd126-136">$clusterPassword</span></span> | |<span data-ttu-id="cd126-137">Wachtwoord van de gebruiker cluster.</span><span class="sxs-lookup"><span data-stu-id="cd126-137">Cluster user password.</span></span> |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a><span data-ttu-id="cd126-138">Snel</span><span class="sxs-lookup"><span data-stu-id="cd126-138">Jump-start</span></span>
<span data-ttu-id="cd126-139">Er zijn verschillende manieren toouse Ambari toomonitor HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="cd126-139">There are several ways toouse Ambari toomonitor HDInsight clusters.</span></span>

<span data-ttu-id="cd126-140">**Azure PowerShell gebruiken**</span><span class="sxs-lookup"><span data-stu-id="cd126-140">**Use Azure PowerShell**</span></span>

<span data-ttu-id="cd126-141">Hello Azure PowerShell-script volgen opgehaald Hallo MapReduce-tracering taakinformatie *in een 3.5 HDInsight-cluster.*</span><span class="sxs-lookup"><span data-stu-id="cd126-141">hello following Azure PowerShell script gets hello MapReduce job tracker information *in an HDInsight 3.5 cluster.*</span></span>  <span data-ttu-id="cd126-142">Hallo belangrijkste verschil is dat we deze details van Hallo YARN-service (in plaats van MapReduce) ophalen.</span><span class="sxs-lookup"><span data-stu-id="cd126-142">hello key difference is that we pull these details from hello YARN service (rather than MapReduce).</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

<span data-ttu-id="cd126-143">Hallo volgende PowerShell-script opgehaald Hallo MapReduce-tracering taakinformatie *in een cluster HDInsight 2.1*:</span><span class="sxs-lookup"><span data-stu-id="cd126-143">hello following PowerShell script gets hello MapReduce job tracker information *in an HDInsight 2.1 cluster*:</span></span>

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

<span data-ttu-id="cd126-144">Hallo-uitvoer is:</span><span class="sxs-lookup"><span data-stu-id="cd126-144">hello output is:</span></span>

![Jobtracker uitvoer][img-jobtracker-output]

<span data-ttu-id="cd126-146">**cURL gebruiken**</span><span class="sxs-lookup"><span data-stu-id="cd126-146">**Use cURL**</span></span>

<span data-ttu-id="cd126-147">Hallo volgende voorbeeld wordt clustergegevens via cURL:</span><span class="sxs-lookup"><span data-stu-id="cd126-147">hello following example gets cluster information by using cURL:</span></span>

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

<span data-ttu-id="cd126-148">Hallo-uitvoer is:</span><span class="sxs-lookup"><span data-stu-id="cd126-148">hello output is:</span></span>

    {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/",
     "Clusters":{"cluster_name":"hdi0211v2.azurehdinsight.net","version":"2.1.3.0.432823"},
     "services"[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/hdfs",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"hdfs"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/services/mapreduce",
        "ServiceInfo":{"cluster_name":"hdi0211v2.azurehdinsight.net","service_name":"mapreduce"}}],
     "hosts":[
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/headnode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0"}},
       {"href":"https://hdi0211v2.azurehdinsight.net/ambari/api/v1/clusters/hdi0211v2.azurehdinsight.net/hosts/workernode0",
        "Hosts":{"cluster_name":"hdi0211v2.azurehdinsight.net",
                 "host_name":"headnode0.{ClusterDNS}.azurehdinsight.net"}}]}

<span data-ttu-id="cd126-149">**Hallo-8-10-2014-release**:</span><span class="sxs-lookup"><span data-stu-id="cd126-149">**For hello 10/8/2014 release**:</span></span>

<span data-ttu-id="cd126-150">Wanneer met behulp van Hallo Ambari eindpunt, 'https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}' hello *hostnaam* veld Hallo volledig gekwalificeerde domeinnaam (FQDN) van Hallo-knooppunt in plaats van de hostnaam Hallo retourneert.</span><span class="sxs-lookup"><span data-stu-id="cd126-150">When using hello Ambari endpoint, "https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}", hello *host_name* field returns hello fully qualified domain name (FQDN) of hello node instead of hello host name.</span></span> <span data-ttu-id="cd126-151">Vóór Hallo 8-10-2014-release, in dit voorbeeld gewoon geretourneerd '**headnode0**'.</span><span class="sxs-lookup"><span data-stu-id="cd126-151">Before hello 10/8/2014 release, this example returned simply "**headnode0**".</span></span> <span data-ttu-id="cd126-152">Na Hallo 8-10-2014-release, krijgt u Hallo FQDN-naam '**headnode0. { ClusterDNS} azurehdinsight.NET .net**', zoals wordt weergegeven in het vorige voorbeeld Hallo.</span><span class="sxs-lookup"><span data-stu-id="cd126-152">After hello 10/8/2014 release, you get hello FQDN "**headnode0.{ClusterDNS}.azurehdinsight.net**", as shown in hello previous example.</span></span> <span data-ttu-id="cd126-153">Deze wijziging is vereist toofacilitate scenario's waarbij meerdere clustertypen (zoals HBase en Hadoop) kunnen worden geïmplementeerd in een virtueel netwerk (VNET).</span><span class="sxs-lookup"><span data-stu-id="cd126-153">This change was required toofacilitate scenarios where multiple cluster types (such as HBase and Hadoop) can be deployed in one virtual network (VNET).</span></span> <span data-ttu-id="cd126-154">Dit gebeurt, bijvoorbeeld: bij gebruik van HBase als een back-end-platform voor Hadoop.</span><span class="sxs-lookup"><span data-stu-id="cd126-154">This happens, for example, when using HBase as a back-end platform for Hadoop.</span></span>

## <a name="ambari-monitoring-apis"></a><span data-ttu-id="cd126-155">Ambari-API's bewaken</span><span class="sxs-lookup"><span data-stu-id="cd126-155">Ambari monitoring APIs</span></span>
<span data-ttu-id="cd126-156">Hallo volgende tabel bevat enkele Hallo meest voorkomende Ambari bewaking API-aanroepen.</span><span class="sxs-lookup"><span data-stu-id="cd126-156">hello following table lists some of hello most common Ambari monitoring API calls.</span></span> <span data-ttu-id="cd126-157">Zie voor meer informatie over Hallo API [Ambari-API-referentiemateriaal][ambari-api-reference].</span><span class="sxs-lookup"><span data-stu-id="cd126-157">For more information about hello API, see [Ambari API Reference][ambari-api-reference].</span></span>

| <span data-ttu-id="cd126-158">Monitor voor API-aanroep</span><span class="sxs-lookup"><span data-stu-id="cd126-158">Monitor API call</span></span> | <span data-ttu-id="cd126-159">URI</span><span class="sxs-lookup"><span data-stu-id="cd126-159">URI</span></span> | <span data-ttu-id="cd126-160">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="cd126-160">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cd126-161">Ophalen van clusters</span><span class="sxs-lookup"><span data-stu-id="cd126-161">Get clusters</span></span> |`/api/v1/clusters` | |
| <span data-ttu-id="cd126-162">Cluster-gegevens opvragen.</span><span class="sxs-lookup"><span data-stu-id="cd126-162">Get cluster info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |<span data-ttu-id="cd126-163">clusters, services, hosts</span><span class="sxs-lookup"><span data-stu-id="cd126-163">clusters, services, hosts</span></span> |
| <span data-ttu-id="cd126-164">Ophalen van services</span><span class="sxs-lookup"><span data-stu-id="cd126-164">Get services</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |<span data-ttu-id="cd126-165">Services bevatten: hdfs, mapreduce</span><span class="sxs-lookup"><span data-stu-id="cd126-165">Services include: hdfs, mapreduce</span></span> |
| <span data-ttu-id="cd126-166">Services-gegevens opvragen.</span><span class="sxs-lookup"><span data-stu-id="cd126-166">Get services info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| <span data-ttu-id="cd126-167">Serviceonderdelen downloaden</span><span class="sxs-lookup"><span data-stu-id="cd126-167">Get service components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |<span data-ttu-id="cd126-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span><span class="sxs-lookup"><span data-stu-id="cd126-168">HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker</span></span> |
| <span data-ttu-id="cd126-169">Onderdeel gegevens opvragen.</span><span class="sxs-lookup"><span data-stu-id="cd126-169">Get component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |<span data-ttu-id="cd126-170">ServiceComponentInfo, host-onderdelen, metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="cd126-170">ServiceComponentInfo, host-components, metrics</span></span> |
| <span data-ttu-id="cd126-171">Hosts ophalen</span><span class="sxs-lookup"><span data-stu-id="cd126-171">Get hosts</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |<span data-ttu-id="cd126-172">headnode0, workernode0</span><span class="sxs-lookup"><span data-stu-id="cd126-172">headnode0, workernode0</span></span> |
| <span data-ttu-id="cd126-173">Hostgegevens niet ophalen.</span><span class="sxs-lookup"><span data-stu-id="cd126-173">Get host info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| <span data-ttu-id="cd126-174">Host-onderdelen downloaden</span><span class="sxs-lookup"><span data-stu-id="cd126-174">Get host components</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |<span data-ttu-id="cd126-175">namenode, resourcemanager</span><span class="sxs-lookup"><span data-stu-id="cd126-175">namenode, resourcemanager</span></span> |
| <span data-ttu-id="cd126-176">Host onderdeel gegevens opvragen.</span><span class="sxs-lookup"><span data-stu-id="cd126-176">Get host component info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |<span data-ttu-id="cd126-177">HostRoles, component, host, metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="cd126-177">HostRoles, component, host, metrics</span></span> |
| <span data-ttu-id="cd126-178">Configuraties ophalen</span><span class="sxs-lookup"><span data-stu-id="cd126-178">Get configurations</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |<span data-ttu-id="cd126-179">Typen config: core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="cd126-179">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |
| <span data-ttu-id="cd126-180">Configuratie-informatie ophalen.</span><span class="sxs-lookup"><span data-stu-id="cd126-180">Get configuration info.</span></span> |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |<span data-ttu-id="cd126-181">Typen config: core-site, hdfs-site, mapred-site, hive-site</span><span class="sxs-lookup"><span data-stu-id="cd126-181">Config types: core-site, hdfs-site, mapred-site, hive-site</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cd126-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cd126-182">Next Steps</span></span>
<span data-ttu-id="cd126-183">Nu u hebt geleerd hoe toouse Ambari bewaking van de API aanroept.</span><span class="sxs-lookup"><span data-stu-id="cd126-183">Now you have learned how toouse Ambari monitoring API calls.</span></span> <span data-ttu-id="cd126-184">toolearn meer, Zie:</span><span class="sxs-lookup"><span data-stu-id="cd126-184">toolearn more, see:</span></span>

* <span data-ttu-id="cd126-185">[HDInsight-clusters met hello Azure-portal beheren][hdinsight-admin-portal]</span><span class="sxs-lookup"><span data-stu-id="cd126-185">[Manage HDInsight clusters using hello Azure portal][hdinsight-admin-portal]</span></span>
* <span data-ttu-id="cd126-186">[HDInsight-clusters met Azure PowerShell beheren][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="cd126-186">[Manage HDInsight clusters using Azure PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="cd126-187">[HDInsight-clusters via opdrachtregelinterface beheren][hdinsight-admin-cli]</span><span class="sxs-lookup"><span data-stu-id="cd126-187">[Manage HDInsight clusters using command-line interface][hdinsight-admin-cli]</span></span>
* <span data-ttu-id="cd126-188">[HDInsight-documentatie][hdinsight-documentation]</span><span class="sxs-lookup"><span data-stu-id="cd126-188">[HDInsight documentation][hdinsight-documentation]</span></span>
* <span data-ttu-id="cd126-189">[Aan de slag met HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="cd126-189">[Get started with HDInsight][hdinsight-get-started]</span></span>

[ambari-home]: http://ambari.apache.org/
[ambari-api-reference]: https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md

[curl]: http://curl.haxx.se
[curl-download]: http://curl.haxx.se/download.html

[microsoft-hadoop-SDK]: http://hadoopsdk.codeplex.com/wikipage?title=Ambari%20Monitoring%20Client

[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-admin-cli]: hdinsight-administer-use-command-line.md
[hdinsight-documentation]: https://docs.microsoft.com/azure/hdinsight/
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[img-jobtracker-output]: ./media/hdinsight-monitor-use-ambari-api/hdi.ambari.monitor.jobtracker.output.png
