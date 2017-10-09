---
title: aaaUse Beeline met Apache Hive - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse hello Beeline client toorun Hive query's met Hadoop op HDInsight. Beeline is een hulpprogramma voor het werken met HiveServer2 via JDBC vast.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: beeline hive, hive beeline
ms.assetid: 3adfb1ba-8924-4a13-98db-10a67ab24fca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: e788ff39f33d928808cfcb83a92f62ac9ae8ca09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-beeline-client-with-apache-hive"></a>Hallo Beeline client met Apache Hive gebruiken

Meer informatie over hoe toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) toorun Hive query's op HDInsight.

Beeline is een Hive-client die is opgenomen op Hallo hoofdknooppunten van uw HDInsight-cluster. Beeline JDBC tooconnect tooHiveServer2, een service die wordt gehost op uw HDInsight-cluster gebruikt. U kunt ook gebruiken Beeline tooaccess Hive in HDInsight op afstand meer dan Hallo internet. Hallo volgende tabel bevat de verbindingsreeksen voor gebruik met Beeline:

| Waar u Beeline van uitvoert | Parameters |
| --- | --- | --- |
| Een SSH-verbinding tooa headnode of edge-knooppunt | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| Externe Hallo-cluster | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> Vervang `admin` met Hallo cluster aanmeldingsaccount voor uw cluster.
>
> Vervang `password` door Hallo wachtwoord voor aanmeldingsaccount Hallo-cluster.
>
> Vervang `clustername` met Hallo-naam van uw HDInsight-cluster.

## <a id="prereq"></a>Vereisten

* Een op Linux gebaseerde Hadoop op HDInsight-cluster.

  > [!IMPORTANT]
  > Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

* Een SSH-client of een lokale Beeline-client. De meeste Hallo stappen in dit document wordt ervan uitgegaan dat u van Beeline van een SSH-sessie toohello cluster gebruikmaakt. Zie voor informatie over het uitvoeren van Beeline uit externe Hallo cluster Hallo [Beeline op afstand gebruiken](#remote) sectie.

    Zie voor meer informatie over het gebruik van SSH [SSH gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="beeline"></a>Gebruik Beeline

1. Bij het starten van Beeline, moet u een verbindingsreeks opgeven voor HiveServer2 op uw HDInsight-cluster. toorun Hallo-opdracht uit externe Hallo-cluster, moet u ook Hallo cluster aanmeldingsnaam account opgeven (standaard `admin`) en het wachtwoord. Hallo tabel toofind Hallo connection string indeling en parameters toouse volgende gebruiken:

    | Waar u Beeline van uitvoert | Parameters |
    | --- | --- | --- |
    | Een SSH-verbinding tooa headnode of edge-knooppunt | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | Externe Hallo-cluster | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    Hallo na de opdracht kan bijvoorbeeld gebruikte toostart Beeline van een SSH-sessie toohello cluster:

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    Met deze opdracht Hallo Beeline client start en tooHiveServer2 Hallo hoofdknooppunt van cluster verbindt. Zodra het Hallo-opdracht is voltooid, wordt u aankomt bij een `jdbc:hive2://headnodehost:10001/>` prompt.

2. Beeline opdrachten beginnen met een `!` teken, bijvoorbeeld `!help` geeft help weer. Hallo echter `!` voor bepaalde opdrachten kunnen worden weggelaten. Bijvoorbeeld: `help` werkt ook.

    Er is een `!sql`, die is gebruikt tooexecute HiveQL-instructies. HiveQL wordt echter zo vaak gebruikt dat kunt u de voorgaande Hallo weglaten `!sql`. Hallo twee instructies te volgen zijn gelijkwaardig:

    ```hiveql
    !sql show tables;
    show tables;
    ```

    Op een nieuw cluster slechts één tabel wordt vermeld: **hivesampletable**.

3. Hallo opdracht toodisplay Hallo schema voor Hallo hivesampletable volgende gebruiken:

    ```hiveql
    describe hivesampletable;
    ```

    Met deze opdracht retourneert Hallo volgende informatie:

        +-----------------------+------------+----------+--+
        |       col_name        | data_type  | comment  |
        +-----------------------+------------+----------+--+
        | clientid              | string     |          |
        | querytime             | string     |          |
        | market                | string     |          |
        | deviceplatform        | string     |          |
        | devicemake            | string     |          |
        | devicemodel           | string     |          |
        | state                 | string     |          |
        | country               | string     |          |
        | querydwelltime        | double     |          |
        | sessionid             | bigint     |          |
        | sessionpagevieworder  | bigint     |          |
        +-----------------------+------------+----------+--+

    Deze informatie wordt Hallo kolommen in Hallo tabel beschreven. Bij sommige query's op deze gegevens kan worden uitgevoerd, gaan we in plaats daarvan maakt een nieuwe tabel toodemonstrate hoe tooload gegevens in Hive en een schema hebt toegepast.

4. Voer Hallo na instructies toocreate een tabel met de naam **log4jLogs** met behulp van voorbeeldgegevens voorzien Hallo HDInsight-cluster:

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    Deze instructies uitvoeren Hallo volgende acties:

    * `DROP TABLE`-Als Hallo tabel bestaat, wordt deze verwijderd.

    * `CREATE EXTERNAL TABLE`-Maakt een **externe** tabel in Hive. De tabeldefinitie Hallo opslaan externe tabellen alleen in Hive. Hallo-gegevens in de oorspronkelijke locatie Hallo gelaten.

    * `ROW FORMAT`-Hoe Hallo gegevens zijn opgemaakt. In dit geval worden Hallo velden in elk logboek gescheiden door een spatie.

    * `STORED AS TEXTFILE LOCATION`-Waarin Hallo gegevens worden opgeslagen en in welke bestandsindeling.

    * `SELECT`: Hiermee kunt u een telling van alle rijen waarin kolom **t4** Hallo waarde bevat **[fout]**. Deze query retourneert een waarde van **3** omdat er zijn drie rijen met deze waarde.

    * `INPUT__FILE__NAME LIKE '%.log'`-Hive probeert tooapply hello tooall schemabestanden in Hallo-directory. In dit geval bevat Hallo map bestanden die niet overeenkomen met de Hallo schema. tooprevent garbagecollection gegevens in de resultaten van de hello, deze instructie Hive vertelt dat we alleen gegevens uit bestanden eindigt op moet retourneren. log.

  > [!NOTE]
  > Externe tabellen moeten worden gebruikt wanneer u van plan Hallo onderliggende gegevens toobe bijgewerkt door een externe bron bent. Bijvoorbeeld, een uploadproces geautomatiseerde gegevens of een MapReduce-bewerking.
  >
  > Verwijderen van een externe tabel komt **niet** Hallo gegevens alleen Hallo tabeldefinitie kunt verwijderen.

    Hallo uitvoer van deze opdracht is vergelijkbaar toohello de volgende tekst:

        INFO  : Tez session hasn't been created yet. Opening session
        INFO  :

        INFO  : Status: Running (Executing on YARN cluster with App id application_1443698635933_0001)

        INFO  : Map 1: -/-      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0(+1)/1
        INFO  : Map 1: 1/1      Reducer 2: 1/1
        +----------+--------+--+
        |   sev    | count  |
        +----------+--------+--+
        | [ERROR]  | 3      |
        +----------+--------+--+
        1 row selected (47.351 seconds)

5. tooexit Beeline, gebruik `!exit`.

## <a id="file"></a>Beeline toorun een bestand HiveQL gebruiken

Volgende stappen toocreate een bestand, voert u met behulp van Beeline hello gebruiken.

1. Gebruik Hallo volgende opdracht toocreate uit een bestand met de naam **query.hql**:

    ```bash
    nano query.hql
    ```

2. Gebruik hello tekst als Hallo inhoud van Hallo-bestand te volgen. Deze query maakt een nieuwe 'interne' tabel met de naam **foutenlogboeken**:

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    Deze instructies uitvoeren Hallo volgende acties:

    * **MAKEN van tabel als niet bestaat** -als Hallo tabel niet al bestaat, wordt deze gemaakt. Sinds Hallo **externe** trefwoord wordt niet gebruikt, wordt deze instructie maakt u een interne tabel. Interne tabellen worden opgeslagen in Hallo Hive-datawarehouse en volledig worden beheerd door Hive.
    * **OPGESLAGEN AS ORC** -Hallo-gegevens opslaat in geoptimaliseerd rij kolommen (ORC)-indeling. ORC is een maximaal geoptimaliseerd en efficiënte indeling voor het opslaan van gegevens met Hive.
    * **INSERT OVERSCHRIJVEN... Selecteer** -rijen uit Hallo geselecteerd **log4jLogs** tabel met **[fout]**, en vervolgens voegt gegevens in Hallo Hallo **foutenlogboeken** tabel.

    > [!NOTE]
    > In tegenstelling tot externe tabellen verwijdert de Hallo onderliggende gegevens ook een interne tabel verwijderen.

3. Gebruik-bestand Hallo toosave **Ctrl**+**_X**, voert u **Y**, en tot slot **Enter**.

4. Hallo toorun Hallo bestand met behulp van Beeline volgende gebruiken:

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > Hallo `-i` parameter Beeline begint, voert Hallo instructies in Hallo query.hql bestand. Zodra het Hallo-query is voltooid, wordt u aankomt bij Hallo `jdbc:hive2://headnodehost:10001/>` prompt. U kunt ook een bestand met de Hallo uitvoeren `-f` parameter Beeline afgesloten nadat Hallo-query is voltooid.

5. tooverify die Hallo **foutenlogboeken** tabel is gemaakt, gebruikt u na de instructie tooreturn alle rijen uit Hallo Hallo **foutenlogboeken**:

    ```hiveql
    SELECT * from errorLogs;
    ```

    Drie rijen met gegevens moeten worden geretourneerd, alle overkoepelende **[fout]** in kolom t4:

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <a id="remote"></a>Beeline op afstand gebruiken

Als u deze Beeline lokaal zijn geïnstalleerd, of wordt gebruikt door een Docker-installatiekopie, zoals [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), moet u de volgende parameters hello gebruiken:

* __Verbindingsreeks__:`-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`

* __Aanmeldingsnaam van de cluster__:`-n admin`

* __Aanmeldingswachtwoord cluster__`-p 'password'`

Vervang Hallo `clustername` in de verbindingsreeks Hallo Hallo-naam van uw HDInsight-cluster.

Vervang `admin` met de naam van uw cluster aanmelding en vervang Hallo `password` met Hallo wachtwoord voor uw cluster-aanmelding.

## <a id="sparksql"></a>Beeline met Spark gebruiken

Spark biedt een eigen implementatie van HiveServer2, die vaak zoals tooas Hallo Spark Thrift-server. Deze service Spark SQL tooresolve query's gebruikt in plaats van Hive en kan zorgen voor betere prestaties, afhankelijk van uw query.

tooconnect toohello Spark Thrift-server van een Spark in HDInsight-cluster, gebruik poort `10002` in plaats van `10001`. Bijvoorbeeld `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.

> [!IMPORTANT]
> Hallo Spark Thrift-server is niet rechtstreeks toegankelijk via internet Hallo. U kunt alleen tooit verbinding van een SSH-sessie of Hallo binnen hetzelfde virtuele Azure-netwerk zoals Hallo HDInsight-cluster.

## <a id="summary"></a><a id="nextsteps"></a>De volgende stappen

Zie voor meer algemene informatie over Hive in HDInsight Hallo document te volgen:

* [Hive gebruiken met Hadoop in HDInsight](hdinsight-use-hive.md)

Zie voor meer informatie over andere manieren kunt u werken met Hadoop op HDInsight Hallo documenten te volgen:

* [Pig gebruiken met Hadoop in HDInsight](hdinsight-use-pig.md)
* [MapReduce gebruiken met Hadoop op HDInsight](hdinsight-use-mapreduce.md)

Als u van Tez met Hive gebruikmaakt, raadpleegt u Hallo documenten te volgen:

* [Hallo Tez UI op HDInsight op basis van Windows gebruiken](hdinsight-debug-tez-ui.md)
* [Hallo Ambari Tez weergave op Linux gebaseerde HDInsight gebruiken](hdinsight-debug-ambari-tez-view.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md

[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html


[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
