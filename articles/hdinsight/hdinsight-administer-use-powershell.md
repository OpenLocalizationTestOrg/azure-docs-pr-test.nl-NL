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
# <a name="manage-hadoop-clusters-in-hdinsight-by-using-azure-powershell"></a>Hadoop-clusters in HDInsight met behulp van Azure PowerShell beheren
[!INCLUDE [selector](../../includes/hdinsight-portal-management-selector.md)]

Azure PowerShell is een krachtige scriptomgeving op servers die u gebruiken kunt om te beheren en de implementatie en beheer van uw workloads in Azure automatiseren. In dit artikel leert u hoe u in Azure HDInsight Hadoop-clusters beheren met behulp van een lokale Azure PowerShell-console door het gebruik van Windows PowerShell. Zie voor een overzicht van de HDInsight-PowerShell-cmdlets [HDInsight cmdlet-verwijzing][hdinsight-powershell-reference].

**Vereisten**

Voordat u dit artikel gaat lezen, moet u beschikken over het volgende:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

## <a name="install-azure-powershell"></a>Azure PowerShell installeren
[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

Als u Azure PowerShell versie 0,9 hebt geïnstalleerd x, moet u deze verwijderen voordat u een nieuwere versie installeert.

De versie van de geïnstalleerde PowerShell controleren:

    Get-Module *azure*

Voer voor het verwijderen van de oudere versie, programma's en onderdelen in het Configuratiescherm.

## <a name="create-clusters"></a>Clusters maken
Zie [maken Linux gebaseerde clusters in HDInsight met behulp van Azure PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md)

## <a name="list-clusters"></a>Lijst met clusters
Gebruik de volgende opdracht voor een lijst met alle clusters in het huidige abonnement:

    Get-AzureRmHDInsightCluster

## <a name="show-cluster"></a>Cluster weergeven
Gebruik de volgende opdracht om details van een specifiek cluster in het huidige abonnement weer te geven:

    Get-AzureRmHDInsightCluster -ClusterName <Cluster Name>

## <a name="delete-clusters"></a>Clusters verwijderen
Gebruik de volgende opdracht om te verwijderen van een cluster:

    Remove-AzureRmHDInsightCluster -ClusterName <Cluster Name>

U kunt ook een cluster verwijderen door het verwijderen van de resourcegroep waarin het cluster. Let op: Hiermee verwijdert u alle resources in de groep met inbegrip van het standaardopslagaccount.

    Remove-AzureRmResourceGroup -Name <Resource Group Name>

## <a name="scale-clusters"></a>Clusters schalen
Het schalen van de functie cluster kunt u het aantal worker-knooppunten gebruikt door een cluster dat wordt uitgevoerd in Azure HDInsight zonder te hoeven maken van het cluster opnieuw wijzigen.

> [!NOTE]
> Alleen clusters met HDInsight versie 3.1.3 of hoger worden ondersteund. Als u de versie van het cluster niet zeker weet, kunt u de pagina eigenschappen controleren.  Zie [lijst en geeft weer clusters](hdinsight-administer-use-portal-linux.md#list-and-show-clusters).
>
>

De gevolgen van het wijzigen van het aantal gegevensknooppunten voor elk type van ondersteund door de HDInsight-cluster:

* Hadoop

    U kunt naadloos Verhoog het aantal worker-knooppunten van een Hadoop-cluster dat wordt uitgevoerd zonder enige impact op alle taken die in behandeling of wordt uitgevoerd. Nieuwe taken kunnen ook worden verzonden terwijl de bewerking uitgevoerd wordt. Fouten in een bewerking voor schaal worden probleemloos verwerkt zodat het cluster altijd in een functionele staat blijft.

    Wanneer een Hadoop-cluster wordt verkleind door het aantal gegevensknooppunten te verminderen, zijn sommige van de services in het cluster opnieuw gestart. Dit zorgt ervoor dat alle actieve en in behandeling zijnde taken mislukken na het voltooien van de bewerking uit te schalen. U kunt echter de taken verzenden zodra de bewerking voltooid is.
* HBase

    U kunt naadloos toevoegen of verwijderen van knooppunten in uw HBase-cluster, terwijl deze wordt uitgevoerd. Regionale Servers worden automatisch verdeeld binnen een paar minuten na voltooiing van de bewerking uit te schalen. U kunt echter ook handmatig de regionale servers verdelen door aanmelden bij de headnode van cluster en het gebruik van de volgende opdrachten vanuit een opdrachtpromptvenster:

        >pushd %HBASE_HOME%\bin
        >hbase shell
        >balancer
* Storm

    U kunt naadloos toevoegen of verwijderen van gegevensknooppunten naar uw Storm-cluster, terwijl deze wordt uitgevoerd. Maar na een geslaagde voltooiing van de bewerking uit te schalen, moet u de topologie opnieuw verdelen.

    Herverdeling kan worden uitgevoerd op twee manieren:

  * Storm-webgebruikersinterface
  * Hulpprogramma voor opdrachtregelinterface (CLI)

    Raadpleeg de [Apache Storm documentatie](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html) voor meer informatie.

    De Storm-webgebruikersinterface is beschikbaar op het HDInsight-cluster:

    ![HDInsight storm scale deel opnieuw](./media/hdinsight-administer-use-management-portal/hdinsight.portal.scale.cluster.png)

    Hier volgt een voorbeeld van hoe u met de opdracht CLI opnieuw verdelen van de Storm-topologie:

        ## Reconfigure the topology "mytopology" to use 5 worker processes,
        ## the spout "blue-spout" to use 3 executors, and
        ## the bolt "yellow-bolt" to use 10 executors
        $ storm rebalance mytopology -n 5 -e blue-spout=3 -e yellow-bolt=10

Als u wilt de grootte van Hadoop-cluster wijzigen met behulp van Azure PowerShell, voer de volgende opdracht vanaf een clientcomputer:

    Set-AzureRmHDInsightClusterSize -ClusterName <Cluster Name> -TargetInstanceCount <NewSize>


## <a name="grantrevoke-access"></a>Toegang verlenen of in te trekken
HDInsight-clusters hebben de volgende HTTP-webservices (al deze services hebt RESTful eindpunten):

* ODBC
* JDBC
* Ambari
* Oozie
* Templeton

Standaard worden deze services verleend om toegang te krijgen. U kunt in te trekken/verlenen toegang. Voor het intrekken van:

    Revoke-AzureRmHDInsightHttpServicesAccess -ClusterName <Cluster Name>

Om toegang te verlenen:

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
> Door de toegang verlenen/intrekken, stelt u de cluster-gebruikersnaam en wachtwoord.
>
>

Dit kan ook worden gedaan via de Portal. Zie [HDInsight beheren met behulp van de Azure-portal][hdinsight-admin-portal].

## <a name="update-http-user-credentials"></a>HTTP-gebruikersreferenties updaten
Dit is dezelfde procedure als [Grant/revoke HTTP toegang](#grant/revoke-access). Als het cluster heeft de HTTP-toegang is verleend, moet u het eerst intrekken.  Vervolgens toegang verlenen en de met nieuwe HTTP gebruikersgegevens.

## <a name="find-the-default-storage-account"></a>Het standaardopslagaccount vinden
De volgende Powershell-script laat zien hoe de naam van het standaardopslagaccount en de standaard opslagaccountsleutel voor een cluster.

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup
    $defaultStorageAccountName = ($cluster.DefaultStorageAccount).Replace(".blob.core.windows.net", "")
    $defaultBlobContainerName = $cluster.DefaultStorageContainer
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey

## <a name="find-the-resource-group"></a>De resourcegroep niet vinden
In de modus Resource Manager behoort elk HDInsight-cluster tot een Azure-resourcegroep.  Zoek de resourcegroep:

    $clusterName = "<HDInsight Cluster Name>"

    $cluster = Get-AzureRmHDInsightCluster -ClusterName $clusterName
    $resourceGroupName = $cluster.ResourceGroup


## <a name="submit-jobs"></a>Verzenden van taken
**MapReduce-taken verzenden**

Zie [uitvoeren Hadoop-MapReduce-voorbeelden in HDInsight op basis van Windows](hdinsight-run-samples.md).

**Hive-taken verzenden**

Zie [uitvoeren Hive-query's met behulp van PowerShell](hdinsight-hadoop-use-hive-powershell.md).

**Pig-taken verzenden**

Zie [uitvoeren Pig-taken met behulp van PowerShell](hdinsight-hadoop-use-pig-powershell.md).

**Om Sqoop taken te verzenden**

Zie [Sqoop gebruiken met HDInsight](hdinsight-use-sqoop.md).

**Oozie-taken verzenden**

Zie [Oozie gebruiken met Hadoop om te definiëren en uitvoeren van een werkstroom in HDInsight](hdinsight-use-oozie.md).

## <a name="upload-data-to-azure-blob-storage"></a>Gegevens uploaden naar Azure Blob-opslag
Zie [Gegevens uploaden naar HDInsight][hdinsight-upload-data].

## <a name="see-also"></a>Zie ook
* [HDInsight-cmdlet-naslagdocumentatie][hdinsight-powershell-reference]
* [HDInsight beheren met behulp van de Azure-portal][hdinsight-admin-portal]
* [HDInsight met behulp van een opdrachtregelinterface beheren][hdinsight-admin-cli]
* [HDInsight-clusters maken][hdinsight-provision]
* [Gegevens uploaden naar HDInsight][hdinsight-upload-data]
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
