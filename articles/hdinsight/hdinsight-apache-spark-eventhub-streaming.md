---
title: Apache Spark-streaming met Event Hubs in Azure HDInsight gebruiken | Microsoft Docs
description: Een Apache Spark-streaming-codevoorbeeld voor het verzenden van een gegevensstroom naar Azure Event Hub en vervolgens deze gebeurtenissen ontvangen in HDInsight Spark-cluster met een scala-toepassing bouwen.
keywords: Apache spark-streaming, spark-streaming, spark-voorbeeld, apache spark-streaming bijvoorbeeld event hub azure voorbeeld, spark-voorbeeld
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 68894e75-3ffa-47bd-8982-96cdad38b7d0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 175a2ad70b1f554d05846eb62fb685d4f259af7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="5f649-104">Apache Spark-streaming: procesgegevens uit Azure Event Hubs met Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f649-104">Apache Spark streaming: Process data from Azure Event Hubs with Spark cluster on HDInsight</span></span>

<span data-ttu-id="5f649-105">In dit artikel maakt u een Apache Spark-streaming-voorbeeldtoepassing die u de volgende stappen omvat:</span><span class="sxs-lookup"><span data-stu-id="5f649-105">In this article, you create an Apache Spark streaming sample that involves the following steps:</span></span>

1. <span data-ttu-id="5f649-106">U een zelfstandige toepassing gebruiken om op te nemen van berichten in een Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="5f649-106">You use a standalone application to ingest messages into an Azure Event Hub.</span></span>

2. <span data-ttu-id="5f649-107">Met twee verschillende benaderingen ophalen u de berichten van Event Hub in realtime met behulp van een toepassing die wordt uitgevoerd in Spark-cluster in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5f649-107">With two different approaches, you retrieve the messages from Event Hub in real-time using an application running in Spark cluster on Azure HDInsight.</span></span>

3. <span data-ttu-id="5f649-108">U streaming analytische pijplijnen om te blijven behouden van gegevens naar andere opslagsystemen bouwen of inzichten verkrijgen van gegevens op elk gewenst moment.</span><span class="sxs-lookup"><span data-stu-id="5f649-108">You build streaming analytic pipelines to persist data to different storage systems, or get insights from data on the fly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f649-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="5f649-109">Prerequisites</span></span>

* <span data-ttu-id="5f649-110">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="5f649-110">An Azure subscription.</span></span> <span data-ttu-id="5f649-111">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="5f649-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="5f649-112">Een Apache Spark-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5f649-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="5f649-113">Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="5f649-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="spark-streaming-concepts"></a><span data-ttu-id="5f649-114">Concepten Spark-Streaming</span><span class="sxs-lookup"><span data-stu-id="5f649-114">Spark Streaming concepts</span></span>

<span data-ttu-id="5f649-115">Zie voor een gedetailleerde uitleg van Spark-streaming [Apache Spark-streaming-overzicht](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span><span class="sxs-lookup"><span data-stu-id="5f649-115">For a detailed explanation of Spark streaming, see [Apache Spark streaming overview](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span></span> <span data-ttu-id="5f649-116">HDInsight biedt dezelfde streaming functies voor een Spark-cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="5f649-116">HDInsight brings the same streaming features to a Spark cluster on Azure.</span></span>  

## <a name="what-does-this-solution-do"></a><span data-ttu-id="5f649-117">Wat doet deze oplossing?</span><span class="sxs-lookup"><span data-stu-id="5f649-117">What does this solution do?</span></span>

<span data-ttu-id="5f649-118">In dit artikel voor het maken van een Spark-streaming-voorbeeld, de volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5f649-118">In this article, to create a Spark streaming example, perform the following steps:</span></span>

1. <span data-ttu-id="5f649-119">Maak een Azure Event Hub die u een stream van gebeurtenissen ontvangt.</span><span class="sxs-lookup"><span data-stu-id="5f649-119">Create an Azure Event Hub that will receive a stream of events.</span></span>

2. <span data-ttu-id="5f649-120">Voer een lokale zelfstandige toepassing die wordt gegenereerd gebeurtenissen en stuurt deze naar de Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="5f649-120">Run a local standalone application that generates events and pushes it to the Azure Event Hub.</span></span> <span data-ttu-id="5f649-121">De voorbeeldtoepassing waarmee dit wordt gepubliceerd op [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="5f649-121">The sample application that does this is published at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span>

3. <span data-ttu-id="5f649-122">Een streaming-toepassing op afstand uitvoeren op een Spark-cluster die streaming-gebeurtenissen van Azure Event Hub leest en analyse van de verschillende gegevensverwerking /.</span><span class="sxs-lookup"><span data-stu-id="5f649-122">Run a streaming application remotely on a Spark cluster that reads streaming events from Azure Event Hub and perform various data processing/analysis.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="5f649-123">Een Azure Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="5f649-123">Create an Azure Event Hub</span></span>

1. <span data-ttu-id="5f649-124">Meld u aan bij de [Azure Portal](https://ms.portal.azure.com), en klik op **nieuw** op linksboven op het scherm.</span><span class="sxs-lookup"><span data-stu-id="5f649-124">Log on to the [Azure Portal](https://ms.portal.azure.com), and click **New** at the top left of the screen.</span></span>

2. <span data-ttu-id="5f649-125">Klik op **Internet van dingen** en vervolgens op **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="5f649-125">Click **Internet of Things**, then click **Event Hubs**.</span></span>

    <span data-ttu-id="5f649-126">![Create event hub voor Spark-streaming-voorbeeld](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "maken event hub voor Spark-streaming-voorbeeld")</span><span class="sxs-lookup"><span data-stu-id="5f649-126">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Create event hub for Spark streaming example")</span></span>

3. <span data-ttu-id="5f649-127">Voer op de blade **Naamruimte maken** een naam in voor de naamruimte.</span><span class="sxs-lookup"><span data-stu-id="5f649-127">In the **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="5f649-128">Kies de prijscategorie (basis of standaard).</span><span class="sxs-lookup"><span data-stu-id="5f649-128">choose the pricing tier (Basic or Standard).</span></span> <span data-ttu-id="5f649-129">Kies ook een Azure-abonnement, resourcegroep en locatie voor het maken van de resource.</span><span class="sxs-lookup"><span data-stu-id="5f649-129">Also, choose an Azure subscription, resource group, and location in which to create the resource.</span></span> <span data-ttu-id="5f649-130">Klik op **Maken** om de naamruimte te maken.</span><span class="sxs-lookup"><span data-stu-id="5f649-130">Click **Create** to create the namespace.</span></span>

      <span data-ttu-id="5f649-131">![Geef de naam van een event hub voor Spark-streaming-voorbeeld](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "bieden u de naam van een event hub voor Spark-streaming-voorbeeld")</span><span class="sxs-lookup"><span data-stu-id="5f649-131">![Provide an event hub name for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Provide an event hub name for Spark streaming example")</span></span>

    > [!NOTE]
    > <span data-ttu-id="5f649-132">Moet u dezelfde **locatie** als uw cluster Apache Spark in HDInsight om latentie en kosten te verminderen.</span><span class="sxs-lookup"><span data-stu-id="5f649-132">You should select the same **Location** as your Apache Spark cluster in HDInsight to reduce latency and costs.</span></span>
    >
    >

4. <span data-ttu-id="5f649-133">Klik in de lijst met naamruimten van Event Hubs op de zojuist gemaakte naamruimte.</span><span class="sxs-lookup"><span data-stu-id="5f649-133">In the Event Hubs namespace list, click the newly-created namespace.</span></span>      


5. <span data-ttu-id="5f649-134">Klik op de blade naamruimte **Event Hubs**, en klik vervolgens op **+ Event Hub** voor het maken van nieuwe Event Hub.</span><span class="sxs-lookup"><span data-stu-id="5f649-134">In the namespace blade, click **Event Hubs**, and then click **+ Event Hub** to create a new Event Hub.</span></span>
   
    <span data-ttu-id="5f649-135">![Create event hub voor Spark-streaming-voorbeeld](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "maken event hub voor Spark-streaming-voorbeeld")</span><span class="sxs-lookup"><span data-stu-id="5f649-135">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Create event hub for Spark streaming example")</span></span>

6. <span data-ttu-id="5f649-136">Typ een naam voor uw Event Hub, stelt u het aantal partities op 10, en het bericht bewaren op 1.</span><span class="sxs-lookup"><span data-stu-id="5f649-136">Type a name for your Event Hub, set the partition count to 10, and message retention to 1.</span></span> <span data-ttu-id="5f649-137">We zijn de berichten in deze oplossing niet archiveren zodat u kunt de rest als standaard laat en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="5f649-137">We are not archiving the messages in this solution so you can leave the rest as default, and then click **Create**.</span></span>
   
    <span data-ttu-id="5f649-138">![Geef details van gebeurtenis hub voor Spark-streaming-voorbeeld](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "event hub-informatie opgeven voor Spark-streaming-voorbeeld")</span><span class="sxs-lookup"><span data-stu-id="5f649-138">![Provide event hub details for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Provide event hub details for Spark streaming example")</span></span>

7. <span data-ttu-id="5f649-139">De zojuist gemaakte Event Hub wordt vermeld in de Event Hub-blade.</span><span class="sxs-lookup"><span data-stu-id="5f649-139">The newly created Event Hub is listed in the Event Hub blade.</span></span>
    
     <span data-ttu-id="5f649-140">![Event Hub voor de Spark-streaming-voorbeeld weergeven](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "weergave Event Hub voor de Spark-streaming-voorbeeld")</span><span class="sxs-lookup"><span data-stu-id="5f649-140">![View Event Hub for the Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "View Event Hub for the Spark streaming example")</span></span>

8. <span data-ttu-id="5f649-141">Klik op de blade Naamruimte (niet de specifieke Event Hub-blade) op **Gedeeld toegangsbeleid** en klik vervolgens op **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="5f649-141">Back in the namespace blade (not the specific Event Hub blade), click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
     <span data-ttu-id="5f649-142">![Event Hub-beleid instellen voor de Spark-streaming-voorbeeld](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Event Hub ingesteld beleid voor het Spark-streaming-voorbeeld")</span><span class="sxs-lookup"><span data-stu-id="5f649-142">![Set Event Hub policies for the Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Set Event Hub policies for the Spark streaming example")</span></span>

9. <span data-ttu-id="5f649-143">Klik op de knop kopiëren kopieert de **RootManageSharedAccessKey** primaire sleutel en de verbindingsreeks naar het Klembord.</span><span class="sxs-lookup"><span data-stu-id="5f649-143">Click the copy button to copy the **RootManageSharedAccessKey** primary key and connection string to the clipboard.</span></span> <span data-ttu-id="5f649-144">Sla deze voor gebruik verderop in de zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="5f649-144">Save these to use later in the tutorial.</span></span>
    
     <span data-ttu-id="5f649-145">![Event Hub beleid sleutels voor de Spark-streaming-voorbeeld weergeven](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "weergave Event Hub beleid sleutels voor het voorbeeld van Spark-streaming")</span><span class="sxs-lookup"><span data-stu-id="5f649-145">![View Event Hub policy keys for the Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "View Event Hub policy keys for the Spark streaming example")</span></span>

## <a name="send-messages-to-azure-event-hub-using-a-sample-scala-application"></a><span data-ttu-id="5f649-146">Berichten verzenden naar Azure Event Hub met behulp van een voorbeeldtoepassing Scala</span><span class="sxs-lookup"><span data-stu-id="5f649-146">Send messages to Azure Event Hub using a sample Scala application</span></span>

<span data-ttu-id="5f649-147">In deze sectie gebruikt u een zelfstandige lokale Scala toepassing die een stream van gebeurtenissen wordt gegenereerd en verzonden naar Azure Event Hub die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f649-147">In this section you use a standalone local Scala application that generates a stream of events and sends it to Azure Event Hub that you created earlier.</span></span> <span data-ttu-id="5f649-148">Deze toepassing is beschikbaar op GitHub op [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span><span class="sxs-lookup"><span data-stu-id="5f649-148">This application is available on GitHub at [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span></span> <span data-ttu-id="5f649-149">De stappen die hier wordt ervan uitgegaan dat u al deze GitHub-opslagplaats hebben forked.</span><span class="sxs-lookup"><span data-stu-id="5f649-149">The steps here assume that you have already forked this GitHub repository.</span></span>

1. <span data-ttu-id="5f649-150">Zorg ervoor dat u hebt het volgende zijn geïnstalleerd op de computer waarop u deze toepassing uitvoert.</span><span class="sxs-lookup"><span data-stu-id="5f649-150">Make sure you have the following installed on the computer where you run this application.</span></span>

    * <span data-ttu-id="5f649-151">Oracle Java Development kit.</span><span class="sxs-lookup"><span data-stu-id="5f649-151">Oracle Java Development kit.</span></span> <span data-ttu-id="5f649-152">Kunt u het installeren van [hier](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="5f649-152">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
    * <span data-ttu-id="5f649-153">Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="5f649-153">Apache Maven.</span></span> <span data-ttu-id="5f649-154">U kunt downloaden van [hier](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="5f649-154">You can download it from [here](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="5f649-155">Vindt u instructies voor het installeren van Maven [hier](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="5f649-155">Instructions to install Maven are available [here](https://maven.apache.org/install.html).</span></span>

2. <span data-ttu-id="5f649-156">Open een opdrachtprompt en navigeer naar de locatie die wordt gekloond van de GitHub-repo voor de voorbeeldtoepassing Scala en voer de volgende opdracht om de toepassing te maken.</span><span class="sxs-lookup"><span data-stu-id="5f649-156">Open a command prompt and navigate to the location you cloned the GitHub repo for the sample Scala application and run the following command to build the application.</span></span>

        mvn package

3. <span data-ttu-id="5f649-157">De jar uitvoer voor de toepassing **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, wordt gemaakt onder **/target** directory.</span><span class="sxs-lookup"><span data-stu-id="5f649-157">The output jar for the application, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, is created under **/target** directory.</span></span> <span data-ttu-id="5f649-158">U kunt deze JAR verderop in dit artikel gebruiken voor het testen van de volledige oplossing.</span><span class="sxs-lookup"><span data-stu-id="5f649-158">You use this JAR later in this article to test the complete solution.</span></span>

## <a name="create-application-to-receive-messages-from-event-hub-into-a-spark-cluster"></a><span data-ttu-id="5f649-159">De toepassing om berichten te ontvangen van Event Hub in een Spark-cluster maken</span><span class="sxs-lookup"><span data-stu-id="5f649-159">Create application to receive messages from Event Hub into a Spark cluster</span></span> 

<span data-ttu-id="5f649-160">Er zijn twee benaderingen Spark-Streaming en Azure Event Hubs, verbinding op basis van de ontvanger en Direct-DStream-verbinding tot stand brengen.</span><span class="sxs-lookup"><span data-stu-id="5f649-160">We have two approaches to connect Spark Streaming and Azure Event Hubs, Receiver-based connection and Direct-DStream-based connection.</span></span> <span data-ttu-id="5f649-161">Direct DStream gebaseerd op januari 2017 is geïntroduceerd in de 2.0.3 release.</span><span class="sxs-lookup"><span data-stu-id="5f649-161">Direct-DStream-based is introduced on Jan of 2017, in the 2.0.3 release.</span></span> <span data-ttu-id="5f649-162">Het is veronderstelde ter vervanging van de oorspronkelijke verbinding op basis van een ontvanger, omdat deze meer zodat en resource-efficiënt.</span><span class="sxs-lookup"><span data-stu-id="5f649-162">It is supposed to replace the original receiver-based connection as it is more performant and resource-efficient.</span></span> <span data-ttu-id="5f649-163">Meer details te vinden in [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span><span class="sxs-lookup"><span data-stu-id="5f649-163">More details found in [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span></span> <span data-ttu-id="5f649-164">Directe DStream ondersteunt alleen Spark 2.0 +.</span><span class="sxs-lookup"><span data-stu-id="5f649-164">Direct DStream only supports Spark 2.0+.</span></span>

### <a name="build-applications-with-the-dependency-to-spark-eventhubs-connector"></a><span data-ttu-id="5f649-165">Toepassingen met de afhankelijkheid met spark-eventhubs-connector maken</span><span class="sxs-lookup"><span data-stu-id="5f649-165">Build applications with the dependency to spark-eventhubs connector</span></span>

<span data-ttu-id="5f649-166">Er wordt ook de staging-versie van Spark-EventHubs publiceren in GitHub.</span><span class="sxs-lookup"><span data-stu-id="5f649-166">We will also publish the staging version of Spark-EventHubs in GitHub.</span></span> <span data-ttu-id="5f649-167">Voor het gebruik van de staging-versie van Spark-EventHubs, wordt de eerste stap is om aan te geven van GitHub als de bron-opslagplaats met het toevoegen van de volgende vermelding aan pom.xml:</span><span class="sxs-lookup"><span data-stu-id="5f649-167">To use the staging version of Spark-EventHubs, the first step is to indicate GitHub as the source repo by adding the following entry to pom.xml:</span></span>

```xml
<repository>
      <id>spark-eventhubs</id>
      <url>https://raw.github.com/hdinsight/spark-eventhubs/maven-repo/</url>
      <snapshots>
        <enabled>true</enabled>
        <updatePolicy>always</updatePolicy>
      </snapshots>
</repository>
```

<span data-ttu-id="5f649-168">Vervolgens kunt u de volgende afhankelijkheden toevoegen aan uw project te laten de prerelease-versie.</span><span class="sxs-lookup"><span data-stu-id="5f649-168">You can then add the following dependency to your project to take the pre-released version.</span></span>

<span data-ttu-id="5f649-169">Maven-afhankelijkheid</span><span class="sxs-lookup"><span data-stu-id="5f649-169">Maven Dependency</span></span>

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

<span data-ttu-id="5f649-170">SBT afhankelijkheid</span><span class="sxs-lookup"><span data-stu-id="5f649-170">SBT Dependency</span></span>

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a><span data-ttu-id="5f649-171">Rechtstreekse verbinding DStream</span><span class="sxs-lookup"><span data-stu-id="5f649-171">Direct DStream Connection</span></span>

<span data-ttu-id="5f649-172">Een vooraf samengestelde jar-bestand met voorbeelden met directe DStream kan worden gedownload [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span><span class="sxs-lookup"><span data-stu-id="5f649-172">A pre-built jar file containing examples using Direct DStream can be downloaded in [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span></span>

<span data-ttu-id="5f649-173">Het jar-bestand bevat drie voorbeelden waarvan de broncode zijn beschikbaar op [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span><span class="sxs-lookup"><span data-stu-id="5f649-173">The jar file contains three examples whose source code are available at [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span></span>

<span data-ttu-id="5f649-174">Duurt [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) als een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="5f649-174">Taking [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) as an example:</span></span>

```scala
private def createStreamingContext(
  sparkCheckpointDir: String,
  batchDuration: Int,
  namespace: String,
  eventHunName: String,
  eventhubParams: Map[String, String],
  progressDir: String) = {
val ssc = new StreamingContext(new SparkContext(), Seconds(batchDuration))
ssc.checkpoint(sparkCheckpointDir)
val inputDirectStream = EventHubsUtils.createDirectStreams(
  ssc,
  namespace,
  progressDir,
  Map(eventHunName -> eventhubParams))

inputDirectStream.map(receivedRecord => (new String(receivedRecord.getBody), 1)).
  reduceByKeyAndWindow((v1, v2) => v1 + v2, (v1, v2) => v1 - v2, Seconds(batchDuration * 3),
    Seconds(batchDuration)).print()

ssc
}

def main(args: Array[String]): Unit = {

if (args.length != 8) {
  println("Usage: program progressDir PolicyName PolicyKey EventHubNamespace EventHubName" +
    " BatchDuration(seconds) Spark_Checkpoint_Directory maxRate")
  sys.exit(1)
}

val progressDir = args(0)
val policyName = args(1)
val policykey = args(2)
val namespace = args(3)
val name = args(4)
val batchDuration = args(5).toInt
val sparkCheckpointDir = args(6)
val maxRate = args(7)

val eventhubParameters = Map[String, String] (
  "eventhubs.policyname" -> policyName,
  "eventhubs.policykey" -> policykey,
  "eventhubs.namespace" -> namespace,
  "eventhubs.name" -> name,
  "eventhubs.partition.count" -> "32",
  "eventhubs.consumergroup" -> "$Default",
  "eventhubs.maxRate" -> s"$maxRate"
)

val ssc = StreamingContext.getOrCreate(sparkCheckpointDir,
  () => createStreamingContext(sparkCheckpointDir, batchDuration, namespace, name,
    eventhubParameters, progressDir))

ssc.start()
ssc.awaitTermination()
}
```

<span data-ttu-id="5f649-175">In het bovenstaande voorbeeld `eventhubParameters` zijn van de parameters die specifiek zijn voor één EventHubs-exemplaar en er moet worden doorgegeven aan de `createDirectStreams` API die wordt gemaakt van een directe DStream objecttoewijzing aan een naamruimte Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="5f649-175">In the above example, `eventhubParameters` are the parameters specific to a single EventHubs instance and you have to pass it to the `createDirectStreams` API which constructs a Direct DStream object mapping to a Event Hubs namespace.</span></span> <span data-ttu-id="5f649-176">U kunt via het object Direct DStream DStream API's die door Spark-Streaming API framework aanroepen.</span><span class="sxs-lookup"><span data-stu-id="5f649-176">Over the Direct DStream object, you can call any DStream API provided by Spark Streaming API framework.</span></span> <span data-ttu-id="5f649-177">In dit voorbeeld berekenen we de frequentie van elk woord in de afgelopen 3 micro batch intervallen.</span><span class="sxs-lookup"><span data-stu-id="5f649-177">In this example, we calculate the frequency of each word within the last 3 micro batch intervals.</span></span>

### <a name="receiver-based-connection"></a><span data-ttu-id="5f649-178">Verbinding op basis van een ontvanger</span><span class="sxs-lookup"><span data-stu-id="5f649-178">Receiver-based Connection</span></span>

<span data-ttu-id="5f649-179">Een Spark-streaming-voorbeeldtoepassing die zijn geschreven in Scala die gebeurtenissen ontvangt en de aan verschillende bestemmingen routeren, is beschikbaar op [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="5f649-179">A Spark streaming example application written in Scala, which receives events and route the to different destinations, is available at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span> <span data-ttu-id="5f649-180">Volg onderstaande stappen voor het bijwerken van de toepassing voor de configuratie van uw Event Hub en de uitvoer jar maken.</span><span class="sxs-lookup"><span data-stu-id="5f649-180">Follow the steps below to update the application for your Event Hub configuration and create the output jar.</span></span>

1. <span data-ttu-id="5f649-181">IntelliJ IDEA Start en selecteer in het startscherm **uitchecken uit versiebeheer** en klik vervolgens op **Git**.</span><span class="sxs-lookup"><span data-stu-id="5f649-181">Launch IntelliJ IDEA and from the launch screen select **Check out from Version Control** and then click **Git**.</span></span>
   
    <span data-ttu-id="5f649-182">![Apache Spark-streaming-voorbeeld - get-bronnen van Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark-streaming-voorbeeld - get-bronnen van Git")</span><span class="sxs-lookup"><span data-stu-id="5f649-182">![Apache Spark streaming example - get sources from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark streaming example - get sources from Git")</span></span>

2. <span data-ttu-id="5f649-183">In de **kloon opslagplaats** dialoogvenster Geef de URL naar de Git-opslagplaats voor klonen uit, geeft u de map te klonen en klikt u op **kloon**.</span><span class="sxs-lookup"><span data-stu-id="5f649-183">In the **Clone Repository** dialog box, provide the URL to the Git repository to clone from, specify the directory to clone to, and then click **Clone**.</span></span>
   
    <span data-ttu-id="5f649-184">![Apache Spark-streaming-voorbeeld - kloon van Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark-streaming-voorbeeld - kloon van Git")</span><span class="sxs-lookup"><span data-stu-id="5f649-184">![Apache Spark streaming example - clone from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark streaming example - clone from Git")</span></span>
3. <span data-ttu-id="5f649-185">Volg de aanwijzingen tot het project volledig is gekloond.</span><span class="sxs-lookup"><span data-stu-id="5f649-185">Follow the prompts till the project is completely cloned.</span></span> <span data-ttu-id="5f649-186">Druk op **Alt + 1** openen de **Project-weergave**.</span><span class="sxs-lookup"><span data-stu-id="5f649-186">Press **Alt + 1** to open the **Project View**.</span></span> <span data-ttu-id="5f649-187">Het bestand is vergelijkbaar met het volgende.</span><span class="sxs-lookup"><span data-stu-id="5f649-187">It should resemble the following.</span></span>
   
    <span data-ttu-id="5f649-188">![Apache Spark-streaming-voorbeeld - Project-weergave](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark-streaming-voorbeeld - Project-weergave")</span><span class="sxs-lookup"><span data-stu-id="5f649-188">![Apache Spark streaming example - Project View](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark streaming example - Project View")</span></span>
4. <span data-ttu-id="5f649-189">Zorg ervoor dat de toepassingscode is gecompileerd met Java8.</span><span class="sxs-lookup"><span data-stu-id="5f649-189">Make sure the application code is compiled with Java8.</span></span> <span data-ttu-id="5f649-190">Om te controleren of dit, klikt u op **bestand**, klikt u op **projectstructuur**, en klik op de **Project** tabblad, zorg ervoor dat Project taal is ingesteld op **8 - lambda's type aantekeningen, enz.**.</span><span class="sxs-lookup"><span data-stu-id="5f649-190">To ensure this, click **File**, click **Project Structure**, and on the **Project** tab, make sure Project language level is set to **8 - Lambdas, type annotations, etc.**.</span></span>
   
    <span data-ttu-id="5f649-191">![Apache Spark-streaming-voorbeeld - Set compiler](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark-streaming-voorbeeld: Set-compiler")</span><span class="sxs-lookup"><span data-stu-id="5f649-191">![Apache Spark streaming example - Set compiler](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark streaming example - Set compiler")</span></span>
5. <span data-ttu-id="5f649-192">Open de **pom.xml** en zorg ervoor dat de versie Spark juist is.</span><span class="sxs-lookup"><span data-stu-id="5f649-192">Open the **pom.xml** and make sure the Spark version is correct.</span></span> <span data-ttu-id="5f649-193">Onder `<properties>` knooppunt, zoekt u naar het volgende fragment en controleer of de versie van Spark.</span><span class="sxs-lookup"><span data-stu-id="5f649-193">Under `<properties>` node, look for the following snippet and verify the Spark version.</span></span>

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. <span data-ttu-id="5f649-194">De toepassing vereist een afhankelijkheid jar aangeroepen **JDBC-stuurprogramma jar**.</span><span class="sxs-lookup"><span data-stu-id="5f649-194">The application requires a dependency jar called **JDBC driver jar**.</span></span> <span data-ttu-id="5f649-195">Dit is vereist voor de berichten ontvangen van de Event Hub naar een Azure SQL database schrijven.</span><span class="sxs-lookup"><span data-stu-id="5f649-195">This is required to write the messages received from Event Hub into an Azure SQL database.</span></span> <span data-ttu-id="5f649-196">U kunt deze jar downloaden (v4.1 of hoger) van [hier](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span><span class="sxs-lookup"><span data-stu-id="5f649-196">You can download this jar (v4.1 or later) from [here](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span></span> <span data-ttu-id="5f649-197">Verwijzing naar deze jar toevoegen in de project-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="5f649-197">Add reference to this jar in the project library.</span></span> <span data-ttu-id="5f649-198">De volgende stappen uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5f649-198">Perform the following steps:</span></span>
     
     1. <span data-ttu-id="5f649-199">Vanuit IntelliJ IDEA venster waarin het hebben van de toepassing openen, klikt u op **bestand**, klikt u op **projectstructuur**, en klik vervolgens op **bibliotheken**.</span><span class="sxs-lookup"><span data-stu-id="5f649-199">From IntelliJ IDEA window where you have the application open, click **File**, click **Project Structure**, and then click **Libraries**.</span></span> 
     2. <span data-ttu-id="5f649-200">Klik op het pictogram toevoegen (![pictogram toevoegen](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), klikt u op **Java**, en navigeer vervolgens naar de locatie waar u de jar JDBC-stuurprogramma gedownload.</span><span class="sxs-lookup"><span data-stu-id="5f649-200">Click the add icon (![add icon](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), click **Java**, and then navigate to the location where you downloaded the JDBC driver jar.</span></span> <span data-ttu-id="5f649-201">Volg de aanwijzingen voor het jar-bestand toevoegen aan de project-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="5f649-201">Follow the prompts to add the jar file to the project library.</span></span>

         <span data-ttu-id="5f649-202">![ontbrekende afhankelijkheden toevoegen](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "ontbrekende afhankelijkheid potten toevoegen")</span><span class="sxs-lookup"><span data-stu-id="5f649-202">![add missing dependencies](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Add missing dependency jars")</span></span>
     3. <span data-ttu-id="5f649-203">Klik op **Toepassen**.</span><span class="sxs-lookup"><span data-stu-id="5f649-203">Click **Apply**.</span></span>

7. <span data-ttu-id="5f649-204">Maak de jar-bestand voor uitvoer.</span><span class="sxs-lookup"><span data-stu-id="5f649-204">Create the output jar file.</span></span> <span data-ttu-id="5f649-205">De volgende stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5f649-205">Perform the following steps.</span></span>

   1. <span data-ttu-id="5f649-206">In de **projectstructuur** in het dialoogvenster, klikt u op **artefacten** en klik vervolgens op het plusteken.</span><span class="sxs-lookup"><span data-stu-id="5f649-206">In the **Project Structure** dialog box, click **Artifacts** and then click the plus symbol.</span></span> <span data-ttu-id="5f649-207">Klik in het pop-updialoogvenster op **JAR**, en klik vervolgens op **van modules met afhankelijkheden**.</span><span class="sxs-lookup"><span data-stu-id="5f649-207">From the pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>      
       
       <span data-ttu-id="5f649-208">![Apache Spark streaming voorbeeld - JAR maken](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "streaming voorbeeld Apache Spark - JAR maken")</span><span class="sxs-lookup"><span data-stu-id="5f649-208">![Apache Spark streaming example - create JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark streaming example - create JAR")</span></span>
   2. <span data-ttu-id="5f649-209">In de **maken JAR van Modules** dialoogvenster vak, klikt u op het weglatingsteken (![weglatingsteken](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) op basis van de **Main klasse**.</span><span class="sxs-lookup"><span data-stu-id="5f649-209">In the **Create JAR from Modules** dialog box, click the ellipsis (![ellipsis](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) against the **Main Class**.</span></span>
   3. <span data-ttu-id="5f649-210">In de **Main-klasse selecteren** dialoogvenster vak, selecteert u een van de beschikbare klassen en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="5f649-210">In the **Select Main Class** dialog box, select any of the available classes and then click **OK**.</span></span>
      
       <span data-ttu-id="5f649-211">![Apache Spark-streaming-voorbeeld - Selecteer klasse voor jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark-streaming-voorbeeld - Selecteer klasse voor jar")</span><span class="sxs-lookup"><span data-stu-id="5f649-211">![Apache Spark streaming example - select class for jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark streaming example - select class for jar")</span></span>
   4. <span data-ttu-id="5f649-212">In de **maken JAR van Modules** dialoogvenster vak, zorg ervoor dat de optie voor het **uitpakken naar het doel JAR** is geselecteerd en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="5f649-212">In the **Create JAR from Modules** dialog box, make sure that the option to **extract to the target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="5f649-213">Hiermee maakt u een één JAR met alle afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="5f649-213">This creates a single JAR with all dependencies.</span></span>
      
       <span data-ttu-id="5f649-214">![Apache Spark streaming voorbeeld - jar maken van modules](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "streaming voorbeeld Apache Spark - jar van modules maken")</span><span class="sxs-lookup"><span data-stu-id="5f649-214">![Apache Spark streaming example - create jar from modules](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark streaming example - create jar from modules")</span></span>
   5. <span data-ttu-id="5f649-215">De **uitvoer indeling** tabblad bevat alle potten die opgenomen als onderdeel van het Maven-project zijn.</span><span class="sxs-lookup"><span data-stu-id="5f649-215">The **Output Layout** tab lists all the jars that are included as part of the Maven project.</span></span> <span data-ttu-id="5f649-216">U kunt selecteren en het verwijderen van ongewenste waarop de toepassing Scala heeft geen directe afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="5f649-216">You can select and delete the ones on which the Scala application has no direct dependency.</span></span> <span data-ttu-id="5f649-217">Voor de toepassing hier maakt, kunt u alles behalve het laatste bestand (**spark-streaming-gegevens-persistentie-voorbeelden gecompileerd uitvoer**).</span><span class="sxs-lookup"><span data-stu-id="5f649-217">For the application we are creating here, you can remove all but the last one (**spark-streaming-data-persistence-examples compile output**).</span></span> <span data-ttu-id="5f649-218">Selecteer de potten om te verwijderen en klik vervolgens op de **verwijderen** pictogram (![pictogram verwijderen](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span><span class="sxs-lookup"><span data-stu-id="5f649-218">Select the jars to delete and then click the **Delete** icon (![delete icon](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span></span>
      
       <span data-ttu-id="5f649-219">![Apache Spark-streaming-voorbeeld - delete uitgepakt potten](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark-streaming-voorbeeld - potten uitgepakt verwijderen")</span><span class="sxs-lookup"><span data-stu-id="5f649-219">![Apache Spark streaming example - delete extracted jars](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark streaming example - delete extracted jars")</span></span>
      
       <span data-ttu-id="5f649-220">Zorg ervoor dat **bouwen op Controleer** selectievakje is ingeschakeld, die zorgt ervoor dat de jar wordt gemaakt telkens wanneer het project wordt gemaakt of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="5f649-220">Make sure **Build on make** box is selected, which ensures that the jar is created every time the project is built or updated.</span></span> <span data-ttu-id="5f649-221">Klik op **Toepassen**.</span><span class="sxs-lookup"><span data-stu-id="5f649-221">Click **Apply**.</span></span>
   6. <span data-ttu-id="5f649-222">In de **uitvoer indeling** tabblad direct aan de onderkant van de **beschikbare elementen** vak hebt u de SQL JDBC jar die u eerder hebt toegevoegd aan de project-bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="5f649-222">In the **Output Layout** tab, right at the bottom of the **Available Elements** box, you have the SQL JDBC jar that you added earlier to the project library.</span></span> <span data-ttu-id="5f649-223">U moet deze optie om te toevoegen de **uitvoer indeling** tabblad. Met de rechtermuisknop op het jar-bestand en klik vervolgens op **uitpakken naar uitvoer hoofdmap**.</span><span class="sxs-lookup"><span data-stu-id="5f649-223">You must add this to the **Output Layout** tab. Right-click the jar file, and then click **Extract Into Output Root**.</span></span>
      
       <span data-ttu-id="5f649-224">![Apache Spark-streaming-voorbeeld - extract afhankelijkheid jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark-streaming-voorbeeld - extract afhankelijkheid jar")</span><span class="sxs-lookup"><span data-stu-id="5f649-224">![Apache Spark streaming example - extract dependency jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark streaming example - extract dependency jar")</span></span>  
      
       <span data-ttu-id="5f649-225">De **uitvoer indeling** tabblad ziet er nu als volgt.</span><span class="sxs-lookup"><span data-stu-id="5f649-225">The **Output Layout** tab should now look like this.</span></span>
      
       <span data-ttu-id="5f649-226">![Apache Spark-streaming-voorbeeld - uiteindelijke uitvoer tabblad](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark-streaming-voorbeeld - tabblad uiteindelijke uitvoer")</span><span class="sxs-lookup"><span data-stu-id="5f649-226">![Apache Spark streaming example - final output tab](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark streaming example - final output tab")</span></span>        
      
       <span data-ttu-id="5f649-227">In de **projectstructuur** in het dialoogvenster, klikt u op **toepassen** en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="5f649-227">In the **Project Structure** dialog box, click **Apply** and then click **OK**.</span></span>    
   7. <span data-ttu-id="5f649-228">Klik in de menubalk op **bouwen**, en klik vervolgens op **Project maken**.</span><span class="sxs-lookup"><span data-stu-id="5f649-228">From the menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="5f649-229">U kunt ook klikken op **bouwen artefacten** voor het maken van de jar.</span><span class="sxs-lookup"><span data-stu-id="5f649-229">You can also click **Build Artifacts** to create the jar.</span></span> <span data-ttu-id="5f649-230">De uitvoer jar wordt gemaakt onder **\classes\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="5f649-230">The output jar is created under **\classes\artifacts**.</span></span>
      
       <span data-ttu-id="5f649-231">![Apache Spark streaming voorbeeld - uitvoer JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "streaming voorbeeld Apache Spark - uitvoer JAR")</span><span class="sxs-lookup"><span data-stu-id="5f649-231">![Apache Spark streaming example - output JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark streaming example - output JAR")</span></span>

## <a name="run-the-application-remotely-on-a-spark-cluster-using-livy"></a><span data-ttu-id="5f649-232">De toepassing op afstand uitvoeren op een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="5f649-232">Run the application remotely on a Spark cluster using Livy</span></span>

<span data-ttu-id="5f649-233">In dit artikel kunt u hier de Apache Spark-streaming van toepassing op afstand op een Spark-cluster worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5f649-233">In this article you use Livy to run the Apache Spark streaming application remotely on a Spark cluster.</span></span> <span data-ttu-id="5f649-234">Zie voor gedetailleerde informatie over het gebruik van Livy met HDInsight Spark-cluster [taken verzenden met een Apache Spark in Azure HDInsight-cluster](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="5f649-234">For detailed discussion on how to use Livy with HDInsight Spark cluster, see [Submit jobs remotely to an Apache Spark cluster on Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span> <span data-ttu-id="5f649-235">Voordat u kunt de Spark-streaming-toepassing wordt uitgevoerd, zijn er zijn een aantal dingen die u moet doen:</span><span class="sxs-lookup"><span data-stu-id="5f649-235">Before you can start running the Spark streaming application, there are a couple of things you should do:</span></span>

1. <span data-ttu-id="5f649-236">Start de lokale zelfstandige toepassing gebeurtenissen genereren en verzonden naar de Event Hub.</span><span class="sxs-lookup"><span data-stu-id="5f649-236">Start the local standalone application to generate events and sent to Event Hub.</span></span> <span data-ttu-id="5f649-237">Gebruik de volgende opdracht om dit te doen:</span><span class="sxs-lookup"><span data-stu-id="5f649-237">Use the following command to do so:</span></span>

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. <span data-ttu-id="5f649-238">Kopieer de jar streaming (**spark-streaming-gegevens-persistentie-examples.jar**) naar de Azure Blob-opslag die is gekoppeld aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="5f649-238">Copy the streaming jar (**spark-streaming-data-persistence-examples.jar**) to the Azure Blob storage associated with the cluster.</span></span> <span data-ttu-id="5f649-239">Dit maakt de jar toegankelijk is voor Livy.</span><span class="sxs-lookup"><span data-stu-id="5f649-239">This makes the jar accessible to Livy.</span></span> <span data-ttu-id="5f649-240">U kunt [ **AzCopy**](../storage/common/storage-use-azcopy.md), een opdrachtregelprogramma, om dit te doen.</span><span class="sxs-lookup"><span data-stu-id="5f649-240">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, to do so.</span></span> <span data-ttu-id="5f649-241">Er zijn veel andere clients die u kunt gebruiken om gegevens te uploaden.</span><span class="sxs-lookup"><span data-stu-id="5f649-241">There are a lot of other clients you can use to upload data.</span></span> <span data-ttu-id="5f649-242">U vindt meer informatie hierover op [gegevens voor Hadoop-taken in HDInsight uploaden](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="5f649-242">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
3. <span data-ttu-id="5f649-243">CURL installeren op de computer waarop u deze toepassingen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5f649-243">Install CURL on the computer where you are running these applications from.</span></span> <span data-ttu-id="5f649-244">We CURL gebruiken om aan te roepen de eindpunten Livy om de taken op afstand uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5f649-244">We use CURL to invoke the Livy endpoints to run the jobs remotely.</span></span>

### <a name="run-the-spark-streaming-application-to-receive-the-events-into-an-azure-storage-blob-as-text"></a><span data-ttu-id="5f649-245">Voer de Spark-streaming-toepassing voor het ontvangen van de gebeurtenissen in een Azure Storage-Blob als tekst</span><span class="sxs-lookup"><span data-stu-id="5f649-245">Run the Spark streaming application to receive the events into an Azure Storage Blob as text</span></span>

<span data-ttu-id="5f649-246">Open een opdrachtprompt, navigeer naar de map waar u CURL geïnstalleerd en voer de volgende opdracht (de vervangen voor de gebruikersnaam en wachtwoord en de cluster-naam):</span><span class="sxs-lookup"><span data-stu-id="5f649-246">Open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="5f649-247">De parameters in het bestand **inputBlob.txt** als volgt gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="5f649-247">The parameters in the file **inputBlob.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="5f649-248">Laat het ons weten wat de parameters in het bestand voor invoer zijn:</span><span class="sxs-lookup"><span data-stu-id="5f649-248">Let us understand what the parameters in the input file are:</span></span>

* <span data-ttu-id="5f649-249">**bestand** is het pad naar het jar-bestand van toepassing op de Azure storage-account die is gekoppeld aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="5f649-249">**file** is the path to the application jar file on the Azure storage account associated with the cluster.</span></span>
* <span data-ttu-id="5f649-250">**className** is de naam van de klasse in de Directory met jar.</span><span class="sxs-lookup"><span data-stu-id="5f649-250">**className** is the name of the class in the jar.</span></span>
* <span data-ttu-id="5f649-251">**argumenten** is de lijst met argumenten dat is vereist door de klasse</span><span class="sxs-lookup"><span data-stu-id="5f649-251">**args** is the list of arguments required by the class</span></span>
* <span data-ttu-id="5f649-252">**numExecutors** is het aantal kernen gebruikt door Spark de streaming-toepassing uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="5f649-252">**numExecutors** is the number of cores used by Spark to run the streaming application.</span></span> <span data-ttu-id="5f649-253">Dit moet altijd ten minste twee keer het aantal partities van de Event Hub.</span><span class="sxs-lookup"><span data-stu-id="5f649-253">This should always be at least twice the number of Event Hub partitions.</span></span>
* <span data-ttu-id="5f649-254">**executorMemory**, **executorCores**, **driverMemory** zijn parameters vereiste resources toegewezen aan de streaming-toepassing.</span><span class="sxs-lookup"><span data-stu-id="5f649-254">**executorMemory**, **executorCores**, **driverMemory** are parameters used to assign required resources to the streaming application.</span></span>

> [!NOTE]
> <span data-ttu-id="5f649-255">U hoeft niet te maken van de uitvoermappen (EventCheckpoint, EventCount/EventCount10) die worden gebruikt als parameters.</span><span class="sxs-lookup"><span data-stu-id="5f649-255">You do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="5f649-256">De streaming-toepassing voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f649-256">The streaming application creates them for you.</span></span>
>
>

<span data-ttu-id="5f649-257">Wanneer u de opdracht uitvoert, ziet u de volgende uitvoer:</span><span class="sxs-lookup"><span data-stu-id="5f649-257">When you run the command, you should see an output like the following:</span></span>

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 to host mysparkcluster.azurehdinsight.net left intact

<span data-ttu-id="5f649-258">Noteer de batch-ID in de laatste regel van de uitvoer (in dit voorbeeld is '1').</span><span class="sxs-lookup"><span data-stu-id="5f649-258">Make a note of the batch ID in the last line of the output (in this example it is '1').</span></span> <span data-ttu-id="5f649-259">Om te bevestigen dat de toepassing wordt uitgevoerd, kunt u uw Azure storage-account die is gekoppeld aan het cluster bekijken en ziet u de **/EventCount/EventCount10** map er hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f649-259">To verify that the application runs successfully, you can look at your Azure storage account associated with the cluster and you should see the **/EventCount/EventCount10** folder created there.</span></span> <span data-ttu-id="5f649-260">Deze map moet bevatten blobs waarmee het aantal gebeurtenissen verwerkt binnen de opgegeven periode voor de parameter wordt vastgelegd **batch interval in seconden**.</span><span class="sxs-lookup"><span data-stu-id="5f649-260">This folder should contain blobs that captures the number of events processed within the time period specified for the parameter **batch-interval-in-seconds**.</span></span>

<span data-ttu-id="5f649-261">De Spark-streaming-toepassing blijft actief totdat u het afsluiten.</span><span class="sxs-lookup"><span data-stu-id="5f649-261">The Spark streaming application will continue to run until you kill it.</span></span> <span data-ttu-id="5f649-262">Gebruik de volgende opdracht om dit te doen:</span><span class="sxs-lookup"><span data-stu-id="5f649-262">To do so, use the following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-the-applications-to-receive-the-events-into-an-azure-storage-blob-as-json"></a><span data-ttu-id="5f649-263">De toepassingen voor het ontvangen van de gebeurtenissen in een Azure Storage-Blob als JSON uitvoeren</span><span class="sxs-lookup"><span data-stu-id="5f649-263">Run the applications to receive the events into an Azure Storage Blob as JSON</span></span>
<span data-ttu-id="5f649-264">Open een opdrachtprompt, navigeer naar de map waar u CURL geïnstalleerd en voer de volgende opdracht (de vervangen voor de gebruikersnaam en wachtwoord en de cluster-naam):</span><span class="sxs-lookup"><span data-stu-id="5f649-264">Open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="5f649-265">De parameters in het bestand **inputJSON.txt** als volgt gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="5f649-265">The parameters in the file **inputJSON.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="5f649-266">De parameters zijn vergelijkbaar met wat u hebt opgegeven voor de tekstuitvoer van de in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="5f649-266">The parameters are similar to what you specified for the text output, in the previous step.</span></span> <span data-ttu-id="5f649-267">Opnieuw, hoeft u niet de uitvoermappen (EventCheckpoint, EventCount/EventCount10) die worden gebruikt als parameters maken.</span><span class="sxs-lookup"><span data-stu-id="5f649-267">Again, you do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="5f649-268">De streaming-toepassing voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f649-268">The streaming application creates them for you.</span></span>

 <span data-ttu-id="5f649-269">Nadat u de opdracht uitvoert, u uw Azure storage-account die is gekoppeld aan het cluster bekijken kunt en u ziet de **/EventStore10** map er hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f649-269">After you run the command, you can look at your Azure storage account associated with the cluster and you should see the **/EventStore10** folder created there.</span></span> <span data-ttu-id="5f649-270">Open elk bestand voorafgegaan door **onderdeel -** en ziet u de gebeurtenissen in een JSON-indeling wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="5f649-270">Open any file prefixed with **part-** and you should see the events processed in a JSON format.</span></span>

### <a name="run-the-applications-to-receive-the-events-into-a-hive-table"></a><span data-ttu-id="5f649-271">De toepassingen voor het ontvangen van de gebeurtenissen in een Hive-tabel uitvoeren</span><span class="sxs-lookup"><span data-stu-id="5f649-271">Run the applications to receive the events into a Hive table</span></span>
<span data-ttu-id="5f649-272">Als u wilt uitvoeren van de Spark-streaming-toepassing die gebeurtenissen naar een Hive-tabel streams moet u een aantal extra onderdelen.</span><span class="sxs-lookup"><span data-stu-id="5f649-272">To run the Spark streaming application that streams events into a Hive table you need some additional components.</span></span> <span data-ttu-id="5f649-273">Dit zijn:</span><span class="sxs-lookup"><span data-stu-id="5f649-273">These are:</span></span>

* <span data-ttu-id="5f649-274">datanucleus api-jdo 3.2.6.jar</span><span class="sxs-lookup"><span data-stu-id="5f649-274">datanucleus-api-jdo-3.2.6.jar</span></span>
* <span data-ttu-id="5f649-275">datanucleus-rdbms-3.2.9.jar</span><span class="sxs-lookup"><span data-stu-id="5f649-275">datanucleus-rdbms-3.2.9.jar</span></span>
* <span data-ttu-id="5f649-276">datanucleus-core-3.2.10.jar</span><span class="sxs-lookup"><span data-stu-id="5f649-276">datanucleus-core-3.2.10.jar</span></span>
* <span data-ttu-id="5f649-277">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="5f649-277">hive-site.xml</span></span>

<span data-ttu-id="5f649-278">De **JAR** bestanden zijn beschikbaar op uw HDInsight Spark-cluster op `/usr/hdp/current/spark-client/lib`.</span><span class="sxs-lookup"><span data-stu-id="5f649-278">The **.jar** files are available on your HDInsight Spark cluster at `/usr/hdp/current/spark-client/lib`.</span></span> <span data-ttu-id="5f649-279">De **hive-site.xml** is beschikbaar op `/usr/hdp/current/spark-client/conf`.</span><span class="sxs-lookup"><span data-stu-id="5f649-279">The **hive-site.xml** is available at `/usr/hdp/current/spark-client/conf`.</span></span>

<span data-ttu-id="5f649-280">U kunt [WinScp](http://winscp.net/eng/download.php) deze bestanden uit het cluster op uw lokale computer worden overschreven.</span><span class="sxs-lookup"><span data-stu-id="5f649-280">You can use [WinScp](http://winscp.net/eng/download.php) to copy over these files from the cluster to your local computer.</span></span> <span data-ttu-id="5f649-281">Vervolgens kunt u hulpprogramma's voor deze bestanden te kopiëren via naar uw opslagaccount die is gekoppeld aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="5f649-281">You can then use tools to copy these files over to your storage account associated with the cluster.</span></span> <span data-ttu-id="5f649-282">Zie voor meer informatie over het uploaden van bestanden naar het opslagaccount [gegevens voor Hadoop-taken in HDInsight uploaden](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="5f649-282">For more information on how to upload files to the storage account, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

<span data-ttu-id="5f649-283">Zodra u de bestanden over naar uw Azure storage-account hebt gekopieerd, open een opdrachtprompt, gaat u naar de map waar u CURL geïnstalleerd en voer de volgende opdracht (de vervangen voor de gebruikersnaam en wachtwoord en de cluster-naam):</span><span class="sxs-lookup"><span data-stu-id="5f649-283">Once you have copied over the files to your Azure storage account, open a command prompt, navigate to the directory where you installed CURL, and run the following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="5f649-284">De parameters in het bestand **inputHive.txt** als volgt gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="5f649-284">The parameters in the file **inputHive.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="5f649-285">De parameters zijn vergelijkbaar met wat u hebt opgegeven voor de tekstuitvoer van de in de vorige stappen.</span><span class="sxs-lookup"><span data-stu-id="5f649-285">The parameters are similar to what you specified for the text output, in the previous steps.</span></span> <span data-ttu-id="5f649-286">Opnieuw, u hoeft te maken van de uitvoermappen (EventCheckpoint, EventCount/EventCount10) of de uitvoer van de Hive-tabel (EventHiveTable10) die worden gebruikt als parameters.</span><span class="sxs-lookup"><span data-stu-id="5f649-286">Again, you do not need to create the output folders (EventCheckpoint, EventCount/EventCount10) or the output Hive table (EventHiveTable10) that are used as parameters.</span></span> <span data-ttu-id="5f649-287">De streaming-toepassing voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f649-287">The streaming application creates them for you.</span></span> <span data-ttu-id="5f649-288">Houd er rekening mee dat de **potten** en **bestanden** optie omvat paden naar de JAR-bestanden en de hive-site.xml die u gekopieerd naar het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="5f649-288">Note that the **jars** and **files** option includes paths to the .jar files and the hive-site.xml that you copied over to the storage account.</span></span>

<span data-ttu-id="5f649-289">Om te controleren of de hive-tabel is gemaakt, kunt u SSH in het cluster en de Hive-query's uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5f649-289">To verify that the hive table was successfully created, you can SSH into the cluster and run Hive queries.</span></span> <span data-ttu-id="5f649-290">Zie voor instructies [Hive gebruiken met Hadoop in HDInsight met SSH](hdinsight-hadoop-use-hive-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="5f649-290">For instructions, see [Use Hive with Hadoop in HDInsight with SSH](hdinsight-hadoop-use-hive-ssh.md).</span></span> <span data-ttu-id="5f649-291">Zodra u met het gebruik van SSH verbonden bent, u kunt Voer de volgende opdracht om te controleren of de Hive-tabel **EventHiveTable10**, wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f649-291">Once you are connected using SSH, you can run the following command to verify that the Hive table, **EventHiveTable10**, is created.</span></span>

    show tables;

<span data-ttu-id="5f649-292">Als het goed is, wordt ongeveer de volgende uitvoer weergegeven:</span><span class="sxs-lookup"><span data-stu-id="5f649-292">You should see an output similar to the following:</span></span>

    OK
    eventhivetable10
    hivesampletable

<span data-ttu-id="5f649-293">U kunt ook een SELECT-query om weer te geven van de inhoud van de tabel uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5f649-293">You can also run a SELECT query to view the contents of the table.</span></span>

    SELECT * FROM eventhivetable10 LIMIT 10;

<span data-ttu-id="5f649-294">Als het goed is, wordt ongeveer de volgende uitvoer weergegeven:</span><span class="sxs-lookup"><span data-stu-id="5f649-294">You should see an output like the following:</span></span>

    ZN90apUSQODDTx7n6Toh6jDbuPngqT4c
    sor2M7xsFwmaRW8W8NDwMneFNMrOVkW1
    o2HcsU735ejSi2bGEcbUSB4btCFmI1lW
    TLuibq4rbj0T9st9eEzIWJwNGtMWYoYS
    HKCpPlWFWAJILwR69MAq863nCWYzDEw6
    Mvx0GQOPYvPR7ezBEpIHYKTKiEhYammQ
    85dRppSBSbZgThLr1s0GMgKqynDUqudr
    5LAWkNqorLj3ZN9a2mfWr9rZqeXKN4pF
    ulf9wSFNjD7BZXCyunozecov9QpEIYmJ
    vWzM3nvOja8DhYcwn0n5eTfOItZ966pa
    Time taken: 4.434 seconds, Fetched: 10 row(s)


### <a name="run-the-applications-to-receive-the-events-into-an-azure-sql-database-table"></a><span data-ttu-id="5f649-295">De toepassingen voor het ontvangen van de gebeurtenissen in een Azure SQL database-tabel uitvoeren</span><span class="sxs-lookup"><span data-stu-id="5f649-295">Run the applications to receive the events into an Azure SQL database table</span></span>
<span data-ttu-id="5f649-296">Voordat u deze stap uitvoert, zorg ervoor dat u hebt een Azure SQL-database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f649-296">Before running this step, make sure you have an Azure SQL database created.</span></span> <span data-ttu-id="5f649-297">Zie voor instructies [maken van een SQL-database in minuten](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="5f649-297">For instructions, see [Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span> <span data-ttu-id="5f649-298">Voor het voltooien van deze sectie, moet u waarden voor de databasenaam, database-servernaam en de beheerdersreferenties voor de database als parameters.</span><span class="sxs-lookup"><span data-stu-id="5f649-298">To complete this section, you need values for database name, database server name, and the database administrator credentials as parameters.</span></span> <span data-ttu-id="5f649-299">U hoeft niet te maken met de databasetabel.</span><span class="sxs-lookup"><span data-stu-id="5f649-299">You do not need to create the database table though.</span></span> <span data-ttu-id="5f649-300">De Spark-streaming-toepassing die voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5f649-300">The Spark streaming application creates that for you.</span></span>

<span data-ttu-id="5f649-301">Open een opdrachtprompt, navigeer naar de map waar u CURL geïnstalleerd en voer de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="5f649-301">Open a command prompt, navigate to the directory where you installed CURL, and run the following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="5f649-302">De parameters in het bestand **inputSQL.txt** als volgt gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="5f649-302">The parameters in the file **inputSQL.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="5f649-303">Om te bevestigen dat de toepassing wordt uitgevoerd, kunt u verbinding met de Azure SQL database met SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="5f649-303">To verify that the application runs successfully, you can connect to the Azure SQL database using SQL Server Management Studio.</span></span> <span data-ttu-id="5f649-304">Zie voor instructies over hoe u dat doet, [verbinding maken met SQL Database met SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="5f649-304">For instructions on how to do that, see [Connect to SQL Database with SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span></span> <span data-ttu-id="5f649-305">Nadat u met de database verbonden bent, kunt u gaat naar de **EventContent** tabel die is gemaakt door de streaming-toepassing.</span><span class="sxs-lookup"><span data-stu-id="5f649-305">Once you are connected to the database, you can navigate to the **EventContent** table that was created by the streaming application.</span></span> <span data-ttu-id="5f649-306">U kunt een snelle query om de gegevens uit de tabel uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5f649-306">You can run a quick query to get the data from the table.</span></span> <span data-ttu-id="5f649-307">Voer de volgende query:</span><span class="sxs-lookup"><span data-stu-id="5f649-307">Run the following query:</span></span>

    SELECT * FROM EventCount

<span data-ttu-id="5f649-308">De uitvoer ziet er als volgt uit:</span><span class="sxs-lookup"><span data-stu-id="5f649-308">You should see output similar to the following:</span></span>

    00046b0f-2552-4980-9c3f-8bba5647c8ee
    000b7530-12f9-4081-8e19-90acd26f9c0c
    000bc521-9c1b-4a42-ab08-dc1893b83f3b
    00123a2a-e00d-496a-9104-108920955718
    0017c68f-7a4e-452d-97ad-5cb1fe5ba81b
    001KsmqL2gfu5ZcuQuTqTxQvVyGCqPp9
    001vIZgOStka4DXtud0e3tX7XbfMnZrN
    00220586-3e1a-4d2d-a89b-05c5892e541a
    0029e309-9e54-4e1b-84be-cd04e6fce5ec
    003333cf-874f-4045-9da3-9f98c2b4ea49
    0043c07e-8d73-420a-9af7-1fcb94575356
    004a11a9-0c2c-4bc0-a7d5-2e0ebd947ab9


## <span data-ttu-id="5f649-309"><a name="seealso"></a>Zie ook</span><span class="sxs-lookup"><span data-stu-id="5f649-309"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="5f649-310">Overzicht: Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f649-310">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)
* [<span data-ttu-id="5f649-311">Ontwerp van de verbinding op basis van de ontvanger en Direct DStream</span><span class="sxs-lookup"><span data-stu-id="5f649-311">Design of Receiver-based Connection and Direct DStream</span></span>](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)

### <a name="scenarios"></a><span data-ttu-id="5f649-312">Scenario's</span><span class="sxs-lookup"><span data-stu-id="5f649-312">Scenarios</span></span>
* [<span data-ttu-id="5f649-313">Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools</span><span class="sxs-lookup"><span data-stu-id="5f649-313">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="5f649-314">Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens</span><span class="sxs-lookup"><span data-stu-id="5f649-314">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="5f649-315">Spark met Machine Learning: Spark in HDInsight gebruiken om voedselinspectieresultaten te voorspellen</span><span class="sxs-lookup"><span data-stu-id="5f649-315">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="5f649-316">Websitelogboekanalyse met Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f649-316">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="5f649-317">Toepassingen maken en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="5f649-317">Create and run applications</span></span>
* [<span data-ttu-id="5f649-318">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="5f649-318">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="5f649-319">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="5f649-319">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="5f649-320">Tools en uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="5f649-320">Tools and extensions</span></span>
* [<span data-ttu-id="5f649-321">De invoegtoepassing HDInsight Tools for IntelliJ IDEA gebruiken om Spark Scala-toepassingen te maken en in te dienen</span><span class="sxs-lookup"><span data-stu-id="5f649-321">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="5f649-322">De invoegtoepassing HDInsight Tools for IntelliJ IDEA gebruiken om op afstand fouten in Spark Scala-toepassingen op te lossen</span><span class="sxs-lookup"><span data-stu-id="5f649-322">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="5f649-323">Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f649-323">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="5f649-324">Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f649-324">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="5f649-325">Externe pakketten gebruiken met Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="5f649-325">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="5f649-326">Jupyter op uw computer installeren en verbinding maken met een HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="5f649-326">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="5f649-327">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="5f649-327">Manage resources</span></span>
* [<span data-ttu-id="5f649-328">Resources beheren voor het Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="5f649-328">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="5f649-329">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="5f649-329">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/
