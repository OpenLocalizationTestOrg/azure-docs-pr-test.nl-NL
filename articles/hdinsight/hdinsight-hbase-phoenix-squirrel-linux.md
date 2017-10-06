---
title: aaaUse Apache Phoenix en SQuirreL met HBase - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse Apache Phoenix in HDInsight, en hoe tooinstall en SQuirreL configureren op uw werkstation tooconnect tooan HBase-cluster in HDInsight.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: cda0f33b-a2e8-494c-972f-ae0bb482b818
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/26/2017
ms.author: jgao
ms.openlocfilehash: a63e8c8212b7a992453ec94fa638ec3863a0ede3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="4fc05-103">Apache Phoenix gebruiken met HBase op basis van Linux-clusters in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4fc05-103">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="4fc05-104">Meer informatie over hoe toouse [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, en hoe toouse SQLLine.</span><span class="sxs-lookup"><span data-stu-id="4fc05-104">Learn how toouse [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how toouse SQLLine.</span></span> <span data-ttu-id="4fc05-105">Zie voor meer informatie over Phoenix [Phoenix in 15 minuten of minder](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="4fc05-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="4fc05-106">Zie voor Hallo Phoenix grammatica, [Phoenix grammatica](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="4fc05-106">For hello Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="4fc05-107">Zie voor Hallo Phoenix versie-informatie in HDInsight, [wat is er nieuw in Hallo Hadoop-clusterversies geleverd door HDInsight?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="4fc05-107">For hello Phoenix version information in HDInsight, see [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="use-sqlline"></a><span data-ttu-id="4fc05-108">Gebruik SQLLine</span><span class="sxs-lookup"><span data-stu-id="4fc05-108">Use SQLLine</span></span>
<span data-ttu-id="4fc05-109">[SQLLine](http://sqlline.sourceforge.net/) is een opdrachtregelprogramma tooexecute SQL.</span><span class="sxs-lookup"><span data-stu-id="4fc05-109">[SQLLine](http://sqlline.sourceforge.net/) is a command-line utility tooexecute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="4fc05-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="4fc05-110">Prerequisites</span></span>
<span data-ttu-id="4fc05-111">Voordat u SQLLine gebruiken kunt, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="4fc05-111">Before you can use SQLLine, you must have hello following:</span></span>

* <span data-ttu-id="4fc05-112">**Een HBase-cluster in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="4fc05-112">**An HBase cluster in HDInsight**.</span></span> <span data-ttu-id="4fc05-113">Voor informatie over het inrichten van HBase-cluster, Zie [aan de slag met Apache HBase in HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="4fc05-113">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="4fc05-114">**Verbinding maken met HBase-cluster via remote desktop protocol Hallo toohello**.</span><span class="sxs-lookup"><span data-stu-id="4fc05-114">**Connect toohello HBase cluster via hello remote desktop protocol**.</span></span> <span data-ttu-id="4fc05-115">Zie voor instructies [beheren Hadoop-clusters in HDInsight met behulp van Azure-portal Hallo][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="4fc05-115">For instructions, see [Manage Hadoop clusters in HDInsight by using hello Azure portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="4fc05-116">Wanneer u verbinding tooan HBase-cluster maakt, moet u tooconnect tooone Hallo Zookeepers.</span><span class="sxs-lookup"><span data-stu-id="4fc05-116">When you connect tooan HBase cluster, you need tooconnect tooone of hello Zookeepers.</span></span> <span data-ttu-id="4fc05-117">Elke HDInsight-cluster heeft drie Zookeepers.</span><span class="sxs-lookup"><span data-stu-id="4fc05-117">Each HDInsight cluster has three Zookeepers.</span></span>

<span data-ttu-id="4fc05-118">**toofind uit Hallo Zookeeper-hostnaam**</span><span class="sxs-lookup"><span data-stu-id="4fc05-118">**toofind out hello Zookeeper host name**</span></span>

1. <span data-ttu-id="4fc05-119">Ambari openen door te bladeren**https://<ClusterName>. azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="4fc05-119">Open Ambari by browsing too**https://<ClusterName>.azurehdinsight.net**.</span></span>
2. <span data-ttu-id="4fc05-120">Hallo HTTP (cluster) toologin van gebruikersnaam en wachtwoord invoeren.</span><span class="sxs-lookup"><span data-stu-id="4fc05-120">Enter hello HTTP (cluster) username and password toologin.</span></span>
3. <span data-ttu-id="4fc05-121">Klik op **ZooKeeper** in het linkermenu Hallo.</span><span class="sxs-lookup"><span data-stu-id="4fc05-121">Click **ZooKeeper** from hello left menu.</span></span> <span data-ttu-id="4fc05-122">Ziet u drie **ZooKeeper Server** vermeld.</span><span class="sxs-lookup"><span data-stu-id="4fc05-122">You see three **ZooKeeper Server** listed.</span></span>
4. <span data-ttu-id="4fc05-123">Klik op een Hallo **ZooKeeper Server** vermeld.</span><span class="sxs-lookup"><span data-stu-id="4fc05-123">Click one of hello **ZooKeeper Server** listed.</span></span> <span data-ttu-id="4fc05-124">Hallo zoeken op Hallo samenvattingsvenster, **hostnaam**.</span><span class="sxs-lookup"><span data-stu-id="4fc05-124">On hello Summary pane, find hello **Hostname**.</span></span> <span data-ttu-id="4fc05-125">Lijkt te*zk1 jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="4fc05-125">It is similar too*zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span></span>

<span data-ttu-id="4fc05-126">**toouse SQLLine**</span><span class="sxs-lookup"><span data-stu-id="4fc05-126">**toouse SQLLine**</span></span>

1. <span data-ttu-id="4fc05-127">Toohello-cluster via SSH verbinding.</span><span class="sxs-lookup"><span data-stu-id="4fc05-127">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="4fc05-128">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="4fc05-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="4fc05-129">Voer vanuit SSH Hallo opdrachten toorun SQLLine te volgen:</span><span class="sxs-lookup"><span data-stu-id="4fc05-129">From SSH, run hello following commands toorun SQLLine:</span></span>

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. <span data-ttu-id="4fc05-130">Voer Hallo opdrachten toocreate na een HBase-tabel en voeg enkele gegeven in:</span><span class="sxs-lookup"><span data-stu-id="4fc05-130">Run hello following commands toocreate a HBase table, and insert some data:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

<span data-ttu-id="4fc05-131">Zie voor meer informatie [SQLLine handmatige](http://sqlline.sourceforge.net/#manual) en [Phoenix grammatica](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="4fc05-131">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fc05-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4fc05-132">Next steps</span></span>
<span data-ttu-id="4fc05-133">In dit artikel hebt u geleerd hoe toouse Apache Phoenix in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4fc05-133">In this article, you have learned how toouse Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="4fc05-134">toolearn meer, Zie:</span><span class="sxs-lookup"><span data-stu-id="4fc05-134">toolearn more, see:</span></span>

* <span data-ttu-id="4fc05-135">[Overzicht van HDInsight HBase][hdinsight-hbase-overview]: HBase is een Apache, open-source NoSQL-database op basis van Hadoop. HBase biedt willekeurige toegang en een sterke consistentie voor grote hoeveelheden ongestructureerde en semigestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="4fc05-135">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="4fc05-136">[HBase-clusters op Azure Virtual Network inrichten][hdinsight-hbase-provision-vnet]: aan de integratie van virtueel netwerk, HBase-clusters geïmplementeerde toohello virtuele netwerk als uw toepassingen zodat kunnen worden dat toepassingen met communiceren kunnen Rechtstreeks HBase.</span><span class="sxs-lookup"><span data-stu-id="4fc05-136">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="4fc05-137">[Configureren van replicatie van HBase in HDInsight](hdinsight-hbase-replication.md): meer informatie over hoe tooconfigure HBase-replicatie tussen twee Azure-datacenters.</span><span class="sxs-lookup"><span data-stu-id="4fc05-137">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how tooconfigure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="4fc05-138">[Twitter-gevoel met HBase in HDInsight analyseren][hbase-twitter-sentiment]: meer informatie over hoe toodo realtime [gevoel analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) van big data met behulp van HBase in een Hadoop-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4fc05-138">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how toodo real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
