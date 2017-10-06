---
title: aaaManage resources voor Apache Spark in Azure HDInsight-cluster | Microsoft Docs
description: Meer informatie over hoe toouse resources beheren voor Spark-clusters in Azure HDInsight voor betere prestaties.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9da7d4e3-458e-4296-a628-77b14643f7e4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: e18682a24f77494db884105f9db03c0a350ddad6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-resources-for-apache-spark-cluster-on-azure-hdinsight"></a>Resources beheren voor Apache Spark-cluster in Azure HDInsight 

In dit artikel leert u hoe tooaccess Hallo interfaces zoals Ambari UI, gebruikersinterface van YARN en Hallo Spark geschiedenis Server die is gekoppeld aan uw Spark-cluster. U wordt ook meer informatie over hoe tootune Hallo clusterconfiguratie voor optimale prestaties.

**Vereisten:**

U moet Hallo volgende hebben:

* Een Azure-abonnement. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Een Apache Spark-cluster in HDInsight. Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="how-do-i-launch-hello-ambari-web-ui"></a>Hoe ik Hallo Ambari-Webgebruikersinterface starten?
1. Van Hallo [Azure Portal](https://portal.azure.com/), vanaf Hallo startboard, klikt u op Hallo tegel voor uw Spark-cluster (als u toohello startboard vastgemaakt). U kunt ook tooyour cluster onder navigeren **door alles bladeren** > **HDInsight-Clusters**.
2. Klik op Hallo blade Spark-cluster **Dashboard**. Wanneer u wordt gevraagd, voert u Hallo beheerdersreferenties voor Hallo Spark-cluster.

    ![Ambari starten](./media/hdinsight-apache-spark-resource-manager/hdinsight-launch-cluster-dashboard.png "Start Resource Manager")
3. Dit moet Hallo Ambari-Webgebruikersinterface, starten, zoals hieronder wordt weergegeven.

    ![Ambari-webgebruikersinterface](./media/hdinsight-apache-spark-resource-manager/ambari-web-ui.png "Ambari-webgebruikersinterface")   

## <a name="how-do-i-launch-hello-spark-history-server"></a>Hoe ik Hallo Spark geschiedenis Server starten?
1. Van Hallo [Azure Portal](https://portal.azure.com/), vanaf Hallo startboard, klikt u op Hallo tegel voor uw Spark-cluster (als u toohello startboard vastgemaakt).
2. Bij Hallo cluster blade onder **snelkoppelingen**, klikt u op **Cluster-Dashboard**. In Hallo **Cluster-Dashboard** blade, klikt u op **Spark geschiedenis Server**.

    ![Spark geschiedenis Server](./media/hdinsight-apache-spark-resource-manager/launch-history-server.png "Spark geschiedenis van Server")

    Wanneer u wordt gevraagd, voert u Hallo beheerdersreferenties voor Hallo Spark-cluster.

## <a name="how-do-i-launch-hello-yarn-ui"></a>Hoe ik Hallo gebruikersinterface van Yarn starten?
U kunt Hallo gebruikersinterface van YARN toomonitor toepassingen die momenteel worden uitgevoerd op Hallo Spark-cluster gebruiken.

1. Cluster-blade hello, klikt u op **Cluster-Dashboard**, en klik vervolgens op **YARN**.

    ![Gebruikersinterface van YARN starten](./media/hdinsight-apache-spark-resource-manager/launch-yarn-ui.png)

   > [!TIP]
   > U kunt ook kunt u ook Hallo gebruikersinterface van YARN van Hallo Ambari UI starten. toolaunch hello Ambari UI, cluster-blade hello, klikt u op **Cluster-Dashboard**, en klik vervolgens op **HDInsight-Cluster-Dashboard**. Hallo Ambari UI, klik op **YARN**, klikt u op **snelkoppelingen**op Hallo active resourcemanager en klik vervolgens op **ResourceManager UI**.
   >
   >

## <a name="what-is-hello-optimum-cluster-configuration-toorun-spark-applications"></a>Wat is Hallo optimale configuratie toorun Spark clustertoepassingen?
Hallo drie belangrijke parameters die kunnen worden gebruikt voor de configuratie van Spark, afhankelijk van de toepassingsvereisten zijn `spark.executor.instances`, `spark.executor.cores`, en `spark.executor.memory`. Een Executor is een proces gestart voor een Spark-toepassing. Het wordt uitgevoerd op hello werkrolknooppunt en is verantwoordelijk toocarry Hallo taken voor de toepassing hello uit. Hallo standaardaantal Executor en Hallo executor grootten voor elk cluster wordt berekend op basis van Hallo aantal worker-knooppunten en Hallo worker knooppuntgrootte. Deze worden opgeslagen in `spark-defaults.conf` op Hallo van head clusterknooppunten.

Hallo drie configuratieparameters kunnen worden geconfigureerd op clusterniveau hello (voor alle toepassingen die worden uitgevoerd op Hallo cluster) of voor elke afzonderlijke toepassing ook kunnen worden opgegeven.

### <a name="change-hello-parameters-using-ambari-ui"></a>Hallo-parameters met Ambari UI wijzigen
1. Hallo Ambari UI Klik **Spark**, klikt u op **Configs**, en vouw vervolgens **aangepaste spark-standaardwaarden**.

    ![Parameters instellen met Ambari](./media/hdinsight-apache-spark-resource-manager/set-parameters-using-ambari.png)
2. Hallo standaardwaarden zijn goede toohave 4 Spark scala-toepassingen op Hallo cluster gelijktijdig worden uitgevoerd. U kunt wijzigingen deze waarden via de gebruikersinterface hello, zoals hieronder wordt weergegeven.

    ![Parameters instellen met Ambari](./media/hdinsight-apache-spark-resource-manager/set-executor-parameters.png)
3. Klik op **opslaan** toosave Hallo configuratiewijzigingen. Bovenaan Hallo Hallo pagina, wordt u gevraagd alle Hallo toorestart betrokken services. Klik op **opnieuw**.

    ![Services opnieuw starten](./media/hdinsight-apache-spark-resource-manager/restart-services.png)

### <a name="change-hello-parameters-for-an-application-running-in-jupyter-notebook"></a>Hallo-parameters voor een toepassing die wordt uitgevoerd in Jupyter-notebook wijzigen
Voor toepassingen die worden uitgevoerd in de Jupyter-notebook hello, kunt u Hallo `%%configure` magic toomake Hallo configuratiewijzigingen. In het ideale geval moet u deze wijzigingen aanbrengen aan Hallo begin van de toepassing hello, voordat u uw eerste codecel uitvoert. Dit zorgt ervoor dat configuration Hallo toegepaste toohello Livy-sessie wanneer deze wordt gemaakt. Als u wilt dat toochange Hallo configuratie op een later stadium in de toepassing hello, moet u Hallo `-f` parameter. Hierdoor alle voortgang in Hallo wordt toepassing wel verloren.

Hallo codefragment hieronder ziet u hoe toochange configuratie voor een toepassing die wordt uitgevoerd in Jupyter Hallo.

    %%configure
    {"executorMemory": "3072M", "executorCores": 4, "numExecutors":10}

Parameters voor de configuratie moeten worden doorgegeven als een JSON-tekenreeks en moeten op de volgende regel Hallo na het Hallo-magic, zoals weergegeven in Hallo voorbeeldkolom.

### <a name="change-hello-parameters-for-an-application-submitted-using-spark-submit"></a>Wijziging Hallo parameters voor een toepassing die wordt verzonden met verzenden spark
Na de opdracht is een voorbeeld van hoe toochange configuratieparameters voor een batch-toepassing die wordt verzonden met behulp van Hallo `spark-submit`.

    spark-submit --class <hello application class tooexecute> --executor-memory 3072M --executor-cores 4 –-num-executors 10 <location of application jar file> <application parameters>

### <a name="change-hello-parameters-for-an-application-submitted-using-curl"></a>Hallo-parameters voor een toepassing die wordt verzonden met cURL wijzigen
Na de opdracht is een voorbeeld van hoe toochange configuratieparameters voor een batch-toepassing die wordt verzonden met behulp van cURL Hallo.

    curl -k -v -H 'Content-Type: application/json' -X POST -d '{"file":"<location of application jar file>", "className":"<hello application class tooexecute>", "args":[<application parameters>], "numExecutors":10, "executorMemory":"2G", "executorCores":5' localhost:8998/batches

### <a name="how-do-i-change-these-parameters-on-a-spark-thrift-server"></a>Hoe kan ik deze parameters op een Spark Thrift-Server wijzigen?
Spark Thrift-Server JDBC/ODBC toegang tooa Spark-cluster en gebruikte tooservice Spark SQL-query's is. Hulpprogramma's zoals Power BI, Tableau enzovoort. ODBC-protocol toocommunicate met Spark Thrift-Server tooexecute Spark SQL-query's gebruiken als een Spark-toepassing. Wanneer een Spark-cluster is gemaakt, twee exemplaren van Hallo Spark Thrift-Server zijn gestart, één op elke hoofdknooppunt. Elke Spark Thrift-Server wordt weergegeven als een Spark-toepassing in de gebruikersinterface van YARN Hallo.

Spark Thrift-Server gebruikt dynamische executor toewijzing Spark en daarom Hallo `spark.executor.instances` wordt niet gebruikt. In plaats daarvan Spark Thrift-Server gebruikt `spark.dynamicAllocation.minExecutors` en `spark.dynamicAllocation.maxExecutors` toospecify Hallo executor count. Hallo configuratieparameters `spark.executor.cores` en `spark.executor.memory` is toomodify Hallo executor grootte gebruikt. U kunt deze parameters kunt wijzigen, zoals hieronder wordt weergegeven.

* Vouw Hallo **geavanceerde spark-thrift-sparkconf** categorie tooupdate Hallo parameters `spark.dynamicAllocation.minExecutors`, `spark.dynamicAllocation.maxExecutors`, en `spark.executor.memory`.

    ![Spark thrift-server configureren](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-1.png)    
* Vouw Hallo **aangepaste spark thrift sparkconf** categorie tooupdate Hallo parameter `spark.executor.cores`.

    ![Spark thrift-server configureren](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-2.png)

### <a name="how-do-i-change-hello-driver-memory-of-hello-spark-thrift-server"></a>Hoe wijzig ik Hallo stuurprogramma geheugen Hallo Spark Thrift-Server?
Spark Thrift-Server stuurprogramma geheugen is % van de geconfigureerde too25 met een grootte voor het hoofdknooppunt RAM-geheugen van Hallo opgegeven Hallo totale RAM-geheugen van het hoofdknooppunt Hallo groter dan 14GB is. U kunt Hallo Ambari UI toochange Hallo stuurprogramma geheugenconfiguratie, zoals hieronder wordt weergegeven.

* Hallo Ambari UI Klik **Spark**, klikt u op **Configs**, vouw **spark env geavanceerde**, en geef vervolgens de waarde voor Hallo **spark_thrift_cmd_opts**.

    ![RAM-geheugen voor Spark thrift-server configureren](./media/hdinsight-apache-spark-resource-manager/spark-thrift-server-ram.png)

## <a name="i-do-not-use-bi-with-spark-cluster-how-do-i-take-hello-resources-back"></a>Ik gebruik geen BI met Spark-cluster. Hoe ik Hallo resources terug uitvoeren?
Aangezien we de dynamische toewijzing Spark gebruiken, zijn hello alleen de resources die worden verbruikt door thrift-server Hallo bronnen voor Hallo twee toepassing modellen. tooreclaim deze resources die moet u stoppen Hallo services Thrift-Server op Hallo-cluster.

1. Hallo Ambari UI, in het linkerdeelvenster hello, klik op **Spark**.
2. Klik in de volgende pagina Hallo op **Spark Thrift Servers**.

    ![Thrift-server opnieuw opstarten](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-1.png)
3. Hier ziet u twee Hallo-headnodes welke Hallo Spark Thrift-Server wordt uitgevoerd. Klik op een Hallo headnodes.

    ![Thrift-server opnieuw opstarten](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-2.png)
4. de volgende pagina Hallo geeft een lijst van alle Hallo services worden uitgevoerd op die headnode. In de lijst Hallo Hallo vervolgkeuzeknop volgende tooSpark Thrift-Server op en klik op **stoppen**.

    ![Thrift-server opnieuw opstarten](./media/hdinsight-apache-spark-resource-manager/restart-thrift-server-3.png)
5. Herhaal deze stappen op Hallo ook andere headnode.

## <a name="my-jupyter-notebooks-are-not-running-as-expected-how-can-i-restart-hello-service"></a>Mijn Jupyter-notebooks niet worden uitgevoerd zoals verwacht. Hoe kan ik Hallo-service opnieuw starten?
Start Hallo Ambari-Webgebruikersinterface zoals hierboven. Hallo navigatiedeelvenster links, klik op **Jupyter**, klikt u op **serviceacties**, en klik vervolgens op **start opnieuw alle**. Hiermee start u Hallo Jupyter-service op alle Hallo headnodes.

    ![Restart Jupyter](./media/hdinsight-apache-spark-resource-manager/restart-jupyter.png "Restart Jupyter")

## <a name="how-do-i-know-if-i-am-running-out-of-resources"></a>Hoe weet ik of mijn onvoldoende resources werkt systeem?
Start de gebruikersinterface van Yarn Hallo zoals hierboven. In de tabel van de Cluster metrische gegevens boven op het welkomstscherm, controleert u de waarden van **geheugen gebruikt** en **Totaal geheugen** kolommen. Als de waarden Hallo 2 bijna, er mogelijk niet voldoende bronnen toostart Hallo volgende toepassing. Hallo geldt toohello **VCores gebruikt** en **VCores totaal** kolommen. Ook in de hoofdweergave hello, als er een toepassing gebleven **GEACCEPTEERDE** status en niet in een overgang **met** noch **mislukt** staat, dit kan ook wel een indicatie deze is niet voldoende bronnen toostart ophalen.

    ![Resource Limit](./media/hdinsight-apache-spark-resource-manager/resource-limit.png "Resource Limit")

## <a name="how-do-i-kill-a-running-application-toofree-up-resource"></a>Hoe kill een actieve toepassing toofree bron?
1. Klik in de gebruikersinterface van Yarn Hallo van het linkerpaneel Hallo, op **met**. Bepalen in lijst van actieve toepassingen Hallo Hallo toepassing toobe afgesloten en klik op Hallo **ID**.

    ![Kill App1](./media/hdinsight-apache-spark-resource-manager/kill-app1.png "App1 afsluiten")

2. Klik op **toepassing Kill** op Hallo rechterbovenhoek, klik vervolgens op **OK**.

    ![Kill App2](./media/hdinsight-apache-spark-resource-manager/kill-app2.png "App2 afsluiten")

## <a name="see-also"></a>Zie ook
* [Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen](hdinsight-apache-spark-job-debugging.md)

### <a name="for-data-analysts"></a>Voor gegevensanalisten

* [Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Websitelogboekanalyse met Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)
* [Analyse van Application Insights-telemetriegegevens met behulp van Spark in HDInsight](hdinsight-spark-analyze-application-insight-logs.md)
* [Gebruik Caffe op Azure HDInsight Spark voor gedistribueerde grondige learning](hdinsight-deep-learning-caffe-spark.md)

### <a name="for-spark-developers"></a>Voor Spark-ontwikkelaars

* [Een zelfstandige toepassing maken met behulp van Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy](hdinsight-apache-spark-livy-rest-interface.md)
* [De invoegtoepassing HDInsight Tools voor IntelliJ IDEA toocreate en verzenden van Spark Scala-toepassingen](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen](hdinsight-apache-spark-eventhub-streaming.md)
* [De invoegtoepassing HDInsight Tools for IntelliJ IDEA toodebug Spark applications op afstand gebruiken](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Externe pakketten gebruiken met Jupyter-notebooks](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster](hdinsight-apache-spark-jupyter-notebook-install-locally.md)
