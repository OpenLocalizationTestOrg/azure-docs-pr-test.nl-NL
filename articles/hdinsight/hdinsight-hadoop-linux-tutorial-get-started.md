---
title: aaaGet gestart met Hadoop en Hive in Azure HDInsight | Microsoft Docs
description: Informatie over hoe toocreate HDInsight-clusters en querygegevens met Hive.
keywords: aan de slag met hadoop, hadoop linux, hadoop quickstart, aan de slag met hive, hive quickstart
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6a12ed4c-9d49-4990-abf5-0a79fdfca459
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: jgao
ms.openlocfilehash: 3d96d78121200ebda3626dd2c3885e3ddacd546d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="hadoop-tutorial-get-started-using-hadoop-in-hdinsight"></a>Hadoop-zelfstudie: aan de slag met Hadoop in HDInsight

Meer informatie over hoe toocreate [Hadoop](http://hadoop.apache.org/) clusters in HDInsight en hoe toorun Hive in HDInsight taken. [Apache Hive](https://hive.apache.org/) is de meest populaire onderdeel Hallo in Hallo Hadoop-ecosysteem. Op dit moment wordt HDInsight geleverd met [zeven verschillende clustertypen](hdinsight-hadoop-introduction.md#overview). Elk clustertype ondersteunt een andere set onderdelen. Alle clustertypen ondersteunen Hive. Zie voor een lijst van ondersteunde onderdelen in HDInsight [wat is er nieuw in Hallo Hadoop-clusterversies geleverd door HDInsight?](hdinsight-component-versioning.md)  

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a>Vereisten
Voordat u met deze zelfstudie begint, moet u over de volgende onderdelen beschikken:

* **Azure-abonnement**: toocreate een gratis één maand-proefaccount, te bladeren[azure.microsoft.com/free](https://azure.microsoft.com/free).

## <a name="create-cluster"></a>Cluster maken

De meeste Hadoop-taken zijn batchtaken. U een cluster maken, voert enkele taken en verwijder vervolgens Hallo-cluster. In deze sectie maakt u een Hadoop-cluster in HDInsight met behulp van een [Azure Resource Manager-sjabloon](../azure-resource-manager/resource-group-template-deploy.md). Het maken van een Azure Resource Manager-sjabloon is niet vereist voor deze zelfstudie. Voor andere methoden voor het maken van cluster en inzicht Hallo-eigenschappen die in deze zelfstudie gebruikt, Zie [HDInsight-clusters maken](hdinsight-hadoop-provision-linux-clusters.md). Hallo selector op Hallo Hallo pagina toochoose bovenaan uw opties voor het maken van cluster gebruiken.

Hallo Resource Manager-sjabloon die wordt gebruikt in deze zelfstudie bevindt zich in [GitHub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-ssh-password/). 

1. Klik op Hallo installatiekopie toosign in tooAzure en open Hallo Resource Manager-sjabloon in hello Azure-portal. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-ssh-password%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Typ of selecteer Hallo volgende waarden:
   
    ![HDInsight Linux get Resource Manager-sjabloon gestart op de portal](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-arm-template-on-portal.png "implementeren Hadoop-cluster aan HDInsigut met Azure portal en een resource manager-sjabloon voor de groep Hallo").
   
    * **Abonnement**: selecteer uw Azure-abonnement.
    * **Resourcegroep**: maak een resourcegroep of selecteer een bestaande resourcegroep.  Een resourcegroep is een container met Azure-onderdelen.  In dit geval bevat resourcegroep Hallo Hallo HDInsight-cluster en Hallo afhankelijke Azure-opslagaccount. 
    * **Locatie**: Selecteer een Azure-locatie waar u toocreate uw cluster.  Kies een locatie dichter tooyou voor betere prestaties. 
    * **Clustertype**: selecteer **hadoop** voor deze zelfstudie.
    * **Clusternaam**: Voer een naam voor Hallo Hadoop-cluster.
    * **Cluster-aanmeldingsnaam en wachtwoord**: Hallo standaardaanmeldnaam is **admin**.
    * **SSH-gebruikersnaam en wachtwoord**: de standaardgebruikersnaam Hallo **sshuser**.  U kunt de naam wijzigen. 
     
    Sommige eigenschappen zijn vastgelegd in het Hallo-sjabloon.  U kunt deze waarden van de sjabloon Hallo configureren.

    * **Locatie**: locatie van de cluster Hallo Hallo en hello afhankelijke storage-account-share Hallo dezelfde locatie als Hallo resourcegroep.
    * **Clusterversie**: 3.5
    * **Type besturingssysteem**: Linux
    * **Het aantal worker-knooppunten**: 2

     Elk cluster is afhankelijk van een [Azure Storage-account](hdinsight-hadoop-use-blob-storage.md) of een [Azure Data Lake-account](hdinsight-hadoop-use-data-lake-store.md). Het wordt standaardopslagaccount hello genoemd. HDInsight-cluster en het standaardopslagaccount moeten worden geplaatst in Hallo dezelfde Azure-regio. Verwijderen van clusters, wordt de Hallo storage-account niet verwijderd. 
     
     Raadpleeg voor meer uitleg over deze eigenschappen [Hadoop-clusters maken in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

3. Selecteer **ik ga akkoord toohello voorwaarden bovengenoemde** en **pincode toodashboard**, en klik vervolgens op **aankoop**. U ziet een nieuwe tegel met de titel **implementatie van sjabloonimplementatie** op Hallo-portaldashboard. Het duurt ongeveer 20 minuten toocreate een cluster. Zodra het Hallo-cluster is gemaakt, is Hallo bijschrift van de tegel Hallo gewijzigde toohello Resourcegroepnaam opgegeven. En resourcegroep Hallo Hallo portal automatisch geopend in een nieuwe blade. U kunt zowel Hallo als Hallo standaard opslag vermeld zien.
   
    ![Aan de slag met resourcegroepen in HDInsight op basis van Linux](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-resource-group.png "Azure HDInsight-clusterresourcegroep").

4. Klik op Hallo cluster naam tooopen Hallo cluster in een nieuwe blade.

   ![Aan de slag met clusterinstellingen in HDInsight op basis van Linux](./media/hdinsight-hadoop-linux-tutorial-get-started/hdinsight-linux-get-started-cluster-settings.png "HDInsight-clustereigenschappen")


## <a name="run-hive-queries"></a>Hive-query's uitvoeren
[Apache Hive](hdinsight-use-hive.md) is de meest populaire onderdeel Hallo gebruikt in HDInsight. Er zijn veel manieren toorun Hive-taken in HDInsight. In deze zelfstudie gebruikt u Hallo Ambari Hive-weergave van Hallo-portal. Voor andere methoden voor het indienen van Hive-taken raadpleegt u [Hive gebruiken in HDInsight](hdinsight-use-hive.md).

1. Klik in de vorige schermafbeelding hello, op **Cluster-Dashboard**, en klik vervolgens op **HDInsight-Cluster-Dashboard**.  U kunt ook te bladeren **https://&lt;ClusterName >. azurehdinsight.net**, waarbij &lt;ClusterName > u hebt gemaakt in de vorige sectie tooopen Ambari van Hallo Hallo-cluster.
2. Hallo Hadoop-gebruikersnaam en wachtwoord die u hebt opgegeven in de vorige sectie Hallo invoeren. Hallo standaardgebruikersnaam **admin**.
3. Open **Hive-weergave** zoals weergegeven in de volgende schermafbeelding Hallo:
   
    ![Ambari-weergaven selecteren](./media/hdinsight-hadoop-linux-tutorial-get-started/selecthiveview.png "HDInsight Hive Weergave-menu").
4. In Hallo **Query-Editor** sectie van Hallo pagina plakken Hallo HiveQL-instructies te volgen in Hallo werkblad:
   
        SHOW TABLES;
   
   > [!NOTE]
   > Puntkomma is vereist voor Hive.       
   > 
   > 
5. Klik op **Uitvoeren**. Een **resultaten queryproces** sectie moet worden weergegeven onder Hallo Query-Editor en informatie over het Hallo-taak weergegeven. 
   
    Zodra het Hallo-query is voltooid, Hallo **resultaten queryproces** sectie vindt u Hallo resultaten van Hallo-bewerking. U ziet één tabel met de naam **hivesampletable**. Deze Hive-voorbeeldtabel wordt geleverd met alle Hallo HDInsight-clusters.
   
    ![HDInsight Hive-weergaven](./media/hdinsight-hadoop-linux-tutorial-get-started/hiveview.png "HDInsight Hive-weergave Query Editor").
6. Herhaal stap 4 en stap 5 toorun Hallo query te volgen:
   
        SELECT * FROM hivesampletable;
   
   > [!TIP]
   > Opmerking Hallo **resultaten opslaan** vervolgkeuzelijst in het bovenste Hallo links van de Hallo **resultaten queryproces** sectie; u kunt deze resultaten tooeither downloaden hello gebruiken of ze tooHDInsight opslag opslaan als een CSV-bestand.
   > 
   > 
7. Klik op **geschiedenis** tooget een lijst met taken Hallo.

Nadat u een Hive-taak hebt voltooid, kunt u [exporteren Hallo resultaten tooAzure SQL-database of SQL Server-database](hdinsight-use-sqoop-mac-linux.md), u kunt ook [visualiseren Hallo resultaten weergeven in Excel](hdinsight-connect-excel-power-query.md). Zie voor meer informatie over het gebruik van Hive in HDInsight [Hive en HiveQL met Hadoop in HDInsight tooanalyze een voorbeeldbestand van de Apache-log4j gebruiken](hdinsight-use-hive.md).

## <a name="clean-up-hello-tutorial"></a>Hallo-zelfstudie opschonen
Nadat u Hallo-zelfstudie hebt voltooid, kunt u toodelete Hallo-cluster. Met HDInsight worden uw gegevens opgeslagen in Azure Storage zodat u een cluster veilig kunt verwijderen wanneer deze niet wordt gebruikt. Voor een HDInsight-cluster worden ook kosten in rekening gebracht, zelfs wanneer het niet wordt gebruikt. Aangezien Hallo kosten voor Hallo cluster vaak zoveel hoger zijn dan Hallo kosten voor opslag, is het financieel aantrekkelijk toodelete clusters wanneer ze zich niet in gebruik. 

> [!NOTE]
> Met behulp van [Azure Data Factory](hdinsight-hadoop-create-linux-clusters-adf.md), HDInsight-clusters op aanvraag maken en configureren van een TimeToLive instelling te Hallo clusters automatisch verwijderen. 
> 
> 

**toodelete hello cluster en/of Hallo storage-standaardaccount**

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Vanuit de portal dashboard hello, klikt u op de tegel Hallo met Hallo Resourcegroepnaam die u hebt gebruikt toen u Hallo cluster hebt gemaakt.
3. Klik op **verwijderen** op Hallo resource blade toodelete Hallo resourcegroep, die Hallo-cluster en Hallo standaardopslagaccount bevat, of klik op de clusternaam Hallo op Hallo **Resources** tegel en klik vervolgens op **Verwijderen** op Hallo cluster-blade. Opmerking verwijderen van resourcegroep Hallo verwijdert Hallo storage-account. Als u tookeep Hallo storage-account wilt, kunt u alleen toodelete Hallo-cluster.

## <a name="troubleshoot"></a>Problemen oplossen

Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) als u problemen ondervindt met het maken van HDInsight-clusters.

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u geleerd hoe toocreate een op Linux gebaseerde HDInsight-cluster met een Resource Manager-sjabloon en hoe tooperform basic Hive-query's.

toolearn meer informatie over het analyseren van gegevens met HDInsight, Zie Hallo artikelen te volgen:

* toolearn meer informatie over het gebruik van Hive met HDInsight, met inbegrip van hoe tooperform Hive query's vanuit Visual Studio, Zie [Hive gebruiken met HDInsight][hdinsight-use-hive].
* toolearn over Pig, een taal gebruikt tootransform gegevens, Zie [Pig gebruiken met HDInsight][hdinsight-use-pig].
* Zie toolearn over MapReduce, een manier toowrite-programma's die gegevens op Hadoop, verwerken [MapReduce gebruiken met HDInsight][hdinsight-use-mapreduce].
* toolearn over het gebruik van Hallo HDInsight Tools voor Visual Studio tooanalyze gegevens in HDInsight, Zie [aan de slag met Visual Studio Hadoop-hulpprogramma's voor HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).

Als u bent klaar toostart werken met uw eigen gegevens en tooknow informatie over hoe HDInsight gegevens opslaat of hoe tooget gegevens in HDInsight, Zie de volgende Hallo nodig:

* Zie [Azure Storage gebruiken met HDInsight](hdinsight-hadoop-use-blob-storage.md) voor meer informatie over hoe HDInsight Azure Storage gebruikt.
* Voor meer informatie over tooupload gegevens tooHDInsight, Zie [uploaden van gegevens tooHDInsight][hdinsight-upload-data].

Als u meer informatie over het maken of beheren van een HDInsight-cluster toolearn, ziet er Hallo:

* toolearn over het beheren van uw Linux gebaseerde HDInsight-cluster, Zie [HDInsight-clusters beheren met Ambari](hdinsight-hadoop-manage-ambari.md).
* Zie toolearn meer informatie over het Hallo-opties die u selecteren kunt bij het maken van een HDInsight-cluster [HDInsight op Linux met aangepaste opties maken](hdinsight-hadoop-provision-linux-clusters.md).
* Als u bekend met Linux en Hadoop bent, maar tooknow details over Hadoop op HDInsight hello wilt, Zie [werken met HDInsight op Linux](hdinsight-hadoop-linux-information.md). Dit artikel biedt informatie zoals:
  
  * URL's voor services die worden gehost op het Hallo-cluster, zoals Ambari en WebHCat
  * Hallo-locatie van Hadoop-bestanden en voorbeelden op het lokale bestandssysteem Hallo
  * Hallo gebruik van Azure Storage (WASB) in plaats van HDFS als Hallo standaard gegevensopslag

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


