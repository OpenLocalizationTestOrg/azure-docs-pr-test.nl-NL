---
title: schaalt aaaApache Kafka - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe tooconfigure schijven voor Apache Kafka-cluster op Azure HDInsight tooincrease schaalbaarheid beheerd.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/14/2017
ms.author: larryfr
ms.openlocfilehash: b51114b33359f2c385f057a7a7a5b134cad27e51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-storage-and-scalability-for-apache-kafka-on-hdinsight"></a>Opslag en schaalbaarheid configureren voor Apache Kafka in HDInsight

Meer informatie over hoe tooconfigure Hallo aantal beheerde schijven gebruikt door Apache Kafka op HDInsight.

Kafka op HDInsight maakt gebruik van de lokale schijf Hallo Hallo virtuele machines Hallo HDInsight-cluster. Omdat Kafka zwaar, zeer i/o is [Azure beheerd schijven](../virtual-machines/windows/managed-disks-overview.md) gebruikte tooprovide hoge doorvoersnelheid is en bieden meer opslagruimte per knooppunt. Als traditionele virtuele harde schijven (VHD) zijn gebruikt voor Kafka, is in elk knooppunt beperkt too1 TB. Met beheerde schijven kunt u meerdere schijven tooachieve 16 TB voor elk knooppunt in het Hallo-cluster.

Hallo biedt volgende diagram een vergelijking tussen Kafka op HDInsight voordat de beheerde schijven en Kafka in HDInsight met beheerde schijven:

![Diagram waarin Kafka in HDInsight wordt weergegeven met één virtuele harde schijf per VM versus meerdere beheerde schijven per VM](./media/hdinsight-apache-kafka-scalability/kafka-with-managed-disks-architecture.png)

## <a name="configure-managed-disks-azure-portal"></a>Beheerde schijven configureren: Azure Portal

1. Volg de stappen Hallo in Hallo [maken van een HDInsight-cluster](hdinsight-hadoop-create-linux-clusters-portal.md) toounderstand Hallo algemene stappen toocreate een cluster met de Hallo-portal. Hallo maken van de portal proces niet worden voltooid.

2. Van Hallo __clustergrootte__ blade, gebruik Hallo __schijven per werkrolknooppunt__ veld tooconfigure Hallo aantal schijven.

    > [!NOTE]
    > Hallo type beheerde schijf kan zijn __standaard__ (HDD) of __Premium__ (SSD). Premium-schijven worden gebruikt met virtuele machines uit de DS- en GS-reeks. Alle andere VM-typen gebruiken standaardschijven.

    ![Afbeelding van Hallo cluster grootte blade met Hallo schijven per werkrolknooppunt gemarkeerd](./media/hdinsight-apache-kafka-scalability/set-managed-disks-portal.png)

## <a name="configure-managed-disks-resource-manager-template"></a>Beheerde schijven configureren: Resource Manager-sjabloon

toocontrol hello aantal schijven gebruikt door Hallo worker-knooppunten in een cluster Kafka, gebruik Hallo gedeelte van de sjabloon hello te volgen:

```json
"dataDisksGroups": [
    {
        "disksPerNode": "[variables('disksPerWorkerNode')]"
    }
    ],
```

U vindt een volledige sjabloon die u laat zien hoe tooconfigure schijven op beheerd [https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json](https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json).

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over het werken met Kafka op HDInsight Hallo documenten te volgen:

* [MirrorMaker toocreate een replica van Kafka op HDInsight gebruiken](hdinsight-apache-kafka-mirroring.md)
* [Apache Storm gebruiken met Kafka in HDInsight](hdinsight-apache-storm-with-kafka.md)
* [Apache Spark gebruiken met Kafka in HDInsight](hdinsight-apache-spark-with-kafka.md)
* [TooKafka verbinding via een virtueel Azure-netwerk](hdinsight-apache-kafka-connect-vpn-gateway.md)

* [HDInsight-blog over beheerde schijven met Kafka](https://azure.microsoft.com/blog/announcing-public-preview-of-apache-kafka-on-hdinsight-with-azure-managed-disks/)