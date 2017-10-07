---
title: aaaApache Spark streamen met Kafka - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse Spark Apache Spark toostream gegevens van of naar Apache Kafka DStreams gebruiken. In dit voorbeeld kunt u gegevens met behulp van een Jupyter-notebook in Spark in HDInsight streamen.
keywords: Voorbeeld van kafka, zookeeper kafka, spark streaming kafka, spark-streaming kafka-voorbeeld
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: dd8f53c1-bdee-4921-b683-3be4c46c2039
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: f48b37aadafa4979cd27af68e8417db6acc8a0e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-dstream-example-with-kafka-preview-on-hdinsight"></a>Apache Spark-streaming (DStream) voorbeeld met Kafka (preview) op HDInsight

Meer informatie over hoe toouse Spark Apache Spark toostream gegevens van of naar Apache Kafka op HDInsight met behulp van DStreams. In dit voorbeeld wordt een Jupyter-notebook die wordt uitgevoerd op Hallo Spark-cluster.
> [!NOTE]
> Hallo stappen in dit document wordt een Azure-resourcegroep met zowel een Spark in HDInsight en een Kafka op HDInsight-cluster maken Deze clusters zijn beide zich binnen een virtueel netwerk van Azure, waardoor Hallo Spark-cluster toodirectly communiceren met de Hallo Kafka-cluster.
>
> Wanneer u klaar bent met de stappen in dit document Hallo onthouden toodelete Hallo clusters tooavoid overtollige kosten.

## <a name="create-hello-clusters"></a>Hallo-clusters maken

Apache Kafka op HDInsight biedt geen toegang tot toohello Kafka beleggingsmakelaars via openbaar internet Hallo. Alles wat vertelt tooKafka moet zich in hetzelfde virtuele Azure-netwerk als knooppunten in Hallo HALLO hallo Kafka-cluster. Bijvoorbeeld, bevinden zowel hello Kafka- en Spark-clusters zich in een Azure-netwerk. Hallo volgende diagram ziet u hoe de communicatie tussen clusters met Hallo loopt:

![Diagram van Spark en Kafka clusters in een Azure-netwerk](./media/hdinsight-apache-spark-with-kafka/spark-kafka-vnet.png)

> [!NOTE]
> Hoewel Kafka zelf beperkt toocommunication binnen het virtuele netwerk hello, Hallo andere services op Hallo cluster zoals SSH en Ambari toegankelijk is via internet. Zie voor meer informatie over Hallo openbare poorten beschikbaar met HDInsight [poorten en URI's die worden gebruikt door HDInsight](hdinsight-hadoop-port-settings-for-services.md).

U kunt een Azure-netwerk, Kafka en Spark clusters handmatig maken, is het eenvoudiger toouse een Azure Resource Manager-sjabloon. Gebruik Hallo volgende stappen uit voor een Azure-netwerk Kafka, toodeploy en Spark-clusters tooyour Azure-abonnement.

1. Hallo na de knop toosign in tooAzure en open Hallo-sjabloon in hello Azure-portal gebruiken.
    
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-spark-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-spark-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
    
    Hello Azure Resource Manager-sjabloon bevindt zich op **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-spark-cluster-in-vnet-v2.1.json**.

    > [!WARNING]
    > de beschikbaarheid van de tooguarantee van Kafka op HDInsight, uw cluster moet ten minste drie worker-knooppunten bevatten. Deze sjabloon maakt een Kafka-cluster dat drie worker-knooppunten bevat.

    Deze sjabloon maakt een 3.6 HDInsight-cluster voor Kafka- en Spark.

2. Gebruik Hallo informatie toopopulate Hallo vermeldingen op Hallo volgen **aangepaste implementatie** blade:
   
    ![Aangepaste HDInsight-implementatie](./media/hdinsight-apache-spark-with-kafka/parameters.png)
   
    * **Resourcegroep**: Maak een groep of een bestaande set selecteren. Deze groep bevat Hallo HDInsight-cluster.

    * **Locatie**: Selecteer een locatie geografisch sluiten tooyou.

    * **Clusternaam baseren**: deze waarde wordt gebruikt als basisnaam voor Hallo Spark en Kafka clusters Hallo. Bijvoorbeeld, voeren **hdi** maakt een Spark-cluster spark hdi__ met de naam en een Kafka-cluster met de naam **kafka hdi**.

    * **Aanmeldingsnaam van gebruiker cluster**: Hallo-beheerdersgebruikersnaam voor Hallo Spark en Kafka-clusters.

    * **Aanmeldingswachtwoord cluster**: Hallo beheerder gebruikerswachtwoord voor Hallo Spark en Kafka-clusters.

    * **SSH-gebruikersnaam**: Hallo SSH gebruiker toocreate voor Hallo Spark en Kafka-clusters.

    * **SSH-wachtwoord**: Hallo-wachtwoord voor Hallo SSH-gebruiker voor Hallo Spark en Kafka-clusters.

3. Lees Hallo **voorwaarden en bepalingen**, en selecteer vervolgens **ik ga akkoord toohello voorwaarden bovengenoemde**.

4. Controleer ten slotte **pincode toodashboard** en selecteer vervolgens **aankoop**. Het duurt ongeveer 20 minuten toocreate Hallo-clusters.

Zodra het Hallo-resources zijn gemaakt, bent u omgeleide tooa blade voor de resourcegroep Hallo Hallo clusters en webdashboard met.

![Resourcegroepblade voor Hallo vnet en clusters](./media/hdinsight-apache-spark-with-kafka/groupblade.png)

> [!IMPORTANT]
> Merk op dat de namen van HDInsight-clusters Hallo Hallo zijn **spark BASENAME** en **kafka BASENAME**, waarbij BASENAME Hallo-naam die u hebt opgegeven toohello sjabloon. U deze namen in latere stappen gebruiken om verbinding te maken van clusters toohello.

## <a name="use-hello-notebooks"></a>Hallo-notebooks gebruiken

Hallo code Hallo zoals beschreven in dit document is beschikbaar op [https://github.com/Azure-Samples/hdinsight-spark-scala-kafka](https://github.com/Azure-Samples/hdinsight-spark-scala-kafka).

Volg de stappen Hallo in Hallo `README.md` bestand toocomplete in dit voorbeeld.

## <a name="delete-hello-cluster"></a>Hallo-cluster verwijderen

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

Aangezien Hallo stappen in dit document beide maken clusters in dezelfde Azure-resourcegroep hello, kunt u de resourcegroep Hallo in hello Azure-portal verwijderen. Verwijderen Hallo groep verwijdert u alle resources die zijn gemaakt op basis van dit document, hello Azure Virtual Network en storage-account door Hallo clusters worden gebruikt.

## <a name="next-steps"></a>Volgende stappen

In dit voorbeeld hebt u geleerd hoe toouse tooread Spark en tooKafka schrijven. Hallo toodiscover koppelingen volgen andere manieren toowork met Kafka gebruiken:

* [Aan de slag met Apache Kafka in HDInsight](hdinsight-apache-kafka-get-started.md)
* [MirrorMaker toocreate een replica van Kafka op HDInsight gebruiken](hdinsight-apache-kafka-mirroring.md)
* [Apache Storm gebruiken met Kafka in HDInsight](hdinsight-apache-storm-with-kafka.md)

