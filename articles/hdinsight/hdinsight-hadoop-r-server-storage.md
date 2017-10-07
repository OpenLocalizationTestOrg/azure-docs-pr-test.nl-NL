---
title: aaaAzure opslagoplossingen mogelijk voor R Server op een HDInsight - Azure | Microsoft Docs
description: Meer informatie over Hallo andere opslag opties beschikbaar toousers met op HDInsight R Server
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 1cf30096-d3ca-45ea-b526-aa3954402f66
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: ff5e80fee14d5e74cbc22e873e6bc1439a3b6037
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a>Azure Storage-oplossingen voor op HDInsight R Server

Microsoft R Server op HDInsight heeft tal van opslaggegevens oplossingen toopersist, code of objecten die bevatten de resultaten van de analyse. Deze omvatten Hallo volgende opties:

- [Azure-blobopslag](https://azure.microsoft.com/services/storage/blobs/)
- [Azure Data Lake Storage](https://azure.microsoft.com/services/data-lake-store/)
- [Azure File storage](https://azure.microsoft.com/services/storage/files/)

U hebt ook Hallo-optie van de toegang tot meerdere Azure storage-accounts of containers met uw HDI-cluster. Azure File storage is een handige gegevens voor de opslagoptie voor gebruik op Hallo edge-knooppunt dat u een Azure Storage-bestandsshare in, bijvoorbeeld Hallo Linux bestandssysteem toomount kunt. Maar Azure-bestandsshares kunnen worden gekoppeld en die wordt gebruikt door een systeem waarop een ondersteund besturingssysteem zoals Windows of Linux. 

Wanneer u een Hadoop-cluster in HDInsight maakt, geeft u ofwel een **Azure storage** account of een **Data Lake store**. Een specifieke storage-container uit dat account bevat Hallo bestandssysteem voor Hallo-cluster dat u (bijvoorbeeld Hallo Hadoop Distributed File System maakt). Zie voor meer informatie en richtlijnen:

- [Azure storage gebruiken met HDInsight](hdinsight-hadoop-use-blob-storage.md)
- [Gebruik Data Lake Store met Azure HDInsight-clusters](hdinsight-hadoop-use-data-lake-store.md). 

Zie voor meer informatie over hello Azure-opslagoplossingen [tooMicrosoft inleiding Azure Storage](../storage/common/storage-introduction.md). 

Zie voor instructies over het selecteren van Hallo meest geschikte opslag optie toouse voor uw scenario [gebruik wanneer toouse Azure Blobs, Azure-bestanden of Azure gegevensschijven](../storage/common/storage-decide-blobs-files-disks.md) 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a>Azure Blob storage-accounts gebruiken met R Server

Indien nodig, kunt u meerdere Azure storage-accounts of containers openen met uw HDI-cluster. toodo u moet dus toospecify Hallo extra opslagaccounts in Hallo UI wanneer u Hallo cluster maken en volg deze stappen toouse ze met R Server.

> [!WARNING]
> Voor prestaties doeleinden, Hallo HDInsight-cluster gemaakt in Hallo hetzelfde Datacenter als Hallo primaire opslagaccount die u opgeeft. Met behulp van een opslagaccount in een andere locatie dan Hallo HDInsight-cluster wordt niet ondersteund.

1. Een HDInsight-cluster maken met de naam van een opslagaccount van **storage1** en standaardcontainer aangeroepen **container1**.
2. Geef een account op extra opslagruimte aangeroepen **storage2**.  
3. Hallo mycsv.csv toohello/share map kopieert en analyse van de op dat bestand.  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. Stel in R-code Hallo naam knooppunt te**standaard** en stel uw tooprocess mappen en bestanden.  

        myNameNode <- "default"
        myPort <- 0

        #Location of hello data:  
        bigDataDirRoot <- "/share"  

        #Define Spark compute context:
        mySparkCluster <- RxSpark(consoleOutput=TRUE)

        #Set compute context:
        rxSetComputeContext(mySparkCluster)

        #Define hello Hadoop Distributed File System (HDFS) file system:
        hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

        #Specify hello input file tooanalyze in HDFS:
        inputFile <-file.path(bigDataDirRoot,"mycsv.csv")

Alle mappen en bestanden verwijzingen punt toohello storage-account Hallo wasb://container1@storage1.blob.core.windows.net. Dit is Hallo **standaard opslagaccount** die is gekoppeld aan Hallo HDInsight-cluster.

Nu, Stel dat u wilt dat tooprocess een bestand met de naam mySpecial.csv bevindt zich op Hallo /private map van **container2** in **storage2**.

Wijs in uw code R Hallo naam knooppunt verwijzing toohello **storage2** storage-account.


    myNameNode <- "wasb://container2@storage2.blob.core.windows.net"
    myPort <- 0

    #Location of hello data:
    bigDataDirRoot <- "/private"

    #Define Spark compute context:
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    #Set compute context:
    rxSetComputeContext(mySparkCluster)

    #Define HDFS file system:
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    #Specify hello input file tooanalyze in HDFS:
    inputFile <-file.path(bigDataDirRoot,"mySpecial.csv")

Alle Hallo map- en verwijzingen nu punt toohello opslagaccount wasb://container2@storage2.blob.core.windows.net. Dit is Hallo **naam knooppunt** die u hebt opgegeven.

U hebt tooconfigure Hallo/User/RevoShare/<SSH username> directory op **storage2** als volgt:


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a>Gebruik een Azure Data Lake store met R Server

toouse Data Lake worden opgeslagen met uw HDInsight-account, moet u toogive na uw cluster toegang tooeach Azure Data Lake store die u toouse wilt. Zie voor instructies over hoe toouse hello Azure portal toocreate een HDInsight-cluster met een Azure Data Lake Store-account als Hallo standaard opslag of als een extra store, [een HDInsight-cluster maken met Data Lake Store met Azure portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

Vervolgens gebruikt u Hallo store in uw R-script veel net zoals een secundaire Azure storage-account zoals beschreven in de vorige procedure Hallo.

### <a name="add-cluster-access-tooyour-azure-data-lake-stores"></a>Cluster toegang tooyour die Azure Data Lake slaat toevoegen
U toegang tot een Data Lake store met behulp van een Service-Principal voor Azure Active Directory (Azure AD) dat is gekoppeld aan uw HDInsight-cluster.

een Azure AD-Service-Principal tooadd:

1. Wanneer u uw HDInsight-cluster maakt, selecteert u **Cluster AAD-identiteit** van Hallo **gegevensbron** tabblad.

2. In Hallo **Cluster AAD-identiteit** dialoogvenster onder **AD Service-Principal selecteren**, selecteer **nieuw**.

Nadat u Service-Principal Hallo Geef een naam en een wachtwoord voor het maken, klikt u op **ADLS-toegang beheren** tooassociate Hallo Service-Principal met uw Data Lake worden opgeslagen.

Het is ook mogelijk tooadd cluster toegang tooone of meer Data Lake worden opgeslagen na het maken van het cluster. Hello Azure portal-vermelding voor een Data Lake store te openen en te gaan**Data Explorer > toegang > toevoegen**. 

### <a name="how-tooaccess-hello-data-lake-store-from-r-server"></a>Hoe tooaccess Hallo Data Lake store van R Server

Zodra u toegang tot tooa Data Lake store gegeven hebt, kunt u Hallo store in R Server op HDInsight Hallo manier als een secundaire Azure storage-account. Hallo enige verschil dat voorvoegsel Hallo is **wasb: / /** wijzigingen te**adl: / /** als volgt:


    # Point toohello ADL store (e.g. ADLtest)
    myNameNode <- "adl://rkadl1.azuredatalakestore.net"
    myPort <- 0

    # Location of hello data (assumes a /share directory on hello ADL account)
    bigDataDirRoot <- "/share"  

    # Define Spark compute context
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    # Set compute context
    rxSetComputeContext(mySparkCluster)

    # Define HDFS file system
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    # Specify hello input file in HDFS tooanalyze
    inputFile <-file.path(bigDataDirRoot,"AirlineDemoSmall.csv")

    # Create factors for days of hello week
    colInfo <- list(DayOfWeek = list(type = "factor",
               levels = c("Monday", "Tuesday", "Wednesday", "Thursday",
                          "Friday", "Saturday", "Sunday")))

    # Define hello data source
    airDS <- RxTextData(file = inputFile, missingValueString = "M",
                    colInfo  = colInfo, fileSystem = hdfsFS)

    # Run a linear regression
    model <- rxLinMod(ArrDelay~CRSDepTime+DayOfWeek, data = airDS)


Hallo volgende opdrachten zijn gebruikte tooconfigure Hallo Data Lake storage-account met Hallo RevoShare directory en Hallo voorbeeld CSV-bestand van het vorige voorbeeld Hallo toevoegen:


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a>Azure File storage gebruiken met R Server

Er is ook een handige gegevens voor de opslagoptie voor gebruik op Hallo edge-knooppunt genoemd Azure Files ((https://azure.microsoft.com/services/storage/files/). Hiermee kunt u toomount een Azure Storage-bestand delen toohello Linux-bestandssysteem. Deze optie is handig voor het opslaan van gegevensbestanden, R-scripts en resultaatobjecten die mogelijk ook later nodig zijn, vooral wanneer het zin toouse Hallo systeemeigen bestandssysteem op Hallo edge-knooppunt in plaats van HDFS maakt. 

Een belangrijk voordeel van Azure Files is dat bestand Hallo shares kunnen worden gekoppeld en die wordt gebruikt door een systeem waarop een ondersteund besturingssysteem zoals Windows of Linux. Het kan bijvoorbeeld worden gebruikt door een andere HDInsight-cluster dat u of iemand in uw team heeft met een virtuele machine in Azure, of zelfs door een on-premises systeem. Zie voor meer informatie:

- [Hoe toouse Azure File storage met Linux](../storage/files/storage-how-to-use-files-linux.md)
- [Hoe toouse Azure File storage in Windows](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a>Volgende stappen

Nu dat u hello Azure opslagopties begrijpt, koppelingen gebruik Hallo volgende toodiscover manieren om gegevens wetenschappelijke taken uitgevoerd met op HDInsight R Server.

* [Overzicht van op HDInsight R Server](hdinsight-hadoop-r-server-overview.md)
* [Aan de slag met R server op Hadoop](hdinsight-hadoop-r-server-get-started.md)
* [RStudio Server tooHDInsight toevoegen (indien niet worden toegevoegd tijdens het maken van het cluster)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Opties voor compute-context voor R Server op HDInsight](hdinsight-hadoop-r-server-compute-contexts.md)

