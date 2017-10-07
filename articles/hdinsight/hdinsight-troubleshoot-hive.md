---
title: aaaTroubleshoot Hive met behulp van Azure HDInsight | Microsoft Docs
description: Vind antwoorden op vragen over het werken met Apache Hive en Azure HDInsight toocommon.
keywords: HDInsight, Hive, veelgestelde vragen over Azure, probleemoplossingsgids, veelgestelde vragen
services: Azure HDInsight
documentationcenter: na
author: dharmeshkakadia
manager: 
editor: 
ms.assetid: 15B8D0F3-F2D3-4746-BDCB-C72944AA9252
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: dharmeshkakadia
ms.openlocfilehash: ac459316e658d0b29eb66f5685f0bc7e693bb277
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-hive-by-using-azure-hdinsight"></a>Hive oplossen met behulp van Azure HDInsight

Meer informatie over de vragen Hallo en hun oplossingen bij het werken met Apache Hive nettoladingen in Apache Ambari.


## <a name="how-do-i-export-a-hive-metastore-and-import-it-on-another-cluster"></a>Hoe ik een Hive-metastore exporteren en importeren op een ander cluster


### <a name="resolution-steps"></a>Stappen voor het oplossen

1. Verbinding toohello HDInsight-cluster via een Secure Shell (SSH)-client. Zie voor meer informatie [lezen van aanvullende](#additional-reading-end).

2. Hallo volgende opdracht op Hallo HDInsight-cluster waaruit u tooexport hello metastore wilt uitvoeren:

    ```apache
    for d in `hive -e "show databases"`; do echo "create database $d; use $d;" >> alltables.sql ; for t in `hive --database $d -e "show tables"` ; do ddl=`hive --database $d -e "show create table $t"`; echo "$ddl ;" >> alltables.sql ; echo "$ddl" | grep -q "PARTITIONED\s*BY" && echo "MSCK REPAIR TABLE $t ;" >> alltables.sql ; done; done
    ```

  Met deze opdracht genereert u een bestand met de naam allatables.sql.

3. Hallo bestand alltables.sql toohello nieuwe HDInsight-cluster te kopiëren en voer vervolgens Hallo volgende opdracht:

  ```apache
  hive -f alltables.sql
  ```

Hallo-code in de stappen voor het oplossen van Hallo wordt ervan uitgegaan dat gegevens op het nieuwe cluster Hallo paden zijn dezelfde Hallo als Hallo gegevenspaden op Hallo oude cluster. Als de gegevenspaden Hallo verschillend zijn, kunt u handmatig bewerken Hallo gegenereerd alltables.sql bestand tooreflect eventuele wijzigingen.

### <a name="additional-reading"></a>Aanvullende bronnen

- [Verbinding tooan HDInsight-cluster via SSH](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-locate-hive-logs-on-a-cluster"></a>Hoe ga ik Hive logboeken naar op een cluster

### <a name="resolution-steps"></a>Stappen voor het oplossen

1. Verbinding toohello HDInsight-cluster via SSH. Zie voor meer informatie **lezen van aanvullende**.

2. clientlogboeken tooview Hive, Hallo volgende opdracht gebruiken:

  ```apache
  /tmp/<username>/hive.log 
  ```

3. tooview Hive metastore logboeken Hallo volgende opdracht gebruiken:

  ```apache
  /var/log/hive/hivemetastore.log 
  ```

4. tooview Hiveserver, gebruikt u Hallo volgende opdracht:

  ```apache
  /var/log/hive/hiveserver2.log 
  ```

### <a name="additional-reading"></a>Aanvullende bronnen

- [Verbinding tooan HDInsight-cluster via SSH](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-launch-hello-hive-shell-with-specific-configurations-on-a-cluster"></a>Hoe ik Hallo Hive-shell met specifieke configuraties die op een cluster starten

### <a name="resolution-steps"></a>Stappen voor het oplossen

1. Geef een sleutel-waardepaar configuratie wanneer u Hallo Hive-shell start. Zie voor meer informatie [lezen van aanvullende](#additional-reading-end).

  ```apache
  hive -hiveconf a=b 
  ```

2. toolist alle effectieve configuraties op Hive-shell, gebruik Hallo volgende opdracht:

  ```apache
  hive> set;
  ```

  Gebruik bijvoorbeeld Hallo Hive-opdrachtshell toostart volgen met de logboekregistratie voor foutopsporing is ingeschakeld op het Hallo-console:

  ```apache
  hive -hiveconf hive.root.logger=ALL,console 
  ```

### <a name="additional-reading"></a>Aanvullende bronnen

- [Hive-configuratie-eigenschappen](https://cwiki.apache.org/confluence/display/Hive/Configuration+Properties)


## <a name="how-do-i-analyze-tez-dag-data-on-a-cluster-critical-path"></a>Hoe analyseer ik Tez DAG gegevens op een cluster kritiek pad


### <a name="resolution-steps"></a>Stappen voor het oplossen
 
1. een Apache Tez tooanalyze omgeleid acyclische grafiek (DAG) in een cluster kritieke grafiek, toohello HDInsight-cluster via SSH verbinding. Zie voor meer informatie [lezen van aanvullende](#additional-reading-end).

2. Voer bij een opdrachtprompt Hallo volgende opdracht:
   
  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar CriticalPath --saveResults --dagId <DagId> --eventFileName <DagData.zip> 
  ```

3. toolist andere analyzers die kunnen worden gebruikt tooanalyze Tez-DAG Hallo volgende opdracht gebruiken:

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-job-analyzer-*.jar
  ```

  Als eerste argument hello, moet u een voorbeeldprogramma opgeven.

  Namen van geldig programma zijn onder andere:
    - **ContainerReuseAnalyzer**: details van de container opnieuw kunnen worden gebruikt in een DAG afdrukken
    - **CriticalPath**: Find Hallo kritieke pad van een DAG
    - **LocalityAnalyzer**: details in een DAG plaats afdrukken
    - **ShuffleTimeAnalyzer**: Hallo willekeurige volgorde tijd details in een DAG analyseren
    - **SkewAnalyzer**: Hallo scheeftrekken details in een DAG analyseren
    - **SlowNodeAnalyzer**: details knooppunt in een DAG afdrukken
    - **SlowTaskIdentifier**: afdrukken trage taakdetails in een DAG
    - **SlowestVertexAnalyzer**: traagste hoekpunt details in een DAG afdrukken
    - **SpillAnalyzer**: gelekt details afdrukken in een DAG
    - **TaskConcurrencyAnalyzer**: afdrukken Hallo taakdetails gelijktijdigheid van taken in een DAG
    - **VertexLevelCriticalPathAnalyzer**: Find Hallo kritieke pad op hoekpunt niveau in een DAG


### <a name="additional-reading"></a>Aanvullende bronnen

- [Verbinding tooan HDInsight-cluster via SSH](hdinsight-hadoop-linux-use-ssh-unix.md)


## <a name="how-do-i-download-tez-dag-data-from-a-cluster"></a>Hoe kan ik Tez DAG gegevens downloaden vanaf een cluster


#### <a name="resolution-steps"></a>Stappen voor het oplossen

Er zijn twee manieren toocollect hello Tez DAG gegevens:

- Vanaf de opdrachtregel Hallo:
 
    Verbinding toohello HDInsight-cluster via SSH. Voer Hallo volgende opdracht achter de opdrachtprompt Hallo:

  ```apache
  hadoop jar /usr/hdp/current/tez-client/tez-history-parser-*.jar org.apache.tez.history.ATSImportTool -downloadDir . -dagId <DagId> 
  ```

- Hallo Ambari Tez weergave gebruiken:
   
  1. Ga tooAmbari. 
  2. Ga tooTez weergave (onder Hallo tegels pictogram in de rechterbovenhoek Hallo). 
  3. Selecteer Hallo gewenste tooview DAG.
  4. Selecteer **downloaden van gegevens**.

### <a name="additional-reading-end"></a>Aanvullende bronnen

[Verbinding tooan HDInsight-cluster via SSH](hdinsight-hadoop-linux-use-ssh-unix.md)






