---
title: aaaCreate een Apache Spark-cluster in Azure HDInsight | Microsoft Docs
description: HDInsight Spark Quick Start op hoe toocreate een Apache Spark-cluster in HDInsight.
keywords: spark-snelstartgids,interactieve spark,interactieve query,hdinsight spark,azure spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 91f41e6a-d463-4eb4-83ef-7bbb1f4556cc
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/21/2017
ms.author: nitinme
ms.openlocfilehash: 002f71b3cd4fb315d4a556cebc9263026515ec4a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-apache-spark-cluster-in-azure-hdinsight"></a>Een Apache Spark-cluster maken in Azure HDInsight

In dit artikel leert u hoe toocreate een Apache Spark-cluster in Azure HDInsight. Zie [Overzicht: Apache Spark in Azure HDInsight](hdinsight-apache-spark-overview.md) voor informatie over Spark in HDInsight.

   ![Quick Start-diagram met een beschrijving van stappen toocreate een Apache Spark-cluster in Azure HDInsight](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-quickstart-interactive-spark-query-flow.png "Spark snel aan de slag met Apache Spark in HDInsight. Geïllustreerde stappen: maken van een cluster; interactieve Spark-query uitvoeren")

## <a name="prerequisites"></a>Vereisten

* **Een Azure-abonnement**. Voordat u met deze zelfstudie begint, moet u een Azure-abonnement hebben. Zie [Maak vandaag nog uw gratis Azure-account](https://azure.microsoft.com/free).

## <a name="create-hdinsight-spark-cluster"></a>HDInsight Spark-cluster maken

In deze sectie maakt u een HDInsight Spark-cluster met behulp van een [Azure Resource Manager-sjabloon](https://azure.microsoft.com/resources/templates/101-hdinsight-spark-linux/). Zie [HDInsight-clusters maken](hdinsight-hadoop-provision-linux-clusters.md) voor andere methoden voor het maken van clusters.

1. Klik op Hallo installatiekopie tooopen Hallo sjabloon in hello Azure-portal te volgen.         

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-spark-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-apache-spark-jupyter-spark-sql/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. Voer Hallo volgende waarden:

    ![HDInsight Spark-cluster maken met behulp van een Azure Resource Manager-sjabloon](./media/hdinsight-apache-spark-jupyter-spark-sql/create-spark-cluster-in-hdinsight-using-azure-resource-manager-template.png "Spark-cluster maken in HDInsight met behulp van een Azure Resource Manager-sjabloon")

    * **Abonnement**: selecteer uw Azure-abonnement voor dit cluster.
    * **Resourcegroep**: maak een nieuwe resourcegroep of selecteer een bestaande. Resourcegroep is gebruikte toomanage Azure-resources voor uw projecten.
    * **Locatie**: Selecteer een locatie voor resourcegroep Hallo. Hallo-sjabloon maakt gebruik van deze locatie voor het maken van Hallo cluster ook als voor Hallo standaard clusteropslag.
    * **Clusternaam**: Voer een naam voor Hallo HDInsight-cluster dat u wilt dat toocreate.
    * **Spark versie**: Selecteer **2.0** als Hallo-versie die u tooinstall op Hallo-cluster wilt.
    * **Cluster-aanmeldingsnaam en wachtwoord**: Hallo standaardaanmeldnaam is admin.
    * **SSH-aanmeldgegevens**.

   Noteer deze waarden.  U moet ze later in de zelfstudie Hallo.

3. Selecteer **ik ga akkoord toohello voorwaarden bovengenoemde**, selecteer **pincode toodashboard**, en klik vervolgens op **aankoop**. U ziet een nieuwe tegel met de titel Implementatie indienen voor Sjabloonimplementatie. Het duurt ongeveer 20 minuten toocreate Hallo-cluster.

Als u een probleem met het maken van HDInsight-clusters, kan het zijn dat u geen Hallo juiste machtigingen toodo dus hebt. Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) voor meer informatie.

> [!NOTE]
> In dit artikel maakt u een Spark-cluster dat gebruik maakt [Azure Storage-Blobs als Hallo cluster opslag](hdinsight-hadoop-use-blob-storage.md). U kunt ook een Spark-cluster maakt gebruik van maken [Azure Data Lake Store](hdinsight-hadoop-use-data-lake-store.md) als Hallo standaard opslag. Zie [Create an HDInsight cluster with Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md) (Een HDInsight-cluster maken met Data Lake Store) voor instructies.
>
>

## <a name="run-a-hive-query-using-spark-sql"></a>Een Hive-query uitvoeren met Spark SQL

Als u een Jupyter-notebook geconfigureerd voor uw HDInsight Spark-cluster gebruikt, krijgt u een vooraf ingestelde `sqlContext` waarmee u kunt toorun Hive-query's met behulp van Spark SQL. In deze sectie leest u hoe een Jupyter-notebook toostart en voer vervolgens een eenvoudige Hive-query.

1. Open Hallo [Azure-portal](https://portal.azure.com/).

2. Als u toopin Hallo cluster toohello-dashboard hebt gekozen, klikt u op Hallo cluster tegel Hallo dashboard toolaunch Hallo cluster blade.

    Als u niet Hallo cluster toohello dashboard in het linkerdeelvenster hello vastmaken, klikt u op **HDInsight-clusters**, en klik vervolgens op Hallo cluster die u hebt gemaakt.

3. Klik in **Snelkoppelingen** op **Clusterdashboards** en klik vervolgens op **Jupyter Notebook**. Voer desgevraagd Hallo beheerdersreferenties voor Hallo-cluster.

   ![Open Jupyter-notebook toorun interactieve Spark SQL-query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-open-jupyter-interactive-spark-sql-query.png "Open Jupyter-notebook toorun interactieve Spark SQL-query")

   > [!NOTE]
   > Hallo Jupyter-notebook zijn ook toegankelijk voor uw cluster door openen Hallo URL te volgen in uw browser. Vervang **CLUSTERNAME** met Hallo-naam van het cluster:
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. Maak een notebook. Klik op **Nieuw** en klik vervolgens op **PySpark**.

   ![Maken van een Jupyter-notebook toorun interactieve Spark SQL-query](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-create-jupyter-interactive-Spark-SQL-query.png "maken van een Jupyter-notebook toorun interactieve Spark SQL-query")

   Een nieuwe notebook gemaakt en geopend met de naam van de Hallo Untitled(Untitled.pynb).

4. Klik op Hallo notebook naam Hallo boven en een beschrijvende naam invoeren als u wilt.

    ![Geef een naam op voor Hallo Jupter notebook toorun interactieve Spark query van](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-jupyter-notebook-name.png "voor Hallo Jupter notebook toorun interactieve Spark query van een naam opgeven")

5.  Plakken Hallo volgende code in een lege cel en druk vervolgens op **SHIFT + ENTER** toorun Hallo code. In onderstaande Hallo code `%%sql` (aangeroepen Hallo sql magic) vertelt Jupyter-notebook toouse Hallo voorinstelling `sqlContext` toorun Hallo Hive-query. Hallo query top 10 rijen Hallo opgehaald uit een Hive-tabel (**hivesampletable**) die is standaard beschikbaar in alle HDInsight-clusters.

        %%sql
        SELECT * FROM hivesampletable LIMIT 10

    ![Hive-query in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query.png "Hive-query in HDInsight Spark")

    Voor meer informatie over Hallo `%%sql` magic en Hallo voorinstelling contexten, Zie [Jupyter beschikbare kernels voor een HDInsight-cluster](hdinsight-apache-spark-jupyter-notebook-kernels.md).

    > [!NOTE]
    > Telkens wanneer u een query in Jupyter uitvoert, ziet u de venstertitel van uw web-browser een **(bezet)** status samen met de notebooktitel Hallo. U ziet ook een gevulde cirkel volgende toohello **PySpark** tekst in de rechterbovenhoek Hallo. Nadat het Hallo-taak is voltooid, verandert deze tooa lege cirkel.
    >
    >
    
6. welkomstscherm moet uitvoer van tooshow Hallo query vernieuwen.

    ![Uitvoer van Hive-query in HDInsight Spark](./media/hdinsight-apache-spark-jupyter-spark-sql/hdinsight-spark-get-started-hive-query-output.png "Uitvoer van Hive-query in HDInsight Spark")

7. Hallo-notebook toorelease Hallo-clusterbronnen afgesloten nadat u klaar bent met het uitvoeren van de toepassing hello. toodo geval is, uit Hallo **bestand** menu op Hallo laptop, klikt u op **sluiten en stoppen**.

8. Als u van plan toocomplete Hallo volgende stappen op een later tijdstip bent, zorg er dan voor dat u Hallo HDInsight cluster die u hebt gemaakt in dit artikel verwijdert. 

    [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-step"></a>Volgende stap 

In dit artikel hebt u geleerd hoe toocreate een HDInsight Spark-cluster en voer een basic Spark SQL-query. Ga toohello volgende artikel toolearn hoe toouse een HDInsight Spark-cluster toorun interactieve query's op voorbeeldgegevens.

> [!div class="nextstepaction"]
>[Interactieve query's uitvoeren op een HDInsight Spark-cluster](hdinsight-apache-spark-load-data-run-query.md)



