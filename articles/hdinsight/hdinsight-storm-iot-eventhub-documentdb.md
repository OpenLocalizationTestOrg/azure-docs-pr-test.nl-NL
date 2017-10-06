---
title: aaaProcess vehicle sensorgegevens met Apache Storm op HDInsight | Microsoft Docs
description: Meer informatie over hoe tooprocess vehicle sensorgegevens uit Event Hubs met Apache Storm op HDInsight. Modelgegevens toevoegen via Azure Cosmos DB en uitvoer toostorage op te slaan.
services: hdinsight,documentdb,notification-hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 78980635-8bef-4c33-96c3-fae50e932e31
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/03/2017
ms.author: larryfr
ms.openlocfilehash: 8f7b1dbb9072e095ea32160bb731bedd071288af
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="process-vehicle-sensor-data-from-azure-event-hubs-using-apache-storm-on-hdinsight"></a>Vehicle sensorgegevens uit Azure Event Hubs met Apache Storm op HDInsight verwerken

Meer informatie over hoe tooprocess vehicle sensorgegevens uit Azure Event Hubs met Apache Storm op HDInsight. In dit voorbeeld leest sensorgegevens uit Azure Event Hubs, verrijkt Hallo gegevens door te verwijzen naar gegevens die zijn opgeslagen in Azure Cosmos DB. Hallo-gegevens worden opgeslagen in Azure Storage met Hallo Hadoop File System (HDFS).

![HDInsight en Hallo-Architectuurdiagram van Internet der dingen (IoT)](./media/hdinsight-storm-iot-eventhub-documentdb/iot.png)

## <a name="overview"></a>Overzicht

Sensoren toovehicles toe te voegen, kunt u toopredict apparatuur problemen op basis van historische gegevens, trends. Ook kunt u toomake verbeteringen op basis van het patroon gebruiksanalyse toofuture-versies. Kunnen tooquickly moeten en efficiënt Hallo gegevens laden van alle voertuigen in Hadoop voordat MapReduce-verwerking kan plaatsvinden. U kunt bovendien toodo analyse voor kritieke fout paden (temperatuur motor, remmen, enzovoort) in realtime.

Azure Event Hubs is toohandle Hallo enorme hoeveelheid gegevens die worden gegenereerd door sensoren gebouwd. Apache Storm kan gebruikte tooload en proces Hallo gegevens zijn voordat deze tijdens het opslaan in HDFS.

## <a name="solution"></a>Oplossing

Telemetriegegevens voor engine temperatuur, temperatuur en vehicle snelheid wordt vastgelegd door sensoren. Gegevens worden vervolgens tooEvent Hubs samen met de Hallo auto Vehicle identificatie nummer (VIN) en een tijdstempel verzonden. Processen erdoor en slaat ze op in HDFS van daaruit een Storm-topologie uitgevoerd op een Apache Storm op HDInsight-cluster Hallo gegevens leest.

Tijdens de verwerking is Hallo VIN gebruikte tooretrieve modelgegevens van de Cosmos-database. Deze gegevens is toohello gegevensstroom toegevoegd voordat deze is opgeslagen.

Hallo-onderdelen die worden gebruikt in Hallo Storm-topologie zijn:

* **EventHubSpout** -leest de gegevens uit Azure Event Hubs
* **TypeConversionBolt** -converteert Hallo JSON-tekenreeks van Event Hubs in een tuple met Hallo sensorgegevens te volgen:
    * Engine temperatuur
    * Temperatuur
    * Snelheid
    * CHASSISNUMMER
    * tijdstempel
* **DataReferencBolt** -Hallo vehicle model van de Cosmos-database met behulp van Hallo VIN worden opgezocht
* **WasbStoreBolt** -stores Hallo gegevens tooHDFS (Azure-opslag)

Hallo volgende afbeelding ziet u een diagram van deze oplossing:

![storm-topologie](./media/hdinsight-storm-iot-eventhub-documentdb/iottopology.png)

## <a name="implementation"></a>Implementatie

Een complete geautomatiseerde oplossing voor dit scenario is beschikbaar als onderdeel van Hallo [HDInsight-Storm-voorbeelden](https://github.com/hdinsight/hdinsight-storm-examples) opslagplaats op GitHub. toouse in dit voorbeeld, volg de stappen Hallo in Hallo [IoTExample README. MD](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/IotExample/README.md).

## <a name="next-steps"></a>Volgende stappen

Zie voor meer voorbeeld Storm-topologieën [voorbeeldtopologieën van Storm op HDInsight](hdinsight-storm-example-topology.md).

