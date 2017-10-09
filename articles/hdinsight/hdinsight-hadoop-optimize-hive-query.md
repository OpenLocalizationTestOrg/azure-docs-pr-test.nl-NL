---
title: aaaOptimize Hive query's in Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toooptimize uw Hive query's voor Hadoop in HDInsight.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d6174c08-06aa-42ac-8e9b-8b8718d9978e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2016
ms.author: jgao
ms.openlocfilehash: d27f8100e1e9f4823040ff9f693e7b78d6192c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hive-queries-in-azure-hdinsight"></a>In Azure HDInsight Hive-query's optimaliseren

Hadoop-clusters zijn standaard niet geoptimaliseerd voor prestaties. In dit artikel bevat informatie over een aantal veelgebruikte optimalisatie methoden voor Hive prestaties die u tooyour query's kunt toepassen.

## <a name="scale-out-worker-nodes"></a>Worker-knooppunten uitbreiden

Vergroten van het aantal worker-knooppunten in een cluster Hallo kunt gebruikmaken van meer mappers en verkleiningstoestellen toobe parallel worden uitgevoerd. Er zijn twee manieren kunt u scale-out in HDInsight verhogen:

* Tijdens het Hallo inrichten, kunt u het aantal worker-knooppunten met hello Azure-portal, Azure PowerShell of platformoverschrijdende opdrachtregelinterface Hallo.  Zie [HDInsight-clusters maken](hdinsight-hadoop-provision-linux-clusters.md) voor meer informatie. Hallo volgende schermafbeelding ziet Hallo worker knooppuntconfiguratie op Hallo Azure-portal:
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* Op Hallo uitvoeringstijd, kunt u ook uitschalen een cluster zonder opnieuw te maken op een:

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

Zie voor meer informatie over Hallo verschillende virtuele machines die door HDInsight worden ondersteund, [HDInsight prijzen](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="enable-tez"></a>Inschakelen van Tez

[Apache Tez](http://hortonworks.com/hadoop/tez/) is een alternatieve uitvoering engine toohello MapReduce-engine:

![tez_1][image-hdi-optimize-hive-tez_1]

Tez is sneller omdat:

* **Omgeleid acyclische grafiek (DAG) worden uitgevoerd als een enkele taak in Hallo MapReduce-engine**. Hallo DAG is vereist voor elke set van mappers toobe gevolgd door een reeks verkleiningstoestellen. Dit zorgt ervoor dat meerdere MapReduce-taken toobe ingezet uit voor elke Hive-query. Tez heeft geen dergelijke beperking en complexe DAG kan worden verwerkt als een taak dus taak starten van de overhead te minimaliseren.
* **Onnodige schrijfbewerkingen voorkomt**. Vervaldatum toomultiple taken wordt ingezet voor Hallo dezelfde Hive-query in de uitvoer van elke taak Hallo-engine MapReduce Hallo tooHDFS voor tussenliggende gegevens geschreven. Aangezien Tez aantal taken voor elke Hive-query minimaliseert is kunnen tooavoid onnodige schrijven.
* **Vertragingen bij het opstarten minimaliseert**. Tez is beter kunnen toominimize opstarten vertraging door het aantal mappers toostart en ook verbeterde optimalisatie in de gehele moet hello te verminderen.
* **Containers hergebruikt**. Wanneer mogelijk Tez kunnen tooreuse containers tooensure die latentie vanwege wordt toostarting van containers verminderd.
* **Continue optimalisatietechnieken**. Optimalisatie is normaal uitgevoerd tijdens de compilatiefase. Maar er meer informatie over Hallo invoer beschikbaar is waarmee voor betere optimalisatie tijdens runtime. Tez maakt gebruik van doorlopende optimalisatietechnieken waardoor verdere toooptimize Hallo-plan in Hallo runtime-fase.

Zie voor meer informatie over deze begrippen [Apache TEZ](http://hortonworks.com/hadoop/tez/).

U kunt een Hive-query Tez ingeschakeld door Mining Hallo query met de onderstaande instelling voor Hallo aanbrengen:

    set hive.execution.engine=tez;

HDInsight-clusters op basis van Linux hebben Tez is standaard ingeschakeld.


## <a name="hive-partitioning"></a>Hive partitioneren

I/o-bewerking is Hallo belangrijke prestatieknelpunt voor het uitvoeren van Hive-query's. Hallo-prestaties kunnen worden verbeterd als Hallo hoeveelheid gegevens die moeten worden toobe gelezen kan worden verminderd. Hive-query's scan standaard volledige Hive-tabellen. Dit is ideaal voor query's zoals tabelscans. Maar voor query's die u alleen tooscan een kleine hoeveelheid gegevens (bijvoorbeeld, query's filteren hoeft), dit gedrag maakt onnodige overhead. Hive partitionering kunt Hive-query's tooaccess alleen Hallo benodigde hoeveelheid gegevens in de Hive-tabellen.

Hive partitioneren wordt geïmplementeerd door het opnieuw indelen van Hallo onbewerkte gegevens naar de nieuwe mappen met elke partitie hebben een eigen map - waarvoor Hallo partitie door Hallo gebruiker is gedefinieerd. Hallo volgende diagram ziet u een Hive-tabel op Hallo kolom partitioneren *jaar*. Een nieuwe map wordt gemaakt voor elk jaar.

![Partitioneren][image-hdi-optimize-hive-partitioning_1]

Enkele overwegingen partitionering:

* **Kan niet onder de partitie** -partitionering voor kolommen met slechts enkele waarden kan leiden tot enkele partities. Partitioneren op geslacht alleen maakt u bijvoorbeeld twee partities toobe (man en vrouwelijke) gemaakt, dus alleen Hallo de latentie te verminderen door een maximum van de helft.
* **Kan niet via partitie** : op Hallo van andere extreme, het maken van een partitie in een kolom met een unieke waarde (bijvoorbeeld userid) zorgt ervoor dat meerdere partities. Via partitie zorgt ervoor dat veel stress op Hallo cluster namenode omdat u toohandle Hallo groot aantal mappen.
* **Voorkomen dat gegevens scheeftrekken** -Kies uw te nemen partitionerende sleutel goed zodat alle partities zelfs grootte zijn. Een voorbeeld is een partitionerende op *status* kan ertoe leiden dat het aantal records onder Californië toobe Hallo bijna 30 x die Vermont vanwege toohello verschil in de populatie.

toocreate een partitietabel gebruiken Hallo *gepartitioneerd door* component:

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

Zodra Hallo gepartitioneerde tabel is gemaakt, kunt u het partitioneren van statische of dynamische partitionering maken.

* **Statische partitioneren** betekent dat er al gedeelde gegevens in Hallo betreffende mappen en vraagt u handmatig op basis van de maplocatie Hallo Hive-partities. Hallo volgende codefragment is een voorbeeld.
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* **Dynamische partitionering** betekent dat u wilt dat Hive toocreate partities automatisch voor u. Aangezien we Hallo partitioneren van tabel uit Hallo faseringstabel al hebt gemaakt, moeten we toodo toohello gepartitioneerde tabel invoegen is:
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

Zie voor meer informatie [gepartitioneerde tabellen](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).

## <a name="use-hello-orcfile-format"></a>Hallo ORCFile indeling gebruiken
Hive ondersteunt verschillende bestandsindelingen. Bijvoorbeeld:

* **Tekst**: dit is de standaardbestandsindeling Hallo en werkt samen met de meeste scenario's
* **Avro**: geschikt is voor interoperabiliteit scenario's
* **ORC/parketvloeren**: meest geschikt voor prestaties

De indeling van de ORC (geoptimaliseerd rij kolommen) is een zeer efficiënte manier toostore Hive-gegevens. Vergeleken tooother indelingen, ORC heeft Hallo volgende voordelen:

* ondersteuning voor complexe gegevenstypen zoals DateTime en complexe en semi-gestructureerde typen
* een too70% compressie
* elke 10.000 rijen, waardoor de rijen overgeslagen indexen
* een aanzienlijke daling van de runtime-uitvoering

tooenable ORC-indeling, eerst maakt u een tabel met Hallo component *opgeslagen als ORC*:

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

Vervolgens maakt invoegen u gegevenstabel toohello ORC uit Hallo faseringstabel. Bijvoorbeeld:

    INSERT INTO TABLE lineitem_orc
    SELECT L_ORDERKEY as L_ORDERKEY, 
           L_PARTKEY as L_PARTKEY , 
           L_SUPPKEY as L_SUPPKEY,
           L_LINENUMBER as L_LINENUMBER,
            L_QUANTITY as L_QUANTITY, 
           L_EXTENDEDPRICE as L_EXTENDEDPRICE,
           L_DISCOUNT as L_DISCOUNT,
           L_TAX as L_TAX,
           L_RETURNFLAG as L_RETURNFLAG,
           L_LINESTATUS as L_LINESTATUS,
           L_SHIPDATE as L_SHIPDATE,
           L_COMMITDATE as L_COMMITDATE,
           L_RECEIPTDATE as L_RECEIPTDATE, 
           L_SHIPINSTRUCT as L_SHIPINSTRUCT,
           L_SHIPMODE as L_SHIPMODE,
           L_COMMENT as L_COMMENT
    FROM lineitem;

U kunt meer lezen over Hallo ORC indeling [hier](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).

## <a name="vectorization"></a>Vectorization

Vectorization kunt Hive tooprocess een batch van 1024 samen rijen in plaats van één rij tegelijk verwerken. Dit betekent dat eenvoudige bewerkingen sneller worden uitgevoerd omdat minder interne code toorun moet.

tooenable vectorization prefix Hallo instelling na uw Hive-query:

    set hive.vectorized.execution.enabled = true;

Zie voor meer informatie [Vectorized queryuitvoering](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).

## <a name="other-optimization-methods"></a>Andere methoden optimalisatie
Er zijn meer optimalisatie methoden die u, bijvoorbeeld overwegen kunt:

* **Hive bucketing:** een techniek waarmee toocluster of segment grote sets van gegevens toooptimize queryprestaties.
* **Deelnemen aan optimalisatie:** optimalisatie van de uitvoering van Hive-query tooimprove planning Hallo efficiëntie joins en gebruiker hints Hallo hoeft te verminderen. Zie voor meer informatie [Join optimalisatie](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).
* **Verhogen verkleiningstoestellen**.

## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u verschillende algemene Hive query optimalisatie methoden geleerd. toolearn Zie meer Hallo artikelen te volgen:

* [Apache Hive in HDInsight gebruiken](hdinsight-use-hive.md)
* [Vertraging vluchtgegevens analyseren met behulp van Hive in HDInsight](hdinsight-analyze-flight-delay-data.md)
* [Twitter-gegevens met Hive in HDInsight analyseren](hdinsight-analyze-twitter-data.md)
* [Hallo Hive-Query-Console gebruiken met Hadoop in HDInsight-sensorgegevens analyseren](hdinsight-hive-analyze-sensor-data.md)
* [Hive gebruiken met HDInsight tooanalyze logboeken van websites](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
