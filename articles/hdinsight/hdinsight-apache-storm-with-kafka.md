---
title: aaaUse Apache Kafka met Storm op HDInsight - Azure | Microsoft Docs
description: "Apache Kafka wordt geïnstalleerd met Apache Storm op HDInsight. Meer informatie over hoe toowrite tooKafka en lees, met behulp van Hallo KafkaBolt en KafkaSpout-onderdelen met Storm. U leert ook hoe toouse Hallo lichtstroom framework toodefine en het verzenden van Storm-topologieën."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e4941329-1580-4cd8-b82e-a2258802c1a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: larryfr
ms.openlocfilehash: 95701f51dfdf6f1a859dcde96d7053df4f21701f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a><span data-ttu-id="b33b9-105">Apache Kafka (preview) met Storm op HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="b33b9-105">Use Apache Kafka (preview) with Storm on HDInsight</span></span>

<span data-ttu-id="b33b9-106">Meer informatie over hoe toouse Apache Storm tooread van en schrijven tooApache Kafka.</span><span class="sxs-lookup"><span data-stu-id="b33b9-106">Learn how toouse Apache Storm tooread from and write tooApache Kafka.</span></span> <span data-ttu-id="b33b9-107">Dit voorbeeld wordt ook hoe toosave gegevens van een Storm-topologie toohello HDFS-compatibele bestandssysteem die door HDInsight worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b33b9-107">This example also demonstrates how toosave data from a Storm topology toohello HDFS-compatible file system used by HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="b33b9-108">Hallo stappen in dit document wordt een Azure-resourcegroep met zowel een Storm op HDInsight en een Kafka op HDInsight-cluster maken</span><span class="sxs-lookup"><span data-stu-id="b33b9-108">hello steps in this document create an Azure resource group that contains both a Storm on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="b33b9-109">Deze clusters zijn beide zich binnen een virtueel netwerk van Azure, waardoor Hallo Storm-cluster toodirectly communiceren met de Hallo Kafka-cluster.</span><span class="sxs-lookup"><span data-stu-id="b33b9-109">These clusters are both located within an Azure Virtual Network, which allows hello Storm cluster toodirectly communicate with hello Kafka cluster.</span></span>
> 
> <span data-ttu-id="b33b9-110">Wanneer u klaar bent met de stappen in dit document Hallo onthouden toodelete Hallo clusters tooavoid overtollige kosten.</span><span class="sxs-lookup"><span data-stu-id="b33b9-110">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="get-hello-code"></a><span data-ttu-id="b33b9-111">Hallo code ophalen</span><span class="sxs-lookup"><span data-stu-id="b33b9-111">Get hello code</span></span>

<span data-ttu-id="b33b9-112">Hallo-code voor Hallo-voorbeeld gebruikt in dit document is beschikbaar op [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span><span class="sxs-lookup"><span data-stu-id="b33b9-112">hello code for hello example used in this document is available at [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span></span>

<span data-ttu-id="b33b9-113">toocompile dit project, moet u na de configuratie voor uw ontwikkelomgeving Hallo:</span><span class="sxs-lookup"><span data-stu-id="b33b9-113">toocompile this project, you need hello following configuration for your development environment:</span></span>

* <span data-ttu-id="b33b9-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) of hoger.</span><span class="sxs-lookup"><span data-stu-id="b33b9-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="b33b9-115">HDInsight 3.5 of hoger vereisen Java 8.</span><span class="sxs-lookup"><span data-stu-id="b33b9-115">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="b33b9-116">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="b33b9-116">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

* <span data-ttu-id="b33b9-117">Een SSH-client (u moet Hallo `ssh` en `scp` opdrachten) - informatie, Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b33b9-117">An SSH client (you need hello `ssh` and `scp` commands) - For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="b33b9-118">Een teksteditor of IDE.</span><span class="sxs-lookup"><span data-stu-id="b33b9-118">A text editor or IDE.</span></span>

<span data-ttu-id="b33b9-119">Hallo kunnen volgende omgevingsvariabelen worden ingesteld wanneer u Java en Hallo JDK op uw ontwikkelwerkstation installeert.</span><span class="sxs-lookup"><span data-stu-id="b33b9-119">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="b33b9-120">Echter, moet u controleren of ze bestaan en dat ze de juiste waarden voor uw systeem Hallo bevatten.</span><span class="sxs-lookup"><span data-stu-id="b33b9-120">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="b33b9-121">`JAVA_HOME`-moet verwijzen toohello directory waarin hello JDK is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b33b9-121">`JAVA_HOME` - should point toohello directory where hello JDK is installed.</span></span>
* <span data-ttu-id="b33b9-122">`PATH`-moet bevatten Hallo paden te volgen:</span><span class="sxs-lookup"><span data-stu-id="b33b9-122">`PATH` - should contain hello following paths:</span></span>
  
    * <span data-ttu-id="b33b9-123">`JAVA_HOME`(of gelijkwaardige Hallo-pad).</span><span class="sxs-lookup"><span data-stu-id="b33b9-123">`JAVA_HOME` (or hello equivalent path).</span></span>
    * <span data-ttu-id="b33b9-124">`JAVA_HOME\bin`(of gelijkwaardige Hallo-pad).</span><span class="sxs-lookup"><span data-stu-id="b33b9-124">`JAVA_HOME\bin` (or hello equivalent path).</span></span>
    * <span data-ttu-id="b33b9-125">Hallo-map is waarin Maven is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b33b9-125">hello directory where Maven is installed.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="b33b9-126">Hallo-clusters maken</span><span class="sxs-lookup"><span data-stu-id="b33b9-126">Create hello clusters</span></span>

<span data-ttu-id="b33b9-127">Apache Kafka op HDInsight biedt geen toegang tot toohello Kafka beleggingsmakelaars via openbaar internet Hallo.</span><span class="sxs-lookup"><span data-stu-id="b33b9-127">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="b33b9-128">Alles wat vertelt tooKafka moet zich in hetzelfde virtuele Azure-netwerk als knooppunten in Hallo HALLO hallo Kafka-cluster.</span><span class="sxs-lookup"><span data-stu-id="b33b9-128">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="b33b9-129">In dit voorbeeld bevinden Hallo Kafka zowel Storm-clusters zich in een Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="b33b9-129">For this example, both hello Kafka and Storm clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="b33b9-130">Hallo volgende diagram ziet u hoe de communicatie tussen clusters met Hallo loopt:</span><span class="sxs-lookup"><span data-stu-id="b33b9-130">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagram van Storm en Kafka clusters in een Azure-netwerk](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="b33b9-132">Andere services op Hallo cluster Hallo zoals SSH en Ambari toegankelijk is via internet.</span><span class="sxs-lookup"><span data-stu-id="b33b9-132">Other services on hello cluster such as SSH and Ambari can be accessed over hello internet.</span></span> <span data-ttu-id="b33b9-133">Zie voor meer informatie over Hallo openbare poorten beschikbaar met HDInsight [poorten en URI's die worden gebruikt door HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="b33b9-133">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="b33b9-134">U kunt een Azure-netwerk Kafka, maken en Storm-clusters handmatig, zijn maar er eenvoudiger toouse een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="b33b9-134">While you can create an Azure virtual network, Kafka, and Storm clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="b33b9-135">Gebruik Hallo volgende stappen uit voor een Azure-netwerk Kafka, toodeploy en Storm-clusters tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="b33b9-135">Use hello following steps toodeploy an Azure virtual network, Kafka, and Storm clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="b33b9-136">Hallo na de knop toosign in tooAzure en open Hallo-sjabloon in hello Azure-portal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b33b9-136">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    <span data-ttu-id="b33b9-137">Hello Azure Resource Manager-sjabloon bevindt zich op **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span><span class="sxs-lookup"><span data-stu-id="b33b9-137">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span></span> <span data-ttu-id="b33b9-138">Hiermee maakt u Hallo resources te volgen:</span><span class="sxs-lookup"><span data-stu-id="b33b9-138">It creates hello following resources:</span></span>
    
    * <span data-ttu-id="b33b9-139">Azure-resourcegroep</span><span class="sxs-lookup"><span data-stu-id="b33b9-139">Azure resource group</span></span>
    * <span data-ttu-id="b33b9-140">Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="b33b9-140">Azure Virtual Network</span></span>
    * <span data-ttu-id="b33b9-141">Azure-opslagaccount</span><span class="sxs-lookup"><span data-stu-id="b33b9-141">Azure Storage account</span></span>
    * <span data-ttu-id="b33b9-142">Kafka op HDInsight versie 3.6 (drie worker-knooppunten)</span><span class="sxs-lookup"><span data-stu-id="b33b9-142">Kafka on HDInsight version 3.6 (three worker nodes)</span></span>
    * <span data-ttu-id="b33b9-143">Storm op HDInsight versie 3.6 (drie worker-knooppunten)</span><span class="sxs-lookup"><span data-stu-id="b33b9-143">Storm on HDInsight version 3.6 (three worker nodes)</span></span>

  > [!WARNING]
  > <span data-ttu-id="b33b9-144">de beschikbaarheid van de tooguarantee van Kafka op HDInsight, uw cluster moet ten minste drie worker-knooppunten bevatten.</span><span class="sxs-lookup"><span data-stu-id="b33b9-144">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="b33b9-145">Deze sjabloon maakt een Kafka-cluster dat drie worker-knooppunten bevat.</span><span class="sxs-lookup"><span data-stu-id="b33b9-145">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="b33b9-146">Gebruik Hallo volgen richtlijnen toopopulate Hallo vermeldingen op Hallo **aangepaste implementatie** blade:</span><span class="sxs-lookup"><span data-stu-id="b33b9-146">Use hello following guidance toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Aangepaste HDInsight-implementatie](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * <span data-ttu-id="b33b9-148">**Resourcegroep**: Maak een groep of een bestaande set selecteren.</span><span class="sxs-lookup"><span data-stu-id="b33b9-148">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="b33b9-149">Deze groep bevat Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="b33b9-149">This group contains hello HDInsight cluster.</span></span>
   
    * <span data-ttu-id="b33b9-150">**Locatie**: Selecteer een locatie geografisch sluiten tooyou.</span><span class="sxs-lookup"><span data-stu-id="b33b9-150">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="b33b9-151">**Clusternaam baseren**: deze waarde wordt gebruikt als basisnaam voor clusters met Storm en Kafka Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="b33b9-151">**Base Cluster Name**: This value is used as hello base name for hello Storm and Kafka clusters.</span></span> <span data-ttu-id="b33b9-152">Bijvoorbeeld, voeren **hdi** maakt een Storm-cluster met de naam **storm hdi** en een Kafka-cluster met de naam **kafka hdi**.</span><span class="sxs-lookup"><span data-stu-id="b33b9-152">For example, entering **hdi** creates a Storm cluster named **storm-hdi** and a Kafka cluster named **kafka-hdi**.</span></span>
   
    * <span data-ttu-id="b33b9-153">**Aanmeldingsnaam van gebruiker cluster**: Hallo-beheerdersgebruikersnaam voor Hallo Storm en Kafka-clusters.</span><span class="sxs-lookup"><span data-stu-id="b33b9-153">**Cluster Login User Name**: hello admin user name for hello Storm and Kafka clusters.</span></span>
   
    * <span data-ttu-id="b33b9-154">**Aanmeldingswachtwoord cluster**: Hallo beheerder gebruikerswachtwoord voor Hallo Storm en Kafka-clusters.</span><span class="sxs-lookup"><span data-stu-id="b33b9-154">**Cluster Login Password**: hello admin user password for hello Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="b33b9-155">**SSH-gebruikersnaam**: Hallo SSH gebruiker toocreate voor Hallo Storm en Kafka-clusters.</span><span class="sxs-lookup"><span data-stu-id="b33b9-155">**SSH User Name**: hello SSH user toocreate for hello Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="b33b9-156">**SSH-wachtwoord**: Hallo-wachtwoord voor Hallo SSH-gebruiker voor Hallo Storm en Kafka-clusters.</span><span class="sxs-lookup"><span data-stu-id="b33b9-156">**SSH Password**: hello password for hello SSH user for hello Storm and Kafka clusters.</span></span>

3. <span data-ttu-id="b33b9-157">Lees Hallo **voorwaarden en bepalingen**, en selecteer vervolgens **ik ga akkoord toohello voorwaarden bovengenoemde**.</span><span class="sxs-lookup"><span data-stu-id="b33b9-157">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="b33b9-158">Controleer ten slotte **pincode toodashboard** en selecteer vervolgens **aankoop**.</span><span class="sxs-lookup"><span data-stu-id="b33b9-158">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="b33b9-159">Het duurt ongeveer 20 minuten toocreate Hallo-clusters.</span><span class="sxs-lookup"><span data-stu-id="b33b9-159">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="b33b9-160">Zodra het Hallo-resources zijn gemaakt, wordt Hallo blade voor de resourcegroep Hallo weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b33b9-160">Once hello resources have been created, hello blade for hello resource group is displayed.</span></span>

![Resourcegroepblade voor Hallo vnet en clusters](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="b33b9-162">Merk op dat de namen van HDInsight-clusters Hallo Hallo zijn **storm BASENAME** en **kafka BASENAME**, waarbij BASENAME Hallo-naam die u hebt opgegeven toohello sjabloon.</span><span class="sxs-lookup"><span data-stu-id="b33b9-162">Notice that hello names of hello HDInsight clusters are **storm-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="b33b9-163">U deze namen in latere stappen gebruiken om verbinding te maken van clusters toohello.</span><span class="sxs-lookup"><span data-stu-id="b33b9-163">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="understanding-hello-code"></a><span data-ttu-id="b33b9-164">Understanding Hallo code</span><span class="sxs-lookup"><span data-stu-id="b33b9-164">Understanding hello code</span></span>

<span data-ttu-id="b33b9-165">Dit project bevat twee topologieën:</span><span class="sxs-lookup"><span data-stu-id="b33b9-165">This project contains two topologies:</span></span>

* <span data-ttu-id="b33b9-166">**KafkaWriter**: gedefinieerd door Hallo **writer.yaml** , deze topologie schrijft willekeurig zinnen tooKafka hello KafkaBolt opgegeven met Apache Storm gebruiken.</span><span class="sxs-lookup"><span data-stu-id="b33b9-166">**KafkaWriter**: Defined by hello **writer.yaml** file, this topology writes random sentences tooKafka using hello KafkaBolt provided with Apache Storm.</span></span>

    <span data-ttu-id="b33b9-167">Deze topologie maakt gebruik van een aangepaste **SentenceSpout** onderdeel toogenerate willekeurig zinnen.</span><span class="sxs-lookup"><span data-stu-id="b33b9-167">This topology uses a custom **SentenceSpout** component toogenerate random sentences.</span></span>

* <span data-ttu-id="b33b9-168">**KafkaReader**: gedefinieerd door Hallo **reader.yaml** -bestand, deze topologie leest de gegevens uit Kafka hello KafkaSpout opgegeven met Apache Storm gebruiken en klik vervolgens logboeken Hallo toostdout gegevens.</span><span class="sxs-lookup"><span data-stu-id="b33b9-168">**KafkaReader**: Defined by hello **reader.yaml** file, this topology reads data from Kafka using hello KafkaSpout provided with Apache Storm, then logs hello data toostdout.</span></span>

    <span data-ttu-id="b33b9-169">Deze topologie gebruikt Hallo Storm HdfsBolt toowrite-gegevensopslag toodefault voor Hallo Storm-cluster.</span><span class="sxs-lookup"><span data-stu-id="b33b9-169">This topology uses hello Storm HdfsBolt toowrite data toodefault storage for hello Storm cluster.</span></span>
### <a name="flux"></a><span data-ttu-id="b33b9-170">Lichtstroom</span><span class="sxs-lookup"><span data-stu-id="b33b9-170">Flux</span></span>

<span data-ttu-id="b33b9-171">Hallo-topologieën worden gedefinieerd met [lichtstroom](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="b33b9-171">hello topologies are defined using [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span></span> <span data-ttu-id="b33b9-172">Lichtstroom werd geïntroduceerd in 0.10.x Storm en kunt u tooseparate hello topologieconfiguratie vanuit Hallo-code.</span><span class="sxs-lookup"><span data-stu-id="b33b9-172">Flux was introduced in Storm 0.10.x and allows you tooseparate hello topology configuration from hello code.</span></span> <span data-ttu-id="b33b9-173">Hallo-topologie is voor de topologieën die gebruikmaken van Hallo lichtstroom framework, gedefinieerd in een YAML-bestand.</span><span class="sxs-lookup"><span data-stu-id="b33b9-173">For Topologies that use hello Flux framework, hello topology is defined in a YAML file.</span></span> <span data-ttu-id="b33b9-174">Hallo YAML-bestand kan worden opgenomen als onderdeel van het Hallo-topologie.</span><span class="sxs-lookup"><span data-stu-id="b33b9-174">hello YAML file can be included as part of hello topology.</span></span> <span data-ttu-id="b33b9-175">Het kan ook een zelfstandig bestand gebruikt bij het verzenden van Hallo topologie zijn.</span><span class="sxs-lookup"><span data-stu-id="b33b9-175">It can also be a standalone file used when you submit hello topology.</span></span> <span data-ttu-id="b33b9-176">Lichtstroom ondersteunt ook het vervangen van de variabelen tijdens runtime, die wordt gebruikt in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="b33b9-176">Flux also supports variable substitution at run-time, which is used in this example.</span></span>

<span data-ttu-id="b33b9-177">Hallo zijn volgende parameters ingesteld tijdens de uitvoering voor deze topologieën:</span><span class="sxs-lookup"><span data-stu-id="b33b9-177">hello following parameters are set at run time for these topologies:</span></span>

* <span data-ttu-id="b33b9-178">`${kafka.topic}`: de naam van de Hallo Hallo Kafka-onderwerp dat Hallo topologieën lezen/schrijven naar.</span><span class="sxs-lookup"><span data-stu-id="b33b9-178">`${kafka.topic}`: hello name of hello Kafka topic that hello topologies read/write to.</span></span>

* <span data-ttu-id="b33b9-179">`${kafka.broker.hosts}`: Hallo die Hallo Kafka makelaars die worden uitgevoerd op host.</span><span class="sxs-lookup"><span data-stu-id="b33b9-179">`${kafka.broker.hosts}`: hello hosts that hello Kafka brokers run on.</span></span> <span data-ttu-id="b33b9-180">Hallo broker informatie wordt gebruikt door Hallo KafkaBolt bij het schrijven van tooKafka.</span><span class="sxs-lookup"><span data-stu-id="b33b9-180">hello broker information is used by hello KafkaBolt when writing tooKafka.</span></span>

* <span data-ttu-id="b33b9-181">`${kafka.zookeeper.hosts}`: Hallo-hosts die Zookeeper op wordt uitgevoerd in Hallo Kafka-cluster.</span><span class="sxs-lookup"><span data-stu-id="b33b9-181">`${kafka.zookeeper.hosts}`: hello hosts that Zookeeper runs on in hello Kafka cluster.</span></span>

<span data-ttu-id="b33b9-182">Zie voor meer informatie over topologieën lichtstroom [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="b33b9-182">For more information on Flux topologies, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="download-and-compile-hello-project"></a><span data-ttu-id="b33b9-183">Download en Hallo project compileren</span><span class="sxs-lookup"><span data-stu-id="b33b9-183">Download and compile hello project</span></span>

1. <span data-ttu-id="b33b9-184">Op uw ontwikkelomgeving downloaden Hallo-project uit [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), opent u een opdrachtregel en de locatie van de toohello mappen dat u hebt gedownload Hallo project wijzigen.</span><span class="sxs-lookup"><span data-stu-id="b33b9-184">On your development environment, download hello project from [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), open a command-line, and change directories toohello location that you downloaded hello project.</span></span>

2. <span data-ttu-id="b33b9-185">Van Hallo **hdinsight, storm, java, kafka** map gebruik Hallo volgende opdracht toocompile Hallo-project en maak een pakket voor implementatie:</span><span class="sxs-lookup"><span data-stu-id="b33b9-185">From hello **hdinsight-storm-java-kafka** directory, use hello following command toocompile hello project and create a package for deployment:</span></span>

  ```bash
  mvn clean package
  ```

    <span data-ttu-id="b33b9-186">Hallo pakket proces maakt een bestand met de naam `KafkaTopology-1.0-SNAPSHOT.jar` in Hallo `target` directory.</span><span class="sxs-lookup"><span data-stu-id="b33b9-186">hello package process creates a file named `KafkaTopology-1.0-SNAPSHOT.jar` in hello `target` directory.</span></span>

3. <span data-ttu-id="b33b9-187">Gebruik Hallo volgende opdrachten toocopy Hallo pakket tooyour Storm op HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="b33b9-187">Use hello following commands toocopy hello package tooyour Storm on HDInsight cluster.</span></span> <span data-ttu-id="b33b9-188">Vervang **gebruikersnaam** met Hallo SSH-gebruikersnaam voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="b33b9-188">Replace **USERNAME** with hello SSH user name for hello cluster.</span></span> <span data-ttu-id="b33b9-189">Vervang **BASENAME** met Hallo basisnaam die u hebt gebruikt bij het Hallo-cluster maken.</span><span class="sxs-lookup"><span data-stu-id="b33b9-189">Replace **BASENAME** with hello base name you used when creating hello cluster.</span></span>

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    <span data-ttu-id="b33b9-190">Voer desgevraagd Hallo het wachtwoord waarmee u bij het maken van clusters Hallo.</span><span class="sxs-lookup"><span data-stu-id="b33b9-190">When prompted, enter hello password you used when creating hello clusters.</span></span>

## <a name="configure-hello-topology"></a><span data-ttu-id="b33b9-191">Hallo-topologie configureren</span><span class="sxs-lookup"><span data-stu-id="b33b9-191">Configure hello topology</span></span>

1. <span data-ttu-id="b33b9-192">Gebruik een van de methoden toodiscover na Hallo Hallo Kafka broker hosts:</span><span class="sxs-lookup"><span data-stu-id="b33b9-192">Use one of hello following methods toodiscover hello Kafka broker hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $brokerHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($brokerHosts -join ":9092,") + ":9092"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="b33b9-193">Hallo Bash-voorbeeld wordt ervan uitgegaan dat `$CLUSTERNAME` Hallo naam bevat van Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="b33b9-193">hello Bash example assumes that `$CLUSTERNAME` contains hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="b33b9-194">Ook wordt ervan uitgegaan dat [jq](https://stedolan.github.io/jq/) is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b33b9-194">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="b33b9-195">Wanneer u wordt gevraagd, voert u Hallo wachtwoord voor aanmeldingsaccount Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="b33b9-195">When prompted, enter hello password for hello cluster login account.</span></span>

    <span data-ttu-id="b33b9-196">Hallo-waarde die het resultaat is vergelijkbaar toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="b33b9-196">hello value returned is similar toohello following text:</span></span>

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > <span data-ttu-id="b33b9-197">Hoewel er mogelijk meer dan twee broker hosts voor uw cluster, hoeft u niet een volledige lijst met alle hosts tooclients tooprovide.</span><span class="sxs-lookup"><span data-stu-id="b33b9-197">While there may be more than two broker hosts for your cluster, you do not need tooprovide a full list of all hosts tooclients.</span></span> <span data-ttu-id="b33b9-198">Een of twee is voldoende.</span><span class="sxs-lookup"><span data-stu-id="b33b9-198">One or two is enough.</span></span>

2. <span data-ttu-id="b33b9-199">Gebruik een van de Hallo methoden toodiscover hello Kafka Zookeeper hosts te volgen:</span><span class="sxs-lookup"><span data-stu-id="b33b9-199">Use one of hello following methods toodiscover hello Kafka Zookeeper hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $zookeeperHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($zookeeperHosts -join ":2181,") + ":2181"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="b33b9-200">Hallo Bash-voorbeeld wordt ervan uitgegaan dat `$CLUSTERNAME` Hallo naam bevat van Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="b33b9-200">hello Bash example assumes that `$CLUSTERNAME` contains hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="b33b9-201">Ook wordt ervan uitgegaan dat [jq](https://stedolan.github.io/jq/) is geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="b33b9-201">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="b33b9-202">Wanneer u wordt gevraagd, voert u Hallo wachtwoord voor aanmeldingsaccount Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="b33b9-202">When prompted, enter hello password for hello cluster login account.</span></span>

    <span data-ttu-id="b33b9-203">Hallo-waarde die het resultaat is vergelijkbaar toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="b33b9-203">hello value returned is similar toohello following text:</span></span>

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > <span data-ttu-id="b33b9-204">Hoewel er meer dan twee Zookeeper-knooppunten, hoeft u niet een volledige lijst met alle hosts tooclients tooprovide.</span><span class="sxs-lookup"><span data-stu-id="b33b9-204">While there are more than two Zookeeper nodes, you do not need tooprovide a full list of all hosts tooclients.</span></span> <span data-ttu-id="b33b9-205">Een of twee is voldoende.</span><span class="sxs-lookup"><span data-stu-id="b33b9-205">One or two is enough.</span></span>

    <span data-ttu-id="b33b9-206">Deze waarde niet opslaan omdat het wordt later gebruikt.</span><span class="sxs-lookup"><span data-stu-id="b33b9-206">Save this value, as it is used later.</span></span>

3. <span data-ttu-id="b33b9-207">Hallo bewerken `dev.properties` bestand in de hoofdmap Hallo van Hallo-project.</span><span class="sxs-lookup"><span data-stu-id="b33b9-207">Edit hello `dev.properties` file in hello root of hello project.</span></span> <span data-ttu-id="b33b9-208">Hallo Broker en Zookeeper hosts informatie toohello overeenkomende regels in dit bestand toevoegen.</span><span class="sxs-lookup"><span data-stu-id="b33b9-208">Add hello Broker and Zookeeper hosts information toohello matching lines in this file.</span></span> <span data-ttu-id="b33b9-209">Hallo is volgende voorbeeld geconfigureerd met behulp van voorbeeldwaarden Hallo uit de vorige stappen Hallo:</span><span class="sxs-lookup"><span data-stu-id="b33b9-209">hello following example is configured using hello sample values from hello previous steps:</span></span>

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. <span data-ttu-id="b33b9-210">Hallo opslaan `dev.properties` bestands- en gebruik vervolgens Hallo na de opdracht tooupload het toohello Storm-cluster:</span><span class="sxs-lookup"><span data-stu-id="b33b9-210">Save hello `dev.properties` file and then use hello following command tooupload it toohello Storm cluster:</span></span>

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="b33b9-211">Vervang **gebruikersnaam** met Hallo SSH-gebruikersnaam voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="b33b9-211">Replace **USERNAME** with hello SSH user name for hello cluster.</span></span> <span data-ttu-id="b33b9-212">Vervang **BASENAME** met Hallo basisnaam die u hebt gebruikt bij het Hallo-cluster maken.</span><span class="sxs-lookup"><span data-stu-id="b33b9-212">Replace **BASENAME** with hello base name you used when creating hello cluster.</span></span>

## <a name="start-hello-writer"></a><span data-ttu-id="b33b9-213">Hallo writer starten</span><span class="sxs-lookup"><span data-stu-id="b33b9-213">Start hello writer</span></span>

1. <span data-ttu-id="b33b9-214">Gebruik hello tooconnect toohello Storm-cluster via SSH te volgen.</span><span class="sxs-lookup"><span data-stu-id="b33b9-214">Use hello following tooconnect toohello Storm cluster using SSH.</span></span> <span data-ttu-id="b33b9-215">Vervang **gebruikersnaam** met Hallo SSH-gebruikersnaam gebruikt bij het Hallo-cluster maken.</span><span class="sxs-lookup"><span data-stu-id="b33b9-215">Replace **USERNAME** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="b33b9-216">Vervang **BASENAME** met Hallo basisnaam gebruikt bij het Hallo-cluster maken.</span><span class="sxs-lookup"><span data-stu-id="b33b9-216">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    <span data-ttu-id="b33b9-217">Voer desgevraagd Hallo het wachtwoord waarmee u bij het maken van clusters Hallo.</span><span class="sxs-lookup"><span data-stu-id="b33b9-217">When prompted, enter hello password you used when creating hello clusters.</span></span>
   
    <span data-ttu-id="b33b9-218">Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.</span><span class="sxs-lookup"><span data-stu-id="b33b9-218">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="b33b9-219">Gebruik van Hallo SSH-verbinding, Hallo opdracht toocreate hello Kafka onderwerp gebruikt door Hallo topologie te volgen:</span><span class="sxs-lookup"><span data-stu-id="b33b9-219">From hello SSH connection, use hello following command toocreate hello Kafka topic used by hello topology:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="b33b9-220">Vervang `$KAFKAZKHOSTS` Hello Zookeeper hosten informatie die u in de vorige sectie Hallo opgehaald.</span><span class="sxs-lookup"><span data-stu-id="b33b9-220">Replace `$KAFKAZKHOSTS` with hello Zookeeper host information you retrieved in hello previous section.</span></span>

2. <span data-ttu-id="b33b9-221">Gebruik van Hallo SSH-verbinding toohello Storm-cluster Hallo opdracht toostart Hallo writer topologie te volgen:</span><span class="sxs-lookup"><span data-stu-id="b33b9-221">From hello SSH connection toohello Storm cluster, use hello following command toostart hello writer topology:</span></span>

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    <span data-ttu-id="b33b9-222">Hallo-parameters gebruikt met deze opdracht zijn:</span><span class="sxs-lookup"><span data-stu-id="b33b9-222">hello parameters used with this command are:</span></span>

    * <span data-ttu-id="b33b9-223">`org.apache.storm.flux.Flux`: Gebruik lichtstroom tooconfigure en voer deze topologie.</span><span class="sxs-lookup"><span data-stu-id="b33b9-223">`org.apache.storm.flux.Flux`: Use Flux tooconfigure and run this topology.</span></span>

    * <span data-ttu-id="b33b9-224">`--remote`: Hallo topologie tooNimbus verzenden.</span><span class="sxs-lookup"><span data-stu-id="b33b9-224">`--remote`: Submit hello topology tooNimbus.</span></span> <span data-ttu-id="b33b9-225">Hallo-topologie wordt verdeeld over Hallo worker-knooppunten in cluster Hallo.</span><span class="sxs-lookup"><span data-stu-id="b33b9-225">hello topology is distributed across hello worker nodes in hello cluster.</span></span>

    * <span data-ttu-id="b33b9-226">`-R /writer.yaml`: Gebruik Hallo `writer.yaml` bestand tooconfigure Hallo topologie.</span><span class="sxs-lookup"><span data-stu-id="b33b9-226">`-R /writer.yaml`: Use hello `writer.yaml` file tooconfigure hello topology.</span></span> <span data-ttu-id="b33b9-227">`-R`Hiermee wordt aangegeven dat deze bron wordt opgenomen in Hallo jar-bestand.</span><span class="sxs-lookup"><span data-stu-id="b33b9-227">`-R` indicates that this resource is included in hello jar file.</span></span> <span data-ttu-id="b33b9-228">Het is in de hoofdmap Hallo van Hallo jar, dus `/writer.yaml` Hallo pad tooit is.</span><span class="sxs-lookup"><span data-stu-id="b33b9-228">It's in hello root of hello jar, so `/writer.yaml` is hello path tooit.</span></span>

    * <span data-ttu-id="b33b9-229">`--filter`: Vullen vermeldingen in Hallo `writer.yaml` topologie met behulp van de waarden in Hallo `dev.properties` bestand.</span><span class="sxs-lookup"><span data-stu-id="b33b9-229">`--filter`: Populate entries in hello `writer.yaml` topology using values in hello `dev.properties` file.</span></span> <span data-ttu-id="b33b9-230">Bijvoorbeeld: waarde van Hallo Hallo `kafka.topic` vermelding in Hallo-bestand is gebruikte tooreplace hello `${kafka.topic}` vermelding in de definitie van de topologie Hallo.</span><span class="sxs-lookup"><span data-stu-id="b33b9-230">For example, hello value of hello `kafka.topic` entry in hello file is used tooreplace hello `${kafka.topic}` entry in hello topology definition.</span></span>

5. <span data-ttu-id="b33b9-231">Zodra het Hallo-topologie is gestart, gebruikt u Hallo opdracht tooverify dat het wegschrijven van gegevens toohello Kafka onderwerp te volgen:</span><span class="sxs-lookup"><span data-stu-id="b33b9-231">Once hello topology has started, use hello following command tooverify that it is writing data toohello Kafka topic:</span></span>

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    <span data-ttu-id="b33b9-232">Vervang `$KAFKAZKHOSTS` Hello Zookeeper hosten informatie die u in de vorige sectie Hallo opgehaald.</span><span class="sxs-lookup"><span data-stu-id="b33b9-232">Replace `$KAFKAZKHOSTS` with hello Zookeeper host information you retrieved in hello previous section.</span></span>

    <span data-ttu-id="b33b9-233">Met deze opdracht maakt gebruik van een script met Kafka toomonitor Hallo onderwerp verzonden.</span><span class="sxs-lookup"><span data-stu-id="b33b9-233">This command uses a script shipped with Kafka toomonitor hello topic.</span></span> <span data-ttu-id="b33b9-234">Na korte tijd, moet het eerst willekeurig zinnen die zijn geschreven toohello onderwerp retourneren.</span><span class="sxs-lookup"><span data-stu-id="b33b9-234">After a moment, it should start returning random sentences that have been written toohello topic.</span></span> <span data-ttu-id="b33b9-235">Hallo uitvoer is vergelijkbaar toohello volgende voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="b33b9-235">hello output is similar toohello following example:</span></span>

        i am at two with nature             
        an apple a day keeps hello doctor away
        snow white and hello seven dwarfs     
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        four score and seven years ago      
        snow white and hello seven dwarfs     
        snow white and hello seven dwarfs     
        i am at two with nature             
        an apple a day keeps hello doctor away

    <span data-ttu-id="b33b9-236">Gebruik Ctrl + c toostop Hallo script.</span><span class="sxs-lookup"><span data-stu-id="b33b9-236">Use Ctrl+c toostop hello script.</span></span>

## <a name="start-hello-reader"></a><span data-ttu-id="b33b9-237">Hallo lezer starten</span><span class="sxs-lookup"><span data-stu-id="b33b9-237">Start hello reader</span></span>

1. <span data-ttu-id="b33b9-238">Gebruik van Hallo SSH-sessie toohello Storm-cluster Hallo opdracht toostart Hallo lezer topologie te volgen:</span><span class="sxs-lookup"><span data-stu-id="b33b9-238">From hello SSH session toohello Storm cluster, use hello following command toostart hello reader topology:</span></span>

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. <span data-ttu-id="b33b9-239">Zodra het Hallo-topologie wordt gestart, opent u Hallo Storm-gebruikersinterface.</span><span class="sxs-lookup"><span data-stu-id="b33b9-239">Once hello topology starts, open hello Storm UI.</span></span> <span data-ttu-id="b33b9-240">Deze web-UI bevindt zich op https://storm-BASENAME.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="b33b9-240">This web UI is located at https://storm-BASENAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="b33b9-241">Vervang __BASENAME__ met Hallo basisnaam gebruikt bij het Hallo-cluster is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b33b9-241">Replace __BASENAME__ with hello base name used when hello cluster was created.</span></span> 

    <span data-ttu-id="b33b9-242">Wanneer u wordt gevraagd, Hallo beheerder aanmeldingsnaam gebruiken (standaard `admin`) en het wachtwoord als Hallo-cluster is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="b33b9-242">When prompted, use hello admin login name (default, `admin`) and password used when hello cluster was created.</span></span> <span data-ttu-id="b33b9-243">Er is een webpagina vergelijkbare toohello installatiekopie te volgen:</span><span class="sxs-lookup"><span data-stu-id="b33b9-243">You see a web page similar toohello following image:</span></span>

    ![Storm-gebruikersinterface](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. <span data-ttu-id="b33b9-245">Hallo Storm-gebruikersinterface, selecteer Hallo __kafka-lezer__ koppeling in Hallo __Topology Summary__ toodisplay informatie over Hallo sectie __kafka-lezer__ topologie.</span><span class="sxs-lookup"><span data-stu-id="b33b9-245">From hello Storm UI, select hello __kafka-reader__ link in hello __Topology Summary__ section toodisplay information about hello __kafka-reader__ topology.</span></span>

    ![Samenvatting van Hallo Storm-webgebruikersinterface topologie](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. <span data-ttu-id="b33b9-247">toodisplay informatie over exemplaren van Hallo berichtenlogboek bolt onderdeel, selecteer Hallo Hallo __berichtenlogboek bolt__ koppeling in Hallo __Bolts (alle tijd)__ sectie.</span><span class="sxs-lookup"><span data-stu-id="b33b9-247">toodisplay information about hello instances of hello logger-bolt component, select hello __logger-bolt__ link in hello __Bolts (All time)__ section.</span></span>

    ![Berichtenlogboek bolt koppeling in Hallo bolts sectie](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. <span data-ttu-id="b33b9-249">In Hallo __Executor__ sectie, selecteert u een koppeling in Hallo __poort__ kolom toodisplay logboekregistratie informatie over dit exemplaar van het Hallo-onderdeel.</span><span class="sxs-lookup"><span data-stu-id="b33b9-249">In hello __Executors__ section, select a link in hello __Port__ column toodisplay logging information about this instance of hello component.</span></span>

    ![Executor koppelen](./media/hdinsight-apache-storm-with-kafka/executors.png)

    <span data-ttu-id="b33b9-251">Hallo-logboek bevat een logboek van Hallo-gegevens lezen uit Hallo Kafka onderwerp.</span><span class="sxs-lookup"><span data-stu-id="b33b9-251">hello log contains a log of hello data read from hello Kafka topic.</span></span> <span data-ttu-id="b33b9-252">Hallo-informatie in Hallo-logboek is vergelijkbaar toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="b33b9-252">hello information in hello log is similar toohello following text:</span></span>

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] hello cow jumped over hello moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: hello cow jumped over hello moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps hello doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps hello doctor away

## <a name="stop-hello-topologies"></a><span data-ttu-id="b33b9-253">Hallo topologieën stoppen</span><span class="sxs-lookup"><span data-stu-id="b33b9-253">Stop hello topologies</span></span>

<span data-ttu-id="b33b9-254">Gebruik van een SSH-sessie toohello Storm-cluster Hallo opdrachten toostop Hallo Storm-topologieën te volgen:</span><span class="sxs-lookup"><span data-stu-id="b33b9-254">From an SSH session toohello Storm cluster, use hello following commands toostop hello Storm topologies:</span></span>

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-hello-cluster"></a><span data-ttu-id="b33b9-255">Hallo-cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="b33b9-255">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="b33b9-256">Aangezien Hallo stappen in dit document beide maken clusters in dezelfde Azure-resourcegroep hello, kunt u de resourcegroep Hallo in hello Azure-portal verwijderen.</span><span class="sxs-lookup"><span data-stu-id="b33b9-256">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="b33b9-257">Verwijderen van het Hallo-resourcegroep Hiermee verwijdert u alle resources die zijn gemaakt op basis van dit document.</span><span class="sxs-lookup"><span data-stu-id="b33b9-257">Deleting hello resource group removes all resources created by following this document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b33b9-258">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b33b9-258">Next steps</span></span>

<span data-ttu-id="b33b9-259">Zie voor meer voorbeeldtopologieën die kunnen worden gebruikt met Storm op HDInsight [voorbeeld Storm-topologieën en -onderdelen](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="b33b9-259">For more example topologies that can be used with Storm on HDInsight, see [Example Storm topologies and components](hdinsight-storm-example-topology.md).</span></span>

<span data-ttu-id="b33b9-260">Zie voor meer informatie over de implementatie en controle-topologieën op Linux gebaseerde HDInsight [implementeren en beheren van Apache Storm-topologieën op HDInsight op basis van Linux](hdinsight-storm-deploy-monitor-topology-linux.md)</span><span class="sxs-lookup"><span data-stu-id="b33b9-260">For information on deploying and monitoring topologies on Linux-based HDInsight, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>