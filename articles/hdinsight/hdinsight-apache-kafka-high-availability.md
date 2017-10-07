---
title: beschikbaarheid van aaaHigh met Apache Kafka - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe tooensure hoge beschikbaarheid met Apache Kafka in Azure HDInsight. Meer informatie over hoe toorebalance replica's in Kafka partitie zodat ze zich op verschillende foutdomeinen binnen hello Azure-regio met HDInsight.
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
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 337468f36b531f83c2999e87907de89cf3d19dd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-your-data-with-apache-kafka-preview-on-hdinsight"></a>Hoge beschikbaarheid van uw gegevens met Apache Kafka (preview) in HDInsight

Meer informatie over hoe tooconfigure partitie replica's voor Kafka onderwerpen tootake profiteren van de onderliggende hardware configuratie van rack. Deze configuratie zorgt er Hallo beschikbaarheid van gegevens die zijn opgeslagen in de Apache-Kafka op HDInsight.

## <a name="fault-and-update-domains-with-kafka"></a>Probleem- en updatedomeinen met Kafka

Een foutdomein is een logische groepering van de onderliggende hardware in een Azure-datacenter. Elk foutdomein deelt een algemene voedingsbron en netwerkswitch. Hallo virtuele machines en beheerde schijven die Hallo knooppunten binnen een HDInsight-cluster implementeren zijn verdeeld over deze domeinen met fouten. Deze architectuur beperkt Hallo potentiële impact van problemen met de fysieke hardware.

Elke Azure-regio heeft een bepaald aantal foutdomeinen. Zie voor een lijst van domeinen en het aantal foutdomeinen ze bevatten Hallo Hallo [beschikbaarheidssets](../virtual-machines/linux/regions-and-availability.md#availability-sets) documentatie.

> [!IMPORTANT]
> Kafka is niet bekend met foutdomeinen. Wanneer u een onderwerp in Kafka maakt, kan deze alle replica's opslaan in Hallo hetzelfde foutdomein. toosolve dit probleem, bieden we Hallo [Kafka partitie deel opnieuw hulpprogramma](https://github.com/hdinsight/hdinsight-kafka-tools).

## <a name="when-toorebalance-partition-replicas"></a>Wanneer de replica's voor het partitioneren van toorebalance

tooensure hello hoogste beschikbaarheid van uw gegevens Kafka, u moet opnieuw verdelen Hallo partitie replica's voor uw onderwerp op Hallo volgende tijden:

* wanneer een nieuw onderwerp of partitie wordt gemaakt

* wanneer u een cluster opschaalt

## <a name="replication-factor"></a>Replicatiefactor

> [!IMPORTANT]
> Wij raden het gebruik aan van een Azure-regio die drie foutdomeinen bevat en van een replicatiefactor van 3.

Als u een regio met slechts twee domeinen met fouten gebruiken moet, gebruikt u een factor van de replicatie van 4 toospread Hallo-replica's gelijkmatig tussen de twee domeinen met fouten Hallo.

Zie voor een voorbeeld van het maken van onderwerpen en -instelling Hallo replicatie factor Hallo [beginnen met Kafka op HDInsight](hdinsight-apache-kafka-get-started.md) document.

## <a name="how-toorebalance-partition-replicas"></a>Hoe toorebalance partitie-replica 's

Gebruik Hallo [Kafka partitie deel opnieuw hulpprogramma](https://github.com/hdinsight/hdinsight-kafka-tools) toorebalance onderwerpen geselecteerd. Dit hulpprogramma moet vanaf een SSH-sessie toohello hoofdknooppunt van het cluster Kafka worden uitgevoerd.

Zie voor meer informatie over tooHDInsight via SSH verbinding te maken, de [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.

## <a name="next-steps"></a>Volgende stappen

* [Schaalbaarheid van Kafka in HDInsight](hdinsight-apache-kafka-scalability.md)
* [Spiegeling met Kafka in HDInsight](hdinsight-apache-kafka-mirroring.md)