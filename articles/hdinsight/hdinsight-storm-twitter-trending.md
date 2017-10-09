---
title: onderwerpen over trends met Apache Storm op HDInsight aaaTwitter | Microsoft Docs
description: Meer informatie over hoe toouse Trident toocreate een Apache Storm-topologie die trends onderwerpen op Twitter bepaalt op basis van hashtags.
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
ms.openlocfilehash: 0281b495d10833c63868b36856c96369b139c553
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a>Onderwerpen over trends met Apache Storm op HDInsight Twitter bepalen

Meer informatie over hoe toouse Trident toocreate een Storm-topologie die bepaalt trends onderwerpen (hash-tags) op Twitter.

Trident is een abstractie op hoog niveau die voorziet in hulpprogramma's zoals joins, aggregaties groepering, functies en filters. Daarnaast voegt Trident primitieven voor stateful, incrementele verwerking. Hallo-voorbeeld gebruikt in dit document is een Trident-topologie met een aangepaste spout en de functie. Diverse ingebouwde functies die worden geleverd door Trident worden ook gebruikt.

## <a name="requirements"></a>Vereisten

* <a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java- en Hallo JDK 1.8</a>

* <a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a>

* <a href="http://git-scm.com/" target="_blank">Git</a>

* Een ontwikkelaarsaccount Twitter

## <a name="download-hello-project"></a>Hallo-project downloaden

Gebruik hello tooclone Hallo CodeProject lokaal te volgen.

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-hello-topology"></a>Understanding Hallo-topologie

Hallo volgende diagram laat zien van de manier waarop gegevens via deze topologie loopt:

![topologie](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> Dit diagram is een vereenvoudigde weergave van Hallo-topologie. Meerdere exemplaren van Hallo onderdelen worden over Hallo knooppunten in cluster Hallo gedistribueerd.


Hallo Trident-code die wordt geïmplementeerd Hallo topologie is als volgt:

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

Deze code voert Hallo van de volgende activiteiten:

1. Maakt een stream van Hallo spout. Hallo spout tweets opgehaald uit Twitter en filtert deze voor specifieke trefwoorden (hou, muziek en koffie in dit voorbeeld).

2. HashtagExtractor, geen aangepaste functie is gebruikte tooextract hash-tags van elke tweet. Hallo hash-tags zijn verzonden toohello stroom.

3. Hallo-stroom is gegroepeerd op hash-code en tooan aggregator doorgegeven. Deze aggregator maakt een telling van het aantal keren dat elke hash-code heeft plaatsgevonden. Deze gegevens worden bewaard in het geheugen. Ten slotte is een nieuwe stream met Hallo hash-code en Hallo aantal verzonden.

4. Hallo **FirstN** assembly is toegepaste tooreturn alleen Hallo top 10 waarden, op basis van het veld met het aantal Hallo.

> [!NOTE]
> Zie voor meer informatie over het werken met Trident Hallo [Trident-API-overzicht](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.

### <a name="hello-spout"></a>Hallo spout

Hallo-spout **TwitterSpout**, maakt gebruik van [Twitter4j](http://twitter4j.org/en/) tooretrieve tweets van Twitter. Een filter is gemaakt voor Hallo woorden __favoriete__, **muziek**, en **koffie**. Binnenkomende tweets (status) die overeenkomen met Hallo filter worden opgeslagen in een gekoppelde blokkerende wachtrij. Ten slotte items worden opgehaald uit de wachtrij Hallo en toohello topologie verzonden.

### <a name="hello-hashtagextractor"></a>Hallo HashtagExtractor

tooextract hash-tags, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) gebruikte tooretrieve alle hash-labels die zijn opgenomen in een tweet Hallo is. Dit zijn dan verzonden toohello stroom.

## <a name="configure-twitter"></a>Twitter configureren

Volgende stappen tooregister een nieuwe Twitter-toepassing hello gebruiken en te verkrijgen van Hallo consumer- en token-informatie die nodig zijn tooread van Twitter:

1. Ga te[Twitter Apps](https://apps.twitter.com) en klik op Hallo **nieuwe app maken** knop. Hallo formulier invullen, laat u Hallo **retouraanroep URL** veld leeg.

2. Wanneer het Hallo-app is gemaakt, klikt u op Hallo **sleutels en toegangstokens** tabblad.

3. Kopiëren Hallo **consumentsleutel** en **consumentgeheim** informatie.

4. Selecteer onderaan Hallo Hallo pagina, **maken van mijn toegangstoken** als er geen tokens bestaan. Wanneer Hallo tokens zijn gemaakt, kopie Hallo **Access Token** en **Access Token geheim** informatie.

5. In Hallo **TwitterSpoutTopology** project u eerder hebt gekloond, open Hallo **resources/twitter4j.properties** bestand, Hallo-gegevens die u hebt verzameld toevoegen in de vorige stappen Hallo en sla Hallo-bestand .

## <a name="build-hello-topology"></a>Hallo-topologie bouwen

Hallo CodeProject toobuild Hallo volgende gebruiken:

        cd [directoryname]
        mvn compile

## <a name="test-hello-topology"></a>Test Hallo-topologie

Gebruik Hallo opdracht tootest Hallo topologie lokaal te volgen:

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

Nadat het Hallo-topologie wordt gestart, ziet u foutopsporingsinformatie Hallo hash met tags en telt verzonden door Hallo-topologie. Hallo-uitvoer moet worden weergegeven vergelijkbaar toohello volgende tekst:

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

Nu dat u lokaal Hallo-topologie hebt getest, ontdekken hoe toodeploy topologie Hallo: [implementeren en beheren van Apache Storm-topologieën op HDInsight](hdinsight-storm-deploy-monitor-topology.md).

U is mogelijk ook geïnteresseerd in de volgende onderwerpen voor Storm Hallo:

* [Java-topologieën ontwikkelen voor Storm op HDInsight met behulp van Maven](hdinsight-storm-develop-java-topology.md)
* [C#-topologieën ontwikkelen voor Storm op HDInsight met behulp van Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)

Voor meer voorbeelden van Storm voor HDInsight:

* [Voorbeeldtopologieën van Storm op HDInsight](hdinsight-storm-example-topology.md)

