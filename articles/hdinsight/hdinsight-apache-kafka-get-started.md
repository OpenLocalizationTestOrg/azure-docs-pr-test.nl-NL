---
title: Met Apache Kafka beginnen - HDInsight | Microsoft Docs
description: Informatie over het maken van een Apache Kafka-cluster in Azure HDInsight. Informatie over het maken van onderwerpen, abonnees en consumenten.
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
ms.openlocfilehash: 03e6996f0f44e04978080b3bd267e924f342b7fc
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="44150-104">Met Apache Kafka (preview) in HDInsight beginnen</span><span class="sxs-lookup"><span data-stu-id="44150-104">Start with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="44150-105">Informatie over het maken en gebruiken van een [Apache Kafka](https://kafka.apache.org)-cluster in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="44150-105">Learn how to create and use an [Apache Kafka](https://kafka.apache.org) cluster on Azure HDInsight.</span></span> <span data-ttu-id="44150-106">Kafka is een open-source, gedistribueerd streamingplatform dat beschikbaar is met HDInsight.</span><span class="sxs-lookup"><span data-stu-id="44150-106">Kafka is an open-source, distributed streaming platform that is available with HDInsight.</span></span> <span data-ttu-id="44150-107">Het wordt vaak gebruikt als een berichtenbroker, omdat het een functionaliteit biedt die vergelijkbaar is met een publicatie-/abonnementswachtrij voor berichten.</span><span class="sxs-lookup"><span data-stu-id="44150-107">It is often used as a message broker, as it provides functionality similar to a publish-subscribe message queue.</span></span>

> [!NOTE]
> <span data-ttu-id="44150-108">Er zijn momenteel twee versies van Kafka beschikbaar met HDInsight: 0.9.0 (HDInsight 3.4) en 0.10.0 (HDInsight 3.5 en 3.6).</span><span class="sxs-lookup"><span data-stu-id="44150-108">There are currently two versions of Kafka available with HDInsight; 0.9.0 (HDInsight 3.4) and 0.10.0 (HDInsight 3.5 and 3.6).</span></span> <span data-ttu-id="44150-109">Voor de stappen in dit document wordt ervan uitgegaan dat u Kafka in HDInsight 3.6 gebruikt.</span><span class="sxs-lookup"><span data-stu-id="44150-109">The steps in this document assume that you are using Kafka on HDInsight 3.6.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a><span data-ttu-id="44150-110">Een Kafka-cluster maken</span><span class="sxs-lookup"><span data-stu-id="44150-110">Create a Kafka cluster</span></span>

<span data-ttu-id="44150-111">Gebruik de volgende stappen om een Kafka in HDInsight-cluster te maken:</span><span class="sxs-lookup"><span data-stu-id="44150-111">Use the following steps to create a Kafka on HDInsight cluster:</span></span>

1. <span data-ttu-id="44150-112">In [Azure Portal](https://portal.azure.com) selecteert u **+ NIEUW**, **Intelligence en analyse** en vervolgens **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="44150-112">From the [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>
   
    ![Een HDInsight-cluster maken](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. <span data-ttu-id="44150-114">Voer bij **Basisbeginselen** de volgende informatie in:</span><span class="sxs-lookup"><span data-stu-id="44150-114">From **Basics**, enter the following information:</span></span>

    * <span data-ttu-id="44150-115">**Clusternaam**: de naam van het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="44150-115">**Cluster Name**: The name of the HDInsight cluster.</span></span>
    * <span data-ttu-id="44150-116">**Abonnement**: selecteer het abonnement dat u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="44150-116">**Subscription**: Select the subscription to use.</span></span>
    * <span data-ttu-id="44150-117">**Aanmeldingsgebruikersnaam** en -**wachtwoord** van cluster: de aanmeldingsgegevens voor toegang tot het cluster via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="44150-117">**Cluster login username** and **Cluster login password**: The login when accessing the cluster over HTTPS.</span></span> <span data-ttu-id="44150-118">U gebruikt deze referenties voor toegang tot services als de Ambari-webinterface of de REST-API.</span><span class="sxs-lookup"><span data-stu-id="44150-118">You use these credentials to access services such as the Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="44150-119">**SSH-gebruikersnaam (Secure Shell)**: de aanmeldingsgegevens voor toegang tot het cluster via SSH.</span><span class="sxs-lookup"><span data-stu-id="44150-119">**Secure Shell (SSH) username**: The login used when accessing the cluster over SSH.</span></span> <span data-ttu-id="44150-120">Het wachtwoord is standaard hetzelfde als het aanmeldingswachtwoord van het cluster.</span><span class="sxs-lookup"><span data-stu-id="44150-120">By default the password is the same as the cluster login password.</span></span>
    * <span data-ttu-id="44150-121">**Resourcegroep**: de resourcegroep waarin het cluster wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="44150-121">**Resource Group**: The resource group to create the cluster in.</span></span>
    * <span data-ttu-id="44150-122">**Locatie**: de Azure-regio waarin het cluster wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="44150-122">**Location**: The Azure region to create the cluster in.</span></span>
   
 ![Abonnement selecteren](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. <span data-ttu-id="44150-124">Selecteer **Clustertype** en stel bij **Clusterconfiguratie** de volgende waarden in:</span><span class="sxs-lookup"><span data-stu-id="44150-124">Select **Cluster type**, and then set the following values from **Cluster configuration**:</span></span>
   
    * <span data-ttu-id="44150-125">**Clustertype**: Kafka</span><span class="sxs-lookup"><span data-stu-id="44150-125">**Cluster Type**: Kafka</span></span>

    * <span data-ttu-id="44150-126">**Versie**: Kafka 0.10.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="44150-126">**Version**: Kafka 0.10.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="44150-127">**Clusterlaag**: standaard</span><span class="sxs-lookup"><span data-stu-id="44150-127">**Cluster Tier**: Standard</span></span>
     
 <span data-ttu-id="44150-128">Gebruik ten slotte de knop **Selecteren** om de instellingen op te slaan.</span><span class="sxs-lookup"><span data-stu-id="44150-128">Finally, use the **Select** button to save settings.</span></span>
     
 ![Clustertype selecteren](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="44150-130">Nadat u het clustertype hebt geselecteerd, gebruikt u de knop __Selecteren__ om het clustertype te selecteren.</span><span class="sxs-lookup"><span data-stu-id="44150-130">After selecting the cluster type, use the __Select__ button to set the cluster type.</span></span> <span data-ttu-id="44150-131">Gebruik vervolgens de knop __Volgende__ om de basisconfiguratie te voltooien.</span><span class="sxs-lookup"><span data-stu-id="44150-131">Next, use the __Next__ button to finish basic configuration.</span></span>

5. <span data-ttu-id="44150-132">Selecteer of maak bij **Opslag** een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="44150-132">From **Storage**, select or create a Storage account.</span></span> <span data-ttu-id="44150-133">Voor de stappen in dit document laat u de andere velden op de standaardwaarden ingesteld.</span><span class="sxs-lookup"><span data-stu-id="44150-133">For the steps in this document, leave the other fields at the default values.</span></span> <span data-ttu-id="44150-134">Gebruik de knop __Volgende__ om de opslagconfiguratie op te slaan.</span><span class="sxs-lookup"><span data-stu-id="44150-134">Use the __Next__ button to save storage configuration.</span></span>

    ![De instellingen van het opslagaccount voor HDInsight configureren](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. <span data-ttu-id="44150-136">Selecteer bij __Toepassingen (optioneel)__ de optie __Volgende__ om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="44150-136">From __Applications (optional)__, select __Next__ to continue.</span></span> <span data-ttu-id="44150-137">Er zijn geen toepassingen vereist voor dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="44150-137">No applications are required for this example.</span></span>

7. <span data-ttu-id="44150-138">Selecteer bij __Clustergrootte__ de optie __Volgende__ om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="44150-138">From __Cluster size__, select __Next__ to continue.</span></span>

    > [!WARNING]
    > <span data-ttu-id="44150-139">Om beschikbaarheid van Kafka op HDInsight te garanderen, moet uw cluster ten minste drie werkknooppunten bevatten.</span><span class="sxs-lookup"><span data-stu-id="44150-139">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span>

    ![De Kafka-clustergrootte instellen](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > <span data-ttu-id="44150-141">De waarde voor de **schijven per werkknooppunt** bepaalt de schaalbaarheid van Kafka op HDInsight.</span><span class="sxs-lookup"><span data-stu-id="44150-141">The **disks per worker node** entry controls the scalability of Kafka on HDInsight.</span></span> <span data-ttu-id="44150-142">Zie voor meer informatie [Configure storage and scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span><span class="sxs-lookup"><span data-stu-id="44150-142">For more information, see [Configure storage and scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

8. <span data-ttu-id="44150-143">Selecteer bij __Geavanceerde instellingen__ de optie __Volgende__ om door te gaan.</span><span class="sxs-lookup"><span data-stu-id="44150-143">From __Advanced settings__, select __Next__ to continue.</span></span>

9. <span data-ttu-id="44150-144">Controleer bij **Samenvatting** de configuratie van het cluster.</span><span class="sxs-lookup"><span data-stu-id="44150-144">From the **Summary**, review the configuration for the cluster.</span></span> <span data-ttu-id="44150-145">Gebruik de koppeling __Bewerken__ om onjuiste instellingen te wijzigen.</span><span class="sxs-lookup"><span data-stu-id="44150-145">Use the __Edit__ links to change any settings that are incorrect.</span></span> <span data-ttu-id="44150-146">Gebruik tot slot de knop __Maken__ om het cluster te maken.</span><span class="sxs-lookup"><span data-stu-id="44150-146">Finally, use the__Create__ button to create the cluster.</span></span>
   
    ![Samenvatting clusterconfiguratie](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > <span data-ttu-id="44150-148">Het kan tot 20 minuten duren om het cluster te maken.</span><span class="sxs-lookup"><span data-stu-id="44150-148">It can take up to 20 minutes to create the cluster.</span></span>

## <a name="connect-to-the-cluster"></a><span data-ttu-id="44150-149">Verbinding maken met het cluster</span><span class="sxs-lookup"><span data-stu-id="44150-149">Connect to the cluster</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44150-150">Wanneer u de volgende stappen uitvoert, moet u een SSH-client gebruiken.</span><span class="sxs-lookup"><span data-stu-id="44150-150">When performing the following steps, you must use an SSH client.</span></span> <span data-ttu-id="44150-151">Zie het document [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="44150-151">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

<span data-ttu-id="44150-152">Gebruik SSH in uw client om verbinding te maken met het cluster:</span><span class="sxs-lookup"><span data-stu-id="44150-152">From your client, use SSH to connect to the cluster:</span></span>

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

<span data-ttu-id="44150-153">Vervang **SSHUSER** door de SSH-gebruikersnaam die u hebt opgegeven tijdens het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="44150-153">Replace **SSHUSER** with the SSH username you provided during cluster creation.</span></span> <span data-ttu-id="44150-154">Vervang **CLUSTERNAME** door de naam van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="44150-154">Replace **CLUSTERNAME** with the name of the cluster.</span></span>

<span data-ttu-id="44150-155">Voer het wachtwoord van het SSH-account in wanneer hierom wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="44150-155">When prompted, enter the password you used for the SSH account.</span></span>

<span data-ttu-id="44150-156">Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.</span><span class="sxs-lookup"><span data-stu-id="44150-156">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="44150-157"><a id="getkafkainfo"></a>Informatie over Zookeeper- en brokerhosts ophalen</span><span class="sxs-lookup"><span data-stu-id="44150-157"><a id="getkafkainfo"></a>Get the Zookeeper and Broker host information</span></span>

<span data-ttu-id="44150-158">Wanneer u met Kafka werkt, moet u twee hostwaarden weten: de *Zookeeper*-hosts en de *brokerhosts*.</span><span class="sxs-lookup"><span data-stu-id="44150-158">When working with Kafka, you must know two host values; the *Zookeeper* hosts and the *Broker* hosts.</span></span> <span data-ttu-id="44150-159">Deze hosts worden gebruikt met de Kafka-API en veel van de hulpprogramma's die bij Kafka worden meegeleverd.</span><span class="sxs-lookup"><span data-stu-id="44150-159">These hosts are used with the Kafka API and many of the utilities that ship with Kafka.</span></span>

<span data-ttu-id="44150-160">Gebruik de volgende stappen om omgevingsvariabelen te maken die de hostinformatie bevatten.</span><span class="sxs-lookup"><span data-stu-id="44150-160">Use the following steps to create environment variables that contain the host information.</span></span> <span data-ttu-id="44150-161">Deze omgevingsvariabelen worden in de stappen in dit document gebruikt.</span><span class="sxs-lookup"><span data-stu-id="44150-161">These environment variables are used in the steps in this document.</span></span>

1. <span data-ttu-id="44150-162">Wanneer er een SSH-verbinding is gemaakt met het cluster, gebruikt u de volgende opdracht om het hulpprogramma `jq` te installeren.</span><span class="sxs-lookup"><span data-stu-id="44150-162">From an SSH connection to the cluster, use the following command to install the `jq` utility.</span></span> <span data-ttu-id="44150-163">Dit hulpprogramma wordt gebruikt om JSON-documenten te parseren en is handig bij het ophalen van informatie van de brokerhost:</span><span class="sxs-lookup"><span data-stu-id="44150-163">This utility is used to parse JSON documents, and is useful in retrieving the broker host information:</span></span>
   
    ```bash
    sudo apt -y install jq
    ```

2. <span data-ttu-id="44150-164">Gebruik de volgende opdrachten om de omgevingsvariabelen in te stellen met informatie die is verkregen van Ambari:</span><span class="sxs-lookup"><span data-stu-id="44150-164">To set the environment variables with information retrieved from Ambari, use the following commands:</span></span>

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="44150-165">Stel `CLUSTERNAME=` in op de naam van het Kafka-cluster.</span><span class="sxs-lookup"><span data-stu-id="44150-165">Set `CLUSTERNAME=` to the name of the Kafka cluster.</span></span> <span data-ttu-id="44150-166">Stel `PASSWORD=` in op het aanmeldingswachtwoord (beheerder) dat u hebt gebruikt bij het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="44150-166">Set `PASSWORD=` to the login (admin) password you used when creating the cluster.</span></span>

    <span data-ttu-id="44150-167">De inhoud van `$KAFKAZKHOSTS` kan er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="44150-167">The following text is an example of the contents of `$KAFKAZKHOSTS`:</span></span>
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    <span data-ttu-id="44150-168">De inhoud van `$KAFKABROKERS` kan er als volgt uitzien:</span><span class="sxs-lookup"><span data-stu-id="44150-168">The following text is an example of the contents of `$KAFKABROKERS`:</span></span>
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > <span data-ttu-id="44150-169">De opdracht `cut` wordt gebruikt om de lijst met hosts in te korten tot twee hostvermeldingen.</span><span class="sxs-lookup"><span data-stu-id="44150-169">The `cut` command is used to trim the list of hosts to two host entries.</span></span> <span data-ttu-id="44150-170">U hoeft niet de volledige lijst met hosts op te geven bij het maken van een Kafka-consument of -producent.</span><span class="sxs-lookup"><span data-stu-id="44150-170">You do not need to provide the full list of hosts when creating a Kafka consumer or producer.</span></span>
   
    > [!WARNING]
    > <span data-ttu-id="44150-171">Ga er niet van uit dat de informatie die uit deze sessie naar voren komt altijd accuraat is.</span><span class="sxs-lookup"><span data-stu-id="44150-171">Do not rely on the information returned from this session to always be accurate.</span></span> <span data-ttu-id="44150-172">Als u het cluster schaalt, worden er nieuwe brokers toegevoegd of verwijderd.</span><span class="sxs-lookup"><span data-stu-id="44150-172">If you scale the cluster, new brokers are added or removed.</span></span> <span data-ttu-id="44150-173">Als er een fout optreedt en een knooppunt is vervangen, kan de hostnaam van het knooppunt veranderen.</span><span class="sxs-lookup"><span data-stu-id="44150-173">If a failure occurs and a node is replaced, the host name for the node may change.</span></span>
    >
    > <span data-ttu-id="44150-174">Haal de informatie over de Zookeeper- en brokerhosts kort voordat u deze gebruikt pas op, om er zeker van te zijn dat de gegevens geldig zijn.</span><span class="sxs-lookup"><span data-stu-id="44150-174">You should retrieve the Zookeeper and broker hosts information shortly before you use it to ensure you have valid information.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="44150-175">Een onderwerp maken</span><span class="sxs-lookup"><span data-stu-id="44150-175">Create a topic</span></span>

<span data-ttu-id="44150-176">Kafka slaat gegevensstromen op in categorieën, zogenaamde *onderwerpen*.</span><span class="sxs-lookup"><span data-stu-id="44150-176">Kafka stores streams of data in categories called *topics*.</span></span> <span data-ttu-id="44150-177">Wanneer er een SSH-verbinding is gemaakt met het hoofdknooppunt van het cluster, gebruikt u een script dat bij Kafka is meegeleverd om een onderwerp te maken:</span><span class="sxs-lookup"><span data-stu-id="44150-177">From An SSH connection to a cluster headnode, use a script provided with Kafka to create a topic:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="44150-178">Met deze opdracht brengt u een verbinding met Zookeeper tot stand met behulp van de hostinformatie die is opgeslagen in `$KAFKAZKHOSTS`. Maak vervolgens een Kafka-onderwerp met de naam **test**.</span><span class="sxs-lookup"><span data-stu-id="44150-178">This command connects to Zookeeper using the host information stored in `$KAFKAZKHOSTS`, and then create Kafka topic named **test**.</span></span> <span data-ttu-id="44150-179">U kunt controleren of het onderwerp is gemaakt door met het volgende script een lijst van de onderwerpen te genereren:</span><span class="sxs-lookup"><span data-stu-id="44150-179">You can verify that the topic was created by using the following script to list topics:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="44150-180">Met deze opdracht krijgt u een lijst van Kafka-onderwerpen, waaronder het onderwerp **test**.</span><span class="sxs-lookup"><span data-stu-id="44150-180">The output of this command lists Kafka topics, which contains the **test** topic.</span></span>

## <a name="produce-and-consume-records"></a><span data-ttu-id="44150-181">Records maken en gebruiken</span><span class="sxs-lookup"><span data-stu-id="44150-181">Produce and consume records</span></span>

<span data-ttu-id="44150-182">Kafka slaat *records* op in onderwerpen.</span><span class="sxs-lookup"><span data-stu-id="44150-182">Kafka stores *records* in topics.</span></span> <span data-ttu-id="44150-183">Records worden geproduceerd door *producenten* en worden gebruikt door *consumenten*.</span><span class="sxs-lookup"><span data-stu-id="44150-183">Records are produced by *producers*, and consumed by *consumers*.</span></span> <span data-ttu-id="44150-184">Producenten halen records op uit Kafka-*brokers*.</span><span class="sxs-lookup"><span data-stu-id="44150-184">Producers retrieve records from Kafka *brokers*.</span></span> <span data-ttu-id="44150-185">Elk werkrolknooppunt in uw HDInsight-cluster is een Kafka-broker.</span><span class="sxs-lookup"><span data-stu-id="44150-185">Each worker node in your HDInsight cluster is a Kafka broker.</span></span>

<span data-ttu-id="44150-186">Gebruik de volgende stappen om records op te slaan in het testonderwerp dat u eerder hebt gemaakt. Lees deze vervolgens met behulp van een consument:</span><span class="sxs-lookup"><span data-stu-id="44150-186">Use the following steps to store records into the test topic you created earlier, and then read them using a consumer:</span></span>

1. <span data-ttu-id="44150-187">Gebruik tijdens de SSH-sessie een script dat bij Kafka is meegeleverd om records te schrijven naar het onderwerp:</span><span class="sxs-lookup"><span data-stu-id="44150-187">From the SSH session, use a script provided with Kafka to write records to the topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    <span data-ttu-id="44150-188">Na deze opdracht keert u niet terug naar de prompt.</span><span class="sxs-lookup"><span data-stu-id="44150-188">You are not returned to the prompt after this command.</span></span> <span data-ttu-id="44150-189">In plaats daarvan typt u een paar tekstberichten en gebruikt u vervolgens **Ctrl + C** om verzending naar het onderwerp te stoppen.</span><span class="sxs-lookup"><span data-stu-id="44150-189">Instead, type a few text messages and then use **Ctrl + C** to stop sending to the topic.</span></span> <span data-ttu-id="44150-190">Elke regel wordt als een afzonderlijke record verzonden.</span><span class="sxs-lookup"><span data-stu-id="44150-190">Each line is sent as a separate record.</span></span>

2. <span data-ttu-id="44150-191">Gebruik een script dat bij Kafka is meegeleverd om records in het onderwerp te lezen:</span><span class="sxs-lookup"><span data-stu-id="44150-191">Use a script provided with Kafka to read records from the topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    <span data-ttu-id="44150-192">Met deze opdracht haalt u de records van het onderwerp op en geeft u deze weer.</span><span class="sxs-lookup"><span data-stu-id="44150-192">This command retrieves the records from the topic and displays them.</span></span> <span data-ttu-id="44150-193">Met `--from-beginning` wordt de consument gevraagd om bij het begin van de stream te beginnen, zodat alle records worden opgehaald.</span><span class="sxs-lookup"><span data-stu-id="44150-193">Using `--from-beginning` tells the consumer to start from the beginning of the stream, so all records are retrieved.</span></span>

3. <span data-ttu-id="44150-194">Gebruik __Ctrl + C__ om de consument te stoppen.</span><span class="sxs-lookup"><span data-stu-id="44150-194">Use __Ctrl + C__ to stop the consumer.</span></span>

## <a name="producer-and-consumer-api"></a><span data-ttu-id="44150-195">Producent- en consument-API</span><span class="sxs-lookup"><span data-stu-id="44150-195">Producer and consumer API</span></span>

<span data-ttu-id="44150-196">U kunt records ook programmatisch maken en gebruiken met behulp van de [Kafka-API's](http://kafka.apache.org/documentation#api).</span><span class="sxs-lookup"><span data-stu-id="44150-196">You can also programmatically produce and consume records using the [Kafka APIs](http://kafka.apache.org/documentation#api).</span></span> <span data-ttu-id="44150-197">Als u een Java-producent en -consument wilt bouwen, gebruikt u de volgende stappen uit de ontwikkelomgeving.</span><span class="sxs-lookup"><span data-stu-id="44150-197">To build a Java producer and consumer, use the following steps from your development environment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44150-198">De volgende onderdelen moeten zijn geïnstalleerd in de ontwikkelingsomgeving:</span><span class="sxs-lookup"><span data-stu-id="44150-198">You must have the following components installed in your development environment:</span></span>
>
> * <span data-ttu-id="44150-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) of een equivalent, zoals OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="44150-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or an equivalent, such as OpenJDK.</span></span>
>
> * [<span data-ttu-id="44150-200">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="44150-200">Apache Maven</span></span>](http://maven.apache.org/)
>
> * <span data-ttu-id="44150-201">Een SSH-client en de opdracht `scp`.</span><span class="sxs-lookup"><span data-stu-id="44150-201">An SSH client and the `scp` command.</span></span> <span data-ttu-id="44150-202">Zie het document [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="44150-202">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

1. <span data-ttu-id="44150-203">Download de voorbeelden van [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span><span class="sxs-lookup"><span data-stu-id="44150-203">Download the examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span></span> <span data-ttu-id="44150-204">Voor de producent/consumentvoorbeelden gebruikt u het project in de directory `Producer-Consumer`.</span><span class="sxs-lookup"><span data-stu-id="44150-204">For the producer/consumer example, use the project in the `Producer-Consumer` directory.</span></span> <span data-ttu-id="44150-205">Dit voorbeeld bevat de volgende klassen:</span><span class="sxs-lookup"><span data-stu-id="44150-205">This example contains the following classes:</span></span>
   
    * <span data-ttu-id="44150-206">**Uitvoering**: hiermee wordt de consument of de producent gestart.</span><span class="sxs-lookup"><span data-stu-id="44150-206">**Run** - starts either the consumer or producer.</span></span>

    * <span data-ttu-id="44150-207">**Producent**: hiermee kunnen 1.000.000 records in het onderwerp worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="44150-207">**Producer** - stores 1,000,000 records to the topic.</span></span>

    * <span data-ttu-id="44150-208">**Consument**: hiermee kunnen records in een onderwerp worden gelezen.</span><span class="sxs-lookup"><span data-stu-id="44150-208">**Consumer** - reads records from the topic.</span></span>

2. <span data-ttu-id="44150-209">Wijzig de mappen in de locatie van de map `Producer-Consumer` en gebruik de volgende opdracht om een JAR-pakket te maken:</span><span class="sxs-lookup"><span data-stu-id="44150-209">To create a jar package, change directories to the location of the `Producer-Consumer` directory and use the following command:</span></span>

    ```
    mvn clean package
    ```

    <span data-ttu-id="44150-210">Met deze opdracht maakt u een directory met de naam `target`, die een bestand met de naam `kafka-producer-consumer-1.0-SNAPSHOT.jar` bevat.</span><span class="sxs-lookup"><span data-stu-id="44150-210">This command creates a directory named `target`, that contains a file named `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="44150-211">Gebruik de volgende opdrachten om het bestand `kafka-producer-consumer-1.0-SNAPSHOT.jar` te kopiëren naar uw HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="44150-211">Use the following commands to copy the `kafka-producer-consumer-1.0-SNAPSHOT.jar` file to your HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    <span data-ttu-id="44150-212">Vervang **SSHUSER** door de SSH-gebruiker van uw cluster en vervang **CLUSTERNAME** door de naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="44150-212">Replace **SSHUSER** with the SSH user for your cluster, and replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="44150-213">Voer het wachtwoord van de SSH-gebruiker in wanneer hierom wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="44150-213">When prompted enter the password for the SSH user.</span></span>

4. <span data-ttu-id="44150-214">Als de `scp`-opdracht het bestand heeft gekopieerd, maakt u verbinding met het cluster met behulp van SSH.</span><span class="sxs-lookup"><span data-stu-id="44150-214">Once the `scp` command finishes copying the file, connect to the cluster using SSH.</span></span> <span data-ttu-id="44150-215">Gebruik de volgende opdracht om records naar het testonderwerp te schrijven:</span><span class="sxs-lookup"><span data-stu-id="44150-215">Use the following command to write records to the test topic:</span></span>

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. <span data-ttu-id="44150-216">Nadat het proces is voltooid, gebruikt u de volgende opdracht om het onderwerp te lezen:</span><span class="sxs-lookup"><span data-stu-id="44150-216">Once the process has finished, use the following command to read from the topic:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    <span data-ttu-id="44150-217">De gelezen records worden weergegeven, samen met een telling van de records.</span><span class="sxs-lookup"><span data-stu-id="44150-217">The records read, along with a count of records, is displayed.</span></span> <span data-ttu-id="44150-218">Mogelijk ziet u tellingen van meer dan 1.000.000, omdat u in een eerdere stap meerdere records naar het onderwerp hebt verzonden met behulp van een script.</span><span class="sxs-lookup"><span data-stu-id="44150-218">You may see a few more than 1,000,000 logged as you sent several records to the topic using a script in an earlier step.</span></span>

6. <span data-ttu-id="44150-219">Gebruik __Ctrl + C__ om de consument af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="44150-219">Use __Ctrl + C__ to exit the consumer.</span></span>

### <a name="multiple-consumers"></a><span data-ttu-id="44150-220">Meerdere consumenten</span><span class="sxs-lookup"><span data-stu-id="44150-220">Multiple consumers</span></span>

<span data-ttu-id="44150-221">Kafka-consumenten gebruiken een consumentengroep bij het lezen van records.</span><span class="sxs-lookup"><span data-stu-id="44150-221">Kafka consumers use a consumer group when reading records.</span></span> <span data-ttu-id="44150-222">Door dezelfde groep voor meerdere consumenten te gebruiken, worden leestaken voor onderwerpen gelijk verdeeld.</span><span class="sxs-lookup"><span data-stu-id="44150-222">Using the same group with multiple consumers results in load balanced reads from a topic.</span></span> <span data-ttu-id="44150-223">Elke consument in de groep ontvangt een deel van de records.</span><span class="sxs-lookup"><span data-stu-id="44150-223">Each consumer in the group receives a portion of the records.</span></span> <span data-ttu-id="44150-224">Voer de volgende stappen uit om dit proces in actie te zien:</span><span class="sxs-lookup"><span data-stu-id="44150-224">To see this process in action, use the following steps:</span></span>

1. <span data-ttu-id="44150-225">Open een nieuwe SSH-sessie met het cluster, zodat u twee sessies hebt.</span><span class="sxs-lookup"><span data-stu-id="44150-225">Open a new SSH session to the cluster, so that you have two of them.</span></span> <span data-ttu-id="44150-226">Gebruik het volgende in elke sessie om een consument te starten met dezelfde consumentengroeps-id:</span><span class="sxs-lookup"><span data-stu-id="44150-226">In each session, use the following to start a consumer with the same consumer group ID:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    <span data-ttu-id="44150-227">Deze opdracht start een consument met behulp van de groeps-id `mygroup`.</span><span class="sxs-lookup"><span data-stu-id="44150-227">This command starts a consumer using the group ID `mygroup`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="44150-228">Gebruik de opdrachten in het gedeelte [Informatie over Zookeeper- en brokerhosts ophalen](#getkafkainfo) om `$KAFKABROKERS` in te stellen voor deze SSH-sessie.</span><span class="sxs-lookup"><span data-stu-id="44150-228">Use the commands in the [Get the Zookeeper and Broker host information](#getkafkainfo) section to set `$KAFKABROKERS` for this SSH session.</span></span>

2. <span data-ttu-id="44150-229">Voor elke sessie worden nu de records geteld die worden ontvangen van het onderwerp.</span><span class="sxs-lookup"><span data-stu-id="44150-229">Watch as each session counts the records it receives from the topic.</span></span> <span data-ttu-id="44150-230">Het totaal van beide sessies moet hetzelfde zijn als wat u eerder ontving van één consument.</span><span class="sxs-lookup"><span data-stu-id="44150-230">The total of both sessions should be the same as you received previously from one consumer.</span></span>

<span data-ttu-id="44150-231">Gebruik door clients binnen dezelfde groep wordt verwerkt door de partities voor het onderwerp.</span><span class="sxs-lookup"><span data-stu-id="44150-231">Consumption by clients within the same group is handled through the partitions for the topic.</span></span> <span data-ttu-id="44150-232">Het eerder gemaakte onderwerp `test` heeft acht partities.</span><span class="sxs-lookup"><span data-stu-id="44150-232">For the `test` topic created earlier, it has eight partitions.</span></span> <span data-ttu-id="44150-233">Als u acht SSH-sessies opent en in alle sessies een consument start, leest de consument de records van één partitie voor het onderwerp.</span><span class="sxs-lookup"><span data-stu-id="44150-233">If you open eight SSH sessions and launch a consumer in all sessions, each consumer reads records from a single partition for the topic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="44150-234">Een consumentengroep kan niet meer consumentexemplaren dan partities bevatten.</span><span class="sxs-lookup"><span data-stu-id="44150-234">There cannot be more consumer instances in a consumer group than partitions.</span></span> <span data-ttu-id="44150-235">In dit voorbeeld kan één consumentengroep maximaal acht consumenten bevatten, omdat het onderwerp dit aantal partities heeft.</span><span class="sxs-lookup"><span data-stu-id="44150-235">In this example, one consumer group can contain up to eight consumers since that is the number of partitions in the topic.</span></span> <span data-ttu-id="44150-236">U kunt ook meerdere consumentengroepen hebben, waarvan elke groep niet meer dan acht consumenten bevat.</span><span class="sxs-lookup"><span data-stu-id="44150-236">Or you can have multiple consumer groups, each with no more than eight consumers.</span></span>

<span data-ttu-id="44150-237">Records worden in Kafka opgeslagen in de volgorde waarin deze worden ontvangen binnen een partitie.</span><span class="sxs-lookup"><span data-stu-id="44150-237">Records stored in Kafka are stored in the order they are received within a partition.</span></span> <span data-ttu-id="44150-238">Als u records *binnen een partitie* op volgorde wilt leveren, maakt u een consumentengroep waarvan het aantal consumentexemplaren gelijk is aan het aantal partities.</span><span class="sxs-lookup"><span data-stu-id="44150-238">To achieve in-ordered delivery for records *within a partition*, create a consumer group where the number of consumer instances matches the number of partitions.</span></span> <span data-ttu-id="44150-239">Als u records *binnen het onderwerp* op volgorde wilt leveren, maakt u een consumentengroep met slechts één consumentexemplaar.</span><span class="sxs-lookup"><span data-stu-id="44150-239">To achieve in-ordered delivery for records *within the topic*, create a consumer group with only one consumer instance.</span></span>

## <a name="streaming-api"></a><span data-ttu-id="44150-240">Streaming-API</span><span class="sxs-lookup"><span data-stu-id="44150-240">Streaming API</span></span>

<span data-ttu-id="44150-241">De streaming-API is in versie 0.10.0 aan Kafka toegevoegd. Eerdere versies zijn afhankelijk van Apache Spark of Storm voor streamverwerking.</span><span class="sxs-lookup"><span data-stu-id="44150-241">The streaming API was added to Kafka in version 0.10.0; earlier versions rely on Apache Spark or Storm for stream processing.</span></span>

1. <span data-ttu-id="44150-242">Download de voorbeelden van [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) naar uw ontwikkelingsomgeving als u dit nog niet hebt gedaan.</span><span class="sxs-lookup"><span data-stu-id="44150-242">If you haven't already done so, download the examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) to your development environment.</span></span> <span data-ttu-id="44150-243">Voor het streamingvoorbeeld gebruikt u het project in de directory `streaming`.</span><span class="sxs-lookup"><span data-stu-id="44150-243">For the streaming example, use the project in the `streaming` directory.</span></span>
   
    <span data-ttu-id="44150-244">Dit project bevat slechts één klasse: `Stream`. Deze leest records van het eerder gemaakte onderwerp `test`.</span><span class="sxs-lookup"><span data-stu-id="44150-244">This project contains only one class, `Stream`, which reads records from the `test` topic created previously.</span></span> <span data-ttu-id="44150-245">De gelezen woorden worden geteld, en elk woord en de telling worden verzonden een onderwerp met de naam `wordcounts`.</span><span class="sxs-lookup"><span data-stu-id="44150-245">It counts the words read, and emits each word and count to a topic named `wordcounts`.</span></span> <span data-ttu-id="44150-246">Het onderwerp `wordcounts` wordt in een latere stap in dit gedeelte gemaakt.</span><span class="sxs-lookup"><span data-stu-id="44150-246">The `wordcounts` topic is created in a later step in this section.</span></span>

2. <span data-ttu-id="44150-247">In de opdrachtregel in uw ontwikkelingsomgeving wijzigt u de directory's in de locatie van de directory `Streaming`. Vervolgens gebruikt u de volgende opdracht om een JAR-pakket te maken:</span><span class="sxs-lookup"><span data-stu-id="44150-247">From the command line in your development environment, change directories to the location of the `Streaming` directory, and then use the following command to create a jar package:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="44150-248">Met deze opdracht maakt u een directory met de naam `target`, die een bestand met de naam `kafka-streaming-1.0-SNAPSHOT.jar` bevat.</span><span class="sxs-lookup"><span data-stu-id="44150-248">This command creates a directory named `target`, which contains a file named `kafka-streaming-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="44150-249">Gebruik de volgende opdrachten om het bestand `kafka-streaming-1.0-SNAPSHOT.jar` te kopiëren naar uw HDInsight-cluster:</span><span class="sxs-lookup"><span data-stu-id="44150-249">Use the following commands to copy the `kafka-streaming-1.0-SNAPSHOT.jar` file to your HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    <span data-ttu-id="44150-250">Vervang **SSHUSER** door de SSH-gebruiker van uw cluster en vervang **CLUSTERNAME** door de naam van het cluster.</span><span class="sxs-lookup"><span data-stu-id="44150-250">Replace **SSHUSER** with the SSH user for your cluster, and replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="44150-251">Voer het wachtwoord van de SSH-gebruiker in wanneer hierom wordt gevraagd.</span><span class="sxs-lookup"><span data-stu-id="44150-251">When prompted enter the password for the SSH user.</span></span>

4. <span data-ttu-id="44150-252">Nadat de opdracht `scp` klaar is met het kopiëren van het bestand, maakt u een SSH-verbinding met het cluster en gebruikt u de volgende opdracht om het onderwerp `wordcounts` te maken:</span><span class="sxs-lookup"><span data-stu-id="44150-252">Once the `scp` command finishes copying the file, connect to the cluster using SSH, and then use the following command to create the `wordcounts` topic:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. <span data-ttu-id="44150-253">Start vervolgens het streamingproces met behulp van de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="44150-253">Next, start the streaming process by using the following command:</span></span>
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    <span data-ttu-id="44150-254">Met deze opdracht wordt het streamingproces op de achtergrond gestart.</span><span class="sxs-lookup"><span data-stu-id="44150-254">This command starts the streaming process in the background.</span></span>

6. <span data-ttu-id="44150-255">Gebruik de volgende opdracht om berichten naar het onderwerp `test` te verzenden.</span><span class="sxs-lookup"><span data-stu-id="44150-255">Use the following command to send messages to the `test` topic.</span></span> <span data-ttu-id="44150-256">Deze berichten worden verwerkt door het streamingvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="44150-256">These messages are processed by the streaming example:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. <span data-ttu-id="44150-257">Gebruik de volgende opdracht om de uitvoer weer te geven die tijdens het streamingproces wordt geschreven naar het onderwerp `wordcounts`:</span><span class="sxs-lookup"><span data-stu-id="44150-257">Use the following command to view the output that is written to the `wordcounts` topic by the streaming process:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > <span data-ttu-id="44150-258">Om de gegevens te bekijken, geeft u de consument de opdracht om de sleutel af te drukken, evenals de deserialisatiefunctie die wordt gebruikt voor de sleutel en waarde.</span><span class="sxs-lookup"><span data-stu-id="44150-258">To view the data, you must tell the consumer to print the key and the deserializer to use for the key and value.</span></span> <span data-ttu-id="44150-259">De sleutelnaam is het woord en de sleutelwaarde bevat de telling.</span><span class="sxs-lookup"><span data-stu-id="44150-259">The key name is the word, and the key value contains the count.</span></span>
   
    <span data-ttu-id="44150-260">De uitvoer lijkt op het volgende:</span><span class="sxs-lookup"><span data-stu-id="44150-260">The output is similar to the following text:</span></span>
   
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
    > <span data-ttu-id="44150-261">De telling wordt verhoogd wanneer er een woord wordt gedetecteerd.</span><span class="sxs-lookup"><span data-stu-id="44150-261">The count increments each time a word is encountered.</span></span>

7. <span data-ttu-id="44150-262">Gebruik __Ctrl + C__ om de consument af te sluiten. Gebruik vervolgens de opdracht `fg` om de streamingtaak weer op de voorgrond uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="44150-262">Use the __Ctrl + C__ to exit the consumer, then use the `fg` command to bring the streaming background task back to the foreground.</span></span> <span data-ttu-id="44150-263">Gebruik __Ctrl + C__ om af te sluiten.</span><span class="sxs-lookup"><span data-stu-id="44150-263">Use __Ctrl + C__ to exit it also.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="44150-264">Het cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="44150-264">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="44150-265">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="44150-265">Troubleshoot</span></span>

<span data-ttu-id="44150-266">Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) als u problemen ondervindt met het maken van HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="44150-266">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="44150-267">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="44150-267">Next steps</span></span>

<span data-ttu-id="44150-268">In dit document hebt u de basisbeginselen geleerd van hoe u met Apache Kafka in HDInsight werkt.</span><span class="sxs-lookup"><span data-stu-id="44150-268">In this document, you have learned the basics of working with Apache Kafka on HDInsight.</span></span> <span data-ttu-id="44150-269">Gebruik de volgende documenten voor meer informatie over het werken met Kafka:</span><span class="sxs-lookup"><span data-stu-id="44150-269">Use the following to learn more about working with Kafka:</span></span>

* [<span data-ttu-id="44150-270">Hoge beschikbaarheid van uw gegevens met Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="44150-270">Ensure high availability of your data with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-high-availability.md)
* [<span data-ttu-id="44150-271">De schaalbaarheid verhogen door beheerde schijven met Kafka in HDInsight te configureren</span><span class="sxs-lookup"><span data-stu-id="44150-271">Increase scalability by configuring managed disks with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* <span data-ttu-id="44150-272">[Documentatie voor Apache Kafka](http://kafka.apache.org/documentation.html) op kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="44150-272">[Apache Kafka documentation](http://kafka.apache.org/documentation.html) at kafka.apache.org.</span></span>
* [<span data-ttu-id="44150-273">MirrorMaker gebruiken voor het maken van een replica van Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="44150-273">Use MirrorMaker to create a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="44150-274">Apache Storm gebruiken met Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="44150-274">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="44150-275">Apache Spark gebruiken met Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="44150-275">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="44150-276">Verbinding maken met Kafka via een Azure Virtual Network</span><span class="sxs-lookup"><span data-stu-id="44150-276">Connect to Kafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
