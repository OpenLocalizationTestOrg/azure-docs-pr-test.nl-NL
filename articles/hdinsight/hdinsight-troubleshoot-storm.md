---
title: aaaTroubleshoot Storm met behulp van Azure HDInsight | Microsoft Docs
description: Vind antwoorden op vragen over het gebruik van Apache Storm met Azure HDInsight toocommon.
keywords: HDInsight, Storm, veelgestelde vragen over Azure, handleiding worden veelvoorkomende problemen oplossen
services: Azure HDInsight
documentationcenter: na
author: raviperi
manager: 
editor: 
ms.assetid: 74E51183-3EF4-4C67-AA60-6E12FAC999B5
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: raviperi
ms.openlocfilehash: 51bcb3dc28eff5ee7bb33252fb2ec71a88ed8e09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storm-by-using-azure-hdinsight"></a><span data-ttu-id="db36a-104">Storm oplossen met behulp van Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="db36a-104">Troubleshoot Storm by using Azure HDInsight</span></span>

<span data-ttu-id="db36a-105">Meer informatie over de meestvoorkomende problemen Hallo en hun oplossingen voor het werken met Apache Storm-nettoladingen in Apache Ambari.</span><span class="sxs-lookup"><span data-stu-id="db36a-105">Learn about hello top issues and their resolutions for working with Apache Storm payloads in Apache Ambari.</span></span>

## <a name="how-do-i-access-hello-storm-ui-on-a-cluster"></a><span data-ttu-id="db36a-106">Hoe krijg ik toegang tot Hallo Storm-gebruikersinterface op een cluster</span><span class="sxs-lookup"><span data-stu-id="db36a-106">How do I access hello Storm UI on a cluster</span></span>
<span data-ttu-id="db36a-107">U hebt twee opties voor toegang tot Hallo Storm-gebruikersinterface vanuit een browser:</span><span class="sxs-lookup"><span data-stu-id="db36a-107">You have two options for accessing hello Storm UI from a browser:</span></span>

### <a name="ambari-ui"></a><span data-ttu-id="db36a-108">Ambari-gebruikersinterface</span><span class="sxs-lookup"><span data-stu-id="db36a-108">Ambari UI</span></span>
1. <span data-ttu-id="db36a-109">Ga toohello Ambari-dashboard.</span><span class="sxs-lookup"><span data-stu-id="db36a-109">Go toohello Ambari dashboard.</span></span>
2. <span data-ttu-id="db36a-110">Selecteer in de lijst met services Hallo **Storm**.</span><span class="sxs-lookup"><span data-stu-id="db36a-110">In hello list of services, select **Storm**.</span></span>
3. <span data-ttu-id="db36a-111">In Hallo **snelkoppelingen** selecteert u **Storm-gebruikersinterface**.</span><span class="sxs-lookup"><span data-stu-id="db36a-111">In hello **Quick Links** menu, select **Storm UI**.</span></span>

### <a name="direct-link"></a><span data-ttu-id="db36a-112">Directe koppeling</span><span class="sxs-lookup"><span data-stu-id="db36a-112">Direct link</span></span>
<span data-ttu-id="db36a-113">U kunt openen Hallo Storm-gebruikersinterface op Hallo URL te volgen:</span><span class="sxs-lookup"><span data-stu-id="db36a-113">You can access hello Storm UI at hello following URL:</span></span>

<span data-ttu-id="db36a-114">https://\<cluster DNS-naam\>/stormui</span><span class="sxs-lookup"><span data-stu-id="db36a-114">https://\<cluster DNS name\>/stormui</span></span>

<span data-ttu-id="db36a-115">Voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="db36a-115">Example:</span></span>

 <span data-ttu-id="db36a-116">https://stormcluster.azurehdinsight.NET/stormui</span><span class="sxs-lookup"><span data-stu-id="db36a-116">https://stormcluster.azurehdinsight.net/stormui</span></span>

## <a name="how-do-i-transfer-storm-event-hub-spout-checkpoint-information-from-one-topology-tooanother"></a><span data-ttu-id="db36a-117">Hoe moet ik Storm event hub spout controlepunt informatie overbrengen van een topologie tooanother</span><span class="sxs-lookup"><span data-stu-id="db36a-117">How do I transfer Storm event hub spout checkpoint information from one topology tooanother</span></span>

<span data-ttu-id="db36a-118">Wanneer u topologieën die lezen uit Azure Event Hubs met Hallo HDInsight Storm event hub spout JAR-bestand ontwikkelt, moet u een topologie met dezelfde naam op een nieuw cluster Hallo implementeren.</span><span class="sxs-lookup"><span data-stu-id="db36a-118">When you develop topologies that read from Azure Event Hubs by using hello HDInsight Storm event hub spout .jar file, you must deploy a topology that has hello same name on a new cluster.</span></span> <span data-ttu-id="db36a-119">U moet echter Hallo controlepuntgegevens die doorgevoerd tooApache ZooKeeper op het oude cluster Hallo was behouden.</span><span class="sxs-lookup"><span data-stu-id="db36a-119">However, you must retain hello checkpoint data that was committed tooApache ZooKeeper on hello old cluster.</span></span>

### <a name="where-checkpoint-data-is-stored"></a><span data-ttu-id="db36a-120">Waar controlepuntgegevens worden opgeslagen</span><span class="sxs-lookup"><span data-stu-id="db36a-120">Where checkpoint data is stored</span></span>
<span data-ttu-id="db36a-121">Controlepuntgegevens voor offsets worden opgeslagen door Hallo event hub spout in ZooKeeper in twee hoofdmappen:</span><span class="sxs-lookup"><span data-stu-id="db36a-121">Checkpoint data for offsets is stored by hello event hub spout in ZooKeeper in two root paths:</span></span>
- <span data-ttu-id="db36a-122">Niet-transactionele spout controlepunten worden opgeslagen in /eventhubspout.</span><span class="sxs-lookup"><span data-stu-id="db36a-122">Nontransactional spout checkpoints are stored in /eventhubspout.</span></span>
- <span data-ttu-id="db36a-123">Transactionele spout controlepuntgegevens worden opgeslagen in / transactionele.</span><span class="sxs-lookup"><span data-stu-id="db36a-123">Transactional spout checkpoint data is stored in /transactional.</span></span>

### <a name="how-toorestore"></a><span data-ttu-id="db36a-124">Hoe toorestore</span><span class="sxs-lookup"><span data-stu-id="db36a-124">How toorestore</span></span>
<span data-ttu-id="db36a-125">Zie tooget Hallo scripts en bibliotheken tooexport gegevens buiten ZooKeeper te gebruiken en vervolgens importeren Hallo gegevens back tooZooKeeper met een nieuwe naam [HDInsight Storm voorbeelden](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span><span class="sxs-lookup"><span data-stu-id="db36a-125">tooget hello scripts and libraries that you use tooexport data out of ZooKeeper and then import hello data back tooZooKeeper with a new name, see [HDInsight Storm examples](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/tools/zkdatatool-1.0).</span></span>

<span data-ttu-id="db36a-126">Hallo lib map bevat de JAR-bestanden die Hallo-implementatie voor Hallo exporteren/importeren bewerking bevatten.</span><span class="sxs-lookup"><span data-stu-id="db36a-126">hello lib folder has .jar files that contain hello implementation for hello export/import operation.</span></span> <span data-ttu-id="db36a-127">Hallo bash map heeft een voorbeeldscript dat laat zien hoe gegevens van tooexport ZooKeeper server op het oude cluster Hallo Hallo en importeer vervolgens back toohello ZooKeeper server op Hallo nieuwe cluster.</span><span class="sxs-lookup"><span data-stu-id="db36a-127">hello bash folder has an example script that demonstrates how tooexport data from hello ZooKeeper server on hello old cluster, and then import it back toohello ZooKeeper server on hello new cluster.</span></span>

<span data-ttu-id="db36a-128">Voer Hallo [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) script uit Hallo ZooKeeper-knooppunten tooexport en importeer gegevens.</span><span class="sxs-lookup"><span data-stu-id="db36a-128">Run hello [stormmeta.sh](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/tools/zkdatatool-1.0/bash/stormmeta.sh) script from hello ZooKeeper nodes tooexport and then import data.</span></span> <span data-ttu-id="db36a-129">Hallo script toohello juist Hortonworks Data Platform HDP ()-versie bijwerken.</span><span class="sxs-lookup"><span data-stu-id="db36a-129">Update hello script toohello correct Hortonworks Data Platform (HDP) version.</span></span> <span data-ttu-id="db36a-130">(We werken over het maken van deze scripts algemene in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="db36a-130">(We are working on making these scripts generic in HDInsight.</span></span> <span data-ttu-id="db36a-131">Algemene scripts kunnen uitvoeren vanaf elk knooppunt op Hallo cluster zonder wijzigingen door de gebruiker Hallo.)</span><span class="sxs-lookup"><span data-stu-id="db36a-131">Generic scripts can run from any node on hello cluster without modifications by hello user.)</span></span>

<span data-ttu-id="db36a-132">de opdracht exporteren Hallo schrijft Hallo tooan Apache Hadoop Distributed File System (HDFS) metagegevenspad (in een store Azure Blob Storage of Azure Data Lake Store) op een locatie die u instelt.</span><span class="sxs-lookup"><span data-stu-id="db36a-132">hello export command writes hello metadata tooan Apache Hadoop Distributed File System (HDFS) path (in an Azure Blob Storage or Azure Data Lake Store store) at a location that you set.</span></span>

### <a name="examples"></a><span data-ttu-id="db36a-133">Voorbeelden</span><span class="sxs-lookup"><span data-stu-id="db36a-133">Examples</span></span>

#### <a name="export-offset-metadata"></a><span data-ttu-id="db36a-134">Offset metagegevens exporteren</span><span class="sxs-lookup"><span data-stu-id="db36a-134">Export offset metadata</span></span>
1. <span data-ttu-id="db36a-135">SSH toogo toohello ZooKeeper-cluster op Hallo-cluster vanaf het controlepunt van welke Hallo offset toobe geëxporteerd moet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="db36a-135">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="db36a-136">Voer Hallo volgende opdracht (na het bijwerken van Hallo HDP versietekenreeks) tooexport ZooKeeper offset gegevens toohello /stormmetadta/zkdata HDFS pad:</span><span class="sxs-lookup"><span data-stu-id="db36a-136">Run hello following command (after you update hello HDP version string) tooexport ZooKeeper offset data toohello /stormmetadta/zkdata HDFS path:</span></span>

    ```apache   
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter export /eventhubspout /stormmetadata/zkdata
    ```

#### <a name="import-offset-metadata"></a><span data-ttu-id="db36a-137">Offset metagegevens importeren</span><span class="sxs-lookup"><span data-stu-id="db36a-137">Import offset metadata</span></span>
1. <span data-ttu-id="db36a-138">SSH toogo toohello ZooKeeper-cluster op Hallo-cluster vanaf het controlepunt van welke Hallo offset toobe geëxporteerd moet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="db36a-138">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="db36a-139">Voer hello volgende opdracht (na het bijwerken van Hallo HDP versietekenreeks) tooimport ZooKeeper gegevens van Hallo HDFS pad/stormmetadata/zkdata toohello ZooKeeper server op Hallo doelcluster offset:</span><span class="sxs-lookup"><span data-stu-id="db36a-139">Run hello following command (after you update hello HDP version string) tooimport ZooKeeper offset data from hello HDFS path /stormmetadata/zkdata toohello ZooKeeper server on hello target cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter import /eventhubspout /home/sshadmin/zkdata
    ```
   
#### <a name="delete-offset-metadata-so-that-topologies-can-start-processing-data-from-hello-beginning-or-from-a-timestamp-that-hello-user-chooses"></a><span data-ttu-id="db36a-140">Offset metagegevens verwijderen zodat topologieën kunnen beginnen met het verwerken van gegevens vanaf het begin van de Hallo of van een tijdstempel die gebruiker Hallo kiest</span><span class="sxs-lookup"><span data-stu-id="db36a-140">Delete offset metadata so that topologies can start processing data from hello beginning, or from a timestamp that hello user chooses</span></span>
1. <span data-ttu-id="db36a-141">SSH toogo toohello ZooKeeper-cluster op Hallo-cluster vanaf het controlepunt van welke Hallo offset toobe geëxporteerd moet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="db36a-141">Use SSH toogo toohello ZooKeeper cluster on hello cluster from which hello checkpoint offset needs toobe exported.</span></span>
2. <span data-ttu-id="db36a-142">Voer hello volgende opdracht (na het bijwerken van Hallo HDP versietekenreeks) toodelete alle ZooKeeper gegevens in de huidige cluster Hallo offset:</span><span class="sxs-lookup"><span data-stu-id="db36a-142">Run hello following command (after you update hello HDP version string) toodelete all ZooKeeper offset data in hello current cluster:</span></span>

    ```apache
    java -cp ./*:/etc/hadoop/conf/*:/usr/hdp/2.5.1.0-56/hadoop/*:/usr/hdp/2.5.1.0-56/hadoop/lib/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/*:/usr/hdp/2.5.1.0-56/hadoop-hdfs/lib/*:/etc/failover-controller/conf/*:/etc/hadoop/* com.microsoft.storm.zkdatatool.ZkdataImporter delete /eventhubspout
    ```

## <a name="how-do-i-locate-storm-binaries-on-a-cluster"></a><span data-ttu-id="db36a-143">Hoe ik Storm binaire bestanden vinden op een cluster</span><span class="sxs-lookup"><span data-stu-id="db36a-143">How do I locate Storm binaries on a cluster</span></span>
<span data-ttu-id="db36a-144">Storm-binaire bestanden voor de huidige HDP stack Hallo zijn in /usr/hdp/current/storm-client.</span><span class="sxs-lookup"><span data-stu-id="db36a-144">Storm binaries for hello current HDP stack are in /usr/hdp/current/storm-client.</span></span> <span data-ttu-id="db36a-145">Hallo-locatie wordt Hallo dezelfde hoofdknooppunten en voor worker-knooppunten.</span><span class="sxs-lookup"><span data-stu-id="db36a-145">hello location is hello same both for head nodes and for worker nodes.</span></span>
 
<span data-ttu-id="db36a-146">Er is mogelijk meerdere binaire bestanden voor specifieke HDP versies in /usr/hdp (bijvoorbeeld /usr/hdp/2.5.0.1233/storm).</span><span class="sxs-lookup"><span data-stu-id="db36a-146">There might be multiple binaries for specific HDP versions in /usr/hdp (for example, /usr/hdp/2.5.0.1233/storm).</span></span> <span data-ttu-id="db36a-147">Hallo /usr/hdp/current/storm-client map is symlinked toohello meest recente versie die wordt uitgevoerd op Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="db36a-147">hello /usr/hdp/current/storm-client folder is symlinked toohello latest version that is running on hello cluster.</span></span>

<span data-ttu-id="db36a-148">Zie voor meer informatie [Connect tooan HDInsight-cluster via SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) en [Storm](http://storm.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="db36a-148">For more information, see [Connect tooan HDInsight cluster by using SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) and [Storm](http://storm.apache.org/).</span></span>
 
## <a name="how-do-i-determine-hello-deployment-topology-of-a-storm-cluster"></a><span data-ttu-id="db36a-149">Hoe bepaal ik implementatietopologie Hallo van een Storm-cluster</span><span class="sxs-lookup"><span data-stu-id="db36a-149">How do I determine hello deployment topology of a Storm cluster</span></span>
<span data-ttu-id="db36a-150">Bepaal eerst alle onderdelen die zijn geïnstalleerd met HDInsight Storm.</span><span class="sxs-lookup"><span data-stu-id="db36a-150">First, identify all components that are installed with HDInsight Storm.</span></span> <span data-ttu-id="db36a-151">Een Storm-cluster bestaat uit vier categorieën van knooppunt:</span><span class="sxs-lookup"><span data-stu-id="db36a-151">A Storm cluster consists of four node categories:</span></span>

* <span data-ttu-id="db36a-152">Gateway-knooppunten</span><span class="sxs-lookup"><span data-stu-id="db36a-152">Gateway nodes</span></span>
* <span data-ttu-id="db36a-153">HEAD-knooppunten</span><span class="sxs-lookup"><span data-stu-id="db36a-153">Head nodes</span></span>
* <span data-ttu-id="db36a-154">ZooKeeper-knooppunten</span><span class="sxs-lookup"><span data-stu-id="db36a-154">ZooKeeper nodes</span></span>
* <span data-ttu-id="db36a-155">Worker-knooppunten</span><span class="sxs-lookup"><span data-stu-id="db36a-155">Worker nodes</span></span>
 
### <a name="gateway-nodes"></a><span data-ttu-id="db36a-156">Gateway-knooppunten</span><span class="sxs-lookup"><span data-stu-id="db36a-156">Gateway nodes</span></span>
<span data-ttu-id="db36a-157">Een gateway-knooppunt is een gateway en de reverse proxyservice waarmee openbare toegang tooan active Ambari management-service.</span><span class="sxs-lookup"><span data-stu-id="db36a-157">A gateway node is a gateway and reverse proxy service that enables public access tooan active Ambari management service.</span></span> <span data-ttu-id="db36a-158">Ambari opvulteken keuze ook verwerkt.</span><span class="sxs-lookup"><span data-stu-id="db36a-158">It also handles Ambari leader election.</span></span>
 
### <a name="head-nodes"></a><span data-ttu-id="db36a-159">HEAD-knooppunten</span><span class="sxs-lookup"><span data-stu-id="db36a-159">Head nodes</span></span>
<span data-ttu-id="db36a-160">Storm-hoofdknooppunten Voer Hallo volgende services:</span><span class="sxs-lookup"><span data-stu-id="db36a-160">Storm head nodes run hello following services:</span></span>
* <span data-ttu-id="db36a-161">Nimbus</span><span class="sxs-lookup"><span data-stu-id="db36a-161">Nimbus</span></span>
* <span data-ttu-id="db36a-162">Ambari-server</span><span class="sxs-lookup"><span data-stu-id="db36a-162">Ambari server</span></span>
* <span data-ttu-id="db36a-163">Metrische gegevens Ambari-server</span><span class="sxs-lookup"><span data-stu-id="db36a-163">Ambari Metrics server</span></span>
* <span data-ttu-id="db36a-164">Ambari metrische gegevens verzamelen</span><span class="sxs-lookup"><span data-stu-id="db36a-164">Ambari Metrics Collector</span></span>
 
### <a name="zookeeper-nodes"></a><span data-ttu-id="db36a-165">ZooKeeper-knooppunten</span><span class="sxs-lookup"><span data-stu-id="db36a-165">ZooKeeper nodes</span></span>
<span data-ttu-id="db36a-166">HDInsight wordt geleverd met een quorum van de ZooKeeper drie knooppunten.</span><span class="sxs-lookup"><span data-stu-id="db36a-166">HDInsight comes with a three-node ZooKeeper quorum.</span></span> <span data-ttu-id="db36a-167">Hallo quorum grootte is vast en kan niet worden geconfigureerd.</span><span class="sxs-lookup"><span data-stu-id="db36a-167">hello quorum size is fixed, and cannot be reconfigured.</span></span>
 
<span data-ttu-id="db36a-168">Storm-services in Hallo cluster zijn geconfigureerd tooautomatically gebruik Hallo ZooKeeper quorum.</span><span class="sxs-lookup"><span data-stu-id="db36a-168">Storm services in hello cluster are configured tooautomatically use hello ZooKeeper quorum.</span></span>
 
### <a name="worker-nodes"></a><span data-ttu-id="db36a-169">Worker-knooppunten</span><span class="sxs-lookup"><span data-stu-id="db36a-169">Worker nodes</span></span>
<span data-ttu-id="db36a-170">Storm worker-knooppunten uitvoeren Hallo volgende services:</span><span class="sxs-lookup"><span data-stu-id="db36a-170">Storm worker nodes run hello following services:</span></span>
* <span data-ttu-id="db36a-171">Supervisor</span><span class="sxs-lookup"><span data-stu-id="db36a-171">Supervisor</span></span>
* <span data-ttu-id="db36a-172">Werknemer Java virtuele machines (JVMs) voor het uitvoeren van topologieën</span><span class="sxs-lookup"><span data-stu-id="db36a-172">Worker Java virtual machines (JVMs), for running topologies</span></span>
* <span data-ttu-id="db36a-173">Ambari-agent</span><span class="sxs-lookup"><span data-stu-id="db36a-173">Ambari agent</span></span>
 
## <a name="how-do-i-locate-storm-event-hub-spout-binaries-for-development"></a><span data-ttu-id="db36a-174">Hoe ik Storm event hub spout binaire bestanden voor de ontwikkeling van vinden</span><span class="sxs-lookup"><span data-stu-id="db36a-174">How do I locate Storm event hub spout binaries for development</span></span>
 
<span data-ttu-id="db36a-175">Zie voor meer informatie over het gebruik van Storm event hub spout JAR-bestanden met uw topologie Hallo resources te volgen.</span><span class="sxs-lookup"><span data-stu-id="db36a-175">For more information about using Storm event hub spout .jar files with your topology, see hello following resources.</span></span>
 
### <a name="java-based-topology"></a><span data-ttu-id="db36a-176">Op basis van Java-topologie</span><span class="sxs-lookup"><span data-stu-id="db36a-176">Java-based topology</span></span>
[<span data-ttu-id="db36a-177">Procesgebeurtenissen van Azure Event Hubs met Storm op HDInsight (Java)</span><span class="sxs-lookup"><span data-stu-id="db36a-177">Process events from Azure Event Hubs with Storm on HDInsight (Java)</span></span>](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-java-event-hub-topology)
 
### <a name="c-based-topology-mono-on-hdinsight-34-linux-storm-clusters"></a><span data-ttu-id="db36a-178">C#-topologie (Mono op HDInsight 3.4 + Linux Storm-clusters) gebaseerd</span><span class="sxs-lookup"><span data-stu-id="db36a-178">C#-based topology (Mono on HDInsight 3.4+ Linux Storm clusters)</span></span>
<span data-ttu-id="db36a-179">[Process events from Azure Event Hubs with Storm on HDInsight (C#)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology) (Gebeurtenissen uit Azure Event Hubs verwerken met Storm op HDInsight (C#))</span><span class="sxs-lookup"><span data-stu-id="db36a-179">[Process events from Azure Event Hubs with Storm on HDInsight (C#)](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-storm-develop-csharp-event-hub-topology)</span></span>
 
### <a name="latest-storm-event-hub-spout-binaries-for-hdinsight-35-linux-storm-clusters"></a><span data-ttu-id="db36a-180">Meest recente Storm event hub spout binaire bestanden voor HDInsight 3.5 + Linux Storm-clusters</span><span class="sxs-lookup"><span data-stu-id="db36a-180">Latest Storm event hub spout binaries for HDInsight 3.5+ Linux Storm clusters</span></span>
<span data-ttu-id="db36a-181">toolearn hoe toouse Hallo nieuwste Storm event hub spout die met HDInsight 3.5 werkt + Linux Storm-clusters, raadpleegt u Hallo mvn-opslagplaats [Leesmij-bestand](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="db36a-181">toolearn how toouse hello latest Storm event hub spout that works with HDInsight 3.5+ Linux Storm clusters, see hello mvn-repo [readme file](https://github.com/hdinsight/mvn-repo/blob/master/README.md).</span></span>
 
### <a name="source-code-examples"></a><span data-ttu-id="db36a-182">Bron-codevoorbeelden</span><span class="sxs-lookup"><span data-stu-id="db36a-182">Source code examples</span></span>
<span data-ttu-id="db36a-183">Zie [voorbeelden](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) van hoe tooread en schrijven van Azure Event Hub met behulp van een Apache Storm-topologie (geschreven in Java) op een Azure HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="db36a-183">See [examples](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) of how tooread and write from Azure Event Hub using an Apache Storm topology (written in Java) on an Azure HDInsight cluster.</span></span>
 
## <a name="how-do-i-locate-storm-log4j-configuration-files-on-clusters"></a><span data-ttu-id="db36a-184">Hoe ik Storm Log4J configuratiebestanden op clusters vinden</span><span class="sxs-lookup"><span data-stu-id="db36a-184">How do I locate Storm Log4J configuration files on clusters</span></span>
 
<span data-ttu-id="db36a-185">configuratiebestanden tooidentify Apache-Log4J voor Storm-services.</span><span class="sxs-lookup"><span data-stu-id="db36a-185">tooidentify Apache Log4J configuration files for Storm services.</span></span>
 
### <a name="on-head-nodes"></a><span data-ttu-id="db36a-186">Over hoofdknooppunten</span><span class="sxs-lookup"><span data-stu-id="db36a-186">On head nodes</span></span>
<span data-ttu-id="db36a-187">Hallo Nimbus Log4J configuratie wordt gelezen uit /usr/hdp/\<HDP versie\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="db36a-187">hello Nimbus Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
### <a name="on-worker-nodes"></a><span data-ttu-id="db36a-188">Op de worker-knooppunten</span><span class="sxs-lookup"><span data-stu-id="db36a-188">On worker nodes</span></span>
<span data-ttu-id="db36a-189">Hallo supervisor Log4J configuratie wordt gelezen uit /usr/hdp/\<HDP versie\>/storm/log4j2/cluster.xml.</span><span class="sxs-lookup"><span data-stu-id="db36a-189">hello supervisor Log4J configuration is read from /usr/hdp/\<HDP version\>/storm/log4j2/cluster.xml.</span></span>
 
<span data-ttu-id="db36a-190">Hallo worker Log4J-configuratiebestand is gelezen uit /usr/hdp/\<HDP versie\>/storm/log4j2/worker.xml.</span><span class="sxs-lookup"><span data-stu-id="db36a-190">hello worker Log4J configuration file is read from /usr/hdp/\<HDP version\>/storm/log4j2/worker.xml.</span></span>
 
<span data-ttu-id="db36a-191">Voorbeelden: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span><span class="sxs-lookup"><span data-stu-id="db36a-191">Examples: /usr/hdp/2.6.0.2-76/storm/log4j2/cluster.xml /usr/hdp/2.6.0.2-76/storm/log4j2/worker.xml</span></span>

