---
title: aaaHive met (Hadoop) van Data Lake tools voor Visual Studio - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toouse Hallo Data Lake tools voor Visual Studio toorun Apache Hive-query's met Apache Hadoop op Azure HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2b3e672a-1195-4fa5-afb7-b7b73937bfbe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: dc76974c02cf68bcf701b2b155842c9e9c5cb988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-data-lake-tools-for-visual-studio"></a>Uitvoeren van Hive-query's met Hallo Data Lake tools voor Visual Studio

Meer informatie over hoe toouse Hallo Data Lake tools voor Visual Studio tooquery Apache Hive. Hallo Data Lake-hulpprogramma's kunt u tooeasily maken, te verzenden en te bewaken tooHadoop voor Hive-query's in Azure HDInsight.

## <a id="prereq"></a>Vereisten

* Een Azure HDInsight (Hadoop in HDInsight)-cluster

  > [!IMPORTANT]
  > Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.

* Visual Studio (een van de volgende versies Hallo):

    * Visual Studio 2013 Community/Professional/Premium/Ultimate met Update 4

    * Visual Studio 2015 (alle versies)

    * Visual Studio 2017 (alle versies)

* HDInsight tools voor Visual Studio of Azure Data Lake tools voor Visual Studio. Zie [aan de slag met Visual Studio Hadoop-hulpprogramma's voor HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) voor informatie over het installeren en configureren van Hallo's.

## <a id="run"></a>Uitvoeren van Hive-query's met behulp van Visual Studio Hallo

1. Open **Visual Studio** en selecteer **nieuw** > **Project** > **Azure Data Lake** > **HIVE** > **Hive-toepassing**. Geef een naam voor dit project.

2. Open Hallo **Script.hql** -bestand dat is gemaakt met dit project en plakken in Hallo HiveQL-instructies te volgen:

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    Deze instructies uitvoeren Hallo volgende acties:

   * `DROP TABLE`: Als Hallo tabel bestaat, wordt het door deze instructie verwijdert.

   * `CREATE EXTERNAL TABLE`: Maakt een nieuwe tabel 'extern' in Hive. De tabeldefinitie Hallo opslaan externe tabellen alleen in Hive (hello gegevens in de oorspronkelijke locatie Hallo blijft).

     > [!NOTE]
     > Externe tabellen moeten worden gebruikt wanneer u van plan Hallo onderliggende gegevens toobe bijgewerkt door een externe bron bent. Bijvoorbeeld, een MapReduce-taak of een Azure-service.
     >
     > Verwijderen van een externe tabel komt **niet** Hallo gegevens alleen Hallo tabeldefinitie kunt verwijderen.

   * `ROW FORMAT`: Hiermee geeft u Hive hoe Hallo gegevens wordt opgemaakt. In dit geval worden Hallo velden in elk logboek gescheiden door een spatie.

   * `STORED AS TEXTFILE LOCATION`: Vertelt Hive waar hello gegevens worden opgeslagen (directory Hallo bijvoorbeeld/gegevens) en dat deze is opgeslagen als tekst.

   * `SELECT`: Selecteer een telling van alle rijen waarin kolom `t4` Hallo waarde bevat `[ERROR]`. Deze instructie retourneert een waarde van `3` omdat er drie rijen met deze waarde.

   * `INPUT__FILE__NAME LIKE '%.log'`-Vertelt Hive dat we alleen gegevens uit bestanden eindigt op moet retourneren. log. Deze component beperkt Hallo search toohello sample.log bestand die Hallo gegevens bevat.

3. Selecteer in de werkbalk Hallo Hallo **HDInsight-Cluster** wilt u toouse voor deze query. Selecteer **indienen** toorun Hallo instructies als een Hive-taak.

   ![Indienings-balk](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. Hallo **taakoverzicht Hive** wordt weergegeven en geeft informatie weer over Hallo taak uitgevoerd. Gebruik Hallo **vernieuwen** toorefresh Hallo taakgegevens tot Hallo koppelen **taakstatus** wijzigingen te**voltooid**.

   ![Taakoverzicht een voltooide taak weergeven](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. Gebruik Hallo **Taakuitvoer** tooview Hallo uitvoer van deze taak te koppelen. Hiermee wordt weergegeven `[ERROR] 3`, dit is Hallo-waarde geretourneerd door deze query.

6. U kunt ook Hive-query's uitvoeren zonder een project maken. Met behulp van **Server Explorer**, vouw **Azure** > **HDInsight**, met de rechtermuisknop op uw HDInsight-server en selecteer vervolgens **een Hive-Query schrijven**.

7. In Hallo **temp.hql** document dat wordt weergegeven, toevoegen Hallo HiveQL-instructies te volgen:

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    Deze instructies uitvoeren Hallo volgende acties:

   * `CREATE TABLE IF NOT EXISTS`: Een tabel gemaakt als deze niet al bestaat. Omdat Hallo `EXTERNAL` trefwoord wordt niet gebruikt, wordt deze instructie maakt u een interne tabel. Interne tabellen worden opgeslagen in Hallo Hive-datawarehouse en worden beheerd door Hive.

     > [!NOTE]
     > In tegenstelling tot `EXTERNAL` tabellen, verwijderen van een interne tabel ook Hallo onderliggende gegevens worden verwijderd.

   * `STORED AS ORC`: Winkels Hallo gegevens in geoptimaliseerde rij kolomindeling (ORC). ORC is een maximaal geoptimaliseerd en efficiënte indeling voor het opslaan van gegevens met Hive.

   * `INSERT OVERWRITE ... SELECT`: Rijen uit Hallo geselecteerd `log4jLogs` tabel met `[ERROR]`, en vervolgens voegt gegevens in Hallo Hallo `errorLogs` tabel.

8. Selecteer in de werkbalk Hallo **indienen** toorun Hallo taak. Gebruik Hallo **taakstatus** toodetermine die Hallo-taak is voltooid.

9. tooverify die Hallo Hallo tabel, gebruik gemaakte taak **Server Explorer** en vouw **Azure** > **HDInsight** > uw HDInsight-cluster > **Hive-Databases** > **standaard**. Hallo **foutenlogboeken** tabel en Hallo **log4jLogs** tabel worden vermeld.

## <a id="nextsteps"></a>Volgende stappen

Zoals u ziet, bieden Hallo HDInsight tools voor Visual Studio een eenvoudige manier toowork met Hive-query's op HDInsight.

Voor algemene informatie over Hive in HDInsight:

* [Hive gebruiken met Hadoop in HDInsight](hdinsight-use-hive.md)

Voor informatie over andere manieren kunt u werken met Hadoop op HDInsight:

* [Pig gebruiken met Hadoop in HDInsight](hdinsight-use-pig.md)

* [MapReduce gebruiken met Hadoop op HDInsight](hdinsight-use-mapreduce.md)

Voor meer informatie over Hallo HDInsight tools voor Visual Studio:

* [Aan de slag met HDInsight tools voor Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)

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

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx

[image-hdi-hive-powershell]: ./media/hdinsight-use-hive/HDI.HIVE.PowerShell.png
[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
[image-hdi-hive-architecture]: ./media/hdinsight-use-hive/HDI.Hive.Architecture.png
