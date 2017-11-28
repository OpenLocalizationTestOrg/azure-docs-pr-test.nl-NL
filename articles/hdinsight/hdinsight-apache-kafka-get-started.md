---
title: aaaStart met Apache Kafka - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe een Apache Kafka toocreate in Azure HDInsight-cluster. Meer informatie over hoe toocreate onderwerpen, abonnees en consumenten.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 43585abf-bec1-4322-adde-6db21de98d7f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: b93299d88dc2cf9a9764662509308ff75fd74474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="7e184-104">Met Apache Kafka (preview) in HDInsight beginnen</span><span class="sxs-lookup"><span data-stu-id="7e184-104">Start with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="7e184-105">Meer informatie over hoe toocreate en gebruik een [Apache Kafka](https://kafka.apache.org) cluster in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e184-105">Learn how toocreate and use an [Apache Kafka](https://kafka.apache.org) cluster on Azure HDInsight.</span></span> <span data-ttu-id="7e184-106">Kafka is een open-source, gedistribueerd streamingplatform dat beschikbaar is met HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e184-106">Kafka is an open-source, distributed streaming platform that is available with HDInsight.</span></span> <span data-ttu-id="7e184-107">Dit wordt vaak gebruikt als broker bericht, aangezien deze vergelijkbare functionaliteit biedt tooa voor publiceren / abonneren berichtenwachtrij.</span><span class="sxs-lookup"><span data-stu-id="7e184-107">It is often used as a message broker, as it provides functionality similar tooa publish-subscribe message queue.</span></span>

> [!NOTE]
> <span data-ttu-id="7e184-108">Er zijn momenteel twee versies van Kafka beschikbaar met HDInsight: 0.9.0 (HDInsight 3.4) en 0.10.0 (HDInsight 3.5 en 3.6).</span><span class="sxs-lookup"><span data-stu-id="7e184-108">There are currently two versions of Kafka available with HDInsight; 0.9.0 (HDInsight 3.4) and 0.10.0 (HDInsight 3.5 and 3.6).</span></span> <span data-ttu-id="7e184-109">Hallo stappen in dit document wordt ervan uitgegaan dat u van Kafka op HDInsight 3.6 gebruikmaakt.</span><span class="sxs-lookup"><span data-stu-id="7e184-109">hello steps in this document assume that you are using Kafka on HDInsight 3.6.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a><span data-ttu-id="7e184-110">Een Kafka-cluster maken</span><span class="sxs-lookup"><span data-stu-id="7e184-110">Create a Kafka cluster</span></span>

<span data-ttu-id="7e184-111">Gebruik Hallo stappen toocreate een Kafka op HDInsight-cluster te volgen:</span><span class="sxs-lookup"><span data-stu-id="7e184-111">Use hello following steps toocreate a Kafka on HDInsight cluster:</span></span>

1. <span data-ttu-id="7e184-112">Van Hallo [Azure-portal](https://portal.azure.com), selecteer **+ nieuw**, **Intelligence en analyse**, en selecteer vervolgens **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="7e184-112">From hello [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>
   
    ![Een HDInsight-cluster maken](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. <span data-ttu-id="7e184-114">Van **basisbeginselen**, Voer Hallo volgende informatie:</span><span class="sxs-lookup"><span data-stu-id="7e184-114">From **Basics**, enter hello following information:</span></span>

    * <span data-ttu-id="7e184-115">**Clusternaam**: Hallo-naam van Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="7e184-115">**Cluster Name**: hello name of hello HDInsight cluster.</span></span>
    * <span data-ttu-id="7e184-116">**Abonnement**: Hallo abonnement toouse selecteren.</span><span class="sxs-lookup"><span data-stu-id="7e184-116">**Subscription**: Select hello subscription toouse.</span></span>
    * <span data-ttu-id="7e184-117">**Gebruikersnaam voor aanmelding cluster** en **Cluster aanmeldingswachtwoord**: Hallo aanmelding bij het openen van Hallo-cluster via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="7e184-117">**Cluster login username** and **Cluster login password**: hello login when accessing hello cluster over HTTPS.</span></span> <span data-ttu-id="7e184-118">U gebruikt deze referenties tooaccess services zoals Hallo Ambari-Webgebruikersinterface of REST-API.</span><span class="sxs-lookup"><span data-stu-id="7e184-118">You use these credentials tooaccess services such as hello Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="7e184-119">**Secure Shell (SSH) gebruikersnaam**: Hallo-aanmeldingsnaam die wordt gebruikt bij het openen van Hallo-cluster via SSH.</span><span class="sxs-lookup"><span data-stu-id="7e184-119">**Secure Shell (SSH) username**: hello login used when accessing hello cluster over SSH.</span></span> <span data-ttu-id="7e184-120">Standaard is Hallo wachtwoord Hallo hetzelfde als Hallo aanmelding het wachtwoord van het cluster.</span><span class="sxs-lookup"><span data-stu-id="7e184-120">By default hello password is hello same as hello cluster login password.</span></span>
    * <span data-ttu-id="7e184-121">**Resourcegroep**: Hallo resource groep toocreate Hallo cluster in.</span><span class="sxs-lookup"><span data-stu-id="7e184-121">**Resource Group**: hello resource group toocreate hello cluster in.</span></span>
    * <span data-ttu-id="7e184-122">**Locatie**: hello Azure-regio toocreate Hallo cluster in.</span><span class="sxs-lookup"><span data-stu-id="7e184-122">**Location**: hello Azure region toocreate hello cluster in.</span></span>
   
 ![Abonnement selecteren](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. <span data-ttu-id="7e184-124">Selecteer **type Cluster**, en de volgende set Hallo waarden uit **clusterconfiguratie**:</span><span class="sxs-lookup"><span data-stu-id="7e184-124">Select **Cluster type**, and then set hello following values from **Cluster configuration**:</span></span>
   
    * <span data-ttu-id="7e184-125">**Clustertype**: Kafka</span><span class="sxs-lookup"><span data-stu-id="7e184-125">**Cluster Type**: Kafka</span></span>

    * <span data-ttu-id="7e184-126">**Versie**: Kafka 0.10.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="7e184-126">**Version**: Kafka 0.10.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="7e184-127">**Clusterlaag**: standaard</span><span class="sxs-lookup"><span data-stu-id="7e184-127">**Cluster Tier**: Standard</span></span>
     
 <span data-ttu-id="7e184-128">Gebruik tot slot Hallo **Selecteer** knop toosave instellingen.</span><span class="sxs-lookup"><span data-stu-id="7e184-128">Finally, use hello **Select** button toosave settings.</span></span>
     
 ![Clustertype selecteren](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="7e184-130">Gebruik na het selecteren van clustertype Hallo Hallo __Selecteer__ knoptype tooset Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="7e184-130">After selecting hello cluster type, use hello __Select__ button tooset hello cluster type.</span></span> <span data-ttu-id="7e184-131">Gebruik vervolgens Hallo __volgende__ knop toofinish basisconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="7e184-131">Next, use hello __Next__ button toofinish basic configuration.</span></span>

5. <span data-ttu-id="7e184-132">Selecteer of maak bij **Opslag** een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="7e184-132">From **Storage**, select or create a Storage account.</span></span> <span data-ttu-id="7e184-133">Laat Hallo andere velden op Hallo standaardwaarden voor Hallo stappen in dit document.</span><span class="sxs-lookup"><span data-stu-id="7e184-133">For hello steps in this document, leave hello other fields at hello default values.</span></span> <span data-ttu-id="7e184-134">Gebruik Hallo __volgende__ knop toosave opslagconfiguratie.</span><span class="sxs-lookup"><span data-stu-id="7e184-134">Use hello __Next__ button toosave storage configuration.</span></span>

    ![Hallo-opslag-accountinstellingen voor HDInsight instellen](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. <span data-ttu-id="7e184-136">Van __toepassingen (optioneel)__, selecteer __volgende__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="7e184-136">From __Applications (optional)__, select __Next__ toocontinue.</span></span> <span data-ttu-id="7e184-137">Er zijn geen toepassingen vereist voor dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="7e184-137">No applications are required for this example.</span></span>

7. <span data-ttu-id="7e184-138">Van __clustergrootte__, selecteer __volgende__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="7e184-138">From __Cluster size__, select __Next__ toocontinue.</span></span>

    > [!WARNING]
    > <span data-ttu-id="7e184-139">de beschikbaarheid van de tooguarantee van Kafka op HDInsight, uw cluster moet ten minste drie worker-knooppunten bevatten.</span><span class="sxs-lookup"><span data-stu-id="7e184-139">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span>

    ![Set Hallo Kafka clustergrootte](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > <span data-ttu-id="7e184-141">Hallo **schijven per werkrolknooppunt** besturingselementen voor gegevensinvoer Hallo schaalbaarheid van Kafka op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7e184-141">hello **disks per worker node** entry controls hello scalability of Kafka on HDInsight.</span></span> <span data-ttu-id="7e184-142">Zie voor meer informatie [Configure storage and scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span><span class="sxs-lookup"><span data-stu-id="7e184-142">For more information, see [Configure storage and scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

8. <span data-ttu-id="7e184-143">Van __geavanceerde instellingen__, selecteer __volgende__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="7e184-143">From __Advanced settings__, select __Next__ toocontinue.</span></span>

9. <span data-ttu-id="7e184-144">Van Hallo **samenvatting**, Controleer de configuratie van Hallo voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="7e184-144">From hello **Summary**, review hello configuration for hello cluster.</span></span> <span data-ttu-id="7e184-145">Gebruik Hallo __bewerken__ koppelingen toochange alle instellingen die onjuist zijn.</span><span class="sxs-lookup"><span data-stu-id="7e184-145">Use hello __Edit__ links toochange any settings that are incorrect.</span></span> <span data-ttu-id="7e184-146">Gebruik tot slot the__Create__ knop toocreate Hallo cluster.</span><span class="sxs-lookup"><span data-stu-id="7e184-146">Finally, use the__Create__ button toocreate hello cluster.</span></span>
   
    ![Samenvatting clusterconfiguratie](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > <span data-ttu-id="7e184-148">Too20 minuten toocreate Hallo cluster kan duren.</span><span class="sxs-lookup"><span data-stu-id="7e184-148">It can take up too20 minutes toocreate hello cluster.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="7e184-149">Verbinding maken met cluster toohello</span><span class="sxs-lookup"><span data-stu-id="7e184-149">Connect toohello cluster</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e184-150">Bij het uitvoeren van Hallo stappen uit te voeren, moet u een SSH-client.</span><span class="sxs-lookup"><span data-stu-id="7e184-150">When performing hello following steps, you must use an SSH client.</span></span> <span data-ttu-id="7e184-151">Zie voor meer informatie, Hallo [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="7e184-151">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

<span data-ttu-id="7e184-152">Gebruik van de client SSH tooconnect toohello cluster:</span><span class="sxs-lookup"><span data-stu-id="7e184-152">From your client, use SSH tooconnect toohello cluster:</span></span>

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

<span data-ttu-id="7e184-153">Vervang **SSHUSER** met Hallo SSH gebruikersnaam die u hebt opgegeven tijdens het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="7e184-153">Replace **SSHUSER** with hello SSH username you provided during cluster creation.</span></span> <span data-ttu-id="7e184-154">Vervang **CLUSTERNAME** met de naam van de cluster Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="7e184-154">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>

<span data-ttu-id="7e184-155">Voer desgevraagd Hallo wachtwoord die u voor Hallo SSH-account gebruikt.</span><span class="sxs-lookup"><span data-stu-id="7e184-155">When prompted, enter hello password you used for hello SSH account.</span></span>

<span data-ttu-id="7e184-156">Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.</span><span class="sxs-lookup"><span data-stu-id="7e184-156">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="7e184-157"><a id="getkafkainfo"></a>Hallo Zookeeper en Broker hostinformatie ophalen</span><span class="sxs-lookup"><span data-stu-id="7e184-157"><a id="getkafkainfo"></a>Get hello Zookeeper and Broker host information</span></span>

<span data-ttu-id="7e184-158">Als u werkt met Kafka, moet u weten twee waarden van de host. Hallo *Zookeeper* hosts en Hallo *Broker* hosts.</span><span class="sxs-lookup"><span data-stu-id="7e184-158">When working with Kafka, you must know two host values; hello *Zookeeper* hosts and hello *Broker* hosts.</span></span> <span data-ttu-id="7e184-159">Deze hosts worden gebruikt met Hallo Kafka API en veel Hallo-hulpprogramma's die worden geleverd met Kafka.</span><span class="sxs-lookup"><span data-stu-id="7e184-159">These hosts are used with hello Kafka API and many of hello utilities that ship with Kafka.</span></span>

<span data-ttu-id="7e184-160">Gebruik Hallo volgende stappen toocreate omgevingsvariabelen die Hallo hostinformatie bevatten.</span><span class="sxs-lookup"><span data-stu-id="7e184-160">Use hello following steps toocreate environment variables that contain hello host information.</span></span> <span data-ttu-id="7e184-161">Deze omgevingsvariabelen worden gebruikt in Hallo stappen in dit document.</span><span class="sxs-lookup"><span data-stu-id="7e184-161">These environment variables are used in hello steps in this document.</span></span>

1. <span data-ttu-id="7e184-162">Van een cluster met SSH-verbinding toohello, gebruik Hallo volgende tooinstall Hallo opdracht `jq` hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="7e184-162">From an SSH connection toohello cluster, use hello following command tooinstall hello `jq` utility.</span></span> <span data-ttu-id="7e184-163">Dit hulpprogramma is gebruikte tooparse JSON-documenten en is handig bij het ophalen van informatie over de host van de Hallo broker:</span><span class="sxs-lookup"><span data-stu-id="7e184-163">This utility is used tooparse JSON documents, and is useful in retrieving hello broker host information:</span></span>
   
    ```bash
    sudo apt -y install jq
    ```

2. <span data-ttu-id="7e184-164">tooset hello omgevingsvariabelen met informatie opgehaald van Ambari, gebruik Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="7e184-164">tooset hello environment variables with information retrieved from Ambari, use hello following commands:</span></span>

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="7e184-165">Stel `CLUSTERNAME=` toohello naam Hallo Kafka-cluster.</span><span class="sxs-lookup"><span data-stu-id="7e184-165">Set `CLUSTERNAME=` toohello name of hello Kafka cluster.</span></span> <span data-ttu-id="7e184-166">Stel `PASSWORD=` toohello (admin) aanmeldingswachtwoord u hebt gebruikt bij het maken van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="7e184-166">Set `PASSWORD=` toohello login (admin) password you used when creating hello cluster.</span></span>

    <span data-ttu-id="7e184-167">Hallo volgende tekst is een voorbeeld van de inhoud van Hallo `$KAFKAZKHOSTS`:</span><span class="sxs-lookup"><span data-stu-id="7e184-167">hello following text is an example of hello contents of `$KAFKAZKHOSTS`:</span></span>
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    <span data-ttu-id="7e184-168">Hallo volgende tekst is een voorbeeld van de inhoud van Hallo `$KAFKABROKERS`:</span><span class="sxs-lookup"><span data-stu-id="7e184-168">hello following text is an example of hello contents of `$KAFKABROKERS`:</span></span>
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > <span data-ttu-id="7e184-169">Hallo `cut` opdracht gebruikte tootrim Hallo lijst met hosts tootwo hostvermeldingen is.</span><span class="sxs-lookup"><span data-stu-id="7e184-169">hello `cut` command is used tootrim hello list of hosts tootwo host entries.</span></span> <span data-ttu-id="7e184-170">U hoeft niet tooprovide Hallo volledige lijst met hosts die bij het maken van een consumer Kafka of de producent.</span><span class="sxs-lookup"><span data-stu-id="7e184-170">You do not need tooprovide hello full list of hosts when creating a Kafka consumer or producer.</span></span>
   
    > [!WARNING]
    > <span data-ttu-id="7e184-171">Vertrouw niet op Hallo informatie geretourneerd door deze sessie tooalways nauwkeurig worden.</span><span class="sxs-lookup"><span data-stu-id="7e184-171">Do not rely on hello information returned from this session tooalways be accurate.</span></span> <span data-ttu-id="7e184-172">Als u Hallo-cluster schaalt, worden nieuwe beleggingsmakelaars toegevoegd of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="7e184-172">If you scale hello cluster, new brokers are added or removed.</span></span> <span data-ttu-id="7e184-173">Als een fout optreedt en een knooppunt wordt vervangen, kan Hallo-hostnaam voor het Hallo-knooppunt veranderen.</span><span class="sxs-lookup"><span data-stu-id="7e184-173">If a failure occurs and a node is replaced, hello host name for hello node may change.</span></span>
    >
    > <span data-ttu-id="7e184-174">Kort voordat u deze tooensure die u hebt geldige informatie gebruiken, moet u Hallo Zookeeper en broker hosts informatie ophalen.</span><span class="sxs-lookup"><span data-stu-id="7e184-174">You should retrieve hello Zookeeper and broker hosts information shortly before you use it tooensure you have valid information.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="7e184-175">Een onderwerp maken</span><span class="sxs-lookup"><span data-stu-id="7e184-175">Create a topic</span></span>

<span data-ttu-id="7e184-176">Kafka slaat gegevensstromen op in categorieën, zogenaamde *onderwerpen*.</span><span class="sxs-lookup"><span data-stu-id="7e184-176">Kafka stores streams of data in categories called *topics*.</span></span> <span data-ttu-id="7e184-177">Gebruik van een SSH-verbinding tooa cluster headnode, een script Kafka toocreate voorzien van een onderwerp:</span><span class="sxs-lookup"><span data-stu-id="7e184-177">From An SSH connection tooa cluster headnode, use a script provided with Kafka toocreate a topic:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="7e184-178">Met deze opdracht verbindt met behulp van Hallo hostinformatie opgeslagen in tooZookeeper `$KAFKAZKHOSTS`, en maak vervolgens met de naam Kafka-onderwerp **testen**.</span><span class="sxs-lookup"><span data-stu-id="7e184-178">This command connects tooZookeeper using hello host information stored in `$KAFKAZKHOSTS`, and then create Kafka topic named **test**.</span></span> <span data-ttu-id="7e184-179">U kunt controleren dat onderwerp Hallo is gemaakt met behulp van de volgende onderwerpen voor script toolist Hallo:</span><span class="sxs-lookup"><span data-stu-id="7e184-179">You can verify that hello topic was created by using hello following script toolist topics:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="7e184-180">Hallo uitvoer van deze opdracht geeft een lijst van Kafka-onderwerpen die Hallo bevat **testen** onderwerp.</span><span class="sxs-lookup"><span data-stu-id="7e184-180">hello output of this command lists Kafka topics, which contains hello **test** topic.</span></span>

## <a name="produce-and-consume-records"></a><span data-ttu-id="7e184-181">Records maken en gebruiken</span><span class="sxs-lookup"><span data-stu-id="7e184-181">Produce and consume records</span></span>

<span data-ttu-id="7e184-182">Kafka slaat *records* op in onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="7e184-182">Kafka stores *records* in topics.</span></span> <span data-ttu-id="7e184-183">Records worden geproduceerd door *producenten* en worden gebruikt door *consumenten*.</span><span class="sxs-lookup"><span data-stu-id="7e184-183">Records are produced by *producers*, and consumed by *consumers*.</span></span> <span data-ttu-id="7e184-184">Producenten halen records op uit Kafka-*brokers*.</span><span class="sxs-lookup"><span data-stu-id="7e184-184">Producers retrieve records from Kafka *brokers*.</span></span> <span data-ttu-id="7e184-185">Elk werkrolknooppunt in uw HDInsight-cluster is een Kafka-broker.</span><span class="sxs-lookup"><span data-stu-id="7e184-185">Each worker node in your HDInsight cluster is a Kafka broker.</span></span>

<span data-ttu-id="7e184-186">Gebruik Hallo stappen toostore records in Hallo test-onderwerp dat u eerder hebt gemaakt en leest u deze met een consumer te volgen:</span><span class="sxs-lookup"><span data-stu-id="7e184-186">Use hello following steps toostore records into hello test topic you created earlier, and then read them using a consumer:</span></span>

1. <span data-ttu-id="7e184-187">Van Hallo SSH-sessie, gebruikt u een script met Kafka toowrite records toohello onderwerp:</span><span class="sxs-lookup"><span data-stu-id="7e184-187">From hello SSH session, use a script provided with Kafka toowrite records toohello topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    <span data-ttu-id="7e184-188">U geen resultaten op toohello vragen na deze opdracht.</span><span class="sxs-lookup"><span data-stu-id="7e184-188">You are not returned toohello prompt after this command.</span></span> <span data-ttu-id="7e184-189">In plaats daarvan, typt u een paar tekstberichten en gebruik vervolgens **Ctrl + c drukken** toostop toohello onderwerp verzenden.</span><span class="sxs-lookup"><span data-stu-id="7e184-189">Instead, type a few text messages and then use **Ctrl + C** toostop sending toohello topic.</span></span> <span data-ttu-id="7e184-190">Elke regel wordt als een afzonderlijke record verzonden.</span><span class="sxs-lookup"><span data-stu-id="7e184-190">Each line is sent as a separate record.</span></span>

2. <span data-ttu-id="7e184-191">Gebruik een script met Kafka tooread records uit Hallo onderwerp:</span><span class="sxs-lookup"><span data-stu-id="7e184-191">Use a script provided with Kafka tooread records from hello topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    <span data-ttu-id="7e184-192">Met deze opdracht haalt Hallo records van Hallo onderwerp en weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7e184-192">This command retrieves hello records from hello topic and displays them.</span></span> <span data-ttu-id="7e184-193">Met behulp van `--from-beginning` vertelt Hallo consumer toostart vanaf Hallo Hallo stream, zodat alle records worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="7e184-193">Using `--from-beginning` tells hello consumer toostart from hello beginning of hello stream, so all records are retrieved.</span></span>

3. <span data-ttu-id="7e184-194">Gebruik __Ctrl + c drukken__ toostop Hallo consumer.</span><span class="sxs-lookup"><span data-stu-id="7e184-194">Use __Ctrl + C__ toostop hello consumer.</span></span>

## <a name="producer-and-consumer-api"></a><span data-ttu-id="7e184-195">Producent- en consument-API</span><span class="sxs-lookup"><span data-stu-id="7e184-195">Producer and consumer API</span></span>

<span data-ttu-id="7e184-196">U kunt ook programmatisch produceren en te gebruiken van records met behulp van Hallo [Kafka-API's](http://kafka.apache.org/documentation#api).</span><span class="sxs-lookup"><span data-stu-id="7e184-196">You can also programmatically produce and consume records using hello [Kafka APIs](http://kafka.apache.org/documentation#api).</span></span> <span data-ttu-id="7e184-197">toobuild een producent Java en de consument gebruik Hallo volgende stappen uit uw ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="7e184-197">toobuild a Java producer and consumer, use hello following steps from your development environment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e184-198">Hiervoor hebt u Hallo componenten zijn geïnstalleerd in uw ontwikkelomgeving te volgen:</span><span class="sxs-lookup"><span data-stu-id="7e184-198">You must have hello following components installed in your development environment:</span></span>
>
> * <span data-ttu-id="7e184-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) of een equivalent, zoals OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="7e184-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or an equivalent, such as OpenJDK.</span></span>
>
> * [<span data-ttu-id="7e184-200">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="7e184-200">Apache Maven</span></span>](http://maven.apache.org/)
>
> * <span data-ttu-id="7e184-201">Een SSH-client en het Hallo `scp` opdracht.</span><span class="sxs-lookup"><span data-stu-id="7e184-201">An SSH client and hello `scp` command.</span></span> <span data-ttu-id="7e184-202">Zie voor meer informatie, Hallo [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span><span class="sxs-lookup"><span data-stu-id="7e184-202">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

1. <span data-ttu-id="7e184-203">Voorbeelden van Hallo downloaden [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span><span class="sxs-lookup"><span data-stu-id="7e184-203">Download hello examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span></span> <span data-ttu-id="7e184-204">Hallo producent/consumer bijvoorbeeld Hallo-project in hello gebruiken `Producer-Consumer` directory.</span><span class="sxs-lookup"><span data-stu-id="7e184-204">For hello producer/consumer example, use hello project in hello `Producer-Consumer` directory.</span></span> <span data-ttu-id="7e184-205">In dit voorbeeld bevat Hallo klassen te volgen:</span><span class="sxs-lookup"><span data-stu-id="7e184-205">This example contains hello following classes:</span></span>
   
    * <span data-ttu-id="7e184-206">**Voer** -Hallo consumer of producent wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="7e184-206">**Run** - starts either hello consumer or producer.</span></span>

    * <span data-ttu-id="7e184-207">**Producent** -stores 1.000.000 records toohello onderwerp.</span><span class="sxs-lookup"><span data-stu-id="7e184-207">**Producer** - stores 1,000,000 records toohello topic.</span></span>

    * <span data-ttu-id="7e184-208">**Consumer** -records van Hallo onderwerp leest.</span><span class="sxs-lookup"><span data-stu-id="7e184-208">**Consumer** - reads records from hello topic.</span></span>

2. <span data-ttu-id="7e184-209">een pakket jar toocreate mappen toohello locatie Hallo wijzigen `Producer-Consumer` directory en gebruik Hallo volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="7e184-209">toocreate a jar package, change directories toohello location of hello `Producer-Consumer` directory and use hello following command:</span></span>

    ```
    mvn clean package
    ```

    <span data-ttu-id="7e184-210">Met deze opdracht maakt u een directory met de naam `target`, die een bestand met de naam `kafka-producer-consumer-1.0-SNAPSHOT.jar` bevat.</span><span class="sxs-lookup"><span data-stu-id="7e184-210">This command creates a directory named `target`, that contains a file named `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="7e184-211">Gebruik Hallo deze opdrachten toocopy hello `kafka-producer-consumer-1.0-SNAPSHOT.jar` bestand tooyour HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="7e184-211">Use hello following commands toocopy hello `kafka-producer-consumer-1.0-SNAPSHOT.jar` file tooyour HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    <span data-ttu-id="7e184-212">Vervang **SSHUSER** met Hallo SSH-gebruiker voor uw cluster, en vervang **CLUSTERNAME** met Hallo-naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="7e184-212">Replace **SSHUSER** with hello SSH user for your cluster, and replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="7e184-213">Als u wordt gevraagd Hallo wachtwoord invoeren voor Hallo SSH-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7e184-213">When prompted enter hello password for hello SSH user.</span></span>

4. <span data-ttu-id="7e184-214">Eenmaal Hallo `scp` opdracht kopiëren van het Hallo-bestand is voltooid, toohello-cluster via SSH verbinding.</span><span class="sxs-lookup"><span data-stu-id="7e184-214">Once hello `scp` command finishes copying hello file, connect toohello cluster using SSH.</span></span> <span data-ttu-id="7e184-215">Gebruik Hallo opdracht toowrite records toohello Testonderwerp te volgen:</span><span class="sxs-lookup"><span data-stu-id="7e184-215">Use hello following command toowrite records toohello test topic:</span></span>

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. <span data-ttu-id="7e184-216">Zodra Hallo is voltooid, gebruikt u de volgende opdracht tooread uit Hallo onderwerp Hallo:</span><span class="sxs-lookup"><span data-stu-id="7e184-216">Once hello process has finished, use hello following command tooread from hello topic:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    <span data-ttu-id="7e184-217">Hallo-records lezen, samen met een telling van records, wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="7e184-217">hello records read, along with a count of records, is displayed.</span></span> <span data-ttu-id="7e184-218">Mogelijk ziet u enkele van meer dan 1.000.000 geregistreerd als u meerdere records toohello onderwerp met een script in een eerdere stap hebt verzonden.</span><span class="sxs-lookup"><span data-stu-id="7e184-218">You may see a few more than 1,000,000 logged as you sent several records toohello topic using a script in an earlier step.</span></span>

6. <span data-ttu-id="7e184-219">Gebruik __Ctrl + c drukken__ tooexit Hallo consumer.</span><span class="sxs-lookup"><span data-stu-id="7e184-219">Use __Ctrl + C__ tooexit hello consumer.</span></span>

### <a name="multiple-consumers"></a><span data-ttu-id="7e184-220">Meerdere consumenten</span><span class="sxs-lookup"><span data-stu-id="7e184-220">Multiple consumers</span></span>

<span data-ttu-id="7e184-221">Kafka-consumenten gebruiken een consumentengroep bij het lezen van records.</span><span class="sxs-lookup"><span data-stu-id="7e184-221">Kafka consumers use a consumer group when reading records.</span></span> <span data-ttu-id="7e184-222">Met behulp van dezelfde groep Hallo met meerdere gebruikers, die balanced resulteert in een load leesbewerkingen van een onderwerp.</span><span class="sxs-lookup"><span data-stu-id="7e184-222">Using hello same group with multiple consumers results in load balanced reads from a topic.</span></span> <span data-ttu-id="7e184-223">Elke consumer in Hallo groep ontvangt een deel van het Hallo-records.</span><span class="sxs-lookup"><span data-stu-id="7e184-223">Each consumer in hello group receives a portion of hello records.</span></span> <span data-ttu-id="7e184-224">toosee dit proces in actie, gebruik Hallo volgende stappen:</span><span class="sxs-lookup"><span data-stu-id="7e184-224">toosee this process in action, use hello following steps:</span></span>

1. <span data-ttu-id="7e184-225">Open een nieuw SSH-sessie toohello cluster, zodat er twee van deze.</span><span class="sxs-lookup"><span data-stu-id="7e184-225">Open a new SSH session toohello cluster, so that you have two of them.</span></span> <span data-ttu-id="7e184-226">Gebruik in elke sessie Hallo na toostart Hallo een consumer met dezelfde consumer groeps-ID:</span><span class="sxs-lookup"><span data-stu-id="7e184-226">In each session, use hello following toostart a consumer with hello same consumer group ID:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    <span data-ttu-id="7e184-227">Deze opdracht start een consumer Hallo groeps-ID met `mygroup`.</span><span class="sxs-lookup"><span data-stu-id="7e184-227">This command starts a consumer using hello group ID `mygroup`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7e184-228">Hallo-opdrachten gebruiken in Hallo [hello Zookeeper en Broker host informatie](#getkafkainfo) sectie tooset `$KAFKABROKERS` voor deze SSH-sessie.</span><span class="sxs-lookup"><span data-stu-id="7e184-228">Use hello commands in hello [Get hello Zookeeper and Broker host information](#getkafkainfo) section tooset `$KAFKABROKERS` for this SSH session.</span></span>

2. <span data-ttu-id="7e184-229">Als elke sessie aantallen Hallo records die wordt ontvangen van Hallo onderwerp volgen.</span><span class="sxs-lookup"><span data-stu-id="7e184-229">Watch as each session counts hello records it receives from hello topic.</span></span> <span data-ttu-id="7e184-230">Hallo totaal van beide-sessies moet dezelfde worden Hallo als u eerder hebt ontvangen van een consumer.</span><span class="sxs-lookup"><span data-stu-id="7e184-230">hello total of both sessions should be hello same as you received previously from one consumer.</span></span>

<span data-ttu-id="7e184-231">Verbruik door clients binnen dezelfde groep wordt verwerkt door Hallo partities voor Hallo onderwerp Hallo.</span><span class="sxs-lookup"><span data-stu-id="7e184-231">Consumption by clients within hello same group is handled through hello partitions for hello topic.</span></span> <span data-ttu-id="7e184-232">Voor Hallo `test` onderwerp eerder hebt gemaakt, heeft acht partities.</span><span class="sxs-lookup"><span data-stu-id="7e184-232">For hello `test` topic created earlier, it has eight partitions.</span></span> <span data-ttu-id="7e184-233">Als u acht SSH-sessies openen en een gebruiker worden gestart in alle sessies, leest de elke consumer records uit één partitie voor Hallo onderwerp.</span><span class="sxs-lookup"><span data-stu-id="7e184-233">If you open eight SSH sessions and launch a consumer in all sessions, each consumer reads records from a single partition for hello topic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7e184-234">Een consumentengroep kan niet meer consumentexemplaren dan partities bevatten.</span><span class="sxs-lookup"><span data-stu-id="7e184-234">There cannot be more consumer instances in a consumer group than partitions.</span></span> <span data-ttu-id="7e184-235">In dit voorbeeld kan een consumergroep up tooeight consumenten bevatten, omdat dat Hallo aantal partities in Hallo onderwerp.</span><span class="sxs-lookup"><span data-stu-id="7e184-235">In this example, one consumer group can contain up tooeight consumers since that is hello number of partitions in hello topic.</span></span> <span data-ttu-id="7e184-236">U kunt ook meerdere consumentengroepen hebben, waarvan elke groep niet meer dan acht consumenten bevat.</span><span class="sxs-lookup"><span data-stu-id="7e184-236">Or you can have multiple consumer groups, each with no more than eight consumers.</span></span>

<span data-ttu-id="7e184-237">Records die zijn opgeslagen in Kafka worden opgeslagen in Hallo volgorde die binnen een partitie worden ontvangen.</span><span class="sxs-lookup"><span data-stu-id="7e184-237">Records stored in Kafka are stored in hello order they are received within a partition.</span></span> <span data-ttu-id="7e184-238">tooachieve-gerangschikt leveringsmethode voor records *binnen een partitie*, een consumergroep waarbij Hallo aantal exemplaren van de consument van overeenkomt met het aantal partities Hallo maken.</span><span class="sxs-lookup"><span data-stu-id="7e184-238">tooachieve in-ordered delivery for records *within a partition*, create a consumer group where hello number of consumer instances matches hello number of partitions.</span></span> <span data-ttu-id="7e184-239">tooachieve-gerangschikt leveringsmethode voor records *Hallo onderwerp*, een consumergroep te maken met een consumer slechts één exemplaar.</span><span class="sxs-lookup"><span data-stu-id="7e184-239">tooachieve in-ordered delivery for records *within hello topic*, create a consumer group with only one consumer instance.</span></span>

## <a name="streaming-api"></a><span data-ttu-id="7e184-240">Streaming-API</span><span class="sxs-lookup"><span data-stu-id="7e184-240">Streaming API</span></span>

<span data-ttu-id="7e184-241">Hallo streaming API is tooKafka toegevoegd in versie 0.10.0; eerdere versies zijn afhankelijk van Apache Spark of Storm voor de verwerking van de stroom.</span><span class="sxs-lookup"><span data-stu-id="7e184-241">hello streaming API was added tooKafka in version 0.10.0; earlier versions rely on Apache Spark or Storm for stream processing.</span></span>

1. <span data-ttu-id="7e184-242">Als u dit nog niet hebt gedaan, downloaden Hallo voorbeelden van [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="7e184-242">If you haven't already done so, download hello examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour development environment.</span></span> <span data-ttu-id="7e184-243">Gebruik voor Hallo streaming-voorbeeld, Hallo-project in Hallo `streaming` directory.</span><span class="sxs-lookup"><span data-stu-id="7e184-243">For hello streaming example, use hello project in hello `streaming` directory.</span></span>
   
    <span data-ttu-id="7e184-244">Dit project bevat slechts één klasse `Stream`, die records leest uit Hallo `test` onderwerp eerder hebt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7e184-244">This project contains only one class, `Stream`, which reads records from hello `test` topic created previously.</span></span> <span data-ttu-id="7e184-245">Het Hallo woorden lezen geteld en verzendt van elk woord en het aantal tooa onderwerp met de naam `wordcounts`.</span><span class="sxs-lookup"><span data-stu-id="7e184-245">It counts hello words read, and emits each word and count tooa topic named `wordcounts`.</span></span> <span data-ttu-id="7e184-246">Hallo `wordcounts` onderwerp in een latere stap in deze sectie wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="7e184-246">hello `wordcounts` topic is created in a later step in this section.</span></span>

2. <span data-ttu-id="7e184-247">Vanaf de opdrachtregel Hallo in uw ontwikkelomgeving, wijzig mappen toohello locatie Hallo `Streaming` directory en gebruik Hallo opdracht toocreate een jar-pakket te volgen:</span><span class="sxs-lookup"><span data-stu-id="7e184-247">From hello command line in your development environment, change directories toohello location of hello `Streaming` directory, and then use hello following command toocreate a jar package:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="7e184-248">Met deze opdracht maakt u een directory met de naam `target`, die een bestand met de naam `kafka-streaming-1.0-SNAPSHOT.jar` bevat.</span><span class="sxs-lookup"><span data-stu-id="7e184-248">This command creates a directory named `target`, which contains a file named `kafka-streaming-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="7e184-249">Gebruik Hallo deze opdrachten toocopy hello `kafka-streaming-1.0-SNAPSHOT.jar` bestand tooyour HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="7e184-249">Use hello following commands toocopy hello `kafka-streaming-1.0-SNAPSHOT.jar` file tooyour HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    <span data-ttu-id="7e184-250">Vervang **SSHUSER** met Hallo SSH-gebruiker voor uw cluster, en vervang **CLUSTERNAME** met Hallo-naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="7e184-250">Replace **SSHUSER** with hello SSH user for your cluster, and replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="7e184-251">Als u wordt gevraagd Hallo wachtwoord invoeren voor Hallo SSH-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="7e184-251">When prompted enter hello password for hello SSH user.</span></span>

4. <span data-ttu-id="7e184-252">Eenmaal Hallo `scp` opdracht kopiëren van het Hallo-bestand is voltooid, toohello-cluster via SSH verbinding maken met en gebruik vervolgens de volgende opdracht toocreate Hallo Hallo `wordcounts` onderwerp:</span><span class="sxs-lookup"><span data-stu-id="7e184-252">Once hello `scp` command finishes copying hello file, connect toohello cluster using SSH, and then use hello following command toocreate hello `wordcounts` topic:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. <span data-ttu-id="7e184-253">Vervolgens start Hallo streaming-proces met behulp van de volgende opdracht Hallo:</span><span class="sxs-lookup"><span data-stu-id="7e184-253">Next, start hello streaming process by using hello following command:</span></span>
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    <span data-ttu-id="7e184-254">Deze opdracht start Hallo proces op de achtergrond Hallo streaming.</span><span class="sxs-lookup"><span data-stu-id="7e184-254">This command starts hello streaming process in hello background.</span></span>

6. <span data-ttu-id="7e184-255">Gebruik Hallo volgende opdracht toosend berichten toohello `test` onderwerp.</span><span class="sxs-lookup"><span data-stu-id="7e184-255">Use hello following command toosend messages toohello `test` topic.</span></span> <span data-ttu-id="7e184-256">Deze berichten worden verwerkt door Hallo streaming-voorbeeld:</span><span class="sxs-lookup"><span data-stu-id="7e184-256">These messages are processed by hello streaming example:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. <span data-ttu-id="7e184-257">Gebruik Hallo tooview Hallo uitvoer van de opdracht die is geschreven toohello na `wordcounts` onderwerp door Hallo streaming proces:</span><span class="sxs-lookup"><span data-stu-id="7e184-257">Use hello following command tooview hello output that is written toohello `wordcounts` topic by hello streaming process:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > <span data-ttu-id="7e184-258">tooview hello gegevens, moet u Hallo consumer tooprint Hallo sleutel en Hallo deserializer toouse voor Hallo-sleutel en waarde zien.</span><span class="sxs-lookup"><span data-stu-id="7e184-258">tooview hello data, you must tell hello consumer tooprint hello key and hello deserializer toouse for hello key and value.</span></span> <span data-ttu-id="7e184-259">Hallo sleutelnaam is Hallo word en Hallo sleutelwaarde bevat Hallo count.</span><span class="sxs-lookup"><span data-stu-id="7e184-259">hello key name is hello word, and hello key value contains hello count.</span></span>
   
    <span data-ttu-id="7e184-260">Hallo uitvoer is vergelijkbaar toohello de volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="7e184-260">hello output is similar toohello following text:</span></span>
   
        dwarfs  13635
        ago     13664
        snow    13636
        dwarfs  13636
        ago     13665
        a       13803
        ago     13666
        a       13804
        ago     13667
        ago     13668
        jumped  13640
        jumped  13641
        a       13805
        snow    13637
   
    > [!NOTE]
    > <span data-ttu-id="7e184-261">Hallo aantal oploopt telkens wanneer een woord wordt aangetroffen.</span><span class="sxs-lookup"><span data-stu-id="7e184-261">hello count increments each time a word is encountered.</span></span>

7. <span data-ttu-id="7e184-262">Gebruik Hallo __Ctrl + c drukken__ tooexit Hallo consumer en gebruik vervolgens Hallo `fg` opdracht toobring Hallo streaming achtergrond taak back toohello voorgrond.</span><span class="sxs-lookup"><span data-stu-id="7e184-262">Use hello __Ctrl + C__ tooexit hello consumer, then use hello `fg` command toobring hello streaming background task back toohello foreground.</span></span> <span data-ttu-id="7e184-263">Gebruik __Ctrl + c drukken__ tooexit deze ook.</span><span class="sxs-lookup"><span data-stu-id="7e184-263">Use __Ctrl + C__ tooexit it also.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="7e184-264">Hallo-cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="7e184-264">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="7e184-265">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="7e184-265">Troubleshoot</span></span>

<span data-ttu-id="7e184-266">Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) als u problemen ondervindt met het maken van HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="7e184-266">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e184-267">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7e184-267">Next steps</span></span>

<span data-ttu-id="7e184-268">In dit document, kunt u Hallo basisbeginselen van het werken met Apache Kafka op HDInsight hebt geleerd.</span><span class="sxs-lookup"><span data-stu-id="7e184-268">In this document, you have learned hello basics of working with Apache Kafka on HDInsight.</span></span> <span data-ttu-id="7e184-269">Hallo toolearn meer informatie over het werken met Kafka volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="7e184-269">Use hello following toolearn more about working with Kafka:</span></span>

* [<span data-ttu-id="7e184-270">Hoge beschikbaarheid van uw gegevens met Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e184-270">Ensure high availability of your data with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-high-availability.md)
* [<span data-ttu-id="7e184-271">De schaalbaarheid verhogen door beheerde schijven met Kafka in HDInsight te configureren</span><span class="sxs-lookup"><span data-stu-id="7e184-271">Increase scalability by configuring managed disks with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* <span data-ttu-id="7e184-272">[Documentatie voor Apache Kafka](http://kafka.apache.org/documentation.html) op kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="7e184-272">[Apache Kafka documentation](http://kafka.apache.org/documentation.html) at kafka.apache.org.</span></span>
* [<span data-ttu-id="7e184-273">MirrorMaker toocreate een replica van Kafka op HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="7e184-273">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="7e184-274">Apache Storm gebruiken met Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e184-274">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="7e184-275">Apache Spark gebruiken met Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="7e184-275">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="7e184-276">TooKafka verbinding via een virtueel Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="7e184-276">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
