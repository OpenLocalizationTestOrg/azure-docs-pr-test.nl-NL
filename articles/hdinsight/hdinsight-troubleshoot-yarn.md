---
title: aaaTroubleshoot YARN met behulp van Azure HDInsight | Microsoft Docs
description: Vind antwoorden op vragen over het werken met Apache Hadoop YARN en Azure HDInsight toocommon.
keywords: HDInsight, YARN Veelgestelde vragen over Azure, probleemoplossingsgids, veelgestelde vragen
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: F76786A9-99AB-4B85-9B15-CA03528FC4CD
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: 800d9738cb27e05a64db470ee58565af3b85aa99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-yarn-by-using-azure-hdinsight"></a>YARN oplossen met behulp van Azure HDInsight

Meer informatie over de meestvoorkomende problemen Hallo en hun oplossingen bij het werken met Apache Hadoop YARN nettoladingen in Apache Ambari.

## <a name="how-do-i-create-a-new-yarn-queue-on-a-cluster"></a>Hoe maak een nieuwe YARN-wachtrij op een cluster


### <a name="resolution-steps"></a>Stappen voor het oplossen 

Gebruik Hallo volgende stappen in de Ambari toocreate een nieuwe YARN-wachtrij en saldo Hallo capaciteit verdeling over alle Hallo wachtrijen. 

In dit voorbeeld twee bestaande wachtrijen (**standaard** en **thriftsvr**) beide zijn gewijzigd van 50% capaciteit too25% capaciteit, waarmee Hallo nieuwe wachtrij (spark) 50% capaciteit.
| Wachtrij | Capaciteit | Maximale capaciteit |
| --- | --- | --- | --- |
| Standaard | 25% | 50% |
| thrftsvr | 25% | 50% |
| Spark | 50% | 50% |

1. Selecteer Hallo **Ambari-weergaven** pictogram en selecteer vervolgens Hallo rasterpatroon. Selecteer vervolgens **YARN Queue Manager**.

    ![Selecteer Hallo Ambari-weergaven pictogram](media/hdinsight-troubleshoot-yarn/create-queue-1.png)
2. Selecteer Hallo **standaard** wachtrij.

    ![Hallo wachtrij selecteren](media/hdinsight-troubleshoot-yarn/create-queue-2.png)
3. Voor Hallo **standaard** wachtrij, wijzigt u Hallo **capaciteit** van 50% too25%. Voor Hallo **thriftsvr** wachtrij, wijzigt u Hallo **capaciteit** too25%.

    ![Hallo capaciteit too25% voor Hallo standaard en thriftsvr wachtrijen wijzigen](media/hdinsight-troubleshoot-yarn/create-queue-3.png)
4. selecteert u een nieuwe wachtrij toocreate **wachtrij toevoegen**.

    ![Selecteer een wachtrij toevoegen](media/hdinsight-troubleshoot-yarn/create-queue-4.png)

5. Naam Hallo nieuwe wachtrij.

    ![Naam Hallo wachtrij Spark](media/hdinsight-troubleshoot-yarn/create-queue-5.png)  

6. Hallo laat **capaciteit** waarden op 50% en selecteer vervolgens Hallo **acties** knop.

    ![Selecteer de actieknop Hallo](media/hdinsight-troubleshoot-yarn/create-queue-6.png)  
7. Selecteer **opslaan en vernieuw wachtrijen**.

    ![Selecteer opslaan en wachtrijen vernieuwen](media/hdinsight-troubleshoot-yarn/create-queue-7.png)  

Deze wijzigingen zijn onmiddellijk op Hallo YARN Scheduler UI zichtbaar.

### <a name="additional-reading"></a>Aanvullende bronnen

- [YARN CapacityScheduler](https://hadoop.apache.org/docs/r2.7.2/hadoop-yarn/hadoop-yarn-site/CapacityScheduler.html)


## <a name="how-do-i-download-yarn-logs-from-a-cluster"></a>Hoe kan ik YARN-logboeken downloaden vanaf een cluster


### <a name="resolution-steps"></a>Stappen voor het oplossen 

1. Verbinding toohello HDInsight-cluster via een Secure Shell (SSH)-client. Zie voor meer informatie [lezen van aanvullende](#additional-reading-2).

2. toolist alle toepassings-id's van Hallo YARN toepassingen die momenteel worden uitgevoerd, Hallo Hallo volgende opdracht uitvoeren:

    ```apache
    yarn top
    ```
    Hallo-id's vermeld in Hallo **APPLICATIONID** kolom. U kunt Logboeken downloaden van Hallo **APPLICATIONID** kolom.

    ```apache
    YARN top - 18:00:07, up 19d, 0:14, 0 active users, queue(s): root
    NodeManager(s): 4 total, 4 active, 0 unhealthy, 0 decommissioned, 0 lost, 0 rebooted
    Queue(s) Applications: 2 running, 10 submitted, 0 pending, 8 completed, 0 killed, 0 failed
    Queue(s) Mem(GB): 97 available, 3 allocated, 0 pending, 0 reserved
    Queue(s) VCores: 58 available, 2 allocated, 0 pending, 0 reserved
    Queue(s) Containers: 2 allocated, 0 pending, 0 reserved

                      APPLICATIONID USER             TYPE      QUEUE   #CONT  #RCONT  VCORES RVCORES     MEM    RMEM  VCORESECS    MEMSECS %PROGR       TIME NAME
     application_1490377567345_0007 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628407    2442611  10.00   18:20:20 Thrift JDBC/ODBC Server
     application_1490377567345_0006 hive            spark  thriftsvr       1       0       1       0      1G      0G    1628430    2442645  10.00   18:20:20 Thrift JDBC/ODBC Server
    ```

3. toodownload YARN-logboeken voor container voor alle toepassing modellen Hallo volgende opdracht gebruiken:
   
    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am ALL > amlogs.txt
    ```

    Met deze opdracht maakt een logbestand met de naam amlogs.txt. 

4. toodownload YARN-logboeken voor container voor alleen Hallo nieuwste toepassing master, Hallo volgende opdracht gebruiken:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am -1 > latestamlogs.txt
    ```

    Met deze opdracht maakt een logbestand met de naam latestamlogs.txt. 

4. toodownload YARN-logboeken voor container voor de eerste twee toepassing modellen Hallo Hallo volgende opdracht gebruiken:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -am 1,2 > first2amlogs.txt 
    ```

    Met deze opdracht maakt een logbestand met de naam first2amlogs.txt. 

5. toodownload alle YARN-Logboeken in container gebruiken Hallo volgende opdracht:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> > logs.txt
    ```

    Met deze opdracht maakt een logbestand met de naam logs.txt. 

6. toodownload hello YARN container logboek voor een specifieke container, gebruik Hallo volgende opdracht:

    ```apache
    yarn logs -applicationIdn logs -applicationId <application_id> -containerId <container_id> > containerlogs.txt 
    ```

    Met deze opdracht maakt een logbestand met de naam containerlogs.txt.

### <a name="additional-reading-2"></a>Aanvullende bronnen

- [TooHDInsight (Hadoop) verbinding via SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix)
- [Apache Hadoop YARN-concepten en toepassingen](https://hortonworks.com/blog/apache-hadoop-yarn-concepts-and-applications/)







