---
title: Toolkit voor Eclipse - toepassingen voor HDInsight Spark Scala maken aaaAzure | Microsoft Docs
description: HDInsight Tools gebruiken in Azure Toolkit voor Spark scala-toepassingen voor Eclipse toodevelop is geschreven in Scala en deze tooan HDInsight Spark-cluster te verzenden, rechtstreeks vanuit Hallo Eclipse IDE.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f6c79550-5803-4e13-b541-e86c4abb420b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: nitinme
ms.openlocfilehash: 3ab70857c1e81f591a1c7e29bc1706ec4899ff58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-toolkit-for-eclipse-toocreate-spark-applications-for-an-hdinsight-cluster"></a>Gebruik Azure Toolkit voor Eclipse toocreate Spark scala-toepassingen voor een HDInsight-cluster

HDInsight Tools gebruiken in Azure Toolkit voor geschreven in Scala van Eclipse toodevelop Spark scala-toepassingen en deze tooan Azure HDInsight Spark-cluster, rechtstreeks vanuit Hallo Eclipse IDE verzenden. U kunt Hallo HDInsight Tools-invoegtoepassing op verschillende manieren gebruiken:

* toodevelop en het verzenden van een Scala Spark-toepassing op een HDInsight Spark-cluster
* tooaccess uw resources Azure HDInsight Spark-cluster
* toodevelop en een Scala Spark-toepassing lokaal uitvoeren

> [!IMPORTANT]
> Dit hulpprogramma kan worden gebruikt toocreate en verzenden van toepassingen alleen voor een HDInsight Spark-cluster op Linux.
> 
> 

## <a name="prerequisites"></a>Vereisten

* Een Apache Spark-cluster in HDInsight. Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
* Oracle Java Development Kit versie 8, die wordt gebruikt voor Hallo Eclipse IDE tijdens runtime. U kunt dit downloaden van Hallo [Oracle website](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* Eclipse IDE. In dit artikel maakt gebruik van Eclipse Neon. U kunt deze installeren via Hallo [Eclipse website](https://www.eclipse.org/downloads/).   
* Spark SDK. U kunt downloaden van [GitHub](http://go.microsoft.com/fwlink/?LinkID=723585&clcid=0x409).


## <a name="install-hdinsight-tools-in-azure-toolkit-for-eclipse-and-scala-plugin"></a>HDInsight-hulpprogramma's in Azure Toolkit voor Eclipse en Scala-invoegtoepassing installeren
### <a name="install-hdinsight-tools"></a>HDInsight-hulpprogramma's installeren
HDInsight Tools voor Eclipse is beschikbaar als onderdeel van Azure Toolkit voor Eclipse. Zie voor installatie-instructies [Azure Toolkit installeren voor Eclipse](../azure-toolkit-for-eclipse-installation.md).
### <a name="install-scala-plugin"></a>Scala-invoegtoepassing installeren
Wanneer u Hallo Intellij opent, detecteert Hallo HDInsight Tools automatisch of u Scala invoegtoepassing geïnstalleerd of niet. Klik op **OK** toocontinue en volg Hallo instructies tooinstall door Hallo Eclipse Marketplace.

 ![Automatische installatie Scala-invoegtoepassing](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala.png)

## <a name="sign-in-tooyour-azure-subscription"></a>Meld u aan tooyour Azure-abonnement
1. Start Eclipse IDE Hallo en Azure Explorer te openen. Op Hallo **venster** menu, klikt u op **weergave tonen**, en klik vervolgens op **andere**. Vouw in het dialoogvenster Hallo dat wordt geopend, **Azure**, klikt u op **Azure Explorer**, en klik vervolgens op **OK**.

    ![Het dialoogvenster weergave weergeven](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-1.png)
2. Klik met de rechtermuisknop Hallo **Azure** knooppunt en klik vervolgens op **aanmelden**.
3. In Hallo **Azure aanmelden** dialoogvenster vak, kies de verificatiemethode hello, klik op **aanmelden**, en voer uw Azure-referenties.
   
    ![Azure Sign In het dialoogvenster](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-2.png)
4. Nadat u bent aangemeld, Hallo **Selecteer abonnementen** dialoogvenster lijsten alle hello Azure-abonnementen die zijn gekoppeld aan het Hallo-referenties. Klik op **Selecteer** tooclose Hallo dialoogvenster.

    ![Selecteer in het dialoogvenster voor abonnementen](./media/hdinsight-apache-spark-eclipse-tool-plugin/Select-Subscriptions.png)
5. Op Hallo **Azure Explorer** tabblad uit, vouw **HDInsight** toosee hello HDInsight Spark-clusters in uw abonnement.
   
    ![HDInsight Spark-clusters in Azure Explorer](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-3.png)
6. U kunt een naam knooppunt toosee Hallo clusterbronnen (bijvoorbeeld opslagaccounts) die zijn gekoppeld aan cluster Hallo verder uitbreiden.
   
    ![Uitbreiden van een cluster naam toosee resources](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-4.png)



## <a name="set-up-a-spark-scala-project-for-an-hdinsight-spark-cluster"></a>Een Spark Scala-project voor een HDInsight Spark-cluster instellen

1. Klik in Hallo Eclipse IDE werkruimte **bestand**, klikt u op **nieuw**, en klik vervolgens op **Project**. 
2. Vouw in de wizard Nieuw Project hello, **HDInsight**, selecteer **Spark in HDInsight (Scala)**, en klik vervolgens op **volgende**.

    ![Hallo Spark in HDInsight (Scala) project selecteren](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-2.png)
3. Hallo Scala project maken wizard automatisch detecteert of de Scala invoegtoepassing geïnstalleerd of niet. Klik op **OK** toocontinue Hallo Scala invoegtoepassing en vervolgens volg Hallo instructies toorestart Eclipse downloaden.

    ![controle van scala](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-scala-2.png)
4. In Hallo **nieuw HDInsight Scala Project** in het dialoogvenster Hallo volgende waarden bevatten, en klik vervolgens op **volgende**:
   * Voer een naam voor Hallo-project.
   * In Hallo **JRE** gebied, zorg ervoor dat **gebruik van een uitvoeringsomgeving JRE** te is ingesteld,**JavaSE 1.7** of hoger.
   * Zorg ervoor dat SDK Spark is set toohello locatie waar u Hallo SDK hebt gedownload. Hallo koppeling toohello downloadlocatie is opgenomen in Hallo [vereisten](#prerequisites) eerder in dit artikel. U kunt ook Hallo SDK downloaden van Hallo opgenomen in het dialoogvenster Hallo koppeling.

    ![Het dialoogvenster New Project van HDInsight Scala](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-3.png)
5.  In het volgende dialoogvenster hello, klikt u op Hallo **bibliotheken** tabblad en klik vervolgens op Hallo standaardinstellingen behouden **voltooien**. 
   
    ![Tabblad bibliotheken](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-hdi-scala-app-4.png)
  
## <a name="create-a-scala-application-for-an-hdinsight-spark-cluster"></a>Een Scala-toepassing voor een HDInsight Spark-cluster maken

1. Vouw in Eclipse IDE, vanuit de Explorer-pakket, Hallo Hallo-project dat u eerder hebt gemaakt, met de rechtermuisknop op **src**, wijst u te**nieuw**, en klik vervolgens op **andere**.
2. In Hallo **een wizard selecteren** dialoogvenster Vouw **Scala Wizards**, klikt u op **Scala Object**, en klik vervolgens op **volgende**.
   
    ![Selecteer in het dialoogvenster wizard](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-1.png)
3. In Hallo **nieuw bestand maken** in het dialoogvenster een naam voor het Hallo-object invoeren, en klik vervolgens op **voltooien**.
   
    ![Dialoogvenster nieuwe bestanden maken](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-2.png)
4. Plak de volgende code in de teksteditor Hallo Hallo:
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        object MyClusterApp{
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("MyClusterApp")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows that have only one digit in hello seventh column in hello CSV
            val rdd1 =  rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACOut")
          }        
        }
5. Hallo-toepassing uitvoeren op een HDInsight Spark-cluster:
   
   1. Met de rechtermuisknop op de projectnaam Hallo vanuit de Explorer-pakket, en selecteer vervolgens **indienen Spark toepassing tooHDInsight**.        
   2. In Hallo **Spark verzending** in het dialoogvenster Hallo volgende waarden bevatten, en klik vervolgens op **indienen**:
      
      * Voor **clusternaam**, selecteer Hallo HDInsight Spark-cluster waarop toorun uw toepassing.
      * Selecteer een artefact in Eclipse-project Hallo of Selecteer een vanaf een vaste schijf. Hallo-standaardwaarde, hangt af van Hallo item die u met de rechtermuisknop in explorer pakket.
      * In Hallo **Main klassenaam** dropdownlist, verzending van wizard weer met alle objectnamen uit het geselecteerde project. Selecteer of voer een gewenste toorun. Als u artefact van harde schijf selecteert, moet u hoofdklasse naam zelf invoeren. 
      * Omdat de toepassingscode Hallo in dit voorbeeld geen geen opdrachtregelargumenten of verwijzen naar potten of bestanden, kunt u Hallo resterende tekstvakken leeg laten.
        
       ![Dialoogvenster Spark verzending](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-3.png)
   3. Hallo **Spark verzending** tabblad moet beginnen met het Hallo voortgang weergeven. U kunt de toepassing hello stoppen Hallo rode knop in Hallo **Spark verzending** venster. U kunt ook Hallo-logboeken voor deze specifieke toepassing uitvoeren door te klikken op het pictogram wereldbol hello (aangeduid met Hallo blauw vak in Hallo installatiekopie) weergeven.
      
       ![Verzending van Spark-venster](./media/hdinsight-apache-spark-eclipse-tool-plugin/create-scala-proj-4.png)

## <a name="access-and-manage-hdinsight-spark-clusters-by-using-hdinsight-tools-in-azure-toolkit-for-eclipse"></a>Toegang tot en HDInsight Spark-clusters beheren met behulp van HDInsight-hulpprogramma's in Azure Toolkit voor Eclipse
U kunt verschillende bewerkingen kunt uitvoeren met behulp van HDInsight-hulpprogramma's, waaronder toegang tot Hallo taakuitvoer.

### <a name="access-hello-job-view"></a>Toegang Hallo taak weergeven
1. Vouw in Azure Explorer **HDInsight**Hallo Spark clusternaam uitvouwen en klik vervolgens op **taken**. 

    ![Taak weergave knooppunt](./media/hdinsight-apache-spark-intellij-tool-plugin/job-view-node.png)

2. Klik op Hallo **taken** knooppunt. Hallo HDInsight Tools detecteert automatisch welk of u Hallo E (fx) clipse invoegtoepassing geïnstalleerd of niet. Klik op **OK** toocontinue en volg Hallo instructies tooinstall Hallo Eclipse Marketplace en Eclipse opnieuw te starten.

    ![Clipse E (fx) installeren](./media/hdinsight-apache-spark-eclipse-tool-plugin/auto-install-efxclipse.png)

3. Open Hallo taakweergave van Hallo **taken** knooppunt. Klik in het rechterdeelvenster Hallo Hallo **Spark taak weergeven** tabblad geeft alle Hallo-toepassingen die op het Hallo-cluster worden uitgevoerd. Klik op de naam Hallo van Hallo toepassing waarvoor u toosee meer informatie wenst.

    ![App-details](./media/hdinsight-apache-spark-intellij-tool-plugin/view-job-logs.png)
4. Als u de muisaanwijzer op Hallo taakgrafiek, wordt standaard uitgevoerd taak gegevens weergegeven. Te klikken op Hallo taakgrafiek toont Hallo fasen grafiek en gegevens die elke taak genereert.

    ![Fase taakdetails](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-graph-stage-info.png)

5. Veelgebruikte Logboeken, waaronder stuurprogramma Stderr, stuurprogramma Stdout en Directory-gegevens worden weergegeven in Hallo **logboek** tabblad.

    ![Logboekgegevens](./media/hdinsight-apache-spark-intellij-tool-plugin/Job-log-info.png)
6. U kunt ook Hallo Spark geschiedenis gebruikersinterface en Hallo gebruikersinterface van YARN (op niveau van de toepassing hello) openen door te klikken op de respectieve hyperlink Hallo Hallo boven aan het Hallo-venster.

### <a name="access-hello-storage-container-for-hello-cluster"></a>Toegang Hallo storage-container voor Hallo-cluster
1. Vouw in Azure Explorer Hallo **HDInsight** hoofdmap knooppunt toosee een lijst met HDInsight Spark-clusters die beschikbaar zijn.
2. Hallo cluster naam toosee Hallo storage-account en Hallo standaardopslagcontainer voor Hallo-cluster uitbreiden.
   
    ![Storage-account en het standaard storage-container](./media/hdinsight-apache-spark-eclipse-tool-plugin/view-explorer-5.png)
3. Klik op Hallo containernaam voor opslag die is gekoppeld aan het Hallo-cluster. Dubbelklik in het rechterdeelvenster Hallo Hallo **HVACOut** map. Open een Hallo **onderdeel -** toosee Hallo uitvoer van de toepassing hello bestanden.

### <a name="access-hello-spark-history-server"></a>Toegang tot Hallo Spark geschiedenis van server
1. Met de rechtermuisknop op de naam van uw Spark-cluster in Azure Explorer en selecteer vervolgens **Open Spark geschiedenis UI**. Wanneer u wordt gevraagd, voert u beheerdersreferenties Hallo voor Hallo-cluster. U moet hebben opgegeven deze tijdens het Hallo-cluster inrichten.
2. In Hallo Spark geschiedenis serverdashboard gebruikt u Hallo toepassing naam toolook voor Hallo toepassing dat u zojuist hebt voltooid. In Hallo voorafgaand aan code, stelt u de naam van de toepassing hello met behulp van `val conf = new SparkConf().setAppName("MyClusterApp")`. Daarom de naam van uw toepassing Spark is **MyClusterApp**.

### <a name="start-hello-ambari-portal"></a>Hallo Ambari portal starten
1. Met de rechtermuisknop op de naam van uw Spark-cluster in Azure Explorer en selecteer vervolgens **beheerportal Open Cluster (Ambari)**. 
2. Wanneer u wordt gevraagd, voert u beheerdersreferenties Hallo voor Hallo-cluster. U moet hebben opgegeven deze tijdens het Hallo-cluster inrichten.

### <a name="manage-azure-subscriptions"></a>Azure-abonnementen beheren
HDInsight-hulpprogramma's in Azure Toolkit voor Eclipse bevat standaard Hallo Spark-clusters van alle uw Azure-abonnementen. Indien nodig, kunt u Hallo abonnementen waarvoor u tooaccess Hallo cluster wilt opgeven. 

1. Azure Explorer met de rechtermuisknop op Hallo **Azure** de hoofd-knooppunt en klik vervolgens op **abonnementen beheren**. 
2. In het dialoogvenster hello, schakel de selectievakjes Hallo voor Hallo-abonnement dat u niet wilt dat tooaccess en klik vervolgens op **sluiten**. U kunt ook klikken op **Afmelden** als u wilt dat toosign buiten uw Azure-abonnement.

## <a name="run-a-spark-scala-application-locally"></a>Een Spark Scala-toepassing lokaal uitvoeren
Kunt u HDInsight-hulpprogramma's in Azure Toolkit voor Eclipse toorun Spark Scala-toepassingen lokaal op uw werkstation. Normaal gesproken deze toepassingen toegang toocluster resources, zoals een opslagcontainer niet nodig en u kunt uitvoeren en lokaal te testen.

### <a name="prerequisite"></a>Vereiste
Terwijl u Hallo lokale Spark Scala-toepassingen op een Windows-computer uitvoert, krijgt u mogelijk een uitzondering zoals toegelicht in [SPARK-2356](https://issues.apache.org/jira/browse/SPARK-2356). Deze uitzondering doet zich voor omdat **WinUtils.exe** ontbreekt in Windows. 

tooresolve deze fout, moet u [downloaden Hallo uitvoerbare](http://public-repo-1.hortonworks.com/hdp-win-alpha/winutils.exe) tooa locatie, zoals **C:\WinUtils\bin**. Vervolgens moet u de omgevingsvariabele Hallo toevoegen **HADOOP_HOME** en stelt u Hallo-waarde van variabele hello te**C\WinUtils**.

### <a name="run-a-local-spark-scala-application"></a>Een lokale Spark Scala-toepassing uitvoeren
1. Start Eclipse en maak een project. In Hallo **nieuw Project** in het dialoogvenster Hallo volgende keuzes maken en klik vervolgens op **volgende**.
   
   * Selecteer in het linkerdeelvenster Hallo **HDInsight**.
   * Selecteer in het rechterdeelvenster Hallo **Spark in HDInsight lokale uitvoeren voorbeeld (Scala)**.

    ![Het dialoogvenster Nieuw project](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run.png)
2. details van tooprovide hello, volg de stappen 3 tot en met 6 uit eerdere sectie Hallo [instellen van een Spark Scala-project voor een HDInsight Spark-cluster](#set-up-a-spark-scala-project-for-an-hdinsight-spark cluster).
3. Hallo-sjabloon wordt toegevoegd een voorbeeldcode (**LogQuery**) onder Hallo **src** map die u lokaal op uw computer uitvoeren kunt.
   
    ![Locatie van LogQuery](./media/hdinsight-apache-spark-eclipse-tool-plugin/local-app.png)
4. Klik met de rechtermuisknop Hallo **LogQuery** -toepassing te verwijzen**uitvoeren als**, en klik vervolgens op **1 Scala toepassing**. Ziet u uitvoer zoals deze in Hallo **Console** tabblad Hallo onderaan:
   
   ![Spark toepassing lokale resultaat van uitgevoerde](./media/hdinsight-apache-spark-eclipse-tool-plugin/hdi-spark-app-local-run-result.png)

## <a name="faq"></a>Veelgestelde vragen
kiest u een toepassing tooAzure Data Lake Store toosubmit **interactief** modus tijdens hello Azure aanmelden. Als u selecteert **automatisch** modus, kunt u een foutmelding krijgt.

![interactief aanmelden](./media/hdinsight-apache-spark-eclipse-tool-plugin/interactive-authentication.png)

Nu we dit heeft opgelost. U kunt een Azure Data Lake Cluster toosubmit uw toepassing met een methode voor aanmelden.

## <a name="feedback-and-known-issues"></a>Feedback en bekende problemen
Op dit moment wordt bekijken Spark uitvoer rechtstreeks niet ondersteund.

Als u suggesties of feedback hebt, of als u problemen ondervindt bij het gebruik van dit hulpprogramma, kunt u gratis toosend ons een e-mailbericht op hdivstool@microsoft.com.

## <a name="seealso"></a>Zie ook
* [Overzicht: Apache Spark in Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenario's
* [Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools](hdinsight-apache-spark-use-bi-tools.md)
* [Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen](hdinsight-apache-spark-eventhub-streaming.md)
* [Websitelogboekanalyse met Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="creating-and-running-applications"></a>Maken en uitvoeren van toepassingen
* [Een zelfstandige toepassing maken met behulp van Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Tools en uitbreidingen
* [Gebruik van Azure Toolkit voor IntelliJ toocreate en het verzenden van Spark Scala-toepassingen](hdinsight-apache-spark-intellij-tool-plugin.md)
* [Gebruik Azure Toolkit voor IntelliJ toodebug Spark scala-toepassingen op afstand via VPN-verbinding](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Gebruik Azure Toolkit voor IntelliJ toodebug Spark scala-toepassingen op afstand via SSH](hdinsight-apache-spark-intellij-tool-debug-remotely-through-ssh.md)
* [Gebruik van HDInsight Tools voor IntelliJ met Hortonworks Sandbox](hdinsight-tools-for-intellij-with-hortonworks-sandbox.md)
* [Zeppelin-notebooks gebruiken met een Spark-cluster in HDInsight](hdinsight-apache-spark-zeppelin-notebook.md)
* [Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Externe pakketten gebruiken met Jupyter-notebooks](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="managing-resources"></a>Resources beheren
* [Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen](hdinsight-apache-spark-job-debugging.md)

