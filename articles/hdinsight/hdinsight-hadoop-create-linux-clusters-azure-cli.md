---
title: aaaCreate Hadoop-clusters met behulp van de opdrachtregel - hello Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe toocreate HDInsight-clusters met meerdere platforms Azure CLI 1.0 Hallo.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 50b01483-455c-4d87-b754-2229005a8ab9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 5295b01054b8c23df0e3b75a3e0e8c933ac48b3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-using-hello-azure-cli"></a>Maken van HDInsight-clusters met hello Azure CLI

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Hallo stappen in dit document procedure voor het maken van een 3.5 HDInsight-cluster met behulp van hello Azure CLI 1.0.

> [!IMPORTANT]
> Linux is Hallo enige besturingssysteem gebruikt op HDInsight versie 3.4 of hoger. Zie [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement) (HDInsight buiten gebruik gestel voor Windows) voor meer informatie.


## <a name="prerequisites"></a>Vereisten

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* **Een Azure-abonnement**. Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).

* **Azure CLI**. Hallo stappen in dit document zijn laatste getest met Azure CLI versie 0.10.14.

    > [!IMPORTANT]
    > Hallo stappen in dit document werken niet met Azure CLI 2.0. Azure CLI 2.0 biedt geen ondersteuning voor het maken van een HDInsight-cluster.

## <a name="log-in-tooyour-azure-subscription"></a>Meld u bij tooyour Azure-abonnement

Hallo stappen beschreven in [tooan Azure-abonnement van hello Azure-opdrachtregelinterface (Azure CLI) verbinding](../xplat-cli-connect.md) en maak verbinding met Hallo tooyour-abonnement **aanmelding** methode.

## <a name="create-a-cluster"></a>Een cluster maken

Hallo stappen moet worden uitgevoerd vanaf een opdrachtregel zoals PowerShell of Bash.

1. Gebruik Hallo opdracht tooauthenticate tooyour Azure-abonnement te volgen:

        azure login

    U na vragen aan gebruiker tooprovide zijn uw naam en wachtwoord. Als u meerdere Azure-abonnementen hebt, gebruikt u `azure account set <subscriptionname>` tooset Hallo abonnement dat hello Azure CLI-opdrachten gebruiken.

2. De modus Resource Manager tooAzure met behulp van de volgende opdracht Hallo switch:

        azure config mode arm

3. Maak een resourcegroep. Deze resourcegroep bevat Hallo HDInsight-cluster en storage-account gekoppeld.

        azure group create groupname location

    * Vervang `groupname` met een unieke naam voor de groep Hallo.

    * Vervang `location` met Hallo geografische regio die u wilt dat toocreate Hallo groep in.

       Gebruik voor een lijst met geldige locaties, Hallo `azure location list` opdracht en gebruik vervolgens een van de locaties van Hallo Hallo `Name` kolom.

4. Een opslagaccount maken. Dit opslagaccount wordt gebruikt als Hallo standaard opslag voor Hallo HDInsight-cluster.

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * Vervang `groupname` met de naam van Hallo groep gemaakt in de vorige stap Hallo Hallo.

    * Vervang `location` met dezelfde locatie worden gebruikt in de vorige stap Hallo Hallo.

    * Vervang `storagename` met een unieke naam voor het Hallo-opslagaccount.

        > [!NOTE]
        > Voor meer informatie over Hallo-parameters die worden gebruikt in deze opdracht gebruiken `azure storage account create -h` tooview help voor deze opdracht.

5. Hallo-sleutel ophalen tooaccess Hallo storage-account gebruikt.

        azure storage account keys list -g groupname storagename

    * Vervang `groupname` met de naam van resourcegroep Hallo.
    * Vervang `storagename` met de naam van het opslagaccount Hallo Hallo.

     Hallo-gegevens die wordt geretourneerd, opslaan Hallo `key` waarde voor `key1`.

6. Maak een HDInsight-cluster.

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * Vervang `groupname` met de naam van resourcegroep Hallo.

    * Vervang `Hadoop` met type Hallo-cluster dat u wenst dat toocreate. Bijvoorbeeld: `Hadoop`, `HBase`, `Kafka`, `Spark`, of `Storm`.

     > [!IMPORTANT]
     > HDInsight clusters worden geleverd in verschillende typen die overeenkomen met de werkbelasting toohello of technologie voor het cluster Hallo is afgestemd op. Er is geen ondersteunde methode toocreate van een cluster waarin meerdere typen zoals Storm en HBase op één cluster.

    * Vervang `location` Hello dezelfde locatie worden gebruikt in de vorige stappen.

    * Vervang `storagename` met Hallo opslagaccountnaam.

    * Vervang `storagekey` met Hallo-sleutel in de vorige stap Hallo verkregen.

    * Voor Hallo `--defaultStorageContainer` parameter, gebruik Hallo dezelfde naam als u voor het Hallo-cluster gebruikt.

    * Vervang `admin` en `httppassword` met Hallo naam en het wachtwoord u wenst dat toouse bij het openen van Hallo-cluster via HTTPS.

    * Vervang `sshuser` en `sshuserpassword` met Hallo gebruikersnaam en wachtwoord desgewenst toouse bij het openen van Hallo-cluster via SSH

    > [!IMPORTANT]
    > In dit voorbeeld maakt een cluster met twee worker opmerkingen. U kunt ook het aantal worker-knooppunten Hallo na het maken van het cluster wijzigen door het vergroten/verkleinen bewerkingen uitvoert. Als u van plan bent over het gebruik van meer dan 32 worker-knooppunten, selecteert u een grootte van het hoofdknooppunt met ten minste 8 kerngeheugens en 14 GB RAM-geheugen. U kunt Hallo hoofdknooppunt grootte instellen met behulp van Hallo `--headNodeSize` parameter tijdens het maken van het cluster.
    >
    > Zie voor meer informatie over knooppuntgrootten en bijbehorende kosten [HDInsight prijzen](https://azure.microsoft.com/pricing/details/hdinsight/).

    Het kan enkele minuten duren voordat Hallo cluster maken van het proces toofinish. Meestal ongeveer 15.

## <a name="troubleshoot"></a>Problemen oplossen

Zie [Vereisten voor toegangsbeheer](hdinsight-administer-use-portal-linux.md#create-clusters) als u problemen ondervindt met het maken van HDInsight-clusters.

## <a name="next-steps"></a>Volgende stappen

Nu u een HDInsight-cluster met behulp van hello Azure CLI hebt gemaakt, gebruiken Hallo toolearn hoe na toowork met het cluster:

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
