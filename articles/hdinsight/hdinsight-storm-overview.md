---
title: aaaWhat is Apache Storm - Azure HDInsight | Microsoft Docs
description: Apache Storm kunt u tooprocess gegevensstromen in realtime. Azure HDInsight kunt u tooeasily Storm-clusters maken op Hallo Azure-cloud. U kunt met Visual Studio maken met C# Storm-oplossingen en vervolgens implementeren tooyour die hdinsight Storm-clusters.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: apache storm use cases,storm cluster,wat is apache storm
ms.assetid: 72d54080-1e48-4a5e-aa50-cce4ffc85077
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 6c6b2925ef3e5666dfecc3fb3c835bb362902c51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-storm-on-azure-hdinsight"></a>Wat is Apache Storm in Azure HDInsight?

[Apache Storm](http://storm.apache.org/) is een gedistribueerd, fouttolerant en open-source computingsysteem. U kunt Storm tooprocess gegevensstromen in realtime gebruiken met Hadoop. Storm-oplossingen bieden ook gegarandeerde verwerking van gegevens, met Hallo mogelijkheid tooreplay gegevens die niet met succes verwerkt Hallo eerst.

Storm op HDInsight biedt Hallo volgende belangrijke voordelen:

* Wordt uitgevoerd als een beheerde service met een SLA van 99,9 procent beschikbaarheid.

* Ondersteunt de mogelijkheid om eenvoudig aanpassingen te implementeren door tijdens of na het maken van een Storm-cluster scripts voor dat cluster uit te voeren. Zie [HDInsight-clusters aanpassen met scriptacties](hdinsight-hadoop-customize-cluster-linux.md) voor meer informatie.

* Gebruikt verschillende talen. U kunt de Storm-onderdelen schrijven in Hallo taal van uw keuze, zoals Java, C# en Python.

    * Visual Studio is geïntegreerd met HDInsight Hallo ontwikkeling, beheer en controle van C#-topologieën. Zie voor meer informatie [ontwikkelen C# Storm-topologieën met HDInsight Tools voor Visual Studio Hallo](hdinsight-storm-develop-csharp-visual-studio-topology.md).

    * Ondersteunt Hallo Trident Java-interface. U kunt Storm-topologieën maken die ondersteuning bieden voor een eenmalige verwerking van berichten, transactionele DataStore-persistentie en een aantal algemene Stream Analytics-bewerkingen.

*  Storm-clusters eenvoudig omhoog en omlaag schalen. U kunt toevoegen of verwijderen van worker-knooppunten met geen impact toorunning Storm-topologieën.

* Geïntegreerd met hello Azure-services te volgen:

    * Azure Event Hubs

    * Azure Virtual Network

    * Azure SQL Database

    * Azure Storage

    * Azure Cosmos DB

* Combineert veilig Hallo-mogelijkheden van meerdere HDInsight-clusters met behulp van virtueel netwerk. U kunt analytische pijplijnen maken die gebruikmaken van Storm-, Kafka-, Spark-, HBase- of Hadoop-clusters.

Zie [deze Engelstalige site](https://storm.apache.org/documentation/Powered-By.html) voor een lijst met bedrijven die Apache Storm gebruiken voor hun oplossingen voor realtime analyse.

tooget de slag met Storm, Zie [aan de slag met Storm op HDInsight][gettingstarted].

## <a name="how-does-storm-work"></a>Hoe werkt Storm

Storm voert topologieën in plaats van Hallo MapReduce-taken die u mogelijk kent. Storm-topologieën bestaan uit meerdere onderdelen die zijn gerangschikt in een Directed Acyclic Graph (DAG). Gegevensoverdrachten tussen onderdelen in de grafiek Hallo Hallo. Elk onderdeel verbruikt een of meer gegevensstromen en kan eventueel een of meer stromen genereren. Hallo volgende diagram illustreert hoe gegevens worden uitgewisseld tussen de onderdelen van een eenvoudige word-count-topologie:

![Voorbeeld van hoe onderdelen zijn gerangschikt in een Storm-topologie](./media/hdinsight-storm-overview/example-apache-storm-topology-diagram.png)

* Via Spout-onderdelen worden gegevens overgebracht naar een topologie. Ze verzenden een of meer stromen naar het Hallo-topologie.

* Bolt-onderdelen verwerken stromen die afkomstig zijn van spouts of andere bolts. Bolts mogelijk eventueel streams verzenden naar Hallo-topologie. Bolts zijn ook verantwoordelijk voor het schrijven van gegevens tooexternal services of opslag, zoals HDFS, Kafka of HBase.

## <a name="ease-of-creation"></a>Eenvoudig te maken

U kunt in enkele minuten een nieuw Storm-cluster op HDInsight inrichten. Zie [Aan de slag met Storm op HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) voor meer informatie over het maken van een Storm-cluster.

## <a name="ease-of-use"></a>Gebruiksgemak

* __Secure Shell (SSH) connectiviteit__: U toegang hebt tot de hoofdknooppunten Hallo van uw Storm-cluster via Hallo Internet met behulp van SSH. U kunt opdrachten rechtstreeks op het cluster uitvoeren met behulp van SSH.

  Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

* __Web-connectiviteit__: alle HDInsight-clusters bieden Hallo Ambari-webgebruikersinterface. U kunt gemakkelijk bewaken, configureren en beheren van services op het cluster met behulp van Hallo Ambari-webgebruikersinterface. Storm-clusters bieden ook Hallo Storm-gebruikersinterface. U kunt bewaken en beheren van de actieve Storm-topologieën vanuit de browser via Hallo Storm-gebruikersinterface.

  Zie voor meer informatie, Hallo [HDInsight beheren met behulp van Hallo Ambari-Webgebruikersinterface](hdinsight-hadoop-manage-ambari.md) en [bewaken en beheren met behulp van Hallo Storm-gebruikersinterface](hdinsight-storm-deploy-monitor-topology-linux.md#monitor-and-manage-storm-ui) documenten.

* __Azure PowerShell en Azure CLI__: PowerShell en CLI beide opdrachtregelprogramma's waarmee u vanaf uw client system toowork met HDInsight en andere Azure-services gebruiken kunt bieden.

* __Visual Studio-integratie__: Azure Data Lake Tools voor Visual Studio project-sjablonen voor het maken van C# Storm-topologieën met behulp van Hallo SCP.Net framework bevatten. Data Lake Tools bieden ook hulpprogramma's voor toodeploy, bewaken en beheren van oplossingen met Storm op HDInsight.

  Zie voor meer informatie [ontwikkelen C# Storm-topologieën met HDInsight Tools voor Visual Studio Hallo](hdinsight-storm-develop-csharp-visual-studio-topology.md).

## <a name="integration-with-other-azure-services"></a>Integratie met andere Azure-services

* __Azure Data Lake Store__: voor een voorbeeld van het gebruik van Data Lake Store met een Storm-cluster raadpleegt u [Use Azure Data Lake Store with Apache Storm with HDInsight](hdinsight-storm-write-data-lake-store.md) (Azure Data Lake Store gebruiken met Apache Storm in HDInsight).

* __Event Hubs__: Zie voor een voorbeeld van het gebruik van Event Hubs met een Storm-cluster, Hallo documenten te volgen:

    * [Develop a Java-based topology for Storm on HDInsight](hdinsight-storm-develop-java-topology.md) (Een topologie op basis van Java ontwikkelen voor Storm op HDInsight)

    * [Process events from Azure Event Hubs with Storm on HDInsight (C#)](hdinsight-storm-develop-csharp-event-hub-topology.md) (Gebeurtenissen uit Azure Event Hubs verwerken met Storm op HDInsight (C#))

* __SQL-Database__, __Cosmos DB__, __Event Hubs__, en __HBase__: sjabloon voorbeelden zijn opgenomen in Hallo Data Lake Tools voor Visual Studio. Zie [Een C#-topologie voor Storm op HDInsight ontwikkelen](hdinsight-storm-develop-csharp-visual-studio-topology.md) voor meer informatie.

## <a name="reliability"></a>Betrouwbaarheid

Apache Storm zorgt ervoor dat elk binnenkomend bericht altijd volledig is verwerkt, zelfs wanneer Hallo gegevensanalyse is verspreid over honderden knooppunten.

Hallo Nimbus-knooppunt biedt functionaliteit vergelijkbaar toohello Hadoop JobTracker en wijst taken toe tooother knooppunten in een cluster via Zookeeper. Zookeeper-knooppunten bieden coördinatie voor een cluster en faciliteren de communicatie tussen Nimbus en Hallo Supervisor proces op Hallo worker-knooppunten. Als een verwerkingsknooppunt uitgeschakeld wordt, Hallo Nimbus-knooppunt in kennis wordt gesteld en het Hallo-taak en gerelateerde gegevens tooanother knooppunt worden toegewezen.

Hallo standaardconfiguratie voor Apache Storm-clusters is toohave slechts één Nimbus knooppunt. Storm in HDInsight ondersteunt twee Nimbus-knooppunten. Als het primaire knooppunt Hallo mislukt, switches Hallo Storm-cluster toohello secundair knooppunt terwijl Hallo primaire knooppunt hersteld. Hallo illustreert volgende diagram Hallo taakconfiguratie stroom voor Storm op HDInsight:

![Diagram van nimbus, zookeeper en supervisor](./media/hdinsight-storm-overview/nimbus.png)

## <a name="scale"></a>Schalen

HDInsight-clusters kunnen dynamisch worden geschaald door werkrolknooppunten toe te voegen of te verwijderen. Deze bewerking kan worden uitgevoerd tijdens het verwerken van gegevens.

> [!IMPORTANT]
> tootake profiteren van nieuwe knooppunten toegevoegd door te schalen, moet u toorebalance Storm-topologieën gestart voordat Hallo clustergrootte werd uitgebreid.

## <a name="support"></a>Ondersteuning

Storm op HDInsight wordt geleverd met volledige en onafgebroken ondersteuning op ondernemingsniveau. Storm op HDInsight beschikt eveneens over een SLA van 99,9 procent. Dit betekent dat wordt gegarandeerd dat een Storm-cluster externe verbinding minimaal 99,9 procent Hallo tijd heeft.

Zie [Ondersteuning van Azure](https://azure.microsoft.com/support/options/) voor meer informatie.

## <a name="apache-storm-use-cases"></a>Use cases van Apache Storm

Hallo Hieronder volgen enkele algemene scenario's waarvoor u Storm op HDInsight kunt gebruiken:

* Internet der dingen (IoT)
* Fraudedetectie
* Sociale analyses
* Extractie, transformatie en laden (ETL)
* Netwerkbewaking
* Search
* Mobile Engagement

Zie voor informatie over praktijkscenario's Hallo [hoe bedrijven Storm gebruiken](https://storm.apache.org/documentation/Powered-By.html) document.

## <a name="development"></a>Ontwikkeling

Met hulp van Data Lake-tools voor Visual Studio kunnen .NET-ontwikkelaars topologieën ontwerpen en implementeren voor Visual Studio. U kunt ook hybride topologieën maken die gebruikmaken van Java- en C#-onderdelen.

Zie [Develop C# topologies for Apache Storm on HDInsight using Hadoop tools for Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md) (C#-topologieën voor Storm op HDInsight ontwikkelen met Visual Studio) voor meer informatie.

U kunt ook Java oplossingen ontwikkelen met behulp van Hallo IDE van uw keuze. Zie [Develop Java topologies for Storm on HDInsight](hdinsight-storm-develop-java-topology.md) (Java-topologieën ontwikkelen voor Storm op HDInsight) voor meer informatie.

Python kan ook worden gebruikt toodevelop Storm-onderdelen. Zie [Develop Storm topologies using Python on HDInsight](hdinsight-storm-develop-python-topology.md) (Storm-topologieën ontwikkelen met Python voor Storm op HDInsight) voor meer informatie.

## <a name="common-development-patterns"></a>Algemene ontwikkelingspatronen

### <a name="guaranteed-message-processing"></a>Gegarandeerde berichtverwerking

Apache Storm kan verschillende niveaus van gegarandeerde berichtverwerking bieden. Een eenvoudige Storm-toepassing biedt u bijvoorbeeld de garantie dat de gegevens minimaal één keer worden verwerkt. Trident kan u de garantie bieden dat gegevens exact één keer worden verwerkt.

Zie [Guarantees on data processing](https://storm.apache.org/about/guarantees-data-processing.html) (Garanties met betrekking tot de gegevensverwerking) op apache.org voor meer informatie.

### <a name="ibasicbolt"></a>IBasicBolt

Hallo patroon voor het lezen van een invoer-tuple tekensetcodering nul of meer tuples zijn, en vervolgens de methode voor het uitvoeren van om Hallo invoer-tuple onmiddellijk achter Hallo Hallo geldt. Storm biedt Hallo [IBasicBolt](https://storm.apache.org/releases/1.0.3/javadocs/org/apache/storm/topology/IBasicBolt.html) interface tooautomate dit patroon.

### <a name="joins"></a>Samenvoegingen

Hoe gegevensstromen worden gekoppeld, varieert per toepassing. U kunt bijvoorbeeld elke tuple uit meerdere streams samenvoegen in één nieuwe stream, of u kunt alleen batches tuples voor een specifiek venster samenvoegen. In beide gevallen kunt u hiervoor [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-) gebruiken. Veld groeperen is een manier om te definiëren hoe tuples worden gerouteerd toobolts.

In Hallo Java-voorbeeld te volgen, wordt fieldsGrouping gebruikt tooroute tuples die afkomstig van onderdelen '1', '2' en '3' toohello MyJoiner bolt zijn:

    builder.setBolt("join", new MyJoiner(), parallelism) .fieldsGrouping("1", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("2", new Fields("joinfield1", "joinfield2")) .fieldsGrouping("3", new Fields("joinfield1", "joinfield2"));

### <a name="batches"></a>Batches

Apache Storm biedt een intern timingmechanisme dat bekend staat als een 'tick tuple'. U kunt instellen hoe vaak in uw topologie een tick tuple wordt verzonden.

Zie [PartialBoltCount.cs](https://github.com/hdinsight/hdinsight-storm-examples/blob/3b2c960549cac122e8874931df4801f0934fffa7/EventCountExample/EventCountTopology/src/main/java/com/microsoft/hdinsight/storm/examples/PartialCountBolt.java) voor een voorbeeld van het gebruik van een tick tuple uit een C#-onderdeel.

### <a name="caches"></a>Caches

In-memory caching wordt vaak gebruikt als mechanisme om de verwerking te versnellen, omdat de veelgebruikte assets in het geheugen blijven staan. Omdat een topologie wordt verdeeld over meerdere knooppunten en meerdere processen binnen elk knooppunt, is het goed om het gebruik van [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-) te overwegen. Gebruik `fieldsGrouping` tooensure tuples met Hallo-velden die worden gebruikt voor zoeken in het cachegeheugen zijn altijd gerouteerde toohello dezelfde verwerken. Met deze groeperingsfunctionaliteit voorkomt u dubbele cachevermeldingen voor verschillende processen.

### <a name="stream-top-n"></a>'Top N' van stromen

Wanneer uw topologie is afhankelijk van de berekening van een top N-waarde, Hallo top N-waarde parallel berekenen Vervolgens samenvoegen Hallo uitvoer van deze berekeningen in een algemene waarde. Deze bewerking kan worden gedaan met [fieldsGrouping](http://storm.apache.org/releases/current/javadocs/org/apache/storm/topology/InputDeclarer.html#fieldsGrouping-java.lang.String-org.apache.storm.tuple.Fields-) tooroute door veld voor parallelle verwerking. U kunt vervolgens tooa bolt die globaal de top N-waarde Hallo bepaalt versturen.

Zie voor een voorbeeld van een top N-waarde wilt berekenen, Hallo [RollingTopWords](https://github.com/apache/storm/blob/master/examples/storm-starter/src/jvm/org/apache/storm/starter/RollingTopWords.java) voorbeeld.

## <a name="logging"></a>Logboekregistratie

Storm Apache-Log4j toolog gegevens gebruikt. Standaard, een grote hoeveelheid gegevens wordt geregistreerd en het moeilijk toosort via Hallo informatie kan zijn. U kunt een configuratiebestand logboekregistratie opnemen als onderdeel van uw Storm-topologie toocontrol logboekregistratie gedrag.

Voor een van de voorbeeldtopologie die u laat zien hoe tooconfigure aan te melden, zien [WordCount Java gebaseerde](hdinsight-storm-develop-java-topology.md) voorbeeld voor Storm op HDInsight.

## <a name="next-steps"></a>Volgende stappen

Meer informatie over realtime analyseoplossingen met Storm in HDInsight:

* [Aan de slag met Apache Storm in HDInsight][gettingstarted]
* [Example Storm toplogies and components for Apache Storm on HDInsight](hdinsight-storm-example-topology.md) (Voorbeelden van Storm-topologieën en -onderdelen in HDInsight)

[stormtrident]: https://storm.apache.org/documentation/Trident-API-Overview.html
[samoa]: http://yahooeng.tumblr.com/post/65453012905/introducing-samoa-an-open-source-platform-for-mining
[apachetutorial]: https://storm.apache.org/documentation/Tutorial.html
[gettingstarted]: hdinsight-apache-storm-tutorial-get-started-linux.md
