---
title: aaaProcess gebeurtenissen van Event Hubs met Storm - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe tooprocess gegevens uit Azure Event Hubs met een C# Storm-topologie gemaakt in Visual Studio met Hallo HDInsight tools voor Visual Studio.
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 67f9d08c-eea0-401b-952b-db765655dad0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 30cd910d80eba066f283197bcbbaf11145bc5524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a><span data-ttu-id="3ed23-103">Procesgebeurtenissen van Azure Event Hubs met Storm op HDInsight (C#)</span><span class="sxs-lookup"><span data-stu-id="3ed23-103">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>

<span data-ttu-id="3ed23-104">Meer informatie over hoe toowork met Azure Event Hubs van Apache Storm op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3ed23-104">Learn how toowork with Azure Event Hubs from Apache Storm on HDInsight.</span></span> <span data-ttu-id="3ed23-105">Dit document wordt een C# Storm-topologie tooread en write gegevens uit Evbent Hubs</span><span class="sxs-lookup"><span data-stu-id="3ed23-105">This document uses a C# Storm topology tooread and write data from Evbent Hubs</span></span>

> [!NOTE]
> <span data-ttu-id="3ed23-106">Zie voor een Java-versie van dit project, [verwerken van gebeurtenissen van Azure Event Hubs met Storm op HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="3ed23-106">For a Java version of this project, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="scpnet"></a><span data-ttu-id="3ed23-107">SCP.NET</span><span class="sxs-lookup"><span data-stu-id="3ed23-107">SCP.NET</span></span>

<span data-ttu-id="3ed23-108">Hallo stappen in dit document gebruikt SCP.NET, een NuGet-pakket dat u het eenvoudig toocreate C#-topologieën en -onderdelen voor gebruik met Storm op HDInsight maakt.</span><span class="sxs-lookup"><span data-stu-id="3ed23-108">hello steps in this document use SCP.NET, a NuGet package that makes it easy toocreate C# topologies and components for use with Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3ed23-109">Tijdens het Hallo stappen in dit document kan zijn afhankelijk van een Windows-ontwikkelomgeving met Visual Studio, Hallo gecompileerd project ingediende tooa Storm op HDInsight-cluster dat gebruik maakt van Linux.</span><span class="sxs-lookup"><span data-stu-id="3ed23-109">While hello steps in this document rely on a Windows development environment with Visual Studio, hello compiled project can be submitted tooa Storm on HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="3ed23-110">Op basis van Linux-clusters die zijn gemaakt na 28 oktober 2016 ondersteunen alleen SCP.NET topologieën.</span><span class="sxs-lookup"><span data-stu-id="3ed23-110">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="3ed23-111">HDInsight 3.4 en groter gebruiken Mono toorun C#-topologieën.</span><span class="sxs-lookup"><span data-stu-id="3ed23-111">HDInsight 3.4 and greater use Mono toorun C# topologies.</span></span> <span data-ttu-id="3ed23-112">Hallo-voorbeeld gebruikt in dit document werkt met HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="3ed23-112">hello example used in this document works with HDInsight 3.6.</span></span> <span data-ttu-id="3ed23-113">Als u van plan om uw eigen .NET-oplossingen voor HDInsight te maken bent, controleert u Hallo [Mono compatibiliteit](http://www.mono-project.com/docs/about-mono/compatibility/) document voor potentiële compatibiliteitsproblemen.</span><span class="sxs-lookup"><span data-stu-id="3ed23-113">If you plan on creating your own .NET solutions for HDInsight, check hello [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>

### <a name="cluster-versioning"></a><span data-ttu-id="3ed23-114">Cluster-versies</span><span class="sxs-lookup"><span data-stu-id="3ed23-114">Cluster versioning</span></span>

<span data-ttu-id="3ed23-115">Hallo Microsoft.SCP.Net.SDK NuGet-pakket die u voor uw project gebruikt moet overeenkomen met de Hallo primaire versie van Storm op HDInsight is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="3ed23-115">hello Microsoft.SCP.Net.SDK NuGet package you use for your project must match hello major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="3ed23-116">HDInsight versie 3.5 en 3.6 Storm gebruiken 1.x, dus moet u SCP.NET versie 1.0.x.x met deze clusters gebruiken.</span><span class="sxs-lookup"><span data-stu-id="3ed23-116">HDInsight versions 3.5 and 3.6 use Storm 1.x, so you must use SCP.NET version 1.0.x.x with these clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3ed23-117">Hallo-voorbeeld in dit document verwacht een HDInsight-3.5 of 3,6 cluster.</span><span class="sxs-lookup"><span data-stu-id="3ed23-117">hello example in this document expects an HDInsight 3.5 or 3.6 cluster.</span></span>
>
> <span data-ttu-id="3ed23-118">Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="3ed23-118">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3ed23-119">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="3ed23-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="3ed23-120">C#-topologieën moeten ook .NET 4.5 gericht.</span><span class="sxs-lookup"><span data-stu-id="3ed23-120">C# topologies must also target .NET 4.5.</span></span>

## <a name="how-toowork-with-event-hubs"></a><span data-ttu-id="3ed23-121">Hoe toowork met Event Hubs</span><span class="sxs-lookup"><span data-stu-id="3ed23-121">How toowork with Event Hubs</span></span>

<span data-ttu-id="3ed23-122">Microsoft biedt een set van Java-onderdelen die gebruikt toocommunicate met Event Hubs van een Storm-topologie worden kunnen.</span><span class="sxs-lookup"><span data-stu-id="3ed23-122">Microsoft provides a set of Java components that can be used toocommunicate with Event Hubs from a Storm topology.</span></span> <span data-ttu-id="3ed23-123">U vindt Hallo Java-archief (JAR)-bestand met een compatibele versie van HDInsight 3.6 van deze onderdelen bij [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="3ed23-123">You can find hello Java archive (JAR) file that contains an HDInsight 3.6 compatible version of these components at [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3ed23-124">Tijdens het Hallo-onderdelen zijn geschreven in Java, kunt u deze eenvoudig gebruiken van een C#-topologie.</span><span class="sxs-lookup"><span data-stu-id="3ed23-124">While hello components are written in Java, you can easily use them from a C# topology.</span></span>

<span data-ttu-id="3ed23-125">Hallo volgende onderdelen worden gebruikt in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="3ed23-125">hello following components are used in this example:</span></span>

* <span data-ttu-id="3ed23-126">__EventHubSpout__: leest de gegevens uit Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="3ed23-126">__EventHubSpout__: Reads data from Event Hubs.</span></span>
* <span data-ttu-id="3ed23-127">__EventHubBolt__: schrijft gegevens tooEvent Hubs.</span><span class="sxs-lookup"><span data-stu-id="3ed23-127">__EventHubBolt__: Writes data tooEvent Hubs.</span></span>
* <span data-ttu-id="3ed23-128">__EventHubSpoutConfig__: tooconfigure EventHubSpout gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3ed23-128">__EventHubSpoutConfig__: Used tooconfigure EventHubSpout.</span></span>
* <span data-ttu-id="3ed23-129">__EventHubBoltConfig__: tooconfigure EventHubBolt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3ed23-129">__EventHubBoltConfig__: Used tooconfigure EventHubBolt.</span></span>

### <a name="example-spout-usage"></a><span data-ttu-id="3ed23-130">Voorbeeld van spout syntaxis</span><span class="sxs-lookup"><span data-stu-id="3ed23-130">Example spout usage</span></span>

<span data-ttu-id="3ed23-131">SCP.NET biedt methoden voor het toevoegen van een EventHubSpout tooyour-topologie.</span><span class="sxs-lookup"><span data-stu-id="3ed23-131">SCP.NET provides methods for adding an EventHubSpout tooyour topology.</span></span> <span data-ttu-id="3ed23-132">Deze methoden maken het gemakkelijker tooadd een spout dan het gebruik van Hallo algemene methoden voor het toevoegen van een Java-component.</span><span class="sxs-lookup"><span data-stu-id="3ed23-132">These methods make it easier tooadd a spout than using hello generic methods for adding a Java component.</span></span> <span data-ttu-id="3ed23-133">Hallo volgende voorbeeld laat zien hoe een spout met behulp van toocreate Hallo __SetEventHubSpout__ en **EventHubSpoutConfig** methoden van SCP.NET:</span><span class="sxs-lookup"><span data-stu-id="3ed23-133">hello following example demonstrates how toocreate a spout by using hello __SetEventHubSpout__ and **EventHubSpoutConfig** methods provided by SCP.NET:</span></span>

```csharp
 topologyBuilder.SetEventHubSpout(
    "EventHubSpout",
    new EventHubSpoutConfig(
        ConfigurationManager.AppSettings["EventHubSharedAccessKeyName"],
        ConfigurationManager.AppSettings["EventHubSharedAccessKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        ConfigurationManager.AppSettings["EventHubEntityPath"],
        eventHubPartitions),
    eventHubPartitions);
```

<span data-ttu-id="3ed23-134">Hallo vorige voorbeeld maakt u een nieuw spout-onderdeel met de naam __EventHubSpout__, en configureert deze toocommunicate met een event hub.</span><span class="sxs-lookup"><span data-stu-id="3ed23-134">hello previous example creates a new spout component named __EventHubSpout__, and configures it toocommunicate with an event hub.</span></span> <span data-ttu-id="3ed23-135">Hallo parallelle uitvoering hint voor Hallo onderdeel is het aantal partities toohello ingesteld in Hallo event hub.</span><span class="sxs-lookup"><span data-stu-id="3ed23-135">hello parallelism hint for hello component is set toohello number of partitions in hello event hub.</span></span> <span data-ttu-id="3ed23-136">Deze instelling kunt u Storm toocreate een exemplaar van Hallo-onderdeel voor elke partitie.</span><span class="sxs-lookup"><span data-stu-id="3ed23-136">This setting allows Storm toocreate an instance of hello component for each partition.</span></span>

### <a name="example-bolt-usage"></a><span data-ttu-id="3ed23-137">Voorbeeld van bolt syntaxis</span><span class="sxs-lookup"><span data-stu-id="3ed23-137">Example bolt usage</span></span>

<span data-ttu-id="3ed23-138">Gebruik Hallo **JavaComponmentConstructor** methode toocreate een exemplaar van Hallo bolt.</span><span class="sxs-lookup"><span data-stu-id="3ed23-138">Use hello **JavaComponmentConstructor** method toocreate an instance of hello bolt.</span></span> <span data-ttu-id="3ed23-139">Hallo volgende voorbeeld laat zien hoe toocreate en configureren van een nieuw exemplaar van Hallo **EventHubBolt**:</span><span class="sxs-lookup"><span data-stu-id="3ed23-139">hello following example demonstrates how toocreate and configure a new instance of hello **EventHubBolt**:</span></span>

```csharp
// Java construcvtor for hello Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set hello bolt toosubscribe toodata from hello spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> <span data-ttu-id="3ed23-140">In dit voorbeeld wordt een Clojure expressie doorgegeven als een tekenreeks, in plaats van **JavaComponentConstructor** toocreate een **EventHubBoltConfig**, zoals Hallo spout voorbeeld hebt.</span><span class="sxs-lookup"><span data-stu-id="3ed23-140">This example uses a Clojure expression passed as a string, instead of using **JavaComponentConstructor** toocreate an **EventHubBoltConfig**, as hello spout example did.</span></span> <span data-ttu-id="3ed23-141">De methode werkt.</span><span class="sxs-lookup"><span data-stu-id="3ed23-141">Either method works.</span></span> <span data-ttu-id="3ed23-142">Hallo methode gebruiken die aanbevolen tooyou werkt.</span><span class="sxs-lookup"><span data-stu-id="3ed23-142">Use hello method that feels best tooyou.</span></span>

## <a name="download-hello-completed-project"></a><span data-ttu-id="3ed23-143">Hallo voltooid-project downloaden</span><span class="sxs-lookup"><span data-stu-id="3ed23-143">Download hello completed project</span></span>

<span data-ttu-id="3ed23-144">U kunt een volledige versie van het Hallo-project gemaakt in deze zelfstudie uit downloaden [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="3ed23-144">You can download a complete version of hello project created in this tutorial from [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span> <span data-ttu-id="3ed23-145">U moet echter nog steeds tooprovide configuratie-instellingen door Hallo stappen in deze zelfstudie te volgen.</span><span class="sxs-lookup"><span data-stu-id="3ed23-145">However, you still need tooprovide configuration settings by following hello steps in this tutorial.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="3ed23-146">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3ed23-146">Prerequisites</span></span>

* <span data-ttu-id="3ed23-147">Een [Apache Storm op HDInsight-cluster versie 3.5 of 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3ed23-147">An [Apache Storm on HDInsight cluster version 3.5 or 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span></span>

    > [!WARNING]
    > <span data-ttu-id="3ed23-148">Hallo-voorbeeld gebruikt in dit document vereist Storm op HDInsight versie 3.5 of 3.6.</span><span class="sxs-lookup"><span data-stu-id="3ed23-148">hello example used in this document requires Storm on HDInsight version 3.5 or 3.6.</span></span> <span data-ttu-id="3ed23-149">Dit werkt niet met oudere versies van HDInsight, vanwege wijzigingen in de naam toobreaking klasse.</span><span class="sxs-lookup"><span data-stu-id="3ed23-149">This does not work with older versions of HDInsight, due toobreaking class name changes.</span></span> <span data-ttu-id="3ed23-150">Zie voor een versie van dit voorbeeld dat met oudere clusters werkt [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span><span class="sxs-lookup"><span data-stu-id="3ed23-150">For a version of this example that works with older clusters, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span></span>

* <span data-ttu-id="3ed23-151">Een [Azure event hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="3ed23-151">An [Azure event hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="3ed23-152">Hallo [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="3ed23-152">hello [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>

* <span data-ttu-id="3ed23-153">Hallo [HDInsight tools voor Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3ed23-153">hello [HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="3ed23-154">Java JDK 1.8 of hoger op uw ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="3ed23-154">Java JDK 1.8 or later on your development environment.</span></span> <span data-ttu-id="3ed23-155">JDK downloads zijn beschikbaar op [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="3ed23-155">JDK downloads are available from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>

  * <span data-ttu-id="3ed23-156">Hallo **JAVA_HOME** omgeving variabele moet punt toohello directory met Java.</span><span class="sxs-lookup"><span data-stu-id="3ed23-156">hello **JAVA_HOME** environment variable must point toohello directory that contains Java.</span></span>
  * <span data-ttu-id="3ed23-157">Hallo **%JAVA_HOME%/bin** directory in Hallo-pad moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3ed23-157">hello **%JAVA_HOME%/bin** directory must be in hello path.</span></span>

## <a name="download-hello-event-hubs-components"></a><span data-ttu-id="3ed23-158">Hallo Event Hubs-onderdelen downloaden</span><span class="sxs-lookup"><span data-stu-id="3ed23-158">Download hello Event Hubs components</span></span>

<span data-ttu-id="3ed23-159">Download Hallo Event Hubs spout en Bolts onderdeel uit [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="3ed23-159">Download hello Event Hubs spout and bolt component from [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

<span data-ttu-id="3ed23-160">Maak een map met de naam `eventhubspout`, en Hallo-bestand op te slaan in directory Hallo.</span><span class="sxs-lookup"><span data-stu-id="3ed23-160">Create a directory named `eventhubspout`, and save hello file into hello directory.</span></span>

## <a name="configure-event-hubs"></a><span data-ttu-id="3ed23-161">Event Hubs configureren</span><span class="sxs-lookup"><span data-stu-id="3ed23-161">Configure Event Hubs</span></span>

<span data-ttu-id="3ed23-162">Event Hubs is Hallo gegevensbron voor dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="3ed23-162">Event Hubs is hello data source for this example.</span></span> <span data-ttu-id="3ed23-163">Gebruik Hallo informatie in 'Een event hub maken' Hallo-sectie van [aan de slag met Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="3ed23-163">Use hello information in hello "Create an event hub" section of [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

1. <span data-ttu-id="3ed23-164">Nadat het Hallo event hub is gemaakt, weergeven Hallo **EventHub** blade in Azure portal en selecteer Hallo **gedeeld toegangsbeleid**.</span><span class="sxs-lookup"><span data-stu-id="3ed23-164">After hello event hub has been created, view hello **EventHub** blade in hello Azure portal, and select **Shared access policies**.</span></span> <span data-ttu-id="3ed23-165">Selecteer **+ toevoegen** tooadd Hallo beleidsregels te volgen:</span><span class="sxs-lookup"><span data-stu-id="3ed23-165">Select **+ Add** tooadd hello following policies:</span></span>

   | <span data-ttu-id="3ed23-166">Naam</span><span class="sxs-lookup"><span data-stu-id="3ed23-166">Name</span></span> | <span data-ttu-id="3ed23-167">Machtigingen</span><span class="sxs-lookup"><span data-stu-id="3ed23-167">Permissions</span></span> |
   | --- | --- |
   | <span data-ttu-id="3ed23-168">schrijver</span><span class="sxs-lookup"><span data-stu-id="3ed23-168">writer</span></span> |<span data-ttu-id="3ed23-169">Verzenden</span><span class="sxs-lookup"><span data-stu-id="3ed23-169">Send</span></span> |
   | <span data-ttu-id="3ed23-170">lezer</span><span class="sxs-lookup"><span data-stu-id="3ed23-170">reader</span></span> |<span data-ttu-id="3ed23-171">Luisteren</span><span class="sxs-lookup"><span data-stu-id="3ed23-171">Listen</span></span> |

    ![Schermafbeelding van de Share access beleid-venster](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. <span data-ttu-id="3ed23-173">Selecteer Hallo **lezer** en **writer** beleid.</span><span class="sxs-lookup"><span data-stu-id="3ed23-173">Select hello **reader** and **writer** policies.</span></span> <span data-ttu-id="3ed23-174">Kopieer en Hallo waarde primaire sleutel voor beide beleidsregels niet opslaan omdat deze waarden later worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="3ed23-174">Copy and save hello primary key value for both policies, as these values are used later.</span></span>

## <a name="configure-hello-eventhubwriter"></a><span data-ttu-id="3ed23-175">Hallo EventHubWriter configureren</span><span class="sxs-lookup"><span data-stu-id="3ed23-175">Configure hello EventHubWriter</span></span>

1. <span data-ttu-id="3ed23-176">Als u hebt niet is gebeurd Hallo meest recente versie van Hallo HDInsight tools voor Visual Studio, Zie [aan de slag met HDInsight tools voor Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3ed23-176">If you have not already installed hello latest version of hello HDInsight tools for Visual Studio, see [Get started using HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="3ed23-177">Hallo-oplossing van downloaden [eventhub-storm-hybride](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="3ed23-177">Download hello solution from [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

3. <span data-ttu-id="3ed23-178">In Hallo **EventHubWriter** project, open Hallo **App.config** bestand.</span><span class="sxs-lookup"><span data-stu-id="3ed23-178">In hello **EventHubWriter** project, open hello **App.config** file.</span></span> <span data-ttu-id="3ed23-179">Gebruik de informatie van de Hallo van Hallo event hub dat u eerder toofill geconfigureerd in Hallo-waarde voor Hallo sleutels te volgen:</span><span class="sxs-lookup"><span data-stu-id="3ed23-179">Use hello information from hello event hub that you configured earlier toofill in hello value for hello following keys:</span></span>

   | <span data-ttu-id="3ed23-180">Sleutel</span><span class="sxs-lookup"><span data-stu-id="3ed23-180">Key</span></span> | <span data-ttu-id="3ed23-181">Waarde</span><span class="sxs-lookup"><span data-stu-id="3ed23-181">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="3ed23-182">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="3ed23-182">EventHubPolicyName</span></span> |<span data-ttu-id="3ed23-183">schrijver (als u een andere naam voor beleid met de Hallo gebruikt *verzenden* toestemming hebben, in plaats daarvan gebruikt.)</span><span class="sxs-lookup"><span data-stu-id="3ed23-183">writer (If you used a different name for hello policy with *Send* permission, use it instead.)</span></span> |
   | <span data-ttu-id="3ed23-184">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="3ed23-184">EventHubPolicyKey</span></span> |<span data-ttu-id="3ed23-185">Hallo-sleutel voor Hallo writer beleid.</span><span class="sxs-lookup"><span data-stu-id="3ed23-185">hello key for hello writer policy.</span></span> |
   | <span data-ttu-id="3ed23-186">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="3ed23-186">EventHubNamespace</span></span> |<span data-ttu-id="3ed23-187">Hallo-naamruimte die uw event hub bevat.</span><span class="sxs-lookup"><span data-stu-id="3ed23-187">hello namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="3ed23-188">EventHubName</span><span class="sxs-lookup"><span data-stu-id="3ed23-188">EventHubName</span></span> |<span data-ttu-id="3ed23-189">De naam van de event hub.</span><span class="sxs-lookup"><span data-stu-id="3ed23-189">Your event hub name.</span></span> |
   | <span data-ttu-id="3ed23-190">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="3ed23-190">EventHubPartitionCount</span></span> |<span data-ttu-id="3ed23-191">Hallo aantal partities in de event hub.</span><span class="sxs-lookup"><span data-stu-id="3ed23-191">hello number of partitions in your event hub.</span></span> |

4. <span data-ttu-id="3ed23-192">Opslaan en sluiten Hallo **App.config** bestand.</span><span class="sxs-lookup"><span data-stu-id="3ed23-192">Save and close hello **App.config** file.</span></span>

## <a name="configure-hello-eventhubreader"></a><span data-ttu-id="3ed23-193">Hallo EventHubReader configureren</span><span class="sxs-lookup"><span data-stu-id="3ed23-193">Configure hello EventHubReader</span></span>

1. <span data-ttu-id="3ed23-194">Open Hallo **EventHubReader** project.</span><span class="sxs-lookup"><span data-stu-id="3ed23-194">Open hello **EventHubReader** project.</span></span>

2. <span data-ttu-id="3ed23-195">Open Hallo **App.config** -bestand voor Hallo **EventHubReader**.</span><span class="sxs-lookup"><span data-stu-id="3ed23-195">Open hello **App.config** file for hello **EventHubReader**.</span></span> <span data-ttu-id="3ed23-196">Gebruik de informatie van de Hallo van Hallo event hub dat u eerder toofill geconfigureerd in Hallo-waarde voor Hallo sleutels te volgen:</span><span class="sxs-lookup"><span data-stu-id="3ed23-196">Use hello information from hello event hub that you configured earlier toofill in hello value for hello following keys:</span></span>

   | <span data-ttu-id="3ed23-197">Sleutel</span><span class="sxs-lookup"><span data-stu-id="3ed23-197">Key</span></span> | <span data-ttu-id="3ed23-198">Waarde</span><span class="sxs-lookup"><span data-stu-id="3ed23-198">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="3ed23-199">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="3ed23-199">EventHubPolicyName</span></span> |<span data-ttu-id="3ed23-200">lezer (als u een andere naam voor beleid met de Hallo gebruikt *luisteren* toestemming hebben, in plaats daarvan gebruikt.)</span><span class="sxs-lookup"><span data-stu-id="3ed23-200">reader (If you used a different name for hello policy with *listen* permission, use it instead.)</span></span> |
   | <span data-ttu-id="3ed23-201">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="3ed23-201">EventHubPolicyKey</span></span> |<span data-ttu-id="3ed23-202">Hallo-sleutel voor Hallo lezer beleid.</span><span class="sxs-lookup"><span data-stu-id="3ed23-202">hello key for hello reader policy.</span></span> |
   | <span data-ttu-id="3ed23-203">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="3ed23-203">EventHubNamespace</span></span> |<span data-ttu-id="3ed23-204">Hallo-naamruimte die uw event hub bevat.</span><span class="sxs-lookup"><span data-stu-id="3ed23-204">hello namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="3ed23-205">EventHubName</span><span class="sxs-lookup"><span data-stu-id="3ed23-205">EventHubName</span></span> |<span data-ttu-id="3ed23-206">De naam van de event hub.</span><span class="sxs-lookup"><span data-stu-id="3ed23-206">Your event hub name.</span></span> |
   | <span data-ttu-id="3ed23-207">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="3ed23-207">EventHubPartitionCount</span></span> |<span data-ttu-id="3ed23-208">Hallo aantal partities in de event hub.</span><span class="sxs-lookup"><span data-stu-id="3ed23-208">hello number of partitions in your event hub.</span></span> |

3. <span data-ttu-id="3ed23-209">Opslaan en sluiten Hallo **App.config** bestand.</span><span class="sxs-lookup"><span data-stu-id="3ed23-209">Save and close hello **App.config** file.</span></span>

## <a name="deploy-hello-topologies"></a><span data-ttu-id="3ed23-210">Hallo-topologieën implementeren</span><span class="sxs-lookup"><span data-stu-id="3ed23-210">Deploy hello topologies</span></span>

1. <span data-ttu-id="3ed23-211">Van **Solution Explorer**, klik met de rechtermuisknop Hallo **EventHubReader** project en selecteer **indienen tooStorm op HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="3ed23-211">From **Solution Explorer**, right-click hello **EventHubReader** project, and select **Submit tooStorm on HDInsight**.</span></span>

    ![Schermopname van Solution Explorer met indienen tooStorm op HDInsight gemarkeerd](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. <span data-ttu-id="3ed23-213">Op Hallo **topologie indienen** in het dialoogvenster, selecteer uw **Storm-Cluster**.</span><span class="sxs-lookup"><span data-stu-id="3ed23-213">On hello **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="3ed23-214">Vouw **aanvullende configuraties**, selecteer **Java bestandspaden**, selecteer **...** , en selecteer Hallo directory waarin Hallo JAR-bestand dat u eerder hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="3ed23-214">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select hello directory that contains hello JAR file that you downloaded earlier.</span></span> <span data-ttu-id="3ed23-215">Tot slot op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="3ed23-215">Finally, click **Submit**.</span></span>

    ![Dialoogvenster Schermafbeelding van de indienings-topologie](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. <span data-ttu-id="3ed23-217">Wanneer het Hallo-topologie is ingediend, Hallo **Storm-topologieën Viewer** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="3ed23-217">When hello topology has been submitted, hello **Storm Topologies Viewer** appears.</span></span> <span data-ttu-id="3ed23-218">tooview informatie over het Hallo-topologie, selecteer Hallo **EventHubReader** topologie in het linkerdeelvenster Hallo.</span><span class="sxs-lookup"><span data-stu-id="3ed23-218">tooview information about hello topology, select hello **EventHubReader** topology in hello left pane.</span></span>

    ![Schermopname van Storm-topologieën Viewer](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. <span data-ttu-id="3ed23-220">Van **Solution Explorer**, klik met de rechtermuisknop Hallo **EventHubWriter** project en selecteer **indienen tooStorm op HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="3ed23-220">From **Solution Explorer**, right-click hello **EventHubWriter** project, and select **Submit tooStorm on HDInsight**.</span></span>

5. <span data-ttu-id="3ed23-221">Op Hallo **topologie indienen** in het dialoogvenster, selecteer uw **Storm-Cluster**.</span><span class="sxs-lookup"><span data-stu-id="3ed23-221">On hello **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="3ed23-222">Vouw **aanvullende configuraties**, selecteer **Java bestandspaden**, selecteer **...** , en selecteer Hallo map Hallo JAR-bestand met u eerder hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="3ed23-222">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select hello directory that contains hello JAR file you downloaded earlier.</span></span> <span data-ttu-id="3ed23-223">Tot slot op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="3ed23-223">Finally, click **Submit**.</span></span>

6. <span data-ttu-id="3ed23-224">Wanneer het Hallo-topologie is ingediend, vernieuw de lijst met de Hallo-topologie in Hallo **Storm-topologieën Viewer** tooverify die beide topologieën op Hallo cluster worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="3ed23-224">When hello topology has been submitted, refresh hello topology list in hello **Storm Topologies Viewer** tooverify that both topologies are running on hello cluster.</span></span>

7. <span data-ttu-id="3ed23-225">In **Storm-topologieën Viewer**, selecteer Hallo **EventHubReader** topologie.</span><span class="sxs-lookup"><span data-stu-id="3ed23-225">In **Storm Topologies Viewer**, select hello **EventHubReader** topology.</span></span>

8. <span data-ttu-id="3ed23-226">tooopen hello onderdeel samenvatting voor Hallo bolt, dubbelklikt u op Hallo **LogBolt** onderdeel in het Hallo-diagram.</span><span class="sxs-lookup"><span data-stu-id="3ed23-226">tooopen hello component summary for hello bolt, double-click hello **LogBolt** component in hello diagram.</span></span>

9. <span data-ttu-id="3ed23-227">In Hallo **Executor** sectie, selecteert u een van de koppelingen Hallo in Hallo **poort** kolom.</span><span class="sxs-lookup"><span data-stu-id="3ed23-227">In hello **Executors** section, select one of hello links in hello **Port** column.</span></span> <span data-ttu-id="3ed23-228">U ziet nu informatie die wordt geregistreerd door Hallo-onderdeel.</span><span class="sxs-lookup"><span data-stu-id="3ed23-228">This displays information logged by hello component.</span></span> <span data-ttu-id="3ed23-229">Hallo geregistreerd informatie is vergelijkbaar toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="3ed23-229">hello logged information is similar toohello following text:</span></span>

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-hello-topologies"></a><span data-ttu-id="3ed23-230">Hallo topologieën stoppen</span><span class="sxs-lookup"><span data-stu-id="3ed23-230">Stop hello topologies</span></span>

<span data-ttu-id="3ed23-231">toostop hello topologieën, selecteert u elke topologie in Hallo **Storm-topologie Viewer**, klikt u vervolgens op **Kill**.</span><span class="sxs-lookup"><span data-stu-id="3ed23-231">toostop hello topologies, select each topology in hello **Storm Topology Viewer**, then click **Kill**.</span></span>

![Schermopname van Storm-topologie-Viewer met Kill knop gemarkeerd](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="3ed23-233">Uw cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="3ed23-233">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="3ed23-234">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3ed23-234">Next steps</span></span>

<span data-ttu-id="3ed23-235">In dit document hebt u geleerd hoe toouse Hallo Java Event Hubs spout en Bolts uit een C#-topologie-toowork met gegevens in Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="3ed23-235">In this document, you have learned how toouse hello Java Event Hubs spout and bolt from a C# topology toowork with data in Azure Event Hubs.</span></span> <span data-ttu-id="3ed23-236">toolearn meer informatie over het maken van C#-topologieën, Zie de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="3ed23-236">toolearn more about creating C# topologies, see hello following:</span></span>

* [<span data-ttu-id="3ed23-237">C#-topologieën ontwikkelen voor Apache Storm op HDInsight met behulp van Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3ed23-237">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="3ed23-238">Programmeerhandleiding voor SCP</span><span class="sxs-lookup"><span data-stu-id="3ed23-238">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)
* [<span data-ttu-id="3ed23-239">Voorbeeldtopologieën van Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="3ed23-239">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
