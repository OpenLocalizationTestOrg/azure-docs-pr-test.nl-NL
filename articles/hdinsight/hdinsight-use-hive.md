---
title: aaaWhat is Apache Hive en HiveQL - Azure HDInsight | Microsoft Docs
description: Apache Hive is een systeem voor het datawarehouse van gegevens voor Hadoop. U kunt de gegevens die zijn opgeslagen in HiveQL, welke vergelijkbaar tooTransact-SQL met Hive query. In dit document leest u hoe toouse Hive en HiveQL met Azure HDInsight.
keywords: hiveql, wat is er hive, hadoop hiveql, hoe toouse hive, informatie over hive, wat is er hive
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2c10f989-7636-41bf-b7f7-c4b67ec0814f
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: a2772312263895ff99b499898264c2e6d5e816e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a>Wat is Apache Hive en HiveQL in Azure HDInsight?

[Apache Hive](http://hive.apache.org/) is een systeem voor het datawarehouse van gegevens voor Hadoop. Hive kunt gegevenssamenvatting, query's en analyse van gegevens. Hive-query's zijn geschreven in HiveQL die een vergelijkbare tooSQL voor query-taal.

Hive kunt u tooproject structuur op grotendeels ongestructureerde gegevens. Nadat u de structuur Hallo gedefinieerd, kunt u HiveQL tooquery Hallo gegevens zonder kennis van Java of MapReduce.

HDInsight biedt verschillende clustertypen die zijn afgestemd op specifieke werkbelasting in gedachten. Hallo na clustertypen worden meestal gebruikt voor Hive-query's:

* __Interactieve Hive__: een Hadoop-cluster waarmee [lage latentie analytische verwerking (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) functionaliteit tooimprove responstijden voor interactieve query's. Zie voor meer informatie, Hallo [beginnen met een interactieve Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md) document.

* __Hadoop__: een Hadoop-cluster dat is afgestemd op batchverwerking werkbelastingen. Zie voor meer informatie, Hallo [starten met Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) document.

* __Spark__: Apache Spark zijn ingebouwde functionaliteit voor het werken met Hive. Zie voor meer informatie, Hallo [beginnen met Spark in HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) document.

* __HBase__: HiveQL gebruikte tooquery opgeslagen gegevens in HBase kan worden. Zie voor meer informatie, Hallo [beginnen met HBase in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) document.

## <a name="how-toouse-hive"></a>Hoe toouse Hive

Gebruik Hallo tabel toodiscover hoe toouse Hive met HDInsight te volgen:

| **Gebruik deze methode** als u wilt dat... | .. .an **interactieve** shell | ... **batch** verwerken | .. .door dit **cluster-besturingssysteem** | .. .from dit **clientbesturingssysteem** |
|:--- |:---:|:---:|:--- |:--- |
| [Hive-weergave](hdinsight-hadoop-use-hive-ambari-view.md) |✔ |✔ |Linux |(Browser gebaseerd) |
| [Beeline client](hdinsight-hadoop-use-hive-beeline.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X of Windows |
| [REST API](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |✔ |Linux- of Windows * |Linux, Unix, Mac OS X of Windows |
| [HDInsight tools voor Visual Studio](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |✔ |Linux- of Windows * |Windows |
| [Windows PowerShell](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |✔ |Linux- of Windows * |Windows |

> [!IMPORTANT]
> \*Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.
>
> Als u een cluster met HDInsight op basis van Windows gebruikt, kunt u Hallo [Query console](hdinsight-hadoop-use-hive-query-console.md) vanuit de browser of [extern bureaublad](hdinsight-hadoop-use-hive-remote-desktop.md) toorun Hive-query's.

## <a name="hiveql-language-reference"></a>HiveQL-taalreferentie

Taalreferentie HiveQL is beschikbaar in Hallo [taal handmatig (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).

## <a name="hive-and-data-structure"></a>Structuur van hive en gegevens

Hive begrijpt hoe toowork met gestructureerd en semi-gestructureerde gegevens. Bijvoorbeeld: tekstbestanden waar Hallo velden worden gescheiden door specifieke tekens. Hallo volgende HiveQL-instructie maakt een tabel door spaties gescheiden gegevens:

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

Hive biedt ook ondersteuning voor aangepaste **serialisatiefunctie/deserializers (serde-schrijfbewerking)** voor complexe of onregelmatig gestructureerde gegevens. Zie voor meer informatie, Hallo [hoe een aangepaste JSON serde-schrijfbewerking met HDInsight toouse](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.

Zie voor meer informatie over ondersteunde bestandsindelingen in Hive Hallo [taal handmatig (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)

## <a name="hive-internal-tables-vs-external-tables"></a>Interne tabellen tegenover externe tabellen hive

Er zijn twee soorten tabellen die u met Hive maken kunt:

* __Interne__: gegevens worden opgeslagen in Hallo Hive-datawarehouse. Hallo datawarehouse bevindt zich op `/hive/warehouse/` op Hallo standaard opslag voor Hallo-cluster.

    Gebruik interne tabellen wanneer:

    * Gegevens is tijdelijk.
    * Wilt u Hive toomanage Hallo levenscyclus van Hallo tabel en gegevens.

* __Externe__: gegevens worden opgeslagen buiten het Hallo-datawarehouse. Hallo-gegevens kunnen worden opgeslagen op opslag die toegankelijk is door Hallo-cluster.

    Gebruik externe tabellen wanneer:

    * Hallo-gegevens worden ook gebruikt buiten Hive. Bijvoorbeeld zijn Hallo-gegevensbestanden bijgewerkt door een ander proces (die wordt niet vergrendeld Hallo-bestanden.)
    * Gegevens moeten tooremain in Hallo onderliggende locatie, zelfs na het Hallo-tabel verwijderen.
    * U moet een aangepaste locatie, zoals een niet-standaard opslagaccount.
    * Een ander programma dan hive beheert gegevensindeling hello, locatie, enzovoort.

Zie voor meer informatie, Hallo [Hive interne en externe tabellen Intro] [ cindygross-hive-tables] blogbericht.

## <a name="user-defined-functions-udf"></a>Gebruiker gedefinieerde functies (UDF)

Hive kan verder worden uitgebreid via **gebruiker gedefinieerde functies (UDF)**. Een UDF kunt u de functionaliteit van tooimplement of logica die eenvoudig niet is gemodelleerd in HiveQL. Zie voor een voorbeeld van het gebruik van UDF's met Hive Hallo documenten te volgen:

* [Een Java door de gebruiker gedefinieerde functie gebruiken met Hive](hdinsight-hadoop-hive-java-udf.md)

* [Een Python door de gebruiker gedefinieerde functie gebruiken met Hive en Pig](hdinsight-python.md)

* [Een C# gebruiker gedefinieerde functie gebruiken met Hive en Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [Hoe de gebruiker gedefinieerde aangepaste component tooadd tooHDInsight functioneren](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [Een voorbeeld Hive gebruiker gedefinieerde functie tooconvert datum-/ tijdnotaties tooHive tijdstempel](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <a id="data"></a>Voorbeeldgegevens

Hive in HDInsight wordt vooraf geladen geleverd met een interne tabel met de naam `hivesampletable`. HDInsight biedt ook een voorbeeld van gegevenssets die kunnen worden gebruikt met Hive. Deze gegevenssets worden opgeslagen in Hallo `/example/data` en `/HdiSamples` mappen. Deze mappen aanwezig zijn in Hallo standaard opslagruimte voor uw cluster.

## <a id="job"></a>Voorbeeld van de Hive-query

Hallo volgende HiveQL-instructies projectkolommen op Hallo `/example/data/sample.log` bestand:

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

In het vorige voorbeeld hello Voer Hallo HiveQL-instructies Hallo van de volgende activiteiten:

* `set hive.execution.engine=tez;`: Sets Hallo uitvoering engine toouse Tez. Tez gebruik in plaats van MapReduce krijgt u een toename van de prestaties van query's. Zie voor meer informatie over Tez hello [Apache Tez gebruiken voor betere prestaties](#usetez) sectie.

    > [!NOTE]
    > Deze instructie is alleen vereist wanneer u een HDInsight op basis van Windows-cluster. Tez is Hallo standaard engine voor het uitvoeren voor HDInsight op basis van Linux.

* `DROP TABLE`: Als Hallo tabel al bestaat, verwijderen.

* `CREATE EXTERNAL TABLE`: Hiermee maakt u een nieuw **externe** tabel in Hive. De tabeldefinitie Hallo opslaan externe tabellen alleen in Hive. in de oorspronkelijke locatie hello en in de oorspronkelijke indeling Hallo Hallo gegevens blijft.

* `ROW FORMAT`: Hiermee geeft u Hive hoe Hallo gegevens wordt opgemaakt. In dit geval worden Hallo velden in elk logboek gescheiden door een spatie.

* `STORED AS TEXTFILE LOCATION`: Vertelt Hive waar hello gegevens worden opgeslagen (Hallo `example/data` directory) en dat deze is opgeslagen als tekst. Hallo-gegevens worden in één bestand of verdeeld over meerdere bestanden binnen Hallo-directory.

* `SELECT`: Hiermee selecteert u een telling van alle rijen waarin hello kolom **t4** Hallo waarde bevat **[fout]**. Deze instructie retourneert een waarde van **3** omdat er drie rijen met deze waarde.

* `INPUT__FILE__NAME LIKE '%.log'`-Hive probeert tooapply hello tooall schemabestanden in Hallo-directory. In dit geval bevat Hallo map bestanden die niet overeenkomen met de Hallo schema. tooprevent garbagecollection gegevens in de resultaten van de hello, deze instructie Hive vertelt dat we alleen gegevens uit bestanden eindigt op moet retourneren. log.

> [!NOTE]
> Externe tabellen moeten worden gebruikt wanneer u van plan Hallo onderliggende gegevens toobe bijgewerkt door een externe bron bent. Bijvoorbeeld, een geautomatiseerd proces of MapReduce-bewerking uploaden.
>
> Verwijderen van een externe tabel komt **niet** Hallo-gegevens verwijderen Hallo tabeldefinitie alleen worden verwijderd.

toocreate een **interne** in plaats van de externe tabel, gebruikt u Hallo HiveQL te volgen:

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

Deze instructies uitvoeren Hallo volgende acties:

* `CREATE TABLE IF NOT EXISTS`: Als Hallo tabel niet bestaat, maken. Omdat Hallo **externe** trefwoord wordt niet gebruikt, wordt deze instructie maakt u een interne tabel. Hallo-tabel is opgeslagen in Hallo Hive-datawarehouse en volledig wordt beheerd door Hive.

* `STORED AS ORC`: Het Hallo-gegevens opslaat in geoptimaliseerd rij kolommen (ORC)-indeling. ORC is een maximaal geoptimaliseerd en efficiënte indeling voor het opslaan van gegevens met Hive.

* `INSERT OVERWRITE ... SELECT`: Rijen uit Hallo geselecteerd **log4jLogs** tabel met **[fout]**, en vervolgens voegt de gegevens in Hallo Hallo **foutenlogboeken** tabel.

> [!NOTE]
> In tegenstelling tot externe tabellen verwijderd voor het verwijderen van een interne tabel ook Hallo onderliggende gegevens.

## <a name="improve-hive-query-performance"></a>Hive-query's sneller

### <a id="usetez"></a>Apache Tez

[Apache Tez](http://tez.apache.org) ligt een framework dat kunt van gegevensintensieve toepassingen, zoals Hive, toorun veel efficiënter op schaal. Tez is standaard ingeschakeld voor Linux gebaseerde HDInsight-clusters.

> [!NOTE]
> Tez is momenteel uitgeschakeld voor Windows gebaseerde HDInsight-clusters standaard en moet zijn ingeschakeld. tootake profiteren van Tez, Hallo na de waarde moet worden ingesteld voor een Hive-query:
>
> `set hive.execution.engine=tez;`
>
> Tez is Hallo standaard engine voor Linux gebaseerde HDInsight-clusters.

Hallo [Hive op Tez-Ontwerpdocumenten](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) bevat details over Hallo implementatie keuzen en afstemmen configuraties.

tooaid bij foutopsporing taken uitgevoerd met Tez, HDInsight biedt Hallo web UI's waarmee u tooview details van Tez-taken te volgen:

* [Hallo Ambari Tez weergave op Linux gebaseerde HDInsight gebruiken](hdinsight-debug-ambari-tez-view.md)

* [Hallo Tez UI op HDInsight op basis van Windows gebruiken](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a>Lage latentie Analytical Processing (LLAP)

[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (soms ook wel lange Live en proces) is een nieuwe functie in Hive 2.0 waarmee de caching van query's in het geheugen. LLAP maakt Hive-query's sneller up te[26 x sneller dan Hive 1.x in sommige gevallen](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).

HDInsight biedt LLAP Hallo clustertype interactieve Hive. Zie voor meer informatie, Hallo [beginnen met een interactieve Hive](hdinsight-hadoop-use-interactive-hive.md) document.

## <a name="hive-jobs-and-sql-server-integration-services"></a>Hive-taken en SQL Server Integration Services

U kunt SQL Server Integration Services (SSIS) toorun een Hive-taak. Hello Azure Feature Pack voor SSIS biedt Hallo onderdelen die met Hive-taken in HDInsight werken te volgen.

* [Azure HDInsight Hive-taak][hivetask]

* [Azure abonnement Verbindingsbeheer][connectionmanager]

Meer informatie over Azure Feature Pack Hallo voor SSIS [hier][ssispack].

## <a id="nextsteps"></a>Volgende stappen

Nu dat u hebt geleerd wat Hive is en hoe toouse met Hadoop in HDInsight, gebruik Hallo volgen koppelingen tooexplore andere manieren toowork met Azure HDInsight.

* [Uploaden van gegevens tooHDInsight][hdinsight-upload-data]
* [Pig gebruiken met HDInsight][hdinsight-use-pig]
* [MapReduce-taken gebruiken met HDInsight][hdinsight-use-mapreduce]

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/
[hivetask]: http://msdn.microsoft.com/library/mt146771(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx

[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md


[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx
