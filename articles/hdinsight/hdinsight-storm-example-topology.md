---
title: "aaaExample Apache Storm-topologieën op HDInsight | Microsoft Docs"
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
ms.openlocfilehash: b20299112f6489b7c99360f0a539fc732703c64a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="example-storm-topologies-and-components-for-apache-storm-on-hdinsight"></a>Voorbeeld van de Storm-topologieën en onderdelen voor Apache Storm op HDInsight

Hallo Hieronder volgt een lijst met voorbeelden gemaakt en beheerd door Microsoft voor gebruik met Apache Storm op HDInsight. Deze voorbeelden hebben betrekking op diverse onderwerpen van basic C# en Java-topologieën tooworking maken met Azure-services zoals Event Hubs, Cosmos DB, Power BI, SQL-Database, HBase op HDInsight en Azure Storage. Enkele voorbeelden demonstreren ook hoe toowork met niet-Azure of zelfs niet-Microsoft-technologieën, zoals SignalR en Socket.IO.

| Beschrijving | Demonstreert | Taal/Framework |
|:--- |:--- |:--- |
| [Apache Storm schrijven tooAzure Data Lake Store](hdinsight-storm-write-data-lake-store.md) |Schrijven van tooAzure Data Lake Store |Java |
| [Event Hub Spout en Bolt bron](https://github.com/apache/storm/tree/master/external/storm-eventhubs) |Bron voor Hallo Event Hub Spout en Bolt |Java |
| [Java gebaseerde topologieën ontwikkelen voor Apache Storm op HDInsight][5797064f] |Maven |Java |
| [C#-topologieën ontwikkelen voor Apache Storm op HDInsight met behulp van Visual Studio][16fce2d1] |HDInsight-hulpprogramma's voor Visual Studio |C#, Java |
| [Maken van meerdere gegevensstromen in een C# Storm-topologie][ec5a4064] |Meerdere streams |C# |
| [Procesgebeurtenissen van Azure Event Hubs met Storm op HDInsight (C#)][844d1d81] |Event Hubs |C# en Java |
| [Procesgebeurtenissen van Azure Event Hubs met Storm op HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md) |Event Hubs |Java |
| [Power Bi toovisualize gegevens uit een Storm-topologie gebruiken][94d15238] |Power BI |C# |
| [Analyseren van sensorgegevens met Storm en HBase in HDInsight][ab894747] |Event Hubs, HBase, Socket.IO, Web-dashboard |C#, Java, JavaScript, HTML |
| [Verwerken van sensorgegevens vehicle van Event Hubs met behulp van Storm op HDInsight][246ee964] |Event Hubs, Cosmos-DB, Azure Storage-Blob (WASB) |C#, Java |
| [Uitpakken, transformeren en Load (ETL) van Azure Event Hubs-tooHBase met Storm op HDInsight][b4b68194] |Event Hubs, HBase |C# |
| [C# Storm-topologie sjabloonproject voor het werken met Azure-services van Storm op HDInsight][ce0c02a2] |Event Hubs, Cosmos-DB, SQL Database, HBase, SignalR |C#, Java |
| [Schaalbaarheid benchmarks voor het lezen van Azure Event Hubs met behulp van Storm op HDInsight][d6c540e3] |Bericht doorvoer, Event Hubs, SQL-Database |C#, Java |
| [Gebeurtenissen met Storm en HBase op HDInsight correleren](hdinsight-storm-correlation-topology.md) |HBase |C# |
| [Python met Storm op HDInsight gebruiken](hdinsight-storm-develop-python-topology.md) |Python-onderdelen met een lichtstroom-topologie |Python |
| [Gebruik Kafka met Storm op HDInsight](hdinsight-apache-storm-with-kafka.md) | Apache Storm lezen en schrijven tooApache Kafka | Java |

### <a name="next-steps"></a>Volgende stappen

* [Aan de slag met Apache Storm in HDInsight][2b8c3488]
* [Meer informatie over hoe toodeploy Storm-topologieën met Storm op HDInsight en beheren][6eb0d3b8]

[2b8c3488]: hdinsight-apache-storm-tutorial-get-started-linux.md "Meer informatie over hoe een Storm op HDInsight-cluster en het gebruik van toocreate voorbeeldtopologieën van Storm-Dashboard toodeploy Hallo."
[6eb0d3b8]: hdinsight-storm-deploy-monitor-topology.md "Meer informatie over hoe toodeploy topologieën met Hallo web gebaseerde Storm-Dashboard en Storm-gebruikersinterface of Hallo HDInsight Tools voor Visual Studio en beheren."
[16fce2d1]: hdinsight-storm-develop-csharp-visual-studio-topology.md "Meer informatie over hoe toocreate C# Storm-topologieën met behulp van HDInsight Tools voor Visual Studio Hallo."
[5797064f]: hdinsight-storm-develop-java-topology.md "Meer informatie over hoe toocreate Storm-topologieën in Java, met behulp van Maven, door het maken van een eenvoudige wordcount-topologie."
[94d15238]: hdinsight-storm-power-bi-topology.md "Laat zien hoe toowrite gegevens tooPower BI vanuit een C#-topologie maakt u een grafiek en een dashboard van Hallo-gegevens."
[ec5a4064]: https://github.com/Blackmist/csharp-storm-example "Demonstreert een eenvoudige Storm-topologie die een wordcount, geïmplementeerd in C# uitvoert. Ook wordt gedemonstreerd hoe toocreate meerdere gegevensstromen binnen een C#-topologie."
[844d1d81]: hdinsight-storm-develop-csharp-event-hub-topology.md "Meer informatie over hoe tooread en write gegevens uit Azure Event Hubs met Storm op HDInsight."
[ab894747]: hdinsight-storm-sensor-data-analysis.md "Ontdek hoe toouse Apache Storm op HDInsight tooprocess sensorgegevens uit Azure Event Hubs met behulp van D3.js visualiseren en (optioneel), sla het tooHBase."
[246ee964]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/IotExample/README.md "Ontdek hoe toouse een Storm-topologie tooread berichten uit Azure Event Hubs gelezen documenten Azure Cosmos DB voor gegevens die verwijzen naar en opslaan van gegevens tooAzure opslag."
[d6c540e3]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/EventCountExample "Verschillende topologieën toodemonstrate doorvoer bij het lezen van Azure Event Hubs en tooSQL opslaan van de Database met behulp van Apache Storm op HDInsight."
[b4b68194]: https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample "Meer informatie over hoe tooread gegevens uit Azure Event Hubs, aggregaat & transformatie Hallo gegevens en vervolgens het tooHBase opslaan op HDInsight."
[ce0c02a2]: https://github.com/hdinsight/hdinsight-storm-examples/tree/master/templates/HDInsightStormExamples "Dit project bevat sjablonen voor spouts, bolts en topologieën toointeract met verschillende Azure-services zoals Event Hubs, Cosmos-database en SQL-Database."

