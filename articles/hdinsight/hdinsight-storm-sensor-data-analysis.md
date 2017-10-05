---
title: Met Apache Storm en HBase-sensorgegevens analyseren | Microsoft Docs
description: Informatie over het met een virtueel netwerk verbinding maken met Apache Storm. Storm gebruiken met HBase sensor om gegevens te verwerken van een event hub en deze te visualiseren met D3.js.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a9a1ac8e-5708-4833-b965-e453815e671f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/09/2017
ms.author: larryfr
ms.openlocfilehash: 0d1cc959c87bd64ed728f8b56c9b9156fa492a8b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a><span data-ttu-id="4ba49-104">Analyseren van sensorgegevens met Apache Storm, Event Hub en HBase in HDInsight (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="4ba49-104">Analyze sensor data with Apache Storm, Event Hub, and HBase in HDInsight (Hadoop)</span></span>

<span data-ttu-id="4ba49-105">Informatie over het gebruik van Apache Storm op HDInsight om te verwerken van sensorgegevens uit Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="4ba49-105">Learn how to use Apache Storm on HDInsight to process sensor data from Azure Event Hub.</span></span> <span data-ttu-id="4ba49-106">De gegevens vervolgens naar Apache HBase in HDInsight wordt opgeslagen en weergegeven met behulp van D3.js.</span><span class="sxs-lookup"><span data-stu-id="4ba49-106">The data is then stored into Apache HBase on HDInsight, and visualized using D3.js.</span></span>

<span data-ttu-id="4ba49-107">De Azure Resource Manager-sjabloon die wordt gebruikt in dit document wordt gedemonstreerd hoe meerdere Azure-resources in een resourcegroep maken.</span><span class="sxs-lookup"><span data-stu-id="4ba49-107">The Azure Resource Manager template used in this document demonstrates how to create multiple Azure resources in a resource group.</span></span> <span data-ttu-id="4ba49-108">De sjabloon maakt u een Azure-netwerk, twee HDInsight-clusters (Storm en HBase) en een Azure-Web-App.</span><span class="sxs-lookup"><span data-stu-id="4ba49-108">The template creates an Azure Virtual Network, two HDInsight clusters (Storm and HBase) and an Azure Web App.</span></span> <span data-ttu-id="4ba49-109">Een node.js-implementatie van een realtime webdashboard is automatisch geïmplementeerd naar de web-app.</span><span class="sxs-lookup"><span data-stu-id="4ba49-109">A node.js implementation of a real-time web dashboard is automatically deployed to the web app.</span></span>

> [!NOTE]
> <span data-ttu-id="4ba49-110">De informatie in dit document en deze in dit document HDInsight versie 3.6 vereisen.</span><span class="sxs-lookup"><span data-stu-id="4ba49-110">The information in this document and example in this document require HDInsight version 3.6.</span></span>
>
> <span data-ttu-id="4ba49-111">Linux is het enige besturingssysteem dat wordt gebruikt in HDInsight-versie 3.4 of hoger.</span><span class="sxs-lookup"><span data-stu-id="4ba49-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4ba49-112">Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4ba49-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ba49-113">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4ba49-113">Prerequisites</span></span>

* <span data-ttu-id="4ba49-114">Een Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="4ba49-114">An Azure subscription.</span></span>
* <span data-ttu-id="4ba49-115">[Node.js](http://nodejs.org/): gebruikt om een voorbeeld van het webdashboard lokaal op uw ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="4ba49-115">[Node.js](http://nodejs.org/): Used to preview the web dashboard locally on your development environment.</span></span>
* <span data-ttu-id="4ba49-116">[Java en de JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): gebruikt voor het ontwikkelen van de Storm-topologie.</span><span class="sxs-lookup"><span data-stu-id="4ba49-116">[Java and the JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): Used to develop the Storm topology.</span></span>
* <span data-ttu-id="4ba49-117">[Maven](http://maven.apache.org/what-is-maven.html): gebruikt voor het bouwen en compileren van het project.</span><span class="sxs-lookup"><span data-stu-id="4ba49-117">[Maven](http://maven.apache.org/what-is-maven.html): Used to build and compile the project.</span></span>
* <span data-ttu-id="4ba49-118">[GIT](http://git-scm.com/): gebruikt voor het downloaden van het project vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="4ba49-118">[Git](http://git-scm.com/): Used to download the project from GitHub.</span></span>
* <span data-ttu-id="4ba49-119">Een **SSH** client: verbinding maken met de Linux gebaseerde HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="4ba49-119">An **SSH** client: Used to connect to the Linux-based HDInsight clusters.</span></span> <span data-ttu-id="4ba49-120">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4ba49-120">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="4ba49-121">U hoeft niet in een bestaand HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="4ba49-121">You do not need an existing HDInsight cluster.</span></span> <span data-ttu-id="4ba49-122">De stappen in dit document maken de volgende bronnen:</span><span class="sxs-lookup"><span data-stu-id="4ba49-122">The steps in this document create the following resources:</span></span>
> 
> * <span data-ttu-id="4ba49-123">Een Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="4ba49-123">An Azure Virtual Network</span></span>
> * <span data-ttu-id="4ba49-124">Een Storm op HDInsight-cluster (op basis van Linux twee worker-knooppunten)</span><span class="sxs-lookup"><span data-stu-id="4ba49-124">A Storm on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="4ba49-125">Een HBase op HDInsight-cluster (op basis van Linux twee worker-knooppunten)</span><span class="sxs-lookup"><span data-stu-id="4ba49-125">An HBase on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="4ba49-126">Een Azure-Web-App die als host fungeert voor de webdashboard</span><span class="sxs-lookup"><span data-stu-id="4ba49-126">An Azure Web App that hosts the web dashboard</span></span>

## <a name="architecture"></a><span data-ttu-id="4ba49-127">Architectuur</span><span class="sxs-lookup"><span data-stu-id="4ba49-127">Architecture</span></span>

![Architectuurdiagram](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

<span data-ttu-id="4ba49-129">In dit voorbeeld bestaat uit de volgende onderdelen:</span><span class="sxs-lookup"><span data-stu-id="4ba49-129">This example consists of the following components:</span></span>

* <span data-ttu-id="4ba49-130">**Azure Event Hubs**: bevat gegevens die worden verzameld van sensoren.</span><span class="sxs-lookup"><span data-stu-id="4ba49-130">**Azure Event Hubs**: Contains data that is collected from sensors.</span></span>
* <span data-ttu-id="4ba49-131">**Storm op HDInsight**: biedt realtime verwerking van gegevens uit Event Hub.</span><span class="sxs-lookup"><span data-stu-id="4ba49-131">**Storm on HDInsight**: Provides real-time processing of data from Event Hub.</span></span>
* <span data-ttu-id="4ba49-132">**HBase in HDInsight**: biedt een permanente NoSQL-gegevensopslag voor gegevens nadat deze is verwerkt door Storm.</span><span class="sxs-lookup"><span data-stu-id="4ba49-132">**HBase on HDInsight**: Provides a persistent NoSQL data store for data after it has been processed by Storm.</span></span>
* <span data-ttu-id="4ba49-133">**Azure Virtual Network service**: beveiligde communicatie tussen de Storm op HDInsight en HBase op HDInsight-clusters mogelijk maakt.</span><span class="sxs-lookup"><span data-stu-id="4ba49-133">**Azure Virtual Network service**: Enables secure communications between the Storm on HDInsight and HBase on HDInsight clusters.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="4ba49-134">Een virtueel netwerk is vereist wanneer de client Java HBase API.</span><span class="sxs-lookup"><span data-stu-id="4ba49-134">A virtual network is required when using the Java HBase client API.</span></span> <span data-ttu-id="4ba49-135">Het is niet toegankelijk via de openbare gateway voor HBase-clusters.</span><span class="sxs-lookup"><span data-stu-id="4ba49-135">It is not exposed over the public gateway for HBase clusters.</span></span> <span data-ttu-id="4ba49-136">HBase en Storm-clusters in hetzelfde virtuele netwerk te installeren, kunt de Storm-cluster (of elk ander systeem in het virtuele netwerk) rechtstreeks toegang krijgen tot HBase met client-API.</span><span class="sxs-lookup"><span data-stu-id="4ba49-136">Installing HBase and Storm clusters into the same virtual network allows the Storm cluster (or any other system on the virtual network) to directly access HBase using client API.</span></span>

* <span data-ttu-id="4ba49-137">**Dashboard website**: een voorbeeld van dashboard dat gegevens in real-time grafieken.</span><span class="sxs-lookup"><span data-stu-id="4ba49-137">**Dashboard website**: An example dashboard that charts data in real time.</span></span>
  
  * <span data-ttu-id="4ba49-138">De website is geïmplementeerd in Node.js.</span><span class="sxs-lookup"><span data-stu-id="4ba49-138">The website is implemented in Node.js.</span></span>
  * <span data-ttu-id="4ba49-139">[Socket.IO](http://socket.io/) voor realtime-communicatie tussen de Storm-topologie en de website wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4ba49-139">[Socket.io](http://socket.io/) is used for real-time communication between the Storm topology and the website.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="4ba49-140">Met Socket.io voor communicatie is een implementatiedetail.</span><span class="sxs-lookup"><span data-stu-id="4ba49-140">Using Socket.io for communication is an implementation detail.</span></span> <span data-ttu-id="4ba49-141">U kunt elk framework communicatie zoals onbewerkte WebSockets of SignalR gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4ba49-141">You can use any communications framework, such as raw WebSockets or SignalR.</span></span>

  * <span data-ttu-id="4ba49-142">[D3.js](http://d3js.org/) wordt gebruikt voor de gegevens die worden verzonden naar de website in een grafiek.</span><span class="sxs-lookup"><span data-stu-id="4ba49-142">[D3.js](http://d3js.org/) is used to graph the data that is sent to the website.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4ba49-143">Twee clusters zijn vereist, omdat er geen ondersteunde methode is voor het maken van een HDInsight-cluster voor Storm en HBase.</span><span class="sxs-lookup"><span data-stu-id="4ba49-143">Two clusters are required, as there is no supported method to create one HDInsight cluster for both Storm and HBase.</span></span>

<span data-ttu-id="4ba49-144">De topologie leest de gegevens uit Event Hub met behulp van de [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) klasse en schrijft gegevens in HBase met behulp van de [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) klasse.</span><span class="sxs-lookup"><span data-stu-id="4ba49-144">The topology reads data from Event Hub by using the [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) class, and writes data into HBase using the [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) class.</span></span> <span data-ttu-id="4ba49-145">Communicatie met de website kan worden bereikt via [socket.io client.java](https://github.com/nkzawa/socket.io-client.java).</span><span class="sxs-lookup"><span data-stu-id="4ba49-145">Communication with the website is accomplished by using [socket.io-client.java](https://github.com/nkzawa/socket.io-client.java).</span></span>

<span data-ttu-id="4ba49-146">Het volgende diagram wordt de indeling van de topologie uitgelegd:</span><span class="sxs-lookup"><span data-stu-id="4ba49-146">The following diagram explains the layout of the topology:</span></span>

![topologiediagram](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> <span data-ttu-id="4ba49-148">Dit diagram is een vereenvoudigde weergave van de topologie.</span><span class="sxs-lookup"><span data-stu-id="4ba49-148">This diagram is a simplified view of the topology.</span></span> <span data-ttu-id="4ba49-149">Een exemplaar van elk onderdeel is gemaakt voor elke partitie in uw Event Hub.</span><span class="sxs-lookup"><span data-stu-id="4ba49-149">An instance of each component is created for each partition in your Event Hub.</span></span> <span data-ttu-id="4ba49-150">Deze instanties zijn verdeeld over de knooppunten in het cluster en gegevens worden gerouteerd tussen deze als volgt:</span><span class="sxs-lookup"><span data-stu-id="4ba49-150">These instances are distributed across the nodes in the cluster, and data is routed between them as follows:</span></span>
> 
> * <span data-ttu-id="4ba49-151">Gegevens van de spout naar de parser gelijkmatig wordt verdeeld.</span><span class="sxs-lookup"><span data-stu-id="4ba49-151">Data from the spout to the parser is load balanced.</span></span>
> * <span data-ttu-id="4ba49-152">Gegevens van de parser naar het Dashboard en de HBase worden gegroepeerd per apparaat-ID, zodat berichten van hetzelfde apparaat altijd naar hetzelfde onderdeel stromen.</span><span class="sxs-lookup"><span data-stu-id="4ba49-152">Data from the parser to the Dashboard and HBase is grouped by Device ID, so that messages from the same device always flow to the same component.</span></span>

### <a name="topology-components"></a><span data-ttu-id="4ba49-153">Topologie-onderdelen</span><span class="sxs-lookup"><span data-stu-id="4ba49-153">Topology components</span></span>

* <span data-ttu-id="4ba49-154">**Event Hub Spout**: de spout is opgegeven als onderdeel van Apache Storm versie 0.10.0 of hoger.</span><span class="sxs-lookup"><span data-stu-id="4ba49-154">**Event Hub Spout**: The spout is provided as part of Apache Storm version 0.10.0 and higher.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="4ba49-155">De Event Hub spout gebruikt in dit voorbeeld is een Storm op HDInsight-cluster versie 3.5 of 3.6 vereist.</span><span class="sxs-lookup"><span data-stu-id="4ba49-155">The Event Hub spout used in this example requires a Storm on HDInsight cluster version 3.5 or 3.6.</span></span>

* <span data-ttu-id="4ba49-156">**ParserBolt.java**: de gegevens die worden verstrekt door de spout is onbewerkte JSON en van tijd tot tijd meer dan een gebeurtenis op een tijdstip is verzonden.</span><span class="sxs-lookup"><span data-stu-id="4ba49-156">**ParserBolt.java**: The data that is emitted by the spout is raw JSON, and occasionally more than one event is emitted at a time.</span></span> <span data-ttu-id="4ba49-157">Deze bolt leest de gegevens die door de spout en parseert het JSON-bericht.</span><span class="sxs-lookup"><span data-stu-id="4ba49-157">This bolt reads the data emitted by the spout and parses the JSON message.</span></span> <span data-ttu-id="4ba49-158">De bolt verzendt vervolgens de gegevens als een tuple die meerdere velden bevat.</span><span class="sxs-lookup"><span data-stu-id="4ba49-158">The bolt then emits the data as a tuple that contains multiple fields.</span></span>
* <span data-ttu-id="4ba49-159">**DashboardBolt.java**: dit onderdeel wordt getoond hoe u van de clientbibliotheek Socket.io voor Java gegevens in realtime te verzenden naar de webdashboard.</span><span class="sxs-lookup"><span data-stu-id="4ba49-159">**DashboardBolt.java**: This component demonstrates how to use the Socket.io client library for Java to send data in real time to the web dashboard.</span></span>
* <span data-ttu-id="4ba49-160">**Er is geen hbase.yaml**: de definitie van de topologie bij uitvoering in lokale modus gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4ba49-160">**no-hbase.yaml**: The topology definition used when running in local mode.</span></span> <span data-ttu-id="4ba49-161">Het wordt HBase-onderdelen gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4ba49-161">It does not use HBase components.</span></span>
* <span data-ttu-id="4ba49-162">**met hbase.yaml**: de definitie van de topologie die wordt gebruikt bij het uitvoeren van de topologie op het cluster.</span><span class="sxs-lookup"><span data-stu-id="4ba49-162">**with-hbase.yaml**: The topology definition used when running the topology on the cluster.</span></span> <span data-ttu-id="4ba49-163">Dit maakt gebruik van HBase-onderdelen.</span><span class="sxs-lookup"><span data-stu-id="4ba49-163">It does use HBase components.</span></span>
* <span data-ttu-id="4ba49-164">**dev.Properties**: de configuratiegegevens voor de Event Hub spout, HBase bolt en dashboard onderdelen.</span><span class="sxs-lookup"><span data-stu-id="4ba49-164">**dev.properties**: The configuration information for the Event Hub spout, HBase bolt, and dashboard components.</span></span>

## <a name="prepare-your-environment"></a><span data-ttu-id="4ba49-165">Uw omgeving voorbereiden</span><span class="sxs-lookup"><span data-stu-id="4ba49-165">Prepare your environment</span></span>

<span data-ttu-id="4ba49-166">Voordat u dit voorbeeld gebruiken, moet u een Azure Event Hub, die de Storm-topologie leest uit.</span><span class="sxs-lookup"><span data-stu-id="4ba49-166">Before you use this example, you must create an Azure Event Hub, which the Storm topology reads from.</span></span>

### <a name="configure-event-hub"></a><span data-ttu-id="4ba49-167">Event Hub configureren</span><span class="sxs-lookup"><span data-stu-id="4ba49-167">Configure Event Hub</span></span>

<span data-ttu-id="4ba49-168">Event Hub is de gegevensbron voor dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="4ba49-168">Event Hub is the data source for this example.</span></span> <span data-ttu-id="4ba49-169">Gebruik de volgende stappen voor het maken van een Event Hub.</span><span class="sxs-lookup"><span data-stu-id="4ba49-169">Use the following steps to create an Event Hub.</span></span>

1. <span data-ttu-id="4ba49-170">Van de [Azure-portal](https://portal.azure.com), selecteer **+ nieuw** -> **Internet der dingen** -> **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="4ba49-170">From the [Azure portal](https://portal.azure.com), select **+ New** -> **Internet of Things** -> **Event Hubs**.</span></span>
2. <span data-ttu-id="4ba49-171">In de **Namespace maken** sectie, de volgende taken uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="4ba49-171">In the **Create Namespace** section, perform the following tasks:</span></span>
   
   1. <span data-ttu-id="4ba49-172">Voer een **naam** voor de naamruimte.</span><span class="sxs-lookup"><span data-stu-id="4ba49-172">Enter a **Name** for the namespace.</span></span>
   2. <span data-ttu-id="4ba49-173">Selecteer een prijscategorie.</span><span class="sxs-lookup"><span data-stu-id="4ba49-173">Select a pricing tier.</span></span> <span data-ttu-id="4ba49-174">**Basic** voldoende is voor dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="4ba49-174">**Basic** is sufficient for this example.</span></span>
   3. <span data-ttu-id="4ba49-175">Selecteer de Azure **abonnement** te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="4ba49-175">Select the Azure **Subscription** to use.</span></span>
   4. <span data-ttu-id="4ba49-176">Selecteer een bestaande resourcegroep of maak een nieuwe.</span><span class="sxs-lookup"><span data-stu-id="4ba49-176">Either select an existing resource group or create a new one.</span></span>
   5. <span data-ttu-id="4ba49-177">Selecteer de **locatie** voor de Event Hub.</span><span class="sxs-lookup"><span data-stu-id="4ba49-177">Select the **Location** for the Event Hub.</span></span>
   6. <span data-ttu-id="4ba49-178">Selecteer **vastmaken aan dashboard**, en klik vervolgens op **maken**.</span><span class="sxs-lookup"><span data-stu-id="4ba49-178">Select **Pin to dashboard**, and then click **Create**.</span></span>

3. <span data-ttu-id="4ba49-179">Wanneer het proces voor het maken is voltooid, wordt de Event Hubs-informatie voor uw naamruimte wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4ba49-179">When the creation process completes, the Event Hubs information for your namespace is displayed.</span></span> <span data-ttu-id="4ba49-180">Hier kunt u selecteren **+ Event Hub toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="4ba49-180">From here, select **+ Add Event Hub**.</span></span> <span data-ttu-id="4ba49-181">In de **Event Hub maken** sectie, voer een naam in van **sensordata**, en selecteer vervolgens **maken**.</span><span class="sxs-lookup"><span data-stu-id="4ba49-181">In the **Create Event Hub** section, enter a name of **sensordata**, and then select **Create**.</span></span> <span data-ttu-id="4ba49-182">Laat de overige velden op de standaardwaarden.</span><span class="sxs-lookup"><span data-stu-id="4ba49-182">Leave the other fields at the default values.</span></span>
4. <span data-ttu-id="4ba49-183">Selecteer in de Event Hubs-weergave voor de naamruimte, **Event Hubs**.</span><span class="sxs-lookup"><span data-stu-id="4ba49-183">From the Event Hubs view for your namespace, select **Event Hubs**.</span></span> <span data-ttu-id="4ba49-184">Selecteer de **sensordata** vermelding.</span><span class="sxs-lookup"><span data-stu-id="4ba49-184">Select the **sensordata** entry.</span></span>
5. <span data-ttu-id="4ba49-185">Selecteer in de Event Hub sensordata **gedeeld toegangsbeleid**.</span><span class="sxs-lookup"><span data-stu-id="4ba49-185">From the sensordata Event Hub, select **Shared access policies**.</span></span> <span data-ttu-id="4ba49-186">Gebruik de **+ toevoegen** koppeling naar de volgende beleidsregels toevoegen:</span><span class="sxs-lookup"><span data-stu-id="4ba49-186">Use the **+ Add** link to add the following policies:</span></span>

    | <span data-ttu-id="4ba49-187">De naam van beleid</span><span class="sxs-lookup"><span data-stu-id="4ba49-187">Policy name</span></span> | <span data-ttu-id="4ba49-188">Claims</span><span class="sxs-lookup"><span data-stu-id="4ba49-188">Claims</span></span> |
    | ----- | ----- |
    | <span data-ttu-id="4ba49-189">apparaten</span><span class="sxs-lookup"><span data-stu-id="4ba49-189">devices</span></span> | <span data-ttu-id="4ba49-190">Verzenden</span><span class="sxs-lookup"><span data-stu-id="4ba49-190">Send</span></span> |
    | <span data-ttu-id="4ba49-191">storm</span><span class="sxs-lookup"><span data-stu-id="4ba49-191">storm</span></span> | <span data-ttu-id="4ba49-192">Luisteren</span><span class="sxs-lookup"><span data-stu-id="4ba49-192">Listen</span></span> |

1. <span data-ttu-id="4ba49-193">Selecteer beide beleidsregels en noteer de **primaire sleutel** waarde.</span><span class="sxs-lookup"><span data-stu-id="4ba49-193">Select both policies and make a note of the **PRIMARY KEY** value.</span></span> <span data-ttu-id="4ba49-194">U moet de waarde voor beide beleidsregels in toekomstige stappen.</span><span class="sxs-lookup"><span data-stu-id="4ba49-194">You need the value for both policies in future steps.</span></span>

## <a name="download-and-configure-the-project"></a><span data-ttu-id="4ba49-195">Downloaden en configureren van het project</span><span class="sxs-lookup"><span data-stu-id="4ba49-195">Download and configure the project</span></span>

<span data-ttu-id="4ba49-196">Gebruik de volgende voor het downloaden van het project vanuit GitHub.</span><span class="sxs-lookup"><span data-stu-id="4ba49-196">Use the following to download the project from GitHub.</span></span>

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

<span data-ttu-id="4ba49-197">Nadat de opdracht is voltooid, hebt u de volgende mapstructuur:</span><span class="sxs-lookup"><span data-stu-id="4ba49-197">After the command completes, you have the following directory structure:</span></span>

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains the topology
            resources/
                log4j2.xml - set logging to minimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO to the web dashboard.
        dashboard/nodejs/ - this is the node.js web dashboard.
        SendEvents/ - utilities to send fake sensor data.

> [!NOTE]
> <span data-ttu-id="4ba49-198">Dit document niet naar alle details van de code die is opgenomen in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="4ba49-198">This document does not go in to full details of the code included in this example.</span></span> <span data-ttu-id="4ba49-199">De code is echter volledig toegelicht.</span><span class="sxs-lookup"><span data-stu-id="4ba49-199">However, the code is fully commented.</span></span>

<span data-ttu-id="4ba49-200">Voor het configureren van het project lezen uit Event Hub, opent u de `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` -bestand en de informatie van uw Event Hub toevoegen aan de volgende regels:</span><span class="sxs-lookup"><span data-stu-id="4ba49-200">To configure the project to read from Event Hub, open the `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` file and add your Event Hub information to the following lines:</span></span>

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a><span data-ttu-id="4ba49-201">Compileren en lokaal te testen</span><span class="sxs-lookup"><span data-stu-id="4ba49-201">Compile and test locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4ba49-202">De topologie lokaal, moet een werkende Storm-ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="4ba49-202">Using the topology locally requires a working Storm development environment.</span></span> <span data-ttu-id="4ba49-203">Zie voor meer informatie [een Storm-ontwikkelomgeving instellen](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) op Apache.org.</span><span class="sxs-lookup"><span data-stu-id="4ba49-203">For more information, see [Setting up a Storm development environment](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) at Apache.org.</span></span>

> [!WARNING]
> <span data-ttu-id="4ba49-204">Als u van een Windows-ontwikkelomgeving gebruikmaakt, ontvangt u mogelijk een `java.io.IOException` wanneer de topologie die lokaal wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4ba49-204">If you are using a Windows development environment, you may receive a `java.io.IOException` when running the topology locally.</span></span> <span data-ttu-id="4ba49-205">Zo ja, verplaatsen op voor het uitvoeren van de topologie op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4ba49-205">If so, move on to running the topology on HDInsight.</span></span>

<span data-ttu-id="4ba49-206">Voordat u test, moet u het dashboard voor het weergeven van de uitvoer van de topologie en genereren van gegevens op te slaan in de Event Hub starten.</span><span class="sxs-lookup"><span data-stu-id="4ba49-206">Before testing, you must start the dashboard to view the output of the topology and generate data to store in Event Hub.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4ba49-207">Het HBase-onderdeel van deze topologie is niet actief bij lokaal te testen.</span><span class="sxs-lookup"><span data-stu-id="4ba49-207">The HBase component of this topology is not active when testing locally.</span></span> <span data-ttu-id="4ba49-208">De Java-API voor het HBase-cluster niet toegankelijk van buiten het virtuele netwerk van Azure die de clusters bevat.</span><span class="sxs-lookup"><span data-stu-id="4ba49-208">The Java API for the HBase cluster cannot be accessed from outside the Azure Virtual Network that contains the clusters.</span></span>

### <a name="start-the-web-application"></a><span data-ttu-id="4ba49-209">De webtoepassing starten</span><span class="sxs-lookup"><span data-stu-id="4ba49-209">Start the web application</span></span>

1. <span data-ttu-id="4ba49-210">Open een opdrachtprompt en wijzig de mappen te `hdinsight-eventhub-example/dashboard`.</span><span class="sxs-lookup"><span data-stu-id="4ba49-210">Open a command prompt and change directories to `hdinsight-eventhub-example/dashboard`.</span></span> <span data-ttu-id="4ba49-211">Gebruik de volgende opdracht voor het installeren van de afhankelijkheden die nodig is voor de webtoepassing:</span><span class="sxs-lookup"><span data-stu-id="4ba49-211">Use the following command to install the dependencies needed by the web application:</span></span>
   
    ```bash
    npm install
    ```

2. <span data-ttu-id="4ba49-212">Gebruik de volgende opdracht om de webtoepassing te starten:</span><span class="sxs-lookup"><span data-stu-id="4ba49-212">Use the following command to start the web application:</span></span>
   
    ```bash
    node server.js
    ```
   
    <span data-ttu-id="4ba49-213">U ziet een bericht dat lijkt op de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="4ba49-213">You see a message similar to the following text:</span></span>
   
        Server listening at port 3000

3. <span data-ttu-id="4ba49-214">Open een webbrowser en voer `http://localhost:3000/` als het adres.</span><span class="sxs-lookup"><span data-stu-id="4ba49-214">Open a web browser and enter `http://localhost:3000/` as the address.</span></span> <span data-ttu-id="4ba49-215">Een pagina zoals in de volgende afbeelding wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="4ba49-215">A page similar to the following image is displayed:</span></span>
   
    ![webdashboard](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    <span data-ttu-id="4ba49-217">Laat deze opdrachtprompt geopend.</span><span class="sxs-lookup"><span data-stu-id="4ba49-217">Leave this command prompt open.</span></span> <span data-ttu-id="4ba49-218">Nadat u hebt getest, gebruik Ctrl + C om te stoppen van de webserver.</span><span class="sxs-lookup"><span data-stu-id="4ba49-218">After testing, use Ctrl-C to stop the web server.</span></span>

### <a name="generate-data"></a><span data-ttu-id="4ba49-219">Gegevens moeten genereren</span><span class="sxs-lookup"><span data-stu-id="4ba49-219">Generate data</span></span>

> [!NOTE]
> <span data-ttu-id="4ba49-220">De stappen in deze sectie gebruiken Node.js, zodat ze kunnen worden gebruikt op elk platform.</span><span class="sxs-lookup"><span data-stu-id="4ba49-220">The steps in this section use Node.js so that they can be used on any platform.</span></span> <span data-ttu-id="4ba49-221">Zie voor voorbeelden van andere taal de `SendEvents` directory.</span><span class="sxs-lookup"><span data-stu-id="4ba49-221">For other language examples, see the `SendEvents` directory.</span></span>

1. <span data-ttu-id="4ba49-222">Open een nieuw opdrachtprompt, shell of terminal en wijzig de mappen te `hdinsight-eventhub-example/SendEvents/nodejs`.</span><span class="sxs-lookup"><span data-stu-id="4ba49-222">Open a new prompt, shell, or terminal, and change directories to `hdinsight-eventhub-example/SendEvents/nodejs`.</span></span> <span data-ttu-id="4ba49-223">Gebruik de volgende opdracht voor het installeren van de afhankelijkheden die nodig is voor de toepassing:</span><span class="sxs-lookup"><span data-stu-id="4ba49-223">To install the dependencies needed by the application, use the following command:</span></span>

    ```bash
    npm install
    ```

2. <span data-ttu-id="4ba49-224">Open de `app.js` -bestand in een teksteditor en voeg de Event Hub-informatie die u eerder hebt verkregen toe:</span><span class="sxs-lookup"><span data-stu-id="4ba49-224">Open the `app.js` file in a text editor and add the Event Hub information you obtained earlier:</span></span>
   
    ```javascript
    // ServiceBus Namespace
    var namespace = 'YourNamespace';
    // Event Hub Name
    var hubname ='sensordata';
    // Shared access Policy name and key (from Event Hub configuration)
    var my_key_name = 'devices';
    var my_key = 'YourKey';
    ```
   
   > [!NOTE]
   > <span data-ttu-id="4ba49-225">In dit voorbeeld wordt ervan uitgegaan dat u hebt gebruikt `sensordata` als de naam van uw Event Hub.</span><span class="sxs-lookup"><span data-stu-id="4ba49-225">This example assumes that you have used `sensordata` as the name of your Event Hub.</span></span> <span data-ttu-id="4ba49-226">En dat `devices` als de naam van het beleid dat is een `Send` claim.</span><span class="sxs-lookup"><span data-stu-id="4ba49-226">And that `devices` as the name of the policy that has a `Send` claim.</span></span>

3. <span data-ttu-id="4ba49-227">Gebruik de volgende opdracht voor het invoegen van nieuwe vermeldingen in de Event Hub:</span><span class="sxs-lookup"><span data-stu-id="4ba49-227">Use the following command to insert new entries in Event Hub:</span></span>
   
    ```bash
    node app.js
    ```
   
    <span data-ttu-id="4ba49-228">Er zijn meerdere regels van uitvoer met de gegevens verzonden naar de Event Hub:</span><span class="sxs-lookup"><span data-stu-id="4ba49-228">You see several lines of output that contain the data sent to Event Hub:</span></span>
   
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"0","Temperature":7}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"1","Temperature":39}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"2","Temperature":86}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"3","Temperature":29}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"4","Temperature":30}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"5","Temperature":5}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"6","Temperature":24}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"7","Temperature":40}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"8","Temperature":43}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"9","Temperature":84}

### <a name="build-and-start-the-topology"></a><span data-ttu-id="4ba49-229">Bouwen en starten van de topologie</span><span class="sxs-lookup"><span data-stu-id="4ba49-229">Build and start the topology</span></span>

1. <span data-ttu-id="4ba49-230">Open een nieuw opdrachtpromptvenster en wijzig de mappen te `hdinsight-eventhub-example/TemperatureMonitor`.</span><span class="sxs-lookup"><span data-stu-id="4ba49-230">Open a new command prompt and change directories to `hdinsight-eventhub-example/TemperatureMonitor`.</span></span> <span data-ttu-id="4ba49-231">Voor het bouwen en de topologie van het pakket, gebruikt u de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="4ba49-231">To build and package the topology, use the following command:</span></span> 

    ```bash
    mvn clean package
    ```

2. <span data-ttu-id="4ba49-232">Voor het starten van de topologie in de lokale modus, moet u de volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="4ba49-232">To start the topology in local mode, use the following command:</span></span>

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * <span data-ttu-id="4ba49-233">`--local`Start de topologie in lokale modus.</span><span class="sxs-lookup"><span data-stu-id="4ba49-233">`--local` starts the topology in local mode.</span></span>
    * <span data-ttu-id="4ba49-234">`--filter`maakt gebruik van de `dev.properties` bestand voor het vullen van de parameters in de definitie van de topologie.</span><span class="sxs-lookup"><span data-stu-id="4ba49-234">`--filter` uses the `dev.properties` file to populate parameters in the topology definition.</span></span>
    * <span data-ttu-id="4ba49-235">`resources/no-hbase.yaml`maakt gebruik van de `no-hbase.yaml` topologie definitie.</span><span class="sxs-lookup"><span data-stu-id="4ba49-235">`resources/no-hbase.yaml` uses the `no-hbase.yaml` topology definition.</span></span>
 
   <span data-ttu-id="4ba49-236">Eenmaal gestart, wordt de topologie vermeldingen van Event Hub leest en zendt deze naar het dashboard op uw lokale computer uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="4ba49-236">Once started, the topology reads entries from Event Hub, and sends them to the dashboard running on your local machine.</span></span> <span data-ttu-id="4ba49-237">Hier ziet u regels worden weergegeven in het webdashboard, vergelijkbaar met de volgende afbeelding:</span><span class="sxs-lookup"><span data-stu-id="4ba49-237">You should see lines appear in the web dashboard, similar to the following image:</span></span>
   
    ![dashboard met gegevens](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. <span data-ttu-id="4ba49-239">Terwijl het dashboard wordt uitgevoerd, gebruikt u de `node app.js` opdracht van de vorige stappen voor het nieuwe gegevens verzenden naar Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="4ba49-239">While the dashboard is running, use the `node app.js` command from the previous steps to send new data to Event Hubs.</span></span> <span data-ttu-id="4ba49-240">Omdat de temperatuur-waarden worden willekeurig gegenereerd, de grafiek moet worden bijgewerkt voor het weergeven van grote wijzigingen in de temperatuur.</span><span class="sxs-lookup"><span data-stu-id="4ba49-240">Because the temperature values are randomly generated, the graph should update to show large changes in temperature.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4ba49-241">U moet zich in de **hdinsight-eventhub-voorbeeld/SendEvents/Nodejs** directory wanneer u de `node app.js` opdracht.</span><span class="sxs-lookup"><span data-stu-id="4ba49-241">You must be in the **hdinsight-eventhub-example/SendEvents/Nodejs** directory when using the `node app.js` command.</span></span>

3. <span data-ttu-id="4ba49-242">Nadat u hebt gecontroleerd dat het dashboard worden bijgewerkt, stopt u de topologie met Ctrl + C.</span><span class="sxs-lookup"><span data-stu-id="4ba49-242">After verifying that the dashboard updates, stop the topology using Ctrl+C.</span></span> <span data-ttu-id="4ba49-243">Ctrl + C kunt u ook de lokale webserver stoppen.</span><span class="sxs-lookup"><span data-stu-id="4ba49-243">You can use Ctrl+C to stop the local web server also.</span></span>

## <a name="create-a-storm-and-hbase-cluster"></a><span data-ttu-id="4ba49-244">Een Storm en HBase-cluster maken</span><span class="sxs-lookup"><span data-stu-id="4ba49-244">Create a Storm and HBase cluster</span></span>

<span data-ttu-id="4ba49-245">De stappen in deze sectie gebruiken een [Azure Resource Manager-sjabloon](../azure-resource-manager/resource-group-template-deploy.md) voor het maken van een virtueel Azure-netwerk en een Storm en HBase-cluster op het virtuele netwerk.</span><span class="sxs-lookup"><span data-stu-id="4ba49-245">The steps in this section use an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) to create an Azure Virtual Network and a Storm and HBase cluster on the virtual network.</span></span> <span data-ttu-id="4ba49-246">De sjabloon ook een Azure-Web-App maakt en implementeert een kopie van het dashboard in de App.</span><span class="sxs-lookup"><span data-stu-id="4ba49-246">The template also creates an Azure Web App and deploys a copy of the dashboard into it.</span></span>

> [!NOTE]
> <span data-ttu-id="4ba49-247">Een virtueel netwerk wordt gebruikt zodat de topologie die wordt uitgevoerd op het Storm-cluster kan rechtstreeks communiceren met de HBase-cluster met de HBase-Java-API.</span><span class="sxs-lookup"><span data-stu-id="4ba49-247">A virtual network is used so that the topology running on the Storm cluster can directly communicate with the HBase cluster using the HBase Java API.</span></span>

<span data-ttu-id="4ba49-248">De Resource Manager-sjabloon gebruikt in dit document bevindt zich in een openbare blob-container op **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span><span class="sxs-lookup"><span data-stu-id="4ba49-248">The Resource Manager template used in this document is located in a public blob container at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span></span>

1. <span data-ttu-id="4ba49-249">Klik op de knop Volgende om te melden bij Azure en open de Resource Manager-sjabloon in de Azure-portal.</span><span class="sxs-lookup"><span data-stu-id="4ba49-249">Click the following button to sign in to Azure and open the Resource Manager template in the Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy to Azure"></a>

2. <span data-ttu-id="4ba49-250">Van de **aangepaste implementatie** sectie, voer de volgende waarden:</span><span class="sxs-lookup"><span data-stu-id="4ba49-250">From the **Custom deployment** section, enter the following values:</span></span>
   
    ![HDInsight-parameters](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * <span data-ttu-id="4ba49-252">**Clusternaam baseren**: deze waarde wordt gebruikt als de basisnaam aan voor de Storm en HBase-clusters.</span><span class="sxs-lookup"><span data-stu-id="4ba49-252">**Base Cluster Name**: This value is used as the base name for the Storm and HBase clusters.</span></span> <span data-ttu-id="4ba49-253">Bijvoorbeeld, voeren **abc** maakt een Storm-cluster met de naam **storm abc** en een HBase-cluster met de naam **hbase abc**.</span><span class="sxs-lookup"><span data-stu-id="4ba49-253">For example, entering **abc** creates a Storm cluster named **storm-abc** and an HBase cluster named **hbase-abc**.</span></span>
   * <span data-ttu-id="4ba49-254">**Aanmeldingsnaam van gebruiker cluster**: de gebruikersnaam van de beheerder voor de Storm en HBase-clusters.</span><span class="sxs-lookup"><span data-stu-id="4ba49-254">**Cluster Login User Name**: The admin user name for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="4ba49-255">**Aanmeldingswachtwoord cluster**: het beheerderswachtwoord voor de Storm en HBase-clusters.</span><span class="sxs-lookup"><span data-stu-id="4ba49-255">**Cluster Login Password**: The admin user password for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="4ba49-256">**SSH-gebruikersnaam**: de SSH-gebruiker maken voor de Storm en HBase-clusters.</span><span class="sxs-lookup"><span data-stu-id="4ba49-256">**SSH User Name**: The SSH user to create for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="4ba49-257">**SSH-wachtwoord**: het wachtwoord voor de SSH-gebruiker voor de Storm en HBase-clusters.</span><span class="sxs-lookup"><span data-stu-id="4ba49-257">**SSH Password**: The password for the SSH user for the Storm and HBase clusters.</span></span>
   * <span data-ttu-id="4ba49-258">**Locatie**: de regio die in de clusters worden gemaakt.</span><span class="sxs-lookup"><span data-stu-id="4ba49-258">**Location**: The region that the clusters are created in.</span></span>
     
     <span data-ttu-id="4ba49-259">Klik op **OK** om de parameters op te slaan.</span><span class="sxs-lookup"><span data-stu-id="4ba49-259">Click **OK** to save the parameters.</span></span>

3. <span data-ttu-id="4ba49-260">Gebruik de **basisbeginselen** sectie een resourcegroep maken of een bestaande set selecteren.</span><span class="sxs-lookup"><span data-stu-id="4ba49-260">Use the **Basics** section to create a resource group or select an existing one.</span></span>
4. <span data-ttu-id="4ba49-261">In de **locatie voor resourcegroep** vervolgkeuzemenu Selecteer dezelfde locatie als u geselecteerd voor de **locatie** parameter in de **instellingen** sectie.</span><span class="sxs-lookup"><span data-stu-id="4ba49-261">In the **Resource group location** dropdown menu, select the same location as you selected for the **Location** parameter in the **Settings** section.</span></span>
5. <span data-ttu-id="4ba49-262">Lees de voorwaarden en selecteer vervolgens **ik ga akkoord met de voorwaarden en bepalingen bovengenoemde**.</span><span class="sxs-lookup"><span data-stu-id="4ba49-262">Read the terms and conditions, and then select **I agree to the terms and conditions stated above**.</span></span>
6. <span data-ttu-id="4ba49-263">Controleer ten slotte **vastmaken aan dashboard** en selecteer vervolgens **aankoop**.</span><span class="sxs-lookup"><span data-stu-id="4ba49-263">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="4ba49-264">Het duurt ongeveer 20 minuten om de clusters te maken.</span><span class="sxs-lookup"><span data-stu-id="4ba49-264">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="4ba49-265">Zodra de resources zijn gemaakt, wordt informatie over de resourcegroep weergegeven.</span><span class="sxs-lookup"><span data-stu-id="4ba49-265">Once the resources have been created, information about the resource group is displayed.</span></span>

![De resourcegroep voor het vnet en clusters](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="4ba49-267">Merk op dat de namen van de HDInsight-clusters **storm BASENAME** en **hbase BASENAME**, waarbij BASENAME is de naam die u hebt opgegeven in de sjabloon.</span><span class="sxs-lookup"><span data-stu-id="4ba49-267">Notice that the names of the HDInsight clusters are **storm-BASENAME** and **hbase-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="4ba49-268">U gebruikt deze namen in een latere stap bij het verbinden met de clusters.</span><span class="sxs-lookup"><span data-stu-id="4ba49-268">You use these names in a later step when connecting to the clusters.</span></span> <span data-ttu-id="4ba49-269">Ook Let op: de naam van de dashboardsite is **basename dashboard**.</span><span class="sxs-lookup"><span data-stu-id="4ba49-269">Also note that the name of the dashboard site is **basename-dashboard**.</span></span> <span data-ttu-id="4ba49-270">Deze waarde wordt verderop in dit document gebruikt.</span><span class="sxs-lookup"><span data-stu-id="4ba49-270">This value is used later in this document.</span></span>

## <a name="configure-the-dashboard-bolt"></a><span data-ttu-id="4ba49-271">Het Dashboard bolt configureren</span><span class="sxs-lookup"><span data-stu-id="4ba49-271">Configure the Dashboard bolt</span></span>

<span data-ttu-id="4ba49-272">Om gegevens te verzenden naar het dashboard dat is geïmplementeerd als een web-app, moet u de volgende regel in wijzigen de `dev.properties`bestand:</span><span class="sxs-lookup"><span data-stu-id="4ba49-272">To send data to the dashboard deployed as a web app, you must modify the following line in the `dev.properties`file:</span></span>

```yaml
dashboard.uri: http://localhost:3000
```

<span data-ttu-id="4ba49-273">Wijziging `http://localhost:3000` naar `http://BASENAME-dashboard.azurewebsites.net` en sla het bestand.</span><span class="sxs-lookup"><span data-stu-id="4ba49-273">Change `http://localhost:3000` to `http://BASENAME-dashboard.azurewebsites.net` and save the file.</span></span> <span data-ttu-id="4ba49-274">Vervang **BASENAME** met de basisnaam die u hebt opgegeven in de vorige stap.</span><span class="sxs-lookup"><span data-stu-id="4ba49-274">Replace **BASENAME** with the base name you provided in the previous step.</span></span> <span data-ttu-id="4ba49-275">Ook kunt u de resourcegroep die eerder hebt gemaakt om te selecteren van het dashboard en de URL.</span><span class="sxs-lookup"><span data-stu-id="4ba49-275">You can also use the resource group created previously to select the dashboard and view the URL.</span></span>

## <a name="create-the-hbase-table"></a><span data-ttu-id="4ba49-276">De HBase-tabel maken</span><span class="sxs-lookup"><span data-stu-id="4ba49-276">Create the HBase table</span></span>

<span data-ttu-id="4ba49-277">Voor het opslaan van gegevens in HBase, moeten we eerst een tabel maken.</span><span class="sxs-lookup"><span data-stu-id="4ba49-277">To store data in HBase, we must first create a table.</span></span> <span data-ttu-id="4ba49-278">Resources die Storm nodig heeft om te schrijven naar vooraf maken, als bij het maken van bronnen van binnen een Storm topologie kan leiden tot meerdere exemplaren wilt maken van dezelfde resource.</span><span class="sxs-lookup"><span data-stu-id="4ba49-278">Pre-create resources that Storm needs to write to, as trying to create resources from inside a Storm topology can result in multiple instances trying to create the same resource.</span></span> <span data-ttu-id="4ba49-279">Maken van de bronnen buiten de topologie en Storm gebruiken voor lezen/schrijven en analyses.</span><span class="sxs-lookup"><span data-stu-id="4ba49-279">Create the resources outside the topology and use Storm for reading/writing and analytics.</span></span>

1. <span data-ttu-id="4ba49-280">SSH gebruiken voor verbinding met de HBase-cluster met behulp van de SSH-gebruiker en het wachtwoord die u hebt opgegeven in de sjabloon tijdens het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="4ba49-280">Use SSH to connect to the HBase cluster using the SSH user and password you supplied to the template during cluster creation.</span></span> <span data-ttu-id="4ba49-281">Bijvoorbeeld, als u verbinding maakt met behulp van de `ssh` opdracht, gebruikt u de volgende syntaxis:</span><span class="sxs-lookup"><span data-stu-id="4ba49-281">For example, if connecting using the `ssh` command, you would use the following syntax:</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    <span data-ttu-id="4ba49-282">Vervang `sshuser` met de SSH-gebruikersnaam die u hebt opgegeven bij het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="4ba49-282">Replace `sshuser` with the SSH user name you provided when creating the cluster.</span></span> <span data-ttu-id="4ba49-283">Vervang `clustername` met de naam van het HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="4ba49-283">Replace `clustername` with the HBase cluster name.</span></span>

2. <span data-ttu-id="4ba49-284">Start de HBase-shell op de SSH-sessie.</span><span class="sxs-lookup"><span data-stu-id="4ba49-284">From the SSH session, start the HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="4ba49-285">Nadat de shell is geladen, ziet u een `hbase(main):001:0>` prompt.</span><span class="sxs-lookup"><span data-stu-id="4ba49-285">Once the shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="4ba49-286">Voer de volgende opdracht om een tabel voor het opslaan van de sensorgegevens maken vanuit de HBase-shell:</span><span class="sxs-lookup"><span data-stu-id="4ba49-286">From the HBase shell, enter the following command to create a table to store the sensor data:</span></span>
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. <span data-ttu-id="4ba49-287">Controleer of dat de tabel is gemaakt met behulp van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="4ba49-287">Verify that the table has been created by using the following command:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="4ba49-288">Hiermee wordt informatie vergelijkbaar met het volgende voorbeeld, wat betekent dat er 0 rijen in de tabel.</span><span class="sxs-lookup"><span data-stu-id="4ba49-288">This returns information similar to the following example, indicating that there are 0 rows in the table.</span></span>
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. <span data-ttu-id="4ba49-289">Voer `exit` om af te sluiten van de HBase-shell:</span><span class="sxs-lookup"><span data-stu-id="4ba49-289">Enter `exit` to exit the HBase shell:</span></span>

## <a name="configure-the-hbase-bolt"></a><span data-ttu-id="4ba49-290">De HBase-bolt configureren</span><span class="sxs-lookup"><span data-stu-id="4ba49-290">Configure the HBase bolt</span></span>

<span data-ttu-id="4ba49-291">Voor het schrijven naar HBase uit het Storm-cluster, moet u de HBase-bolt opgeven met de configuratiedetails van uw HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="4ba49-291">To write to HBase from the Storm cluster, you must provide the HBase bolt with the configuration details of your HBase cluster.</span></span>

1. <span data-ttu-id="4ba49-292">Gebruik een van de volgende voorbeelden voor het ophalen van het quorum Zookeeper voor uw HBase-cluster:</span><span class="sxs-lookup"><span data-stu-id="4ba49-292">Use one of the following examples to retrieve the Zookeeper quorum for your HBase cluster:</span></span>

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > <span data-ttu-id="4ba49-293">Vervang `your_HDInsight_cluster_name` door de naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="4ba49-293">Replace `your_HDInsight_cluster_name` with the name of your HDInsight cluster.</span></span> <span data-ttu-id="4ba49-294">Voor meer informatie over het installeren van de `jq` hulpprogramma, Zie [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="4ba49-294">For more information on installing the `jq` utility, see [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span></span>
    >
    > <span data-ttu-id="4ba49-295">Voer desgevraagd het wachtwoord voor aanmelding bij de HDInsight-beheerder.</span><span class="sxs-lookup"><span data-stu-id="4ba49-295">When prompted, enter the password for the HDInsight admin login.</span></span>

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > <span data-ttu-id="4ba49-296">Vervang ' your_HDInsight_cluster_name met de naam van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="4ba49-296">Replace \`your_HDInsight_cluster_name with the name of your HDInsight cluster.</span></span> <span data-ttu-id="4ba49-297">Voer desgevraagd het wachtwoord voor aanmelding bij de HDInsight-beheerder.</span><span class="sxs-lookup"><span data-stu-id="4ba49-297">When prompted, enter the password for the HDInsight admin login.</span></span>
    >
    > <span data-ttu-id="4ba49-298">Dit voorbeeld vereist Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4ba49-298">This example requires Azure PowerShell.</span></span> <span data-ttu-id="4ba49-299">Zie voor meer informatie over het gebruik van Azure PowerShell [aan de slag met Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span><span class="sxs-lookup"><span data-stu-id="4ba49-299">For more information on using Azure PowerShell, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span></span>

    <span data-ttu-id="4ba49-300">De informatie die wordt geretourneerd door deze voorbeelden is vergelijkbaar met de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="4ba49-300">The information returned by these examples is similar to the following text:</span></span>

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    <span data-ttu-id="4ba49-301">Deze informatie wordt gebruikt door Storm om te communiceren met de HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="4ba49-301">This information is used by Storm to communicate with the HBase cluster.</span></span>

2. <span data-ttu-id="4ba49-302">Wijzig de `dev.properties` -bestand en de Zookeeper quorum informatie toevoegen aan de volgende regel:</span><span class="sxs-lookup"><span data-stu-id="4ba49-302">Modify the `dev.properties` file and add the Zookeeper quorum information to the following line:</span></span>

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-the-solution-to-hdinsight"></a><span data-ttu-id="4ba49-303">Bouwen, pakket, en de oplossing implementeren in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4ba49-303">Build, package, and deploy the solution to HDInsight</span></span>

<span data-ttu-id="4ba49-304">Gebruik de volgende stappen voor het implementeren van de Storm-topologie met het storm-cluster in uw ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="4ba49-304">In your development environment, use the following steps to deploy the Storm topology to the storm cluster.</span></span>

1. <span data-ttu-id="4ba49-305">Van de `TemperatureMonitor` directory, gebruik de volgende opdracht voor het uitvoeren van een nieuwe build en maak een JAR-pakket van uw project:</span><span class="sxs-lookup"><span data-stu-id="4ba49-305">From the `TemperatureMonitor` directory, use the following command to perform a new build and create a JAR package from your project:</span></span>
   
        mvn clean package
   
    <span data-ttu-id="4ba49-306">Deze opdracht maakt u een bestand met de naam `TemperatureMonitor-1.0-SNAPSHOT.jar in the `doel ' map van uw project.</span><span class="sxs-lookup"><span data-stu-id="4ba49-306">This command creates a file named `TemperatureMonitor-1.0-SNAPSHOT.jar in the `target\` directory of your project.</span></span>

2. <span data-ttu-id="4ba49-307">Scp gebruiken voor het uploaden van de `TemperatureMonitor-1.0-SNAPSHOT.jar` en `dev.properties` bestanden naar uw Storm-cluster.</span><span class="sxs-lookup"><span data-stu-id="4ba49-307">Use scp to upload the `TemperatureMonitor-1.0-SNAPSHOT.jar` and `dev.properties` files to your Storm cluster.</span></span> <span data-ttu-id="4ba49-308">Vervang in het volgende voorbeeld wordt `sshuser` met de SSH-gebruiker die u hebt opgegeven bij het maken van het cluster en `clustername` met de naam van uw Storm-cluster.</span><span class="sxs-lookup"><span data-stu-id="4ba49-308">In the following example, replace `sshuser` with the SSH user you provided when creating the cluster, and `clustername` with the name of your Storm cluster.</span></span> <span data-ttu-id="4ba49-309">Voer desgevraagd het wachtwoord voor de SSH-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="4ba49-309">When prompted, enter the password for the SSH user.</span></span>
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > <span data-ttu-id="4ba49-310">Dit kan enige tijd duren om de bestanden te uploaden.</span><span class="sxs-lookup"><span data-stu-id="4ba49-310">It may take several minutes to upload the files.</span></span>

    <span data-ttu-id="4ba49-311">Voor meer informatie over het gebruik van de `scp` en `ssh` opdrachten met HDInsight, Zie [SSH gebruiken met HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="4ba49-311">For more information on using the `scp` and `ssh` commands with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

3. <span data-ttu-id="4ba49-312">Zodra het bestand zijn geüpload, moet u een verbinding maken met de Storm-cluster via SSH.</span><span class="sxs-lookup"><span data-stu-id="4ba49-312">Once the file has been uploaded, connect to the Storm cluster using SSH.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="4ba49-313">Vervang `sshuser` met de SSH-gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="4ba49-313">Replace `sshuser` with the SSH user name.</span></span> <span data-ttu-id="4ba49-314">Vervang `clustername` met de naam van het Storm-cluster.</span><span class="sxs-lookup"><span data-stu-id="4ba49-314">Replace `clustername` with the Storm cluster name.</span></span>

4. <span data-ttu-id="4ba49-315">Gebruik de volgende opdracht bij de SSH-sessie voor het starten van de topologie:</span><span class="sxs-lookup"><span data-stu-id="4ba49-315">To start the topology, use the following command from the SSH session:</span></span>
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * <span data-ttu-id="4ba49-316">`--remote`verzendt de topologie van de Nimbus-service, die u het naar de supervisor knooppunten in het cluster distribueert.</span><span class="sxs-lookup"><span data-stu-id="4ba49-316">`--remote` submits the topology to the Nimbus service, which distributes it to the supervisor nodes in the cluster.</span></span>
    * <span data-ttu-id="4ba49-317">`--filter`maakt gebruik van de `dev.properties` bestand voor het vullen van de parameters in de definitie van de topologie.</span><span class="sxs-lookup"><span data-stu-id="4ba49-317">`--filter` uses the `dev.properties` file to populate parameters in the topology definition.</span></span>
    * <span data-ttu-id="4ba49-318">`-R /with-hbase.yaml`maakt gebruik van de `with-hbase.yaml` topologie die zijn opgenomen in het pakket.</span><span class="sxs-lookup"><span data-stu-id="4ba49-318">`-R /with-hbase.yaml` uses the `with-hbase.yaml` topology included in the package.</span></span>

5. <span data-ttu-id="4ba49-319">Nadat de topologie is gestart, open een browser naar de website die u in Azure hebt gepubliceerd, gebruikt u vervolgens de `node app.js` opdracht om gegevens te verzenden naar Event Hub.</span><span class="sxs-lookup"><span data-stu-id="4ba49-319">After the topology has started, open a browser to the website you published on Azure, then use the `node app.js` command to send data to Event Hub.</span></span> <span data-ttu-id="4ba49-320">Hier ziet u de webdashboard bijwerken om de informatie weer te geven.</span><span class="sxs-lookup"><span data-stu-id="4ba49-320">You should see the web dashboard update to display the information.</span></span>
   
    ![dashboard](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a><span data-ttu-id="4ba49-322">HBase-gegevens weergeven</span><span class="sxs-lookup"><span data-stu-id="4ba49-322">View HBase data</span></span>

<span data-ttu-id="4ba49-323">Gebruik de volgende stappen voor het verbinding maken met HBase en te controleren dat de gegevens is geschreven naar de tabel:</span><span class="sxs-lookup"><span data-stu-id="4ba49-323">Use the following steps to connect to HBase and verify that the data has been written to the table:</span></span>

1. <span data-ttu-id="4ba49-324">SSH gebruiken voor verbinding met de HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="4ba49-324">Use SSH to connect to the HBase cluster.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="4ba49-325">Vervang `sshuser` met de SSH-gebruikersnaam.</span><span class="sxs-lookup"><span data-stu-id="4ba49-325">Replace `sshuser` with the SSH user name.</span></span> <span data-ttu-id="4ba49-326">Vervang `clustername` met de naam van het HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="4ba49-326">Replace `clustername` with the HBase cluster name.</span></span>

2. <span data-ttu-id="4ba49-327">Start de HBase-shell op de SSH-sessie.</span><span class="sxs-lookup"><span data-stu-id="4ba49-327">From the SSH session, start the HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="4ba49-328">Nadat de shell is geladen, ziet u een `hbase(main):001:0>` prompt.</span><span class="sxs-lookup"><span data-stu-id="4ba49-328">Once the shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="4ba49-329">Weergave rijen uit de tabel:</span><span class="sxs-lookup"><span data-stu-id="4ba49-329">View rows from the table:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="4ba49-330">Met deze opdracht retourneert informatie vergelijkbaar met de volgende tekst, die aangeeft dat er gegevens in de tabel.</span><span class="sxs-lookup"><span data-stu-id="4ba49-330">This command returns information similar to the following text, indicating that there is data in the table.</span></span>
   
        hbase(main):002:0> scan 'SensorData'
        ROW                             COLUMN+CELL
        \x00\x00\x00\x00               column=cf:temperature, timestamp=1467290788277, value=\x00\x00\x00\x04
        \x00\x00\x00\x00               column=cf:timestamp, timestamp=1467290788277, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x01               column=cf:temperature, timestamp=1467290788348, value=\x00\x00\x00M
        \x00\x00\x00\x01               column=cf:timestamp, timestamp=1467290788348, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x02               column=cf:temperature, timestamp=1467290788268, value=\x00\x00\x00R
        \x00\x00\x00\x02               column=cf:timestamp, timestamp=1467290788268, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x03               column=cf:temperature, timestamp=1467290788269, value=\x00\x00\x00#
        \x00\x00\x00\x03               column=cf:timestamp, timestamp=1467290788269, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x04               column=cf:temperature, timestamp=1467290788356, value=\x00\x00\x00>
        \x00\x00\x00\x04               column=cf:timestamp, timestamp=1467290788356, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x05               column=cf:temperature, timestamp=1467290788326, value=\x00\x00\x00\x0D
        \x00\x00\x00\x05               column=cf:timestamp, timestamp=1467290788326, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x06               column=cf:temperature, timestamp=1467290788253, value=\x00\x00\x009
        \x00\x00\x00\x06               column=cf:timestamp, timestamp=1467290788253, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x07               column=cf:temperature, timestamp=1467290788229, value=\x00\x00\x00\x12
        \x00\x00\x00\x07               column=cf:timestamp, timestamp=1467290788229, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x08               column=cf:temperature, timestamp=1467290788336, value=\x00\x00\x00\x16
        \x00\x00\x00\x08               column=cf:timestamp, timestamp=1467290788336, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x09               column=cf:temperature, timestamp=1467290788246, value=\x00\x00\x001
        \x00\x00\x00\x09               column=cf:timestamp, timestamp=1467290788246, value=2015-02-10T14:43.05.00320Z
        10 row(s) in 0.1800 seconds
   
   > [!NOTE]
   > <span data-ttu-id="4ba49-331">Deze scanbewerking retourneert maximaal 10 rijen uit de tabel.</span><span class="sxs-lookup"><span data-stu-id="4ba49-331">This scan operation returns a maximum of 10 rows from the table.</span></span>

## <a name="delete-your-clusters"></a><span data-ttu-id="4ba49-332">Uw clusters verwijderen</span><span class="sxs-lookup"><span data-stu-id="4ba49-332">Delete your clusters</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="4ba49-333">Als u wilt de clusters-, opslag- en web-app in één keer verwijderen, de resourcegroep waarin ze te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="4ba49-333">To delete the clusters, storage, and web app at one time, delete the resource group that contains them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4ba49-334">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4ba49-334">Next steps</span></span>

<span data-ttu-id="4ba49-335">Zie voor meer voorbeelden van Storm-topologieën met HDInsight [voorbeeldtopologieën van Storm op HDInsight](hdinsight-storm-example-topology.md)</span><span class="sxs-lookup"><span data-stu-id="4ba49-335">For more examples of Storm topologies with HDInsight, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md)</span></span>

<span data-ttu-id="4ba49-336">Zie voor meer informatie over de Apache Storm, de [Apache Storm](https://storm.incubator.apache.org/) site.</span><span class="sxs-lookup"><span data-stu-id="4ba49-336">For more information about Apache Storm, see the [Apache Storm](https://storm.incubator.apache.org/) site.</span></span>

<span data-ttu-id="4ba49-337">Zie voor meer informatie over HBase in HDInsight, het [HBase met HDInsight Overview](hdinsight-hbase-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4ba49-337">For more information about HBase on HDInsight, see the [HBase with HDInsight Overview](hdinsight-hbase-overview.md).</span></span>

<span data-ttu-id="4ba49-338">Zie voor meer informatie over Socket.io de [socket.io](http://socket.io/) site.</span><span class="sxs-lookup"><span data-stu-id="4ba49-338">For more information about Socket.io, see the [socket.io](http://socket.io/) site.</span></span>

<span data-ttu-id="4ba49-339">Zie voor meer informatie over D3.js [D3.js - documenten met aangestuurd](http://d3js.org/).</span><span class="sxs-lookup"><span data-stu-id="4ba49-339">For more information about D3.js, see [D3.js - Data Driven Documents](http://d3js.org/).</span></span>

<span data-ttu-id="4ba49-340">Zie voor meer informatie over het maken van topologieën in Java [ontwikkelen van Java-topologieën voor Apache Storm op HDInsight](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="4ba49-340">For information about creating topologies in Java, see [Develop Java topologies for Apache Storm on HDInsight](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="4ba49-341">Zie voor meer informatie over het maken van topologieën in .NET [C#-topologieën ontwikkelen voor Apache Storm op HDInsight met behulp van Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="4ba49-341">For information about creating topologies in .NET, see [Develop C# topologies for Apache Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

[azure-portal]: https://portal.azure.com
