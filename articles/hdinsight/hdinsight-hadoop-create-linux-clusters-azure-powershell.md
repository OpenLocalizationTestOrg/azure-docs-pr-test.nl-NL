---
title: aaaCreate Hadoop-clusters met behulp van PowerShell - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toocreate Hadoop, HBase, Storm of Spark-clusters op Linux voor HDInsight met behulp van Azure PowerShell.
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
ms.openlocfilehash: 53afe4702f6b61a0720ceda48a4a34d7fa8797d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a>Op basis van Linux-clusters maken in HDInsight met behulp van Azure PowerShell

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Azure PowerShell is een krachtige scriptomgeving toocontrol gebruiken en automatiseren Hallo-implementatie en beheer van uw werkbelastingen in Microsoft Azure. Dit document bevat informatie over hoe toocreate een op Linux gebaseerde HDInsight-cluster met behulp van Azure PowerShell. Dit omvat ook een voorbeeldscript.

> [!NOTE]
> Azure PowerShell is alleen beschikbaar op Windows-clients. Als u van een Linux-, Unix- of Mac OS X-client gebruikmaakt, Zie [maken van een Linux gebaseerde HDInsight-cluster met Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) voor informatie over het gebruik van hello Azure CLI toocreate een cluster.

## <a name="prerequisites"></a>Vereisten
Hallo volgende voordat u deze procedure begint, moet u hebben:

* Een Azure-abonnement. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* [Azure PowerShell](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > Azure PowerShell-ondersteuning voor het beheer van HDInsight-resources met behulp van Azure Service Manager is **afgeschaft** en per 1 januari 2017 verdwenen. Hallo stappen in dit document gebruiken Hallo nieuwe HDInsight-cmdlets die met Azure Resource Manager werken.
    >
    > Volg de stappen Hallo in [Azure PowerShell installeren](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall Hallo meest recente versie van Azure PowerShell. Als u scripts hebt die moeten toobe toouse Hallo nieuwe cmdlets die met Azure Resource Manager werken gewijzigd, Zie [migreren tooAzure ontwikkeling Resource Manager gebaseerde hulpprogramma's voor HDInsight-clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) voor meer informatie.

## <a name="create-cluster"></a>Cluster maken

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

toocreate een HDInsight-cluster met behulp van Azure PowerShell, moet u Hallo procedures te volgen:

* Een Azure-resourcegroep maken
* Een Azure Storage-account maken
* Een Azure Blob-container maken
* Een HDInsight-cluster maken

Hallo volgende script laat zien hoe een nieuw cluster toocreate:

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]

Hallo-waarden die u voor Hallo cluster aanmelding opgeeft zijn gebruikte toocreate hello Hadoop-gebruikersaccount voor Hallo-cluster. Gebruik dit account tooconnect tooservices gehost op Hallo cluster zoals web-UI of REST-API's.

Hallo-waarden die u opgeeft voor de SSH-gebruiker Hallo zijn gebruikte toocreate Hallo SSH-gebruiker voor Hallo cluster. Gebruik dit account toostart een externe SSH-sessie op Hallo-cluster en taken uitvoeren. Zie voor meer informatie, Hallo [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.

> [!IMPORTANT]
> Als u van plan bent toouse meer dan 32 worker-knooppunten (bij het maken van een cluster maken of door vergroten/verkleinen Hallo cluster na aanmaak), moet u ook een hoofdknooppunt grootte opgeven met ten minste 8 kerngeheugens en 14 GB RAM-geheugen.
>
> Zie voor meer informatie over knooppuntgrootten en bijbehorende kosten [HDInsight prijzen](https://azure.microsoft.com/pricing/details/hdinsight/).

Kan duren too20 minuten toocreate een cluster.

## <a name="create-cluster-configuration-object"></a>Cluster maken: Configuration-object

U kunt ook maken voor een HDInsight configuration-object met behulp `New-AzureRmHDInsightClusterConfig` cmdlet. U kunt deze configuratie object tooenable extra configuratieopties voor uw cluster wijzigen. Gebruik tot slot Hallo `-Config` parameter Hallo `New-AzureRmHDInsightCluster` cmdlet toouse Hallo configuratie.

Hallo volgende script maakt een object configuratie tooconfigure een R Server voor het type van HDInsight-cluster. Hallo-configuratie kan een edge-knooppunt, RStudio en een extra storage-account.

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]

> [!WARNING]
> Met behulp van een opslagaccount in een andere locatie dan Hallo HDInsight-cluster wordt niet ondersteund. Wanneer u in dit voorbeeld, Hallo aanvullende storage-account maken in Hallo dezelfde locatie als het Hallo-server.

## <a name="customize-clusters"></a>Clusters aanpassen

* Zie [aanpassen HDInsight-clusters met behulp van de Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).
* Zie [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="delete-hello-cluster"></a>Hallo-cluster verwijderen

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Problemen oplossen

Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) als u problemen ondervindt met het maken van HDInsight-clusters.

## <a name="next-steps"></a>Volgende stappen

Nu u een HDInsight-cluster hebt gemaakt, gebruiken Hallo hoe resources toolearn na toowork met uw cluster.

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
* [Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen](hdinsight-apache-spark-eventhub-streaming.md)

