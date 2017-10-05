---
title: Met behulp van PowerShell - Azure HDInsight Hadoop-clusters maken | Microsoft Docs
description: Informatie over het maken van Hadoop, HBase, Storm of Spark-clusters op Linux voor HDInsight met behulp van Azure PowerShell.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4208deca-d64a-45e1-8948-2673d5d7678c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: ca75974e6ec4f60739137d4cb5458bbfd735de3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a>Op basis van Linux-clusters maken in HDInsight met behulp van Azure PowerShell

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Azure PowerShell is een krachtige scriptomgeving op servers die u gebruiken kunt om te beheren en de implementatie en beheer van uw werkbelastingen in Microsoft Azure automatiseren. Dit document bevat informatie over het maken van een Linux gebaseerde HDInsight-cluster met behulp van Azure PowerShell. Dit omvat ook een voorbeeldscript.

> [!NOTE]
> Azure PowerShell is alleen beschikbaar op Windows-clients. Als u van een Linux-, Unix- of Mac OS X-client gebruikmaakt, Zie [maken van een Linux gebaseerde HDInsight-cluster met Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) voor informatie over het gebruik van de Azure CLI om een cluster te maken.

## <a name="prerequisites"></a>Vereisten
Hiervoor hebt u het volgende voordat u deze procedure begint:

* Een Azure-abonnement. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* [Azure PowerShell](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > Azure PowerShell-ondersteuning voor het beheer van HDInsight-resources met behulp van Azure Service Manager is **afgeschaft** en per 1 januari 2017 verdwenen. In de stappen in dit document worden de nieuwe HDInsight-cmdlets gebruikt die met Azure Resource Manager werken.
    >
    > Volg de stappen in [Azure PowerShell installeren](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) de meest recente versie van Azure PowerShell installeren. Als u scripts hebt die moeten worden gewijzigd om ze te kunnen gebruiken met de nieuwe cmdlets die werken met Azure Resource Manager, raadpleegt u [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) (Migreren naar op Azure Resource Manager gebaseerde hulpprogramma’s voor HDInsight-clusters) voor meer informatie.

## <a name="create-cluster"></a>Cluster maken

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Voor het maken van een HDInsight-cluster met behulp van Azure PowerShell, moet u de volgende procedures uitvoeren:

* Een Azure-resourcegroep maken
* Een Azure Storage-account maken
* Een Azure Blob-container maken
* Een HDInsight-cluster maken

Het volgende script laat zien hoe u een nieuw cluster maken:

[!code-powershell[belangrijkste](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]

De waarden die u voor de aanmelding van de cluster opgeeft worden gebruikt voor het maken van het Hadoop-gebruikersaccount voor het cluster. Dit account verbinding maken met services die worden gehost op het cluster, zoals web UI of REST-API's gebruiken.

De waarden die u voor de SSH-gebruiker opgeeft worden gebruikt voor het maken van de SSH-gebruiker voor het cluster. Dit account wordt gebruikt voor een externe SSH-sessie starten op het cluster en taken uitvoeren. Zie het document [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

> [!IMPORTANT]
> Als u meer dan 32 worker-knooppunten (op bij het maken van het cluster of wilt door het schalen van het cluster na aanmaak) gebruiken, moet u ook een hoofdknooppunt grootte opgeven met ten minste 8 kerngeheugens en 14 GB RAM-geheugen.
>
> Zie voor meer informatie over knooppuntgrootten en bijbehorende kosten [HDInsight prijzen](https://azure.microsoft.com/pricing/details/hdinsight/).

Er kunnen maximaal 20 minuten om een cluster te maken.

## <a name="create-cluster-configuration-object"></a>Cluster maken: Configuration-object

U kunt ook maken voor een HDInsight configuration-object met behulp `New-AzureRmHDInsightClusterConfig` cmdlet. U kunt dit configuratieobject zodat extra configuratieopties voor uw cluster wijzigen. Gebruik tot slot de `-Config` parameter van de `New-AzureRmHDInsightCluster` cmdlet de configuratie te gebruiken.

Het volgende script maakt een configuratieobject voor de configuratie van een R Server op type HDInsight-cluster. De configuratie maakt een edge-knooppunt, RStudio en een extra storage-account.

[!code-powershell[belangrijkste](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]

> [!WARNING]
> Met behulp van een opslagaccount in een andere locatie dan het HDInsight-cluster wordt niet ondersteund. Wanneer u in dit voorbeeld gebruikt, moet u de aanvullende storage-account maken in dezelfde locatie als de server.

## <a name="customize-clusters"></a>Clusters aanpassen

* Zie [aanpassen HDInsight-clusters met behulp van de Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).
* Zie [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="delete-the-cluster"></a>Het cluster verwijderen

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Problemen oplossen

Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) als u problemen ondervindt met het maken van HDInsight-clusters.

## <a name="next-steps"></a>Volgende stappen

Nu u een HDInsight-cluster hebt gemaakt, gebruiken de volgende bronnen voor meer informatie over het werken met uw cluster.

### <a name="hadoop-clusters"></a>Hadoop-clusters

* [Hive gebruiken met HDInsight](hdinsight-use-hive.md)
* [Pig gebruiken met HDInsight](hdinsight-use-pig.md)
* [MapReduce gebruiken met HDInsight](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>HBase-clusters

* [Aan de slag met HBase in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md)
* [Ontwikkelen van Java-toepassingen voor HBase in HDInsight](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Storm-clusters

* [Java-topologieën ontwikkelen voor Storm op HDInsight](hdinsight-storm-develop-java-topology.md)
* [Python-onderdelen in Storm op HDInsight gebruiken](hdinsight-storm-develop-python-topology.md)
* [Implementeren en bewaken topologieën met Storm op HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a>Spark-clusters

* [Een zelfstandige toepassing maken met behulp van Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy](hdinsight-apache-spark-livy-rest-interface.md)
* [Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools](hdinsight-apache-spark-use-bi-tools.md)
* [Spark met Machine Learning: Spark in HDInsight gebruiken om voedselinspectieresultaten te voorspellen](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen](hdinsight-apache-spark-eventhub-streaming.md)

