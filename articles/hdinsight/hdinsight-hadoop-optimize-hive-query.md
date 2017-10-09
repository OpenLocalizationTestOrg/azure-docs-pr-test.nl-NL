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
# <a name="optimize-hive-queries-in-azure-hdinsight"></a><span data-ttu-id="87e65-103">In Azure HDInsight Hive-query's optimaliseren</span><span class="sxs-lookup"><span data-stu-id="87e65-103">Optimize Hive queries in Azure HDInsight</span></span>

<span data-ttu-id="87e65-104">Hadoop-clusters zijn standaard niet geoptimaliseerd voor prestaties.</span><span class="sxs-lookup"><span data-stu-id="87e65-104">By default, Hadoop clusters are not optimized for performance.</span></span> <span data-ttu-id="87e65-105">In dit artikel bevat informatie over een aantal veelgebruikte optimalisatie methoden voor Hive prestaties die u tooyour query's kunt toepassen.</span><span class="sxs-lookup"><span data-stu-id="87e65-105">This article covers some most common Hive performance optimization methods that you can apply tooyour queries.</span></span>

## <a name="scale-out-worker-nodes"></a><span data-ttu-id="87e65-106">Worker-knooppunten uitbreiden</span><span class="sxs-lookup"><span data-stu-id="87e65-106">Scale out worker nodes</span></span>

<span data-ttu-id="87e65-107">Vergroten van het aantal worker-knooppunten in een cluster Hallo kunt gebruikmaken van meer mappers en verkleiningstoestellen toobe parallel worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="87e65-107">Increasing hello number of worker nodes in a cluster can leverage more mappers and reducers toobe run in parallel.</span></span> <span data-ttu-id="87e65-108">Er zijn twee manieren kunt u scale-out in HDInsight verhogen:</span><span class="sxs-lookup"><span data-stu-id="87e65-108">There are two ways you can increase scale out in HDInsight:</span></span>

* <span data-ttu-id="87e65-109">Tijdens het Hallo inrichten, kunt u het aantal worker-knooppunten met hello Azure-portal, Azure PowerShell of platformoverschrijdende opdrachtregelinterface Hallo.</span><span class="sxs-lookup"><span data-stu-id="87e65-109">At hello provision time, you can specify hello number of worker nodes using hello Azure portal, Azure PowerShell, or Cross-platform command-line interface.</span></span>  <span data-ttu-id="87e65-110">Zie [HDInsight-clusters maken](hdinsight-hadoop-provision-linux-clusters.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="87e65-110">For more information, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="87e65-111">Hallo volgende schermafbeelding ziet Hallo worker knooppuntconfiguratie op Hallo Azure-portal:</span><span class="sxs-lookup"><span data-stu-id="87e65-111">hello following screenshot shows hello worker node configuration on hello Azure portal:</span></span>
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* <span data-ttu-id="87e65-113">Op Hallo uitvoeringstijd, kunt u ook uitschalen een cluster zonder opnieuw te maken op een:</span><span class="sxs-lookup"><span data-stu-id="87e65-113">At hello run time, you can also scale out a cluster without recreating one:</span></span>

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

<span data-ttu-id="87e65-115">Zie voor meer informatie over Hallo verschillende virtuele machines die door HDInsight worden ondersteund, [HDInsight prijzen](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="87e65-115">For more information about hello different virtual machines supported by HDInsight, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="enable-tez"></a><span data-ttu-id="87e65-116">Inschakelen van Tez</span><span class="sxs-lookup"><span data-stu-id="87e65-116">Enable Tez</span></span>

<span data-ttu-id="87e65-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) is een alternatieve uitvoering engine toohello MapReduce-engine:</span><span class="sxs-lookup"><span data-stu-id="87e65-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) is an alternative execution engine toohello MapReduce engine:</span></span>

![tez_1][image-hdi-optimize-hive-tez_1]

<span data-ttu-id="87e65-119">Tez is sneller omdat:</span><span class="sxs-lookup"><span data-stu-id="87e65-119">Tez is faster because:</span></span>

* <span data-ttu-id="87e65-120">**Omgeleid acyclische grafiek (DAG) worden uitgevoerd als een enkele taak in Hallo MapReduce-engine**.</span><span class="sxs-lookup"><span data-stu-id="87e65-120">**Execute Directed Acyclic Graph (DAG) as a single job in hello MapReduce engine**.</span></span> <span data-ttu-id="87e65-121">Hallo DAG is vereist voor elke set van mappers toobe gevolgd door een reeks verkleiningstoestellen.</span><span class="sxs-lookup"><span data-stu-id="87e65-121">hello DAG requires each set of mappers toobe followed by one set of reducers.</span></span> <span data-ttu-id="87e65-122">Dit zorgt ervoor dat meerdere MapReduce-taken toobe ingezet uit voor elke Hive-query.</span><span class="sxs-lookup"><span data-stu-id="87e65-122">This causes multiple MapReduce jobs toobe spun off for each Hive query.</span></span> <span data-ttu-id="87e65-123">Tez heeft geen dergelijke beperking en complexe DAG kan worden verwerkt als een taak dus taak starten van de overhead te minimaliseren.</span><span class="sxs-lookup"><span data-stu-id="87e65-123">Tez does not have such constraint and can process complex DAG as one job thus minimizing job startup overhead.</span></span>
* <span data-ttu-id="87e65-124">**Onnodige schrijfbewerkingen voorkomt**.</span><span class="sxs-lookup"><span data-stu-id="87e65-124">**Avoids unnecessary writes**.</span></span> <span data-ttu-id="87e65-125">Vervaldatum toomultiple taken wordt ingezet voor Hallo dezelfde Hive-query in de uitvoer van elke taak Hallo-engine MapReduce Hallo tooHDFS voor tussenliggende gegevens geschreven.</span><span class="sxs-lookup"><span data-stu-id="87e65-125">Due toomultiple jobs being spun for hello same Hive query in hello MapReduce engine, hello output of each job is written tooHDFS for intermediate data.</span></span> <span data-ttu-id="87e65-126">Aangezien Tez aantal taken voor elke Hive-query minimaliseert is kunnen tooavoid onnodige schrijven.</span><span class="sxs-lookup"><span data-stu-id="87e65-126">Since Tez minimizes number of jobs for each Hive query it is able tooavoid unnecessary write.</span></span>
* <span data-ttu-id="87e65-127">**Vertragingen bij het opstarten minimaliseert**.</span><span class="sxs-lookup"><span data-stu-id="87e65-127">**Minimizes start-up delays**.</span></span> <span data-ttu-id="87e65-128">Tez is beter kunnen toominimize opstarten vertraging door het aantal mappers toostart en ook verbeterde optimalisatie in de gehele moet hello te verminderen.</span><span class="sxs-lookup"><span data-stu-id="87e65-128">Tez is better able toominimize start-up delay by reducing hello number of mappers it needs toostart and also improving optimization throughout.</span></span>
* <span data-ttu-id="87e65-129">**Containers hergebruikt**.</span><span class="sxs-lookup"><span data-stu-id="87e65-129">**Reuses containers**.</span></span> <span data-ttu-id="87e65-130">Wanneer mogelijk Tez kunnen tooreuse containers tooensure die latentie vanwege wordt toostarting van containers verminderd.</span><span class="sxs-lookup"><span data-stu-id="87e65-130">Whenever possible Tez is able tooreuse containers tooensure that latency due toostarting up containers is reduced.</span></span>
* <span data-ttu-id="87e65-131">**Continue optimalisatietechnieken**.</span><span class="sxs-lookup"><span data-stu-id="87e65-131">**Continuous optimization techniques**.</span></span> <span data-ttu-id="87e65-132">Optimalisatie is normaal uitgevoerd tijdens de compilatiefase.</span><span class="sxs-lookup"><span data-stu-id="87e65-132">Traditionally optimization was done during compilation phase.</span></span> <span data-ttu-id="87e65-133">Maar er meer informatie over Hallo invoer beschikbaar is waarmee voor betere optimalisatie tijdens runtime.</span><span class="sxs-lookup"><span data-stu-id="87e65-133">However more information about hello inputs is available that allow for better optimization during runtime.</span></span> <span data-ttu-id="87e65-134">Tez maakt gebruik van doorlopende optimalisatietechnieken waardoor verdere toooptimize Hallo-plan in Hallo runtime-fase.</span><span class="sxs-lookup"><span data-stu-id="87e65-134">Tez uses continuous optimization techniques that allows it toooptimize hello plan further into hello runtime phase.</span></span>

<span data-ttu-id="87e65-135">Zie voor meer informatie over deze begrippen [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span><span class="sxs-lookup"><span data-stu-id="87e65-135">For more details on these concepts, see [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="87e65-136">U kunt een Hive-query Tez ingeschakeld door Mining Hallo query met de onderstaande instelling voor Hallo aanbrengen:</span><span class="sxs-lookup"><span data-stu-id="87e65-136">You can make any Hive query Tez enabled by prefixing hello query with hello setting below:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="87e65-137">HDInsight-clusters op basis van Linux hebben Tez is standaard ingeschakeld.</span><span class="sxs-lookup"><span data-stu-id="87e65-137">Linux-based HDInsight clusters have Tez enabled by default.</span></span>


## <a name="hive-partitioning"></a><span data-ttu-id="87e65-138">Hive partitioneren</span><span class="sxs-lookup"><span data-stu-id="87e65-138">Hive partitioning</span></span>

<span data-ttu-id="87e65-139">I/o-bewerking is Hallo belangrijke prestatieknelpunt voor het uitvoeren van Hive-query's.</span><span class="sxs-lookup"><span data-stu-id="87e65-139">I/O operation is hello major performance bottleneck for running Hive queries.</span></span> <span data-ttu-id="87e65-140">Hallo-prestaties kunnen worden verbeterd als Hallo hoeveelheid gegevens die moeten worden toobe gelezen kan worden verminderd.</span><span class="sxs-lookup"><span data-stu-id="87e65-140">hello performance can be improved if hello amount of data that needs toobe read can be reduced.</span></span> <span data-ttu-id="87e65-141">Hive-query's scan standaard volledige Hive-tabellen.</span><span class="sxs-lookup"><span data-stu-id="87e65-141">By default, Hive queries scan entire Hive tables.</span></span> <span data-ttu-id="87e65-142">Dit is ideaal voor query's zoals tabelscans.</span><span class="sxs-lookup"><span data-stu-id="87e65-142">This is great for queries like table scans.</span></span> <span data-ttu-id="87e65-143">Maar voor query's die u alleen tooscan een kleine hoeveelheid gegevens (bijvoorbeeld, query's filteren hoeft), dit gedrag maakt onnodige overhead.</span><span class="sxs-lookup"><span data-stu-id="87e65-143">However for queries that only need tooscan a small amount of data (for example, queries with filtering), this behavior creates unnecessary overhead.</span></span> <span data-ttu-id="87e65-144">Hive partitionering kunt Hive-query's tooaccess alleen Hallo benodigde hoeveelheid gegevens in de Hive-tabellen.</span><span class="sxs-lookup"><span data-stu-id="87e65-144">Hive partitioning allows Hive queries tooaccess only hello necessary amount of data in Hive tables.</span></span>

<span data-ttu-id="87e65-145">Hive partitioneren wordt geïmplementeerd door het opnieuw indelen van Hallo onbewerkte gegevens naar de nieuwe mappen met elke partitie hebben een eigen map - waarvoor Hallo partitie door Hallo gebruiker is gedefinieerd.</span><span class="sxs-lookup"><span data-stu-id="87e65-145">Hive partitioning is implemented by reorganizing hello raw data into new directories with each partition having its own directory - where hello partition is defined by hello user.</span></span> <span data-ttu-id="87e65-146">Hallo volgende diagram ziet u een Hive-tabel op Hallo kolom partitioneren *jaar*.</span><span class="sxs-lookup"><span data-stu-id="87e65-146">hello following diagram illustrates partitioning a Hive table by hello column *Year*.</span></span> <span data-ttu-id="87e65-147">Een nieuwe map wordt gemaakt voor elk jaar.</span><span class="sxs-lookup"><span data-stu-id="87e65-147">A new directory is created for each year.</span></span>

![Partitioneren][image-hdi-optimize-hive-partitioning_1]

<span data-ttu-id="87e65-149">Enkele overwegingen partitionering:</span><span class="sxs-lookup"><span data-stu-id="87e65-149">Some partitioning considerations:</span></span>

* <span data-ttu-id="87e65-150">**Kan niet onder de partitie** -partitionering voor kolommen met slechts enkele waarden kan leiden tot enkele partities.</span><span class="sxs-lookup"><span data-stu-id="87e65-150">**Do not under partition** - Partitioning on columns with only a few values can cause few partitions.</span></span> <span data-ttu-id="87e65-151">Partitioneren op geslacht alleen maakt u bijvoorbeeld twee partities toobe (man en vrouwelijke) gemaakt, dus alleen Hallo de latentie te verminderen door een maximum van de helft.</span><span class="sxs-lookup"><span data-stu-id="87e65-151">For example, partitioning on gender only creates two partitions toobe created (male and female), thus only reduce hello latency by a maximum of half.</span></span>
* <span data-ttu-id="87e65-152">**Kan niet via partitie** : op Hallo van andere extreme, het maken van een partitie in een kolom met een unieke waarde (bijvoorbeeld userid) zorgt ervoor dat meerdere partities.</span><span class="sxs-lookup"><span data-stu-id="87e65-152">**Do not over partition** - On hello other extreme, creating a partition on a column with a unique value (for example, userid) causes multiple partitions.</span></span> <span data-ttu-id="87e65-153">Via partitie zorgt ervoor dat veel stress op Hallo cluster namenode omdat u toohandle Hallo groot aantal mappen.</span><span class="sxs-lookup"><span data-stu-id="87e65-153">Over partition causes much stress on hello cluster namenode as it has toohandle hello large number of directories.</span></span>
* <span data-ttu-id="87e65-154">**Voorkomen dat gegevens scheeftrekken** -Kies uw te nemen partitionerende sleutel goed zodat alle partities zelfs grootte zijn.</span><span class="sxs-lookup"><span data-stu-id="87e65-154">**Avoid data skew** - Choose your partitioning key wisely so that all partitions are even size.</span></span> <span data-ttu-id="87e65-155">Een voorbeeld is een partitionerende op *status* kan ertoe leiden dat het aantal records onder Californië toobe Hallo bijna 30 x die Vermont vanwege toohello verschil in de populatie.</span><span class="sxs-lookup"><span data-stu-id="87e65-155">An example is partitioning on *State* may cause hello number of records under California toobe almost 30x that of Vermont due toohello difference in population.</span></span>

<span data-ttu-id="87e65-156">toocreate een partitietabel gebruiken Hallo *gepartitioneerd door* component:</span><span class="sxs-lookup"><span data-stu-id="87e65-156">toocreate a partition table, use hello *Partitioned By* clause:</span></span>

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

<span data-ttu-id="87e65-157">Zodra Hallo gepartitioneerde tabel is gemaakt, kunt u het partitioneren van statische of dynamische partitionering maken.</span><span class="sxs-lookup"><span data-stu-id="87e65-157">Once hello partitioned table is created, you can either create static partitioning or dynamic partitioning.</span></span>

* <span data-ttu-id="87e65-158">**Statische partitioneren** betekent dat er al gedeelde gegevens in Hallo betreffende mappen en vraagt u handmatig op basis van de maplocatie Hallo Hive-partities.</span><span class="sxs-lookup"><span data-stu-id="87e65-158">**Static partitioning** means that you have already sharded data in hello appropriate directories and you can ask Hive partitions manually based on hello directory location.</span></span> <span data-ttu-id="87e65-159">Hallo volgende codefragment is een voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="87e65-159">hello following code snippet is an example.</span></span>
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* <span data-ttu-id="87e65-160">**Dynamische partitionering** betekent dat u wilt dat Hive toocreate partities automatisch voor u.</span><span class="sxs-lookup"><span data-stu-id="87e65-160">**Dynamic partitioning** means that you want Hive toocreate partitions automatically for you.</span></span> <span data-ttu-id="87e65-161">Aangezien we Hallo partitioneren van tabel uit Hallo faseringstabel al hebt gemaakt, moeten we toodo toohello gepartitioneerde tabel invoegen is:</span><span class="sxs-lookup"><span data-stu-id="87e65-161">Since we have already created hello partitioning table from hello staging table, all we need toodo is insert data toohello partitioned table:</span></span>
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

<span data-ttu-id="87e65-162">Zie voor meer informatie [gepartitioneerde tabellen](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span><span class="sxs-lookup"><span data-stu-id="87e65-162">For more details, see [Partitioned Tables](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span></span>

## <a name="use-hello-orcfile-format"></a><span data-ttu-id="87e65-163">Hallo ORCFile indeling gebruiken</span><span class="sxs-lookup"><span data-stu-id="87e65-163">Use hello ORCFile format</span></span>
<span data-ttu-id="87e65-164">Hive ondersteunt verschillende bestandsindelingen.</span><span class="sxs-lookup"><span data-stu-id="87e65-164">Hive supports different file formats.</span></span> <span data-ttu-id="87e65-165">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="87e65-165">For example:</span></span>

* <span data-ttu-id="87e65-166">**Tekst**: dit is de standaardbestandsindeling Hallo en werkt samen met de meeste scenario's</span><span class="sxs-lookup"><span data-stu-id="87e65-166">**Text**: this is hello default file format and works with most scenarios</span></span>
* <span data-ttu-id="87e65-167">**Avro**: geschikt is voor interoperabiliteit scenario's</span><span class="sxs-lookup"><span data-stu-id="87e65-167">**Avro**: works well for interoperability scenarios</span></span>
* <span data-ttu-id="87e65-168">**ORC/parketvloeren**: meest geschikt voor prestaties</span><span class="sxs-lookup"><span data-stu-id="87e65-168">**ORC/Parquet**: best suited for performance</span></span>

<span data-ttu-id="87e65-169">De indeling van de ORC (geoptimaliseerd rij kolommen) is een zeer efficiënte manier toostore Hive-gegevens.</span><span class="sxs-lookup"><span data-stu-id="87e65-169">ORC (Optimized Row Columnar) format is a highly efficient way toostore Hive data.</span></span> <span data-ttu-id="87e65-170">Vergeleken tooother indelingen, ORC heeft Hallo volgende voordelen:</span><span class="sxs-lookup"><span data-stu-id="87e65-170">Compared tooother formats, ORC has hello following advantages:</span></span>

* <span data-ttu-id="87e65-171">ondersteuning voor complexe gegevenstypen zoals DateTime en complexe en semi-gestructureerde typen</span><span class="sxs-lookup"><span data-stu-id="87e65-171">support for complex types including DateTime and complex and semi-structured types</span></span>
* <span data-ttu-id="87e65-172">een too70% compressie</span><span class="sxs-lookup"><span data-stu-id="87e65-172">up too70% compression</span></span>
* <span data-ttu-id="87e65-173">elke 10.000 rijen, waardoor de rijen overgeslagen indexen</span><span class="sxs-lookup"><span data-stu-id="87e65-173">indexes every 10,000 rows, which allow skipping rows</span></span>
* <span data-ttu-id="87e65-174">een aanzienlijke daling van de runtime-uitvoering</span><span class="sxs-lookup"><span data-stu-id="87e65-174">a significant drop in run-time execution</span></span>

<span data-ttu-id="87e65-175">tooenable ORC-indeling, eerst maakt u een tabel met Hallo component *opgeslagen als ORC*:</span><span class="sxs-lookup"><span data-stu-id="87e65-175">tooenable ORC format, you first create a table with hello clause *Stored as ORC*:</span></span>

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

<span data-ttu-id="87e65-176">Vervolgens maakt invoegen u gegevenstabel toohello ORC uit Hallo faseringstabel.</span><span class="sxs-lookup"><span data-stu-id="87e65-176">Next, you insert data toohello ORC table from hello staging table.</span></span> <span data-ttu-id="87e65-177">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="87e65-177">For example:</span></span>

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

<span data-ttu-id="87e65-178">U kunt meer lezen over Hallo ORC indeling [hier](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span><span class="sxs-lookup"><span data-stu-id="87e65-178">You can read more on hello ORC format [here](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span></span>

## <a name="vectorization"></a><span data-ttu-id="87e65-179">Vectorization</span><span class="sxs-lookup"><span data-stu-id="87e65-179">Vectorization</span></span>

<span data-ttu-id="87e65-180">Vectorization kunt Hive tooprocess een batch van 1024 samen rijen in plaats van één rij tegelijk verwerken.</span><span class="sxs-lookup"><span data-stu-id="87e65-180">Vectorization allows Hive tooprocess a batch of 1024 rows together instead of processing one row at a time.</span></span> <span data-ttu-id="87e65-181">Dit betekent dat eenvoudige bewerkingen sneller worden uitgevoerd omdat minder interne code toorun moet.</span><span class="sxs-lookup"><span data-stu-id="87e65-181">It means that simple operations are done faster because less internal code needs toorun.</span></span>

<span data-ttu-id="87e65-182">tooenable vectorization prefix Hallo instelling na uw Hive-query:</span><span class="sxs-lookup"><span data-stu-id="87e65-182">tooenable vectorization prefix your Hive query with hello following setting:</span></span>

    set hive.vectorized.execution.enabled = true;

<span data-ttu-id="87e65-183">Zie voor meer informatie [Vectorized queryuitvoering](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span><span class="sxs-lookup"><span data-stu-id="87e65-183">For more information, see [Vectorized query execution](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span></span>

## <a name="other-optimization-methods"></a><span data-ttu-id="87e65-184">Andere methoden optimalisatie</span><span class="sxs-lookup"><span data-stu-id="87e65-184">Other optimization methods</span></span>
<span data-ttu-id="87e65-185">Er zijn meer optimalisatie methoden die u, bijvoorbeeld overwegen kunt:</span><span class="sxs-lookup"><span data-stu-id="87e65-185">There are more optimization methods that you can consider, for example:</span></span>

* <span data-ttu-id="87e65-186">**Hive bucketing:** een techniek waarmee toocluster of segment grote sets van gegevens toooptimize queryprestaties.</span><span class="sxs-lookup"><span data-stu-id="87e65-186">**Hive bucketing:** a technique that allows toocluster or segment large sets of data toooptimize query performance.</span></span>
* <span data-ttu-id="87e65-187">**Deelnemen aan optimalisatie:** optimalisatie van de uitvoering van Hive-query tooimprove planning Hallo efficiëntie joins en gebruiker hints Hallo hoeft te verminderen.</span><span class="sxs-lookup"><span data-stu-id="87e65-187">**Join optimization:** optimization of Hive's query execution planning tooimprove hello efficiency of joins and reduce hello need for user hints.</span></span> <span data-ttu-id="87e65-188">Zie voor meer informatie [Join optimalisatie](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span><span class="sxs-lookup"><span data-stu-id="87e65-188">For more information, see [Join optimization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span></span>
* <span data-ttu-id="87e65-189">**Verhogen verkleiningstoestellen**.</span><span class="sxs-lookup"><span data-stu-id="87e65-189">**Increase Reducers**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="87e65-190">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="87e65-190">Next steps</span></span>
<span data-ttu-id="87e65-191">In dit artikel hebt u verschillende algemene Hive query optimalisatie methoden geleerd.</span><span class="sxs-lookup"><span data-stu-id="87e65-191">In this article, you have learned several common Hive query optimization methods.</span></span> <span data-ttu-id="87e65-192">toolearn Zie meer Hallo artikelen te volgen:</span><span class="sxs-lookup"><span data-stu-id="87e65-192">toolearn more, see hello following articles:</span></span>

* [<span data-ttu-id="87e65-193">Apache Hive in HDInsight gebruiken</span><span class="sxs-lookup"><span data-stu-id="87e65-193">Use Apache Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="87e65-194">Vertraging vluchtgegevens analyseren met behulp van Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="87e65-194">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="87e65-195">Twitter-gegevens met Hive in HDInsight analyseren</span><span class="sxs-lookup"><span data-stu-id="87e65-195">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="87e65-196">Hallo Hive-Query-Console gebruiken met Hadoop in HDInsight-sensorgegevens analyseren</span><span class="sxs-lookup"><span data-stu-id="87e65-196">Analyze sensor data using hello Hive Query Console on Hadoop in HDInsight</span></span>](hdinsight-hive-analyze-sensor-data.md)
* [<span data-ttu-id="87e65-197">Hive gebruiken met HDInsight tooanalyze logboeken van websites</span><span class="sxs-lookup"><span data-stu-id="87e65-197">Use Hive with HDInsight tooanalyze logs from websites</span></span>](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
