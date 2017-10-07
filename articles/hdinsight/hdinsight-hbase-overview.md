---
title: aaaWhat is HBase in Azure HDInsight? | Microsoft Docs
description: Een inleiding tooApache HBase in HDInsight, een NoSQL-database is gebaseerd op Hadoop. Meer informatie over de toepassingsmogelijkheden en HBase tooother Hadoop-clusters vergelijken.
keywords: bigtable, nosql, wat is hbase, apache hbase, hbase, hbase-overzicht,
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: d2a76d53-133a-4849-a30c-88d9c794391c
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 0d28378d07b1a168e38748548578be11310d2228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hbase-in-hdinsight-a-nosql-database-that-provides-bigtable-like-capabilities-for-hadoop"></a>Wat is HBase in HDInsight: een NoSQL-database die op BigTable gelijkende mogelijkheden voor Hadoop levert
Apache HBase is een open-source NoSQL-database die is gebaseerd op Hadoop en die is gemodelleerd naar Google BigTable. HBase biedt willekeurige toegang en een sterke consistentie voor grote hoeveelheden ongestructureerde en semigestructureerde gegevens in een database zonder schema die is georganiseerd op basis van kolomfamilies.

Gegevens worden opgeslagen in het Hallo-rijen van een tabel en gegevens in een rij worden gegroepeerd per kolomfamilie. HBase is een database zonder schema in Hallo zin dat geen van beide kolommen als soort gegevens die zijn opgeslagen in deze Hallo Hallo moet toobe gedefinieerd voordat u ze gebruikt. Hallo open source code wordt lineair geschaald toohandle petabytes aan gegevens op duizenden knooppunten. Het kan zijn afhankelijk van gegevensredundantie, batchverwerking en andere functies die worden geboden door gedistribueerde toepassingen in Hallo Hadoop-ecosysteem.

## <a name="how-is-hbase-implemented-in-azure-hdinsight"></a>How wordt HBase geïmplementeerd in Azure HDInsight?
HDInsight HBase wordt aangeboden als een beheerd cluster dat is geïntegreerd in hello Azure-omgeving. Hallo-clusters zijn geconfigureerde toostore gegevens rechtstreeks in [Azure Storage](./hdinsight-hadoop-use-blob-storage.md) of [Azure Data Lake Store](./hdinsight-hadoop-use-data-lake-store.md), waarmee u lage latentie en verbeterde elasticiteit met betrekking tot prestatie- en kostenopties. Hierdoor kunnen klanten interactieve websites toobuild die werken met grote gegevenssets, toobuild-services die gegevens van sensor- en telemetriegegevens van miljoenen eindpunten en tooanalyze deze gegevens met Hadoop-taken. HBase en Hadoop vormen een goed startpunt voor big data-projecten in Azure. in het bijzonder ze ervoor zorgen dat realtime toepassingen toowork met grote gegevenssets.

Hallo HDInsight-implementatie maakt gebruik van Hallo uitbreidbare architectuur van HBase tooprovide automatische sharding van tabellen, sterke consistentie voor lees- en schrijfbewerkingen en automatische failover. De prestaties zijn verbeterd dankzij in-memory caching voor leesbewerkingen en streamen met een hoge gegevensdoorvoer voor schrijfbewerkingen. Een HBase-cluster kan worden gemaakt in het virtuele netwerk. Zie [HDInsight-clusters maken in Azure Virtual Network][hbase-provision-vnet] voor meer informatie.

## <a name="how-is-data-managed-in-hdinsight-hbase"></a>Hoe worden gegevens in HDInsight HBase beheerd?
Gegevens kunnen worden beheerd in HBase met behulp van Hallo `create`, `get`, `put`, en `scan` opdrachten uit Hallo HBase-shell. Gegevens toohello database worden geschreven met behulp van `put` en gelezen met `get`. Hallo `scan` opdracht gebruikte tooobtain gegevens uit meerdere rijen in een tabel is. Gegevens kunnen ook worden beheerd met behulp van Hallo HBase C# API, die een clientbibliotheek boven op Hallo HBase REST-API biedt. Er kan ook een query op de HBase-database worden uitgevoerd met Hive. Zie voor een inleiding toothese programming modellen, [aan de slag met HBase met Hadoop in HDInsight][hbase-get-started]. CO-processoren zijn ook beschikbaar is, waarmee gegevens worden verwerkt in Hallo knooppunten die host Hallo-database.

> [!NOTE]
> Thrift wordt niet ondersteund door HBase in HDInsight.
>

## <a name="scenarios-use-cases-for-hbase"></a>Scenario's: gebruiksvoorbeelden voor HBase
Hallo canonieke gebruiksvoorbeeld waarvoor bigtable (en door uitbreiding HBase) is gemaakt is zoeken op het web. Zoekmachines bouwen indexen die termen toohello webpagina's waarin deze worden toegewezen. Er zijn echter tal van andere gebruiksvoorbeeld waarvoor HBase geschikt is. Enkele daarvan worden gespecificeerd in deze sectie.

* Sleutel-waardearchief
  
    HBase kan worden gebruikt als een sleutel-waardearchief en is geschikt voor het beheren van berichtsystemen. Facebook gebruikt HBase voor het berichtensysteem. Daarnaast is HBase ideaal voor het opslaan en beheren van de communicatie via internet. WebTable gebruikt HBase toosearch voor en tabellen die zijn geëxtraheerd uit webpagina's te beheren.
* Sensorgegevens
  
    HBase is handig wanneer u gegevens wilt vastleggen die stapsgewijs uit diverse bronnen worden verzameld. Dit omvat sociale analyses, time series, het up-to-date houden van interactieve dashboards met trends en prestatiemeteritems en het beheren van auditlogboeksystemen. Voorbeelden zijn Bloomberg-traderterminal en Hallo Open Time Series Database (OpenTSDB) die worden opgeslagen en biedt toegang tot toometrics verzameld over de status Hallo van server-systemen.
* Realtime query
  
    [Phoenix](http://phoenix.apache.org/) is een SQL-query-engine voor Apache HBase. Deze is toegankelijk als een JDBC-stuurprogramma en maakt het uitvoeren van query's en beheren van HBase-tabellen SQL mogelijk.
* HBase als een platform
  
    Toepassingen kunnen worden uitgevoerd in HBase door HBase te gebruiken als gegevensopslag. Voorbeelden hiervan zijn Phoenix, OpenTSDB, Kiji en Titan. Toepassingen kunnen ook worden geïntegreerd met HBase. Voorbeelden hiervan zijn Hive, Pig, Solr, Storm, Flume, Impala, Spark, Ganglia en Drill.

## <a name="next-steps"></a>Volgende stappen
* [Aan de slag met HBase en Hadoop in HDInsight][hbase-get-started]
* [HDInsight-clusters maken in Azure Virtual Network][hbase-provision-vnet]
* [HBase-replicatie in HDInsight configureren](hdinsight-hbase-replication.md)
* [Het Twitter-gevoel met HBase in HDInsight analyseren][hbase-twitter-sentiment]
* [Maven toobuild Java-toepassingen die gebruikmaken van HBase met HDInsight (Hadoop) gebruiken][hbase-build-java-maven]

## <a name="see-also"></a>Zie ook
* [Apache HBase](https://hbase.apache.org/)
* [Bigtable: een gedistribueerd opslagsysteem voor gestructureerde gegevens](http://research.google.com/archive/bigtable.html)

[hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md

[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hbase-build-java-maven]: hdinsight-hbase-build-java-maven.md

[hdinsight-use-hive]: hdinsight-use-hive.md

[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md

[hbase-get-started]: http://azure.microsoft.com/documentation/articles/hdinsight-hbase-get-started/

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-management-portal]: https://portal.azure.com/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
