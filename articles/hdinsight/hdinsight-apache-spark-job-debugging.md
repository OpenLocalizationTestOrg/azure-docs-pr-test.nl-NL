---
title: Apache Spark aaaDebug taken die worden uitgevoerd op Azure HDInsight | Microsoft Docs
description: Gebruikersinterface van YARN, Spark-UI en Spark geschiedenis tootrack en foutopsporing servertaken uitgevoerd op een Spark-cluster in Azure HDInsight gebruiken
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 59af05a7-2bd9-44b0-b55f-2438d294198b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 33d352a5773920735aa4e5e8532b78122f381377
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-apache-spark-jobs-running-on-azure-hdinsight"></a>Fouten opsporen in Apache Spark taken uitgevoerd op Azure HDInsight

In dit artikel leert u hoe tootrack en foutopsporing Spark taken worden uitgevoerd op HDInsight-clusters met Hallo gebruikersinterface van YARN Spark-gebruikersinterface en Hallo Spark geschiedenis Server. Voor dit artikel gaat we een Spark-taak met een laptop beschikbaar met Hallo Spark-cluster, **Machine learning: Predictive Analytics op voeding inspectie gegevens met behulp van MLLib**. U kunt stappen hieronder tootrack een toepassing die u verzonden met een andere benadering, bijvoorbeeld hello gebruiken **spark indienen**.

## <a name="prerequisites"></a>Vereisten
U moet Hallo volgende hebben:

* Een Azure-abonnement. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Een Apache Spark-cluster in HDInsight. Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
* U moet hebben gestart Hallo-notebook  **[Machine learning: Predictive Analytics op voeding inspectie gegevens met behulp van MLLib](hdinsight-apache-spark-machine-learning-mllib-ipython.md)**. Voor instructies over het toorun deze laptop, volg Hallo koppeling.  

## <a name="track-an-application-in-hello-yarn-ui"></a>Een toepassing in de gebruikersinterface van YARN Hallo bijhouden
1. Start Hallo gebruikersinterface van YARN. Cluster-blade hello, klikt u op **Cluster-Dashboard**, en klik vervolgens op **YARN**.
   
    ![Gebruikersinterface van YARN starten](./media/hdinsight-apache-spark-job-debugging/launch-yarn-ui.png)
   
   > [!TIP]
   > U kunt ook kunt u ook Hallo gebruikersinterface van YARN van Hallo Ambari UI starten. toolaunch hello Ambari UI, cluster-blade hello, klikt u op **Cluster-Dashboard**, en klik vervolgens op **HDInsight-Cluster-Dashboard**. Hallo Ambari UI, klik op **YARN**, klikt u op **snelkoppelingen**op Hallo active resourcemanager en klik vervolgens op **ResourceManager UI**.    
   > 
   > 
2. Omdat u Hallo Spark taak met Jupyter-notebooks gestart, Hallo toepassing hello naam heeft **remotesparkmagics** (dit is de naam Hallo voor alle toepassingen die worden gestart vanaf Hallo notitieblokken). Klik op Hallo toepassings-ID tegen Hallo toepassing naam tooget meer informatie over het Hallo-taak. Hallo toepassingsweergave wordt gestart.
   
    ![Spark toepassings-ID vinden](./media/hdinsight-apache-spark-job-debugging/find-application-id.png)
   
    Voor dergelijke toepassingen die worden gestart vanuit Jupyter-notebooks Hallo Hallo status is altijd **met** voordat u Hallo notebook afgesloten.
3. Uit de weergave van de toepassing hello, kunt u verder toofind uit Hallo containers die zijn gekoppeld aan het Hallo-Logboeken (stdout/stderr) en toepassing hello inzoomen. U kunt ook Hallo Spark UI starten door te klikken op Hallo bijbehorende toohello koppelen **bijhouden URL**, zoals hieronder weergegeven. 
   
    ![Container logboeken downloaden](./media/hdinsight-apache-spark-job-debugging/download-container-logs.png)

## <a name="track-an-application-in-hello-spark-ui"></a>Bijhouden van een toepassing in Hallo Spark-gebruikersinterface
In Hallo Spark-gebruikersinterface, kunt u inzoomen op Hallo Spark taken die zijn geïnitieerd door Hallo-toepassing die u eerder hebt gestart.

1. toolaunch hello Spark-gebruikersinterface uit de weergave van de toepassing hello, klik op de koppeling Hallo tegen Hallo **bijhouden URL**, zoals weergegeven in de schermopname Hallo hierboven. Hier ziet u alle taken van de Hallo Spark dat door de toepassing hello die wordt uitgevoerd in de Jupyter-notebook Hallo worden gestart.
   
    ![Spark-taken weergeven](./media/hdinsight-apache-spark-job-debugging/view-spark-jobs.png)
2. Klik op Hallo **Executor** toosee verwerking en opslag van gegevens voor elke executor tabblad. U kunt ook de aanroepstack Hallo ophalen door te klikken op Hallo **Thread Dump** koppeling.
   
    ![Spark Executor weergeven](./media/hdinsight-apache-spark-job-debugging/view-spark-executors.png)
3. Klik op Hallo **fasen** toosee Hallo fasen gekoppeld aan de toepassing hello tabblad.
   
    ![Spark fasen weergeven](./media/hdinsight-apache-spark-job-debugging/view-spark-stages.png)
   
    Elk stadium kan hebben meerdere taken waarvoor u Uitvoeringsstatistieken, zoals weergeven kunt hieronder weergegeven.
   
    ![Spark fasen weergeven](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-details.png) 
4. U kunt Hallo fase pagina met details DAG visualisatie starten. Vouw Hallo **DAG visualisatie** koppelen bovenaan Hallo Hallo pagina, zoals hieronder wordt weergegeven.
   
    ![Spark fasen DAG visualisatie weergeven](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-dag-visualization.png)
   
    Vertegenwoordigt de verschillende stadia in Hallo toepassing hello DAG of directe Aclyic grafiek. Elke blauw vak in Hallo grafiek vertegenwoordigt een Spark-bewerking aangeroepen vanuit Hallo-toepassing.
5. Hallo fase pagina met details kunt u ook Hallo toepassing tijdlijnweergave starten. Vouw Hallo **gebeurtenis tijdlijn** koppelen bovenaan Hallo Hallo pagina, zoals hieronder wordt weergegeven.
   
    ![Spark fasen gebeurtenis tijdlijn weergeven](./media/hdinsight-apache-spark-job-debugging/view-spark-stages-event-timeline.png)
   
    Hiermee worden Hallo Spark gebeurtenissen weergegeven in de vorm Hallo van een tijdlijn. Hallo tijdlijnweergave is beschikbaar op drie niveaus tussen jobs binnen een taak en binnen een fase. Hallo afbeelding hierboven vastgelegd Hallo tijdlijnweergave voor een bepaald stadium.
   
   > [!TIP]
   > Als u Hallo selecteert **zoomen inschakelen** selectievakje, kunt u bladeren naar links en naar rechts over Hallo tijdlijnweergave.
   > 
   > 
6. Andere tabbladen in Hallo Spark UI bevatten nuttige informatie over ook Hallo Spark-exemplaar.
   
   * Tabblad opslag - als de toepassing een RDDs maakt vindt u informatie over die in het tabblad Hallo-opslag.
   * Tabblad omgeving - op dit tabblad bevat veel nuttige informatie over uw Spark-exemplaar, zoals Hallo 
     * Versie van scala
     * Gebeurtenislogboek van directory die is gekoppeld aan het Hallo-cluster
     * Het aantal kernen voor toepassing hello executor
     * Enz.

## <a name="find-information-about-completed-jobs-using-hello-spark-history-server"></a>Voor meer informatie over voltooide taken met behulp van Hallo Spark geschiedenis van Server
Zodra een taak is voltooid, wordt Hallo informatie over Hallo taak permanent in Hallo Spark geschiedenis Server.

1. toolaunch hello Spark geschiedenis Server, cluster-blade hello, klikt u op **Cluster-Dashboard**, en klik vervolgens op **Spark geschiedenis Server**.
   
    ![Spark geschiedenis Server starten](./media/hdinsight-apache-spark-job-debugging/launch-spark-history-server.png)
   
   > [!TIP]
   > U kunt ook kunt u ook Hallo Spark geschiedenis Server UI uit Hallo Ambari UI starten. toolaunch hello Ambari UI, cluster-blade hello, klikt u op **Cluster-Dashboard**, en klik vervolgens op **HDInsight-Cluster-Dashboard**. Hallo Ambari UI, klik op **Spark**, klikt u op **snelkoppelingen**, en klik vervolgens op **Spark geschiedenis Server UI**.
   > 
   > 
2. Hier ziet u alle Hallo voltooid toepassingen vermeld. Op een aanvraag-ID toodrill omlaag in een toepassing voor meer informatie.
   
    ![Spark geschiedenis Server starten](./media/hdinsight-apache-spark-job-debugging/view-completed-applications.png)

## <a name="see-also"></a>Zie ook
*  [Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-resource-manager.md)

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


