---
title: aaaUse Apache Spark-streaming met Event Hubs in Azure HDInsight | Microsoft Docs
description: Een voorbeeld van Apache Spark-streaming voor hoe toosend data stream tooAzure Event Hub en ontvangt deze gebeurtenissen in HDInsight Spark-cluster met een scala-toepassing bouwen.
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
ms.openlocfilehash: 10cc5884047b3b8249fe8a8822a16a19780a4af3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="apache-spark-streaming-process-data-from-azure-event-hubs-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="09111-104">Apache Spark-streaming: procesgegevens uit Azure Event Hubs met Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="09111-104">Apache Spark streaming: Process data from Azure Event Hubs with Spark cluster on HDInsight</span></span>

<span data-ttu-id="09111-105">In dit artikel maakt u een Apache Spark-streaming-voorbeeld waarbij Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="09111-105">In this article, you create an Apache Spark streaming sample that involves hello following steps:</span></span>

1. <span data-ttu-id="09111-106">U kunt een zelfstandige toepassing tooingest berichten gebruiken in een Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="09111-106">You use a standalone application tooingest messages into an Azure Event Hub.</span></span>

2. <span data-ttu-id="09111-107">Met twee verschillende benaderingen ophalen u Hallo-berichten van Event Hub in realtime met behulp van een toepassing die wordt uitgevoerd in Spark-cluster in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="09111-107">With two different approaches, you retrieve hello messages from Event Hub in real-time using an application running in Spark cluster on Azure HDInsight.</span></span>

3. <span data-ttu-id="09111-108">Als u streaming analytische pijplijnen toopersist gegevens toodifferent opslagsystemen bouwen of inzichten verkrijgen van gegevens op Hallo snel.</span><span class="sxs-lookup"><span data-stu-id="09111-108">You build streaming analytic pipelines toopersist data toodifferent storage systems, or get insights from data on hello fly.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09111-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="09111-109">Prerequisites</span></span>

* <span data-ttu-id="09111-110">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="09111-110">An Azure subscription.</span></span> <span data-ttu-id="09111-111">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="09111-111">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="09111-112">Een Apache Spark-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="09111-112">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="09111-113">Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span><span class="sxs-lookup"><span data-stu-id="09111-113">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="spark-streaming-concepts"></a><span data-ttu-id="09111-114">Concepten Spark-Streaming</span><span class="sxs-lookup"><span data-stu-id="09111-114">Spark Streaming concepts</span></span>

<span data-ttu-id="09111-115">Zie voor een gedetailleerde uitleg van Spark-streaming [Apache Spark-streaming-overzicht](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span><span class="sxs-lookup"><span data-stu-id="09111-115">For a detailed explanation of Spark streaming, see [Apache Spark streaming overview](http://spark.apache.org/docs/latest/streaming-programming-guide.html#overview).</span></span> <span data-ttu-id="09111-116">HDInsight biedt Hallo dezelfde streaming functies tooa Spark-cluster in Azure.</span><span class="sxs-lookup"><span data-stu-id="09111-116">HDInsight brings hello same streaming features tooa Spark cluster on Azure.</span></span>  

## <a name="what-does-this-solution-do"></a><span data-ttu-id="09111-117">Wat doet deze oplossing?</span><span class="sxs-lookup"><span data-stu-id="09111-117">What does this solution do?</span></span>

<span data-ttu-id="09111-118">Voer in dit artikel wordt een voorbeeld van de Spark-streaming toocreate Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="09111-118">In this article, toocreate a Spark streaming example, perform hello following steps:</span></span>

1. <span data-ttu-id="09111-119">Maak een Azure Event Hub die u een stream van gebeurtenissen ontvangt.</span><span class="sxs-lookup"><span data-stu-id="09111-119">Create an Azure Event Hub that will receive a stream of events.</span></span>

2. <span data-ttu-id="09111-120">Uitvoeren van een lokale zelfstandige toepassing die wordt gegenereerd gebeurtenissen en stuurt deze toohello Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="09111-120">Run a local standalone application that generates events and pushes it toohello Azure Event Hub.</span></span> <span data-ttu-id="09111-121">Hallo-voorbeeldtoepassing die dit biedt is gepubliceerd op [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="09111-121">hello sample application that does this is published at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span>

3. <span data-ttu-id="09111-122">Een streaming-toepassing op afstand uitvoeren op een Spark-cluster die streaming-gebeurtenissen van Azure Event Hub leest en analyse van de verschillende gegevensverwerking /.</span><span class="sxs-lookup"><span data-stu-id="09111-122">Run a streaming application remotely on a Spark cluster that reads streaming events from Azure Event Hub and perform various data processing/analysis.</span></span>

## <a name="create-an-azure-event-hub"></a><span data-ttu-id="09111-123">Een Azure Event Hub maken</span><span class="sxs-lookup"><span data-stu-id="09111-123">Create an Azure Event Hub</span></span>

1. <span data-ttu-id="09111-124">Meld u aan toohello [Azure Portal](https://ms.portal.azure.com), en klik op **nieuw** op Hallo linksboven welkomstscherm.</span><span class="sxs-lookup"><span data-stu-id="09111-124">Log on toohello [Azure Portal](https://ms.portal.azure.com), and click **New** at hello top left of hello screen.</span></span>

2. <span data-ttu-id="09111-125">Klik op **Internet van dingen** en vervolgens op **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="09111-125">Click **Internet of Things**, then click **Event Hubs**.</span></span>

    <span data-ttu-id="09111-126">![Create event hub voor Spark-streaming-voorbeeld](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "maken event hub voor Spark-streaming-voorbeeld")</span><span class="sxs-lookup"><span data-stu-id="09111-126">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-create-event-hub-for-spark-streaming.png "Create event hub for Spark streaming example")</span></span>

3. <span data-ttu-id="09111-127">In Hallo **naamruimte maken** blade, voer de naam van een naamruimte.</span><span class="sxs-lookup"><span data-stu-id="09111-127">In hello **Create namespace** blade, enter a namespace name.</span></span> <span data-ttu-id="09111-128">Kies Hallo prijscategorie (basis of standaard).</span><span class="sxs-lookup"><span data-stu-id="09111-128">choose hello pricing tier (Basic or Standard).</span></span> <span data-ttu-id="09111-129">Ook een Azure-abonnement, resourcegroep en locatie kiezen in welke toocreate Hallo-resource.</span><span class="sxs-lookup"><span data-stu-id="09111-129">Also, choose an Azure subscription, resource group, and location in which toocreate hello resource.</span></span> <span data-ttu-id="09111-130">Klik op **maken** toocreate Hallo naamruimte.</span><span class="sxs-lookup"><span data-stu-id="09111-130">Click **Create** toocreate hello namespace.</span></span>

      <span data-ttu-id="09111-131">![Geef de naam van een event hub voor Spark-streaming-voorbeeld](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "bieden u de naam van een event hub voor Spark-streaming-voorbeeld")</span><span class="sxs-lookup"><span data-stu-id="09111-131">![Provide an event hub name for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-name-for-spark-streaming.png "Provide an event hub name for Spark streaming example")</span></span>

    > [!NOTE]
    > <span data-ttu-id="09111-132">U selecteert moet Hallo dezelfde **locatie** als uw cluster Apache Spark in HDInsight tooreduce latentie en kosten.</span><span class="sxs-lookup"><span data-stu-id="09111-132">You should select hello same **Location** as your Apache Spark cluster in HDInsight tooreduce latency and costs.</span></span>
    >
    >

4. <span data-ttu-id="09111-133">Klik op Hallo gemaakte naamruimte in Hallo Event Hubs naamruimte lijst.</span><span class="sxs-lookup"><span data-stu-id="09111-133">In hello Event Hubs namespace list, click hello newly-created namespace.</span></span>      


5. <span data-ttu-id="09111-134">Klik op Hallo naamruimte blade **Event Hubs**, en klik vervolgens op **+ Event Hub** toocreate nieuwe Event Hub.</span><span class="sxs-lookup"><span data-stu-id="09111-134">In hello namespace blade, click **Event Hubs**, and then click **+ Event Hub** toocreate a new Event Hub.</span></span>
   
    <span data-ttu-id="09111-135">![Create event hub voor Spark-streaming-voorbeeld](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "maken event hub voor Spark-streaming-voorbeeld")</span><span class="sxs-lookup"><span data-stu-id="09111-135">![Create event hub for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-open-event-hubs-blade-for-spark-streaming-example.png "Create event hub for Spark streaming example")</span></span>

6. <span data-ttu-id="09111-136">Typ een naam voor uw Event Hub, set Hallo partitie aantal too10 en bericht bewaren too1.</span><span class="sxs-lookup"><span data-stu-id="09111-136">Type a name for your Event Hub, set hello partition count too10, and message retention too1.</span></span> <span data-ttu-id="09111-137">We zijn Hallo-berichten in deze oplossing niet archiveren zodat u kunt Hallo rest als standaard laat en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="09111-137">We are not archiving hello messages in this solution so you can leave hello rest as default, and then click **Create**.</span></span>
   
    <span data-ttu-id="09111-138">![Geef details van gebeurtenis hub voor Spark-streaming-voorbeeld](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "event hub-informatie opgeven voor Spark-streaming-voorbeeld")</span><span class="sxs-lookup"><span data-stu-id="09111-138">![Provide event hub details for Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-provide-event-hub-details-for-spark-streaming-example.png "Provide event hub details for Spark streaming example")</span></span>

7. <span data-ttu-id="09111-139">Hallo nieuw gemaakte Event Hub wordt vermeld in Hallo Event Hub-blade.</span><span class="sxs-lookup"><span data-stu-id="09111-139">hello newly created Event Hub is listed in hello Event Hub blade.</span></span>
    
     <span data-ttu-id="09111-140">![Event Hub voor Hallo Spark-streaming voorbeeld weergeven](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "weergave Event Hub voor Hallo Spark-streaming voorbeeld")</span><span class="sxs-lookup"><span data-stu-id="09111-140">![View Event Hub for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-for-spark-streaming-example.png "View Event Hub for hello Spark streaming example")</span></span>

8. <span data-ttu-id="09111-141">Klik op terug in Hallo naamruimte blade (geen Hallo specifieke Event Hub blade) **gedeeld toegangsbeleid**, en klik vervolgens op **RootManageSharedAccessKey**.</span><span class="sxs-lookup"><span data-stu-id="09111-141">Back in hello namespace blade (not hello specific Event Hub blade), click **Shared access policies**, and then click **RootManageSharedAccessKey**.</span></span>
    
     <span data-ttu-id="09111-142">![Stel beleid in de Event Hub voor Hallo Spark-streaming voorbeeld](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Event Hub ingesteld beleid voor Hallo Spark-streaming voorbeeld")</span><span class="sxs-lookup"><span data-stu-id="09111-142">![Set Event Hub policies for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-set-event-hub-policies-for-spark-streaming-example.png "Set Event Hub policies for hello Spark streaming example")</span></span>

9. <span data-ttu-id="09111-143">Klik op Hallo kopie knop toocopy Hallo **RootManageSharedAccessKey** primaire sleutel en connection string toohello Klembord.</span><span class="sxs-lookup"><span data-stu-id="09111-143">Click hello copy button toocopy hello **RootManageSharedAccessKey** primary key and connection string toohello clipboard.</span></span> <span data-ttu-id="09111-144">Sla deze toouse verderop in de zelfstudie Hallo.</span><span class="sxs-lookup"><span data-stu-id="09111-144">Save these toouse later in hello tutorial.</span></span>
    
     <span data-ttu-id="09111-145">![Event Hub beleid sleutels voor Hallo Spark-streaming voorbeeld weergeven](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "weergave Event Hub beleid sleutels voor Hallo Spark-streaming voorbeeld")</span><span class="sxs-lookup"><span data-stu-id="09111-145">![View Event Hub policy keys for hello Spark streaming example](./media/hdinsight-apache-spark-eventhub-streaming/hdinsight-view-event-hub-policy-keys.png "View Event Hub policy keys for hello Spark streaming example")</span></span>

## <a name="send-messages-tooazure-event-hub-using-a-sample-scala-application"></a><span data-ttu-id="09111-146">Verzenden van berichten tooAzure Event Hub met behulp van een voorbeeldtoepassing Scala</span><span class="sxs-lookup"><span data-stu-id="09111-146">Send messages tooAzure Event Hub using a sample Scala application</span></span>

<span data-ttu-id="09111-147">In deze sectie gebruikt u een zelfstandige lokale Scala toepassing die een stream van gebeurtenissen wordt gegenereerd en verzendt het tooAzure Event Hub die u eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="09111-147">In this section you use a standalone local Scala application that generates a stream of events and sends it tooAzure Event Hub that you created earlier.</span></span> <span data-ttu-id="09111-148">Deze toepassing is beschikbaar op GitHub op [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span><span class="sxs-lookup"><span data-stu-id="09111-148">This application is available on GitHub at [https://github.com/hdinsight/eventhubs-sample-event-producer](https://github.com/hdinsight/eventhubs-sample-event-producer).</span></span> <span data-ttu-id="09111-149">Hier Hallo stappen wordt ervan uitgegaan dat u al deze GitHub-opslagplaats hebben forked.</span><span class="sxs-lookup"><span data-stu-id="09111-149">hello steps here assume that you have already forked this GitHub repository.</span></span>

1. <span data-ttu-id="09111-150">Zorg ervoor dat er Hallo volgende geïnstalleerd op Hallo-computer waarop u deze toepassing uitvoert.</span><span class="sxs-lookup"><span data-stu-id="09111-150">Make sure you have hello following installed on hello computer where you run this application.</span></span>

    * <span data-ttu-id="09111-151">Oracle Java Development kit.</span><span class="sxs-lookup"><span data-stu-id="09111-151">Oracle Java Development kit.</span></span> <span data-ttu-id="09111-152">Kunt u het installeren van [hier](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span><span class="sxs-lookup"><span data-stu-id="09111-152">You can install it from [here](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).</span></span>
    * <span data-ttu-id="09111-153">Apache Maven.</span><span class="sxs-lookup"><span data-stu-id="09111-153">Apache Maven.</span></span> <span data-ttu-id="09111-154">U kunt downloaden van [hier](https://maven.apache.org/download.cgi).</span><span class="sxs-lookup"><span data-stu-id="09111-154">You can download it from [here](https://maven.apache.org/download.cgi).</span></span> <span data-ttu-id="09111-155">Vindt u instructies tooinstall Maven [hier](https://maven.apache.org/install.html).</span><span class="sxs-lookup"><span data-stu-id="09111-155">Instructions tooinstall Maven are available [here](https://maven.apache.org/install.html).</span></span>

2. <span data-ttu-id="09111-156">Open een opdrachtprompt en navigeer toohello locatie gekloond van GitHub-repo-Hallo voor de voorbeeldtoepassing Scala Hallo en Hallo na opdracht toobuild Hallo toepassing uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="09111-156">Open a command prompt and navigate toohello location you cloned hello GitHub repo for hello sample Scala application and run hello following command toobuild hello application.</span></span>

        mvn package

3. <span data-ttu-id="09111-157">Hallo uitvoer jar voor toepassing hello, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, wordt gemaakt onder **/target** directory.</span><span class="sxs-lookup"><span data-stu-id="09111-157">hello output jar for hello application, **com-microsoft-azure-eventhubs-client-example-0.2.0.jar**, is created under **/target** directory.</span></span> <span data-ttu-id="09111-158">U deze JAR verderop in dit artikel tootest Hallo volledige oplossing gebruiken.</span><span class="sxs-lookup"><span data-stu-id="09111-158">You use this JAR later in this article tootest hello complete solution.</span></span>

## <a name="create-application-tooreceive-messages-from-event-hub-into-a-spark-cluster"></a><span data-ttu-id="09111-159">Toepassing tooreceive berichten van Event Hub maken in een Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="09111-159">Create application tooreceive messages from Event Hub into a Spark cluster</span></span> 

<span data-ttu-id="09111-160">Er zijn twee benaderingen tooconnect Spark-Streaming en Azure Event Hubs, verbinding op basis van de ontvanger en Direct-DStream-verbinding.</span><span class="sxs-lookup"><span data-stu-id="09111-160">We have two approaches tooconnect Spark Streaming and Azure Event Hubs, Receiver-based connection and Direct-DStream-based connection.</span></span> <span data-ttu-id="09111-161">Direct DStream gebaseerd is op januari 2017 geïntroduceerd in Hallo 2.0.3 release.</span><span class="sxs-lookup"><span data-stu-id="09111-161">Direct-DStream-based is introduced on Jan of 2017, in hello 2.0.3 release.</span></span> <span data-ttu-id="09111-162">Dit moet omdat deze meer zodat tooreplace Hallo oorspronkelijke op basis van een ontvanger verbinding en resource-efficiënt.</span><span class="sxs-lookup"><span data-stu-id="09111-162">It is supposed tooreplace hello original receiver-based connection as it is more performant and resource-efficient.</span></span> <span data-ttu-id="09111-163">Meer details te vinden in [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span><span class="sxs-lookup"><span data-stu-id="09111-163">More details found in [https://github.com/hdinsight/spark-eventhubs](https://github.com/hdinsight/spark-eventhubs).</span></span> <span data-ttu-id="09111-164">Directe DStream ondersteunt alleen Spark 2.0 +.</span><span class="sxs-lookup"><span data-stu-id="09111-164">Direct DStream only supports Spark 2.0+.</span></span>

### <a name="build-applications-with-hello-dependency-toospark-eventhubs-connector"></a><span data-ttu-id="09111-165">Toepassingen met Hallo afhankelijkheid toospark eventhubs-connector maken</span><span class="sxs-lookup"><span data-stu-id="09111-165">Build applications with hello dependency toospark-eventhubs connector</span></span>

<span data-ttu-id="09111-166">We ook publiceren Hallo staging-versie van Spark-EventHubs in GitHub.</span><span class="sxs-lookup"><span data-stu-id="09111-166">We will also publish hello staging version of Spark-EventHubs in GitHub.</span></span> <span data-ttu-id="09111-167">toouse hello staging-versie van Spark-EventHubs: Hallo eerste stap is het tooindicate GitHub als bron opslagplaats Hallo door toe te voegen Hallo vermelding toopom.xml te volgen:</span><span class="sxs-lookup"><span data-stu-id="09111-167">toouse hello staging version of Spark-EventHubs, hello first step is tooindicate GitHub as hello source repo by adding hello following entry toopom.xml:</span></span>

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

<span data-ttu-id="09111-168">Vervolgens kunt u toevoegen Hallo afhankelijkheid tooyour project tootake Hallo prerelease-versie te volgen.</span><span class="sxs-lookup"><span data-stu-id="09111-168">You can then add hello following dependency tooyour project tootake hello pre-released version.</span></span>

<span data-ttu-id="09111-169">Maven-afhankelijkheid</span><span class="sxs-lookup"><span data-stu-id="09111-169">Maven Dependency</span></span>

```xml
<!-- https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11 -->
<dependency>
    <groupId>com.microsoft.azure</groupId>
    <artifactId>spark-streaming-eventhubs_2.11</artifactId>
    <version>2.0.4</version>
</dependency>
```

<span data-ttu-id="09111-170">SBT afhankelijkheid</span><span class="sxs-lookup"><span data-stu-id="09111-170">SBT Dependency</span></span>

```
// https://mvnrepository.com/artifact/com.microsoft.azure/spark-streaming-eventhubs_2.11
libraryDependencies += "com.microsoft.azure" % "spark-streaming-eventhubs_2.11" % "2.0.4"
```

### <a name="direct-dstream-connection"></a><span data-ttu-id="09111-171">Rechtstreekse verbinding DStream</span><span class="sxs-lookup"><span data-stu-id="09111-171">Direct DStream Connection</span></span>

<span data-ttu-id="09111-172">Een vooraf samengestelde jar-bestand met voorbeelden met directe DStream kan worden gedownload [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span><span class="sxs-lookup"><span data-stu-id="09111-172">A pre-built jar file containing examples using Direct DStream can be downloaded in [http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar](http://central.maven.org/maven2/com/microsoft/azure/spark-streaming-eventhubs_2.11/2.0.4/spark-streaming-eventhubs_2.11-2.0.4.jar).</span></span>

<span data-ttu-id="09111-173">Hallo jar-bestand bevat drie voorbeelden waarvan de broncode zijn beschikbaar op [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span><span class="sxs-lookup"><span data-stu-id="09111-173">hello jar file contains three examples whose source code are available at [https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream](https://github.com/hdinsight/spark-eventhubs/tree/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream).</span></span>

<span data-ttu-id="09111-174">Duurt [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) als een voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="09111-174">Taking [WindowingWordCount](https://github.com/hdinsight/spark-eventhubs/blob/master/examples/src/main/scala/com/microsoft/spark/streaming/examples/directdstream/WindowingWordCount.scala) as an example:</span></span>

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

<span data-ttu-id="09111-175">In Hallo hierboven bijvoorbeeld `eventhubParameters` zijn Hallo parameters specifieke tooa één EventHubs-exemplaar en hebt u toopass het toohello `createDirectStreams` API die een directe DStream object tooa Event Hubs toewijzingsnaamruimte vormt.</span><span class="sxs-lookup"><span data-stu-id="09111-175">In hello above example, `eventhubParameters` are hello parameters specific tooa single EventHubs instance and you have toopass it toohello `createDirectStreams` API which constructs a Direct DStream object mapping tooa Event Hubs namespace.</span></span> <span data-ttu-id="09111-176">U kunt op Hallo Direct DStream object DStream API's die door framework Spark-Streaming-API aanroepen.</span><span class="sxs-lookup"><span data-stu-id="09111-176">Over hello Direct DStream object, you can call any DStream API provided by Spark Streaming API framework.</span></span> <span data-ttu-id="09111-177">In dit voorbeeld berekenen we Hallo frequentie van elk woord in hello laatste 3 micro batch-intervallen.</span><span class="sxs-lookup"><span data-stu-id="09111-177">In this example, we calculate hello frequency of each word within hello last 3 micro batch intervals.</span></span>

### <a name="receiver-based-connection"></a><span data-ttu-id="09111-178">Verbinding op basis van een ontvanger</span><span class="sxs-lookup"><span data-stu-id="09111-178">Receiver-based Connection</span></span>

<span data-ttu-id="09111-179">Een Spark-streaming-voorbeeldtoepassing die zijn geschreven in Scala die gebeurtenissen en route Hallo toodifferent bestemmingen ontvangt, is beschikbaar op [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span><span class="sxs-lookup"><span data-stu-id="09111-179">A Spark streaming example application written in Scala, which receives events and route hello toodifferent destinations, is available at [https://github.com/hdinsight/spark-streaming-data-persistence-examples](https://github.com/hdinsight/spark-streaming-data-persistence-examples).</span></span> <span data-ttu-id="09111-180">Hallo stappen hieronder tooupdate Hallo-toepassing voor de configuratie van uw Event Hub en Hallo uitvoer jar maken.</span><span class="sxs-lookup"><span data-stu-id="09111-180">Follow hello steps below tooupdate hello application for your Event Hub configuration and create hello output jar.</span></span>

1. <span data-ttu-id="09111-181">Start IntelliJ IDEA en van Hallo starten scherm selecteren **uitchecken uit versiebeheer** en klik vervolgens op **Git**.</span><span class="sxs-lookup"><span data-stu-id="09111-181">Launch IntelliJ IDEA and from hello launch screen select **Check out from Version Control** and then click **Git**.</span></span>
   
    <span data-ttu-id="09111-182">![Apache Spark-streaming-voorbeeld - get-bronnen van Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark-streaming-voorbeeld - get-bronnen van Git")</span><span class="sxs-lookup"><span data-stu-id="09111-182">![Apache Spark streaming example - get sources from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-get-source-from-git.png "Apache Spark streaming example - get sources from Git")</span></span>

2. <span data-ttu-id="09111-183">In Hallo **kloon opslagplaats** in het dialoogvenster bieden Hallo URL toohello Git-opslagplaats tooclone uit, geef Hallo directory tooclone aan en klik op **kloon**.</span><span class="sxs-lookup"><span data-stu-id="09111-183">In hello **Clone Repository** dialog box, provide hello URL toohello Git repository tooclone from, specify hello directory tooclone to, and then click **Clone**.</span></span>
   
    <span data-ttu-id="09111-184">![Apache Spark-streaming-voorbeeld - kloon van Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark-streaming-voorbeeld - kloon van Git")</span><span class="sxs-lookup"><span data-stu-id="09111-184">![Apache Spark streaming example - clone from Git](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-clone-from-git.png "Apache Spark streaming example - clone from Git")</span></span>
3. <span data-ttu-id="09111-185">Volg Hallo aanwijzingen tot Hallo project volledig is gekloond.</span><span class="sxs-lookup"><span data-stu-id="09111-185">Follow hello prompts till hello project is completely cloned.</span></span> <span data-ttu-id="09111-186">Druk op **Alt + 1** tooopen hello **Project-weergave**.</span><span class="sxs-lookup"><span data-stu-id="09111-186">Press **Alt + 1** tooopen hello **Project View**.</span></span> <span data-ttu-id="09111-187">Het bestand is vergelijkbaar Hallo volgende.</span><span class="sxs-lookup"><span data-stu-id="09111-187">It should resemble hello following.</span></span>
   
    <span data-ttu-id="09111-188">![Apache Spark-streaming-voorbeeld - Project-weergave](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark-streaming-voorbeeld - Project-weergave")</span><span class="sxs-lookup"><span data-stu-id="09111-188">![Apache Spark streaming example - Project View](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-project-view.png "Apache Spark streaming example - Project View")</span></span>
4. <span data-ttu-id="09111-189">Zorg ervoor dat de toepassingscode Hallo is gecompileerd met Java8.</span><span class="sxs-lookup"><span data-stu-id="09111-189">Make sure hello application code is compiled with Java8.</span></span> <span data-ttu-id="09111-190">tooensure, klikt u op **bestand**, klikt u op **projectstructuur**, en op Hallo **Project** tabblad, stel projectniveau taal te**8 - lambda's, het type aantekeningen, enz.**.</span><span class="sxs-lookup"><span data-stu-id="09111-190">tooensure this, click **File**, click **Project Structure**, and on hello **Project** tab, make sure Project language level is set too**8 - Lambdas, type annotations, etc.**.</span></span>
   
    <span data-ttu-id="09111-191">![Apache Spark-streaming-voorbeeld - Set compiler](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark-streaming-voorbeeld: Set-compiler")</span><span class="sxs-lookup"><span data-stu-id="09111-191">![Apache Spark streaming example - Set compiler](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-java-8-compiler.png "Apache Spark streaming example - Set compiler")</span></span>
5. <span data-ttu-id="09111-192">Open Hallo **pom.xml** en zorg ervoor dat Hallo Spark versie juist is.</span><span class="sxs-lookup"><span data-stu-id="09111-192">Open hello **pom.xml** and make sure hello Spark version is correct.</span></span> <span data-ttu-id="09111-193">Onder `<properties>` knooppunt, zoekt u naar Hallo volgende codefragment en controleer of Hallo Spark versie.</span><span class="sxs-lookup"><span data-stu-id="09111-193">Under `<properties>` node, look for hello following snippet and verify hello Spark version.</span></span>

        <scala.version>2.11.8</scala.version>
        <scala.compat.version>2.11.8</scala.compat.version>
        <scala.binary.version>2.11</scala.binary.version>
        <spark.version>2.0.0</spark.version>

6. <span data-ttu-id="09111-194">Hallo toepassing vereist een afhankelijkheid jar aangeroepen **JDBC-stuurprogramma jar**.</span><span class="sxs-lookup"><span data-stu-id="09111-194">hello application requires a dependency jar called **JDBC driver jar**.</span></span> <span data-ttu-id="09111-195">Dit is vereiste toowrite Hallo-berichten ontvangen van de Event Hub naar een Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="09111-195">This is required toowrite hello messages received from Event Hub into an Azure SQL database.</span></span> <span data-ttu-id="09111-196">U kunt deze jar downloaden (v4.1 of hoger) van [hier](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span><span class="sxs-lookup"><span data-stu-id="09111-196">You can download this jar (v4.1 or later) from [here](https://msdn.microsoft.com/sqlserver/aa937724.aspx).</span></span> <span data-ttu-id="09111-197">Verwijzing toothis jar in Hallo project bibliotheek toevoegen.</span><span class="sxs-lookup"><span data-stu-id="09111-197">Add reference toothis jar in hello project library.</span></span> <span data-ttu-id="09111-198">Voer Hallo stappen te volgen:</span><span class="sxs-lookup"><span data-stu-id="09111-198">Perform hello following steps:</span></span>
     
     1. <span data-ttu-id="09111-199">Vanuit IntelliJ IDEA venster waarin het hebben van Hallo toepassing openen, klikt u op **bestand**, klikt u op **projectstructuur**, en klik vervolgens op **bibliotheken**.</span><span class="sxs-lookup"><span data-stu-id="09111-199">From IntelliJ IDEA window where you have hello application open, click **File**, click **Project Structure**, and then click **Libraries**.</span></span> 
     2. <span data-ttu-id="09111-200">Klik op Hallo pictogram toevoegen (![pictogram toevoegen](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), klikt u op **Java**, en navigeert u vervolgens toohello locatie waar u Hallo JDBC-stuurprogramma jar hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="09111-200">Click hello add icon (![add icon](./media/hdinsight-apache-spark-eventhub-streaming/add-icon.png)), click **Java**, and then navigate toohello location where you downloaded hello JDBC driver jar.</span></span> <span data-ttu-id="09111-201">Ga als volgt Hallo prompts tooadd Hallo jar-bestand toohello project bibliotheek.</span><span class="sxs-lookup"><span data-stu-id="09111-201">Follow hello prompts tooadd hello jar file toohello project library.</span></span>

         <span data-ttu-id="09111-202">![ontbrekende afhankelijkheden toevoegen](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "ontbrekende afhankelijkheid potten toevoegen")</span><span class="sxs-lookup"><span data-stu-id="09111-202">![add missing dependencies](./media/hdinsight-apache-spark-eventhub-streaming/add-missing-dependency-jars.png "Add missing dependency jars")</span></span>
     3. <span data-ttu-id="09111-203">Klik op **Toepassen**.</span><span class="sxs-lookup"><span data-stu-id="09111-203">Click **Apply**.</span></span>

7. <span data-ttu-id="09111-204">Hallo uitvoer jar-bestand maken.</span><span class="sxs-lookup"><span data-stu-id="09111-204">Create hello output jar file.</span></span> <span data-ttu-id="09111-205">Hallo stappen uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="09111-205">Perform hello following steps.</span></span>

   1. <span data-ttu-id="09111-206">In Hallo **projectstructuur** in het dialoogvenster, klikt u op **artefacten** en klik vervolgens op Hallo plus symbool.</span><span class="sxs-lookup"><span data-stu-id="09111-206">In hello **Project Structure** dialog box, click **Artifacts** and then click hello plus symbol.</span></span> <span data-ttu-id="09111-207">Klik in het pop-updialoogvenster hello, op **JAR**, en klik vervolgens op **van modules met afhankelijkheden**.</span><span class="sxs-lookup"><span data-stu-id="09111-207">From hello pop-up dialog box, click **JAR**, and then click **From modules with dependencies**.</span></span>      
       
       <span data-ttu-id="09111-208">![Apache Spark streaming voorbeeld - JAR maken](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "streaming voorbeeld Apache Spark - JAR maken")</span><span class="sxs-lookup"><span data-stu-id="09111-208">![Apache Spark streaming example - create JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar.png "Apache Spark streaming example - create JAR")</span></span>
   2. <span data-ttu-id="09111-209">In Hallo **maken JAR van Modules** dialoogvenster vak, klikt u op Hallo weglatingsteken (![weglatingsteken](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) tegen Hallo **Main klasse**.</span><span class="sxs-lookup"><span data-stu-id="09111-209">In hello **Create JAR from Modules** dialog box, click hello ellipsis (![ellipsis](./media/hdinsight-apache-spark-eventhub-streaming/ellipsis.png)) against hello **Main Class**.</span></span>
   3. <span data-ttu-id="09111-210">In Hallo **Main-klasse selecteren** dialoogvenster vak, selecteert u een van de beschikbare klassen Hallo en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="09111-210">In hello **Select Main Class** dialog box, select any of hello available classes and then click **OK**.</span></span>
      
       <span data-ttu-id="09111-211">![Apache Spark-streaming-voorbeeld - Selecteer klasse voor jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark-streaming-voorbeeld - Selecteer klasse voor jar")</span><span class="sxs-lookup"><span data-stu-id="09111-211">![Apache Spark streaming example - select class for jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-select-class-for-jar.png "Apache Spark streaming example - select class for jar")</span></span>
   4. <span data-ttu-id="09111-212">In Hallo **maken JAR van Modules** dialoogvenster zorg die optie hello te**toohello doel JAR extraheren** is geselecteerd en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="09111-212">In hello **Create JAR from Modules** dialog box, make sure that hello option too**extract toohello target JAR** is selected, and then click **OK**.</span></span> <span data-ttu-id="09111-213">Hiermee maakt u een één JAR met alle afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="09111-213">This creates a single JAR with all dependencies.</span></span>
      
       <span data-ttu-id="09111-214">![Apache Spark streaming voorbeeld - jar maken van modules](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "streaming voorbeeld Apache Spark - jar van modules maken")</span><span class="sxs-lookup"><span data-stu-id="09111-214">![Apache Spark streaming example - create jar from modules](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-create-jar-from-modules.png "Apache Spark streaming example - create jar from modules")</span></span>
   5. <span data-ttu-id="09111-215">Hallo **uitvoer indeling** tabblad bevat alle Hallo potten die opgenomen als onderdeel van Hallo Maven-project zijn.</span><span class="sxs-lookup"><span data-stu-id="09111-215">hello **Output Layout** tab lists all hello jars that are included as part of hello Maven project.</span></span> <span data-ttu-id="09111-216">U kunt selecteren en delete Hallo toepassingsgroepen waarop Scala toepassing hello heeft geen directe afhankelijkheid.</span><span class="sxs-lookup"><span data-stu-id="09111-216">You can select and delete hello ones on which hello Scala application has no direct dependency.</span></span> <span data-ttu-id="09111-217">Voor de toepassing hello hier maakt, kunt u alle maar Hallo laatste (**spark-streaming-gegevens-persistentie-voorbeelden gecompileerd uitvoer**).</span><span class="sxs-lookup"><span data-stu-id="09111-217">For hello application we are creating here, you can remove all but hello last one (**spark-streaming-data-persistence-examples compile output**).</span></span> <span data-ttu-id="09111-218">Hallo potten toodelete selecteren en klik vervolgens op Hallo **verwijderen** pictogram (![pictogram verwijderen](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span><span class="sxs-lookup"><span data-stu-id="09111-218">Select hello jars toodelete and then click hello **Delete** icon (![delete icon](./media/hdinsight-apache-spark-eventhub-streaming/delete-icon.png)).</span></span>
      
       <span data-ttu-id="09111-219">![Apache Spark-streaming-voorbeeld - delete uitgepakt potten](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark-streaming-voorbeeld - potten uitgepakt verwijderen")</span><span class="sxs-lookup"><span data-stu-id="09111-219">![Apache Spark streaming example - delete extracted jars](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-delete-output-jars.png "Apache Spark streaming example - delete extracted jars")</span></span>
      
       <span data-ttu-id="09111-220">Zorg ervoor dat **bouwen op Controleer** selectievakje is ingeschakeld, waardoor wordt gegarandeerd dat jar hello wordt gemaakt telkens wanneer Hallo-project wordt gemaakt of bijgewerkt.</span><span class="sxs-lookup"><span data-stu-id="09111-220">Make sure **Build on make** box is selected, which ensures that hello jar is created every time hello project is built or updated.</span></span> <span data-ttu-id="09111-221">Klik op **Toepassen**.</span><span class="sxs-lookup"><span data-stu-id="09111-221">Click **Apply**.</span></span>
   6. <span data-ttu-id="09111-222">In Hallo **uitvoer indeling** tabblad rechts onderin Hallo Hallo **beschikbare elementen** vak hebt Hallo SQL JDBC jar dat u eerder toohello project bibliotheek toegevoegd.</span><span class="sxs-lookup"><span data-stu-id="09111-222">In hello **Output Layout** tab, right at hello bottom of hello **Available Elements** box, you have hello SQL JDBC jar that you added earlier toohello project library.</span></span> <span data-ttu-id="09111-223">U moet deze toohello toevoegen **uitvoer indeling** tabblad. Met de rechtermuisknop op Hallo jar-bestand en klik vervolgens op **uitpakken naar uitvoer hoofdmap**.</span><span class="sxs-lookup"><span data-stu-id="09111-223">You must add this toohello **Output Layout** tab. Right-click hello jar file, and then click **Extract Into Output Root**.</span></span>
      
       <span data-ttu-id="09111-224">![Apache Spark-streaming-voorbeeld - extract afhankelijkheid jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark-streaming-voorbeeld - extract afhankelijkheid jar")</span><span class="sxs-lookup"><span data-stu-id="09111-224">![Apache Spark streaming example - extract dependency jar](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-extract-dependency-jar.png "Apache Spark streaming example - extract dependency jar")</span></span>  
      
       <span data-ttu-id="09111-225">Hallo **uitvoer indeling** tabblad ziet er nu als volgt.</span><span class="sxs-lookup"><span data-stu-id="09111-225">hello **Output Layout** tab should now look like this.</span></span>
      
       <span data-ttu-id="09111-226">![Apache Spark-streaming-voorbeeld - uiteindelijke uitvoer tabblad](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark-streaming-voorbeeld - tabblad uiteindelijke uitvoer")</span><span class="sxs-lookup"><span data-stu-id="09111-226">![Apache Spark streaming example - final output tab](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-final-output-tab.png "Apache Spark streaming example - final output tab")</span></span>        
      
       <span data-ttu-id="09111-227">In Hallo **projectstructuur** in het dialoogvenster, klikt u op **toepassen** en klik vervolgens op **OK**.</span><span class="sxs-lookup"><span data-stu-id="09111-227">In hello **Project Structure** dialog box, click **Apply** and then click **OK**.</span></span>    
   7. <span data-ttu-id="09111-228">In de menubalk hello, klikt u op **bouwen**, en klik vervolgens op **Project maken**.</span><span class="sxs-lookup"><span data-stu-id="09111-228">From hello menu bar, click **Build**, and then click **Make Project**.</span></span> <span data-ttu-id="09111-229">U kunt ook klikken op **bouwen artefacten** toocreate Hallo jar.</span><span class="sxs-lookup"><span data-stu-id="09111-229">You can also click **Build Artifacts** toocreate hello jar.</span></span> <span data-ttu-id="09111-230">Hallo uitvoer jar gemaakt onder **\classes\artifacts**.</span><span class="sxs-lookup"><span data-stu-id="09111-230">hello output jar is created under **\classes\artifacts**.</span></span>
      
       <span data-ttu-id="09111-231">![Apache Spark streaming voorbeeld - uitvoer JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "streaming voorbeeld Apache Spark - uitvoer JAR")</span><span class="sxs-lookup"><span data-stu-id="09111-231">![Apache Spark streaming example - output JAR](./media/hdinsight-apache-spark-eventhub-streaming/spark-streaming-example-output-jar.png "Apache Spark streaming example - output JAR")</span></span>

## <a name="run-hello-application-remotely-on-a-spark-cluster-using-livy"></a><span data-ttu-id="09111-232">Hallo-toepassing op afstand uitvoeren op een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="09111-232">Run hello application remotely on a Spark cluster using Livy</span></span>

<span data-ttu-id="09111-233">In dit artikel gebruikt u Livy toorun Hallo Apache Spark-streaming toepassing op afstand op een Spark-cluster.</span><span class="sxs-lookup"><span data-stu-id="09111-233">In this article you use Livy toorun hello Apache Spark streaming application remotely on a Spark cluster.</span></span> <span data-ttu-id="09111-234">Zie voor gedetailleerde informatie over hoe toouse Livy met HDInsight Spark-cluster, [indienen taken op afstand tooan Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span><span class="sxs-lookup"><span data-stu-id="09111-234">For detailed discussion on how toouse Livy with HDInsight Spark cluster, see [Submit jobs remotely tooan Apache Spark cluster on Azure HDInsight](hdinsight-apache-spark-livy-rest-interface.md).</span></span> <span data-ttu-id="09111-235">Voordat u kunt Hallo Spark-streaming toepassing uitvoert, zijn er zijn een aantal dingen die u moet doen:</span><span class="sxs-lookup"><span data-stu-id="09111-235">Before you can start running hello Spark streaming application, there are a couple of things you should do:</span></span>

1. <span data-ttu-id="09111-236">Hallo lokale zelfstandige toepassingsgebeurtenissen toogenerate Start en tooEvent Hub verzonden.</span><span class="sxs-lookup"><span data-stu-id="09111-236">Start hello local standalone application toogenerate events and sent tooEvent Hub.</span></span> <span data-ttu-id="09111-237">Hallo opdracht toodo dus volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="09111-237">Use hello following command toodo so:</span></span>

        java -cp com-microsoft-azure-eventhubs-client-example-0.2.0.jar com.microsoft.eventhubs.client.example.EventhubsClientDriver --eventhubs-namespace "mysbnamespace" --eventhubs-name "myeventhub" --policy-name "mysendpolicy" --policy-key "<policy key>" --message-length 32 --thread-count 32 --message-count -1

2. <span data-ttu-id="09111-238">Kopiëren Hallo jar streaming (**spark-streaming-gegevens-persistentie-examples.jar**) toohello Azure Blob-opslag die is gekoppeld aan het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="09111-238">Copy hello streaming jar (**spark-streaming-data-persistence-examples.jar**) toohello Azure Blob storage associated with hello cluster.</span></span> <span data-ttu-id="09111-239">Hierdoor Hallo jar toegankelijk tooLivy.</span><span class="sxs-lookup"><span data-stu-id="09111-239">This makes hello jar accessible tooLivy.</span></span> <span data-ttu-id="09111-240">U kunt [ **AzCopy**](../storage/common/storage-use-azcopy.md), een opdracht hulpprogramma toodo dus regel.</span><span class="sxs-lookup"><span data-stu-id="09111-240">You can use [**AzCopy**](../storage/common/storage-use-azcopy.md), a command line utility, toodo so.</span></span> <span data-ttu-id="09111-241">Er zijn veel andere clients kunt u tooupload gegevens.</span><span class="sxs-lookup"><span data-stu-id="09111-241">There are a lot of other clients you can use tooupload data.</span></span> <span data-ttu-id="09111-242">U vindt meer informatie hierover op [gegevens voor Hadoop-taken in HDInsight uploaden](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="09111-242">You can find more about them at [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>
3. <span data-ttu-id="09111-243">Installeer CURL op Hallo-computer waarop u deze toepassingen worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="09111-243">Install CURL on hello computer where you are running these applications from.</span></span> <span data-ttu-id="09111-244">We gebruiken CURL tooinvoke hello Livy eindpunten toorun Hallo op afstand taken.</span><span class="sxs-lookup"><span data-stu-id="09111-244">We use CURL tooinvoke hello Livy endpoints toorun hello jobs remotely.</span></span>

### <a name="run-hello-spark-streaming-application-tooreceive-hello-events-into-an-azure-storage-blob-as-text"></a><span data-ttu-id="09111-245">Hallo Spark streaming tooreceive Hallo toepassingsgebeurtenissen uitvoeren in een Azure Storage-Blob als tekst</span><span class="sxs-lookup"><span data-stu-id="09111-245">Run hello Spark streaming application tooreceive hello events into an Azure Storage Blob as text</span></span>

<span data-ttu-id="09111-246">Open een opdrachtprompt, navigeer toohello directory waarin u CURL hebt geïnstalleerd en Voer Hallo opdracht (vervangen gebruikersnaam en wachtwoord en het cluster name) te volgen:</span><span class="sxs-lookup"><span data-stu-id="09111-246">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputBlob.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="09111-247">parameters in bestand Hallo Hallo **inputBlob.txt** als volgt gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="09111-247">hello parameters in hello file **inputBlob.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsEventCount", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="09111-248">Laat het ons weten wat Hallo-parameters in het invoerbestand Hallo zijn:</span><span class="sxs-lookup"><span data-stu-id="09111-248">Let us understand what hello parameters in hello input file are:</span></span>

* <span data-ttu-id="09111-249">**bestand** Hallo pad toohello toepassing jar-bestand op Hallo Azure storage-account is gekoppeld aan het Hallo-cluster is.</span><span class="sxs-lookup"><span data-stu-id="09111-249">**file** is hello path toohello application jar file on hello Azure storage account associated with hello cluster.</span></span>
* <span data-ttu-id="09111-250">**className** Hallo naam is van het Hallo-klasse in Hallo jar.</span><span class="sxs-lookup"><span data-stu-id="09111-250">**className** is hello name of hello class in hello jar.</span></span>
* <span data-ttu-id="09111-251">**argumenten** Hallo lijst met argumenten dat is vereist door Hallo-klasse</span><span class="sxs-lookup"><span data-stu-id="09111-251">**args** is hello list of arguments required by hello class</span></span>
* <span data-ttu-id="09111-252">**numExecutors** Hallo aantal kernen die wordt gebruikt door Spark toorun Hallo streaming van toepassing is.</span><span class="sxs-lookup"><span data-stu-id="09111-252">**numExecutors** is hello number of cores used by Spark toorun hello streaming application.</span></span> <span data-ttu-id="09111-253">Dit moet altijd ten minste tweemaal Hallo aantal Event Hub-partities.</span><span class="sxs-lookup"><span data-stu-id="09111-253">This should always be at least twice hello number of Event Hub partitions.</span></span>
* <span data-ttu-id="09111-254">**executorMemory**, **executorCores**, **driverMemory** zijn parameters gebruikt tooassign vereist resources toohello streaming-toepassing.</span><span class="sxs-lookup"><span data-stu-id="09111-254">**executorMemory**, **executorCores**, **driverMemory** are parameters used tooassign required resources toohello streaming application.</span></span>

> [!NOTE]
> <span data-ttu-id="09111-255">U hoeft niet toocreate Hallo uitvoermappen (EventCheckpoint, EventCount/EventCount10) die worden gebruikt als parameters.</span><span class="sxs-lookup"><span data-stu-id="09111-255">You do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="09111-256">streaming-toepassing Hello ze voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="09111-256">hello streaming application creates them for you.</span></span>
>
>

<span data-ttu-id="09111-257">Wanneer u Hallo-opdracht uitvoert, ziet u uitvoer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="09111-257">When you run hello command, you should see an output like hello following:</span></span>

    < HTTP/1.1 201 Created
    < Content-Type: application/json; charset=UTF-8
    < Location: /18
    < Server: Microsoft-IIS/8.5
    < X-Powered-By: ARR/2.5
    < X-Powered-By: ASP.NET
    < Date: Tue, 01 Dec 2015 05:39:10 GMT
    < Content-Length: 37
    <
    {"id":1,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact

<span data-ttu-id="09111-258">Noteer Hallo batch-ID in de laatste regel Hallo van Hallo uitvoer (in dit voorbeeld is '1').</span><span class="sxs-lookup"><span data-stu-id="09111-258">Make a note of hello batch ID in hello last line of hello output (in this example it is '1').</span></span> <span data-ttu-id="09111-259">tooverify die toepassing hello met succes wordt uitgevoerd, kunt u uw Azure storage-account die is gekoppeld aan cluster Hallo bekijken en ziet u Hallo **/EventCount/EventCount10** map er hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="09111-259">tooverify that hello application runs successfully, you can look at your Azure storage account associated with hello cluster and you should see hello **/EventCount/EventCount10** folder created there.</span></span> <span data-ttu-id="09111-260">Deze map moet bevatten blobs die worden vastgelegd Hallo aantal gebeurtenissen dat is verwerkt in Hallo periode opgegeven voor parameter Hallo **batch interval in seconden**.</span><span class="sxs-lookup"><span data-stu-id="09111-260">This folder should contain blobs that captures hello number of events processed within hello time period specified for hello parameter **batch-interval-in-seconds**.</span></span>

<span data-ttu-id="09111-261">Hallo Spark-streaming toepassing blijft toorun totdat u het afsluiten.</span><span class="sxs-lookup"><span data-stu-id="09111-261">hello Spark streaming application will continue toorun until you kill it.</span></span> <span data-ttu-id="09111-262">toodo gebruik dus Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="09111-262">toodo so, use hello following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/1"

### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-storage-blob-as-json"></a><span data-ttu-id="09111-263">Hallo toepassingen uitvoeren tooreceive Hallo gebeurtenissen in een Azure Storage-Blob als JSON</span><span class="sxs-lookup"><span data-stu-id="09111-263">Run hello applications tooreceive hello events into an Azure Storage Blob as JSON</span></span>
<span data-ttu-id="09111-264">Open een opdrachtprompt, navigeer toohello directory waarin u CURL hebt geïnstalleerd en Voer Hallo opdracht (vervangen gebruikersnaam en wachtwoord en het cluster name) te volgen:</span><span class="sxs-lookup"><span data-stu-id="09111-264">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputJSON.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="09111-265">parameters in bestand Hallo Hallo **inputJSON.txt** als volgt gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="09111-265">hello parameters in hello file **inputJSON.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureBlobAsJSON", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-store-folder", "/EventStore10"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="09111-266">Hallo-parameters zijn vergelijkbaar toowhat die u hebt opgegeven voor de tekstuitvoer Hallo in de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="09111-266">hello parameters are similar toowhat you specified for hello text output, in hello previous step.</span></span> <span data-ttu-id="09111-267">Opnieuw, hoeft u niet toocreate Hallo uitvoermappen (EventCheckpoint, EventCount/EventCount10) die worden gebruikt als parameters.</span><span class="sxs-lookup"><span data-stu-id="09111-267">Again, you do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) that are used as parameters.</span></span> <span data-ttu-id="09111-268">streaming-toepassing Hello ze voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="09111-268">hello streaming application creates them for you.</span></span>

 <span data-ttu-id="09111-269">Nadat u Hallo-opdracht uitvoert, u uw Azure storage-account die is gekoppeld aan cluster Hallo bekijken kunt en u Hallo ziet **/EventStore10** map er hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="09111-269">After you run hello command, you can look at your Azure storage account associated with hello cluster and you should see hello **/EventStore10** folder created there.</span></span> <span data-ttu-id="09111-270">Open elk bestand voorafgegaan door **onderdeel -** en ziet u Hallo gebeurtenissen in een JSON-indeling wordt verwerkt.</span><span class="sxs-lookup"><span data-stu-id="09111-270">Open any file prefixed with **part-** and you should see hello events processed in a JSON format.</span></span>

### <a name="run-hello-applications-tooreceive-hello-events-into-a-hive-table"></a><span data-ttu-id="09111-271">Hallo toepassingen tooreceive Hallo gebeurtenissen uitvoeren in een Hive-tabel</span><span class="sxs-lookup"><span data-stu-id="09111-271">Run hello applications tooreceive hello events into a Hive table</span></span>
<span data-ttu-id="09111-272">toorun hello Spark-streaming toepassing streams gebeurtenissen in een component tabel u moet een aantal extra onderdelen.</span><span class="sxs-lookup"><span data-stu-id="09111-272">toorun hello Spark streaming application that streams events into a Hive table you need some additional components.</span></span> <span data-ttu-id="09111-273">Dit zijn:</span><span class="sxs-lookup"><span data-stu-id="09111-273">These are:</span></span>

* <span data-ttu-id="09111-274">datanucleus api-jdo 3.2.6.jar</span><span class="sxs-lookup"><span data-stu-id="09111-274">datanucleus-api-jdo-3.2.6.jar</span></span>
* <span data-ttu-id="09111-275">datanucleus-rdbms-3.2.9.jar</span><span class="sxs-lookup"><span data-stu-id="09111-275">datanucleus-rdbms-3.2.9.jar</span></span>
* <span data-ttu-id="09111-276">datanucleus-core-3.2.10.jar</span><span class="sxs-lookup"><span data-stu-id="09111-276">datanucleus-core-3.2.10.jar</span></span>
* <span data-ttu-id="09111-277">hive-site.xml</span><span class="sxs-lookup"><span data-stu-id="09111-277">hive-site.xml</span></span>

<span data-ttu-id="09111-278">Hallo **JAR** bestanden zijn beschikbaar op uw HDInsight Spark-cluster op `/usr/hdp/current/spark-client/lib`.</span><span class="sxs-lookup"><span data-stu-id="09111-278">hello **.jar** files are available on your HDInsight Spark cluster at `/usr/hdp/current/spark-client/lib`.</span></span> <span data-ttu-id="09111-279">Hallo **hive-site.xml** is beschikbaar op `/usr/hdp/current/spark-client/conf`.</span><span class="sxs-lookup"><span data-stu-id="09111-279">hello **hive-site.xml** is available at `/usr/hdp/current/spark-client/conf`.</span></span>

<span data-ttu-id="09111-280">U kunt [WinScp](http://winscp.net/eng/download.php) toocopy via deze bestanden vanaf Hallo cluster tooyour lokale computer.</span><span class="sxs-lookup"><span data-stu-id="09111-280">You can use [WinScp](http://winscp.net/eng/download.php) toocopy over these files from hello cluster tooyour local computer.</span></span> <span data-ttu-id="09111-281">Vervolgens kunt u extra toocopy deze bestanden via tooyour storage-account die is gekoppeld aan het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="09111-281">You can then use tools toocopy these files over tooyour storage account associated with hello cluster.</span></span> <span data-ttu-id="09111-282">Zie voor meer informatie over hoe tooupload toohello opslagaccount bestanden, [gegevens voor Hadoop-taken in HDInsight uploaden](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="09111-282">For more information on how tooupload files toohello storage account, see [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md).</span></span>

<span data-ttu-id="09111-283">Zodra u hebt gekopieerd via Hallo bestanden tooyour Azure storage-account, open een opdrachtprompt, navigeer toohello directory waarin u CURL hebt geïnstalleerd en Voer Hallo opdracht (vervangen gebruikersnaam en wachtwoord en het cluster name) te volgen:</span><span class="sxs-lookup"><span data-stu-id="09111-283">Once you have copied over hello files tooyour Azure storage account, open a command prompt, navigate toohello directory where you installed CURL, and run hello following command (replace username/password and cluster name):</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputHive.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="09111-284">parameters in bestand Hallo Hallo **inputHive.txt** als volgt gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="09111-284">hello parameters in hello file **inputHive.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToHiveTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--event-hive-table", "EventHiveTable10" ], "jars":["wasb:///example/jars/datanucleus-api-jdo-3.2.6.jar", "wasb:///example/jars/datanucleus-rdbms-3.2.9.jar", "wasb:///example/jars/datanucleus-core-3.2.10.jar"], "files":["wasb:///example/jars/hive-site.xml"], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="09111-285">Hallo-parameters zijn vergelijkbaar toowhat die u hebt opgegeven voor de tekstuitvoer Hallo in de vorige stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="09111-285">hello parameters are similar toowhat you specified for hello text output, in hello previous steps.</span></span> <span data-ttu-id="09111-286">Opnieuw, hoeft u geen toocreate Hallo uitvoer mappen (EventCheckpoint, EventCount/EventCount10) of Hallo uitvoer Hive-tabel (EventHiveTable10) die worden gebruikt als parameters.</span><span class="sxs-lookup"><span data-stu-id="09111-286">Again, you do not need toocreate hello output folders (EventCheckpoint, EventCount/EventCount10) or hello output Hive table (EventHiveTable10) that are used as parameters.</span></span> <span data-ttu-id="09111-287">streaming-toepassing Hello ze voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="09111-287">hello streaming application creates them for you.</span></span> <span data-ttu-id="09111-288">Houd er rekening mee dat Hallo **potten** en **bestanden** optie omvat paden toohello JAR-bestanden en Hallo hive-site.xml die u hebt gekopieerd via toohello storage-account.</span><span class="sxs-lookup"><span data-stu-id="09111-288">Note that hello **jars** and **files** option includes paths toohello .jar files and hello hive-site.xml that you copied over toohello storage account.</span></span>

<span data-ttu-id="09111-289">tooverify die Hallo hive-tabel is gemaakt, kunt u SSH in Hallo-cluster en Hive-query's uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="09111-289">tooverify that hello hive table was successfully created, you can SSH into hello cluster and run Hive queries.</span></span> <span data-ttu-id="09111-290">Zie voor instructies [Hive gebruiken met Hadoop in HDInsight met SSH](hdinsight-hadoop-use-hive-ssh.md).</span><span class="sxs-lookup"><span data-stu-id="09111-290">For instructions, see [Use Hive with Hadoop in HDInsight with SSH](hdinsight-hadoop-use-hive-ssh.md).</span></span> <span data-ttu-id="09111-291">Zodra u met het gebruik van SSH verbonden bent, kunt u uitvoeren na de opdracht tooverify Hallo die Hallo Hive-tabel **EventHiveTable10**, wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="09111-291">Once you are connected using SSH, you can run hello following command tooverify that hello Hive table, **EventHiveTable10**, is created.</span></span>

    show tables;

<span data-ttu-id="09111-292">U ziet een uitvoer vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="09111-292">You should see an output similar toohello following:</span></span>

    OK
    eventhivetable10
    hivesampletable

<span data-ttu-id="09111-293">U kunt een SELECT-query ook tooview Hallo inhoud van Hallo tabel uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="09111-293">You can also run a SELECT query tooview hello contents of hello table.</span></span>

    SELECT * FROM eventhivetable10 LIMIT 10;

<span data-ttu-id="09111-294">Hier ziet u uitvoer Hallo volgende:</span><span class="sxs-lookup"><span data-stu-id="09111-294">You should see an output like hello following:</span></span>

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


### <a name="run-hello-applications-tooreceive-hello-events-into-an-azure-sql-database-table"></a><span data-ttu-id="09111-295">Hallo toepassingen tooreceive Hallo gebeurtenissen uitvoeren in een Azure SQL-databasetabel</span><span class="sxs-lookup"><span data-stu-id="09111-295">Run hello applications tooreceive hello events into an Azure SQL database table</span></span>
<span data-ttu-id="09111-296">Voordat u deze stap uitvoert, zorg ervoor dat u hebt een Azure SQL-database gemaakt.</span><span class="sxs-lookup"><span data-stu-id="09111-296">Before running this step, make sure you have an Azure SQL database created.</span></span> <span data-ttu-id="09111-297">Zie voor instructies [maken van een SQL-database in minuten](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="09111-297">For instructions, see [Create a SQL database in minutes](../sql-database/sql-database-get-started.md).</span></span> <span data-ttu-id="09111-298">toocomplete dit sectie, moet u waarden voor de databasenaam, database-servernaam en Hallo database beheerdersreferenties als parameters.</span><span class="sxs-lookup"><span data-stu-id="09111-298">toocomplete this section, you need values for database name, database server name, and hello database administrator credentials as parameters.</span></span> <span data-ttu-id="09111-299">U hoeft niet toocreate Hallo databasetabel al.</span><span class="sxs-lookup"><span data-stu-id="09111-299">You do not need toocreate hello database table though.</span></span> <span data-ttu-id="09111-300">Hallo Spark-streaming toepassing die voor u gemaakt.</span><span class="sxs-lookup"><span data-stu-id="09111-300">hello Spark streaming application creates that for you.</span></span>

<span data-ttu-id="09111-301">Open een opdrachtprompt, navigeer toohello directory waarin u CURL hebt geïnstalleerd en Voer Hallo volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="09111-301">Open a command prompt, navigate toohello directory where you installed CURL, and run hello following command:</span></span>

    curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\inputSQL.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

<span data-ttu-id="09111-302">parameters in bestand Hallo Hallo **inputSQL.txt** als volgt gedefinieerd:</span><span class="sxs-lookup"><span data-stu-id="09111-302">hello parameters in hello file **inputSQL.txt** are defined as follows:</span></span>

    { "file":"wasb:///example/jars/spark-streaming-data-persistence-examples.jar", "className":"com.microsoft.spark.streaming.examples.workloads.EventhubsToAzureSQLTable", "args":["--eventhubs-namespace", "mysbnamespace", "--eventhubs-name", "myeventhub", "--policy-name", "myreceivepolicy", "--policy-key", "<put-your-key-here>", "--consumer-group", "$default", "--partition-count", 10, "--batch-interval-in-seconds", 20, "--checkpoint-directory", "/EventCheckpoint", "--event-count-folder", "/EventCount/EventCount10", "--sql-server-fqdn", "<database-server-name>.database.windows.net", "--sql-database-name", "mysparkdatabase", "--database-username", "sparkdbadmin", "--database-password", "<put-password-here>", "--event-sql-table", "EventContent" ], "numExecutors":20, "executorMemory":"1G", "executorCores":1, "driverMemory":"2G" }

<span data-ttu-id="09111-303">tooverify die toepassing hello met succes wordt uitgevoerd, kunt u toohello Azure SQL database met behulp van SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="09111-303">tooverify that hello application runs successfully, you can connect toohello Azure SQL database using SQL Server Management Studio.</span></span> <span data-ttu-id="09111-304">Voor instructies over het toodo die Zie [tooSQL Database met SQL Server Management Studio verbinding](../sql-database/sql-database-connect-query-ssms.md).</span><span class="sxs-lookup"><span data-stu-id="09111-304">For instructions on how toodo that, see [Connect tooSQL Database with SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md).</span></span> <span data-ttu-id="09111-305">Wanneer u verbonden toohello database bent, kunt u navigeren toohello **EventContent** tabel die is gemaakt door Hallo streaming-toepassing.</span><span class="sxs-lookup"><span data-stu-id="09111-305">Once you are connected toohello database, you can navigate toohello **EventContent** table that was created by hello streaming application.</span></span> <span data-ttu-id="09111-306">U kunt een snelle tooget Hallo querygegevens uit Hallo tabel uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="09111-306">You can run a quick query tooget hello data from hello table.</span></span> <span data-ttu-id="09111-307">Voer Hallo query te volgen:</span><span class="sxs-lookup"><span data-stu-id="09111-307">Run hello following query:</span></span>

    SELECT * FROM EventCount

<span data-ttu-id="09111-308">Hier ziet u uitvoer vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="09111-308">You should see output similar toohello following:</span></span>

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


## <span data-ttu-id="09111-309"><a name="seealso"></a>Zie ook</span><span class="sxs-lookup"><span data-stu-id="09111-309"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="09111-310">Overzicht: Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="09111-310">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)
* [<span data-ttu-id="09111-311">Ontwerp van de verbinding op basis van de ontvanger en Direct DStream</span><span class="sxs-lookup"><span data-stu-id="09111-311">Design of Receiver-based Connection and Direct DStream</span></span>](https://www.slideshare.net/NanZhu/seattle-sparkmeetup032317)

### <a name="scenarios"></a><span data-ttu-id="09111-312">Scenario's</span><span class="sxs-lookup"><span data-stu-id="09111-312">Scenarios</span></span>
* [<span data-ttu-id="09111-313">Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools</span><span class="sxs-lookup"><span data-stu-id="09111-313">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="09111-314">Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens</span><span class="sxs-lookup"><span data-stu-id="09111-314">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="09111-315">Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken</span><span class="sxs-lookup"><span data-stu-id="09111-315">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="09111-316">Websitelogboekanalyse met Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="09111-316">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="09111-317">Toepassingen maken en uitvoeren</span><span class="sxs-lookup"><span data-stu-id="09111-317">Create and run applications</span></span>
* [<span data-ttu-id="09111-318">Een zelfstandige toepassing maken met behulp van Scala</span><span class="sxs-lookup"><span data-stu-id="09111-318">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="09111-319">Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy</span><span class="sxs-lookup"><span data-stu-id="09111-319">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="09111-320">Tools en uitbreidingen</span><span class="sxs-lookup"><span data-stu-id="09111-320">Tools and extensions</span></span>
* [<span data-ttu-id="09111-321">De invoegtoepassing HDInsight Tools voor toocreate IntelliJ IDEA gebruiken en het verzenden van Spark Scala-toepassingen</span><span class="sxs-lookup"><span data-stu-id="09111-321">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="09111-322">De invoegtoepassing HDInsight Tools for IntelliJ IDEA toodebug Spark applications op afstand gebruiken</span><span class="sxs-lookup"><span data-stu-id="09111-322">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="09111-323">Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight</span><span class="sxs-lookup"><span data-stu-id="09111-323">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="09111-324">Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="09111-324">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="09111-325">Externe pakketten gebruiken met Jupyter-notebooks</span><span class="sxs-lookup"><span data-stu-id="09111-325">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="09111-326">Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster</span><span class="sxs-lookup"><span data-stu-id="09111-326">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="09111-327">Resources beheren</span><span class="sxs-lookup"><span data-stu-id="09111-327">Manage resources</span></span>
* [<span data-ttu-id="09111-328">Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="09111-328">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="09111-329">Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen</span><span class="sxs-lookup"><span data-stu-id="09111-329">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]: ../storage-create-storage-account/
