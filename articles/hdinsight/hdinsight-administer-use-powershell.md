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
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a>Hadoop-clusters in HDInsight met behulp van Azure PowerShell beheren
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Azure PowerShell is een krachtige scriptomgeving toocontrol gebruiken en automatiseren Hallo-implementatie en beheer van uw workloads in Azure. In dit artikel leert u hoe toomanage Hadoop-clusters in Azure HDInsight met behulp van een lokale Azure PowerShell-console via Hallo van Windows PowerShell gebruiken. Zie voor lijst Hallo Hallo HDInsight PowerShell-cmdlets [HDInsight cmdlet-verwijzing][hdinsight-powershell-reference].

**Vereisten**

Voordat u dit artikel, moet u de volgende Hallo hebben:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="install-azure-powershell"></a>Azure PowerShell installeren
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

Als u Azure PowerShell versie 0,9 hebt geïnstalleerd x, moet u deze verwijderen voordat u een nieuwere versie installeert.

toocheck versie Hallo Hallo PowerShell:

    Get-Module *azure*

toouninstall hello oudere versie, programma's en onderdelen in Configuratiescherm Hallo uitgevoerd.

## <a name="create-clusters"></a>Clusters maken
Zie [maken Linux gebaseerde clusters in HDInsight met behulp van Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)

## <a name="list-clusters"></a>Lijst met clusters
Hallo opdracht toolist na alle clusters in het huidige abonnement hello gebruiken:

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a>Cluster weergeven
Gebruik onderstaande opdracht tooshow gegevens van een specifieke cluster in het huidige abonnement Hallo Hallo:

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a>Clusters verwijderen
Gebruik Hallo opdracht toodelete een cluster te volgen:

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

U kunt ook een cluster verwijderen door het verwijderen van resourcegroep Hallo die Hallo cluster bevat. Let op: Hiermee verwijdert u alle Hallo bronnen in Hallo-groep met inbegrip van Hallo storage-standaardaccount.

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a>Clusters schalen
Hallo-cluster schalen van functie kunt u toochange Hallo aantal worker-knooppunten gebruikt door een cluster dat wordt uitgevoerd in Azure HDInsight zonder toore-Hallo cluster maken.

> [!NOTE]
> Alleen clusters met HDInsight versie 3.1.3 of hoger worden ondersteund. Als u niet zeker Hallo versie van het cluster weet, kunt u de eigenschappenpagina Hallo controleren.  Zie [lijst en geeft weer clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).
>
>

Hallo gevolgen van het aantal gegevensknooppunten voor elk type ondersteund door HDInsight cluster Hallo wijzigen:

* Hadoop

    Hallo aantal worker-knooppunten van een Hadoop-cluster dat wordt uitgevoerd zonder enige impact op alle taken die in behandeling of wordt uitgevoerd, kunt u naadloos verhogen. Nieuwe taken kunnen ook worden verzonden tijdens het Hallo-bewerking wordt uitgevoerd. Fouten in een bewerking voor schaal worden probleemloos verwerkt zodat hello cluster altijd functioneel is overblijft.

    Wanneer een Hadoop-cluster wordt verkleind door het aantal gegevensknooppunten hello te verminderen, worden sommige services in de cluster Hallo Hallo opnieuw gestart. Dit zorgt ervoor dat alle actieve en in behandeling zijnde taken toofail op Hallo Hallo schalen van de bewerking is voltooid. U kunt echter Hallo taken verzenden zodra Hallo-bewerking voltooid is.
* HBase

    U kunt naadloos toevoegen of verwijderen van knooppunten tooyour HBase-cluster, terwijl deze wordt uitgevoerd. Regionale Servers worden automatisch verdeeld binnen een paar minuten na voltooiing van Hallo bewerking schalen. U kunt echter ook handmatig Hallo regionale servers verdelen door logboekregistratie in toohello headnode van het cluster en actieve Hallo volgende opdrachten uit een opdrachtpromptvenster:

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* Storm

    U kunt naadloos toevoegen of verwijderen van gegevens knooppunten tooyour Storm-cluster, terwijl deze wordt uitgevoerd. Maar nadat de bewerking schalen Hallo installatie is voltooid, moet u toorebalance Hallo topologie.

    Herverdeling kan worden uitgevoerd op twee manieren:

  * Storm-webgebruikersinterface
  * Hulpprogramma voor opdrachtregelinterface (CLI)

    Raadpleeg toohello [Apache Storm documentatie](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) voor meer informatie.

    Hallo Storm-webgebruikersinterface is beschikbaar op Hallo HDInsight-cluster:

    ![HDInsight storm scale deel opnieuw](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    Hier volgt een voorbeeld hoe toouse Hallo CLI toorebalance Hallo Storm-topologie opdracht:

        ## Reconfigure hello topology "mytopology" toouse 5 worker processes,
        ## hello spout "blue-spout" toouse 3 executors, and
        ## hello bolt "yellow-bolt" toouse 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

toochange hello Hadoop-clusters met behulp van Azure PowerShell, uitvoeren van de volgende opdracht vanaf een clientcomputer Hallo:

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a>Toegang verlenen of in te trekken
HDInsight-clusters hebben Hallo HTTP-webservices (al deze services hebt RESTful eindpunten) te volgen:

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Standaard worden deze services verleend om toegang te krijgen. U kunt in te trekken/grant Hallo toegang. toorevoke:

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

toogrant:

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
> Door het Hallo toegang verlenen/intrekken, wordt u opnieuw ingesteld Hallo cluster-gebruikersnaam en wachtwoord.
>
>

Dit kan ook worden gedaan via Hallo Portal. Zie [HDInsight beheren met behulp van Azure-portal Hallo][hdinsight-admin-portal].

## <a name="update-http-user-credentials"></a>HTTP-gebruikersreferenties updaten
Is Hallo dezelfde procedure als [Grant/revoke HTTP toegang](#grant/revoke-access). Als het cluster Hallo Hallo HTTP-toegang is verleend, moet u het eerst intrekken.  Vervolgens toegang verlenen en Hallo met nieuwe HTTP gebruikersgegevens.

## <a name="find-hello-default-storage-account"></a>Hallo standaardopslagaccount vinden
Hallo volgende Powershell-script laat zien hoe tooget Hallo naam van het standaardopslagaccount en Hallo standaard opslagaccountsleutel voor een cluster.

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-hello-resource-group"></a>Hallo resourcegroep vinden
In de modus Resource Manager hello hoort elk HDInsight-cluster tooan Azure-resourcegroep.  toofind hello resourcegroep:

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a>Verzenden van taken
**toosubmit MapReduce-taken**

Zie [uitvoeren Hadoop-MapReduce-voorbeelden in HDInsight op basis van Windows](hdinsight-run-samples.md).

**toosubmit Hive-taken**

Zie [uitvoeren Hive-query's met behulp van PowerShell](hdinsight-hadoop-use-hive-powershell.md).

**toosubmit Pig-taken**

Zie [uitvoeren Pig-taken met behulp van PowerShell](hdinsight-hadoop-use-pig-powershell.md).

**toosubmit Sqoop taken**

Zie [Sqoop gebruiken met HDInsight](hdinsight-use-sqoop.md).

**toosubmit Oozie taken**

Zie [Oozie gebruiken met Hadoop toodefine en voer een werkstroom in HDInsight](hdinsight-use-oozie.md).

## <a name="upload-data-tooazure-blob-storage"></a>Uploaden van gegevens tooAzure Blob-opslag
Zie [uploaden van gegevens tooHDInsight][hdinsight-upload-data].

## <a name="see-also"></a>Zie ook
* [HDInsight-cmdlet-naslagdocumentatie][hdinsight-powershell-reference]
* [HDInsight beheren met behulp van hello Azure-portal][hdinsight-admin-portal]
* [HDInsight met behulp van een opdrachtregelinterface beheren][hdinsight-admin-cli]
* [HDInsight-clusters maken][hdinsight-provision]
* [Uploaden van gegevens tooHDInsight][hdinsight-upload-data]
* [Hadoop-taken programmatisch verzenden][hdinsight-submit-jobs]
* [Aan de slag met Azure HDInsight][hdinsight-get-started]

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
