---
title: Data Lake Store prestaties afstemmen richtlijnen aaaAzure | Microsoft Docs
description: Azure Data Lake Store-prestaties afstemmen richtlijnen
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: cgronlun
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: stewu
ms.openlocfilehash: 939faa068c0f81d18d9533956f4d336bc4d0cbe3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="tuning-azure-data-lake-store-for-performance"></a>Azure Data Lake Store voor prestaties afstemmen

Data Lake Store ondersteunt hoge gegevensdoorvoer voor i/o-intensieve analyse en gegevensverplaatsing.  In Azure Data Lake Store is met behulp van alle beschikbare doorvoer – Hallo hoeveelheid gegevens die kunnen worden gelezen of geschreven per seconde – belangrijk tooget Hallo optimale prestaties.  Dit wordt bereikt door het uitvoeren van zoveel leest en schrijft parallel mogelijk.

![Data Lake Store-prestaties](./media/data-lake-store-performance-tuning-guidance/throughput.png)

Azure Data Lake Store kunt schalen tooprovide Hallo nodig doorvoer voor alle analytics scenario. Een Azure Data Lake Store-account biedt standaard automatisch voldoende doorvoer toomeet Hallo behoeften van een categorie gebruiksvoorbeelden. Hallo gevallen waarin klanten wordt uitgevoerd in de standaardlimiet Hallo Hallo ADLS-account kan worden geconfigureerd tooprovide meer doorvoer door contact op met Microsoft ondersteuning.

## <a name="data-ingestion"></a>Gegevensopname

Bij het ophalen van gegevens uit een bron system tooADLS, is het belangrijk tooconsider die bron hardware, bron netwerkhardware en network connectivity tooADLS Hallo Hallo knelpunt kan worden.  

![Data Lake Store-prestaties](./media/data-lake-store-performance-tuning-guidance/bottleneck.png)

Het is belangrijk tooensure die Hallo verplaatsing van gegevens wordt niet beïnvloed door deze factoren.

### <a name="source-hardware"></a>Bron-Hardware

Of u van lokale machines of virtuele machines in Azure gebruikmaakt, moet u zorgvuldig Hallo geschikte hardware. SSD's tooHDDs liever voor bron schijfhardware, en kies vervolgens schijfhardware met sneller aandrijfassen. Gebruik voor bron netwerkhardware, Hallo snelste NIC's mogelijk.  In Azure, wordt aangeraden Azure D14 virtuele machines die op de juiste wijze krachtige Hallo-schijf- en netwerkhardware.

### <a name="network-connectivity-tooazure-data-lake-store"></a>Network Connectivity tooAzure Data Lake Store

Hallo-netwerkverbinding tussen de brongegevens en Azure Data Lake store kan soms Hallo knelpunt zijn. Wanneer de brongegevens On-Premises is, overweeg het gebruik van een specifieke verbinding met [Azure ExpressRoute](https://azure.microsoft.com/en-us/services/expressroute/) . Als de brongegevens in Azure, Hallo worden aanbevolen wanneer Hallo gegevens in Hallo dezelfde Azure-regio als Hallo Data Lake Store.

### <a name="configure-data-ingestion-tools-for-maximum-parallelization"></a>Gegevensopname hulpprogramma's voor maximale garandeert configureren

Nadat u Hallo bron hardware hebt opgelost en network connectivity knelpunten hierboven, u bent klaar tooconfigure de opname-hulpprogramma's. Hallo volgende tabel bevat een overzicht van de registersleutelinstellingen voor verschillende hulpprogramma's van populaire opname Hallo en biedt uitgebreide prestaties artikelen voor hen afstemmen.  Dit gaat u naar meer informatie over dit hulpprogramma toouse voor uw scenario toolearn [artikel](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-data-scenarios).

| Hulpprogramma               | Instellingen     | Meer informatie                                                                 |
|--------------------|------------------------------------------------------|------------------------------|
| PowerShell       | PerFileThreadCount, ConcurrentFileCount |  [Koppeling](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-get-started-powershell#performance-guidance-while-using-powershell)   |
| AdlCopy    | Azure Data Lake Analytics-eenheden  |   [Koppeling](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-copy-data-azure-storage-blob#performance-considerations-for-using-adlcopy)         |
| DistCp            | -m (toewijzen)   | [Koppeling](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-copy-data-wasb-distcp#performance-considerations-while-using-distcp)                             |
| Azure Data Factory| parallelCopies    | [Koppeling](../data-factory/data-factory-copy-activity-performance.md)                          |
| Sqoop           | FS.Azure.Block.Size, -m (toewijzen)    |   [Koppeling](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/)        |

## <a name="structure-your-data-set"></a>Structuur van uw gegevensset

Wanneer gegevens worden opgeslagen in Data Lake Store, de grootte van Hallo aantal bestanden en de mappenstructuur van invloed zijn op de prestaties.  Hallo bevat volgende sectie aanbevelingen in de volgende gebieden.  

### <a name="file-size"></a>Bestandsgrootte

Analytics-engines zoals HDInsight en Azure Data Lake Analytics hebben doorgaans een overhead per bestand.  Als u uw gegevens zo veel kleine bestanden opslaat, kan dit de prestaties negatief beïnvloeden.  

Uw gegevens in het algemeen zijn ingedeeld in grotere grootte bestanden voor betere prestaties.  Als een vuistregel organiseert gegevenssets in bestanden van 256MB of hoger. In sommige gevallen, zoals afbeeldingen en binaire gegevens, is het niet mogelijk tooprocess ze parallel.  In deze gevallen is wordt het tookeep afzonderlijke bestanden dan 2GB aanbevolen.

Soms beperkt gegevenspijplijnen besturen Hallo onbewerkte gegevens met een groot aantal kleine bestanden.  Het verdient aanbeveling toohave een proces voor 'koken' die groter genereert bestanden toouse voor downstream-toepassingen.  

### <a name="organizing-time-series-data-in-folders"></a>Time Series-gegevens in mappen ordenen

Hive en ADLA werkbelastingen kunt partitie verwijderen van de tijdreeks gegevens enkele query's bij het lezen van slechts een subset van gegevens op Hallo die zorgt voor betere prestaties.    

Deze pijplijnen die timeseries gegevens opnemen, plaatst u vaak hun bestanden met een zeer gestructureerd naamgeving voor bestanden en mappen. Hieronder vindt u een voorbeeld van een zeer gangbaar zien we voor gegevens die is geordend op datum:

    \DataSet\YYYY\MM\DD\datafile_YYYY_MM_DD.tsv

U ziet dat Hallo datetime-gegevens worden weergegeven als de mappen en in Hallo bestandsnaam.

Voor datum en tijd Hallo Hier volgt een algemene patroon

    \DataSet\YYYY\MM\DD\HH\mm\datafile_YYYY_MM_DD_HH_mm.tsv

Hallo keuze met Hallo map- en organisatie moet opnieuw optimaliseren voor de bestandsgrootte Hallo en een redelijke aantal bestanden in elke map.

## <a name="optimizing-io-intensive-jobs-on-hadoop-and-spark-workloads-on-hdinsight"></a>I/o-intensieve taken op de werkbelastingen voor Hadoop en Spark in HDInsight optimaliseren

Taken kunnen worden onderverdeeld in een van de volgende drie categorieën Hallo:

* **CPU-intensief.**  Deze taken zijn lang berekening tijdstippen met minimale i/o-tijden.  Voorbeelden zijn machine learning en natuurlijke taal taken verwerken.  
* **Geheugenintensief.**  Deze taken veel geheugen gebruiken.  Voorbeelden zijn PageRank en realtime analytics-taken.  
* **I/o-intensieve.**  Deze taken te besteden aan de meeste van de tijd die tijdens het doorzoeken van i/o.  Een veelvoorkomend voorbeeld is een kopieertaak die alleen lezen en schrijfbewerkingen.  Andere voorbeelden zijn onder meer gegevens voorbereiding taken die grote hoeveelheden gegevens lezen, voert een aantal gegevenstransformatie en vervolgens schrijfbewerkingen Hallo back toohello gegevensarchief.  

Hallo richtlijnen te volgen is alleen van toepassing tooI/O-intensieve taken.

### <a name="general-considerations-for-an-hdinsight-cluster"></a>Algemene overwegingen voor een HDInsight-cluster

* **HDInsight-versies.** Gebruik de nieuwste versie Hallo van HDInsight voor de beste prestaties.
* **Regio's.** Hallo Data Lake Store in Hallo plaatsen dezelfde regio bevinden als Hallo HDInsight-cluster.  

Een HDInsight-cluster bestaat uit twee hoofdknooppunten en een aantal worker-knooppunten. Elk werkrolknooppunt biedt een aantal kernen en het geheugen dat wordt bepaald door Hallo VM-type.  Wanneer een taak wordt uitgevoerd, is YARN Hallo resource onderhandelaar waarmee Hallo beschikbaar geheugen en kernen toocreate containers worden toegewezen.  Elke container uitvoert Hallo taken benodigde toocomplete Hallo taak.  Snel uitvoeren containers in parallelle tooprocess taken. Daarom wordt de prestaties verbeterd door het uitvoeren van parallelle-containers zoveel mogelijk.

Er zijn drie lagen in een HDInsight-cluster die afgestemd tooincrease worden kunnen Hallo aantal containers en gebruikmaken van alle beschikbare doorvoer.  

* **Fysieke laag**
* **YARN-laag**
* **Laag van de werkbelasting**

### <a name="physical-layer"></a>Fysieke laag

**Voer een cluster met meer knooppunten en/of groter formaat virtuele machines.**  Een groter cluster kunt u toorun meer YARN-containers zoals weergegeven in volgende Hallo-afbeelding.

![Data Lake Store-prestaties](./media/data-lake-store-performance-tuning-guidance/VM.png)

**Virtuele machines met meer netwerkbandbreedte gebruiken.**  Hallo hoeveelheid netwerkbandbreedte kan een knelpunt zijn als er minder netwerkbandbreedte dan een Data Lake Store-doorvoer.  Andere virtuele machines hebben verschillende grootten voor netwerk-bandbreedte.  Kies een VM-type die Hallo grootste mogelijke netwerkbandbreedte heeft.

### <a name="yarn-layer"></a>YARN-laag

**Kleinere YARN-containers gebruiken.**  Hallo-grootte van elke container YARN toocreate meer containers met Hallo verkleinen dezelfde hoeveelheid resources.

![Data Lake Store-prestaties](./media/data-lake-store-performance-tuning-guidance/small-containers.png)

Afhankelijk van uw werkbelasting moet altijd er een YARN container minimumgrootte die nodig is. Als u een container te klein kiest, worden de taken worden uitgevoerd in-geheugen problemen. Doorgaans moet YARN containers niet kleiner zijn dan 1GB. Het is algemene toosee 3GB YARN containers. Voor sommige werkbelastingen moet u grotere YARN-containers.  

**Kernen per YARN-container verhogen.**  Het aantal kernen tooeach container tooincrease Hallo aantal toegewezen parallelle taken die worden uitgevoerd in elke container Hallo verhogen.  Dit werkt voor toepassingen zoals Spark die meerdere taken per container worden uitgevoerd.  Voor toepassingen zoals Hive welke uitvoeren die een enkele thread in elke container is een betere toohave meer containers in plaats van meer kernen per container.   

### <a name="workload-layer"></a>Laag van de werkbelasting

**Alle beschikbare containers gebruiken.**  Het aantal taken toobe Hallo gelijk of groter dan het aantal beschikbare containers Hallo zo instellen dat alle resources worden gebruikt.

![Data Lake Store-prestaties](./media/data-lake-store-performance-tuning-guidance/use-containers.png)

**Mislukte taken zijn kostbaar.** Als u elke taak heeft een grote hoeveelheid gegevens tooprocess, vervolgens resulteert mislukken van een taak in een dure probeer het opnieuw.  Daarom is het beter toocreate meer taken, die elk een kleine hoeveelheid gegevens verwerkt.

In aanvulling toohello algemene richtlijnen hierboven heeft elke toepassing beschikbaar tootune verschillende parameters voor de specifieke toepassing. Hallo in de volgende tabel vindt u enkele van Hallo parameters en koppelingen tooget met prestaties afstemmen voor elke toepassing is gestart.

| Workload               | Parameter tooset taken                                                         |
|--------------------|-------------------------------------------------------------------------------------|
| [Spark in HDInisight](data-lake-store-performance-tuning-spark.md)       | <ul><li>NUM Executor</li><li>Executor-geheugen</li><li>Executor kernen</li></ul> |
| [Hive in HDInsight](data-lake-store-performance-tuning-hive.md)    | <ul><li>hive.tez.container.Size</li></ul>         |
| [MapReduce in HDInsight](data-lake-store-performance-tuning-mapreduce.md)            | <ul><li>mapreduce.map.Memory</li><li>Mapreduce.job.Maps</li><li>mapreduce.reduce.Memory</li><li>Mapreduce.job.reduces</li></ul> |
| [Storm op HDInsight](data-lake-store-performance-tuning-storm.md)| <ul><li>Aantal werkprocessen</li><li>Aantal exemplaren van spout executor</li><li>Aantal exemplaren van bolt executor </li><li>Aantal spout taken</li><li>Aantal bolt taken</li></ul>|

## <a name="see-also"></a>Zie ook
* [Overzicht van Azure Data Lake Store](data-lake-store-overview.md)
* [Aan de slag met Azure Data Lake Analytics](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
