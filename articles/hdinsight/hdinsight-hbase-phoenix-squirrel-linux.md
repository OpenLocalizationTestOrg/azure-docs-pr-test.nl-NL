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
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a>Apache Phoenix gebruiken met HBase op basis van Linux-clusters in HDInsight
Meer informatie over hoe toouse [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, en hoe toouse SQLLine. Zie voor meer informatie over Phoenix [Phoenix in 15 minuten of minder](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html). Zie voor Hallo Phoenix grammatica, [Phoenix grammatica](http://phoenix.apache.org/language/index.html).

> [!NOTE]
> Zie voor Hallo Phoenix versie-informatie in HDInsight, [wat is er nieuw in Hallo Hadoop-clusterversies geleverd door HDInsight?](hdinsight-component-versioning.md).
>
>

## <a name="use-sqlline"></a>Gebruik SQLLine
[SQLLine](http://sqlline.sourceforge.net/) is een opdrachtregelprogramma tooexecute SQL.

### <a name="prerequisites"></a>Vereisten
Voordat u SQLLine gebruiken kunt, moet u de volgende Hallo hebben:

* **Een HBase-cluster in HDInsight**. Voor informatie over het inrichten van HBase-cluster, Zie [aan de slag met Apache HBase in HDInsight][hdinsight-hbase-get-started].
* **Verbinding maken met HBase-cluster via remote desktop protocol Hallo toohello**. Zie voor instructies [beheren Hadoop-clusters in HDInsight met behulp van Azure-portal Hallo][hdinsight-manage-portal].

Wanneer u verbinding tooan HBase-cluster maakt, moet u tooconnect tooone Hallo Zookeepers. Elke HDInsight-cluster heeft drie Zookeepers.

**toofind uit Hallo Zookeeper-hostnaam**

1. Ambari openen door te bladeren**https://<ClusterName>. azurehdinsight.net**.
2. Hallo HTTP (cluster) toologin van gebruikersnaam en wachtwoord invoeren.
3. Klik op **ZooKeeper** in het linkermenu Hallo. Ziet u drie **ZooKeeper Server** vermeld.
4. Klik op een Hallo **ZooKeeper Server** vermeld. Hallo zoeken op Hallo samenvattingsvenster, **hostnaam**. Lijkt te*zk1 jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.

**toouse SQLLine**

1. Toohello-cluster via SSH verbinding. Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

2. Voer vanuit SSH Hallo opdrachten toorun SQLLine te volgen:

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. Voer Hallo opdrachten toocreate na een HBase-tabel en voeg enkele gegeven in:

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

Zie voor meer informatie [SQLLine handmatige](http://sqlline.sourceforge.net/#manual) en [Phoenix grammatica](http://phoenix.apache.org/language/index.html).

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd hoe toouse Apache Phoenix in HDInsight.  toolearn meer, Zie:

* [Overzicht van HDInsight HBase][hdinsight-hbase-overview]: HBase is een Apache, open-source NoSQL-database op basis van Hadoop. HBase biedt willekeurige toegang en een sterke consistentie voor grote hoeveelheden ongestructureerde en semigestructureerde gegevens.
* [HBase-clusters op Azure Virtual Network inrichten][hdinsight-hbase-provision-vnet]: aan de integratie van virtueel netwerk, HBase-clusters geïmplementeerde toohello virtuele netwerk als uw toepassingen zodat kunnen worden dat toepassingen met communiceren kunnen Rechtstreeks HBase.
* [Configureren van replicatie van HBase in HDInsight](hdinsight-hbase-replication.md): meer informatie over hoe tooconfigure HBase-replicatie tussen twee Azure-datacenters.
* [Twitter-gevoel met HBase in HDInsight analyseren][hbase-twitter-sentiment]: meer informatie over hoe toodo realtime [gevoel analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) van big data met behulp van HBase in een Hadoop-cluster in HDInsight.

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
