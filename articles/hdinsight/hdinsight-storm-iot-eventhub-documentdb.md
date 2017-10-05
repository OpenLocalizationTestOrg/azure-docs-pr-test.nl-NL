---
title: Verwerken van sensorgegevens vehicle met Apache Storm op HDInsight | Microsoft Docs
description: Informatie over het verwerken van sensorgegevens vehicle van Event Hubs met behulp van Apache Storm op HDInsight. Modelgegevens toevoegen via Azure Cosmos DB en uitvoer naar de opslag op te slaan.
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
ms.openlocfilehash: 8e8ebc724e1c70e8fcd56312adef5da2342373ea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="process-vehicle-sensor-data-from-azure-event-hubs-using-apache-storm-on-hdinsight"></a>Vehicle sensorgegevens uit Azure Event Hubs met Apache Storm op HDInsight verwerken

Informatie over het verwerken van sensorgegevens vehicle uit Azure Event Hubs met Apache Storm op HDInsight. In dit voorbeeld leest sensorgegevens uit Azure Event Hubs, verrijkt de gegevens door te verwijzen naar gegevens die zijn opgeslagen in Azure Cosmos DB. De gegevens worden opgeslagen in Azure Storage met Hadoop File System (HDFS).

![HDInsight en -Architectuurdiagram van het Internet der dingen (IoT)](./media/hdinsight-storm-iot-eventhub-documentdb/iot.png)

## <a name="overview"></a>Overzicht

Sensoren aan voertuigen toe te voegen, kunt u apparatuur problemen op basis van historische gegevens, trends te voorspellen. Ook kunt u verbeteringen in toekomstige versies op basis van gebruiksanalyse patroon. U moet kunnen snel en efficiënt laden van de gegevens van alle voertuigen in Hadoop voordat MapReduce-verwerking kan plaatsvinden. Mogelijk wilt u daarnaast analyses voor kritieke fout paden (temperatuur motor, remmen, enzovoort) in realtime.

Azure Event Hubs is gebouwd voor het afhandelen van de grote hoeveelheid gegevens die worden gegenereerd door sensoren. Apache Storm kan worden gebruikt om te laden en de gegevens verwerken voordat deze wordt opgeslagen in HDFS.

## <a name="solution"></a>Oplossing

Telemetriegegevens voor engine temperatuur, temperatuur en vehicle snelheid wordt vastgelegd door sensoren. Gegevens worden vervolgens verzonden naar Event Hubs samen met de auto Vehicle-id-nummer (VIN) en een tijdstempel. Processen erdoor en slaat ze op in HDFS van daaruit een Storm-topologie uitgevoerd op een Apache Storm op HDInsight-cluster leest de gegevens.

Tijdens de verwerking wordt het Chassisnummer gebruikt voor het ophalen van informatie over model van de Cosmos-database. Deze gegevens is toegevoegd aan de gegevensstroom voordat deze is opgeslagen.

De onderdelen die worden gebruikt in de Storm-topologie zijn:

* **EventHubSpout** -leest de gegevens uit Azure Event Hubs
* **TypeConversionBolt** -JSON-tekenreeks van Event Hubs converteert naar een tuple met de volgende sensorgegevens:
    * Engine temperatuur
    * Temperatuur
    * Snelheid
    * CHASSISNUMMER
    * tijdstempel
* **DataReferencBolt** -Hiermee zoekt u het model drager van de Cosmos-database met behulp van het Chassisnummer
* **WasbStoreBolt** -slaat de gegevens naar HDFS (Azure-opslag)

De volgende afbeelding ziet u een diagram van deze oplossing:

![storm-topologie](./media/hdinsight-storm-iot-eventhub-documentdb/iottopology.png)

## <a name="implementation"></a>Implementatie

Een complete geautomatiseerde oplossing voor dit scenario is beschikbaar als onderdeel van de [HDInsight-Storm-voorbeelden](https://github.com/hdinsight/hdinsight-storm-examples) opslagplaats op GitHub. Volg de stappen in dit voorbeeld kunt gebruiken, de [IoTExample README. MD](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/IotExample/README.md).

## <a name="next-steps"></a>Volgende stappen

Zie voor meer voorbeeld Storm-topologieën [voorbeeldtopologieën van Storm op HDInsight](hdinsight-storm-example-topology.md).

