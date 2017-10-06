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
# <a name="monitor-hadoop-clusters-in-hdinsight-using-hello-ambari-api"></a>Monitor voor Hadoop-clusters in HDInsight met behulp van Hallo Ambari-API
Meer informatie over hoe toomonitor HDInsight-clusters met behulp van Ambari APIs.

> [!NOTE]
> Hallo-informatie in dit artikel is hoofdzakelijk voor HDInsight op basis van Windows-clusters, die geen alleen-lezen-versie van Hallo Ambari REST-API. Zie voor Linux gebaseerde clusters [beheren Hadoop-clusters met Ambari](hdinsight-hadoop-manage-ambari.md).
> 
> 

## <a name="what-is-ambari"></a>Wat is Ambari?
[Apache Ambari] [ ambari-home] wordt gebruikt voor het inrichten, beheren en controleren van Apache Hadoop-clusters. Bevat een intuïtieve verzameling hulpprogramma's voor operators en een krachtige reeks API's die verbergen Hallo complexiteit van Hadoop Hallo werking van clusters vereenvoudigen. Zie voor meer informatie over Hallo API's, [Ambari-API-referentiemateriaal][ambari-api-reference]. 

HDInsight ondersteunt momenteel alleen Hallo Ambari bewakingsfunctie. Ambari-API 1.0 wordt ondersteund door clusters van HDInsight versie 3.0 en 2.1. In dit artikel bevat informatie over toegang tot Ambari APIs HDInsight versie 3.1 of 2.1-clusters. Hallo belangrijkste verschil tussen Hallo twee is dat sommige onderdelen Hallo Hallo introductie van nieuwe mogelijkheden (zoals Hallo taakserver geschiedenis) zijn gewijzigd. 

**Vereisten**

Voordat u deze zelfstudie begint, moet u de volgende items Hallo hebben:

* **Een werkstation met Azure PowerShell**.
* (Optioneel) [cURL][curl]. tooinstall, Zie [cURL Releases en Downloads][curl-download].
  
  > [!NOTE]
  > Wanneer Hallo cURL-opdracht in Windows, gebruik dubbele aanhalingstekens in plaats van enkele aanhalingstekens voor optiewaarden hello gebruiken.
  > 
  > 
* **Een Azure HDInsight-cluster**. Zie voor instructies over het cluster inrichten [aan de slag met HDInsight] [ hdinsight-get-started] of [HDInsight-clusters inrichten][hdinsight-provision]. U moet Hallo gegevens toogo Hallo-zelfstudie te volgen:
  
  | Cluster-eigenschap | Azure PowerShell de naam van variabele | Waarde | Beschrijving |
  | --- | --- | --- | --- |
  |   De naam van de HDInsight-cluster |$clusterName | |Hallo-naam van uw HDInsight-cluster. |
  |   Cluster-gebruikersnaam |$clusterUsername | |Clusternaam van de gebruiker opgegeven waarop het Hallo-cluster is gemaakt. |
  |   Het wachtwoord van cluster |$clusterPassword | |Wachtwoord van de gebruiker cluster. |

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]


## <a name="jump-start"></a>Snel
Er zijn verschillende manieren toouse Ambari toomonitor HDInsight-clusters.

**Azure PowerShell gebruiken**

Hello Azure PowerShell-script volgen opgehaald Hallo MapReduce-tracering taakinformatie *in een 3.5 HDInsight-cluster.*  Hallo belangrijkste verschil is dat we deze details van Hallo YARN-service (in plaats van MapReduce) ophalen.

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName/services/YARN/components/RESOURCEMANAGER"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'yarn.queueMetrics'

Hallo volgende PowerShell-script opgehaald Hallo MapReduce-tracering taakinformatie *in een cluster HDInsight 2.1*:

    $clusterName = "<HDInsightClusterName>"
    $clusterUsername = "<HDInsightClusterUsername>"
    $clusterPassword = "<HDInsightClusterPassword>"

    $ambariUri = "https://$clusterName.azurehdinsight.net:443/ambari"
    $uriJobTracker = "$ambariUri/api/v1/clusters/$clusterName.azurehdinsight.net/services/mapreduce/components/jobtracker"

    $passwd = ConvertTo-SecureString $clusterPassword -AsPlainText -Force
    $creds = New-Object System.Management.Automation.PSCredential ($clusterUsername, $passwd)

    $response = Invoke-RestMethod -Method Get -Uri $uriJobTracker -Credential $creds -OutVariable $OozieServerStatus

    $response.metrics.'mapred.JobTracker'

Hallo-uitvoer is:

![Jobtracker uitvoer][img-jobtracker-output]

**cURL gebruiken**

Hallo volgende voorbeeld wordt clustergegevens via cURL:

    curl -u <username>:<password> -k https://<ClusterName>.azurehdinsight.net:443/ambari/api/v1/clusters/<ClusterName>.azurehdinsight.net

Hallo-uitvoer is:

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

**Hallo-8-10-2014-release**:

Wanneer met behulp van Hallo Ambari eindpunt, 'https://{clusterDns}.azurehdinsight.net/ambari/api/v1/clusters/{clusterDns}.azurehdinsight.net/services/{servicename}/components/{componentname}' hello *hostnaam* veld Hallo volledig gekwalificeerde domeinnaam (FQDN) van Hallo-knooppunt in plaats van de hostnaam Hallo retourneert. Vóór Hallo 8-10-2014-release, in dit voorbeeld gewoon geretourneerd '**headnode0**'. Na Hallo 8-10-2014-release, krijgt u Hallo FQDN-naam '**headnode0. { ClusterDNS} azurehdinsight.NET .net**', zoals wordt weergegeven in het vorige voorbeeld Hallo. Deze wijziging is vereist toofacilitate scenario's waarbij meerdere clustertypen (zoals HBase en Hadoop) kunnen worden geïmplementeerd in een virtueel netwerk (VNET). Dit gebeurt, bijvoorbeeld: bij gebruik van HBase als een back-end-platform voor Hadoop.

## <a name="ambari-monitoring-apis"></a>Ambari-API's bewaken
Hallo volgende tabel bevat enkele Hallo meest voorkomende Ambari bewaking API-aanroepen. Zie voor meer informatie over Hallo API [Ambari-API-referentiemateriaal][ambari-api-reference].

| Monitor voor API-aanroep | URI | Beschrijving |
| --- | --- | --- |
| Ophalen van clusters |`/api/v1/clusters` | |
| Cluster-gegevens opvragen. |`/api/v1/clusters/<ClusterName>.azurehdinsight.net` |clusters, services, hosts |
| Ophalen van services |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services` |Services bevatten: hdfs, mapreduce |
| Services-gegevens opvragen. |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>` | |
| Serviceonderdelen downloaden |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components` |HDFS: namenode, datanodeMapReduce: jobtracker; tasktracker |
| Onderdeel gegevens opvragen. |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/services/<ServiceName>/components/<ComponentName>` |ServiceComponentInfo, host-onderdelen, metrische gegevens |
| Hosts ophalen |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts` |headnode0, workernode0 |
| Hostgegevens niet ophalen. |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>` | |
| Host-onderdelen downloaden |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components` |namenode, resourcemanager |
| Host onderdeel gegevens opvragen. |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/hosts/<HostName>/host_components/<ComponentName>` |HostRoles, component, host, metrische gegevens |
| Configuraties ophalen |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations` |Typen config: core-site, hdfs-site, mapred-site, hive-site |
| Configuratie-informatie ophalen. |`/api/v1/clusters/<ClusterName>.azurehdinsight.net/configurations?type=<ConfigType>&tag=<VersionName>` |Typen config: core-site, hdfs-site, mapred-site, hive-site |

## <a name="next-steps"></a>Volgende stappen
Nu u hebt geleerd hoe toouse Ambari bewaking van de API aanroept. toolearn meer, Zie:

* [HDInsight-clusters met hello Azure-portal beheren][hdinsight-admin-portal]
* [HDInsight-clusters met Azure PowerShell beheren][hdinsight-admin-powershell]
* [HDInsight-clusters via opdrachtregelinterface beheren][hdinsight-admin-cli]
* [HDInsight-documentatie][hdinsight-documentation]
* [Aan de slag met HDInsight][hdinsight-get-started]

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
