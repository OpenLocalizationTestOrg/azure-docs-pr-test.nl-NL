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
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a><span data-ttu-id="ea3a1-103">Onderwerpen over trends met Apache Storm op HDInsight Twitter bepalen</span><span class="sxs-lookup"><span data-stu-id="ea3a1-103">Determine Twitter trending topics with Apache Storm on HDInsight</span></span>

<span data-ttu-id="ea3a1-104">Meer informatie over hoe toouse Trident toocreate een Storm-topologie die bepaalt trends onderwerpen (hash-tags) op Twitter.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-104">Learn how toouse Trident toocreate a Storm topology that determines trending topics (hash tags) on Twitter.</span></span>

<span data-ttu-id="ea3a1-105">Trident is een abstractie op hoog niveau die voorziet in hulpprogramma's zoals joins, aggregaties groepering, functies en filters.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-105">Trident is a high-level abstraction that provides tools such as joins, aggregations, grouping, functions, and filters.</span></span> <span data-ttu-id="ea3a1-106">Daarnaast voegt Trident primitieven voor stateful, incrementele verwerking.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-106">Additionally, Trident adds primitives for doing stateful, incremental processing.</span></span> <span data-ttu-id="ea3a1-107">Hallo-voorbeeld gebruikt in dit document is een Trident-topologie met een aangepaste spout en de functie.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-107">hello example used in this document is a Trident topology with a custom spout and function.</span></span> <span data-ttu-id="ea3a1-108">Diverse ingebouwde functies die worden geleverd door Trident worden ook gebruikt.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-108">It also uses several built-in functions provided by Trident.</span></span>

## <a name="requirements"></a><span data-ttu-id="ea3a1-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ea3a1-109">Requirements</span></span>

* <span data-ttu-id="ea3a1-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java- en Hallo JDK 1.8</a></span><span class="sxs-lookup"><span data-stu-id="ea3a1-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java and hello JDK 1.8</a></span></span>

* <span data-ttu-id="ea3a1-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span><span class="sxs-lookup"><span data-stu-id="ea3a1-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span></span>

* <span data-ttu-id="ea3a1-112"><a href="http://git-scm.com/" target="_blank">Git</a></span><span class="sxs-lookup"><span data-stu-id="ea3a1-112"><a href="http://git-scm.com/" target="_blank">Git</a></span></span>

* <span data-ttu-id="ea3a1-113">Een ontwikkelaarsaccount Twitter</span><span class="sxs-lookup"><span data-stu-id="ea3a1-113">A Twitter developer account</span></span>

## <a name="download-hello-project"></a><span data-ttu-id="ea3a1-114">Hallo-project downloaden</span><span class="sxs-lookup"><span data-stu-id="ea3a1-114">Download hello project</span></span>

<span data-ttu-id="ea3a1-115">Gebruik hello tooclone Hallo CodeProject lokaal te volgen.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-115">Use hello following code tooclone hello project locally.</span></span>

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-hello-topology"></a><span data-ttu-id="ea3a1-116">Understanding Hallo-topologie</span><span class="sxs-lookup"><span data-stu-id="ea3a1-116">Understanding hello topology</span></span>

<span data-ttu-id="ea3a1-117">Hallo volgende diagram laat zien van de manier waarop gegevens via deze topologie loopt:</span><span class="sxs-lookup"><span data-stu-id="ea3a1-117">hello following diagram shows of how data flows through this topology:</span></span>

![topologie](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> <span data-ttu-id="ea3a1-119">Dit diagram is een vereenvoudigde weergave van Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-119">This diagram is a simplified view of hello topology.</span></span> <span data-ttu-id="ea3a1-120">Meerdere exemplaren van Hallo onderdelen worden over Hallo knooppunten in cluster Hallo gedistribueerd.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-120">Multiple instances of hello components are distributed across hello nodes in hello cluster.</span></span>


<span data-ttu-id="ea3a1-121">Hallo Trident-code die wordt geïmplementeerd Hallo topologie is als volgt:</span><span class="sxs-lookup"><span data-stu-id="ea3a1-121">hello Trident code that implements hello topology is as follows:</span></span>

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

<span data-ttu-id="ea3a1-122">Deze code voert Hallo van de volgende activiteiten:</span><span class="sxs-lookup"><span data-stu-id="ea3a1-122">This code performs hello following actions:</span></span>

1. <span data-ttu-id="ea3a1-123">Maakt een stream van Hallo spout.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-123">Creates a stream from hello spout.</span></span> <span data-ttu-id="ea3a1-124">Hallo spout tweets opgehaald uit Twitter en filtert deze voor specifieke trefwoorden (hou, muziek en koffie in dit voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="ea3a1-124">hello spout retrieves tweets from Twitter, and filters them for specific keywords (love, music, and coffee in this example).</span></span>

2. <span data-ttu-id="ea3a1-125">HashtagExtractor, geen aangepaste functie is gebruikte tooextract hash-tags van elke tweet.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-125">HashtagExtractor, a custom function, is used tooextract hash tags from each tweet.</span></span> <span data-ttu-id="ea3a1-126">Hallo hash-tags zijn verzonden toohello stroom.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-126">hello hash tags are emitted toohello stream.</span></span>

3. <span data-ttu-id="ea3a1-127">Hallo-stroom is gegroepeerd op hash-code en tooan aggregator doorgegeven.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-127">hello stream is grouped by hash tag, and passed tooan aggregator.</span></span> <span data-ttu-id="ea3a1-128">Deze aggregator maakt een telling van het aantal keren dat elke hash-code heeft plaatsgevonden.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-128">This aggregator creates a count of how many times each hash tag has occurred.</span></span> <span data-ttu-id="ea3a1-129">Deze gegevens worden bewaard in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-129">This data is persisted in memory.</span></span> <span data-ttu-id="ea3a1-130">Ten slotte is een nieuwe stream met Hallo hash-code en Hallo aantal verzonden.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-130">Finally, a new stream is emitted that contains hello hash tag and hello count.</span></span>

4. <span data-ttu-id="ea3a1-131">Hallo **FirstN** assembly is toegepaste tooreturn alleen Hallo top 10 waarden, op basis van het veld met het aantal Hallo.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-131">hello **FirstN** assembly is applied tooreturn only hello top 10 values, based on hello count field.</span></span>

> [!NOTE]
> <span data-ttu-id="ea3a1-132">Zie voor meer informatie over het werken met Trident Hallo [Trident-API-overzicht](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-132">For more information on working with Trident, see hello [Trident API overview](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.</span></span>

### <a name="hello-spout"></a><span data-ttu-id="ea3a1-133">Hallo spout</span><span class="sxs-lookup"><span data-stu-id="ea3a1-133">hello spout</span></span>

<span data-ttu-id="ea3a1-134">Hallo-spout **TwitterSpout**, maakt gebruik van [Twitter4j](http://twitter4j.org/en/) tooretrieve tweets van Twitter.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-134">hello spout, **TwitterSpout**, uses [Twitter4j](http://twitter4j.org/en/) tooretrieve tweets from Twitter.</span></span> <span data-ttu-id="ea3a1-135">Een filter is gemaakt voor Hallo woorden __favoriete__, **muziek**, en **koffie**.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-135">A filter is created for hello words __love__, **music**, and **coffee**.</span></span> <span data-ttu-id="ea3a1-136">Binnenkomende tweets (status) die overeenkomen met Hallo filter worden opgeslagen in een gekoppelde blokkerende wachtrij.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-136">Incoming tweets (status) that match hello filter are stored in a linked blocking queue.</span></span> <span data-ttu-id="ea3a1-137">Ten slotte items worden opgehaald uit de wachtrij Hallo en toohello topologie verzonden.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-137">Finally, items are pulled off hello queue and emitted toohello topology.</span></span>

### <a name="hello-hashtagextractor"></a><span data-ttu-id="ea3a1-138">Hallo HashtagExtractor</span><span class="sxs-lookup"><span data-stu-id="ea3a1-138">hello HashtagExtractor</span></span>

<span data-ttu-id="ea3a1-139">tooextract hash-tags, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) gebruikte tooretrieve alle hash-labels die zijn opgenomen in een tweet Hallo is.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-139">tooextract hash tags, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) is used tooretrieve all hash tags that are contained in hello tweet.</span></span> <span data-ttu-id="ea3a1-140">Dit zijn dan verzonden toohello stroom.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-140">These are then emitted toohello stream.</span></span>

## <a name="configure-twitter"></a><span data-ttu-id="ea3a1-141">Twitter configureren</span><span class="sxs-lookup"><span data-stu-id="ea3a1-141">Configure Twitter</span></span>

<span data-ttu-id="ea3a1-142">Volgende stappen tooregister een nieuwe Twitter-toepassing hello gebruiken en te verkrijgen van Hallo consumer- en token-informatie die nodig zijn tooread van Twitter:</span><span class="sxs-lookup"><span data-stu-id="ea3a1-142">Use hello following steps tooregister a new Twitter application and obtain hello consumer and access token information needed tooread from Twitter:</span></span>

1. <span data-ttu-id="ea3a1-143">Ga te[Twitter Apps](https://apps.twitter.com) en klik op Hallo **nieuwe app maken** knop.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-143">Go too[Twitter Apps](https://apps.twitter.com) and click hello **Create new app** button.</span></span> <span data-ttu-id="ea3a1-144">Hallo formulier invullen, laat u Hallo **retouraanroep URL** veld leeg.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-144">When filling in hello form, leave hello **Callback URL** field empty.</span></span>

2. <span data-ttu-id="ea3a1-145">Wanneer het Hallo-app is gemaakt, klikt u op Hallo **sleutels en toegangstokens** tabblad.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-145">When hello app is created, click hello **Keys and Access Tokens** tab.</span></span>

3. <span data-ttu-id="ea3a1-146">Kopiëren Hallo **consumentsleutel** en **consumentgeheim** informatie.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-146">Copy hello **Consumer Key** and **Consumer Secret** information.</span></span>

4. <span data-ttu-id="ea3a1-147">Selecteer onderaan Hallo Hallo pagina, **maken van mijn toegangstoken** als er geen tokens bestaan.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-147">At hello bottom of hello page, select **Create my access token** if no tokens exist.</span></span> <span data-ttu-id="ea3a1-148">Wanneer Hallo tokens zijn gemaakt, kopie Hallo **Access Token** en **Access Token geheim** informatie.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-148">When hello tokens have been created, copy hello **Access Token** and **Access Token Secret** information.</span></span>

5. <span data-ttu-id="ea3a1-149">In Hallo **TwitterSpoutTopology** project u eerder hebt gekloond, open Hallo **resources/twitter4j.properties** bestand, Hallo-gegevens die u hebt verzameld toevoegen in de vorige stappen Hallo en sla Hallo-bestand .</span><span class="sxs-lookup"><span data-stu-id="ea3a1-149">In hello **TwitterSpoutTopology** project you previously cloned, open hello **resources/twitter4j.properties** file, add hello information you gathered in hello previous steps, and then save hello file.</span></span>

## <a name="build-hello-topology"></a><span data-ttu-id="ea3a1-150">Hallo-topologie bouwen</span><span class="sxs-lookup"><span data-stu-id="ea3a1-150">Build hello topology</span></span>

<span data-ttu-id="ea3a1-151">Hallo CodeProject toobuild Hallo volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="ea3a1-151">Use hello following code toobuild hello project:</span></span>

        cd [directoryname]
        mvn compile

## <a name="test-hello-topology"></a><span data-ttu-id="ea3a1-152">Test Hallo-topologie</span><span class="sxs-lookup"><span data-stu-id="ea3a1-152">Test hello topology</span></span>

<span data-ttu-id="ea3a1-153">Gebruik Hallo opdracht tootest Hallo topologie lokaal te volgen:</span><span class="sxs-lookup"><span data-stu-id="ea3a1-153">Use hello following command tootest hello topology locally:</span></span>

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

<span data-ttu-id="ea3a1-154">Nadat het Hallo-topologie wordt gestart, ziet u foutopsporingsinformatie Hallo hash met tags en telt verzonden door Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="ea3a1-154">After hello topology starts, you should see debug information that contains hello hash tags and counts emitted by hello topology.</span></span> <span data-ttu-id="ea3a1-155">Hallo-uitvoer moet worden weergegeven vergelijkbaar toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="ea3a1-155">hello output should appear similar toohello following text:</span></span>

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a><span data-ttu-id="ea3a1-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ea3a1-156">Next steps</span></span>

<span data-ttu-id="ea3a1-157">Nu dat u lokaal Hallo-topologie hebt getest, ontdekken hoe toodeploy topologie Hallo: [implementeren en beheren van Apache Storm-topologieën op HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span><span class="sxs-lookup"><span data-stu-id="ea3a1-157">Now that you have tested hello topology locally, discover how toodeploy hello topology: [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span></span>

<span data-ttu-id="ea3a1-158">U is mogelijk ook geïnteresseerd in de volgende onderwerpen voor Storm Hallo:</span><span class="sxs-lookup"><span data-stu-id="ea3a1-158">You may also be interested in hello following Storm topics:</span></span>

* [<span data-ttu-id="ea3a1-159">Java-topologieën ontwikkelen voor Storm op HDInsight met behulp van Maven</span><span class="sxs-lookup"><span data-stu-id="ea3a1-159">Develop Java topologies for Storm on HDInsight using Maven</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="ea3a1-160">C#-topologieën ontwikkelen voor Storm op HDInsight met behulp van Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ea3a1-160">Develop C# topologies for Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="ea3a1-161">Voor meer voorbeelden van Storm voor HDInsight:</span><span class="sxs-lookup"><span data-stu-id="ea3a1-161">For more Storm examples for HDInsight:</span></span>

* [<span data-ttu-id="ea3a1-162">Voorbeeldtopologieën van Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="ea3a1-162">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

