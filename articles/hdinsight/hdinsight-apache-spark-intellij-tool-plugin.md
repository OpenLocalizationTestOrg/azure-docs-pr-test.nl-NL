---
title: 'Azure Toolkit voor IntelliJ: Spark toepassingen maken voor een HDInsight-cluster | Microsoft Docs'
description: Hello Azure Toolkit gebruiken voor Spark scala-toepassingen voor IntelliJ toodevelop is geschreven in Scala en verzend deze tooan HDInsight Spark-cluster.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 73304272-6c8b-482e-af7c-cd25d95dab4d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 22cce014bb848a54e198e77a50bf13448012310e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-intellij-toocreate-spark-applications-for-an-hdinsight-cluster"></a>Gebruik Azure Toolkit voor IntelliJ toocreate Spark scala-toepassingen voor een HDInsight-cluster

Gebruik hello Azure Toolkit voor IntelliJ invoegtoepassing toodevelop Spark toepassingen geschreven in Scala en deze vervolgens verzenden tooan HDInsight Spark-cluster rechtstreeks vanuit Hallo IntelliJ integrated development environment (IDE). U kunt Hallo invoegtoepassing in een aantal manieren gebruiken:

* Ontwikkelen en het verzenden van een Scala Spark-toepassing op een HDInsight Spark-cluster.
* Toegang tot de bronnen van uw Azure HDInsight Spark-cluster.
* Ontwikkelen en een Scala Spark-toepassing lokaal uitvoeren.

toocreate van uw project, weergave Hallo [Spark scala-toepassingen maken met hello Azure Toolkit voor IntelliJ](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ) video.

> [!IMPORTANT]
> U kunt deze invoegtoepassing toocreate gebruiken en verzenden van toepassingen alleen voor een HDInsight Spark-cluster op Linux.
> 

## <a name="prerequisites"></a>Vereisten

- Een Apache Spark-cluster in HDInsight Linux. Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
- Oracle Java Development Kit. U kunt deze installeren via Hallo [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
- IntelliJ IDEA. In dit artikel gebruikt versie 2017.1. U kunt deze installeren via Hallo [JetBrains website](https://www.jetbrains.com/idea/download/).

## <a name="install-azure-toolkit-for-intellij"></a>Azure Toolkit voor IntelliJ installeren
Zie voor installatie-instructies [Azure Toolkit installeren voor IntelliJ](../azure-toolkit-for-intellij-installation.md).

## <a name="sign-in-tooyour-azure-subscription"></a>Meld u aan tooyour Azure-abonnement

1. Hallo IntelliJ IDE Start en Azure Explorer te openen. Op Hallo **weergave** selecteert u **hulpprogramma Windows**, en selecteer vervolgens **Azure Explorer**.
       
   ![Hello Azure Explorer-koppeling](./media/hdinsight-apache-spark-intellij-tool-plugin/show-azure-explorer.png)

2. Klik met de rechtermuisknop Hallo **Azure** knooppunt en selecteer vervolgens **aanmelden**.

3. In Hallo **Azure aanmelden** dialoogvenster, **aanmelden**, en voer uw Azure-referenties.

    ![Hello Azure teken in het dialoogvenster](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-2.png)

4. Nadat u bent aangemeld, Hallo **Selecteer abonnementen** dialoogvenster lijsten alle Azure-abonnementen die zijn gekoppeld aan Hallo Hallo referenties. Selecteer Hallo **Selecteer** knop.

    ![dialoogvenster Hallo-abonnementen selecteren](./media/hdinsight-apache-spark-intellij-tool-plugin/Select-Subscriptions.png)

5. Op Hallo **Azure Explorer** tabblad uit, vouw **HDInsight** tooview-Hallo HDInsight Spark-clusters die zich in uw abonnement.
   
    ![HDInsight Spark-clusters in Azure Explorer](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-3.png)

6. tooview hello resources (bijvoorbeeld opslagaccounts) die gekoppeld aan cluster hello zijn, u kunt een naam van de cluster-knooppunt verder uitbreiden.
   
    ![Een uitgebreide naam van de cluster-knooppunt](./media/hdinsight-apache-spark-intellij-tool-plugin/view-explorer-4.png)

## <a name="run-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a>Een Spark Scala-toepassing uitvoeren op een HDInsight Spark-cluster

1. Start IntelliJ IDEA en maak vervolgens een project. In Hallo **nieuw Project** dialoogvenster vak, Hallo te volgen: 

   a. Selecteer **HDInsight** > **Spark in HDInsight (Scala)**.

   b. In Hallo **Build hulpprogramma** lijst, selecteert u Hallo te volgen, op basis van tooyour nodig:

      * **Maven**, voor ondersteuning van de wizard Scala project maken
      * **SBT**, voor het beheren van Hallo afhankelijkheden en bouwen voor Hallo Scala project

    ![het dialoogvenster Nieuw Project Hallo](./media/hdinsight-apache-spark-intellij-tool-plugin/create-hdi-scala-app.png)

2. Selecteer **volgende**.

3. Hallo Scala maken van het project wizard detecteert automatisch of u Hallo Scala invoegtoepassing hebt geïnstalleerd. Selecteer **installeren**.

   ![Controle van de invoegtoepassing scala](./media/hdinsight-apache-spark-intellij-tool-plugin/Scala-Plugin-check-Reminder.PNG) 

4. toodownload hello Scala invoegtoepassing, selecteer **OK**. Ga als volgt Hallo instructies toorestart IntelliJ. 

   ![Hallo Scala invoegtoepassing installatievenster](./media/hdinsight-apache-spark-intellij-tool-plugin/Choose-Scala-Plugin.PNG)

5. In Hallo **nieuw Project** venster Hallo te volgen:  

    ![Hallo Spark SDK selecteren](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-new-project.png)

   a. Voer een naam en locatie.

   b. In Hallo **Project SDK** vervolgkeuzelijst, selecteer **Java 1.8** voor Hallo Spark 2.x-cluster, of selecteer **Java 1.7** voor Hallo Spark 1.x-cluster.

   c. In Hallo **Spark versie** vervolgkeuzelijst, wizard voor het maken van project Scala integreert de juiste versie Hallo voor Spark SDK en Scala SDK. Als Hallo Spark-cluster versie ouder dan 2.0 is, selecteert u **Spark 1.x**. Selecteer anders **Spark2.x**. In dit voorbeeld wordt **Spark 2.0.2 (Scala 2.11.8)**.

6. Selecteer **Voltooien**.

7. een artefact Hallo Spark project automatisch voor u gemaakt. tooview hello artefacten, Hallo te volgen:

   a. Op Hallo **bestand** selecteert u **projectstructuur**.

   b. In Hallo **projectstructuur** dialoogvenster, **artefacten** tooview Hallo standaard artefacten die wordt gemaakt. U kunt ook uw eigen artefacten maken door het selecteren van Hallo plus -teken (**+**).

      ![Gegevens in het dialoogvenster Hallo artefact](./media/hdinsight-apache-spark-intellij-tool-plugin/default-artifact.png)
      
8. De broncode van uw toepassing toevoegen door Hallo volgende te doen:

   a. In Projectverkenner met de rechtermuisknop op **src**, wijst u te**nieuw**, en selecteer vervolgens **Scala klasse**.
      
      ![Opdrachten voor het maken van een klasse Scala van Projectverkenner](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code.png)

   b. In Hallo **nieuwe Scala klasse maken** dialoogvenster vak, Geef een naam op, selecteer **Object** in Hallo **soort** vak en selecteer vervolgens **OK**.
      
      ![Dialoogvenster Nieuwe Scala klasse maken](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-scala-code-object.png)

   c. In Hallo **MyClusterApp.scala** bestand, plak Hallo code te volgen. Hallo code Hallo gegevens leest uit HVAC.csv (beschikbaar op alle HDInsight Spark-clusters), haalt Hallo rijen met slechts één cijfer in Hallo zevende kolom in Hallo CSV-bestand, en schrijft Hallo uitvoer te**/HVACOut** onder Hallo-standaard Storage-container voor Hallo-cluster.

        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
    
        object MyClusterApp{
            def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
    
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
    
            //find hello rows that have only one digit in hello seventh column in hello CSV file
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
    
            rdd1.saveAsTextFile("wasb:///HVACOut")
            }
    
        }

9. Hallo-toepassing uitvoeren op een HDInsight Spark-cluster door Hallo volgende te doen:

   a. In Projectverkenner met de rechtermuisknop op de projectnaam Hallo en selecteer vervolgens **indienen Spark toepassing tooHDInsight**.
      
      ![Hallo indienen Spark toepassing tooHDInsight opdracht](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-1.png)

   b. U na vragen aan gebruiker tooenter zijn de referenties van uw Azure-abonnement. In Hallo **Spark verzending** in het dialoogvenster Hallo volgende waarden bevatten, en selecteer vervolgens **indienen**.
      
      * Voor **Spark-clusters (alleen voor Linux)**, selecteer Hallo HDInsight Spark-cluster waarop toorun uw toepassing.

      * Selecteer een artefact uit Hallo IntelliJ project of Selecteer een van de vaste schijf Hallo.

      * In Hallo **Main klassenaam** vak, selecteer Hallo weglatingsteken (**...** ), selecteer Hallo hoofdklasse in de broncode van uw toepassing en selecteer vervolgens **OK**.

        ![dialoogvenster voor Hallo Main-klasse selecteren](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-3.png)

      * Omdat de toepassingscode Hallo in dit voorbeeld geen opdrachtregelargumenten vereist of verwijzen naar potten of bestanden, kunt u Hallo resterende selectievakjes leeg laten. Nadat u Hallo informatie te verstrekken, eruit dialoogvenster Hallo Hallo installatiekopie te volgen.
        
        ![Hallo Spark verzending van het dialoogvenster](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-submit-spark-app-2.png)

   c. Hallo **Spark verzending** op Hallo onderaan Hallo venster tabblad moet beginnen met het Hallo de voortgang weergeven. U kunt ook Hallo toepassing stoppen Hallo rode knop selecteren in Hallo **Spark verzending** venster.
      
      ![Hallo Spark verzending venster](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-result.png)
      
      toolearn hoe tooaccess Hallo taakuitvoer, raadpleegt u Hallo ' toegang en HDInsight Spark-clusters beheren met behulp van Azure Toolkit voor IntelliJ ' verderop in dit artikel.

## <a name="run-or-debug-a-spark-scala-application-on-an-hdinsight-spark-cluster"></a>Uitvoeren of fouten opsporen in een Spark Scala-toepassing op een HDInsight Spark-cluster
Aangeraden wordt ook een andere manier om Hallo Spark toepassing toohello-cluster in te dienen. U kunt dit doen Hallo parameters door in te stellen Hallo **uitvoeren/Debug configuraties** IDE. Zie voor meer informatie [op afstand fouten opsporen in Spark scala-toepassingen op een HDInsight-cluster in Azure werkset voor IntelliJ via SSH](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh).

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-azure-toolkit-for-intellij"></a>Toegang tot en HDInsight Spark-clusters beheren met behulp van Azure Toolkit voor IntelliJ
U kunt verschillende bewerkingen kunt uitvoeren met behulp van Azure Toolkit voor IntelliJ.

### <a name="access-hello-job-view"></a>Toegang Hallo taak weergeven
1. Vouw in Azure Explorer **HDInsight**Hallo Spark clusternaam uitvouwen en selecteer vervolgens **taken**.  

    ![Taak weergave knooppunt](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. Klik in het rechterdeelvenster Hallo Hallo **Spark taak weergeven** tabblad geeft alle Hallo-toepassingen die op het Hallo-cluster worden uitgevoerd. Selecteer de naam Hallo van Hallo toepassing waarvoor u toosee meer informatie wenst.

    ![App-details](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)

3. toodisplay actieve taak basisinformatie, houd de muis boven Hallo taakgrafiek. Selecteer een knooppunt op Hallo taakgrafiek tooview Hallo fasen grafiek en informatie die u elke taak die wordt gegenereerd.

    ![Fase taakdetails](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

4. veelgebruikte Logboeken, zoals tooview *stuurprogramma Stderr*, *stuurprogramma Stdout*, en *Directory Info*, selecteer Hallo **logboek** tabblad.

    ![Logboekgegevens](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)

5. U kunt ook Hallo Spark geschiedenis gebruikersinterface en Hallo gebruikersinterface van YARN (op niveau van de toepassing hello) weergeven door een koppeling Hallo boven aan het Hallo-venster te selecteren.

### <a name="access-hello-spark-history-server"></a>Toegang tot Hallo Spark geschiedenis van server
1. Vouw in Azure Explorer **HDInsight**, met de rechtermuisknop op de naam van uw Spark-cluster en selecteer vervolgens **Open Spark geschiedenis UI**. 

2. Wanneer u wordt gevraagd, voer de beheerdersreferenties Hallo-cluster, dat u hebt opgegeven bij het instellen van Hallo-cluster.

3. Op Hallo Spark geschiedenis serverdashboard kunt u Hallo toepassing naam toolook voor Hallo toepassing dat u zojuist hebt voltooid. In Hallo voorafgaand aan code, stelt u de naam van de toepassing hello met behulp van `val conf = new SparkConf().setAppName("MyClusterApp")`. De naam van uw toepassing Spark is daarom **MyClusterApp**.

### <a name="start-hello-ambari-portal"></a>Hallo Ambari portal starten
1. Vouw in Azure Explorer **HDInsight**, met de rechtermuisknop op de naam van uw Spark-cluster en selecteer vervolgens **beheerportal Open Cluster (Ambari)**. 

2. Wanneer u wordt gevraagd, voert u beheerdersreferenties Hallo voor Hallo-cluster. U deze referenties hebt opgegeven tijdens het installatieproces Hallo-cluster.

### <a name="manage-azure-subscriptions"></a>Azure-abonnementen beheren
Azure-Toolkit voor IntelliJ bevat standaard Hallo Spark-clusters van alle uw Azure-abonnementen. Indien nodig, kunt u opgeven dat u wilt dat tooaccess Hallo-abonnementen. 

1. Azure Explorer met de rechtermuisknop op Hallo **Azure** de hoofd-knooppunt en selecteer vervolgens **abonnementen beheren**. 

2. Schakel in het dialoogvenster Hallo Hallo selectievakjes volgende toohello abonnementen u niet wilt dat tooaccess en selecteer vervolgens **sluiten**. U kunt ook selecteren **Afmelden** als u wilt dat toosign buiten uw Azure-abonnement.

## <a name="run-a-spark-scala-application-locally"></a>Een Spark Scala-toepassing lokaal uitvoeren
U kunt Azure Toolkit voor IntelliJ toorun Spark Scala-toepassingen lokaal op uw werkstation. Hallo toepassingen meestal niet nodig hebt toegang tot toocluster resources, zoals de storage-containers en u kunt uitvoeren en lokaal te testen.

### <a name="prerequisite"></a>Vereiste
Terwijl u Hallo lokale Spark Scala-toepassingen op een Windows-computer uitvoert, krijgt u mogelijk een uitzondering, zoals wordt beschreven in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356). Hallo uitzondering doet zich voor omdat WinUtils.exe in Windows ontbreekt. 

tooresolve deze fout [downloaden Hallo uitvoerbare](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa locatie zoals **C:\WinUtils\bin**. Vervolgens voegt u de omgevingsvariabele Hallo **HADOOP_HOME**, en stelt u Hallo-waarde van variabele hello te**C\WinUtils**.

### <a name="run-a-local-spark-scala-application"></a>Een lokale Spark Scala-toepassing uitvoeren
1. IntelliJ IDEA Start en een project maken. 

2. In Hallo **nieuw Project** dialoogvenster vak, Hallo te volgen:
   
    a. Selecteer **HDInsight** > **Spark in HDInsight lokaal uitvoeren voorbeeld (Scala)**.

    b. In Hallo **Build hulpprogramma** lijst, selecteert u Hallo te volgen, op basis van tooyour nodig:

      * **Maven**, voor ondersteuning van de wizard Scala project maken
      * **SBT**, voor het beheren van Hallo afhankelijkheden en bouwen voor Hallo Scala project

    ![het dialoogvenster Nieuw Project Hallo](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run.png)

3. Selecteer **volgende**.
 
4. In het volgende venster hello, Hallo te volgen:
   
    a. Voer een naam en locatie.

    b. In Hallo **Project SDK** vervolgkeuzelijst, selecteert u een Java-versie die is hoger dan versie 1.7.

    c. In Hallo **Spark versie** vervolgkeuzelijst, de versie van de optie Hallo van Scala dat u wilt dat toouse: Scala 2.11.x voor Spark 2.0 of Scala 2.10.x voor Spark 1.6.

    ![het dialoogvenster Nieuw Project Hallo](./media/hdinsight-apache-spark-intellij-tool-plugin/Create-local-project.PNG)

5. Selecteer **Voltooien**.

6. Hallo-sjabloon wordt toegevoegd een voorbeeldcode (**LogQuery**) onder Hallo **src** map die u lokaal op uw computer uitvoeren kunt.
   
    ![Locatie van LogQuery](./media/hdinsight-apache-spark-intellij-tool-plugin/local-app.png)

7. Klik met de rechtermuisknop Hallo **LogQuery** toepassing en selecteer vervolgens **uitvoeren 'LogQuery'**. Op Hallo **uitvoeren** tabblad Hallo onderin, ziet u uitvoer Hallo volgende:
   
   ![Spark toepassing lokale resultaat van uitgevoerde](./media/hdinsight-apache-spark-intellij-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="convert-existing-intellij-idea-applications-toouse-azure-toolkit-for-intellij"></a>Bestaande IntelliJ IDEA toepassingen toouse Azure Toolkit voor IntelliJ converteren
Hallo bestaande Spark Scala-toepassingen die u hebt gemaakt in IntelliJ IDEA toobe compatibel is met de Azure-Toolkit voor IntelliJ kunnen worden geconverteerd. Vervolgens kunt u Hallo invoegtoepassing toosubmit Hallo toepassingen tooan HDInsight Spark-cluster.

1. Voor een bestaande Spark Scala-toepassing die is gemaakt via IntelliJ IDEA, Hallo gekoppeld .iml bestand te openen.

2. In de hoofdmap van het Hallo niveau is een **module** element Hallo volgende:
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4">

   Hallo element tooadd bewerken `UniqueKey="HDInsightTool"` dus die Hallo **module** element ziet eruit als Hallo volgende:
   
        <module org.jetbrains.idea.maven.project.MavenProjectsManager.isMavenModule="true" type="JAVA_MODULE" version="4" UniqueKey="HDInsightTool">

3. Hallo wijzigingen opslaan. Nu moet uw toepassing compatibel zijn met Azure Toolkit voor IntelliJ. U kunt dit testen met de rechtermuisknop op de projectnaam Hallo in Projectverkenner. pop-upmenu Hallo heeft nu Hallo optie **indienen Spark toepassing tooHDInsight**.

## <a name="troubleshooting"></a>Problemen oplossen

### <a name="error-in-local-run-please-use-a-larger-heap-size"></a>Fout bij lokaal uitvoeren: *gebruik een grotere heapgrootte*
Als u een 32-bits Java SDK tijdens de uitvoering van lokale, kunt u in Spark 1.6 Hallo volgende fouten tegenkomen:

    Exception in thread "main" java.lang.IllegalArgumentException: System memory 259522560 must be at least 4.718592E8. Please use a larger heap size.
        at org.apache.spark.memory.UnifiedMemoryManager$.getMaxMemory(UnifiedMemoryManager.scala:193)
        at org.apache.spark.memory.UnifiedMemoryManager$.apply(UnifiedMemoryManager.scala:175)
        at org.apache.spark.SparkEnv$.create(SparkEnv.scala:354)
        at org.apache.spark.SparkEnv$.createDriverEnv(SparkEnv.scala:193)
        at org.apache.spark.SparkContext.createSparkEnv(SparkContext.scala:288)
        at org.apache.spark.SparkContext.<init>(SparkContext.scala:457)
        at LogQuery$.main(LogQuery.scala:53)
        at LogQuery.main(LogQuery.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:57)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:606)
        at com.intellij.rt.execution.application.AppMain.main(AppMain.java:144)

Deze fouten optreden omdat hello, heap-grootte niet groot genoeg zijn voor Spark toorun is. Spark vereist ten minste 471 MB. (Zie voor meer informatie [SPARK 12081](https://issues.apache.org/jira/browse/SPARK-12081).) Een eenvoudige oplossing is toouse een 64-bits Java SDK. U kunt ook Hallo JVM-instellingen in IntelliJ wijzigen door toe te voegen Hallo volgende opties:

    -Xms128m -Xmx512m -XX:MaxPermSize=300m -ea

![Toe te voegen opties toohello vak 'VM options' IntelliJ](./media/hdinsight-apache-spark-intellij-tool-plugin/change-heap-size.png)

## <a name="faq"></a>Veelgestelde vragen
kiest u een toepassing tooAzure Data Lake Store toosubmit **interactief** modus tijdens hello Azure aanmelden. Als u selecteert **automatisch** modus, kunt u een foutmelding krijgt.

![interactief aanmelden](./media/hdinsight-apache-spark-intellij-tool-plugin/interative-signin.png)

Nu we dit heeft opgelost. U kunt een Azure Data Lake Cluster toosubmit uw toepassing met een methode voor aanmelden.

## <a name="feedback-and-known-issues"></a>Feedback en bekende problemen
Op dit moment wordt bekijken Spark uitvoer rechtstreeks niet ondersteund.

Als u suggesties of feedback hebt, of als er problemen optreden wanneer u deze invoegtoepassing gebruikt, een e-mail sturen naar hdivstool@microsoft.com.

## <a name="seealso"></a>Volgende stappen
* [Overzicht: Apache Spark in Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="demo"></a>Demo
* Maak Scala project (video): [Spark Scala-toepassingen maken](https://channel9.msdn.com/Series/AzureDataLake/Create-Spark-Applications-with-the-Azure-Toolkit-for-IntelliJ)
* Foutopsporing op afstand (video): [gebruik Azure Toolkit voor IntelliJ toodebug Spark scala-toepassingen op afstand op HDInsight-Cluster](https://channel9.msdn.com/Series/AzureDataLake/Debug-HDInsight-Spark-Applications-with-Azure-Toolkit-for-IntelliJ)

### <a name="scenarios"></a>Scenario's
* [Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools](hdinsight-apache-spark-use-bi-tools.md)
* [Spark met Machine Learning: Spark in HDInsight tooanalyze bouwen met behulp van HVAC-gegevens temperatuur gebruiken](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark-Streaming: Spark in HDInsight toobuild realtime streamingtoepassingen gebruiken](hdinsight-apache-spark-eventhub-streaming.md)
* [Websitelogboekanalyse met Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a>Maken en uitvoeren van toepassingen
* [Een zelfstandige toepassing maken met behulp van Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Tools en uitbreidingen
* [Gebruik Azure Toolkit voor IntelliJ toodebug Spark scala-toepassingen op afstand via VPN-verbinding](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Gebruik Azure Toolkit voor IntelliJ toodebug Spark scala-toepassingen op afstand via SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Gebruik van HDInsight Tools voor IntelliJ met Hortonworks Sandbox](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [HDInsight-hulpprogramma's gebruiken in Azure Toolkit voor Eclipse toocreate Spark scala-toepassingen](hdinsight-apache-spark-eclipse-tool-plugin.md)
* [Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Externe pakketten gebruiken met Jupyter-notebooks](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a>Resources beheren
* [Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen](hdinsight-apache-spark-job-debugging.md)

