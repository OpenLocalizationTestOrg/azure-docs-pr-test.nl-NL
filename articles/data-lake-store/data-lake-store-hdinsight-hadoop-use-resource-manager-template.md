---
title: aaaUse Azure-sjablonen toocreate HDInsight en Data Lake Store | Microsoft Docs
description: Gebruik Azure Resource Manager-sjablonen toocreate en HDInsight-clusters gebruiken met Azure Data Lake Store
services: data-lake-store,hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 8ef8152f-2121-461e-956c-51c55144919d
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: nitinme
ms.openlocfilehash: eb88a626f2837dcc29295f3f73a91757059c3bb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-hdinsight-cluster-with-data-lake-store-using-azure-resource-manager-template"></a>Een HDInsight-cluster maken met Data Lake Store met Azure Resource Manager-sjabloon
> [!div class="op_single_selector"]
> * [Portal gebruiken](data-lake-store-hdinsight-hadoop-use-portal.md)
> * [Met behulp van PowerShell (voor opslag van de standaard)](data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
> * [Met behulp van PowerShell (voor extra opslagruimte)](data-lake-store-hdinsight-hadoop-use-powershell.md)
> * [Resource Manager gebruiken](data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)
>
>

Meer informatie over hoe toouse Azure PowerShell tooconfigure een HDInsight-cluster met Azure Data Lake Store **als extra opslagruimte**.

Voor ondersteunde clustertypen, worden Data Lake Store gebruikt als een standaard-opslag- of aanvullende storage-account. Wanneer Data Lake Store als extra opslagruimte wordt gebruikt, Hallo storage-standaardaccount voor Hallo clusters is nog steeds Azure Storage-Blobs (WASB) en Hallo cluster-gerelateerde bestanden (zoals Logboeken, enzovoort) worden nog steeds geschreven toohello standaard opslag tijdens het Hallo-gegevens die u hebt gewenste tooprocess kunnen worden opgeslagen in een Data Lake Store-account. Met behulp van Data Lake Store als extra storage-account heeft geen gevolgen voor prestaties of de Hallo mogelijkheid tooread schrijftijd toohello opslag van Hallo-cluster.

## <a name="using-data-lake-store-for-hdinsight-cluster-storage"></a>Met behulp van Data Lake Store voor opslag van HDInsight-cluster

Hier volgen enkele belangrijke overwegingen voor het gebruik van HDInsight met Data Lake Store:

* Optie toocreate HDInsight-clusters met toegang tooData Lake Store als standaard opslag is beschikbaar voor HDInsight versie 3.5 en 3.6.

* Optie toocreate HDInsight-clusters met toegang tooData Lake Store als extra opslag is beschikbaar voor HDInsight versie 3.2, 3.4, 3.5 en 3.6.

In dit artikel inrichten we een Hadoop-cluster met Data Lake Store als extra opslagruimte. Zie voor instructies over hoe toocreate een Hadoop-cluster met Data Lake Store als standaard opslag, [een HDInsight-cluster maken met Data Lake Store met Azure Portal](data-lake-store-hdinsight-hadoop-use-portal.md).

## <a name="prerequisites"></a>Vereisten
Voordat u deze zelfstudie begint, moet u de volgende Hallo hebben:

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).
* **Azure PowerShell 1.0 of hoger**. Zie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).
* **Azure Active Directory Service-Principal**. Stappen in deze zelfstudie bieden instructies over het toocreate een service-principal in Azure AD. U moet echter een Azure AD-beheerder toobe kunnen toocreate een service-principal. Als u een Azure AD-beheerder bent, kunt u deze vereiste overslaan en doorgaan met het Hallo-zelfstudie.

    **Als u niet een Azure AD-beheerder**, u zich niet kunnen tooperform Hallo stappen vereist toocreate een service-principal. In dat geval moet uw Azure AD-beheerder eerst een service-principal maken voordat u een HDInsight-cluster met Data Lake Store maken kunt. Bovendien Hallo service-principal moet worden gemaakt met een certificaat, zoals beschreven op [een service-principal maken met certificaat](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-certificate-from-certificate-authority).

## <a name="create-an-hdinsight-cluster-with-azure-data-lake-store"></a>Een HDInsight-cluster maken met Azure Data Lake Store
Hallo Resource Manager-sjabloon en Hallo vereisten voor het gebruik van de sjabloon hello, zijn beschikbaar op GitHub op [een HDInsight Linux-cluster met nieuwe Data Lake Store implementeren](https://github.com/Azure/azure-quickstart-templates/tree/master/201-hdinsight-datalake-store-azure-storage). Volg Hallo instructies op deze koppeling toocreate een HDInsight-cluster met Azure Data Lake Store als extra opslagruimte Hallo.

Hallo-instructies op de hierboven genoemde Hallo-koppeling vereist PowerShell. Voordat u met deze instructies begint, zorg er dan voor dat u zich aanmeldt tooyour Azure-account. Op het bureaublad een nieuw Azure PowerShell-venster openen en voer de volgende codefragmenten Hallo. Wanneer de vraag toolog, zorg ervoor dat u zich aanmelden als een Hallo abonnement beheerders/eigenaars:

```
# Log in tooyour Azure account
Login-AzureRmAccount

# List all hello subscriptions associated tooyour account
Get-AzureRmSubscription

# Select a subscription
Set-AzureRmContext -SubscriptionId <subscription ID>
```

## <a name="upload-sample-data-toohello-azure-data-lake-store"></a>Voorbeeld gegevens toohello Azure Data Lake Store uploaden
Hallo Resource Manager-sjabloon een nieuwe Data Lake Store-account maakt en koppelt dit aan Hallo HDInsight-cluster. U moet nu uploaden sommige sample data toohello Data Lake Store. U hebt deze gegevens in Hallo zelfstudie toorun taken van een HDInsight-cluster die toegang gegevens in Data Lake Store hello tot later nodig. Voor instructies over het tooupload van gegevens, Zie [uploaden van een bestand tooyour Data Lake Store](data-lake-store-get-started-portal.md#uploaddata). Als u een aantal gegevens voorbeeld tooupload zoekt, kunt u krijgen Hallo **Ambulance Data** map uit Hallo [Azure Data Lake Git-opslagplaats](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData).

## <a name="set-relevant-acls-on-hello-sample-data"></a>Stel relevante ACL's op Hallo voorbeeldgegevens
toomake ervoor Hallo voorbeeldgegevens die u uploadt, is toegankelijk vanuit Hallo HDInsight-cluster, moet u ervoor zorgen dat hello Azure AD-toepassing die de identiteit van de gebruikte tooestablish tussen Hallo HDInsight-cluster en Data Lake Store toegang toohello bestand/map waarin die u zich heeft tooaccess probeert. toodo dit Hallo volgende stappen uit te voeren.

1. Hallo-naam van hello Azure AD-toepassing die is gekoppeld aan de HDInsight-cluster en Hallo Data Lake Store vinden. Eenzijdige toolook voor de naam van de Hallo tooopen hello HDInsight-cluster blade dat u met Resource Manager-sjabloon Hallo gemaakt, klikt u op Hallo **Cluster AAD-identiteit** tabblad en zoekt u Hallo-waarde van **Service-Principal Weergavenaam**.
2. Bieden nu toegang toothis Azure AD-toepassing op Hallo bestand of de map die u wilt dat tooaccess van Hallo HDInsight-cluster. Zie tooset Hallo rechts ACL's op Hallo bestand of de map in Data Lake Store [beveiligen van gegevens in Data Lake Store](data-lake-store-secure-data.md#filepermissions).

## <a name="run-test-jobs-on-hello-hdinsight-cluster-toouse-hello-data-lake-store"></a>Testtaken uitvoeren op Hallo HDInsight-cluster toouse Hallo Data Lake Store
Nadat u een HDInsight-cluster hebt geconfigureerd, kunt u uitvoeren testtaken op Hallo cluster tootest die Hallo HDInsight cluster toegang heeft tot Data Lake Store. toodo dus voeren we een voorbeeld Hive-taak die u een tabel met voorbeeldgegevens Hallo maakt dat u hebt geüpload eerdere tooyour Data Lake Store.

In deze sectie gaat u SSH in een cluster in HDInsight Linux en Voer Hallo een Hive-voorbeeldquery. Als u een Windows-client gebruikt, wordt u aangeraden **PuTTY**, die kan worden gedownload vanaf [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

Zie voor meer informatie over het gebruik van PuTTY [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).

1. Eenmaal zijn verbonden, start u Hallo CLI Hive via Hallo volgende opdracht:

   ```
   hive
   ```
2. Gebruik Hallo CLI Hallo na toocreate instructies een nieuwe tabel met de naam te geven **voertuigen** met behulp van de voorbeeldgegevens Hallo in Hallo Data Lake Store:

   ```
   DROP TABLE vehicles;
   CREATE EXTERNAL TABLE vehicles (str string) LOCATION 'adl://<mydatalakestore>.azuredatalakestore.net:443/';
   SELECT * FROM vehicles LIMIT 10;
   ```

   U ziet een uitvoer vergelijkbare toohello volgende:

   ```
   1,1,2014-09-14 00:00:03,46.81006,-92.08174,51,S,1
   1,2,2014-09-14 00:00:06,46.81006,-92.08174,13,NE,1
   1,3,2014-09-14 00:00:09,46.81006,-92.08174,48,NE,1
   1,4,2014-09-14 00:00:12,46.81006,-92.08174,30,W,1
   1,5,2014-09-14 00:00:15,46.81006,-92.08174,47,S,1
   1,6,2014-09-14 00:00:18,46.81006,-92.08174,9,S,1
   1,7,2014-09-14 00:00:21,46.81006,-92.08174,53,N,1
   1,8,2014-09-14 00:00:24,46.81006,-92.08174,63,SW,1
   1,9,2014-09-14 00:00:27,46.81006,-92.08174,4,NE,1
   1,10,2014-09-14 00:00:30,46.81006,-92.08174,31,N,1
   ```


## <a name="access-data-lake-store-using-hdfs-commands"></a>Toegang tot Data Lake Store met HDFS-opdrachten
Wanneer u Hallo HDInsight cluster toouse Data Lake Store hebt geconfigureerd, kunt u Hallo HDFS shell-opdrachten tooaccess Hallo store.

In deze sectie gaat u SSH in een cluster in HDInsight Linux en Voer Hallo HDFS-opdrachten. Als u een Windows-client gebruikt, wordt u aangeraden **PuTTY**, die kan worden gedownload vanaf [http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html](http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html).

Zie voor meer informatie over het gebruik van PuTTY [SSH gebruiken met Hadoop op basis van Linux in HDInsight via Windows ](../hdinsight/hdinsight-hadoop-linux-use-ssh-windows.md).

Eenmaal zijn verbonden, gebruik Hallo HDFS bestandssysteem toolist Hallo opdrachtbestanden in Hallo Data Lake Store te volgen.

```
hdfs dfs -ls adl://<Data Lake Store account name>.azuredatalakestore.net:443/
```

Hallo-bestand dat u hebt geüpload eerdere toohello Data Lake Store moet u deze lijst.

```
15/09/17 21:41:15 INFO web.CaboWebHdfsFileSystem: Replacing original urlConnectionFactory with org.apache.hadoop.hdfs.web.URLConnectionFactory@21a728d6
Found 1 items
-rwxrwxrwx   0 NotSupportYet NotSupportYet     671388 2015-09-16 22:16 adl://mydatalakestore.azuredatalakestore.net:443/mynewfolder
```

U kunt ook Hallo `hdfs dfs -put` opdracht tooupload sommige bestanden toohello Data Lake Store en gebruik vervolgens `hdfs dfs -ls` tooverify of Hallo bestanden geüpload.


## <a name="next-steps"></a>Volgende stappen
* [Gegevens kopiëren van Azure Storage Blobs tooData Lake Store](data-lake-store-copy-data-wasb-distcp.md)
