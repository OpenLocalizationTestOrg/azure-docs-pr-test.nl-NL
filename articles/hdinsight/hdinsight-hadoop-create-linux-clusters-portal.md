---
title: aaaCreate Hadoop-clusters met een webbrowser - Azure HDInsight | Microsoft Docs
description: Informatie over hoe toocreate Hadoop, HBase, Storm of Spark-clusters op Linux voor HDInsight met een webbrowser en hello Azure preview-portal.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 697278cf-0032-4f7c-b9b2-a84c4347659e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 63027e35e2d66dd76218aff3e0c085fc811736ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-hello-azure-portal"></a>Op basis van Linux-clusters maken in HDInsight met behulp van hello Azure-portal
[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Hello Azure-portal is een webgebaseerde beheerprogramma voor services en bronnen die worden gehost in Microsoft Azure-cloud Hallo. In dit artikel leert u hoe toocreate Linux gebaseerde HDInsight-clusters met Hallo-portal.

## <a name="prerequisites"></a>Vereisten
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Een moderne webbrowser**. Hello Azure-portal gebruikt HTML5 en Javascript en werkt mogelijk niet correct in oudere webbrowsers.

## <a name="create-clusters"></a>Clusters maken
Hello Azure-portal beschrijft de meeste Hallo clustereigenschappen. Azure Resource Manager-sjabloon kunt u een groot aantal details verbergen. Zie voor meer informatie [maken Linux gebaseerde Hadoop-clusters in HDInsight met behulp van Azure Resource Manager-sjablonen](hdinsight-hadoop-create-linux-clusters-arm-templates.md).

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]


1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Klik op  **+** , klikt u op **Intelligence en analyse**, en klik vervolgens op **HDInsight**.
   
    ![Een nieuw cluster maken in Azure-portal Hallo](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster.png "maken van een nieuw cluster in hello Azure-portal")

3. In Hallo **HDInsight** blade, klikt u op **aangepast (grootte, instellingen, apps)**, klikt u op **basisbeginselen**, en voer de volgende informatie Hallo.

    ![Een nieuw cluster maken in Azure-portal Hallo](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-basics.png "maken van een nieuw cluster in hello Azure-portal")

    * Voer **Clusternaam** in: deze naam moet uniek zijn.

    * Van Hallo **abonnement** vervolgkeuzelijst, selecteer hello Azure-abonnement dat wordt gebruikt voor het Hallo-cluster.

    * Klik op **type Cluster**, en selecteer vervolgens:
   
        * **Type cluster**: als u niet welke toochoose weet, selecteert u **Hadoop**. Het is meest populaire clustertype Hallo.
     
            > [!IMPORTANT]
            > HDInsight clusters worden geleverd in verschillende typen die overeenkomen met de werkbelasting toohello of technologie voor het cluster Hallo is afgestemd op. Er is geen ondersteunde methode toocreate van een cluster waarin meerdere typen zoals Storm en HBase op één cluster. 
            > 
            > 
        
        * **Besturingssysteem**: selecteer **Linux**.
        
        * **Versie**: standaardversie hello gebruiken als u niet welke toochoose weet. Zie [HDInsight-clusterversies](hdinsight-component-versioning.md) voor meer informatie.
        * **Cluster-laag**: Azure HDInsight biedt Hallo big data cloud twee categorieën aanbiedingen: lagen Standard en Premium-laag. Zie [Clusterlagen](hdinsight-hadoop-provision-linux-clusters.md#cluster-tiers) voor meer informatie.

    * Voor **clusteraanmeldgegevens** en **Cluster aanmeldingswachtwoord**, Hallo gebruikersnaam en wachtwoord voor gebruiker met beheerdersrechten Hallo bieden.

    * Voer een **SSH-gebruikersnaam** en als u toohave Hallo SSH-wachtwoord gelijk aan Hallo beheerderswachtwoord dat u eerder hebt opgegeven wilt, selecteert u Hallo **gebruik hetzelfde wachtwoord als cluster aanmelding** selectievakje. Als dit niet het geval is, Geef een **wachtwoord** of **openbare sleutel**, die wordt gebruikt tooauthenticate Hallo SSH-gebruiker zijn. Met behulp van een openbare sleutel is Hallo aanbevolen benadering. Klik op **Selecteer** op Hallo onder toosave Hallo referenties configuratie.
   
        Zie [SSH-sleutels gebruiken met HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) voor informatie.

    * Voor **resourcegroep**, opgeven of u wilt dat een nieuwe resourcegroep toocreate of gebruik een bestaande.

    * Geef een datacenter **locatie** waar Hallo cluster wordt gemaakt.

    * Klik op **Volgende**.

4. Op Hallo **opslag** blade aangeven of u Azure Storage (WASB) of de Data Lake Store als uw standaard-opslag. Bekijkt hello tabel hieronder voor meer informatie.

    ![Een nieuw cluster maken in Azure-portal Hallo](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-storage.png "maken van een nieuw cluster in hello Azure-portal")

    | Storage                                      | Beschrijving |
    |----------------------------------------------|-------------|
    | **Azure Storage-Blobs als standaard opslag**   | <ul><li>Voor **primaire opslagtype**, selecteer **Azure Storage**. Daarna voor **selectiemethode**, kunt u **abonnementen** als u wilt dat toospecify een opslagaccount die deel uitmaakt van uw Azure-abonnement en selecteer vervolgens Hallo storage-account. Klik anders op **toegangssleutel** en Hallo-informatie voor Hallo storage-account dat u wilt dat toochoose van buiten uw Azure-abonnement te bieden.</li><li>Voor **standaardcontainer**, u kunt ervoor kiezen toogo met Hallo container standaardnaam voorgesteld door Hallo portal of geef uw eigen.</li><li>Als u WASB als standaard opslag gebruikt, hoeft u (optioneel) op **extra Opslagaccounts** toospecify extra opslagaccounts die tooassociate met Hallo-cluster. In Hallo **Azure Opslagsleutels** blade klikt u op **opslag van een sleutel**, en vervolgens kunt u uw storage-account van uw Azure-abonnementen of van andere abonnementen (bieden Hallo storage-account toegangssleutel).</li><li>Als u WASB als standaard opslag gebruikt, hoeft u (optioneel) op **Data Lake Store toegang** toospecify Azure Data Lake Store als extra opslagruimte. Zie voor meer informatie [een HDInsight-cluster maken met Data Lake Store met Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</li></ul> |
    | **Azure Data Lake Store als standaard opslag** | Voor **primaire opslagtype**, selecteer **Data Lake Store** en Raadpleeg toohello artikel [een HDInsight-cluster maken met Data Lake Store met Azure Portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md) voor instructies. |
    | **Met externe metastores**                      | U kunt eventueel een SQL-database toosave Hive en Oozie metagegevens gekoppeld aan Hallo cluster opgeven. Voor **selecteert u een SQL-database voor Hive** selecteert u een SQL-database en geef vervolgens Hallo gebruikersnaam en wachtwoord voor Hallo-database. Herhaal deze stappen voor Oozie-metagegevens.<br><br>Enkele overwegingen bij het gebruik van Azure SQL-database voor metastores. <ul><li>Hello Azure SQL database die wordt gebruikt voor de metastore Hallo moet connectiviteit tooother toestaan Azure-services, waaronder Azure HDInsight. Op Hallo Azure SQL database dashboard aan de rechterkant hello, klikt u op Hallo servernaam. Dit is Hallo-server op welke Hallo SQL database-instantie wordt uitgevoerd. Wanneer u zich op Hallo Serverweergave, klikt u op **configureren**, en vervolgens voor **Azure Services**, klikt u op **Ja**, en klik vervolgens op **opslaan**.</li><li>Bij het maken van een metastore gebruik niet de naam van een database met streepjes of afbreekstreepjes, zoals dit Hallo cluster maken van het proces toofail kan veroorzaken.</li></ul>                                                                                                                                                                       |

    Klik op **Volgende**. 

    > [!WARNING]
    > Met een account extra opslagruimte in een andere locatie dan Hallo HDInsight-cluster wordt niet ondersteund.

5. Klik desgewenst op **toepassingen** tooinstall toepassingen die met HDInsight-clusters werken. Deze toepassingen kunnen zijn ontwikkeld door Microsoft, door onafhankelijke softwareleveranciers (ISV) of door u zelf. Zie voor meer informatie [installeren HDInsight-toepassingen](hdinsight-apps-install-applications.md#install-applications-during-cluster-creation).


6. Klik op **clustergrootte** toodisplay informatie over het Hallo-knooppunten die worden gemaakt voor dit cluster. Het aantal worker-knooppunten die u nodig hebt voor de cluster Hallo Hallo instellen. Hallo geschatte kosten van het Hallo-cluster worden weergegeven binnen het Hallo-blade.
   
    ![Knooppunt prijzen lagen blade](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-nodes.png "aantal clusterknooppunten opgeven")
   
   > [!IMPORTANT]
   > Als u van plan op meer dan 32 worker-knooppunten bent, bij het maken van een cluster maken of door het Hallo-cluster schalen na het maken, moet u een grootte van het hoofdknooppunt met ten minste 8 kerngeheugens en 14GB selecteren RAM-geheugen.
   > 
   > Zie voor meer informatie over knooppuntgrootten en bijbehorende kosten [HDInsight prijzen](https://azure.microsoft.com/pricing/details/hdinsight/).
   > 
   > 
   
   Klik op **volgende** toosave Hallo knooppunt configuratie prijzen.

7. Klik op **geavanceerde instellingen** tooconfigure andere optionele instellingen zoals het gebruik van **scriptacties** toocustomize een tooinstall cluster aangepaste onderdelen of lid te worden van een **virtueel netwerk**. Bekijkt hello tabel hieronder voor meer informatie.

    ![Knooppunt prijzen lagen blade](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-advanced.png "aantal clusterknooppunten opgeven")

    | Optie | Beschrijving |
    |--------|-------------|
    | **Scriptacties** | Gebruik deze optie als u wilt dat toouse een aangepast script toocustomize een cluster, zoals het Hallo-cluster wordt gemaakt. Zie voor meer informatie over scriptacties [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md). |
    | **Virtueel netwerk** | Selecteer een Azure virtuele netwerk en het Hallo-subnet als u tooplace Hallo cluster in een virtueel netwerk wilt toevoegen. Zie voor meer informatie over het gebruik van HDInsight met een virtueel netwerk, met inbegrip van specifieke configuratievereisten voor Hallo virtueel netwerk [mogelijkheden uitbreiden HDInsight met behulp van een Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md). |

    Klik op **Volgende**.

8. Op Hallo **samenvatting** blade Controleer Hallo-informatie die u eerder hebt ingevoerd, en klik vervolgens op **maken**.

    ![Knooppunt prijzen lagen blade](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-summary.png "aantal clusterknooppunten opgeven")
    
    > [!NOTE]
    > Het duurt enige tijd Hallo cluster toobe gemaakt, meestal ongeveer 15 minuten. Hallo-tegel op Hallo Startboard gebruiken of Hallo **meldingen** post op Hallo links van Hallo pagina toocheck op Hallo inrichtingsproces.
    > 
    > 
12. Zodra het Hallo maken van het proces is voltooid, klikt u op Hallo tegel voor cluster Hallo Hallo Startboard toolaunch Hallo cluster blade. cluster-blade Hallo bevat Hallo volgende informatie.
    
    ![Cluster-blade](./media/hdinsight-hadoop-create-linux-cluster-portal/hdinsight-create-cluster-completed.png "eigenschappen van het Cluster")
    
    Gebruik hello toounderstand Hallo pictogrammen Hallo boven aan deze blade te volgen.
    
    * **Overzicht** tabblad bevat alle Hallo essentiële informatie over Hallo cluster zoals Hallo naam resourcegroep Hallo bij Hallo locatie, Hallo-besturingssysteem, de URL voor de cluster-dashboard hello, enzovoort hoort.
    * **Dashboard** stuurt u toohello Ambari portal die zijn gekoppeld aan het Hallo-cluster.
    * **Secure Shell**: informatie nodig tooaccess Hallo-cluster via SSH.
    * **Schaal cluster** kunt u het aantal worker-knooppunten die zijn gekoppeld aan cluster Hallo Hallo verhogen.
    * **Verwijderen**: verwijderingen Hallo HDInsight-cluster.
    

## <a name="customize-clusters"></a>Clusters aanpassen
* Zie [aanpassen HDInsight-clusters met behulp van de Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md).
* Zie [aanpassen HDInsight-clusters met behulp van de scriptactie](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="delete-hello-cluster"></a>Hallo-cluster verwijderen
[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Problemen oplossen

Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) als u problemen ondervindt met het maken van HDInsight-clusters.

## <a name="next-steps"></a>Volgende stappen
Nu u een HDInsight-cluster hebt gemaakt, gebruiken Hallo toolearn hoe na toowork met het cluster:

### <a name="hadoop-clusters"></a>Hadoop-clusters
* [Hive gebruiken met HDInsight](hdinsight-use-hive.md)
* [Pig gebruiken met HDInsight](hdinsight-use-pig.md)
* [MapReduce gebruiken met HDInsight](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>HBase-clusters
* [Aan de slag met HBase in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md)
* [Ontwikkelen van Java-toepassingen voor HBase in HDInsight](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Storm-clusters
* [Java-topologieën ontwikkelen voor Storm op HDInsight](hdinsight-storm-develop-java-topology.md)
* [Python-onderdelen in Storm op HDInsight gebruiken](hdinsight-storm-develop-python-topology.md)
* [Implementeren en bewaken topologieën met Storm op HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a>Spark-clusters
* [Een zelfstandige toepassing maken met behulp van Scala](hdinsight-apache-spark-create-standalone-application.md)
* [Taken op afstand uitvoeren in een Spark-cluster met behulp van Livy](hdinsight-apache-spark-livy-rest-interface.md)
* [Spark met BI: interactieve gegevensanalyses uitvoeren met behulp van Spark in HDInsight met BI-tools](hdinsight-apache-spark-use-bi-tools.md)
* [Spark met Machine Learning: Spark in HDInsight toopredict voedselinspectieresultaten gebruiken](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark-streaming: Spark in HDInsight gebruiken voor het bouwen van realtime streamingtoepassingen](hdinsight-apache-spark-eventhub-streaming.md)

