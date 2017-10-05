---
title: Verwerken van gebeurtenissen van Event Hubs met Storm - Azure HDInsight | Microsoft Docs
description: Informatie over het verwerken van gegevens uit Azure Event Hubs met een C# Storm-topologie in Visual Studio gemaakt met behulp van de HDInsight tools voor Visual Studio.
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
ms.openlocfilehash: 4b6fd87b057d93175d3ef284238d77be3bdde61d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a><span data-ttu-id="caf55-103">Procesgebeurtenissen van Azure Event Hubs met Storm op HDInsight (C#)</span><span class="sxs-lookup"><span data-stu-id="caf55-103">Process events from Azure Event Hubs with Storm on HDInsight (C#)</span></span>

<span data-ttu-id="caf55-104">Informatie over het werken met Azure Event Hubs van Apache Storm op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="caf55-104">Learn how to work with Azure Event Hubs from Apache Storm on HDInsight.</span></span> <span data-ttu-id="caf55-105">Dit document wordt een C# Storm-topologie te lezen en schrijven van gegevens uit Evbent Hubs</span><span class="sxs-lookup"><span data-stu-id="caf55-105">This document uses a C# Storm topology to read and write data from Evbent Hubs</span></span>

> [!NOTE]
> <span data-ttu-id="caf55-106">Zie voor een Java-versie van dit project, [verwerken van gebeurtenissen van Azure Event Hubs met Storm op HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="caf55-106">For a Java version of this project, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="scpnet"></a><span data-ttu-id="caf55-107">SCP.NET</span><span class="sxs-lookup"><span data-stu-id="caf55-107">SCP.NET</span></span>

<span data-ttu-id="caf55-108">De stappen in dit document SCP.NET, een NuGet-pakket waarmee u eenvoudig te maken van C#-topologieën en -onderdelen voor gebruik met Storm op HDInsight kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="caf55-108">The steps in this document use SCP.NET, a NuGet package that makes it easy to create C# topologies and components for use with Storm on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="caf55-109">Terwijl de stappen in dit document, is afhankelijk van een Windows-ontwikkelomgeving met Visual Studio, kan het project gecompileerd naar een Storm op HDInsight-cluster dat gebruik maakt van Linux worden verzonden.</span><span class="sxs-lookup"><span data-stu-id="caf55-109">While the steps in this document rely on a Windows development environment with Visual Studio, the compiled project can be submitted to a Storm on HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="caf55-110">Op basis van Linux-clusters die zijn gemaakt na 28 oktober 2016 ondersteunen alleen SCP.NET topologieën.</span><span class="sxs-lookup"><span data-stu-id="caf55-110">Only Linux-based clusters created after October 28, 2016, support SCP.NET topologies.</span></span>

<span data-ttu-id="caf55-111">HDInsight 3.4 en groter gebruiken Mono voor het uitvoeren van C#-topologieën.</span><span class="sxs-lookup"><span data-stu-id="caf55-111">HDInsight 3.4 and greater use Mono to run C# topologies.</span></span> <span data-ttu-id="caf55-112">Het voorbeeld in dit document gebruikt werkt met HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="caf55-112">The example used in this document works with HDInsight 3.6.</span></span> <span data-ttu-id="caf55-113">Als u van plan om uw eigen .NET-oplossingen voor HDInsight te maken bent, controleert u de [Mono compatibiliteit](http://www.mono-project.com/docs/about-mono/compatibility/) document voor potentiële compatibiliteitsproblemen.</span><span class="sxs-lookup"><span data-stu-id="caf55-113">If you plan on creating your own .NET solutions for HDInsight, check the [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>

### <a name="cluster-versioning"></a><span data-ttu-id="caf55-114">Cluster-versies</span><span class="sxs-lookup"><span data-stu-id="caf55-114">Cluster versioning</span></span>

<span data-ttu-id="caf55-115">Het Microsoft.SCP.Net.SDK NuGet-pakket dat u voor uw project gebruikt moet overeenkomen met de primaire versie van Storm op HDInsight is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="caf55-115">The Microsoft.SCP.Net.SDK NuGet package you use for your project must match the major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="caf55-116">HDInsight versie 3.5 en 3.6 Storm gebruiken 1.x, dus moet u SCP.NET versie 1.0.x.x met deze clusters gebruiken.</span><span class="sxs-lookup"><span data-stu-id="caf55-116">HDInsight versions 3.5 and 3.6 use Storm 1.x, so you must use SCP.NET version 1.0.x.x with these clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="caf55-117">In het voorbeeld in dit document verwacht een HDInsight-3.5 of 3,6 cluster.</span><span class="sxs-lookup"><span data-stu-id="caf55-117">The example in this document expects an HDInsight 3.5 or 3.6 cluster.</span></span>
>
> <span data-ttu-id="caf55-118">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="caf55-118">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="caf55-119">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="caf55-119">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="caf55-120">C#-topologieën moeten ook .NET 4.5 gericht.</span><span class="sxs-lookup"><span data-stu-id="caf55-120">C# topologies must also target .NET 4.5.</span></span>

## <a name="how-to-work-with-event-hubs"></a><span data-ttu-id="caf55-121">Werken met Event Hubs</span><span class="sxs-lookup"><span data-stu-id="caf55-121">How to work with Event Hubs</span></span>

<span data-ttu-id="caf55-122">Microsoft biedt een set van Java-onderdelen die kunnen worden gebruikt om te communiceren met Event Hubs van een Storm-topologie.</span><span class="sxs-lookup"><span data-stu-id="caf55-122">Microsoft provides a set of Java components that can be used to communicate with Event Hubs from a Storm topology.</span></span> <span data-ttu-id="caf55-123">U vindt de Java-archief (JAR)-bestand met een compatibele versie van HDInsight 3.6 van deze onderdelen bij [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="caf55-123">You can find the Java archive (JAR) file that contains an HDInsight 3.6 compatible version of these components at [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="caf55-124">Terwijl de onderdelen zijn geschreven in Java, kunt u deze eenvoudig gebruiken van een C#-topologie.</span><span class="sxs-lookup"><span data-stu-id="caf55-124">While the components are written in Java, you can easily use them from a C# topology.</span></span>

<span data-ttu-id="caf55-125">De volgende onderdelen worden gebruikt in dit voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="caf55-125">The following components are used in this example:</span></span>

* <span data-ttu-id="caf55-126">__EventHubSpout__: leest de gegevens uit Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="caf55-126">__EventHubSpout__: Reads data from Event Hubs.</span></span>
* <span data-ttu-id="caf55-127">__EventHubBolt__: schrijft gegevens naar Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="caf55-127">__EventHubBolt__: Writes data to Event Hubs.</span></span>
* <span data-ttu-id="caf55-128">__EventHubSpoutConfig__: gebruikt voor het configureren van EventHubSpout.</span><span class="sxs-lookup"><span data-stu-id="caf55-128">__EventHubSpoutConfig__: Used to configure EventHubSpout.</span></span>
* <span data-ttu-id="caf55-129">__EventHubBoltConfig__: gebruikt voor het configureren van EventHubBolt.</span><span class="sxs-lookup"><span data-stu-id="caf55-129">__EventHubBoltConfig__: Used to configure EventHubBolt.</span></span>

### <a name="example-spout-usage"></a><span data-ttu-id="caf55-130">Voorbeeld van spout syntaxis</span><span class="sxs-lookup"><span data-stu-id="caf55-130">Example spout usage</span></span>

<span data-ttu-id="caf55-131">SCP.NET biedt methoden voor het toevoegen van een EventHubSpout aan uw topologie.</span><span class="sxs-lookup"><span data-stu-id="caf55-131">SCP.NET provides methods for adding an EventHubSpout to your topology.</span></span> <span data-ttu-id="caf55-132">Deze methoden kunnen gemakkelijker toevoegen van een spout dan het gebruik van de algemene methoden voor het toevoegen van een Java-component.</span><span class="sxs-lookup"><span data-stu-id="caf55-132">These methods make it easier to add a spout than using the generic methods for adding a Java component.</span></span> <span data-ttu-id="caf55-133">Het volgende voorbeeld laat zien hoe een spout maken met behulp van de __SetEventHubSpout__ en **EventHubSpoutConfig** methoden van SCP.NET:</span><span class="sxs-lookup"><span data-stu-id="caf55-133">The following example demonstrates how to create a spout by using the __SetEventHubSpout__ and **EventHubSpoutConfig** methods provided by SCP.NET:</span></span>

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

<span data-ttu-id="caf55-134">Het vorige voorbeeld maakt u een nieuw spout-onderdeel met de naam __EventHubSpout__, en geconfigureerd om te communiceren met een event hub.</span><span class="sxs-lookup"><span data-stu-id="caf55-134">The previous example creates a new spout component named __EventHubSpout__, and configures it to communicate with an event hub.</span></span> <span data-ttu-id="caf55-135">De parallelle uitvoering geheugensteun voor het onderdeel is ingesteld op het aantal partities in de event hub.</span><span class="sxs-lookup"><span data-stu-id="caf55-135">The parallelism hint for the component is set to the number of partitions in the event hub.</span></span> <span data-ttu-id="caf55-136">Deze instelling kunt Storm een exemplaar van het onderdeel voor elke partitie te maken.</span><span class="sxs-lookup"><span data-stu-id="caf55-136">This setting allows Storm to create an instance of the component for each partition.</span></span>

### <a name="example-bolt-usage"></a><span data-ttu-id="caf55-137">Voorbeeld van bolt syntaxis</span><span class="sxs-lookup"><span data-stu-id="caf55-137">Example bolt usage</span></span>

<span data-ttu-id="caf55-138">Gebruik de **JavaComponmentConstructor** methode voor het maken van een exemplaar van de bolt.</span><span class="sxs-lookup"><span data-stu-id="caf55-138">Use the **JavaComponmentConstructor** method to create an instance of the bolt.</span></span> <span data-ttu-id="caf55-139">Het volgende voorbeeld toont hoe maken en configureren van een nieuw exemplaar van de **EventHubBolt**:</span><span class="sxs-lookup"><span data-stu-id="caf55-139">The following example demonstrates how to create and configure a new instance of the **EventHubBolt**:</span></span>

```csharp
// Java construcvtor for the Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set the bolt to subscribe to data from the spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> <span data-ttu-id="caf55-140">In dit voorbeeld wordt een Clojure expressie doorgegeven als een tekenreeks, in plaats van **JavaComponentConstructor** maken een **EventHubBoltConfig**, zoals in het voorbeeld spout heeft.</span><span class="sxs-lookup"><span data-stu-id="caf55-140">This example uses a Clojure expression passed as a string, instead of using **JavaComponentConstructor** to create an **EventHubBoltConfig**, as the spout example did.</span></span> <span data-ttu-id="caf55-141">De methode werkt.</span><span class="sxs-lookup"><span data-stu-id="caf55-141">Either method works.</span></span> <span data-ttu-id="caf55-142">Gebruik de methode die u het beste werkt.</span><span class="sxs-lookup"><span data-stu-id="caf55-142">Use the method that feels best to you.</span></span>

## <a name="download-the-completed-project"></a><span data-ttu-id="caf55-143">Downloaden voltooid project</span><span class="sxs-lookup"><span data-stu-id="caf55-143">Download the completed project</span></span>

<span data-ttu-id="caf55-144">U kunt een volledige versie van het project gemaakt in deze zelfstudie uit downloaden [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="caf55-144">You can download a complete version of the project created in this tutorial from [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span> <span data-ttu-id="caf55-145">U moet echter nog steeds configuratieinstellingen opgeven door de stappen in deze zelfstudie te volgen.</span><span class="sxs-lookup"><span data-stu-id="caf55-145">However, you still need to provide configuration settings by following the steps in this tutorial.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="caf55-146">Vereisten</span><span class="sxs-lookup"><span data-stu-id="caf55-146">Prerequisites</span></span>

* <span data-ttu-id="caf55-147">Een [Apache Storm op HDInsight-cluster versie 3.5 of 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="caf55-147">An [Apache Storm on HDInsight cluster version 3.5 or 3.6](hdinsight-apache-storm-tutorial-get-started.md).</span></span>

    > [!WARNING]
    > <span data-ttu-id="caf55-148">Het voorbeeld in dit document gebruikt vereist Storm op HDInsight versie 3.5 of 3.6.</span><span class="sxs-lookup"><span data-stu-id="caf55-148">The example used in this document requires Storm on HDInsight version 3.5 or 3.6.</span></span> <span data-ttu-id="caf55-149">Dit werkt niet met oudere versies van HDInsight, als gevolg van wijzigingen in klasse de naam op te splitsen.</span><span class="sxs-lookup"><span data-stu-id="caf55-149">This does not work with older versions of HDInsight, due to breaking class name changes.</span></span> <span data-ttu-id="caf55-150">Zie voor een versie van dit voorbeeld dat met oudere clusters werkt [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span><span class="sxs-lookup"><span data-stu-id="caf55-150">For a version of this example that works with older clusters, see [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).</span></span>

* <span data-ttu-id="caf55-151">Een [Azure event hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="caf55-151">An [Azure event hub](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

* <span data-ttu-id="caf55-152">De [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="caf55-152">The [Azure .NET SDK](http://azure.microsoft.com/downloads/).</span></span>

* <span data-ttu-id="caf55-153">De [HDInsight tools voor Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="caf55-153">The [HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="caf55-154">Java JDK 1.8 of hoger op uw ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="caf55-154">Java JDK 1.8 or later on your development environment.</span></span> <span data-ttu-id="caf55-155">JDK downloads zijn beschikbaar op [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span><span class="sxs-lookup"><span data-stu-id="caf55-155">JDK downloads are available from [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).</span></span>

  * <span data-ttu-id="caf55-156">De **JAVA_HOME** omgevingsvariabele moet verwijzen naar de map waarin zich Java.</span><span class="sxs-lookup"><span data-stu-id="caf55-156">The **JAVA_HOME** environment variable must point to the directory that contains Java.</span></span>
  * <span data-ttu-id="caf55-157">De **%JAVA_HOME%/bin** directory in het pad moet worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="caf55-157">The **%JAVA_HOME%/bin** directory must be in the path.</span></span>

## <a name="download-the-event-hubs-components"></a><span data-ttu-id="caf55-158">De Event Hubs-onderdelen downloaden</span><span class="sxs-lookup"><span data-stu-id="caf55-158">Download the Event Hubs components</span></span>

<span data-ttu-id="caf55-159">Download de spout Event Hubs en Bolts onderdeel uit [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span><span class="sxs-lookup"><span data-stu-id="caf55-159">Download the Event Hubs spout and bolt component from [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).</span></span>

<span data-ttu-id="caf55-160">Maak een map met de naam `eventhubspout`, en sla het bestand naar de map.</span><span class="sxs-lookup"><span data-stu-id="caf55-160">Create a directory named `eventhubspout`, and save the file into the directory.</span></span>

## <a name="configure-event-hubs"></a><span data-ttu-id="caf55-161">Event Hubs configureren</span><span class="sxs-lookup"><span data-stu-id="caf55-161">Configure Event Hubs</span></span>

<span data-ttu-id="caf55-162">Event Hubs is de gegevensbron voor dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="caf55-162">Event Hubs is the data source for this example.</span></span> <span data-ttu-id="caf55-163">Gebruik de informatie in de sectie 'Een event hub maken' van [aan de slag met Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span><span class="sxs-lookup"><span data-stu-id="caf55-163">Use the information in the "Create an event hub" section of [Get started with Event Hubs](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).</span></span>

1. <span data-ttu-id="caf55-164">Nadat de event hub is gemaakt, weergeven de **EventHub** blade in de Azure portal en selecteer **gedeeld toegangsbeleid**.</span><span class="sxs-lookup"><span data-stu-id="caf55-164">After the event hub has been created, view the **EventHub** blade in the Azure portal, and select **Shared access policies**.</span></span> <span data-ttu-id="caf55-165">Selecteer **+ toevoegen** toevoegen van het volgende beleid:</span><span class="sxs-lookup"><span data-stu-id="caf55-165">Select **+ Add** to add the following policies:</span></span>

   | <span data-ttu-id="caf55-166">Naam</span><span class="sxs-lookup"><span data-stu-id="caf55-166">Name</span></span> | <span data-ttu-id="caf55-167">Machtigingen</span><span class="sxs-lookup"><span data-stu-id="caf55-167">Permissions</span></span> |
   | --- | --- |
   | <span data-ttu-id="caf55-168">schrijver</span><span class="sxs-lookup"><span data-stu-id="caf55-168">writer</span></span> |<span data-ttu-id="caf55-169">Verzenden</span><span class="sxs-lookup"><span data-stu-id="caf55-169">Send</span></span> |
   | <span data-ttu-id="caf55-170">lezer</span><span class="sxs-lookup"><span data-stu-id="caf55-170">reader</span></span> |<span data-ttu-id="caf55-171">Luisteren</span><span class="sxs-lookup"><span data-stu-id="caf55-171">Listen</span></span> |

    ![Schermafbeelding van de Share access beleid-venster](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. <span data-ttu-id="caf55-173">Selecteer de **lezer** en **writer** beleid.</span><span class="sxs-lookup"><span data-stu-id="caf55-173">Select the **reader** and **writer** policies.</span></span> <span data-ttu-id="caf55-174">Kopieer en de waarde van de primaire sleutel voor beide beleidsregels niet opslaan omdat deze waarden later worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="caf55-174">Copy and save the primary key value for both policies, as these values are used later.</span></span>

## <a name="configure-the-eventhubwriter"></a><span data-ttu-id="caf55-175">De EventHubWriter configureren</span><span class="sxs-lookup"><span data-stu-id="caf55-175">Configure the EventHubWriter</span></span>

1. <span data-ttu-id="caf55-176">Als u hebt niet is gebeurd de nieuwste versie van de HDInsight tools voor Visual Studio, Zie [aan de slag met HDInsight tools voor Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="caf55-176">If you have not already installed the latest version of the HDInsight tools for Visual Studio, see [Get started using HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

2. <span data-ttu-id="caf55-177">Downloaden van de oplossing van [eventhub-storm-hybride](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span><span class="sxs-lookup"><span data-stu-id="caf55-177">Download the solution from [eventhub-storm-hybrid](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).</span></span>

3. <span data-ttu-id="caf55-178">In de **EventHubWriter** project, open de **App.config** bestand.</span><span class="sxs-lookup"><span data-stu-id="caf55-178">In the **EventHubWriter** project, open the **App.config** file.</span></span> <span data-ttu-id="caf55-179">Gebruik de informatie van de event hub die u eerder hebt geconfigureerd in de waarde voor de volgende sleutels te vullen:</span><span class="sxs-lookup"><span data-stu-id="caf55-179">Use the information from the event hub that you configured earlier to fill in the value for the following keys:</span></span>

   | <span data-ttu-id="caf55-180">Sleutel</span><span class="sxs-lookup"><span data-stu-id="caf55-180">Key</span></span> | <span data-ttu-id="caf55-181">Waarde</span><span class="sxs-lookup"><span data-stu-id="caf55-181">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="caf55-182">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="caf55-182">EventHubPolicyName</span></span> |<span data-ttu-id="caf55-183">schrijver (als u een andere naam voor het beleid met gebruikt *verzenden* toestemming hebben, in plaats daarvan gebruikt.)</span><span class="sxs-lookup"><span data-stu-id="caf55-183">writer (If you used a different name for the policy with *Send* permission, use it instead.)</span></span> |
   | <span data-ttu-id="caf55-184">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="caf55-184">EventHubPolicyKey</span></span> |<span data-ttu-id="caf55-185">De sleutel voor het beleid writer.</span><span class="sxs-lookup"><span data-stu-id="caf55-185">The key for the writer policy.</span></span> |
   | <span data-ttu-id="caf55-186">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="caf55-186">EventHubNamespace</span></span> |<span data-ttu-id="caf55-187">De naamruimte die uw event hub bevat.</span><span class="sxs-lookup"><span data-stu-id="caf55-187">The namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="caf55-188">EventHubName</span><span class="sxs-lookup"><span data-stu-id="caf55-188">EventHubName</span></span> |<span data-ttu-id="caf55-189">De naam van de event hub.</span><span class="sxs-lookup"><span data-stu-id="caf55-189">Your event hub name.</span></span> |
   | <span data-ttu-id="caf55-190">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="caf55-190">EventHubPartitionCount</span></span> |<span data-ttu-id="caf55-191">Het aantal partities in de event hub.</span><span class="sxs-lookup"><span data-stu-id="caf55-191">The number of partitions in your event hub.</span></span> |

4. <span data-ttu-id="caf55-192">Sla op en sluit de **App.config** bestand.</span><span class="sxs-lookup"><span data-stu-id="caf55-192">Save and close the **App.config** file.</span></span>

## <a name="configure-the-eventhubreader"></a><span data-ttu-id="caf55-193">De EventHubReader configureren</span><span class="sxs-lookup"><span data-stu-id="caf55-193">Configure the EventHubReader</span></span>

1. <span data-ttu-id="caf55-194">Open de **EventHubReader** project.</span><span class="sxs-lookup"><span data-stu-id="caf55-194">Open the **EventHubReader** project.</span></span>

2. <span data-ttu-id="caf55-195">Open de **App.config** bestand voor de **EventHubReader**.</span><span class="sxs-lookup"><span data-stu-id="caf55-195">Open the **App.config** file for the **EventHubReader**.</span></span> <span data-ttu-id="caf55-196">Gebruik de informatie van de event hub die u eerder hebt geconfigureerd in de waarde voor de volgende sleutels te vullen:</span><span class="sxs-lookup"><span data-stu-id="caf55-196">Use the information from the event hub that you configured earlier to fill in the value for the following keys:</span></span>

   | <span data-ttu-id="caf55-197">Sleutel</span><span class="sxs-lookup"><span data-stu-id="caf55-197">Key</span></span> | <span data-ttu-id="caf55-198">Waarde</span><span class="sxs-lookup"><span data-stu-id="caf55-198">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="caf55-199">EventHubPolicyName</span><span class="sxs-lookup"><span data-stu-id="caf55-199">EventHubPolicyName</span></span> |<span data-ttu-id="caf55-200">lezer (als u een andere naam voor het beleid met gebruikt *luisteren* toestemming hebben, in plaats daarvan gebruikt.)</span><span class="sxs-lookup"><span data-stu-id="caf55-200">reader (If you used a different name for the policy with *listen* permission, use it instead.)</span></span> |
   | <span data-ttu-id="caf55-201">EventHubPolicyKey</span><span class="sxs-lookup"><span data-stu-id="caf55-201">EventHubPolicyKey</span></span> |<span data-ttu-id="caf55-202">De sleutel voor het beleid van de lezer.</span><span class="sxs-lookup"><span data-stu-id="caf55-202">The key for the reader policy.</span></span> |
   | <span data-ttu-id="caf55-203">EventHubNamespace</span><span class="sxs-lookup"><span data-stu-id="caf55-203">EventHubNamespace</span></span> |<span data-ttu-id="caf55-204">De naamruimte die uw event hub bevat.</span><span class="sxs-lookup"><span data-stu-id="caf55-204">The namespace that contains your event hub.</span></span> |
   | <span data-ttu-id="caf55-205">EventHubName</span><span class="sxs-lookup"><span data-stu-id="caf55-205">EventHubName</span></span> |<span data-ttu-id="caf55-206">De naam van de event hub.</span><span class="sxs-lookup"><span data-stu-id="caf55-206">Your event hub name.</span></span> |
   | <span data-ttu-id="caf55-207">EventHubPartitionCount</span><span class="sxs-lookup"><span data-stu-id="caf55-207">EventHubPartitionCount</span></span> |<span data-ttu-id="caf55-208">Het aantal partities in de event hub.</span><span class="sxs-lookup"><span data-stu-id="caf55-208">The number of partitions in your event hub.</span></span> |

3. <span data-ttu-id="caf55-209">Sla op en sluit de **App.config** bestand.</span><span class="sxs-lookup"><span data-stu-id="caf55-209">Save and close the **App.config** file.</span></span>

## <a name="deploy-the-topologies"></a><span data-ttu-id="caf55-210">De topologieën implementeren</span><span class="sxs-lookup"><span data-stu-id="caf55-210">Deploy the topologies</span></span>

1. <span data-ttu-id="caf55-211">Van **Solution Explorer**, met de rechtermuisknop op de **EventHubReader** project en selecteer **indienen Storm op HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="caf55-211">From **Solution Explorer**, right-click the **EventHubReader** project, and select **Submit to Storm on HDInsight**.</span></span>

    ![Schermopname van Solution Explorer met Storm op HDInsight gemarkeerd indienen](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. <span data-ttu-id="caf55-213">Op de **topologie indienen** in het dialoogvenster, selecteer uw **Storm-Cluster**.</span><span class="sxs-lookup"><span data-stu-id="caf55-213">On the **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="caf55-214">Vouw **aanvullende configuraties**, selecteer **Java bestandspaden**, selecteer **...** , en selecteer de map waarin het JAR-bestand dat u eerder hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="caf55-214">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select the directory that contains the JAR file that you downloaded earlier.</span></span> <span data-ttu-id="caf55-215">Tot slot op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="caf55-215">Finally, click **Submit**.</span></span>

    ![Dialoogvenster Schermafbeelding van de indienings-topologie](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. <span data-ttu-id="caf55-217">Wanneer de topologie is ingediend, de **Storm-topologieën Viewer** wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="caf55-217">When the topology has been submitted, the **Storm Topologies Viewer** appears.</span></span> <span data-ttu-id="caf55-218">Als u informatie over de topologie, selecteer de **EventHubReader** topologie in het linkerdeelvenster.</span><span class="sxs-lookup"><span data-stu-id="caf55-218">To view information about the topology, select the **EventHubReader** topology in the left pane.</span></span>

    ![Schermopname van Storm-topologieën Viewer](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. <span data-ttu-id="caf55-220">Van **Solution Explorer**, met de rechtermuisknop op de **EventHubWriter** project en selecteer **indienen Storm op HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="caf55-220">From **Solution Explorer**, right-click the **EventHubWriter** project, and select **Submit to Storm on HDInsight**.</span></span>

5. <span data-ttu-id="caf55-221">Op de **topologie indienen** in het dialoogvenster, selecteer uw **Storm-Cluster**.</span><span class="sxs-lookup"><span data-stu-id="caf55-221">On the **Submit Topology** dialog box, select your **Storm Cluster**.</span></span> <span data-ttu-id="caf55-222">Vouw **aanvullende configuraties**, selecteer **Java bestandspaden**, selecteer **...** , en selecteer de map waarin het JAR-bestand dat u eerder hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="caf55-222">Expand **Additional Configurations**, select **Java File Paths**, select **...**, and select the directory that contains the JAR file you downloaded earlier.</span></span> <span data-ttu-id="caf55-223">Tot slot op **indienen**.</span><span class="sxs-lookup"><span data-stu-id="caf55-223">Finally, click **Submit**.</span></span>

6. <span data-ttu-id="caf55-224">Wanneer de topologie is ingediend, vernieuw de lijst topologie in de **Storm-topologieën Viewer** om te controleren dat beide topologieën worden uitgevoerd op het cluster.</span><span class="sxs-lookup"><span data-stu-id="caf55-224">When the topology has been submitted, refresh the topology list in the **Storm Topologies Viewer** to verify that both topologies are running on the cluster.</span></span>

7. <span data-ttu-id="caf55-225">In **Storm-topologieën Viewer**, selecteer de **EventHubReader** topologie.</span><span class="sxs-lookup"><span data-stu-id="caf55-225">In **Storm Topologies Viewer**, select the **EventHubReader** topology.</span></span>

8. <span data-ttu-id="caf55-226">Als u wilt de samenvatting voor de bolt component openen, dubbelklikt u op de **LogBolt** onderdeel in het diagram.</span><span class="sxs-lookup"><span data-stu-id="caf55-226">To open the component summary for the bolt, double-click the **LogBolt** component in the diagram.</span></span>

9. <span data-ttu-id="caf55-227">In de **Executor** sectie, selecteer een van de koppelingen in de **poort** kolom.</span><span class="sxs-lookup"><span data-stu-id="caf55-227">In the **Executors** section, select one of the links in the **Port** column.</span></span> <span data-ttu-id="caf55-228">U ziet nu informatie die wordt geregistreerd door het onderdeel.</span><span class="sxs-lookup"><span data-stu-id="caf55-228">This displays information logged by the component.</span></span> <span data-ttu-id="caf55-229">De geregistreerde gegevens is vergelijkbaar met de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="caf55-229">The logged information is similar to the following text:</span></span>

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-the-topologies"></a><span data-ttu-id="caf55-230">De topologieën stoppen</span><span class="sxs-lookup"><span data-stu-id="caf55-230">Stop the topologies</span></span>

<span data-ttu-id="caf55-231">Als u wilt de topologieën stoppen, selecteert u elke topologie in de **Storm-topologie Viewer**, klikt u vervolgens op **Kill**.</span><span class="sxs-lookup"><span data-stu-id="caf55-231">To stop the topologies, select each topology in the **Storm Topology Viewer**, then click **Kill**.</span></span>

![Schermopname van Storm-topologie-Viewer met Kill knop gemarkeerd](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="caf55-233">Uw cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="caf55-233">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="caf55-234">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="caf55-234">Next steps</span></span>

<span data-ttu-id="caf55-235">In dit document hebt u geleerd hoe gebruikt u de spout Java Event Hubs en Bolts uit een C#-topologie wilt werken met gegevens in Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="caf55-235">In this document, you have learned how to use the Java Event Hubs spout and bolt from a C# topology to work with data in Azure Event Hubs.</span></span> <span data-ttu-id="caf55-236">Zie de volgende onderwerpen voor meer informatie over het maken van C#-topologieën:</span><span class="sxs-lookup"><span data-stu-id="caf55-236">To learn more about creating C# topologies, see the following:</span></span>

* [<span data-ttu-id="caf55-237">C#-topologieën ontwikkelen voor Apache Storm op HDInsight met behulp van Visual Studio</span><span class="sxs-lookup"><span data-stu-id="caf55-237">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="caf55-238">Programmeerhandleiding voor SCP</span><span class="sxs-lookup"><span data-stu-id="caf55-238">SCP programming guide</span></span>](hdinsight-storm-scp-programming-guide.md)
* [<span data-ttu-id="caf55-239">Voorbeeldtopologieën van Storm op HDInsight</span><span class="sxs-lookup"><span data-stu-id="caf55-239">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
