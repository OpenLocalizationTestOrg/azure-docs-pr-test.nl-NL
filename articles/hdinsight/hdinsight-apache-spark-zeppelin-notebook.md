---
title: aaaUse Zeppelin-notebooks met Apache Spark in Azure HDInsight-cluster | Microsoft Docs
description: Stapsgewijze instructies over hoe toouse Zeppelin-notebooks met Apache Spark in Azure HDInsight-clusters.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: df489d70-7788-4efa-a089-e5e5006421e2
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3ab479cfccc7fd38a9bf6a9fb4f5928beec8ff7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-zeppelin-notebooks-with-apache-spark-cluster-on-azure-hdinsight"></a>Zeppelin-notebooks met Apache Spark-cluster in Azure HDInsight gebruiken

HDInsight Spark-clusters bevatten Zeppelin-notebooks waarmee u toorun Spark taken kunt. In dit artikel leert u hoe toouse Hallo Zeppelin laptop op een HDInsight-cluster.

> [!NOTE]
> Zeppelin-notebooks zijn alleen beschikbaar voor Spark 1.6.3 in HDInsight 3.5 en Spark 2.1.0 in HDInsight 3.6.
>

**Vereisten:**

* Een Azure-abonnement. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* Een Apache Spark-cluster in HDInsight. Zie voor instructies [maken Apache Spark-clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

## <a name="launch-a-zeppelin-notebook"></a>Een laptop Zeppelin starten
1. Klik op Hallo blade Spark-cluster **Cluster-Dashboard**, en klik vervolgens op **Zeppelin-Notebook**. Voer desgevraagd Hallo beheerdersreferenties voor Hallo-cluster.
   
   > [!NOTE]
   > U mogelijk ook Hallo Zeppelin-Notebook voor uw cluster door de volgende URL in uw browser openen-Hallo bereiken. Vervang **CLUSTERNAME** met Hallo-naam van het cluster:
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/zeppelin`
   > 
   > 
2. Maak een nieuwe notebook. Hallo-headerdeelvenster, klik op **Notebook**, en klik vervolgens op **nieuwe notitie maken**.
   
    ![Maak een nieuwe Zeppelin-notebook](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-create-zeppelin-notebook.png "een nieuwe Zeppelin-notebook maken")
   
    Voer een naam voor de notebook Hallo en klik vervolgens op **opmerking maken**.
3. Zorg er ook Hallo notebook header toont een verbonden status. Dit wordt aangeduid met een groen punt in de rechterbovenhoek Hallo.
   
    ![Zeppelin-notebook status](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-connected.png "Zeppelin-notebook status")
4. Laad voorbeeldgegevens in een tijdelijke tabel. Wanneer u een Spark-cluster in HDInsight, Hallo voorbeeldgegevensbestand, maakt **hvac.csv**, is het opslagaccount gekopieerde toohello gekoppeld onder **\HdiSamples\SensorSampleData\hvac**.
   
    Plak in lege alinea Hallo die standaard wordt gemaakt in de nieuwe notebook hello, Hallo codefragment te volgen.
   
        %livy.spark
        //hello above magic instructs Zeppelin toouse hello Livy Scala interpreter
   
        // Create an RDD using hello default Spark context, sc
        val hvacText = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")
   
        // Define a schema
        case class Hvac(date: String, time: String, targettemp: Integer, actualtemp: Integer, buildingID: String)
   
        // Map hello values in hello .csv file toohello schema
        val hvac = hvacText.map(s => s.split(",")).filter(s => s(0) != "Date").map(
            s => Hvac(s(0), 
                    s(1),
                    s(2).toInt,
                    s(3).toInt,
                    s(6)
            )
        ).toDF()
   
        // Register as a temporary table called "hvac"
        hvac.registerTempTable("hvac")
   
    Druk op **SHIFT + ENTER** of klik op Hallo **afspelen** knop voor Hallo alinea toorun Hallo codefragment. Hallo-status op Hallo-rechtsonder in Hallo lid moet worden voortgezet van gereed in behandeling zijnde tooFINISHED die wordt uitgevoerd. Hallo-uitvoer wordt weergegeven aan de onderkant Hallo Hallo dezelfde paragraph. Hallo schermafbeelding ziet er Hallo volgende:
   
    ![Een tijdelijke tabel maken van ruwe gegevens](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-load-data.png "een tijdelijke tabel maken van ruwe gegevens")
   
    U kunt ook een titel tooeach alinea opgeven. Vanuit de rechterhoek hello, klikt u op Hallo **instellingen** pictogram en klik vervolgens op **titel weergeven**.
5. U kunt nu Spark SQL-instructies uitvoeren op Hallo **hvac** tabel. Plak Hallo volgende query in een nieuw lid. Hallo query haalt Hallo gebouw-ID en Hallo verschil tussen het Hallo-doel en de werkelijke temperaturen voor elke bouwen op een bepaalde datum. Druk op **SHIFT + ENTER**.
   
        %sql
        select buildingID, (targettemp - actualtemp) as temp_diff, date from hvac where date = "6/1/13" 
   
    Hallo **% sql** instructie op Hallo begin vertelt Hallo notebook toouse hello Livy Scala interpreter.
   
    Hallo volgende schermafbeelding ziet u uitvoer Hallo.
   
    ![Voer een Spark SQL-instructie Hallo notebook met](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-1.png "een Spark SQL-instructie met behulp van de notebook Hallo uitvoert")
   
     Klik op Hallo weergave opties (gemarkeerd in de rechthoek) tooswitch tussen verschillende manieren voor Hallo dezelfde uitvoer. Klik op **instellingen** toochoose welke consitutes Hallo sleutel en waarden in Hallo uitvoer. schermopname hierboven gebruikt Hallo **buildingID** als Hallo-sleutel en de gemiddelde Hallo van **temp_diff** Hallo-waarde.
6. U kunt ook Spark SQL-instructies voor het gebruik van variabelen in Hallo-query uitvoeren. Hallo volgende codefragment bevat hoe toodefine een variabele, **Temp**, in de query Hallo met Hallo mogelijke waarden die u wilt tooquery met. Wanneer u Hallo query voor het eerst uitvoert, wordt een vervolgkeuzelijst wordt automatisch gevuld met Hallo-waarden die u hebt opgegeven voor het Hallo-variabele.
   
        %sql
        select buildingID, date, targettemp, (targettemp - actualtemp) as temp_diff from hvac where targettemp > "${Temp = 65,65|75|85}" 
   
    In dit fragment plakken in een nieuwe alinea en druk op **SHIFT + ENTER**. Hallo volgende schermafbeelding ziet u uitvoer Hallo.
   
    ![Voer een Spark SQL-instructie Hallo notebook met](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-spark-query-2.png "een Spark SQL-instructie met behulp van de notebook Hallo uitvoert")
   
    Voor de volgende query's, kunt u een nieuwe waarde te selecteren in de vervolgkeuzelijst Hallo en Hallo query opnieuw uitvoeren. Klik op **instellingen** toochoose welke consitutes Hallo sleutel en waarden in Hallo uitvoer. schermopname hierboven gebruikt Hallo **buildingID** als sleutel Hallo Hallo gemiddelde van **temp_diff** Hallo-waarde en **targettemp** als Hallo-groep.
7. Hallo Livy interpreter tooexit Hallo toepassing opnieuw. toodo Hiertoe opent u interpreter instellingen door te klikken op Hallo vastgelegd in de gebruikersnaam van Hallo rechterbovenhoek en klik vervolgens op **Interpreter**.
   
    ![Start interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive-uitvoer")
8. Schuif tooLivy interpreter instellingen en klik vervolgens op **opnieuw**.
   
    ![Opnieuw opstarten Hallo Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "hello Zeppelin intepreter starten")

## <a name="how-do-i-use-external-packages-with-hello-notebook"></a>Hoe gebruik ik externe pakketten met Hallo notebook
U kunt Hallo Zeppelin-notebook in Apache Spark-cluster in HDInsight (Linux) toouse externe, community bijgedragen pakketten die niet opgenomen out-of-the-box in Hallo cluster zijn configureren. U kunt zoeken Hallo [Maven opslagplaats](http://search.maven.org/) voor Hallo volledige lijst met pakketten die beschikbaar zijn. U kunt ook een lijst met beschikbare pakketten opvragen uit andere bronnen. Bijvoorbeeld, een volledige lijst met pakketten community bijgedragen is beschikbaar op [Spark pakketten](http://spark-packages.org/).

In dit artikel ziet u hoe toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pakket met de Jupyter-notebook Hallo.

1. Open interpreter instellingen. In de rechterbovenhoek hello, Hallo vastgelegd in de gebruikersnaam van de op en klik op **Interpreter**.
   
    ![Start interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive-uitvoer")
2. Schuif tooLivy interpreter instellingen en klik vervolgens op **bewerken**.
   
    ![Wijzig de instellingen van de interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-1.png "interpreter instellingen wijzigen")
3. Voeg een nieuwe sleutel aangeroepen **livy.spark.jars.packages** en stel de waarde in de indeling Hallo `group:id:version`. Dus als u wilt dat toouse hello [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar) pakket, moet u Hallo waarde instellen van Hallo sleutel te`com.databricks:spark-csv_2.10:1.4.0`.
   
    ![Wijzig de instellingen van de interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-use-external-package-2.png "interpreter instellingen wijzigen")
   
    Klik op **opslaan** en Hallo Livy interpreter opnieuw opstarten.
4. **Tip**: als u wilt dat toounderstand hoe tooarrive op Hallo-waarde van Hallo sleutel, hier hierboven hoe.
   
    a. Hallo-pakket niet vinden in Hallo Maven-opslagplaats. Voor deze zelfstudie gebruikt we [spark-csv](http://search.maven.org/#artifactdetails%7Ccom.databricks%7Cspark-csv_2.10%7C1.4.0%7Cjar).
   
    b. Verzamel uit de opslagplaats hello, Hallo waarden voor **GroupId**, **artefact-id**, en **versie**.
   
    ![Externe pakketten gebruiken met Jupyter-notebook](./media/hdinsight-apache-spark-zeppelin-notebook/use-external-packages-with-jupyter.png "externe pakketten gebruiken met Jupyter-notebook")
   
    c. Samenvoegen van Hallo drie waarden, gescheiden door een dubbele punt (**:**).
   
        com.databricks:spark-csv_2.10:1.4.0

## <a name="where-are-hello-zeppelin-notebooks-saved"></a>Waar zijn Hallo Zeppelin-notebooks opgeslagen?
Hallo Zeppelin-notebooks worden toohello cluster headnodes opgeslagen. Dus als u Hallo cluster verwijdert, Hallo notitieblokken eveneens worden verwijderd. Als u uw notitieblokken toopreserve voor later gebruik op andere clusters wilt, moet u deze exporteren wanneer u klaar bent met het Hallo-taken uitvoeren. tooexport een laptop, klikt u op Hallo **exporteren** pictogram zoals weergegeven in onderstaande Hallo-afbeelding.

![Downloaden van de notebook](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-download-notebook.png "downloaden Hallo notebook")

Dit bespaart Hallo notebook als een JSON-bestand op uw downloadlocatie.

## <a name="livy-session-management"></a>Sessiebeheer Livy
Wanneer u het eerste code alinea Hallo in uw laptop Zeppelin uitvoert, wordt een nieuwe sessie van Livy gemaakt in uw HDInsight Spark-cluster. Deze sessie worden verdeeld over alle Zeppelin-notebooks die u maakt. Als voor een bepaalde reden Hallo Livy sessie is afgesloten (cluster opnieuw opstarten, enzovoort), kunt u niet kunt toorun taken van Hallo Zeppelin notebook.

In dat geval moet u de volgende stappen uit voordat u kunt de uitvoering van taken van een laptop Zeppelin Hallo uitvoeren. 

1. Opnieuw opstarten Hallo Livy interpreter uit Hallo Zeppelin laptop. toodo Hiertoe opent u interpreter instellingen door te klikken op Hallo vastgelegd in de gebruikersnaam van Hallo rechterbovenhoek en klik vervolgens op **Interpreter**.
   
    ![Start interpreter](./media/hdinsight-apache-spark-zeppelin-notebook/zeppelin-launch-interpreter.png "Hive-uitvoer")
2. Schuif tooLivy interpreter instellingen en klik vervolgens op **opnieuw**.
   
    ![Opnieuw opstarten Hallo Livy intepreter](./media/hdinsight-apache-spark-zeppelin-notebook/hdinsight-zeppelin-restart-interpreter.png "hello Zeppelin intepreter starten")
3. Een codecel uitvoeren vanaf een bestaande Zeppelin-notebook. Hiermee maakt u een nieuwe sessie van Livy in Hallo HDInsight-cluster.

## <a name="seealso"></a>Zie ook
* [Overzicht: Apache Spark in Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenario's
* [Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools](hdinsight-apache-spark-use-bi-tools.md)
* [Spark met Machine Learning: Spark in HDInsight gebruiken voor het analyseren van de gebouwtemperatuur met behulp van HVAC-gegevens](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen](hdinsight-apache-spark-eventhub-streaming.md)
* [Websitelogboekanalyse met Spark in HDInsight](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>Toepassingen maken en uitvoeren
* [Een zelfstandige toepassing maken met behulp van Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>Tools en uitbreidingen
* [De invoegtoepassing HDInsight Tools voor toocreate IntelliJ IDEA gebruiken en het verzenden van Spark Scala-toepassingen](hdinsight-apache-spark-intellij-tool-plugin.md)
* [De invoegtoepassing HDInsight Tools for IntelliJ IDEA toodebug Spark applications op afstand gebruiken](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [Beschikbare kernels voor Jupyter-notebook in Spark-cluster voor HDInsight](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [Externe pakketten gebruiken met Jupyter-notebooks](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [Jupyter op uw computer installeren en verbinding maken met tooan HDInsight Spark-cluster](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>Resources beheren
* [Resources beheren voor Hallo Apache Spark-cluster in Azure HDInsight](hdinsight-apache-spark-resource-manager.md)
* [Taken die worden uitgevoerd in een Apache Spark-cluster in HDInsight, traceren en er fouten in oplossen](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md 







