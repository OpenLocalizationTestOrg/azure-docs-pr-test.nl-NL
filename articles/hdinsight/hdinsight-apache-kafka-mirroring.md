---
title: onderwerpen over aaaMirror Apache Kafka - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe een replica van een Kafka op HDInsight-cluster toomaintain door mirroring van onderwerpen tooa secundaire cluster toouse Apache Kafka spiegelen functie.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 015d276e-f678-4f2b-9572-75553c56625b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: 5ace0251d7402d4d7d9b28726e253ce7091a87ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-mirrormaker-tooreplicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a><span data-ttu-id="cffb8-103">Gebruik MirrorMaker tooreplicate Apache Kafka onderwerpen met Kafka op HDInsight (preview)</span><span class="sxs-lookup"><span data-stu-id="cffb8-103">Use MirrorMaker tooreplicate Apache Kafka topics with Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="cffb8-104">Meer informatie over hoe toouse Apache Kafka het spiegelen van de functie tooreplicate onderwerpen tooa secundaire cluster.</span><span class="sxs-lookup"><span data-stu-id="cffb8-104">Learn how toouse Apache Kafka's mirroring feature tooreplicate topics tooa secondary cluster.</span></span> <span data-ttu-id="cffb8-105">Het spiegelen kan worden uitgevoerd als een continu proces of af en toe worden gebruikt als een methode voor het migreren van gegevens uit een cluster tooanother.</span><span class="sxs-lookup"><span data-stu-id="cffb8-105">Mirroring can be ran as a continuous process, or used intermittently as a method of migrating data from one cluster tooanother.</span></span>

<span data-ttu-id="cffb8-106">In dit voorbeeld is het spiegelen gebruikte tooreplicate onderwerpen tussen twee clusters met HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cffb8-106">In this example, mirroring is used tooreplicate topics between two HDInsight clusters.</span></span> <span data-ttu-id="cffb8-107">Beide clusters zijn in een Azure-netwerk in Hallo dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="cffb8-107">Both clusters are in an Azure Virtual Network in hello same region.</span></span>

> [!WARNING]
> <span data-ttu-id="cffb8-108">Spiegeling moet niet worden beschouwd als een manier tooachieve fouttolerantie.</span><span class="sxs-lookup"><span data-stu-id="cffb8-108">Mirroring should not be considered as a means tooachieve fault-tolerance.</span></span> <span data-ttu-id="cffb8-109">Hallo offset tooitems binnen een onderwerp zijn de verschillen tussen clusters van Hallo bron- en doelserver, zodat clients kunnen niet door elkaar Hallo twee gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cffb8-109">hello offset tooitems within a topic are different between hello source and destination clusters, so clients cannot use hello two interchangeably.</span></span>
>
> <span data-ttu-id="cffb8-110">Als u zich zorgen over fouttolerantie, stelt u replicatie voor Hallo onderwerpen binnen het cluster.</span><span class="sxs-lookup"><span data-stu-id="cffb8-110">If you are concerned about fault tolerance, you should set replication for hello topics within your cluster.</span></span> <span data-ttu-id="cffb8-111">Zie voor meer informatie [aan de slag met Kafka op HDInsight](hdinsight-apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="cffb8-111">For more information, see [Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md).</span></span>

## <a name="how-kafka-mirroring-works"></a><span data-ttu-id="cffb8-112">De werking van Kafka spiegelen</span><span class="sxs-lookup"><span data-stu-id="cffb8-112">How Kafka mirroring works</span></span>

<span data-ttu-id="cffb8-113">Mirroring werkt met behulp van Hallo MirrorMaker hulpprogramma (onderdeel van Apache Kafka) tooconsume records van de onderwerpen in de broncluster hello en maak vervolgens een lokale kopie op Hallo doelcluster.</span><span class="sxs-lookup"><span data-stu-id="cffb8-113">Mirroring works by using hello MirrorMaker tool (part of Apache Kafka) tooconsume records from topics on hello source cluster and then create a local copy on hello destination cluster.</span></span> <span data-ttu-id="cffb8-114">MirrorMaker maakt gebruik van een (of meer) *consumenten* die gelezen van Hallo broncluster, en een *producent* die schrijft toohello lokale (doel) cluster.</span><span class="sxs-lookup"><span data-stu-id="cffb8-114">MirrorMaker uses one (or more) *consumers* that read from hello source cluster, and a *producer* that writes toohello local (destination) cluster.</span></span>

<span data-ttu-id="cffb8-115">Hallo volgende diagram illustreert Hallo spiegelen proces:</span><span class="sxs-lookup"><span data-stu-id="cffb8-115">hello following diagram illustrates hello Mirroring process:</span></span>

![Diagram van Hallo proces spiegelen](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

<span data-ttu-id="cffb8-117">Apache Kafka op HDInsight biedt geen toegang tot toohello Kafka service ten opzichte van Hallo openbare internet.</span><span class="sxs-lookup"><span data-stu-id="cffb8-117">Apache Kafka on HDInsight does not provide access toohello Kafka service over hello public internet.</span></span> <span data-ttu-id="cffb8-118">Moeten in Hallo Kafka producenten en consumenten hetzelfde virtuele Azure-netwerk als Hallo knooppunten in Hallo Kafka-cluster.</span><span class="sxs-lookup"><span data-stu-id="cffb8-118">Kafka producers or consumers must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="cffb8-119">Bijvoorbeeld, bevinden zowel Hallo Kafka bron en bestemming clusters zich in een Azure-netwerk.</span><span class="sxs-lookup"><span data-stu-id="cffb8-119">For this example, both hello Kafka source and destination clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="cffb8-120">Hallo volgende diagram ziet u hoe de communicatie tussen clusters met Hallo loopt:</span><span class="sxs-lookup"><span data-stu-id="cffb8-120">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagram van de bron en bestemming Kafka-clusters in een Azure-netwerk](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

<span data-ttu-id="cffb8-122">de bron- en doelserver clusters Hallo kunnen afwijken van Hallo aantal knooppunten en partities en offsets binnen Hallo onderwerpen zijn ook verschillend.</span><span class="sxs-lookup"><span data-stu-id="cffb8-122">hello source and destination clusters can be different in hello number of nodes and partitions, and offsets within hello topics are different also.</span></span> <span data-ttu-id="cffb8-123">Hallo-sleutelwaarde die wordt gebruikt voor het partitioneren, mirroring worden bijgehouden, zodat de volgorde van de records op basis van de per-sleutel wordt behouden.</span><span class="sxs-lookup"><span data-stu-id="cffb8-123">Mirroring maintains hello key value that is used for partitioning, so record order is preserved on a per-key basis.</span></span>

### <a name="mirroring-across-network-boundaries"></a><span data-ttu-id="cffb8-124">Spiegelen buiten de netwerkgrenzen van</span><span class="sxs-lookup"><span data-stu-id="cffb8-124">Mirroring across network boundaries</span></span>

<span data-ttu-id="cffb8-125">Als u toomirror tussen clusters met Kafka in verschillende netwerken moet, zijn er aanvullende overwegingen na Hallo:</span><span class="sxs-lookup"><span data-stu-id="cffb8-125">If you need toomirror between Kafka clusters in different networks, there are hello following additional considerations:</span></span>

* <span data-ttu-id="cffb8-126">**Gateways**: Hallo-netwerken kunnen toocommunicate op Hallo TCPIP niveau zijn.</span><span class="sxs-lookup"><span data-stu-id="cffb8-126">**Gateways**: hello networks must be able toocommunicate at hello TCPIP level.</span></span>

* <span data-ttu-id="cffb8-127">**Naamomzetting**: Hallo Kafka-clusters in elk netwerk moet kunnen tooconnect tooeach andere met behulp van hostnamen.</span><span class="sxs-lookup"><span data-stu-id="cffb8-127">**Name resolution**: hello Kafka clusters in each network must be able tooconnect tooeach other by using hostnames.</span></span> <span data-ttu-id="cffb8-128">Hiervoor moet mogelijk een Domain Name System (DNS)-server in elk netwerk dat is geconfigureerd tooforward aanvragen toohello andere netwerken.</span><span class="sxs-lookup"><span data-stu-id="cffb8-128">This may require a Domain Name System (DNS) server in each network that is configured tooforward requests toohello other networks.</span></span>

    <span data-ttu-id="cffb8-129">Bij het maken van een virtueel netwerk van Azure, in plaats van automatische DNS opgegeven Hallo met Hallo netwerk, moet u een aangepaste DNS-server en Hallo IP-adres voor Hallo-server.</span><span class="sxs-lookup"><span data-stu-id="cffb8-129">When creating an Azure Virtual Network, instead of using hello automatic DNS provided with hello network, you must specify a custom DNS server and hello IP address for hello server.</span></span> <span data-ttu-id="cffb8-130">Na Hallo die virtueel netwerk is gemaakt, moet u vervolgens maken een Azure-virtuele Machine die wordt gebruikt dat IP-adres, en vervolgens installeren en configureren van DNS-software op deze.</span><span class="sxs-lookup"><span data-stu-id="cffb8-130">After hello Virtual Network has been created, you must then create an Azure Virtual Machine that uses that IP address, then install and configure DNS software on it.</span></span>

    > [!WARNING]
    > <span data-ttu-id="cffb8-131">Maak en configureer Hallo aangepaste DNS-server voordat u HDInsight installeert in Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="cffb8-131">Create and configure hello custom DNS server before installing HDInsight into hello Virtual Network.</span></span> <span data-ttu-id="cffb8-132">Er is geen aanvullende configuratie vereist voor HDInsight toouse Hallo DNS-server is geconfigureerd voor Hallo virtueel netwerk.</span><span class="sxs-lookup"><span data-stu-id="cffb8-132">There is no additional configuration required for HDInsight toouse hello DNS server configured for hello Virtual Network.</span></span>

<span data-ttu-id="cffb8-133">Zie voor meer informatie over het verbinden van twee virtuele netwerken van Azure [een VNet-naar-VNet-verbinding configureren](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="cffb8-133">For more information on connecting two Azure Virtual Networks, see [Configure a VNet-to-VNet connection](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

## <a name="create-kafka-clusters"></a><span data-ttu-id="cffb8-134">Kafka-clusters maken</span><span class="sxs-lookup"><span data-stu-id="cffb8-134">Create Kafka clusters</span></span>

<span data-ttu-id="cffb8-135">U kunt een virtuele Azure-netwerk maken en handmatig Kafka-clusters, zijn maar er eenvoudiger toouse een Azure Resource Manager-sjabloon.</span><span class="sxs-lookup"><span data-stu-id="cffb8-135">While you can create an Azure virtual network and Kafka clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="cffb8-136">Gebruik Hallo volgende stap toodeploy een Azure-netwerk en twee Kafka clusters tooyour Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="cffb8-136">Use hello following steps toodeploy an Azure virtual network and two Kafka clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="cffb8-137">Hallo na de knop toosign in tooAzure en open Hallo-sjabloon in hello Azure-portal gebruiken.</span><span class="sxs-lookup"><span data-stu-id="cffb8-137">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    <span data-ttu-id="cffb8-138">Hello Azure Resource Manager-sjabloon bevindt zich op **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="cffb8-138">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="cffb8-139">de beschikbaarheid van de tooguarantee van Kafka op HDInsight, uw cluster moet ten minste drie worker-knooppunten bevatten.</span><span class="sxs-lookup"><span data-stu-id="cffb8-139">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="cffb8-140">Deze sjabloon maakt een Kafka-cluster dat drie worker-knooppunten bevat.</span><span class="sxs-lookup"><span data-stu-id="cffb8-140">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="cffb8-141">Gebruik Hallo informatie toopopulate Hallo vermeldingen op Hallo volgen **aangepaste implementatie** blade:</span><span class="sxs-lookup"><span data-stu-id="cffb8-141">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
    
    ![Aangepaste HDInsight-implementatie](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * <span data-ttu-id="cffb8-143">**Resourcegroep**: Maak een groep of een bestaande set selecteren.</span><span class="sxs-lookup"><span data-stu-id="cffb8-143">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="cffb8-144">Deze groep bevat Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="cffb8-144">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="cffb8-145">**Locatie**: Selecteer een locatie geografisch sluiten tooyou.</span><span class="sxs-lookup"><span data-stu-id="cffb8-145">**Location**: Select a location geographically close tooyou.</span></span>
     
    * <span data-ttu-id="cffb8-146">**Clusternaam baseren**: deze waarde wordt gebruikt als basisnaam van Hallo voor Hallo Kafka-clusters.</span><span class="sxs-lookup"><span data-stu-id="cffb8-146">**Base Cluster Name**: This value is used as hello base name for hello Kafka clusters.</span></span> <span data-ttu-id="cffb8-147">Bijvoorbeeld, voeren **hdi** wordt gemaakt met de naam clusters **bron hdi** en **dest hdi**.</span><span class="sxs-lookup"><span data-stu-id="cffb8-147">For example, entering **hdi** creates clusters named **source-hdi** and **dest-hdi**.</span></span>

    * <span data-ttu-id="cffb8-148">**Aanmeldingsnaam van gebruiker cluster**: Hallo beheerder gebruikersnaam op voor het Hallo-bron- en doelserver Kafka-clusters.</span><span class="sxs-lookup"><span data-stu-id="cffb8-148">**Cluster Login User Name**: hello admin user name for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="cffb8-149">**Aanmeldingswachtwoord cluster**: Hallo beheerderswachtwoord voor het Hallo-bron- en doelserver Kafka-clusters.</span><span class="sxs-lookup"><span data-stu-id="cffb8-149">**Cluster Login Password**: hello admin user password for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="cffb8-150">**SSH-gebruikersnaam**: Hallo SSH gebruiker toocreate voor Hallo bron- en doelserver Kafka-clusters.</span><span class="sxs-lookup"><span data-stu-id="cffb8-150">**SSH User Name**: hello SSH user toocreate for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="cffb8-151">**SSH-wachtwoord**: Hallo-wachtwoord voor Hallo SSH-gebruiker voor het Hallo-bron- en doelserver Kafka-clusters.</span><span class="sxs-lookup"><span data-stu-id="cffb8-151">**SSH Password**: hello password for hello SSH user for hello source and destination Kafka clusters.</span></span>

3. <span data-ttu-id="cffb8-152">Lees Hallo **voorwaarden en bepalingen**, en selecteer vervolgens **ik ga akkoord toohello voorwaarden bovengenoemde**.</span><span class="sxs-lookup"><span data-stu-id="cffb8-152">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="cffb8-153">Controleer ten slotte **pincode toodashboard** en selecteer vervolgens **aankoop**.</span><span class="sxs-lookup"><span data-stu-id="cffb8-153">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="cffb8-154">Het duurt ongeveer 20 minuten toocreate Hallo-clusters.</span><span class="sxs-lookup"><span data-stu-id="cffb8-154">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="cffb8-155">Zodra het Hallo-resources zijn gemaakt, bent u omgeleide tooa blade voor de resourcegroep Hallo Hallo clusters en webdashboard met.</span><span class="sxs-lookup"><span data-stu-id="cffb8-155">Once hello resources have been created, you are redirected tooa blade for hello resource group that contains hello clusters and web dashboard.</span></span>

![Resourcegroepblade voor Hallo vnet en clusters](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="cffb8-157">Merk op dat de namen van HDInsight-clusters Hallo Hallo zijn **bron BASENAME** en **dest BASENAME**, waarbij BASENAME Hallo-naam die u hebt opgegeven toohello sjabloon.</span><span class="sxs-lookup"><span data-stu-id="cffb8-157">Notice that hello names of hello HDInsight clusters are **source-BASENAME** and **dest-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="cffb8-158">U deze namen in latere stappen gebruiken om verbinding te maken van clusters toohello.</span><span class="sxs-lookup"><span data-stu-id="cffb8-158">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="create-topics"></a><span data-ttu-id="cffb8-159">Help-onderwerpen maken</span><span class="sxs-lookup"><span data-stu-id="cffb8-159">Create topics</span></span>

1. <span data-ttu-id="cffb8-160">Verbinding maken met toohello **bron** cluster via SSH:</span><span class="sxs-lookup"><span data-stu-id="cffb8-160">Connect toohello **source** cluster using SSH:</span></span>

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="cffb8-161">Vervang **sshuser** met Hallo SSH-gebruikersnaam gebruikt bij het Hallo-cluster maken.</span><span class="sxs-lookup"><span data-stu-id="cffb8-161">Replace **sshuser** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="cffb8-162">Vervang **BASENAME** met Hallo basisnaam gebruikt bij het Hallo-cluster maken.</span><span class="sxs-lookup"><span data-stu-id="cffb8-162">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

    <span data-ttu-id="cffb8-163">Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.</span><span class="sxs-lookup"><span data-stu-id="cffb8-163">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="cffb8-164">Gebruik Hallo volgende toofind hello Zookeeper hosts voor broncluster Hallo-opdrachten:</span><span class="sxs-lookup"><span data-stu-id="cffb8-164">Use hello following commands toofind hello Zookeeper hosts for hello source cluster:</span></span>

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get hello zookeeper hosts for hello source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    
    Replace `$PASSWORD` with hello password for hello cluster.

    Replace `$CLUSTERNAME` with hello name of hello source cluster.

3. toocreate a topic named `testtopic`, use hello following command:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. <span data-ttu-id="cffb8-165">Gebruik Hallo opdracht tooverify die Hallo onderwerp te volgen is gemaakt:</span><span class="sxs-lookup"><span data-stu-id="cffb8-165">Use hello following command tooverify that hello topic was created:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="cffb8-166">Hallo-antwoord bevat `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="cffb8-166">hello response contains `testtopic`.</span></span>

4. <span data-ttu-id="cffb8-167">Gebruik Hallo tooview hello Zookeeper informatie over de host voor deze volgen (Hallo **bron**) cluster:</span><span class="sxs-lookup"><span data-stu-id="cffb8-167">Use hello following tooview hello Zookeeper host information for this (hello **source**) cluster:</span></span>

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="cffb8-168">Hiermee wordt informatie vergelijkbare toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="cffb8-168">This returns information similar toohello following text:</span></span>

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    <span data-ttu-id="cffb8-169">Deze gegevens worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="cffb8-169">Save this information.</span></span> <span data-ttu-id="cffb8-170">Het wordt gebruikt in de volgende sectie Hallo.</span><span class="sxs-lookup"><span data-stu-id="cffb8-170">It is used in hello next section.</span></span>

## <a name="configure-mirroring"></a><span data-ttu-id="cffb8-171">Configureer het spiegelen</span><span class="sxs-lookup"><span data-stu-id="cffb8-171">Configure mirroring</span></span>

1. <span data-ttu-id="cffb8-172">Verbinding maken met toohello **bestemming** cluster met behulp van een andere SSH-sessie:</span><span class="sxs-lookup"><span data-stu-id="cffb8-172">Connect toohello **destination** cluster using a different SSH session:</span></span>

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="cffb8-173">Vervang **sshuser** met Hallo SSH-gebruikersnaam gebruikt bij het Hallo-cluster maken.</span><span class="sxs-lookup"><span data-stu-id="cffb8-173">Replace **sshuser** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="cffb8-174">Vervang **BASENAME** met Hallo basisnaam gebruikt bij het Hallo-cluster maken.</span><span class="sxs-lookup"><span data-stu-id="cffb8-174">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

    <span data-ttu-id="cffb8-175">Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.</span><span class="sxs-lookup"><span data-stu-id="cffb8-175">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="cffb8-176">Gebruik Hallo volgende opdracht toocreate een `consumer.properties` -bestand dat wordt beschreven hoe toocommunicate Hello **bron** cluster:</span><span class="sxs-lookup"><span data-stu-id="cffb8-176">Use hello following command toocreate a `consumer.properties` file that describes how toocommunicate with hello **source** cluster:</span></span>

    ```bash
    nano consumer.properties
    ```

    <span data-ttu-id="cffb8-177">Gebruik Hallo na de tekst hello inhoud Hallo `consumer.properties` bestand:</span><span class="sxs-lookup"><span data-stu-id="cffb8-177">Use hello following text as hello contents of hello `consumer.properties` file:</span></span>

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    <span data-ttu-id="cffb8-178">Vervang **SOURCE_ZKHOSTS** Hello Zookeeper fungeert als host voor gegevens van Hallo **bron** cluster.</span><span class="sxs-lookup"><span data-stu-id="cffb8-178">Replace **SOURCE_ZKHOSTS** with hello Zookeeper hosts information from hello **source** cluster.</span></span>

    <span data-ttu-id="cffb8-179">Dit bestand wordt Hallo consumer informatie toouse beschreven bij het lezen van Hallo bron Kafka-cluster.</span><span class="sxs-lookup"><span data-stu-id="cffb8-179">This file describes hello consumer information toouse when reading from hello source Kafka cluster.</span></span> <span data-ttu-id="cffb8-180">Zie voor meer informatie consumer-configuratie [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) op kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="cffb8-180">For more information consumer configuration, see [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) at kafka.apache.org.</span></span>

    <span data-ttu-id="cffb8-181">Gebruik-bestand Hallo toosave **Ctrl + X**, **Y**, en vervolgens **Enter**.</span><span class="sxs-lookup"><span data-stu-id="cffb8-181">toosave hello file, use **Ctrl + X**, **Y**, and then **Enter**.</span></span>

3. <span data-ttu-id="cffb8-182">Voordat u configureert Hallo producent die communiceert met het doelcluster hello, u moet Hallo broker hosts vinden voor Hallo **bestemming** cluster.</span><span class="sxs-lookup"><span data-stu-id="cffb8-182">Before configuring hello producer that communicates with hello destination cluster, you must find hello broker hosts for hello **destination** cluster.</span></span> <span data-ttu-id="cffb8-183">Hallo opdrachten tooretrieve na deze informatie gebruiken:</span><span class="sxs-lookup"><span data-stu-id="cffb8-183">Use hello following commands tooretrieve this information:</span></span>

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    <span data-ttu-id="cffb8-184">Vervang `$PASSWORD` met Hallo aanmeldingswachtwoord account (admin) voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="cffb8-184">Replace `$PASSWORD` with hello login account (admin) password for hello cluster.</span></span>

    <span data-ttu-id="cffb8-185">Vervang `$CLUSTERNAME` met de naam van het doelcluster Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="cffb8-185">Replace `$CLUSTERNAME` with hello name of hello destination cluster.</span></span>

    <span data-ttu-id="cffb8-186">Deze opdrachten retourneren informatie vergelijkbare toohello volgende:</span><span class="sxs-lookup"><span data-stu-id="cffb8-186">These commands return information similar toohello following:</span></span>

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. <span data-ttu-id="cffb8-187">Gebruik Hallo toocreate na een `producer.properties` -bestand dat wordt beschreven hoe toocommunicate Hello **bestemming** cluster:</span><span class="sxs-lookup"><span data-stu-id="cffb8-187">Use hello following toocreate a `producer.properties` file that describes how toocommunicate with hello **destination** cluster:</span></span>

    ```bash
    nano producer.properties
    ```

    <span data-ttu-id="cffb8-188">Gebruik Hallo na de tekst hello inhoud Hallo `producer.properties` bestand:</span><span class="sxs-lookup"><span data-stu-id="cffb8-188">Use hello following text as hello contents of hello `producer.properties` file:</span></span>

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    <span data-ttu-id="cffb8-189">Vervang **DEST_BROKERS** met Hallo broker informatie uit de vorige stap Hallo.</span><span class="sxs-lookup"><span data-stu-id="cffb8-189">Replace **DEST_BROKERS** with hello broker information from hello previous step.</span></span>

    <span data-ttu-id="cffb8-190">Zie voor meer informatie producent configuratie, [producent Configs](https://kafka.apache.org/documentation#producerconfigs) op kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="cffb8-190">For more information producer configuration, see [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) at kafka.apache.org.</span></span>

## <a name="start-mirrormaker"></a><span data-ttu-id="cffb8-191">MirrorMaker starten</span><span class="sxs-lookup"><span data-stu-id="cffb8-191">Start MirrorMaker</span></span>

1. <span data-ttu-id="cffb8-192">Van Hallo SSH-verbinding toohello **bestemming** cluster, Hallo opdracht toostart hello MirrorMaker proces volgende gebruiken:</span><span class="sxs-lookup"><span data-stu-id="cffb8-192">From hello SSH connection toohello **destination** cluster, use hello following command toostart hello MirrorMaker process:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    <span data-ttu-id="cffb8-193">in dit voorbeeld gebruikt Hallo-parameters zijn:</span><span class="sxs-lookup"><span data-stu-id="cffb8-193">hello parameters used in this example are:</span></span>

    * <span data-ttu-id="cffb8-194">**--consumer.config**: Hiermee geeft u Hallo-bestand dat de consument eigenschappen bevat.</span><span class="sxs-lookup"><span data-stu-id="cffb8-194">**--consumer.config**: Specifies hello file that contains consumer properties.</span></span> <span data-ttu-id="cffb8-195">Deze eigenschappen zijn gebruikte toocreate een consumer die uit Hallo leest *bron* Kafka-cluster.</span><span class="sxs-lookup"><span data-stu-id="cffb8-195">These properties are used toocreate a consumer that reads from hello *source* Kafka cluster.</span></span>

    * <span data-ttu-id="cffb8-196">**--producer.config**: Hiermee geeft u Hallo-bestand dat de producent eigenschappen bevat.</span><span class="sxs-lookup"><span data-stu-id="cffb8-196">**--producer.config**: Specifies hello file that contains producer properties.</span></span> <span data-ttu-id="cffb8-197">Deze eigenschappen zijn gebruikte toocreate een producent die toohello schrijft *bestemming* Kafka-cluster.</span><span class="sxs-lookup"><span data-stu-id="cffb8-197">These properties are used toocreate a producer that writes toohello *destination* Kafka cluster.</span></span>

    * <span data-ttu-id="cffb8-198">**--geaccepteerde**: een lijst met onderwerpen die MirrorMaker van Hallo bron cluster toohello doel repliceert.</span><span class="sxs-lookup"><span data-stu-id="cffb8-198">**--whitelist**: A list of topics that MirrorMaker replicates from hello source cluster toohello destination.</span></span>

    * <span data-ttu-id="cffb8-199">**--num.streams**: aantal consumer threads toocreate Hallo.</span><span class="sxs-lookup"><span data-stu-id="cffb8-199">**--num.streams**: hello number of consumer threads toocreate.</span></span>

 <span data-ttu-id="cffb8-200">Bij het opstarten retourneert MirrorMaker informatie vergelijkbare toohello volgende tekst:</span><span class="sxs-lookup"><span data-stu-id="cffb8-200">On startup, MirrorMaker returns information similar toohello following text:</span></span>

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. <span data-ttu-id="cffb8-201">Van Hallo SSH-verbinding toohello **bron** cluster, gebruikt u Hallo opdracht toostart producent te volgen en verzenden van berichten toohello onderwerp:</span><span class="sxs-lookup"><span data-stu-id="cffb8-201">From hello SSH connection toohello **source** cluster, use hello following command toostart a producer and send messages toohello topic:</span></span>

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    <span data-ttu-id="cffb8-202">Vervang `$PASSWORD` met hello (admin) aanmeldingswachtwoord voor Hallo broncluster.</span><span class="sxs-lookup"><span data-stu-id="cffb8-202">Replace `$PASSWORD` with hello login (admin) password for hello source cluster.</span></span>

    <span data-ttu-id="cffb8-203">Vervang `$CLUSTERNAME` met de naam van het broncluster Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="cffb8-203">Replace `$CLUSTERNAME` with hello name of hello source cluster.</span></span>

     <span data-ttu-id="cffb8-204">Wanneer u bij een lege regel met een cursor aankomt, typt u in een paar tekstberichten.</span><span class="sxs-lookup"><span data-stu-id="cffb8-204">When you arrive at a blank line with a cursor, type in a few text messages.</span></span> <span data-ttu-id="cffb8-205">Dit onderwerp toohello worden verzonden op Hallo **bron** cluster.</span><span class="sxs-lookup"><span data-stu-id="cffb8-205">These are sent toohello topic on hello **source** cluster.</span></span> <span data-ttu-id="cffb8-206">Wanneer u klaar bent, gebruikt u **Ctrl + c drukken** tooend Hallo producent proces.</span><span class="sxs-lookup"><span data-stu-id="cffb8-206">When done, use **Ctrl + C** tooend hello producer process.</span></span>

3. <span data-ttu-id="cffb8-207">Van Hallo SSH-verbinding toohello **bestemming** cluster, gebruikt u **Ctrl + c drukken** tooend hello MirrorMaker proces.</span><span class="sxs-lookup"><span data-stu-id="cffb8-207">From hello SSH connection toohello **destination** cluster, use **Ctrl + C** tooend hello MirrorMaker process.</span></span> <span data-ttu-id="cffb8-208">Vervolgens gebruik Hallo deze tooverify die Hallo opdrachten `testtopic` onderwerp is gemaakt en die gegevens in Hallo onderwerp gerepliceerde toothis mirror is:</span><span class="sxs-lookup"><span data-stu-id="cffb8-208">Then use hello following commands tooverify that hello `testtopic` topic was created, and that data in hello topic was replicated toothis mirror:</span></span>

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    <span data-ttu-id="cffb8-209">Vervang `$PASSWORD` met hello (admin) aanmeldingswachtwoord voor Hallo doelcluster.</span><span class="sxs-lookup"><span data-stu-id="cffb8-209">Replace `$PASSWORD` with hello login (admin) password for hello destination cluster.</span></span>

    <span data-ttu-id="cffb8-210">Vervang `$CLUSTERNAME` met de naam van het doelcluster Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="cffb8-210">Replace `$CLUSTERNAME` with hello name of hello destination cluster.</span></span>

    <span data-ttu-id="cffb8-211">Hallo lijst met onderwerpen bevat nu `testtopic`, die wordt gemaakt wanneer MirrorMaster Hallo onderwerp uit Hallo bron cluster toohello doel weerspiegelt.</span><span class="sxs-lookup"><span data-stu-id="cffb8-211">hello list of topics now includes `testtopic`, which is created when MirrorMaster mirrors hello topic from hello source cluster toohello destination.</span></span> <span data-ttu-id="cffb8-212">Hallo-berichten die zijn opgehaald uit het Hallo-onderwerp zijn hetzelfde als ingevoerd in de broncluster Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="cffb8-212">hello messages retrieved from hello topic are hello same as entered on hello source cluster.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="cffb8-213">Hallo-cluster verwijderen</span><span class="sxs-lookup"><span data-stu-id="cffb8-213">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="cffb8-214">Aangezien Hallo stappen in dit document beide maken clusters in dezelfde Azure-resourcegroep hello, kunt u de resourcegroep Hallo in hello Azure-portal verwijderen.</span><span class="sxs-lookup"><span data-stu-id="cffb8-214">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="cffb8-215">Verwijderen van het Hallo-resourcegroep Hiermee verwijdert u alle resources die zijn gemaakt op basis van dit document, hello Azure Virtual Network en storage-account door Hallo clusters worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="cffb8-215">Deleting hello resource group removes all resources created by following this document, hello Azure Virtual Network, and storage account used by hello clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cffb8-216">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cffb8-216">Next Steps</span></span>

<span data-ttu-id="cffb8-217">In dit document hebt u geleerd hoe toouse MirrorMaker toocreate een replica van een Kafka-cluster.</span><span class="sxs-lookup"><span data-stu-id="cffb8-217">In this document, you learned how toouse MirrorMaker toocreate a replica of a Kafka cluster.</span></span> <span data-ttu-id="cffb8-218">Hallo toodiscover koppelingen volgen andere manieren toowork met Kafka gebruiken:</span><span class="sxs-lookup"><span data-stu-id="cffb8-218">Use hello following links toodiscover other ways toowork with Kafka:</span></span>

* <span data-ttu-id="cffb8-219">[Apache Kafka MirrorMaker documentatie](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) op cwiki.apache.org.</span><span class="sxs-lookup"><span data-stu-id="cffb8-219">[Apache Kafka MirrorMaker documentation](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) at cwiki.apache.org.</span></span>
* [<span data-ttu-id="cffb8-220">Aan de slag met Apache Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="cffb8-220">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* [<span data-ttu-id="cffb8-221">Apache Spark gebruiken met Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="cffb8-221">Use Apache Spark with Kafka on HDInsight</span></span>](hdinsight-apache-spark-with-kafka.md)
* [<span data-ttu-id="cffb8-222">Apache Storm gebruiken met Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="cffb8-222">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="cffb8-223">TooKafka verbinding via een virtueel Azure-netwerk</span><span class="sxs-lookup"><span data-stu-id="cffb8-223">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
