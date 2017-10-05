---
title: Twitter trends onderwerpen met Apache Storm op HDInsight | Microsoft Docs
description: Informatie over het Trident gebruiken voor het maken van een Apache Storm-topologie die trends onderwerpen op Twitter op basis van hashtags bepaalt.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 63b280ea-5c07-4dc8-a35f-dccf5a96ba93
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/14/2017
ms.author: larryfr
ms.openlocfilehash: d588221586f151319436525c5098b0bb2694e5f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a>Onderwerpen over trends met Apache Storm op HDInsight Twitter bepalen

Informatie over het gebruik van Trident voor het maken van een Storm-topologie die trends onderwerpen (hash-tags) op Twitter bepaalt.

Trident is een abstractie op hoog niveau die voorziet in hulpprogramma's zoals joins, aggregaties groepering, functies en filters. Daarnaast voegt Trident primitieven voor stateful, incrementele verwerking. Het voorbeeld gebruikt in dit document is een Trident-topologie met een aangepaste spout en de functie. Diverse ingebouwde functies die worden geleverd door Trident worden ook gebruikt.

## <a name="requirements"></a>Vereisten

* <a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java en de JDK 1.8</a>

* <a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a>

* <a href="http://git-scm.com/" target="_blank">Git</a>

* Een ontwikkelaarsaccount Twitter

## <a name="download-the-project"></a>Downloaden van het project

De volgende code gebruiken voor het klonen van het project lokaal.

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-the-topology"></a>Inzicht in de topologie

Het volgende diagram ziet van hoe gegevens via deze topologie loopt:

![topologie](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> Dit diagram is een vereenvoudigde weergave van de topologie. Meerdere exemplaren van de onderdelen zijn verdeeld over de knooppunten in het cluster.


De Trident-code die u de topologie implementeert is als volgt:

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

Deze code worden de volgende acties uitgevoerd:

1. Maakt een stream van de spout. De spout tweets opgehaald uit Twitter en filtert deze voor specifieke trefwoorden (hou, muziek en koffie in dit voorbeeld).

2. HashtagExtractor, geen aangepaste functie wordt gebruikt voor het hash-tags van elke tweet uitpakken. De hash-labels worden verzonden naar de stroom.

3. De stroom is gegroepeerd op hash-code en doorgegeven aan een aggregator. Deze aggregator maakt een telling van het aantal keren dat elke hash-code heeft plaatsgevonden. Deze gegevens worden bewaard in het geheugen. Ten slotte is een nieuwe stream met de hash-code en het aantal verzonden.

4. De **FirstN** assembly is toegepast, zodat alleen de top 10 waarden, die zijn gebaseerd op het aantalveld.

> [!NOTE]
> Zie voor meer informatie over het werken met Trident de [Trident-API-overzicht](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.

### <a name="the-spout"></a>De spout

De spout **TwitterSpout**, maakt gebruik van [Twitter4j](http://twitter4j.org/en/) tweets ophalen uit Twitter. Een filter is gemaakt voor de woorden __favoriete__, **muziek**, en **koffie**. Binnenkomende tweets (status) die overeenkomen met het filter worden opgeslagen in een gekoppelde blokkerende wachtrij. Ten slotte worden artikelen opgehaald uit de wachtrij en verzonden naar de topologie.

### <a name="the-hashtagextractor"></a>De HashtagExtractor

Uitpakken van het hash-tags [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) voor het ophalen van alle hash-labels die zijn opgenomen in de tweet wordt gebruikt. Deze worden vervolgens verzonden naar de stroom.

## <a name="configure-twitter"></a>Twitter configureren

Gebruik de volgende stappen een nieuwe Twitter-toepassing registreren en de consumer- en token-informatie nodig voor het lezen van Twitter krijgen:

1. Ga naar [Twitter Apps](https://apps.twitter.com) en klik op de **nieuwe app maken** knop. Bij het invullen in het formulier, laat de **retouraanroep URL** veld leeg.

2. Wanneer de app is gemaakt, klikt u op de **sleutels en toegangstokens** tabblad.

3. Kopieer de **consumentsleutel** en **consumentgeheim** informatie.

4. Selecteer aan de onderkant van de pagina **maken van mijn toegangstoken** als er geen tokens bestaan. Wanneer de tokens zijn gemaakt, kopieert de **Access Token** en **Access Token geheim** informatie.

5. In de **TwitterSpoutTopology** project dat u eerder hebt gekloond, opent de **resources/twitter4j.properties** bestand, voegt u de informatie die u hebt verzameld in de vorige stappen en sla het bestand.

## <a name="build-the-topology"></a>De topologie bouwen

Gebruik de volgende code om het project te bouwen:

        cd [directoryname]
        mvn compile

## <a name="test-the-topology"></a>De topologie testen

Gebruik de volgende opdracht voor het testen van de topologie lokaal:

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

Nadat de topologie wordt gestart, ziet u foutopsporingsinformatie met de hash-tags en telt verzonden door de topologie. De uitvoer ziet er ongeveer de volgende tekst:

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a>Volgende stappen

Nu dat u de topologie lokaal hebt getest, het implementeren van de topologie detecteren: [implementeren en beheren van Apache Storm-topologieën op HDInsight](hdinsight-storm-deploy-monitor-topology.md).

U is mogelijk ook geïnteresseerd in de volgende onderwerpen voor Storm:

* [Java-topologieën ontwikkelen voor Storm op HDInsight met behulp van Maven](hdinsight-storm-develop-java-topology.md)
* [C#-topologieën ontwikkelen voor Storm op HDInsight met behulp van Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)

Voor meer voorbeelden van Storm voor HDInsight:

* [Voorbeeldtopologieën van Storm op HDInsight](hdinsight-storm-example-topology.md)

