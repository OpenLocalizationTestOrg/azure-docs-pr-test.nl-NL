---
title: aaaCreate Scala app toorun op Spark-clusters - Azure HDInsight | Microsoft Docs
description: Maak een toepassing Spark is geschreven in Scala met Apache Maven zoals Hallo systeem en een bestaande Maven archetype voor Scala geleverd door IntelliJ IDEA opbouwen.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b2467a40-a340-4b80-bb00-f2c3339db57b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: b25291b60921021486f55d78b4832a070a54d163
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-scala-maven-application-toorun-on-apache-spark-cluster-on-hdinsight"></a>Maken van een toepassing Scala Maven toorun op Apache Spark-cluster in HDInsight

Meer informatie over hoe een Spark-toepassing die is geschreven in Scala met behulp van Maven met IntelliJ IDEA toocreate. Hallo artikel gebruikt Apache Maven Hallo systeem bouwen en begint met een bestaande Maven archetype voor Scala geleverd door IntelliJ IDEA.  Maken van een toepassing Scala in IntelliJ IDEA omvat Hallo stappen te volgen:

* Maven gebruiken als Hallo build-systeem.
* Project Object Model (POM) tooresolve Spark module bestandsafhankelijkheden bijwerken.
* Uw toepassing worden geschreven in Scala.
* Genereert een jar-bestand dat verzonden tooHDInsight Spark-clusters worden kan.
* Hallo-toepassing uitvoeren in Spark-cluster met behulp van Livy.

> [!NOTE]
> HDInsight biedt ook een IntelliJ IDEA invoegtoepassing hulpprogramma tooease Hallo proces van het maken en verzenden van toepassingen tooan HDInsight Spark-cluster op Linux. Zie voor meer informatie [gebruik de invoegtoepassing HDInsight Tools for IntelliJ IDEA toocreate en het verzenden van Spark scala-toepassingen](hdinsight-apache-spark-intellij-tool-plugin.md).
> 
> 

## <a name="prerequisites"></a>Vereisten

* Een Azure-abonnement. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Een Apache Spark-cluster in HDInsight. Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).
* Oracle Java Development kit. Kunt u het installeren van [hier](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).
* Een Java IDE. Dit artikel wordt IntelliJ IDEA 15.0.1 gebruikt. Kunt u het installeren van [hier](https://www.jetbrains.com/idea/download/).

## <a name="install-scala-plugin-for-intellij-idea"></a>Scala-invoegtoepassing voor IntelliJ IDEA installeren
Als IntelliJ IDEA installatie niet niet gevraagd voor het inschakelen van Scala-invoegtoepassing, IntelliJ IDEA starten en te volgen stappen tooinstall Hallo invoegtoepassing Hallo doorlopen:

1. IntelliJ IDEA Start en klik in het welkomstscherm op **configureren** en klik vervolgens op **Plugins**.
   
    ![Scala invoegtoepassing inschakelen](./media/hdinsight-apache-spark-create-standalone-application/enable-scala-plugin.png)
2. Klik in het volgende scherm hello, op **JetBrains installeren invoegtoepassing** van linkerbenedenhoek Hallo. In Hallo **JetBrains Plugins Bladeren** dialoogvenster dat wordt geopend, Scala zoeken en klik vervolgens op **installeren**.
   
    ![Scala-invoegtoepassing installeren](./media/hdinsight-apache-spark-create-standalone-application/install-scala-plugin.png)
3. Nadat het Hallo-invoegtoepassing is geïnstalleerd, klikt u op Hallo **opnieuw IntelliJ IDEA knop** toorestart Hallo IDE.

## <a name="create-a-standalone-scala-project"></a>Een zelfstandige Scala-project maken
1. IntelliJ IDEA Start en een nieuw project maken. Controleer in Hallo het dialoogvenster new project, Hallo volgende keuzes en klik vervolgens op **volgende**.
   
    ![Maven-project maken](./media/hdinsight-apache-spark-create-standalone-application/create-maven-project.png)
   
   * Selecteer **Maven** als Hallo projecttype.
   * Geef een **Project SDK**. Klik op Nieuw en navigeer toohello Java-installatiemap, meestal `C:\Program Files\Java\jdk1.8.0_66`.
   * Selecteer Hallo **maken van archetype** optie.
   * Selecteer in de lijst Hallo van archetypes, **org.scala tools.archetypes:scala-archetype eenvoudige**. Hiermee wordt de juiste mapstructuur Hallo en Hallo vereist afhankelijkheden toowrite Scala standaardprogramma voor downloaden.
2. Relevante waarden opgeven voor **GroupId**, **artefact-id**, en **versie**. Klik op **Volgende**.
3. Accepteer de standaardwaarden Hallo Hallo volgende in het dialoogvenster waarin u Maven-basismap en andere instellingen voor gebruikers opgeven, en klikt u op **volgende**.
4. Geef een naam en locatie Hallo laatste in het dialoogvenster en klik vervolgens op **voltooien**.
5. Hallo verwijderen **MySpec.Scala** op het bestand **src\test\scala\com\microsoft\spark\example**. U hoeft niet dit voor de toepassing hello.
6. Indien nodig, wijzig de naam Hallo standaard bron- en -bestanden. Ga te vanuit het linkerdeelvenster Hallo in Hallo IntelliJ IDEA**src\main\scala\com.microsoft.spark.example**. Met de rechtermuisknop op **App.scala**, klikt u op **opsplitsen**, bestandsnaam wijzigen, klikt u op en geef in het dialoogvenster hello, Hallo nieuwe naam voor de toepassing hello en klik op **opsplitsen**.
   
    ![De naam van bestanden](./media/hdinsight-apache-spark-create-standalone-application/rename-scala-files.png)  
7. In latere stappen Hallo wordt Hallo pom.xml toodefine Hallo afhankelijkheden voor Hallo Spark Scala-toepassing bijgewerkt. Voor deze afhankelijkheden toobe gedownload en automatisch opgelost dat moet u Maven dienovereenkomstig configureren.
   
    ![Maven configureren voor automatische downloads](./media/hdinsight-apache-spark-create-standalone-application/configure-maven.png)
   
   1. Van Hallo **bestand** menu, klikt u op **instellingen**.
   2. In Hallo **instellingen** dialoogvenster Ga te**bouwen, kan worden uitgevoerd, implementatie** > **Build Tools** > **Maven**  >  **Importeren**.
   3. Hallo-optie te selecteren**Import Maven projects automatisch**.
   4. Klik op **toepassen**, en klik vervolgens op **OK**.
8. Hallo Scala bron bestand tooinclude uw toepassingscode bijwerken. Open en vervang bestaande voorbeeldcode met de volgende code Hallo Hallo en Hallo wijzigingen opslaan. Deze code Hallo gegevens leest uit Hallo HVAC.csv (beschikbaar op alle HDInsight Spark-clusters), haalt Hallo rijen met slechts één cijfer in Hallo zesde kolom en schrijft Hallo uitvoer te**/HVACOut** onder Hallo standaard opslag container voor Hallo-cluster.
   
        package com.microsoft.spark.example
   
        import org.apache.spark.SparkConf
        import org.apache.spark.SparkContext
   
        /**
          * Test IO toowasb
          */
        object WasbIOTest {
          def main (arg: Array[String]): Unit = {
            val conf = new SparkConf().setAppName("WASBIOTest")
            val sc = new SparkContext(conf)
   
            val rdd = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
            //find hello rows which have only one digit in hello 7th column in hello CSV
            val rdd1 = rdd.filter(s => s.split(",")(6).length() == 1)
   
            rdd1.saveAsTextFile("wasb:///HVACout")
          }
        }
9. Hallo pom.xml bijwerken.
   
   1. Binnen `<project>\<properties>` Hallo volgende toevoegen:
      
          <scala.version>2.10.4</scala.version>
          <scala.compat.version>2.10.4</scala.compat.version>
          <scala.binary.version>2.10</scala.binary.version>
   2. Binnen `<project>\<dependencies>` Hallo volgende toevoegen:
      
           <dependency>
             <groupId>org.apache.spark</groupId>
             <artifactId>spark-core_${scala.binary.version}</artifactId>
             <version>1.4.1</version>
           </dependency>
      
      Sla de wijzigingen toopom.xml.
10. Hallo JAR-bestand maken. IntelliJ IDEA kunt maken van de JAR als een artefact van een project. Hallo stappen uitvoeren.
    
    1. Van Hallo **bestand** menu, klikt u op **projectstructuur**.
    2. In Hallo **projectstructuur** in het dialoogvenster, klikt u op **artefacten** en klik vervolgens op Hallo plus symbool. Klik in het pop-updialoogvenster hello, op **JAR**, en klik vervolgens op **van modules met afhankelijkheden**.
       
        ![JAR maken](./media/hdinsight-apache-spark-create-standalone-application/create-jar-1.png)
    3. In Hallo **maken JAR van Modules** dialoogvenster vak, klikt u op Hallo weglatingsteken (![weglatingsteken](./media/hdinsight-apache-spark-create-standalone-application/ellipsis.png) ) tegen Hallo **Main klasse**.
    4. In Hallo **Main-klasse selecteren** in het dialoogvenster, selecteer Hallo-klasse die wordt standaard weergegeven en klik vervolgens op **OK**.
       
        ![JAR maken](./media/hdinsight-apache-spark-create-standalone-application/create-jar-2.png)
    5. In Hallo **maken JAR van Modules** dialoogvenster zorg die optie hello te**toohello doel JAR extraheren** is geselecteerd en klik vervolgens op **OK**. Hiermee maakt u een één JAR met alle afhankelijkheden.
       
        ![JAR maken](./media/hdinsight-apache-spark-create-standalone-application/create-jar-3.png)
    6. Hallo uitvoer indeling tabblad bevat alle Hallo potten die opgenomen als onderdeel van Hallo Maven-project zijn. U kunt selecteren en delete Hallo toepassingsgroepen waarop Scala toepassing hello heeft geen directe afhankelijkheid. Voor de toepassing hello hier maakt, kunt u alle maar Hallo laatste (**SparkSimpleApp compileren uitvoer**). Hallo potten toodelete selecteren en klik vervolgens op Hallo **verwijderen** pictogram.
       
        ![JAR maken](./media/hdinsight-apache-spark-create-standalone-application/delete-output-jars.png)
       
        Zorg ervoor dat **bouwen op Controleer** selectievakje is ingeschakeld, waardoor wordt gegarandeerd dat jar hello wordt gemaakt telkens wanneer Hallo-project wordt gemaakt of bijgewerkt. Klik op **toepassen** en vervolgens **OK**.
    7. In de menubalk hello, klikt u op **bouwen**, en klik vervolgens op **Project maken**. U kunt ook klikken op **bouwen artefacten** toocreate Hallo jar. Hallo uitvoer jar gemaakt onder **\out\artifacts**.
       
        ![JAR maken](./media/hdinsight-apache-spark-create-standalone-application/output.png)

## <a name="run-hello-application-on-hello-spark-cluster"></a>Hallo-toepassing uitvoeren op Hallo Spark-cluster
toorun hello toepassing op Hallo-cluster, moet u doen Hallo volgende:

* **Kopiëren Hallo toepassing jar toohello Azure storage-blob** die zijn gekoppeld aan het Hallo-cluster. U kunt [ **AzCopy**](../storage/common/storage-use-azcopy.md), een opdracht hulpprogramma toodo dus regel. Er zijn veel andere clients ook dat u tooupload gegevens kunt gebruiken. U vindt meer informatie hierover op [gegevens voor Hadoop-taken in HDInsight uploaden](hdinsight-upload-data.md).
* **Livy toosubmit een taak van toepassing op afstand gebruiken** toohello Spark-cluster. Spark-clusters in HDInsight omvat Livy die beschrijft de REST-eindpunten tooremotely indienen Spark-taken. Zie voor meer informatie [Spark verzenden van taken op afstand met behulp van Livy met Spark-clusters in HDInsight](hdinsight-apache-spark-livy-rest-interface.md).

## <a name="next-step"></a>Volgende stap

In dit artikel u leert hoe toocreate een Spark scala-toepassing. Geavanceerde toohello volgende artikel toolearn hoe toorun deze toepassing op een HDInsight Spark-cluster met behulp van Livy.

> [!div class="nextstepaction"]
>[Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy](hdinsight-apache-spark-livy-rest-interface.md)

