---
title: aaaAn inleiding tooApache Kafka op HDInsight - Azure | Microsoft Docs
description: 'Meer informatie over de Apache-Kafka op HDInsight: Wat is, wat het doet en waar toofind voorbeelden en ophalen van informatie gestart.'
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: f284b6e3-5f3b-4a50-b455-917e77588069
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/15/2017
ms.author: larryfr
ms.openlocfilehash: 1bc198d4cf93a4682030d4fa5f71030f49ad64be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="introducing-apache-kafka-on-hdinsight-preview"></a>Inleiding tot Apache Kafka in HDInsight (preview)

[Apache Kafka](https://kafka.apache.org) is een open source gedistribueerde streaming-platform die gebruikt toobuild realtime worden kan streaming gegevenspijplijnen en toepassingen. Kafka biedt ook bericht broker functionaliteit vergelijkbaar tooa berichtenwachtrij, kunt u publiceren en abonneren toonamed gegevensstromen. Kafka op HDInsight biedt u een beheerde, maximaal beschikbare en zeer schaalbare service in Hallo Microsoft Azure-cloud.

## <a name="why-use-kafka-on-hdinsight"></a>Waarom Kafka op HDInsight gebruiken?

Kafka biedt Hallo volgende kenmerken:

* Messaging-patroon publiceren / abonneren: Kafka biedt een producent-API voor het publiceren van records tooa Kafka onderwerp. Hallo Consumer-API wordt gebruikt wanneer u zich abonneert tooa onderwerp.

* Streamverwerking: Kafka wordt vaak gebruikt met Apache Storm of Spark voor streamverwerking in realtime. Kafka 0.10.0.0 (HDInsight versie 3.5) geïntroduceerd om een streaming-API waarmee u toobuild oplossingen streaming zonder dat Storm of Spark.

* Horizontale schaal: Kafka partities streams op Hallo-knooppunten in Hallo HDInsight-cluster. Consumer-processen kunnen worden gekoppeld aan afzonderlijke partities tooprovide taakverdeling wanneer records worden verbruikt.

* Levering op volgorde: binnen elke partitie records worden opgeslagen in de stroom Hallo Hallo zodat ze werden ontvangen. Door één consumentenproces aan een partitie te koppelen, kunt u garanderen dat de records in de juiste volgorde worden verwerkt.

* Fouttolerantie: Kunnen partities worden gerepliceerd tussen knooppunten tooprovide fouttolerantie.

* Integratie met Azure beheerd schijven: beheerde schijven biedt hogere schaal en doorvoer voor Hallo-schijven die worden gebruikt door Hallo virtuele machines in Hallo HDInsight-cluster.

    Beheerde schijven zijn standaard ingeschakeld voor Kafka in HDInsight en Hallo aantal schijven gebruikt per knooppunt kan worden geconfigureerd tijdens het maken van HDInsight. Zie [Azure Managed Disks](../virtual-machines/windows/managed-disks-overview.md) voor meer informatie over beheerde schijven.

    Zie [Increase scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md) (Schaalbaarheid verhogen van Kafka in HDInsight) voor informatie over het configureren van beheerde schijven met Kafka in HDInsight.

## <a name="use-cases"></a>Gebruiksvoorbeelden

* **Messaging-**: aangezien het Hallo ondersteunt bericht patroon voor publiceren / abonneren, Kafka wordt vaak gebruikt als broker bericht.

* **Bijhouden van activiteiten**: aangezien Kafka logboekregistratie in volgorde van records, biedt het kan worden gebruikt tootrack en activiteiten opnieuw maken. Bijvoorbeeld gebruikersacties op een website of in een toepassing.

* **Aggregatie**: stream verwerking gebruikt, kunt u statistische gegevens uit verschillende stromen toocombine en Hallo-gegevens in de operationele gegevens centraliseren.

* **Transformatie**: met streamverwerking kunt u de gegevens uit meerdere invoeronderwerpen combineren en vertalen naar één of meer uitvoeronderwerpen.

## <a name="next-steps"></a>Volgende stappen

Gebruik Hallo volgende koppelingen toolearn hoe toouse Apache Kafka op HDInsight:

* [Aan de slag met Kafka in HDInsight](hdinsight-apache-kafka-get-started.md)

* [MirrorMaker toocreate een replica van Kafka op HDInsight gebruiken](hdinsight-apache-kafka-mirroring.md)

* [Apache Storm gebruiken met Kafka in HDInsight](hdinsight-apache-storm-with-kafka.md)

* [Apache Spark gebruiken met Kafka in HDInsight](hdinsight-apache-spark-with-kafka.md)

* [TooKafka verbinding via een virtueel Azure-netwerk](hdinsight-apache-kafka-connect-vpn-gateway.md)
