---
title: aaaUse Hadoop Hive op Hallo Query-Console in de HDInsight - Azure | Microsoft Docs
description: Meer informatie over hoe toouse Hallo webgebaseerde Console Query toorun Hive-query's op een HDInsight Hadoop-cluster van uw browser.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5ae074b0-f55e-472d-94a7-005b0e79f779
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 621882082c9a07655d34b8dc980b8e47dd04b745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-query-console"></a>Uitvoeren van Hive-query's met behulp van Hallo Query-Console
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

In dit artikel leert u hoe toouse hello HDInsight Query Console toorun Hive-query's op een HDInsight Hadoop-cluster van uw browser.

> [!IMPORTANT]
> Hallo HDInsight Query-Console is alleen beschikbaar op Windows gebaseerde HDInsight-clusters. Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.
>
> Voor HDInsight 3.4 of hoger, Zie [uitvoeren Hive-query's in de Ambari Hive-weergave](hdinsight-hadoop-use-hive-ambari-view.md) voor informatie over het uitvoeren van Hive-query's vanuit een webbrowser.

## <a id="prereq"></a>Vereisten
toocomplete hello stappen in dit artikel, moet u de volgende Hallo.

* Een HDInsight Hadoop op basis van Windows-cluster
* Een moderne webbrowser

## <a id="run"></a>Uitvoeren van Hive-query's met behulp van Hallo Query-Console
1. Open een webbrowser en navigeer te**https://CLUSTERNAME.azurehdinsight.net**, waarbij **CLUSTERNAME** Hallo-naam van uw HDInsight-cluster. Als u wordt gevraagd, voert u Hallo-gebruikersnaam en wachtwoord die u hebt gebruikt toen u Hallo cluster hebt gemaakt.
2. Hallo-koppelingen bovenaan Hallo Hallo pagina, selecteer **Hive-Editor**. U ziet nu een formulier dat gebruikt tooenter hello HiveQL-instructies worden kan die u wilt dat toorun in Hallo HDInsight-cluster.

    ![Hallo hive-editor](./media/hdinsight-hadoop-use-hive-query-console/queryconsole.png)

    Vervang de tekst hello `Select * from hivesampletable` Hello HiveQL-instructies te volgen:

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Deze instructies uitvoeren Hallo volgende acties:

   * **DROP TABLE**: Hiermee verwijdert u Hallo tabel en het Hallo-gegevensbestand als Hallo tabel al bestaat.
   * **EXTERNE tabel maken**: maakt een nieuwe 'extern' tabel in Hive. Externe tabellen opslaan alleen Hallo tabeldefinitie in Hive; Hallo-gegevens in de oorspronkelijke locatie Hallo gelaten.

     > [!NOTE]
     > Externe tabellen moeten worden gebruikt wanneer u gegevens toobe worden bijgewerkt door een externe bron (zoals een uploadproces geautomatiseerde gegevens) of door een andere MapReduce-bewerking onderliggende hello verwacht, maar u wilt dat altijd Hive query toouse Hallo meest recente gegevens.
     >
     > Verwijderen van een externe tabel komt **niet** Hallo gegevens alleen Hallo tabeldefinitie kunt verwijderen.
     >
     >
   * **INDELING van de rij**: Hive-wordt uitgelegd hoe Hallo gegevens wordt opgemaakt. In dit geval worden Hallo velden in elk logboek gescheiden door een spatie.
   * **AS TEXTFILE locatie opgeslagen**: vertelt Hive waar Hallo gegevens zijn opgeslagen (directory Hallo bijvoorbeeld/gegevens) en deze is opgeslagen als tekst
   * **Selecteer**: Selecteer een telling van alle rijen waarin kolom **t4** Hallo waarde bevatten **[fout]**. Dit moet een waarde van retourneren **3** omdat er drie rijen met deze waarde.
   * **INPUT__FILE__NAME zoals '%.log'** -vertelt Hive die we alleen gegevens uit bestanden eindigt op moet retourneren. log. Hiermee beperkt u Hallo zoeken toohello sample.log-bestand dat Hallo gegevens bevat, en voorkomt dat het retourneren van gegevens uit andere voorbeeld gegevensbestanden die komen niet overeen met de Hallo-schema die is gedefinieerd.
3. Klik op **indienen**. Hallo **taak sessie** op Hallo onderaan Hallo pagina details voor Hallo-taak moet worden weergegeven.
4. Wanneer Hallo **Status** wijzigingen te veld**voltooid**, selecteer **Details weergeven** voor Hallo-taak. Op de pagina met details Hallo Hallo **Taakuitvoer** bevat `[ERROR]    3`. U kunt Hallo **downloaden** knop onder deze toodownload veld van een bestand met de Hallo-uitvoer van Hallo-taak.

## <a id="summary"></a>Samenvatting
Zoals u ziet, Hive query's in een HDInsight-cluster Hallo Query-Console biedt een eenvoudige manier toorun Hallo taakstatus controleren en Hallo uitvoer ophalen.

Selecteer toolearn meer over het gebruik van Hive-Query Console toorun Hive-taken **aan de slag** bovenaan Hallo Hallo Query-Console, gebruik vervolgens Hallo voorbeelden die worden geleverd. Elke steekproef begeleidt bij Hallo proces van het gebruik van Hive tooanalyze gegevens, inclusief uitleg over Hallo HiveQL-instructies in het Hallo-voorbeeld gebruikt.

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



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
