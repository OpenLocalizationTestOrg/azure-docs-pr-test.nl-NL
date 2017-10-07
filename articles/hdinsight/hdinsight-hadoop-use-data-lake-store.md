---
title: aaaUse Data Lake Store met Hadoop in Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe tooquery gegevens van Azure Data Lake Store en toostore resultaten van de analyse.
keywords: blob storage, hdfs, gestructureerde gegevens, niet-gestructureerde gegevens, data lake store
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/03/2017
ms.author: jgao
ms.openlocfilehash: 89633218a37a2fe05043e05d61199dcc0252d7f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a>Data Lake Store gebruiken met Azure HDInsight-clusters

tooanalyze gegevens in HDInsight-cluster, kunt u Hallo gegevens opslaan ofwel in [Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), of beide. Beide opties voor opslag kunnen u toosafely verwijdert u het die hdinsight-clusters worden gebruikt voor berekeningen zonder verlies van gebruikersgegevens.

In dit artikel wordt beschreven hoe Data Lake Store werkt met HDInsight-clusters. toolearn hoe Azure Storage werkt met HDInsight-clusters, Zie [Azure Storage gebruiken met Azure HDInsight-clusters](hdinsight-hadoop-use-blob-storage.md). Zie [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) (Hadoop-clusters maken in HDInsight) voor meer informatie over het maken van HDInsight-clusters.

> [!NOTE]
> De toegang tot Data Lake Store verloopt altijd via een beveiligd kanaal, zodat er geen `adls`-bestandssysteemschemanaam is. U gebruikt altijd `adl`.
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a>Beschikbaarheid van HDInsight-clusters

Hadoop ondersteunt een notatie van het standaardbestandssysteem Hallo. Hallo standaardbestandssysteem impliceert een standaardschema en instantie. Het kan ook gebruikte tooresolve relatieve paden zijn. Tijdens het Hallo HDInsight-cluster maken, kunt u een blob-container in Azure Storage als het standaardbestandssysteem Hallo opgeven of u kunt Azure Storage of Azure Data Lake Store met HDInsight 3.5 en nieuwere versies selecteren als Hallo bestanden van het systeem met een enkele uitzonderingen. 

HDInsight-clusters kunnen Data Lake Store op twee manieren gebruiken:

* Als Hallo standaard opslag
* als extra opslag, met Azure Storage Blob als standaardopslag.

Vanaf nu slechts enkele Hallo HDInsight clusterondersteuning typen/versies met Data Lake Store als standaard opslag en extra opslagaccounts:

| HDInsight-clustertype | Data Lake Store als standaardopslag | Data Lake Store als extra opslag| Opmerkingen |
|------------------------|------------------------------------|---------------------------------------|------|
| HDInsight-versie 3.6 | Ja | Ja | |
| HDInsight-versie 3.5 | Ja | Ja | Met uitzondering van HBase Hallo|
| HDInsight-versie 3.4 | Nee | Ja | |
| HDInsight-versie 3.3 | Nee | Nee | |
| HDInsight-versie 3.2 | Nee | Ja | |
| HDInsight Premium (laag)| Nee | Nee | |
| Storm | | |U kunt Data Lake Store toowrite gegevens van een Storm-topologie. U kunt Data Lake Store ook gebruiken voor referentiegegevens die vervolgens kunnen worden gelezen door een Storm-topologie.|

Met behulp van Data Lake Store als extra storage-account niet van invloed op prestaties of Hallo mogelijkheid tooread of tooAzure opslag schrijven van Hallo-cluster.


## <a name="use-data-lake-store-as-default-storage"></a>Data Lake Store als standaardopslag gebruiken

Wanneer HDInsight met Data Lake Store als standaard opslag wordt geïmplementeerd, worden Hallo cluster-gerelateerde bestanden opgeslagen in Data Lake Store in Hallo locatie te volgen:

    adl://mydatalakestore/<cluster_root_path>/

waar `<cluster_root_path>` Hallo naam is van een map die u in Data Lake Store maakt. Als u een pad naar de hoofdmap van ieder cluster opgeeft, kunt u dezelfde Data Lake Store-account voor meer dan één cluster Hallo. U kunt dus instellingen hebben waarbij:

* Cluster1 kunt Hallo pad gebruiken`adl://mydatalakestore/cluster1storage`
* Cluster2 kunt Hallo pad gebruiken`adl://mydatalakestore/cluster2storage`

U ziet dat beide clusters gebruik Hallo Hallo dezelfde Data Lake Store-account **mydatalakestore**. Elk cluster heeft toegang tot tooits eigenaar hoofdmap bestandssysteem in Data Lake Store. Hello Azure portal implementatie-ervaring met name wordt u gevraagd een mapnaam toouse zoals **/clusters/\<clustername >** voor Hallo hoofdpad.

toobe kunnen toouse een Data Lake Store als standaard opslag, moet u verlenen Hallo service principal toegang toohello paden te volgen:

- Hallo Data Lake Store-account root.  Bijvoorbeeld: adl://mydatalakestore/.
- Hallo-map voor alle mappen van het cluster.  Bijvoorbeeld: adl://mydatalakestore/clusters.
- Hallo-map voor het Hallo-cluster.  Bijvoorbeeld: adl://mydatalakestore/clusters/cluster1storage.

Zie [Configure Data Lake store access](#configure-data-lake-store-access) voor meer informatie over het maken van service-principal en het verlenen van toegang.


## <a name="use-data-lake-store-as-additional-storage"></a>Data Lake Store als extra opslag gebruiken

U kunt Data Lake Store als extra opslag voor ook Hallo-cluster. In dergelijke gevallen kan Hallo standaard clusteropslag zijn van een Azure Storage-Blob of een Data Lake Store-account. Als u een HDInsight-taken op Hallo-gegevens die zijn opgeslagen in Data Lake Store als extra opslagruimte uitvoert, moet u Hallo volledig gekwalificeerde pad toohello bestanden gebruiken. Bijvoorbeeld:

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

Er is geen **cluster_root_path** in nu Hallo-URL. Dat komt doordat Data Lake Store is niet een standaard-opslag in dit geval zodat toodo hoeft u Hallo pad toohello bestanden.

toobe kunnen toouse een Data Lake Store als extra opslagruimte, hoeft u alleen toogrant Hallo service principal toegang toohello paden waar uw bestanden worden opgeslagen.  Bijvoorbeeld:

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

Zie [Configure Data Lake store access](#configure-data-lake-store-access) voor meer informatie over het maken van service-principal en het verlenen van toegang.


## <a name="use-more-than-one-data-lake-store-accounts"></a>Meerdere Data Lake Store-accounts gebruiken

Een Data Lake Store-account als extra toe te voegen en het toevoegen van meer dan één Data Lake Store worden accounts bereikt door geeft Hallo HDInsight-cluster toestemming van de gegevens in een of meer Data Lake Store-accounts. Zie [Toegang tot Data Lake Store configureren](#configure-data-lake-store-access).

## <a name="configure-data-lake-store-access"></a>Toegang tot Data Lake Store configureren

tooconfigure Data Lake store toegang vanaf uw HDInsight-cluster, moet u een Azure Active directory (Azure AD) service-principal hebben. Alleen een Azure AD-beheerder kan een service-principal maken. Hallo-service-principal moet worden gemaakt met een certificaat. Zie voor meer informatie [Toegang tot Data Lake Store configureren](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access) en [Service-principal maken met zelfondertekend certificaat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).

> [!NOTE]
> Als u toouse Azure Data Lake Store als extra opslag voor HDInsight-cluster gaat, wordt aangeraden dat u dit doen terwijl u Hallo-cluster maakt, zoals beschreven in dit artikel. Het toevoegen van Azure Data Lake Store als extra opslagruimte tooan is bestaand HDInsight-cluster een ingewikkeld proces en foutgevoelige tooerrors.
>

## <a name="access-files-from-hello-cluster"></a>Toegang tot bestanden Hallo-cluster

Er zijn verschillende manieren Hallo-bestanden in Data Lake Store is toegankelijk vanuit een HDInsight-cluster.

* **De volledig gekwalificeerde naam Hallo**. Met deze methode voert u Hallo volledig pad toohello bestand opgeven dat u wilt dat tooaccess.

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* **Met behulp van de verkorte padindeling Hallo**. Met deze methode voert u Hallo pad up toohello cluster hoofdmap vervangen door adl: / / /. Dus in bovenstaande Hallo voorbeeld, kunt u vervangen `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` met `adl:///`.

        adl:///<file path>

* **Met behulp van het relatieve pad Hallo**. Met deze methode voert u alleen Hallo relatief pad toohello bestand opgeven dat u wilt dat tooaccess. Als bijvoorbeeld Hallo volledige pad toohello bestand is:

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    U hebt toegang tot hetzelfde sample.log bestand Hallo met behulp van deze relatief pad in plaats daarvan.

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-toodata-lake-store"></a>HDInsight-clusters maken met toegang tot tooData Lake Store

Gebruik Hallo koppelingen voor gedetailleerde instructies te volgen op hoe toocreate HDInsight-clusters met toegang tot tooData Lake Store.

* [Portal gebruiken](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [PowerShell gebruiken (met Data Lake Store als standaardopslag)](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [PowerShell gebruiken (met Data Lake Store als extra opslag)](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [Azure-sjablonen gebruiken](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a>Volgende stappen
In dit artikel hebt u geleerd hoe toouse HDFS-compatibele Azure Data Lake Store met HDInsight. Hiermee kunt u toobuild schaalbare, op lange termijn, archiveren voor gegevensverzameling en gebruik HDInsight toounlock Hallo informatie binnen Hallo opgeslagen gestructureerde en ongestructureerde gegevens.

Zie voor meer informatie:

* [Aan de slag met Azure HDInsight][hdinsight-get-started]
* [Aan de slag met Azure Data Lake Store](../data-lake-store/data-lake-store-get-started-portal.md)
* [Uploaden van gegevens tooHDInsight][hdinsight-upload-data]
* [Hive gebruiken met HDInsight][hdinsight-use-hive]
* [Pig gebruiken met HDInsight][hdinsight-use-pig]
* [Azure Storage Shared Access Signatures toorestrict toegang toodata gebruiken met HDInsight][hdinsight-use-sas]

[hdinsight-use-sas]: hdinsight-storage-sharedaccesssignature-permissions.md
[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-creation]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[blob-storage-restAPI]: http://msdn.microsoft.com/library/windowsazure/dd135733.aspx
[azure-storage-create]:../storage/common/storage-create-storage-account.md

[img-hdi-powershell-blobcommands]: ./media/hdinsight-hadoop-use-blob-storage/HDI.PowerShell.BlobCommands.png
[img-hdi-quick-create]: ./media/hdinsight-hadoop-use-blob-storage/HDI.QuickCreateCluster.png
[img-hdi-custom-create-storage-account]: ./media/hdinsight-hadoop-use-blob-storage/HDI.CustomCreateStorageAccount.png  
