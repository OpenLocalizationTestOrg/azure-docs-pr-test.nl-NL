---
title: aaaCreate Hadoop-cluster met een veilige overdracht storage-accounts in Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe HDInsight-clusters met veilige overdracht toocreate ingeschakeld voor Azure storage-accounts.
keywords: aan de slag met hadoop, hadoop linux, hadoop Quick Start, veilige overdracht, azure opslagaccount
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: jgao
ms.openlocfilehash: 0acb8814ad0d5d5b5652d930b2e3da90f9d7978d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a>Hadoop-cluster maken met opslagaccounts voor veilige overdracht in Azure HDInsight

Hallo [vereiste gegevensoverdracht Secure](../storage/common/storage-require-secure-transfer.md) functie verhoogt Hallo beveiliging van uw Azure Storage-account door het afdwingen van alle aanvragen tooyour-account via een beveiligde verbinding. Deze functie en Hallo wasbs-schema worden alleen ondersteund door de HDInsight-cluster versie 3,6 of hoger. 

## <a name="prerequisites"></a>Vereisten
Voordat u met deze zelfstudie begint, moet u over de volgende onderdelen beschikken:

* **Azure-abonnement**: toocreate een gratis één maand-proefaccount, te bladeren[azure.microsoft.com/free](https://azure.microsoft.com/free).
* **Een Azure-opslagaccount met veilige overdracht**. Zie voor instructies Hallo [een opslagaccount maken](../storage/common/storage-create-storage-account.md#create-a-storage-account) en [vereisen veilige overdracht](../storage/common/storage-require-secure-transfer.md).
* **Een Blob-container op Hallo opslagaccount**. 
## <a name="create-cluster"></a>Cluster maken

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


In deze sectie maakt u een Hadoop-cluster in HDInsight met behulp van een [Azure Resource Manager-sjabloon](../azure-resource-manager/resource-group-template-deploy.md). Hallo-sjabloon bevindt zich in [Github](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/). Het maken van een Azure Resource Manager-sjabloon is niet vereist voor deze zelfstudie. Voor andere methoden voor het maken van cluster en inzicht Hallo-eigenschappen die in deze zelfstudie gebruikt, Zie [HDInsight-clusters maken](hdinsight-hadoop-provision-linux-clusters.md).

1. Klik op Hallo installatiekopie toosign in tooAzure en open Hallo Resource Manager-sjabloon in hello Azure-portal. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. Ga als volgt Hallo instructies toocreate Hallo cluster Hello volgende specificaties: 

    - Geef HDInsight versie 3.6 op.  Hallo standaardversie is 3.5. Versie 3.6 of hoger is vereist.
    - Geef een opslagaccount met veilige overdracht op.
    - Korte naam voor het Hallo-opslagaccount gebruiken.
    - Zowel Hallo storage-account en de blob-container Hallo moeten vooraf worden gemaakt. 

    Zie voor instructies Hallo [cluster maken](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster). 

Als u uw eigen configuratiebestanden script actie tooprovide opgeeft, moet u wasbs in Hallo volgende instellingen:

- fs.defaultFS (core-site)
- spark.eventLog.dir 
- spark.history.fs.logDirectory

## <a name="add-additional-storage-accounts"></a>Extra opslagaccounts toevoegen

Er zijn verschillende opties tooadd extra veilige overdracht ingeschakeld storage-accounts:

- Hello Azure Resource Manager-sjabloon in de laatste sectie Hallo wijzigen.
- Maken van een cluster met de Hallo [Azure-portal](https://portal.azure.com) en gekoppelde storage-account opgeven.
- Gebruik script actie tooadd extra veilige overdracht ingeschakeld storage accounts tooan bestaand HDInsight-cluster.  Zie voor meer informatie [toevoegen van extra opslagruimte accounts tooHDInsight](hdinsight-hadoop-add-storage.md).

## <a name="next-steps"></a>Volgende stappen
In deze zelfstudie hebt u geleerd hoe toocreate een HDInsight-cluster, en schakel veilige transfer toohello storage-accounts.

toolearn meer informatie over het analyseren van gegevens met HDInsight, Zie Hallo artikelen te volgen:

* toolearn meer informatie over het gebruik van Hive met HDInsight, met inbegrip van hoe tooperform Hive query's vanuit Visual Studio, Zie [Hive gebruiken met HDInsight][hdinsight-use-hive].
* toolearn over Pig, een taal gebruikt tootransform gegevens, Zie [Pig gebruiken met HDInsight][hdinsight-use-pig].
* Zie toolearn over MapReduce, een manier toowrite-programma's die gegevens op Hadoop, verwerken [MapReduce gebruiken met HDInsight][hdinsight-use-mapreduce].
* toolearn over het gebruik van Hallo HDInsight Tools voor Visual Studio tooanalyze gegevens in HDInsight, Zie [aan de slag met Visual Studio Hadoop-hulpprogramma's voor HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).

toolearn meer informatie over hoe HDInsight gegevens opslaat of hoe tooget gegevens in HDInsight, raadpleegt u Hallo artikelen te volgen:

* Zie [Azure Storage gebruiken met HDInsight](hdinsight-hadoop-use-blob-storage.md) voor meer informatie over hoe HDInsight Azure Storage gebruikt.
* Voor meer informatie over tooupload gegevens tooHDInsight, Zie [uploaden van gegevens tooHDInsight][hdinsight-upload-data].

toolearn meer informatie over het maken of beheren van een HDInsight-cluster, Zie Hallo artikelen te volgen:

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


