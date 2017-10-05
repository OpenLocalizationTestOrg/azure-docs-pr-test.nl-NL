---
title: Gebruik van Apache Phoenix en SQuirreL met HBase - Azure HDInsight | Microsoft Docs
description: Informatie over het gebruik van Apache Phoenix in HDInsight en het installeren en configureren van SQuirreL op uw werkstation verbinding maken met een HBase-cluster in HDInsight.
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
ms.openlocfilehash: 13d17083bbe26fa9745ce4c5fef9f56859243c2e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="07134-103">Apache Phoenix gebruiken met HBase op basis van Linux-clusters in HDInsight</span><span class="sxs-lookup"><span data-stu-id="07134-103">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="07134-104">Informatie over het gebruik [Apache Phoenix](http://phoenix.apache.org/) in HDInsight en het gebruik van SQLLine.</span><span class="sxs-lookup"><span data-stu-id="07134-104">Learn how to use [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how to use SQLLine.</span></span> <span data-ttu-id="07134-105">Zie voor meer informatie over Phoenix [Phoenix in 15 minuten of minder](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="07134-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="07134-106">Zie voor de grammatica Phoenix [Phoenix grammatica](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="07134-106">For the Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="07134-107">Zie voor de versie-informatie voor Phoenix in HDInsight, [wat is er nieuw in de Hadoop-clusterversies geleverd door HDInsight?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="07134-107">For the Phoenix version information in HDInsight, see [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="use-sqlline"></a><span data-ttu-id="07134-108">Gebruik SQLLine</span><span class="sxs-lookup"><span data-stu-id="07134-108">Use SQLLine</span></span>
<span data-ttu-id="07134-109">[SQLLine](http://sqlline.sourceforge.net/) is een opdrachtregelprogramma SQL uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="07134-109">[SQLLine](http://sqlline.sourceforge.net/) is a command-line utility to execute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="07134-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="07134-110">Prerequisites</span></span>
<span data-ttu-id="07134-111">Voordat u SQLLine gebruiken kunt, moet u het volgende hebben:</span><span class="sxs-lookup"><span data-stu-id="07134-111">Before you can use SQLLine, you must have the following:</span></span>

* <span data-ttu-id="07134-112">**Een HBase-cluster in HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="07134-112">**An HBase cluster in HDInsight**.</span></span> <span data-ttu-id="07134-113">Voor informatie over het inrichten van HBase-cluster, Zie [aan de slag met Apache HBase in HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="07134-113">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="07134-114">**Verbinding maken met de HBase-cluster via remote desktop protocol**.</span><span class="sxs-lookup"><span data-stu-id="07134-114">**Connect to the HBase cluster via the remote desktop protocol**.</span></span> <span data-ttu-id="07134-115">Zie voor instructies [beheren Hadoop-clusters in HDInsight met behulp van de Azure-portal][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="07134-115">For instructions, see [Manage Hadoop clusters in HDInsight by using the Azure portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="07134-116">Wanneer u verbinding met een HBase-cluster maakt, moet u verbinding maken met een van de Zookeepers.</span><span class="sxs-lookup"><span data-stu-id="07134-116">When you connect to an HBase cluster, you need to connect to one of the Zookeepers.</span></span> <span data-ttu-id="07134-117">Elke HDInsight-cluster heeft drie Zookeepers.</span><span class="sxs-lookup"><span data-stu-id="07134-117">Each HDInsight cluster has three Zookeepers.</span></span>

<span data-ttu-id="07134-118">**Om erachter te komen de Zookeeper-hostnaam**</span><span class="sxs-lookup"><span data-stu-id="07134-118">**To find out the Zookeeper host name**</span></span>

1. <span data-ttu-id="07134-119">Ambari openen door te bladeren naar **https://<ClusterName>. azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="07134-119">Open Ambari by browsing to **https://<ClusterName>.azurehdinsight.net**.</span></span>
2. <span data-ttu-id="07134-120">HTTP (cluster) gebruikersnaam en wachtwoord invoeren om aan te melden.</span><span class="sxs-lookup"><span data-stu-id="07134-120">Enter the HTTP (cluster) username and password to login.</span></span>
3. <span data-ttu-id="07134-121">Klik op **ZooKeeper** in het menu links.</span><span class="sxs-lookup"><span data-stu-id="07134-121">Click **ZooKeeper** from the left menu.</span></span> <span data-ttu-id="07134-122">Ziet u drie **ZooKeeper Server** vermeld.</span><span class="sxs-lookup"><span data-stu-id="07134-122">You see three **ZooKeeper Server** listed.</span></span>
4. <span data-ttu-id="07134-123">Klik op een van de **ZooKeeper Server** vermeld.</span><span class="sxs-lookup"><span data-stu-id="07134-123">Click one of the **ZooKeeper Server** listed.</span></span> <span data-ttu-id="07134-124">Zoek op het samenvattingsvenster de **hostnaam**.</span><span class="sxs-lookup"><span data-stu-id="07134-124">On the Summary pane, find the **Hostname**.</span></span> <span data-ttu-id="07134-125">Het is vergelijkbaar met *zk1 jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="07134-125">It is similar to *zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span></span>

<span data-ttu-id="07134-126">**SQLLine gebruiken**</span><span class="sxs-lookup"><span data-stu-id="07134-126">**To use SQLLine**</span></span>

1. <span data-ttu-id="07134-127">Verbinding maken met het cluster via SSH.</span><span class="sxs-lookup"><span data-stu-id="07134-127">Connect to the cluster using SSH.</span></span> <span data-ttu-id="07134-128">Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="07134-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="07134-129">Voer de volgende opdrachten om uit te voeren SQLLine uit in SSH:</span><span class="sxs-lookup"><span data-stu-id="07134-129">From SSH, run the following commands to run SQLLine:</span></span>

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. <span data-ttu-id="07134-130">Voer de volgende opdrachten om een HBase-tabel te maken en voeg enkele gegeven in:</span><span class="sxs-lookup"><span data-stu-id="07134-130">Run the following commands to create a HBase table, and insert some data:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

<span data-ttu-id="07134-131">Zie voor meer informatie [SQLLine handmatige](http://sqlline.sourceforge.net/#manual) en [Phoenix grammatica](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="07134-131">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="07134-132">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="07134-132">Next steps</span></span>
<span data-ttu-id="07134-133">In dit artikel hebt u geleerd hoe u van Apache Phoenix in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="07134-133">In this article, you have learned how to use Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="07134-134">Voor meer informatie zie:</span><span class="sxs-lookup"><span data-stu-id="07134-134">To learn more, see:</span></span>

* <span data-ttu-id="07134-135">[Overzicht van HDInsight HBase][hdinsight-hbase-overview]: HBase is een Apache, open-source NoSQL-database op basis van Hadoop. HBase biedt willekeurige toegang en een sterke consistentie voor grote hoeveelheden ongestructureerde en semigestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="07134-135">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="07134-136">[HBase-clusters op Azure Virtual Network inrichten][hdinsight-hbase-provision-vnet]: door de integratie van virtueel netwerk, HBase-clusters kunnen worden geïmplementeerd op hetzelfde virtuele netwerk als uw toepassingen zodat toepassingen met HBase communiceren kunnen rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="07134-136">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="07134-137">[Configureren van replicatie van HBase in HDInsight](hdinsight-hbase-replication.md): informatie over het configureren van HBase-replicatie tussen twee Azure-datacenters.</span><span class="sxs-lookup"><span data-stu-id="07134-137">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how to configure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="07134-138">[Twitter-gevoel met HBase in HDInsight analyseren][hbase-twitter-sentiment]: meer informatie over hoe u realtime [gevoel analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) van big data met behulp van HBase in een Hadoop-cluster in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="07134-138">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how to do real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

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
