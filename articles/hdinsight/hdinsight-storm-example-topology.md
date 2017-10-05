---
title: "Voorbeeld van Apache Storm-topologieën op HDInsight | Microsoft Docs"
description: "Een lijst met Storm-voorbeeldtopologieën gemaakt en getest met Apache Storm op HDInsight, met inbegrip van eenvoudige C# en Java-topologieën en werken met Event Hubs."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f9b1bdff-5928-4705-a76d-52fd200917cb
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.openlocfilehash: 71482e24e519319d506d61e0582420e35f1cae70
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="example-storm-topologies-and-components-for-apache-storm-on-hdinsight"></a>Voorbeeld van de Storm-topologieën en onderdelen voor Apache Storm op HDInsight

Hier volgt een lijst met voorbeelden gemaakt en beheerd door Microsoft voor gebruik met Apache Storm op HDInsight. Deze voorbeelden hebben betrekking op diverse onderwerpen uit het maken van eenvoudige C# en Java-topologieën te werken met Azure-services zoals Event Hubs, Cosmos DB, Power BI, SQL-Database, HBase op HDInsight en Azure Storage. Sommige voorbeelden ook het werken met niet-Azure of zelfs niet-Microsoft-technologieën, zoals SignalR en Socket.IO.

| Beschrijving | Demonstreert | Taal/Framework |
|:--- |:--- |:--- |
| [Schrijven naar Azure Data Lake Store van Apache Storm](hdinsight-storm-write-data-lake-store.md) |Schrijven naar het Azure Data Lake Store |Java |
| [Event Hub Spout en Bolt bron](https://github.com/apache/storm/tree/master/external/storm-eventhubs) |Bron voor de Event Hub Spout en Bolt |Java |
| [Java gebaseerde topologieën ontwikkelen voor Apache Storm op HDInsight][5797064f] |Maven |Java |
| [C#-topologieën ontwikkelen voor Apache Storm op HDInsight met behulp van Visual Studio][16fce2d1] |HDInsight-hulpprogramma's voor Visual Studio |C#, Java |
| [Maken van meerdere gegevensstromen in een C# Storm-topologie][ec5a4064] |Meerdere streams |C# |
| [Procesgebeurtenissen van Azure Event Hubs met Storm op HDInsight (C#)][844d1d81] |Event Hubs |C# en Java |
| [Procesgebeurtenissen van Azure Event Hubs met Storm op HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md) |Event Hubs |Java |
| [Power Bi gebruiken om gegevens van een Storm-topologie te visualiseren][94d15238] |Power BI |C# |
| [Analyseren van sensorgegevens met Storm en HBase in HDInsight][ab894747] |Event Hubs, HBase, Socket.IO, Web-dashboard |C#, Java, JavaScript, HTML |
| [Verwerken van sensorgegevens vehicle van Event Hubs met behulp van Storm op HDInsight][246ee964] |Event Hubs, Cosmos-DB, Azure Storage-Blob (WASB) |C#, Java |
| [Uitpakken, transformeren en Load (ETL) uit Azure Event Hubs HBase, Storm op HDInsight gebruiken][b4b68194] |Event Hubs, HBase |C# |
| [C# Storm-topologie sjabloonproject voor het werken met Azure-services van Storm op HDInsight][ce0c02a2] |Event Hubs, Cosmos-DB, SQL Database, HBase, SignalR |C#, Java |
| [Schaalbaarheid benchmarks voor het lezen van Azure Event Hubs met behulp van Storm op HDInsight][d6c540e3] |Bericht doorvoer, Event Hubs, SQL-Database |C#, Java |
| [Gebeurtenissen met Storm en HBase op HDInsight correleren](hdinsight-storm-correlation-topology.md) |HBase |C# |
| [Python met Storm op HDInsight gebruiken](hdinsight-storm-develop-python-topology.md) |Python-onderdelen met een lichtstroom-topologie |Python |
| [Gebruik Kafka met Storm op HDInsight](hdinsight-apache-storm-with-kafka.md) | Apache Storm lezen en schrijven van Apache Kafka | Java |

### <a name="next-steps"></a>Volgende stappen

* [Aan de slag met Apache Storm in HDInsight][2b8c3488]
* [Meer informatie over het implementeren en beheren van Storm-topologieën met Storm op HDInsight][6eb0d3b8]

[2b8c3488]: hdinsight-apache-storm-tutorial-get-started-linux.md "Informatie over het maken van een Storm op HDInsight-cluster en het Storm-Dashboard gebruiken voor het implementeren van voorbeeldtopologieën."
[6eb0d3b8]: hdinsight-storm-deploy-monitor-topology.md "Informatie over het implementeren en beheren van topologieën met het web gebaseerde Storm-Dashboard en Storm-gebruikersinterface of de HDInsight Tools voor Visual Studio."
[16fce2d1]: hdinsight-storm-develop-csharp-visual-studio-topology.md "Informatie over het maken van C# Storm-topologieën met behulp van de HDInsight Tools voor Visual Studio."
[5797064f]: hdinsight-storm-develop-java-topology.md "Informatie over het maken van Storm-topologieën in Java, met behulp van Maven, door het maken van een eenvoudige wordcount-topologie."
[94d15238]: hdinsight-storm-power-bi-topology.md "Demonstreert hoe u gegevens schrijven naar Power BI uit een C#-topologie en vervolgens een grafiek en een dashboard maken van de gegevens."
[ec5a4064]: https://github.com/Blackmist/csharp-storm-example "Demonstreert een eenvoudige Storm-topologie die een wordcount, geïmplementeerd in C# uitvoert. Dit toont ook aan het maken van meerdere gegevensstromen binnen een C#-topologie."
[844d1d81]: hdinsight-storm-develop-csharp-event-hub-topology.md "Informatie over het lezen en schrijven van gegevens uit Azure Event Hubs met Storm op HDInsight."
[ab894747]: hdinsight-storm-sensor-data-analysis.md "Informatie over het gebruik van Apache Storm op HDInsight voor het verwerken van sensorgegevens uit Azure Event Hubs met behulp van D3.js visualiseren en (optioneel) op te slaan voor HBase."
[246ee964]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/IotExample/README.md "Informatie over het gebruik van een Storm-topologie om berichten te lezen uit Azure Event Hubs gelezen documenten Azure Cosmos DB voor gegevens die verwijzen naar en opslaan van gegevens naar Azure Storage."
[d6c540e3]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/EventCountExample "Verschillende topologieën voor het demonstreren van doorvoer wanneer lezen uit Azure Event Hubs en opslaan met SQL Database met Apache Storm op HDInsight."
[b4b68194]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample "Informatie over het lezen van gegevens uit Azure Event Hubs, cumulatieve & de gegevens transformeren en sla deze op in HBase in HDInsight."
[ce0c02a2]: https://github.com/hdinsight/hdinsight-storm-examples/tree/master/templates/HDInsightStormExamples "Dit project bevat sjablonen voor spouts, bolts en topologieën kunnen communiceren met verschillende Azure-services zoals Event Hubs, Cosmos-database en SQL-Database."

