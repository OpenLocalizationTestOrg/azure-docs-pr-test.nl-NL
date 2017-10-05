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
# <a name="determine-twitter-trending-topics-with-apache-storm-on-hdinsight"></a><span data-ttu-id="f0183-103">Onderwerpen over trends met Apache Storm op HDInsight Twitter bepalen</span><span class="sxs-lookup"><span data-stu-id="f0183-103">Determine Twitter trending topics with Apache Storm on HDInsight</span></span>

<span data-ttu-id="f0183-104">Informatie over het gebruik van Trident voor het maken van een Storm-topologie die trends onderwerpen (hash-tags) op Twitter bepaalt.</span><span class="sxs-lookup"><span data-stu-id="f0183-104">Learn how to use Trident to create a Storm topology that determines trending topics (hash tags) on Twitter.</span></span>

<span data-ttu-id="f0183-105">Trident is een abstractie op hoog niveau die voorziet in hulpprogramma's zoals joins, aggregaties groepering, functies en filters.</span><span class="sxs-lookup"><span data-stu-id="f0183-105">Trident is a high-level abstraction that provides tools such as joins, aggregations, grouping, functions, and filters.</span></span> <span data-ttu-id="f0183-106">Daarnaast voegt Trident primitieven voor stateful, incrementele verwerking.</span><span class="sxs-lookup"><span data-stu-id="f0183-106">Additionally, Trident adds primitives for doing stateful, incremental processing.</span></span> <span data-ttu-id="f0183-107">Het voorbeeld gebruikt in dit document is een Trident-topologie met een aangepaste spout en de functie.</span><span class="sxs-lookup"><span data-stu-id="f0183-107">The example used in this document is a Trident topology with a custom spout and function.</span></span> <span data-ttu-id="f0183-108">Diverse ingebouwde functies die worden geleverd door Trident worden ook gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f0183-108">It also uses several built-in functions provided by Trident.</span></span>

## <a name="requirements"></a><span data-ttu-id="f0183-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f0183-109">Requirements</span></span>

* <span data-ttu-id="f0183-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java en de JDK 1.8</a></span><span class="sxs-lookup"><span data-stu-id="f0183-110"><a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">Java and the JDK 1.8</a></span></span>

* <span data-ttu-id="f0183-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span><span class="sxs-lookup"><span data-stu-id="f0183-111"><a href="http://maven.apache.org/what-is-maven.html" target="_blank">Maven</a></span></span>

* <span data-ttu-id="f0183-112"><a href="http://git-scm.com/" target="_blank">Git</a></span><span class="sxs-lookup"><span data-stu-id="f0183-112"><a href="http://git-scm.com/" target="_blank">Git</a></span></span>

* <span data-ttu-id="f0183-113">Een ontwikkelaarsaccount Twitter</span><span class="sxs-lookup"><span data-stu-id="f0183-113">A Twitter developer account</span></span>

## <a name="download-the-project"></a><span data-ttu-id="f0183-114">Downloaden van het project</span><span class="sxs-lookup"><span data-stu-id="f0183-114">Download the project</span></span>

<span data-ttu-id="f0183-115">De volgende code gebruiken voor het klonen van het project lokaal.</span><span class="sxs-lookup"><span data-stu-id="f0183-115">Use the following code to clone the project locally.</span></span>

    git clone https://github.com/Blackmist/TwitterTrending

## <a name="understanding-the-topology"></a><span data-ttu-id="f0183-116">Inzicht in de topologie</span><span class="sxs-lookup"><span data-stu-id="f0183-116">Understanding the topology</span></span>

<span data-ttu-id="f0183-117">Het volgende diagram ziet van hoe gegevens via deze topologie loopt:</span><span class="sxs-lookup"><span data-stu-id="f0183-117">The following diagram shows of how data flows through this topology:</span></span>

![topologie](./media/hdinsight-storm-twitter-trending/trident.png)

> [!NOTE]
> <span data-ttu-id="f0183-119">Dit diagram is een vereenvoudigde weergave van de topologie.</span><span class="sxs-lookup"><span data-stu-id="f0183-119">This diagram is a simplified view of the topology.</span></span> <span data-ttu-id="f0183-120">Meerdere exemplaren van de onderdelen zijn verdeeld over de knooppunten in het cluster.</span><span class="sxs-lookup"><span data-stu-id="f0183-120">Multiple instances of the components are distributed across the nodes in the cluster.</span></span>


<span data-ttu-id="f0183-121">De Trident-code die u de topologie implementeert is als volgt:</span><span class="sxs-lookup"><span data-stu-id="f0183-121">The Trident code that implements the topology is as follows:</span></span>

    topology.newStream("spout", spout)
        .each(new Fields("tweet"), new HashtagExtractor(), new Fields("hashtag"))
        .groupBy(new Fields("hashtag"))
        .persistentAggregate(new MemoryMapState.Factory(), new Count(), new Fields("count"))
        .newValuesStream()
        .applyAssembly(new FirstN(10, "count"))
        .each(new Fields("hashtag", "count"), new Debug());

<span data-ttu-id="f0183-122">Deze code worden de volgende acties uitgevoerd:</span><span class="sxs-lookup"><span data-stu-id="f0183-122">This code performs the following actions:</span></span>

1. <span data-ttu-id="f0183-123">Maakt een stream van de spout.</span><span class="sxs-lookup"><span data-stu-id="f0183-123">Creates a stream from the spout.</span></span> <span data-ttu-id="f0183-124">De spout tweets opgehaald uit Twitter en filtert deze voor specifieke trefwoorden (hou, muziek en koffie in dit voorbeeld).</span><span class="sxs-lookup"><span data-stu-id="f0183-124">The spout retrieves tweets from Twitter, and filters them for specific keywords (love, music, and coffee in this example).</span></span>

2. <span data-ttu-id="f0183-125">HashtagExtractor, geen aangepaste functie wordt gebruikt voor het hash-tags van elke tweet uitpakken.</span><span class="sxs-lookup"><span data-stu-id="f0183-125">HashtagExtractor, a custom function, is used to extract hash tags from each tweet.</span></span> <span data-ttu-id="f0183-126">De hash-labels worden verzonden naar de stroom.</span><span class="sxs-lookup"><span data-stu-id="f0183-126">The hash tags are emitted to the stream.</span></span>

3. <span data-ttu-id="f0183-127">De stroom is gegroepeerd op hash-code en doorgegeven aan een aggregator.</span><span class="sxs-lookup"><span data-stu-id="f0183-127">The stream is grouped by hash tag, and passed to an aggregator.</span></span> <span data-ttu-id="f0183-128">Deze aggregator maakt een telling van het aantal keren dat elke hash-code heeft plaatsgevonden.</span><span class="sxs-lookup"><span data-stu-id="f0183-128">This aggregator creates a count of how many times each hash tag has occurred.</span></span> <span data-ttu-id="f0183-129">Deze gegevens worden bewaard in het geheugen.</span><span class="sxs-lookup"><span data-stu-id="f0183-129">This data is persisted in memory.</span></span> <span data-ttu-id="f0183-130">Ten slotte is een nieuwe stream met de hash-code en het aantal verzonden.</span><span class="sxs-lookup"><span data-stu-id="f0183-130">Finally, a new stream is emitted that contains the hash tag and the count.</span></span>

4. <span data-ttu-id="f0183-131">De **FirstN** assembly is toegepast, zodat alleen de top 10 waarden, die zijn gebaseerd op het aantalveld.</span><span class="sxs-lookup"><span data-stu-id="f0183-131">The **FirstN** assembly is applied to return only the top 10 values, based on the count field.</span></span>

> [!NOTE]
> <span data-ttu-id="f0183-132">Zie voor meer informatie over het werken met Trident de [Trident-API-overzicht](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.</span><span class="sxs-lookup"><span data-stu-id="f0183-132">For more information on working with Trident, see the [Trident API overview](http://storm.apache.org/releases/current/Trident-API-Overview.html) document.</span></span>

### <a name="the-spout"></a><span data-ttu-id="f0183-133">De spout</span><span class="sxs-lookup"><span data-stu-id="f0183-133">The spout</span></span>

<span data-ttu-id="f0183-134">De spout **TwitterSpout**, maakt gebruik van [Twitter4j](http://twitter4j.org/en/) tweets ophalen uit Twitter.</span><span class="sxs-lookup"><span data-stu-id="f0183-134">The spout, **TwitterSpout**, uses [Twitter4j](http://twitter4j.org/en/) to retrieve tweets from Twitter.</span></span> <span data-ttu-id="f0183-135">Een filter is gemaakt voor de woorden __favoriete__, **muziek**, en **koffie**.</span><span class="sxs-lookup"><span data-stu-id="f0183-135">A filter is created for the words __love__, **music**, and **coffee**.</span></span> <span data-ttu-id="f0183-136">Binnenkomende tweets (status) die overeenkomen met het filter worden opgeslagen in een gekoppelde blokkerende wachtrij.</span><span class="sxs-lookup"><span data-stu-id="f0183-136">Incoming tweets (status) that match the filter are stored in a linked blocking queue.</span></span> <span data-ttu-id="f0183-137">Ten slotte worden artikelen opgehaald uit de wachtrij en verzonden naar de topologie.</span><span class="sxs-lookup"><span data-stu-id="f0183-137">Finally, items are pulled off the queue and emitted to the topology.</span></span>

### <a name="the-hashtagextractor"></a><span data-ttu-id="f0183-138">De HashtagExtractor</span><span class="sxs-lookup"><span data-stu-id="f0183-138">The HashtagExtractor</span></span>

<span data-ttu-id="f0183-139">Uitpakken van het hash-tags [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) voor het ophalen van alle hash-labels die zijn opgenomen in de tweet wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f0183-139">To extract hash tags, [getHashtagEntities](http://twitter4j.org/javadoc/twitter4j/EntitySupport.html#getHashtagEntities--) is used to retrieve all hash tags that are contained in the tweet.</span></span> <span data-ttu-id="f0183-140">Deze worden vervolgens verzonden naar de stroom.</span><span class="sxs-lookup"><span data-stu-id="f0183-140">These are then emitted to the stream.</span></span>

## <a name="configure-twitter"></a><span data-ttu-id="f0183-141">Twitter configureren</span><span class="sxs-lookup"><span data-stu-id="f0183-141">Configure Twitter</span></span>

<span data-ttu-id="f0183-142">Gebruik de volgende stappen een nieuwe Twitter-toepassing registreren en de consumer- en token-informatie nodig voor het lezen van Twitter krijgen:</span><span class="sxs-lookup"><span data-stu-id="f0183-142">Use the following steps to register a new Twitter application and obtain the consumer and access token information needed to read from Twitter:</span></span>

1. <span data-ttu-id="f0183-143">Ga naar [Twitter Apps](https://apps.twitter.com) en klik op de **nieuwe app maken** knop.</span><span class="sxs-lookup"><span data-stu-id="f0183-143">Go to [Twitter Apps](https://apps.twitter.com) and click the **Create new app** button.</span></span> <span data-ttu-id="f0183-144">Bij het invullen in het formulier, laat de **retouraanroep URL** veld leeg.</span><span class="sxs-lookup"><span data-stu-id="f0183-144">When filling in the form, leave the **Callback URL** field empty.</span></span>

2. <span data-ttu-id="f0183-145">Wanneer de app is gemaakt, klikt u op de **sleutels en toegangstokens** tabblad.</span><span class="sxs-lookup"><span data-stu-id="f0183-145">When the app is created, click the **Keys and Access Tokens** tab.</span></span>

3. <span data-ttu-id="f0183-146">Kopieer de **consumentsleutel** en **consumentgeheim** informatie.</span><span class="sxs-lookup"><span data-stu-id="f0183-146">Copy the **Consumer Key** and **Consumer Secret** information.</span></span>

4. <span data-ttu-id="f0183-147">Selecteer aan de onderkant van de pagina **maken van mijn toegangstoken** als er geen tokens bestaan.</span><span class="sxs-lookup"><span data-stu-id="f0183-147">At the bottom of the page, select **Create my access token** if no tokens exist.</span></span> <span data-ttu-id="f0183-148">Wanneer de tokens zijn gemaakt, kopieert de **Access Token** en **Access Token geheim** informatie.</span><span class="sxs-lookup"><span data-stu-id="f0183-148">When the tokens have been created, copy the **Access Token** and **Access Token Secret** information.</span></span>

5. <span data-ttu-id="f0183-149">In de **TwitterSpoutTopology** project dat u eerder hebt gekloond, opent de **resources/twitter4j.properties** bestand, voegt u de informatie die u hebt verzameld in de vorige stappen en sla het bestand.</span><span class="sxs-lookup"><span data-stu-id="f0183-149">In the **TwitterSpoutTopology** project you previously cloned, open the **resources/twitter4j.properties** file, add the information you gathered in the previous steps, and then save the file.</span></span>

## <a name="build-the-topology"></a><span data-ttu-id="f0183-150">De topologie bouwen</span><span class="sxs-lookup"><span data-stu-id="f0183-150">Build the topology</span></span>

<span data-ttu-id="f0183-151">Gebruik de volgende code om het project te bouwen:</span><span class="sxs-lookup"><span data-stu-id="f0183-151">Use the following code to build the project:</span></span>

        cd [directoryname]
        mvn compile

## <a name="test-the-topology"></a><span data-ttu-id="f0183-152">De topologie testen</span><span class="sxs-lookup"><span data-stu-id="f0183-152">Test the topology</span></span>

<span data-ttu-id="f0183-153">Gebruik de volgende opdracht voor het testen van de topologie lokaal:</span><span class="sxs-lookup"><span data-stu-id="f0183-153">Use the following command to test the topology locally:</span></span>

    mvn compile exec:java -Dstorm.topology=com.microsoft.example.TwitterTrendingTopology

<span data-ttu-id="f0183-154">Nadat de topologie wordt gestart, ziet u foutopsporingsinformatie met de hash-tags en telt verzonden door de topologie.</span><span class="sxs-lookup"><span data-stu-id="f0183-154">After the topology starts, you should see debug information that contains the hash tags and counts emitted by the topology.</span></span> <span data-ttu-id="f0183-155">De uitvoer ziet er ongeveer de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="f0183-155">The output should appear similar to the following text:</span></span>

    DEBUG: [Quicktellervalentine, 7]
    DEBUG: [GRAMMYs, 7]
    DEBUG: [AskSam, 7]
    DEBUG: [poppunk, 1]
    DEBUG: [rock, 1]
    DEBUG: [punkrock, 1]
    DEBUG: [band, 1]
    DEBUG: [punk, 1]
    DEBUG: [indonesiapunkrock, 1]

## <a name="next-steps"></a><span data-ttu-id="f0183-156">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="f0183-156">Next steps</span></span>

<span data-ttu-id="f0183-157">Nu dat u de topologie lokaal hebt getest, het implementeren van de topologie detecteren: [implementeren en beheren van Apache Storm-topologieën op HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span><span class="sxs-lookup"><span data-stu-id="f0183-157">Now that you have tested the topology locally, discover how to deploy the topology: [Deploy and manage Apache Storm topologies on HDInsight](hdinsight-storm-deploy-monitor-topology.md).</span></span>

<span data-ttu-id="f0183-158">U is mogelijk ook geïnteresseerd in de volgende onderwerpen voor Storm:</span><span class="sxs-lookup"><span data-stu-id="f0183-158">You may also be interested in the following Storm topics:</span></span>

* [<span data-ttu-id="f0183-159">Java-topologieën ontwikkelen voor Storm op HDInsight met behulp van Maven</span><span class="sxs-lookup"><span data-stu-id="f0183-159">Develop Java topologies for Storm on HDInsight using Maven</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="f0183-160">C#-topologieën ontwikkelen voor Storm op HDInsight met behulp van Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f0183-160">Develop C# topologies for Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)

<span data-ttu-id="f0183-161">Voor meer voorbeelden van Storm voor HDInsight:</span><span class="sxs-lookup"><span data-stu-id="f0183-161">For more Storm examples for HDInsight:</span></span>

* [<span data-ttu-id="f0183-162">Voorbeeldtopologieën van Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="f0183-162">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)

