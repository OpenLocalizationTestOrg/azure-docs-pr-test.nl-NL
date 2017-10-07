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
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a><span data-ttu-id="c8b20-103">Azure Storage-oplossingen voor op HDInsight R Server</span><span class="sxs-lookup"><span data-stu-id="c8b20-103">Azure Storage solutions for R Server on HDInsight</span></span>

<span data-ttu-id="c8b20-104">Microsoft R Server op HDInsight heeft tal van opslaggegevens oplossingen toopersist, code of objecten die bevatten de resultaten van de analyse.</span><span class="sxs-lookup"><span data-stu-id="c8b20-104">Microsoft R Server on HDInsight has a variety of storage solutions toopersist data, code, or objects that contain results from analysis.</span></span> <span data-ttu-id="c8b20-105">Deze omvatten Hallo volgende opties:</span><span class="sxs-lookup"><span data-stu-id="c8b20-105">These include hello following options:</span></span>

- [<span data-ttu-id="c8b20-106">Azure-blobopslag</span><span class="sxs-lookup"><span data-stu-id="c8b20-106">Azure Blob</span></span>](https://azure.microsoft.com/services/storage/blobs/)
- [<span data-ttu-id="c8b20-107">Azure Data Lake Storage</span><span class="sxs-lookup"><span data-stu-id="c8b20-107">Azure Data Lake Storage</span></span>](https://azure.microsoft.com/services/data-lake-store/)
- [<span data-ttu-id="c8b20-108">Azure File storage</span><span class="sxs-lookup"><span data-stu-id="c8b20-108">Azure File storage</span></span>](https://azure.microsoft.com/services/storage/files/)

<span data-ttu-id="c8b20-109">U hebt ook Hallo-optie van de toegang tot meerdere Azure storage-accounts of containers met uw HDI-cluster.</span><span class="sxs-lookup"><span data-stu-id="c8b20-109">You also have hello option of accessing multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="c8b20-110">Azure File storage is een handige gegevens voor de opslagoptie voor gebruik op Hallo edge-knooppunt dat u een Azure Storage-bestandsshare in, bijvoorbeeld Hallo Linux bestandssysteem toomount kunt.</span><span class="sxs-lookup"><span data-stu-id="c8b20-110">Azure File storage is a convenient data storage option for use on hello edge node that enables you toomount an Azure Storage file share to, for example, hello Linux file system.</span></span> <span data-ttu-id="c8b20-111">Maar Azure-bestandsshares kunnen worden gekoppeld en die wordt gebruikt door een systeem waarop een ondersteund besturingssysteem zoals Windows of Linux.</span><span class="sxs-lookup"><span data-stu-id="c8b20-111">But Azure File shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> 

<span data-ttu-id="c8b20-112">Wanneer u een Hadoop-cluster in HDInsight maakt, geeft u ofwel een **Azure storage** account of een **Data Lake store**.</span><span class="sxs-lookup"><span data-stu-id="c8b20-112">When you create an Hadoop cluster in HDInsight, you specify either an **Azure storage** account or a **Data Lake store**.</span></span> <span data-ttu-id="c8b20-113">Een specifieke storage-container uit dat account bevat Hallo bestandssysteem voor Hallo-cluster dat u (bijvoorbeeld Hallo Hadoop Distributed File System maakt).</span><span class="sxs-lookup"><span data-stu-id="c8b20-113">A specific storage container from that account holds hello file system for hello cluster that you create (for example, hello Hadoop Distributed File System).</span></span> <span data-ttu-id="c8b20-114">Zie voor meer informatie en richtlijnen:</span><span class="sxs-lookup"><span data-stu-id="c8b20-114">For more information and guidance, see:</span></span>

- [<span data-ttu-id="c8b20-115">Azure storage gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="c8b20-115">Use Azure storage with HDInsight</span></span>](hdinsight-hadoop-use-blob-storage.md)
- <span data-ttu-id="c8b20-116">[Gebruik Data Lake Store met Azure HDInsight-clusters](hdinsight-hadoop-use-data-lake-store.md).</span><span class="sxs-lookup"><span data-stu-id="c8b20-116">[Use Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> 

<span data-ttu-id="c8b20-117">Zie voor meer informatie over hello Azure-opslagoplossingen [tooMicrosoft inleiding Azure Storage](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c8b20-117">For more information on hello Azure storage solutions, see [Introduction tooMicrosoft Azure Storage](../storage/common/storage-introduction.md).</span></span> 

<span data-ttu-id="c8b20-118">Zie voor instructies over het selecteren van Hallo meest geschikte opslag optie toouse voor uw scenario [gebruik wanneer toouse Azure Blobs, Azure-bestanden of Azure gegevensschijven](../storage/common/storage-decide-blobs-files-disks.md)</span><span class="sxs-lookup"><span data-stu-id="c8b20-118">For guidance on selecting hello most appropriate storage option toouse for your scenario, see [Deciding when toouse Azure Blobs, Azure Files, or Azure Data Disks](../storage/common/storage-decide-blobs-files-disks.md)</span></span> 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a><span data-ttu-id="c8b20-119">Azure Blob storage-accounts gebruiken met R Server</span><span class="sxs-lookup"><span data-stu-id="c8b20-119">Use Azure Blob storage accounts with R Server</span></span>

<span data-ttu-id="c8b20-120">Indien nodig, kunt u meerdere Azure storage-accounts of containers openen met uw HDI-cluster.</span><span class="sxs-lookup"><span data-stu-id="c8b20-120">If necessary, you can access multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="c8b20-121">toodo u moet dus toospecify Hallo extra opslagaccounts in Hallo UI wanneer u Hallo cluster maken en volg deze stappen toouse ze met R Server.</span><span class="sxs-lookup"><span data-stu-id="c8b20-121">toodo so, you need toospecify hello additional storage accounts in hello UI when you create hello cluster, and then follow these steps toouse them with R Server.</span></span>

> [!WARNING]
> <span data-ttu-id="c8b20-122">Voor prestaties doeleinden, Hallo HDInsight-cluster gemaakt in Hallo hetzelfde Datacenter als Hallo primaire opslagaccount die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="c8b20-122">For performance purposes, hello HDInsight cluster is created in hello same data center as hello primary storage account that you specify.</span></span> <span data-ttu-id="c8b20-123">Met behulp van een opslagaccount in een andere locatie dan Hallo HDInsight-cluster wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="c8b20-123">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span>

1. <span data-ttu-id="c8b20-124">Een HDInsight-cluster maken met de naam van een opslagaccount van **storage1** en standaardcontainer aangeroepen **container1**.</span><span class="sxs-lookup"><span data-stu-id="c8b20-124">Create an HDInsight cluster with a storage account name of **storage1** and a default container called **container1**.</span></span>
2. <span data-ttu-id="c8b20-125">Geef een account op extra opslagruimte aangeroepen **storage2**.</span><span class="sxs-lookup"><span data-stu-id="c8b20-125">Specify an additional storage account called **storage2**.</span></span>  
3. <span data-ttu-id="c8b20-126">Hallo mycsv.csv toohello/share map kopieert en analyse van de op dat bestand.</span><span class="sxs-lookup"><span data-stu-id="c8b20-126">Copy hello mycsv.csv file toohello /share directory, and perform analysis on that file.</span></span>  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. <span data-ttu-id="c8b20-127">Stel in R-code Hallo naam knooppunt te**standaard** en stel uw tooprocess mappen en bestanden.</span><span class="sxs-lookup"><span data-stu-id="c8b20-127">In R code, set hello name node too**default,** and set your directory and file tooprocess.</span></span>  

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

<span data-ttu-id="c8b20-128">Alle mappen en bestanden verwijzingen punt toohello storage-account Hallo wasb://container1@storage1.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="c8b20-128">All hello directory and file references point toohello storage account wasb://container1@storage1.blob.core.windows.net.</span></span> <span data-ttu-id="c8b20-129">Dit is Hallo **standaard opslagaccount** die is gekoppeld aan Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="c8b20-129">This is hello **default storage account** that's associated with hello HDInsight cluster.</span></span>

<span data-ttu-id="c8b20-130">Nu, Stel dat u wilt dat tooprocess een bestand met de naam mySpecial.csv bevindt zich op Hallo /private map van **container2** in **storage2**.</span><span class="sxs-lookup"><span data-stu-id="c8b20-130">Now, suppose you want tooprocess a file called mySpecial.csv that's located in hello  /private directory of **container2** in **storage2**.</span></span>

<span data-ttu-id="c8b20-131">Wijs in uw code R Hallo naam knooppunt verwijzing toohello **storage2** storage-account.</span><span class="sxs-lookup"><span data-stu-id="c8b20-131">In your R code, point hello name node reference toohello **storage2** storage account.</span></span>


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

<span data-ttu-id="c8b20-132">Alle Hallo map- en verwijzingen nu punt toohello opslagaccount wasb://container2@storage2.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="c8b20-132">All of hello directory and file references now point toohello storage account wasb://container2@storage2.blob.core.windows.net.</span></span> <span data-ttu-id="c8b20-133">Dit is Hallo **naam knooppunt** die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="c8b20-133">This is hello **Name Node** that you’ve specified.</span></span>

<span data-ttu-id="c8b20-134">U hebt tooconfigure Hallo/User/RevoShare/<SSH username> directory op **storage2** als volgt:</span><span class="sxs-lookup"><span data-stu-id="c8b20-134">You have tooconfigure hello /user/RevoShare/<SSH username> directory on **storage2** as follows:</span></span>


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a><span data-ttu-id="c8b20-135">Gebruik een Azure Data Lake store met R Server</span><span class="sxs-lookup"><span data-stu-id="c8b20-135">Use an Azure Data Lake store with R Server</span></span>

<span data-ttu-id="c8b20-136">toouse Data Lake worden opgeslagen met uw HDInsight-account, moet u toogive na uw cluster toegang tooeach Azure Data Lake store die u toouse wilt.</span><span class="sxs-lookup"><span data-stu-id="c8b20-136">toouse Data Lake stores with your HDInsight account, you need toogive your cluster access tooeach Azure Data Lake store that you want toouse.</span></span> <span data-ttu-id="c8b20-137">Zie voor instructies over hoe toouse hello Azure portal toocreate een HDInsight-cluster met een Azure Data Lake Store-account als Hallo standaard opslag of als een extra store, [een HDInsight-cluster maken met Data Lake Store met Azure portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="c8b20-137">For instructions on how toouse hello Azure portal toocreate a HDInsight cluster with an Azure Data Lake Store account as hello default storage or as an additional store, see [Create an HDInsight cluster with Data Lake Store using Azure portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

<span data-ttu-id="c8b20-138">Vervolgens gebruikt u Hallo store in uw R-script veel net zoals een secundaire Azure storage-account zoals beschreven in de vorige procedure Hallo.</span><span class="sxs-lookup"><span data-stu-id="c8b20-138">You then use hello store in your R script much like you did a secondary Azure storage account as described in hello previous procedure.</span></span>

### <a name="add-cluster-access-tooyour-azure-data-lake-stores"></a><span data-ttu-id="c8b20-139">Cluster toegang tooyour die Azure Data Lake slaat toevoegen</span><span class="sxs-lookup"><span data-stu-id="c8b20-139">Add cluster access tooyour Azure Data Lake stores</span></span>
<span data-ttu-id="c8b20-140">U toegang tot een Data Lake store met behulp van een Service-Principal voor Azure Active Directory (Azure AD) dat is gekoppeld aan uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="c8b20-140">You access a Data Lake store by using an Azure Active Directory (Azure AD) Service Principal that's associated with your HDInsight cluster.</span></span>

<span data-ttu-id="c8b20-141">een Azure AD-Service-Principal tooadd:</span><span class="sxs-lookup"><span data-stu-id="c8b20-141">tooadd an Azure AD Service Principal:</span></span>

1. <span data-ttu-id="c8b20-142">Wanneer u uw HDInsight-cluster maakt, selecteert u **Cluster AAD-identiteit** van Hallo **gegevensbron** tabblad.</span><span class="sxs-lookup"><span data-stu-id="c8b20-142">When you create your HDInsight cluster, select **Cluster AAD Identity** from hello **Data Source** tab.</span></span>

2. <span data-ttu-id="c8b20-143">In Hallo **Cluster AAD-identiteit** dialoogvenster onder **AD Service-Principal selecteren**, selecteer **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="c8b20-143">In hello **Cluster AAD Identity** dialog box, under **Select AD Service Principal**, select **Create new**.</span></span>

<span data-ttu-id="c8b20-144">Nadat u Service-Principal Hallo Geef een naam en een wachtwoord voor het maken, klikt u op **ADLS-toegang beheren** tooassociate Hallo Service-Principal met uw Data Lake worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="c8b20-144">After you give hello Service Principal a name and create a password for it, click **Manage ADLS Access** tooassociate hello Service Principal with your Data Lake stores.</span></span>

<span data-ttu-id="c8b20-145">Het is ook mogelijk tooadd cluster toegang tooone of meer Data Lake worden opgeslagen na het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="c8b20-145">It’s also possible tooadd cluster access tooone or more Data Lake stores following cluster creation.</span></span> <span data-ttu-id="c8b20-146">Hello Azure portal-vermelding voor een Data Lake store te openen en te gaan**Data Explorer > toegang > toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="c8b20-146">Open hello Azure portal entry for a Data Lake store and go too**Data Explorer > Access > Add**.</span></span> 

### <a name="how-tooaccess-hello-data-lake-store-from-r-server"></a><span data-ttu-id="c8b20-147">Hoe tooaccess Hallo Data Lake store van R Server</span><span class="sxs-lookup"><span data-stu-id="c8b20-147">How tooaccess hello Data Lake store from R Server</span></span>

<span data-ttu-id="c8b20-148">Zodra u toegang tot tooa Data Lake store gegeven hebt, kunt u Hallo store in R Server op HDInsight Hallo manier als een secundaire Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="c8b20-148">Once you’ve given access tooa Data Lake store, you can use hello store in R Server on HDInsight hello way you would a secondary Azure storage account.</span></span> <span data-ttu-id="c8b20-149">Hallo enige verschil dat voorvoegsel Hallo is **wasb: / /** wijzigingen te**adl: / /** als volgt:</span><span class="sxs-lookup"><span data-stu-id="c8b20-149">hello only difference is that hello prefix **wasb://** changes too**adl://** as follows:</span></span>


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


<span data-ttu-id="c8b20-150">Hallo volgende opdrachten zijn gebruikte tooconfigure Hallo Data Lake storage-account met Hallo RevoShare directory en Hallo voorbeeld CSV-bestand van het vorige voorbeeld Hallo toevoegen:</span><span class="sxs-lookup"><span data-stu-id="c8b20-150">hello following commands are used tooconfigure hello Data Lake storage account with hello RevoShare directory and add hello sample .csv file from hello previous example:</span></span>


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a><span data-ttu-id="c8b20-151">Azure File storage gebruiken met R Server</span><span class="sxs-lookup"><span data-stu-id="c8b20-151">Use Azure File storage with R Server</span></span>

<span data-ttu-id="c8b20-152">Er is ook een handige gegevens voor de opslagoptie voor gebruik op Hallo edge-knooppunt genoemd Azure Files ((https://azure.microsoft.com/services/storage/files/).</span><span class="sxs-lookup"><span data-stu-id="c8b20-152">There is also a convenient data storage option for use on hello edge node called [Azure Files]((https://azure.microsoft.com/services/storage/files/).</span></span> <span data-ttu-id="c8b20-153">Hiermee kunt u toomount een Azure Storage-bestand delen toohello Linux-bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="c8b20-153">It enables you toomount an Azure Storage file share toohello Linux file system.</span></span> <span data-ttu-id="c8b20-154">Deze optie is handig voor het opslaan van gegevensbestanden, R-scripts en resultaatobjecten die mogelijk ook later nodig zijn, vooral wanneer het zin toouse Hallo systeemeigen bestandssysteem op Hallo edge-knooppunt in plaats van HDFS maakt.</span><span class="sxs-lookup"><span data-stu-id="c8b20-154">This option can be handy for storing data files, R scripts, and result objects that might be needed later, especially when it makes sense toouse hello native file system on hello edge node rather than HDFS.</span></span> 

<span data-ttu-id="c8b20-155">Een belangrijk voordeel van Azure Files is dat bestand Hallo shares kunnen worden gekoppeld en die wordt gebruikt door een systeem waarop een ondersteund besturingssysteem zoals Windows of Linux.</span><span class="sxs-lookup"><span data-stu-id="c8b20-155">A major benefit of Azure Files is that hello file shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> <span data-ttu-id="c8b20-156">Het kan bijvoorbeeld worden gebruikt door een andere HDInsight-cluster dat u of iemand in uw team heeft met een virtuele machine in Azure, of zelfs door een on-premises systeem.</span><span class="sxs-lookup"><span data-stu-id="c8b20-156">For example, it can be used by another HDInsight cluster that you or someone on your team has, by an Azure VM, or even by an on-premises system.</span></span> <span data-ttu-id="c8b20-157">Zie voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="c8b20-157">For more information, see:</span></span>

- [<span data-ttu-id="c8b20-158">Hoe toouse Azure File storage met Linux</span><span class="sxs-lookup"><span data-stu-id="c8b20-158">How toouse Azure File storage with Linux</span></span>](../storage/files/storage-how-to-use-files-linux.md)
- [<span data-ttu-id="c8b20-159">Hoe toouse Azure File storage in Windows</span><span class="sxs-lookup"><span data-stu-id="c8b20-159">How toouse Azure File storage on Windows</span></span>](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a><span data-ttu-id="c8b20-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c8b20-160">Next steps</span></span>

<span data-ttu-id="c8b20-161">Nu dat u hello Azure opslagopties begrijpt, koppelingen gebruik Hallo volgende toodiscover manieren om gegevens wetenschappelijke taken uitgevoerd met op HDInsight R Server.</span><span class="sxs-lookup"><span data-stu-id="c8b20-161">Now that you understand hello Azure storage options, use hello following links toodiscover ways of getting data science tasks done with R Server on HDInsight.</span></span>

* [<span data-ttu-id="c8b20-162">Overzicht van op HDInsight R Server</span><span class="sxs-lookup"><span data-stu-id="c8b20-162">Overview of R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-overview.md)
* [<span data-ttu-id="c8b20-163">Aan de slag met R server op Hadoop</span><span class="sxs-lookup"><span data-stu-id="c8b20-163">Get started with R server on Hadoop</span></span>](hdinsight-hadoop-r-server-get-started.md)
* [<span data-ttu-id="c8b20-164">RStudio Server tooHDInsight toevoegen (indien niet worden toegevoegd tijdens het maken van het cluster)</span><span class="sxs-lookup"><span data-stu-id="c8b20-164">Add RStudio Server tooHDInsight (if not added during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="c8b20-165">Opties voor compute-context voor R Server op HDInsight</span><span class="sxs-lookup"><span data-stu-id="c8b20-165">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)

