---
title: aaaUse hello Azure portal toocreate Azure HDInsight-clusters met Data Lake Store | Microsoft Docs
description: Gebruik hello Azure portal toocreate en HDInsight-clusters gebruiken met Azure Data Lake Store
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: a8c45a83-a8e3-4227-8b02-1bc1e1de6767
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: nitinme
ms.openlocfilehash: f23113d444a3c5a01894dba29f75f3621b2d16bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-with-data-lake-store-by-using-hello-azure-portal"></a>HDInsight-clusters maken met Data Lake Store met behulp van hello Azure-portal
> [!div class="op_single_selector"]
> * [Gebruik hello Azure-portal](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Gebruik PowerShell (voor opslag van de standaard)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Gebruik PowerShell (voor extra opslagruimte)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Gebruik Resource Manager](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Meer informatie over hoe toouse hello Azure portal toocreate een HDInsight-cluster met een Azure Data Lake Store-account als Hallo standaard opslag of een extra opslagruimte. Hoewel de extra opslagruimte is optioneel voor een HDInsight-cluster, is de aanbevolen toostore uw zakelijke gegevens op Hallo extra opslagaccounts.

## <a name="prerequisites"></a>Vereisten
Voordat u deze zelfstudie begint, zorg ervoor dat u Hallo volgens de vereisten hebt voldaan:

* **Een Azure-abonnement**. Ga te[gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).
* **Een Azure Data Lake Store-account**. Volg de instructies uit Hallo [aan de slag met Azure Data Lake Store met behulp van Azure-portal Hallo](data-lake-store-get-started-portal.md). U moet ook een hoofdmap op Hallo-account maken.  In deze zelfstudie een hoofdmap aangeroepen __/clusters__ wordt gebruikt.
* **Een Azure Active Directory-service-principal**. Deze handleiding bevat instructies voor het toocreate een service-principal in Azure Active Directory (Azure AD). Echter, een service-principal toocreate, moet u een Azure AD-beheerder. Als u een beheerder bent, kunt u deze vereiste overslaan en doorgaan met het Hallo-zelfstudie.

    >[!NOTE]
    >U kunt een service principal maken alleen als u een Azure AD-beheerder. Uw Azure AD-beheerder moet maken een service principal voordat u een HDInsight-cluster met Data Lake Store maken kunt. Bovendien Hallo service-principal moet worden gemaakt met een certificaat, zoals beschreven op [een service-principal maken met certificaat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).
    >

## <a name="create-an-hdinsight-cluster"></a>Een HDInsight-cluster maken

In deze sectie maakt u een HDInsight-cluster met Data Lake Store-accounts als Hallo standaard of Hallo extra opslagruimte. Dit artikel is alleen gericht Hallo-onderdeel van het Data Lake Store-accounts configureren.  Zie voor Hallo algemene cluster maken informatie en procedures [maken Hadoop-clusters in HDInsight](../hdinsight/hdinsight-hadoop-provision-linux-clusters.md).

### <a name="create-a-cluster-with-data-lake-store-as-default-storage"></a>Een cluster met Data Lake Store als standaard opslag maken

**toocreate een HDInsight-cluster met een Data Lake Store als Hallo storage-standaardaccount**

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Ga als volgt [clusters maken](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) voor Hallo algemene informatie over het maken van HDInsight-clusters.
3. Op Hallo **opslag** blade onder **primaire opslagtype**, selecteer **Data Lake Store**, en voer de volgende informatie Hallo:

    ![Add service-principal tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.adls.storage.png "service principal tooHDInsight-cluster toevoegen")

    - **Selecteer Data Lake Store-account**: Selecteer een bestaande Data Lake Store-account. Er is een bestaande Data Lake Store-account vereist.  Zie [vereisten](#prereuisites).
    - **Hoofdpad naar**: Geef een pad op waar Hallo cluster-specifieke bestanden toobe opgeslagen zijn. Op het Hallo-schermafbeelding is __/clusters/myhdiadlcluster/__, in welke Hallo __/clusters__ map moet bestaan en hello Portal maakt *myhdicluster* map.  Hallo *myhdicluster* Hallo clusternaam.
    - **Data Lake Store toegang**: toegang tussen Hallo Data Lake Store-account en HDInsight-cluster configureren. Zie voor instructies [Configure Data Lake Store toegang](#configure-data-lake-store-access).
    - **Extra opslagaccounts**: Azure Storage-Accounts toevoegen als extra opslagruimte accounts voor Hallo-cluster. tooadd extra Data Lake winkels wordt gedaan door middel van een Hallo cluster machtigingen van de gegevens in Data Lake Store-accounts meer tijdens het configureren van een Data Lake Store-account als de primaire opslagtype Hallo. Zie [Toegang tot Data Lake Store configureren](#configure-data-lake-store-access).

4. Op Hallo **Data Lake Store toegang**, klikt u op **Selecteer**, en ga verder met maken van het cluster, zoals beschreven in [maken Hadoop-clusters in HDInsight](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md).


### <a name="create-a-cluster-with-data-lake-store-as-additional-storage"></a>Een cluster maken met Data Lake Store als extra opslagruimte

Hallo maakt volgende instructies een HDInsight-cluster met een Azure Storage-account als Hallo standaard opslag en een Data Lake Store-account als extra opslag.
**toocreate een HDInsight-cluster met een Data Lake Store als Hallo storage-standaardaccount**

1. Meld u aan toohello [Azure-portal](https://portal.azure.com).
2. Ga als volgt [clusters maken](../hdinsight/hdinsight-hadoop-create-linux-clusters-portal.md#create-clusters) voor Hallo algemene informatie over het maken van HDInsight-clusters.
3. Op Hallo **opslag** blade onder **primaire opslagtype**, selecteer **Azure Storage**, en voer de volgende informatie Hallo:

    ![Add service-principal tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.1.png "service principal tooHDInsight-cluster toevoegen")

    - **Selectiemethode**: gebruik een van de Hallo volgende opties:

        * Selecteer een opslagaccount die deel uitmaakt van uw Azure-abonnement toospecify **abonnementen**, en selecteer vervolgens Hallo storage-account.
        * een opslagaccount die zich buiten uw Azure-abonnement, selecteer toospecify **toegangssleutel**, en geef vervolgens Hallo-informatie voor Hallo buiten de storage-account.

    - **Standaardcontainer**: Gebruik de standaardwaarde Hallo of geef de naam van uw eigen.

    - Extra Storage-accounts: meer Azure Storage-accounts toevoegen als Hallo extra opslagruimte.
    - Data Lake Store toegang: toegang tussen Hallo Data Lake Store-account en HDInsight-cluster configureren. Zie voor instructies [Configure Data Lake Store toegang](#configure-data-lake-store-access).

## <a name="configure-data-lake-store-access"></a>Data Lake Store toegang configureren 

In deze sectie configureert u Data Lake Store-toegang van HDInsight-clusters met een Azure Active Directory-service-principal. 

### <a name="specify-a-service-principal"></a>Geef een service-principal

Van hello Azure-portal, moet u een bestaande service-principal gebruiken of een nieuwe maken.

**toocreate een service-principal van hello Azure-portal**

1. Klik op **Data Lake Store toegang** Hallo Store-blade.
2. Op Hallo **Data Lake Store toegang** blade, klikt u op **nieuw**.
3. Klik op **Service-Principal**, en volg Hallo instructies toocreate een service-principal.
4. Hallo-certificaat downloaden als u toouse besluit opnieuw in toekomstige Hallo. Downloaden Hallo-certificaat is handig dat als u wilt dat toouse Hallo dezelfde service-principal bij het maken van aanvullende HDInsight-clusters.

    ![Add service-principal tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.2.png "service principal tooHDInsight-cluster toevoegen")

4. Klik op **toegang** tooconfigure Hallo maptoegang.  Zie [bestandsmachtigingen configureren](#configure-file-permissions).


**toouse een bestaande service-principal van hello Azure-portal**

1. Klik op **Data Lake Store toegang**.
1. Op Hallo **Data Lake Store toegang** blade, klikt u op **gebruik bestaande**.
2. Klik op **Service-Principal**, en selecteer vervolgens een service-principal. 
3. Hallo-certificaat (.pfx-bestand) die is gekoppeld aan de geselecteerde service-principal uploaden en voer vervolgens het certificaatwachtwoord Hallo.

    ![Add service-principal tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.5.png "service principal tooHDInsight-cluster toevoegen")

4. Klik op **toegang** tooconfigure Hallo maptoegang.  Zie [bestandsmachtigingen configureren](#configure-file-permissions).


### <a name="configure-file-permissions"></a>Bestandsmachtigingen configureren

Hallo configureert zijn verschillend afhankelijk van of Hallo-account wordt gebruikt als Hallo standaard opslag of een extra storage-account:

- Gebruikt als standaard opslag

    - machtiging op hoofdniveau Hallo Hallo Data Lake Store-account
    - de machtiging op hoofdniveau Hallo Hallo opslag van HDInsight-cluster. Bijvoorbeeld, Hallo __/clusters__ map die eerder in de zelfstudie hello wordt gebruikt.
- Als extra opslag gebruiken

    - De machtiging op Hallo mappen waarin u de toegang moet opslaan.

**tooassign toestemming op Hallo hoofdniveau Data Lake Store-account**

1. Op Hallo **Data Lake Store toegang** blade, klikt u op **toegang**. Hallo **Selecteer bestandsmachtigingen** blade wordt geopend. Geeft alle Hallo Data Lake Store-accounts in uw abonnement.
2. Beweeg de muisaanwijzer (niet op) Hallo muis op de naam van de Hallo Hallo toomake Hallo selectievakje zichtbaar is, en selecteer het selectievakje Hallo Data Lake Store-account.

    ![Add service-principal tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3.png "service principal tooHDInsight-cluster toevoegen")

  Standaard __lezen__, __schrijven__, en __EXECUTE__ zijn geselecteerd.

3. Klik op **Selecteer** op Hallo onder aan Hallo pagina.
4. Klik op **uitvoeren** tooassign machtiging.
5. Klik op **Gereed**.

**tooassign toestemming op Hallo hoofdniveau HDInsight-cluster**

1. Op Hallo **Data Lake Store toegang** blade, klikt u op **toegang**. Hallo **Selecteer bestandsmachtigingen** blade wordt geopend. Geeft alle Hallo Data Lake Store-accounts in uw abonnement.
1. Van Hallo **Selecteer bestandsmachtigingen** blade, klikt u op Hallo Data Lake Store naam tooshow de inhoud ervan.
2. Gewenste Hallo HDInsight-cluster opslag hoofdmap Hallo selectievakje op Hallo links van de map Hallo selecteren. Hallo cluster opslag hoofdmap is toohello schermafbeelding eerder volgens, __/clusters__ map die u hebt opgegeven tijdens het Hallo Data Lake Store als standaard opslag selecteren.
3. Hallo-machtigingen voor map Hallo instellen.  Standaard lezen, schrijven en uitvoeren zijn geselecteerd.
4. Klik op **Selecteer** op Hallo onder aan Hallo pagina.
5. Klik op **Run**.
6. Klik op **Gereed**.

Als u Data Lake Store als extra opslagruimte gebruikt, moet u toewijzen machtiging alleen voor Hallo mappen dat u wilt dat tooaccess van Hallo HDInsight-cluster. Bijvoorbeeld in Hallo onderstaande schermafbeelding u bieden toegang alleen te**hdiaddonstorage** map in een Data Lake Store-account.

![Service-principal machtigingen toohello HDInsight-cluster toewijzen](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.3-1.png "toewijzen service principal machtigingen toohello HDInsight-cluster")


## <a name="verify-cluster-set-up"></a>Controleer of cluster instellen

Nadat Hallo cluster setup voltooid is, op de cluster-blade hello, controleert u of uw resultaten als volgt een of beide Hallo stappen te volgen:

* tooverify die Hallo gekoppelde opslag voor Hallo cluster Hallo Data Lake Store-account die u hebt opgegeven is, klikt u op **opslagaccounts** in het linkerdeelvenster Hallo.

    ![Add service-principal tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6-1.png "service principal tooHDInsight-cluster toevoegen")

* tooverify die Hallo service-principal is correct gekoppeld Hallo HDInsight-cluster, klik op **Data Lake Store toegang** in het linkerdeelvenster Hallo.

    ![Add service-principal tooHDInsight cluster](./media/data-lake-store-hdinsight-hadoop-use-portal/hdi.adl.6.png "service principal tooHDInsight-cluster toevoegen")


## <a name="examples"></a>Voorbeelden

Nadat u Hallo-cluster met Data Lake Store als uw opslag hebt ingesteld, Raadpleeg toothese voorbeelden van hoe toouse HDInsight-cluster tooanalyze Hallo gegevens die zijn opgeslagen in Data Lake Store.

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-primary-storage"></a>Een Hive-query uitvoeren op gegevens in een Data Lake Store (als primaire opslag)

een Hive-query toorun Hallo Hive weergaven interface in Hallo Ambari-portal gebruiken. Zie voor instructies over hoe toouse Ambari Hive-weergaven, [gebruik Hallo Hive-weergave met Hadoop in HDInsight](../hdinsight/hdinsight-hadoop-use-hive-ambari-view.md).

Wanneer u met gegevens in een Data Lake Store werkt, zijn er enkele tekenreeksen toochange.

Als u, bijvoorbeeld Hallo-cluster gebruiken die u hebt gemaakt met Data Lake Store als primaire opslag Hallo pad toohello gegevens zijn: *adl: / / < data_lake_store_account_name > /azuredatalakestore.net/path/to/file*. Een Hive-query toocreate een tabel met voorbeeldgegevens die zijn opgeslagen in Data Lake Store-account Hallo ziet eruit als Hallo-instructie:

    CREATE EXTERNAL TABLE websitelog (str string) LOCATION 'adl://hdiadlsstorage.azuredatalakestore.net/clusters/myhdiadlcluster/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/'

Beschrijvingen van:
* `adl://hdiadlstorage.azuredatalakestore.net/`Hallo-hoofdmap Hallo Data Lake Store-account is.
* `/clusters/myhdiadlcluster`bevat Hallo Hallo cluster gegevens die u hebt opgegeven tijdens het Hallo-cluster maken.
* `/HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/`is de locatie Hallo van Hallo-voorbeeldbestand die u hebt gebruikt in Hallo-query.

### <a name="run-a-hive-query-against-data-in-a-data-lake-store-as-additional-storage"></a>Een Hive-query uitvoeren op gegevens in een Data Lake Store (als extra opslag)

Als Hallo-cluster dat u hebt gemaakt Blob-opslag als standaard opslag gebruikt, Hallo voorbeeldgegevens niet is opgenomen in hello Azure Data Lake Store-account dat wordt gebruikt als extra opslagruimte. In dat geval eerst Hallo gegevens overbrengt uit Blob storage toohello Data Lake Store en voer vervolgens de Hallo query's zoals weergegeven in het voorgaande voorbeeld Hallo.

Zie voor informatie over hoe toocopy gegevens uit Blob storage tooa Data Lake opslaan, Hallo artikelen te volgen:

* [Distcp toocopy gegevens gebruiken tussen Azure Storage-blobs en Data Lake Store](data-lake-store-copy-data-wasb-distcp.md)
* [Gebruik AdlCopy toocopy gegevens uit Azure Storage blobs tooData Lake Store](data-lake-store-copy-data-azure-storage-blob.md)

### <a name="use-data-lake-store-with-a-spark-cluster"></a>Gebruik Data Lake Store met een Spark-cluster
U kunt een Spark-cluster toorun Spark taken gebruiken voor gegevens die zijn opgeslagen in een Data Lake Store. Zie voor meer informatie [gebruik HDInsight Spark-cluster tooanalyze gegevens in Data Lake Store](../hdinsight/hdinsight-apache-spark-use-with-data-lake-store.md).


### <a name="use-data-lake-store-in-a-storm-topology"></a>Gebruik Data Lake Store in een Storm-topologie
U kunt Hallo Data Lake Store toowrite gegevens van een Storm-topologie. Voor instructies over het tooachieve dit scenario, Zie [gebruik Azure Data Lake Store met Apache Storm met HDInsight](../hdinsight/hdinsight-storm-write-data-lake-store.md).

## <a name="see-also"></a>Zie ook
* [PowerShell: Een HDInsight-cluster toouse Data Lake Store maken](data-lake-store-hdinsight-hadoop-use-powershell.md)

[makecert]: https://msdn.microsoft.com/library/windows/desktop/ff548309(v=vs.85).aspx
[pvk2pfx]: https://msdn.microsoft.com/library/windows/desktop/ff550672(v=vs.85).aspx
