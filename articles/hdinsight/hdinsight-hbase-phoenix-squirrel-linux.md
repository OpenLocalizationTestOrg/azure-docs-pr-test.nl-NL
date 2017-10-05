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
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a>Apache Phoenix gebruiken met HBase op basis van Linux-clusters in HDInsight
Informatie over het gebruik [Apache Phoenix](http://phoenix.apache.org/) in HDInsight en het gebruik van SQLLine. Zie voor meer informatie over Phoenix [Phoenix in 15 minuten of minder](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html). Zie voor de grammatica Phoenix [Phoenix grammatica](http://phoenix.apache.org/language/index.html).

> [!NOTE]
> Zie voor de versie-informatie voor Phoenix in HDInsight, [wat is er nieuw in de Hadoop-clusterversies geleverd door HDInsight?](hdinsight-component-versioning.md).
>
>

## <a name="use-sqlline"></a>Gebruik SQLLine
[SQLLine](http://sqlline.sourceforge.net/) is een opdrachtregelprogramma SQL uitvoeren.

### <a name="prerequisites"></a>Vereisten
Voordat u SQLLine gebruiken kunt, moet u het volgende hebben:

* **Een HBase-cluster in HDInsight**. Voor informatie over het inrichten van HBase-cluster, Zie [aan de slag met Apache HBase in HDInsight][hdinsight-hbase-get-started].
* **Verbinding maken met de HBase-cluster via remote desktop protocol**. Zie voor instructies [beheren Hadoop-clusters in HDInsight met behulp van de Azure-portal][hdinsight-manage-portal].

Wanneer u verbinding met een HBase-cluster maakt, moet u verbinding maken met een van de Zookeepers. Elke HDInsight-cluster heeft drie Zookeepers.

**Om erachter te komen de Zookeeper-hostnaam**

1. Ambari openen door te bladeren naar **https://<ClusterName>. azurehdinsight.net**.
2. HTTP (cluster) gebruikersnaam en wachtwoord invoeren om aan te melden.
3. Klik op **ZooKeeper** in het menu links. Ziet u drie **ZooKeeper Server** vermeld.
4. Klik op een van de **ZooKeeper Server** vermeld. Zoek op het samenvattingsvenster de **hostnaam**. Het is vergelijkbaar met *zk1 jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.

**SQLLine gebruiken**

1. Verbinding maken met het cluster via SSH. Zie [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor meer informatie.

2. Voer de volgende opdrachten om uit te voeren SQLLine uit in SSH:

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. Voer de volgende opdrachten om een HBase-tabel te maken en voeg enkele gegeven in:

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

Zie voor meer informatie [SQLLine handmatige](http://sqlline.sourceforge.net/#manual) en [Phoenix grammatica](http://phoenix.apache.org/language/index.html).

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd hoe u van Apache Phoenix in HDInsight.  Voor meer informatie zie:

* [Overzicht van HDInsight HBase][hdinsight-hbase-overview]: HBase is een Apache, open-source NoSQL-database op basis van Hadoop. HBase biedt willekeurige toegang en een sterke consistentie voor grote hoeveelheden ongestructureerde en semigestructureerde gegevens.
* [HBase-clusters op Azure Virtual Network inrichten][hdinsight-hbase-provision-vnet]: door de integratie van virtueel netwerk, HBase-clusters kunnen worden geïmplementeerd op hetzelfde virtuele netwerk als uw toepassingen zodat toepassingen met HBase communiceren kunnen rechtstreeks.
* [Configureren van replicatie van HBase in HDInsight](hdinsight-hbase-replication.md): informatie over het configureren van HBase-replicatie tussen twee Azure-datacenters.
* [Twitter-gevoel met HBase in HDInsight analyseren][hbase-twitter-sentiment]: meer informatie over hoe u realtime [gevoel analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) van big data met behulp van HBase in een Hadoop-cluster in HDInsight.

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
