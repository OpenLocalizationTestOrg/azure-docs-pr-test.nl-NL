---
title: aaaUse Hadoop Hive en extern bureaublad in HDInsight - Azure | Microsoft Docs
description: Informatie over hoe tooconnect tooHadoop-cluster in HDInsight met behulp van extern bureaublad en vervolgens Hive-query's uitvoeren met behulp van Hallo opdrachtregelinterface Hive.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c228e35-d58a-4f22-917a-1d20c9da89b4
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: f86ffc1be33a8b0b2346d1a1388e5dfa6d0f8777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a>Hive gebruiken met Hadoop op HDInsight met extern bureaublad
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

In dit artikel leert u hoe tooconnect tooan HDInsight-cluster met behulp van extern bureaublad en voer vervolgens Hive query's met behulp van Hallo Hive-opdrachtregelinterface (CLI).

> [!IMPORTANT]
> Extern bureaublad is alleen beschikbaar op HDInsight-clusters die Windows hello besturingssysteem gebruiken. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.
>
> Voor HDInsight 3.4 of hoger, Zie [Hive gebruiken met HDInsight en Beeline](hdinsight-hadoop-use-hive-beeline.md) voor informatie over het uitvoeren van Hive-query rechtstreeks op Hallo-cluster vanaf een opdrachtregel.

## <a id="prereq"></a>Vereisten
toocomplete hello stappen in dit artikel, moet u de volgende Hallo:

* Een cluster op basis van Windows HDInsight (Hadoop in HDInsight)
* Een clientcomputer met Windows 10, Windows 8 of Windows 7

## <a id="connect"></a>Verbinding maken met extern bureaublad
Extern bureaublad inschakelen voor Hallo HDInsight-cluster en verbind tooit met behulp Hallo-instructies in de [tooHDInsight clusters met RDP verbinding](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

## <a id="hive"></a>Hallo Hive-opdracht gebruiken
Wanneer u verbinding hebt met het bureaublad toohello voor Hallo HDInsight-cluster gebruiken Hallo toowork met Hive stappen te volgen:

1. Hallo HDInsight bureaublad starten Hallo **Hadoop-opdrachtregel**.
2. Voer Hallo opdracht toostart Hallo Hive CLI te volgen:

        %hive_home%\bin\hive

    Als Hallo CLI is gestart, ziet u Hallo CLI Hive-prompt: `hive>`.
3. Gebruik Hallo CLI Hallo na toocreate instructies een nieuwe tabel met de naam te geven **log4jLogs** voorbeeldgegevens gebruikt:

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Deze instructies uitvoeren Hallo volgende acties:

   * **DROP TABLE**: Hiermee verwijdert u Hallo tabel en het Hallo-gegevensbestand als Hallo tabel al bestaat.
   * **EXTERNE tabel maken**: maakt een nieuwe 'extern' tabel in Hive. Externe tabellen opslaan alleen Hallo tabeldefinitie in Hive (hello gegevens in de oorspronkelijke locatie Hallo blijft).

     > [!NOTE]
     > Externe tabellen moeten worden gebruikt wanneer u gegevens toobe worden bijgewerkt door een externe bron (zoals een uploadproces geautomatiseerde gegevens) of door een andere MapReduce-bewerking onderliggende hello verwacht, maar u wilt dat altijd Hive query toouse Hallo meest recente gegevens.
     >
     > Verwijderen van een externe tabel komt **niet** Hallo gegevens alleen Hallo tabeldefinitie kunt verwijderen.
     >
     >
   * **INDELING van de rij**: Hive-wordt uitgelegd hoe Hallo gegevens wordt opgemaakt. In dit geval worden Hallo velden in elk logboek gescheiden door een spatie.
   * **AS TEXTFILE locatie opgeslagen**: vertelt Hive waar Hallo gegevens zijn opgeslagen (directory Hallo bijvoorbeeld/gegevens) en deze is opgeslagen als tekst.
   * **Selecteer**: selecteert een telling van alle rijen waarin kolom **t4** Hallo waarde bevat **[fout]**. Dit moet een waarde van retourneren **3** omdat er drie rijen met deze waarde.
   * **INPUT__FILE__NAME zoals '%.log'** -vertelt Hive die we alleen gegevens uit bestanden eindigt op moet retourneren. log. Hiermee beperkt u Hallo zoeken toohello sample.log-bestand dat Hallo gegevens bevat, en voorkomt dat het retourneren van gegevens uit andere voorbeeld gegevensbestanden die komen niet overeen met de Hallo-schema die is gedefinieerd.
4. Gebruik Hallo na toocreate instructies een nieuwe 'interne' tabel met de naam **foutenlogboeken**:

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    Deze instructies uitvoeren Hallo volgende acties:

   * **MAKEN van tabel als niet bestaat**: maakt een tabel als deze niet al bestaat. Omdat Hallo **externe** trefwoord wordt niet gebruikt, is dit een interne tabel die is opgeslagen in Hallo Hive-datawarehouse en volledig wordt beheerd door Hive.

     > [!NOTE]
     > In tegenstelling tot **externe** tabellen, verwijderen van een interne tabel ook Hallo onderliggende gegevens worden verwijderd.
     >
     >
   * **OPGESLAGEN AS ORC**: Hallo-gegevens opslaat in geoptimaliseerde rij kolomindeling (ORC). Dit is een maximaal geoptimaliseerd en efficiënte indeling voor het opslaan van gegevens met Hive.
   * **INSERT OVERSCHRIJVEN... Selecteer**: rijen uit Hallo geselecteerd **log4jLogs** tabel met **[fout]**, en vervolgens voegt gegevens in Hallo Hallo **foutenlogboeken** tabel.

     tooverify die alleen rijen die bevatten **[fout]** in kolom t4 waren opgeslagen toohello **foutenlogboeken** tabel, gebruikt u na de instructie tooreturn alle rijen uit Hallo Hallo **foutenlogboeken**:

       Selecteer * uit foutenlogboeken;

     Drie rijen met gegevens moeten worden geretourneerd, alle overkoepelende **[fout]** in kolom t4.

## <a id="summary"></a>Samenvatting
Zoals u ziet, Hallo Hallo Hive opdracht biedt een eenvoudige manier toointeractively Hive-query's uitvoeren op een HDInsight-cluster, Hallo monitor status van taken en Hallo uitvoer ophalen.

## <a id="nextsteps"></a>Volgende stappen
Voor algemene informatie over Hive in HDInsight:

* [Hive gebruiken met Hadoop in HDInsight](hdinsight-use-hive.md)

Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:

* [Pig gebruiken met Hadoop in HDInsight](hdinsight-use-pig.md)
* [MapReduce gebruiken met Hadoop op HDInsight](hdinsight-use-mapreduce.md)

Als u van Tez met Hive gebruikmaakt, raadpleegt u Hallo volgende documenten voor het opsporen van informatie:

* [Hallo Tez UI op HDInsight op basis van Windows gebruiken](hdinsight-debug-tez-ui.md)
* [Hallo Ambari Tez weergave op Linux gebaseerde HDInsight gebruiken](hdinsight-debug-ambari-tez-view.md)

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

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





[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
