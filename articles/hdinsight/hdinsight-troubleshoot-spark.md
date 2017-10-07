---
title: aaaTroubleshoot Spark met behulp van Azure HDInsight | Microsoft Docs
description: Vind antwoorden op vragen over het werken met Apache Spark en Azure HDInsight toocommon.
keywords: Azure HDInsight, Spark, veelgestelde vragen, het oplossen van de handleiding, bekende problemen, de configuratie van de toepassing, Ambari
services: Azure HDInsight
documentationcenter: na
author: arijitt
manager: 
editor: 
ms.assetid: 25D89586-DE5B-4268-B5D5-CC2CE12207ED
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/7/2017
ms.author: arijitt
ms.openlocfilehash: c9f910daf295462238a3143ae2589db6d383097f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-spark-by-using-azure-hdinsight"></a>Spark oplossen met behulp van Azure HDInsight

Meer informatie over de meestvoorkomende problemen Hallo en hun oplossingen bij het werken met Apache Spark nettoladingen in Apache Ambari.

## <a name="how-do-i-configure-a-spark-application-by-using-ambari-on-clusters"></a>Hoe kan ik een Spark-toepassing configureren met behulp van Ambari op clusters

### <a name="resolution-steps"></a>Stappen voor het oplossen

Hallo configuratiewaarden voor deze procedure zijn eerder in HDInsight ingesteld. Zie toodetermine welke configuraties Spark toobe set en toowhat waarden moeten [wat een Spark-toepassing OutofMemoryError uitzondering veroorzaakt](#what-causes-a-spark-application-outofmemoryerror-exception). 

1. Selecteer in de lijst Hallo van clusters, **Spark2**.

    ![Selecteer de cluster in lijst](media/hdinsight-troubleshoot-spark/update-config-1.png)

2. Selecteer Hallo **Configs** tabblad.

    ![Selecteer Hallo Configs tabblad](media/hdinsight-troubleshoot-spark/update-config-2.png)

3. Selecteer in de lijst Hallo van configuraties, **standaardinstellingen van aangepaste spark2**.

    ![Selecteer de aangepaste-spark-standaardinstellingen](media/hdinsight-troubleshoot-spark/update-config-3.png)

4. Zoek naar Hallo waarde instellen dat u nodig hebt tooadjust, zoals **spark.executor.memory**. In dit geval Hallo waarde van **4608m** is te hoog.

    ![Selecteer Hallo spark.executor.memory veld](media/hdinsight-troubleshoot-spark/update-config-4.png)

5. Set Hallo waarde toohello aanbevolen instelling. Hallo waarde **2048m** voor deze instelling wordt aanbevolen.

    ![Wijziging waarde too2048m](media/hdinsight-troubleshoot-spark/update-config-5.png)

6. Hallo waarde opslaan en sla vervolgens Hallo-configuratie. Selecteer op de werkbalk Hallo **opslaan**.

    ![Hallo-instelling en configuratie opslaan](media/hdinsight-troubleshoot-spark/update-config-6a.png)

    U wordt gewaarschuwd als alle configuraties aandacht vereisen. Houd er rekening mee Hallo-items en selecteer vervolgens **toch doorgaan**. 

    ![Selecteer wilt u toch doorgaan](media/hdinsight-troubleshoot-spark/update-config-6b.png)

    Voeg een opmerking over Hallo configuratiewijzigingen en selecteer vervolgens **opslaan**.

    ![Voer een opmerking over Hallo wijzigingen](media/hdinsight-troubleshoot-spark/update-config-6c.png)

7. Telkens wanneer een configuratie wordt opgeslagen, wordt u gevraagd toorestart Hallo-service. Selecteer **opnieuw**.

    ![Opnieuw opstarten selecteren](media/hdinsight-troubleshoot-spark/update-config-7a.png)

    Bevestig Hallo opnieuw opstarten.

    ![Selecteer bevestigen alle opnieuw starten](media/hdinsight-troubleshoot-spark/update-config-7b.png)

    Hallo-processen die worden uitgevoerd, kunt u bekijken.

    ![Bekijk actieve processen](media/hdinsight-troubleshoot-spark/update-config-7c.png)

8. U kunt configuraties kunt toevoegen. Selecteer in de lijst Hallo van configuraties, **standaardinstellingen van aangepaste spark2**, en selecteer vervolgens **eigenschap toevoegen**.

    ![Selecteer een eigenschap toevoegen](media/hdinsight-troubleshoot-spark/update-config-8.png)

9. Een nieuwe eigenschap definiëren. U kunt één eigenschap definiëren met behulp van een dialoogvenster voor specifieke instellingen, bijvoorbeeld Hallo-gegevenstype. Of u kunt meerdere eigenschappen definiëren met behulp van één definitie per regel. 

    In dit voorbeeld Hallo **spark.driver.memory** eigenschap is gedefinieerd met een waarde van **4g**.

    ![Nieuwe eigenschap definiëren](media/hdinsight-troubleshoot-spark/update-config-9.png)

10. Hallo-configuratie op te slaan en Hallo-service vervolgens opnieuw te starten zoals beschreven in stap 6 en 7.

Deze wijzigingen zijn hele cluster, maar kunnen worden genegeerd wanneer u Hallo Spark taak indient.

### <a name="additional-reading"></a>Aanvullende bronnen

[Verzending van de taak Spark in HDInsight-clusters](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-a-jupyter-notebook-on-clusters"></a>Hoe kan ik een Spark-toepassing configureren met behulp van een Jupyter-notebook in clusters

### <a name="resolution-steps"></a>Stappen voor het oplossen

1. Zie toodetermine welke configuraties Spark toobe set en toowhat waarden moeten [wat een Spark-toepassing OutofMemoryError uitzondering veroorzaakt](#what-causes-a-spark-application-outofmemoryerror-exception).

2. In de eerste cel Hallo van Hallo Jupyter-notebook na Hallo **%% configureren** richtlijn Hallo Spark-configuraties in geldige JSON-indeling opgeven. De werkelijke waarden Hallo zo nodig wijzigen:

    ![Een configuratie toevoegen](media/hdinsight-troubleshoot-spark/add-configuration-cell.png)

### <a name="additional-reading"></a>Aanvullende bronnen

[Verzending van de taak Spark in HDInsight-clusters](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-livy-on-clusters"></a>Hoe kan ik een Spark-toepassing configureren met behulp van Livy op clusters

### <a name="resolution-steps"></a>Stappen voor het oplossen

1. Zie toodetermine welke configuraties Spark toobe set en toowhat waarden moeten [wat een Spark-toepassing OutofMemoryError uitzondering veroorzaakt](#what-causes-a-spark-application-outofmemoryerror-exception). 

2. Hallo Spark toepassing tooLivy verzenden met behulp van een REST-client, zoals cURL. Gebruik een opdracht vergelijkbare toohello volgende. De werkelijke waarden Hallo zo nodig wijzigen:

    ```apache
    curl -k --user 'username:password' -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://container@storageaccountname.blob.core.windows.net/example/jars/sparkapplication.jar", "className":"com.microsoft.spark.application", "numExecutors":4, "executorMemory":"4g", "executorCores":2, "driverMemory":"8g", "driverCores":4}'  
    ```

### <a name="additional-reading"></a>Aanvullende bronnen

[Verzending van de taak Spark in HDInsight-clusters](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="how-do-i-configure-a-spark-application-by-using-spark-submit-on-clusters"></a>Hoe configureer een toepassing met behulp van spark indienen Spark op clusters

### <a name="resolution-steps"></a>Stappen voor het oplossen

1. Zie toodetermine welke configuraties Spark toobe set en toowhat waarden moeten [wat een Spark-toepassing OutofMemoryError uitzondering veroorzaakt](#what-causes-a-spark-application-outofmemoryerror-exception).

2. Spark-shell start met behulp van een opdracht vergelijkbare toohello volgende. Hallo werkelijke waarde van Hallo configuraties zo nodig wijzigen: 

    ```apache
    spark-submit --master yarn-cluster --class com.microsoft.spark.application --num-executors 4 --executor-memory 4g --executor-cores 2 --driver-memory 8g --driver-cores 4 /home/user/spark/sparkapplication.jar
    ```

### <a name="additional-reading"></a>Aanvullende bronnen

[Verzending van de taak Spark in HDInsight-clusters](https://blogs.msdn.microsoft.com/azuredatalake/2017/01/06/spark-job-submission-on-hdinsight-101/)


## <a name="what-causes-a-spark-application-outofmemoryerror-exception"></a>Wat een Spark-toepassing OutofMemoryError uitzondering veroorzaakt

### <a name="detailed-description"></a>Gedetailleerde beschrijving

Hallo Spark toepassing mislukt met de volgende typen van niet-onderschepte uitzonderingen Hallo:

```apache
ERROR Executor: Exception in task 7.0 in stage 6.0 (TID 439) 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

```apache
ERROR SparkUncaughtExceptionHandler: Uncaught exception in thread Thread[Executor task launch worker-0,5,main] 

java.lang.OutOfMemoryError 
    at java.io.ByteArrayOutputStream.hugeCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.grow(Unknown Source) 
    at java.io.ByteArrayOutputStream.ensureCapacity(Unknown Source) 
    at java.io.ByteArrayOutputStream.write(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.drain(Unknown Source) 
    at java.io.ObjectOutputStream$BlockDataOutputStream.setBlockDataMode(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject0(Unknown Source) 
    at java.io.ObjectOutputStream.writeObject(Unknown Source) 
    at org.apache.spark.serializer.JavaSerializationStream.writeObject(JavaSerializer.scala:44) 
    at org.apache.spark.serializer.JavaSerializerInstance.serialize(JavaSerializer.scala:101) 
    at org.apache.spark.executor.Executor$TaskRunner.run(Executor.scala:239) 
    at java.util.concurrent.ThreadPoolExecutor.runWorker(Unknown Source) 
    at java.util.concurrent.ThreadPoolExecutor$Worker.run(Unknown Source) 
    at java.lang.Thread.run(Unknown Source) 
```

### <a name="probable-cause"></a>Mogelijke oorzaak

Hallo meest waarschijnlijke oorzaak van deze uitzondering is dat niet voldoende geheugen toohello Java virtuele machines (JVMs) wordt toegewezen. Deze JVMs worden gestart als Executor of stuurprogramma's als onderdeel van Hallo Spark-toepassing. 

### <a name="resolution-steps"></a>Stappen voor het oplossen

1. Maximale grootte van Hallo gegevens Hallo Spark toepassing ingangen Hallo bepalen. U kunt een schatting op basis van de maximale grootte Hallo van Hallo invoergegevens Hallo tussenliggende gegevens die wordt geproduceerd door transformeren Hallo invoergegevens en Hallo uitvoergegevens die wordt gemaakt bij het Hallo-toepassing is verder Hallo tussenliggende gegevens transformeren. Dit proces is een iteratief als u een initiële formele schatting niet maken. 

2. Zorg ervoor dat Hallo HDInsight-cluster dat u gaat toouse heeft onvoldoende bronnen in termen van geheugen en kernen tooaccommodate Hallo Spark toepassing. U kunt dit vaststellen door Hallo cluster metrische gegevens sectie van de gebruikersinterface van YARN Hallo Hallo waarden weer te geven van **geheugen gebruikt** vs. **Totaal geheugen**, en **VCores gebruikt** vs. **Totaal aantal VCores**.

3. Hallo Spark volgende configuraties tooappropriate waarden, dit mag niet meer dan 90% van het beschikbare geheugen Hallo en kernen ingesteld. Hallo-waarden moet binnen de geheugenvereisten Hallo Hallo Spark-toepassing: 

    ```apache
    spark.executor.instances (Example: 8 for 8 executor count) 
    spark.executor.memory (Example: 4g for 4 GB) 
    spark.yarn.executor.memoryOverhead (Example: 384m for 384 MB) 
    spark.executor.cores (Example: 2 for 2 cores per executor) 
    spark.driver.memory (Example: 8g for 8GB) 
    spark.driver.cores (Example: 4 for 4 cores)   
    spark.yarn.driver.memoryOverhead (Example: 384m for 384MB) 
    ```

    tooget hello Totaal geheugen gebruikt door alle Executor, Hallo volgende opdracht uitvoeren: 
    
    ```apache
    spark.executor.instances * (spark.executor.memory + spark.yarn.executor.memoryOverhead) 
    ```
    tooget hello Totaal geheugen gebruikt door het Hallo-stuurprogramma Hallo volgende opdracht uitvoeren:
    
    ```apache
    spark.driver.memory + spark.yarn.driver.memoryOverhead
    ```

### <a name="additional-reading"></a>Aanvullende bronnen

- [Overzicht van Spark geheugen](http://spark.apache.org/docs/latest/tuning.html#memory-management-overview)
- [Fouten opsporen in een Spark-toepassing op een HDInsight-cluster](https://blogs.msdn.microsoft.com/azuredatalake/2016/12/19/spark-debugging-101/)

