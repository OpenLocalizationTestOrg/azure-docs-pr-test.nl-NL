---
title: 'Azure Toolkit voor IntelliJ: fouten opsporen in Spark scala-toepassingen op afstand via SSH | Microsoft Docs'
description: Stapsgewijze instructies voor hoe toouse HDInsight-hulpprogramma's in Azure Toolkit voor IntelliJ toodebug toepassingen op afstand op HDInsight-clusters via SSH
keywords: foutopsporing op afstand intellij, externe foutopsporing intellij, ssh, intellij, hdinsight, fouten opsporen in intellij, foutopsporing
services: hdinsight
documentationcenter: 
author: jejiang
manager: DJ
editor: Jenny Jiang
tags: azure-portal
ms.assetid: 
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: 
ms.devlang: 
ms.topic: article
ms.date: 08/24/2017
ms.author: Jenny Jiang
ms.openlocfilehash: bf3ab9d04c2ff9fcb6bbbdeefb11f55a12fbd845
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="debug-spark-applications-on-an-hdinsight-cluster-with-azure-toolkit-for-intellij-through-ssh"></a>Fouten opsporen in Spark scala-toepassingen op een HDInsight-cluster in Azure werkset voor IntelliJ via SSH

In dit artikel vindt u stapsgewijze instructies voor het HDInsight-hulpprogramma's in Azure Toolkit toouse voor IntelliJ toodebug toepassingen op afstand op een HDInsight-cluster. toodebug uw project, kunt u ook Hallo weergeven [fouten opsporen in HDInsight Spark-toepassingen met Azure Toolkit voor IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ) video.

**Vereisten**

* **HDInsight-hulpprogramma's in Azure Toolkit voor IntelliJ**. Dit hulpprogramma maakt deel uit van Azure Toolkit voor IntelliJ. Zie voor meer informatie [Azure Toolkit installeren voor IntelliJ](https://docs.microsoft.com/en-us/azure/azure-toolkit-for-intellij-installation).
* **Azure Toolkit voor IntelliJ**. Deze toolkit toocreate Spark scala-toepassingen gebruiken voor een HDInsight-cluster. Voor meer informatie instructies Hallo in [gebruik Azure Toolkit voor IntelliJ toocreate Spark scala-toepassingen voor een HDInsight-cluster](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-plugin).
* **HDInsight SSH-service met gebruikersnaam en wachtwoord management**. Zie voor meer informatie [tooHDInsight (Hadoop) verbinding via SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) en [SSH gebruiken tunneling tooaccess Ambari web-UI, JobHistory, NameNode, Oozie en andere web-UI](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-linux-ambari-ssh-tunnel). 
 

## <a name="create-a-spark-scala-application-and-configure-it-for-remote-debugging"></a>Een Spark Scala-toepassing maken en te configureren voor foutopsporing op afstand

1. Start IntelliJ IDEA en maak vervolgens een project. In Hallo **nieuw Project** dialoogvenster vak, Hallo te volgen:

   a. Selecteer **HDInsight**. 

   b. Selecteer een Java of Scala sjabloon op basis van uw voorkeur. Selecteer tussen Hallo volgende opties:

      - **Spark in HDInsight (Scala)**

      - **Spark in HDInsight (Java)**

      - **Spark in HDInsight-Cluster uitvoeren voorbeeld (Scala)**

      In dit voorbeeld wordt een **Spark in HDInsight-Cluster uitvoeren voorbeeld (Scala)** sjabloon.

   c. In Hallo **Build hulpprogramma** lijst, selecteert u Hallo te volgen, op basis van tooyour nodig:

      - **Maven**, voor ondersteuning van de wizard Scala project maken

      -  **SBT**, voor het beheren van Hallo afhankelijkheden en bouwen voor Hallo Scala project 

      ![Een debug-project maken](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-create-projectfor-debug-remotely.png)

   d. Selecteer **volgende**.     
 
3. In Hallo volgende **nieuw Project** venster Hallo te volgen:

   ![Selecteer Hallo Spark-SDK](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-new-project.png)

   a. Voer een naam van het project en de projectlocatie.

   b. In Hallo **Project SDK** vervolgkeuzelijst, selecteer **Java 1.8** voor **2.x Spark** cluster of selecteer **Java 1.7** voor **Spark 1. x** cluster.

   c. In Hallo **Spark versie** vervolgkeuzelijst, Hallo Scala project maken wizard integreert de juiste versie Hallo voor Spark SDK en Scala SDK. Als Hallo spark-cluster versie ouder dan 2.0 is, selecteert u **Spark 1.x**. Selecteer anders **2.x Spark.** In dit voorbeeld wordt **Spark 2.0.2 (Scala 2.11.8)**.

   d. Selecteer **Voltooien**.

4. Selecteer **src** > **belangrijkste** > **scala** tooopen uw code in Hallo-project. In dit voorbeeld wordt Hallo **SparkCore_wasbloTest** script.

5. Hallo tooaccess **configuraties bewerken** menu, selecteer Hallo-pictogram in de rechterbovenhoek Hallo. U kunt vanuit dit menu maken of bewerken Hallo configuraties voor foutopsporing op afstand.

   ![Configuraties bewerken](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-edit-configurations.png) 

6. In Hallo **uitvoeren/Debug configuraties** in het dialoogvenster, selecteer Hallo plus -teken (**+**). Selecteer vervolgens Hallo **Submit Spark Job** optie.

   ![Nieuwe configuratie toevoegen](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-add-new-Configuration.png)
7. Geef gegevens voor **naam**, **Spark-cluster**, en **Main klassenaam**. Selecteer vervolgens **geavanceerde configuratie**. 

   ![Configuraties voor foutopsporing uitvoeren](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-run-debug-configurations.png)

8. In Hallo **Spark verzending van geavanceerde configuratie** dialoogvenster, **foutopsporing op afstand inschakelen Spark**. Hallo-SSH-gebruikersnaam invoeren en een wachtwoord invoeren of een bestand met een persoonlijke sleutel gebruiken. toosave hello configuratie, selecteert u **OK**.

   ![Spark foutopsporing op afstand inschakelen](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-enable-spark-remote-debug.png)

9. Hallo-configuratie wordt nu opgeslagen met de Hallo-naam die u hebt opgegeven. tooview configuratiedetails hello, selecteer Hallo configuratienaam. toomake gewijzigd, schakelt u **configuraties bewerken**. 

10. Nadat u de configuratie-instellingen Hallo hebt voltooid, kunt u Hallo-project uitvoeren op externe Hallo-cluster of foutopsporing op afstand uitvoeren.

## <a name="learn-how-tooperform-remote-debugging"></a>Meer informatie over hoe foutopsporing op afstand tooperform
### <a name="scenario-1-perform-remote-run"></a>Scenario 1: Extern uitvoeren uitvoeren

In deze sectie wordt uitgelegd hoe u dat toodebug stuurprogramma's en Executor.

    import org.apache.spark.{SparkConf, SparkContext}

    object LogQuery {
      val exampleApacheLogs = List(
        """10.10.10.10 - "FRED" [18/Jan/2013:17:56:07 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 315 "http://referall.com/" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.350 "-" - "" 265 923 934 ""
          | 62.24.11.25 images.com 1358492167 - Whatup""".stripMargin.lines.mkString,
        """10.10.10.10 - "FRED" [18/Jan/2013:18:02:37 +1100] "GET http://images.com/2013/Generic.jpg
          | HTTP/1.1" 304 306 "http:/referall.com" "Mozilla/4.0 (compatible; MSIE 7.0; Windows NT 5.1;
          | GTB7.4; .NET CLR 2.0.50727; .NET CLR 3.0.04506.30; .NET CLR 3.0.04506.648; .NET CLR
          | 3.5.21022; .NET CLR 3.0.4506.2152; .NET CLR 1.0.3705; .NET CLR 1.1.4322; .NET CLR
          | 3.5.30729; Release=ARP)" "UD-1" - "image/jpeg" "whatever" 0.352 "-" - "" 256 977 988 ""
          | 0 73.23.2.15 images.com 1358492557 - Whatup""".stripMargin.lines.mkString
      )
      def main(args: Array[String]) {
        val sparkconf = new SparkConf().setAppName("Log Query")
        val sc = new SparkContext(sparkconf)
        val dataSet = sc.parallelize(exampleApacheLogs)
        // scalastyle:off
        val apacheLogRegex =
          """^([\d.]+) (\S+) (\S+) \[([\w\d:/]+\s[+\-]\d{4})\] "(.+?)" (\d{3}) ([\d\-]+) "([^"]+)" "([^"]+)".*""".r
        // scalastyle:on
        /** Tracks hello total query count and number of aggregate bytes for a particular group. */
        class Stats(val count: Int, val numBytes: Int) extends Serializable {
          def merge(other: Stats): Stats = new Stats(count + other.count, numBytes + other.numBytes)
          override def toString: String = "bytes=%s\tn=%s".format(numBytes, count)
        }
        def extractKey(line: String): (String, String, String) = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              if (user != "\"-\"") (ip, user, query)
              else (null, null, null)
            case _ => (null, null, null)
          }
        }
        def extractStats(line: String): Stats = {
          apacheLogRegex.findFirstIn(line) match {
            case Some(apacheLogRegex(ip, _, user, dateTime, query, status, bytes, referer, ua)) =>
              new Stats(1, bytes.toInt)
            case _ => new Stats(1, 0)
          }
        }
        
        dataSet.map(line => (extractKey(line), extractStats(line)))
          .reduceByKey((a, b) => a.merge(b))
          .collect().foreach{
          case (user, query) => println("%s\t%s".format(user, query))}

        sc.stop()
      }
    }


1. Dingen instellen en selecteer vervolgens Hallo **Debug** pictogram.

   ![Selecteer Hallo debug-pictogram](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-icon.png)

2. Als de uitvoering van het programma Hallo Hallo belangrijk punt bereikt, ziet u een **stuurprogramma** tabblad en de twee **Executor** tabbladen in Hallo **foutopsporingsprogramma** deelvenster. Selecteer Hallo **hervatten programma** pictogram toocontinue Hallo code, die vervolgens de volgende onderbrekingspunt Hallo bereikt en is gericht op Hallo overeenkomt met **Executor** tabblad. U kunt logboekbestanden voor het uitvoeren voor overeenkomende Hallo Hallo bekijken **Console** tabblad.

   ![Tabblad foutopsporing](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debugger-tab.png)

### <a name="scenario-2-perform-remote-debugging-and-bug-fixing"></a>Scenario 2: Voer foutopsporing op afstand en het verhelpen van problemen
In deze sectie zien we u hoe toodynamically update Hallo variabelewaarde met behulp van Hallo IntelliJ foutopsporing mogelijkheid voor een eenvoudige oplossing. In de Hallo volgende codevoorbeeld, wordt een uitzondering opgetreden omdat Hallo doelbestand al bestaat.
  
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext

        object SparkCore_WasbIOTest {
          def main(arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("SparkCore_WasbIOTest")
            val sc = new SparkContext(conf)
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

            // Find hello rows that have only one digit in hello sixth column.
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)

            try {
              var target = "wasb:///HVACout2_testdebug1";
              rdd1.saveAsTextFile(target);
            } catch {
              case ex: Exception => {
                throw ex;
              }
            }
          }
        }


#### <a name="tooperform-remote-debugging-and-bug-fixing"></a>foutopsporing op afstand tooperform en het verhelpen van problemen
1. Twee dingen instellen en selecteer vervolgens Hallo **Debug** pictogram toostart Hallo proces foutopsporing op afstand.

2. Hallo-code reageert op Hallo eerste belangrijk punt en Hallo-parameter en de variabele gegevens worden weergegeven in Hallo **variabelen** deelvenster. 

3. Selecteer Hallo **hervatten programma** pictogram toocontinue. Hallo-code reageert op Hallo tweede punt. Hallo-uitzondering is opgetreden, zoals verwacht.

  ![Genereert fout](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-throw-error.png) 

4. Selecteer Hallo **hervatten programma** pictogram opnieuw. Hallo **HDInsight Spark verzending** venster een fout met 'job run is mislukt' weergegeven.

  ![Verzending van de fout](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-error-submission.png) 

5. toodynamically update Hallo variabelewaarde via Hallo IntelliJ foutopsporing functie, selecteer **Debug** opnieuw. Hallo **variabelen** deelvenster opnieuw wordt weergegeven. 

6. Klik met de rechtermuisknop Hallo doel op Hallo **Debug** tabblad en selecteer vervolgens **waarde instellen**. Voer vervolgens een nieuwe waarde voor Hallo-variabele. Selecteer vervolgens **Enter** toosave Hallo waarde. 

  ![Waarde instellen](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-set-value.png) 

7. Selecteer Hallo **hervatten programma** pictogram toocontinue toorun Hallo programma. Dit moment is geen uitzondering opgetreden. U kunt zien dat Hallo-project met succes wordt uitgevoerd zonder eventuele uitzonderingen.

  ![Fouten opsporen in zonder uitzondering](./media/hdinsight-apache-spark-intellij-tool-debug-remotely/hdinsight-debug-without-exception.png)

## <a name="seealso"></a>Volgende stappen
* [Overzicht: Apache Spark in Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>Demo
* Maak Scala project (video): [Spark Scala-toepassingen maken](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)
* Foutopsporing op afstand (video): [gebruik Azure Toolkit voor IntelliJ toodebug Spark scala-toepassingen op afstand op een HDInsight-cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

### <a name="scenarios"></a>Scenario's
* [Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools](hdinsight-apache-spark-use-bi-tools.md)
* [Spark met Machine Learning: Spark in HDInsight tooanalyze bouwen met behulp van HVAC-gegevens temperatuur gebruiken](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark-Streaming: Spark in HDInsight toobuild realtime streamingtoepassingen gebruiken](hdinsight-apache-spark-eventhub-streaming.md)
* [Websitelogboekanalyse met Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Toepassingen maken en uitvoeren
* [Een zelfstandige toepassing maken met behulp van Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Tools en uitbreidingen
* [Gebruik Azure Toolkit voor IntelliJ toocreate Spark scala-toepassingen voor een HDInsight-cluster](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Gebruik Azure Toolkit voor IntelliJ toodebug Spark scala-toepassingen op afstand via VPN-verbinding](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Gebruik van HDInsight Tools voor IntelliJ met Hortonworks Sandbox](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [HDInsight-hulpprogramma's gebruiken in Azure Toolkit voor Eclipse toocreate Spark scala-toepassingen](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight Hallo](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Externe pakketten gebruiken met Jupyter-notebooks](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Resources beheren
* [Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen](hdinsight-apache-spark-job-debugging.md)
