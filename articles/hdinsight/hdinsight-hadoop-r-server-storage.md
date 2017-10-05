---
title: Azure Storage-oplossingen voor R Server op een HDInsight - Azure | Microsoft Docs
description: Meer informatie over de verschillende opties voor opslag beschikbaar voor gebruikers met R Server op HDInsight
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
ms.openlocfilehash: aef9c15636ccaecce07d4fa218a40ed26ebad9df
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-solutions-for-r-server-on-hdinsight"></a><span data-ttu-id="eef53-103">Azure Storage-oplossingen voor op HDInsight R Server</span><span class="sxs-lookup"><span data-stu-id="eef53-103">Azure Storage solutions for R Server on HDInsight</span></span>

<span data-ttu-id="eef53-104">Microsoft R Server op HDInsight heeft een aantal opslagoplossingen voor het persistent maken van gegevens, code of objecten die bevatten de resultaten van de analyse.</span><span class="sxs-lookup"><span data-stu-id="eef53-104">Microsoft R Server on HDInsight has a variety of storage solutions to persist data, code, or objects that contain results from analysis.</span></span> <span data-ttu-id="eef53-105">Deze omvatten de volgende opties:</span><span class="sxs-lookup"><span data-stu-id="eef53-105">These include the following options:</span></span>

- [<span data-ttu-id="eef53-106">Azure-blobopslag</span><span class="sxs-lookup"><span data-stu-id="eef53-106">Azure Blob</span></span>](https://azure.microsoft.com/services/storage/blobs/)
- [<span data-ttu-id="eef53-107">Azure Data Lake Storage</span><span class="sxs-lookup"><span data-stu-id="eef53-107">Azure Data Lake Storage</span></span>](https://azure.microsoft.com/services/data-lake-store/)
- [<span data-ttu-id="eef53-108">Azure File storage</span><span class="sxs-lookup"><span data-stu-id="eef53-108">Azure File storage</span></span>](https://azure.microsoft.com/services/storage/files/)

<span data-ttu-id="eef53-109">U hebt ook de optie van de toegang tot meerdere Azure storage-accounts of containers met uw HDI-cluster.</span><span class="sxs-lookup"><span data-stu-id="eef53-109">You also have the option of accessing multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="eef53-110">Azure File storage is een handige gegevens voor de opslagoptie voor gebruik op de edge-knooppunt dat kunt u het koppelen van een Azure Storage-bestandsshare, bijvoorbeeld het Linux-bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="eef53-110">Azure File storage is a convenient data storage option for use on the edge node that enables you to mount an Azure Storage file share to, for example, the Linux file system.</span></span> <span data-ttu-id="eef53-111">Maar Azure-bestandsshares kunnen worden gekoppeld en die wordt gebruikt door een systeem waarop een ondersteund besturingssysteem zoals Windows of Linux.</span><span class="sxs-lookup"><span data-stu-id="eef53-111">But Azure File shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> 

<span data-ttu-id="eef53-112">Wanneer u een Hadoop-cluster in HDInsight maakt, geeft u ofwel een **Azure storage** account of een **Data Lake store**.</span><span class="sxs-lookup"><span data-stu-id="eef53-112">When you create an Hadoop cluster in HDInsight, you specify either an **Azure storage** account or a **Data Lake store**.</span></span> <span data-ttu-id="eef53-113">Een specifieke storage-container uit dat account bevat het bestandssysteem voor het cluster dat u (bijvoorbeeld Hadoop Distributed File System maakt).</span><span class="sxs-lookup"><span data-stu-id="eef53-113">A specific storage container from that account holds the file system for the cluster that you create (for example, the Hadoop Distributed File System).</span></span> <span data-ttu-id="eef53-114">Zie voor meer informatie en richtlijnen:</span><span class="sxs-lookup"><span data-stu-id="eef53-114">For more information and guidance, see:</span></span>

- [<span data-ttu-id="eef53-115">Azure storage gebruiken met HDInsight</span><span class="sxs-lookup"><span data-stu-id="eef53-115">Use Azure storage with HDInsight</span></span>](hdinsight-hadoop-use-blob-storage.md)
- <span data-ttu-id="eef53-116">[Gebruik Data Lake Store met Azure HDInsight-clusters](hdinsight-hadoop-use-data-lake-store.md).</span><span class="sxs-lookup"><span data-stu-id="eef53-116">[Use Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> 

<span data-ttu-id="eef53-117">Zie voor meer informatie over de Azure storage-oplossingen [Inleiding tot Microsoft Azure Storage](../storage/common/storage-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="eef53-117">For more information on the Azure storage solutions, see [Introduction to Microsoft Azure Storage](../storage/common/storage-introduction.md).</span></span> 

<span data-ttu-id="eef53-118">Zie voor instructies over het selecteren van de meest geschikte opslagoptie gebruiken voor uw scenario [beslissen wanneer u Azure Blobs, Azure-bestanden of Azure gegevensschijven gebruiken](../storage/common/storage-decide-blobs-files-disks.md)</span><span class="sxs-lookup"><span data-stu-id="eef53-118">For guidance on selecting the most appropriate storage option to use for your scenario, see [Deciding when to use Azure Blobs, Azure Files, or Azure Data Disks](../storage/common/storage-decide-blobs-files-disks.md)</span></span> 


## <a name="use-azure-blob-storage-accounts-with-r-server"></a><span data-ttu-id="eef53-119">Azure Blob storage-accounts gebruiken met R Server</span><span class="sxs-lookup"><span data-stu-id="eef53-119">Use Azure Blob storage accounts with R Server</span></span>

<span data-ttu-id="eef53-120">Indien nodig, kunt u meerdere Azure storage-accounts of containers openen met uw HDI-cluster.</span><span class="sxs-lookup"><span data-stu-id="eef53-120">If necessary, you can access multiple Azure storage accounts or containers with your HDI cluster.</span></span> <span data-ttu-id="eef53-121">Om dit te doen, moet u de extra opslagaccounts in de gebruikersinterface opgeven wanneer u het cluster maakt en vervolgens als volgt te werk als u wilt gebruiken met R Server.</span><span class="sxs-lookup"><span data-stu-id="eef53-121">To do so, you need to specify the additional storage accounts in the UI when you create the cluster, and then follow these steps to use them with R Server.</span></span>

> [!WARNING]
> <span data-ttu-id="eef53-122">Voor de doeleinden van prestaties, wordt het HDInsight-cluster gemaakt in hetzelfde Datacenter als het primaire opslagaccount die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="eef53-122">For performance purposes, the HDInsight cluster is created in the same data center as the primary storage account that you specify.</span></span> <span data-ttu-id="eef53-123">Met behulp van een opslagaccount in een andere locatie dan het HDInsight-cluster wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="eef53-123">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span>

1. <span data-ttu-id="eef53-124">Een HDInsight-cluster maken met de naam van een opslagaccount van **storage1** en standaardcontainer aangeroepen **container1**.</span><span class="sxs-lookup"><span data-stu-id="eef53-124">Create an HDInsight cluster with a storage account name of **storage1** and a default container called **container1**.</span></span>
2. <span data-ttu-id="eef53-125">Geef een account op extra opslagruimte aangeroepen **storage2**.</span><span class="sxs-lookup"><span data-stu-id="eef53-125">Specify an additional storage account called **storage2**.</span></span>  
3. <span data-ttu-id="eef53-126">Kopieer het bestand mycsv.csv naar de map/share en analyse van de op dat bestand.</span><span class="sxs-lookup"><span data-stu-id="eef53-126">Copy the mycsv.csv file to the /share directory, and perform analysis on that file.</span></span>  

        hadoop fs –mkdir /share
        hadoop fs –copyFromLocal myscsv.scv /share  

4. <span data-ttu-id="eef53-127">In de R-code, stelt u de naam van knooppunt op **standaard** en stel uw directory en het bestand om te verwerken.</span><span class="sxs-lookup"><span data-stu-id="eef53-127">In R code, set the name node to **default,** and set your directory and file to process.</span></span>  

        myNameNode <- "default"
        myPort <- 0

        #Location of the data:  
        bigDataDirRoot <- "/share"  

        #Define Spark compute context:
        mySparkCluster <- RxSpark(consoleOutput=TRUE)

        #Set compute context:
        rxSetComputeContext(mySparkCluster)

        #Define the Hadoop Distributed File System (HDFS) file system:
        hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

        #Specify the input file to analyze in HDFS:
        inputFile <-file.path(bigDataDirRoot,"mycsv.csv")

<span data-ttu-id="eef53-128">Alle mappen en bestanden verwijzingen verwijzen naar het opslagaccount wasb://container1@storage1.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="eef53-128">All the directory and file references point to the storage account wasb://container1@storage1.blob.core.windows.net.</span></span> <span data-ttu-id="eef53-129">Dit is de **standaard opslagaccount** die is gekoppeld aan het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="eef53-129">This is the **default storage account** that's associated with the HDInsight cluster.</span></span>

<span data-ttu-id="eef53-130">Stel nu dat u wilt laten verwerken van een bestand met de naam mySpecial.csv die zich in de /private map van **container2** in **storage2**.</span><span class="sxs-lookup"><span data-stu-id="eef53-130">Now, suppose you want to process a file called mySpecial.csv that's located in the  /private directory of **container2** in **storage2**.</span></span>

<span data-ttu-id="eef53-131">In uw code R, wijst u de naam van knooppunt verwijzing naar de **storage2** storage-account.</span><span class="sxs-lookup"><span data-stu-id="eef53-131">In your R code, point the name node reference to the **storage2** storage account.</span></span>


    myNameNode <- "wasb://container2@storage2.blob.core.windows.net"
    myPort <- 0

    #Location of the data:
    bigDataDirRoot <- "/private"

    #Define Spark compute context:
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    #Set compute context:
    rxSetComputeContext(mySparkCluster)

    #Define HDFS file system:
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    #Specify the input file to analyze in HDFS:
    inputFile <-file.path(bigDataDirRoot,"mySpecial.csv")

<span data-ttu-id="eef53-132">Alle verwijzingen van de map- en wijs nu het opslagaccount wasb://container2@storage2.blob.core.windows.net.</span><span class="sxs-lookup"><span data-stu-id="eef53-132">All of the directory and file references now point to the storage account wasb://container2@storage2.blob.core.windows.net.</span></span> <span data-ttu-id="eef53-133">Dit is de **naam knooppunt** die u hebt opgegeven.</span><span class="sxs-lookup"><span data-stu-id="eef53-133">This is the **Name Node** that you’ve specified.</span></span>

<span data-ttu-id="eef53-134">U hoeft te configureren/User/RevoShare/<SSH username> directory op **storage2** als volgt:</span><span class="sxs-lookup"><span data-stu-id="eef53-134">You have to configure the /user/RevoShare/<SSH username> directory on **storage2** as follows:</span></span>


    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare
    hadoop fs -mkdir wasb://container2@storage2.blob.core.windows.net/user/RevoShare/<RDP username>



## <a name="use-an-azure-data-lake-store-with-r-server"></a><span data-ttu-id="eef53-135">Gebruik een Azure Data Lake store met R Server</span><span class="sxs-lookup"><span data-stu-id="eef53-135">Use an Azure Data Lake store with R Server</span></span>

<span data-ttu-id="eef53-136">Voor het gebruik van Data Lake winkels met uw HDInsight-account, moet u uw cluster toegang geven tot elke Azure Data Lake store die u wilt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="eef53-136">To use Data Lake stores with your HDInsight account, you need to give your cluster access to each Azure Data Lake store that you want to use.</span></span> <span data-ttu-id="eef53-137">Zie voor instructies over het gebruik van de Azure-portal voor het maken van een HDInsight-cluster met een Azure Data Lake Store-account als de standaard-opslag of als een extra store [een HDInsight-cluster maken met Data Lake Store met Azure-portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="eef53-137">For instructions on how to use the Azure portal to create a HDInsight cluster with an Azure Data Lake Store account as the default storage or as an additional store, see [Create an HDInsight cluster with Data Lake Store using Azure portal](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).</span></span>

<span data-ttu-id="eef53-138">U gebruikt het archief in uw R-script veel net zoals een secundaire Azure storage-account zoals beschreven in de vorige procedure.</span><span class="sxs-lookup"><span data-stu-id="eef53-138">You then use the store in your R script much like you did a secondary Azure storage account as described in the previous procedure.</span></span>

### <a name="add-cluster-access-to-your-azure-data-lake-stores"></a><span data-ttu-id="eef53-139">Toegang tot cluster toevoegen aan uw Azure Data Lake-winkels</span><span class="sxs-lookup"><span data-stu-id="eef53-139">Add cluster access to your Azure Data Lake stores</span></span>
<span data-ttu-id="eef53-140">U toegang tot een Data Lake store met behulp van een Service-Principal voor Azure Active Directory (Azure AD) dat is gekoppeld aan uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="eef53-140">You access a Data Lake store by using an Azure Active Directory (Azure AD) Service Principal that's associated with your HDInsight cluster.</span></span>

<span data-ttu-id="eef53-141">Toevoegen van een Azure AD-Service-Principal:</span><span class="sxs-lookup"><span data-stu-id="eef53-141">To add an Azure AD Service Principal:</span></span>

1. <span data-ttu-id="eef53-142">Wanneer u uw HDInsight-cluster maakt, selecteert u **Cluster AAD-identiteit** van de **gegevensbron** tabblad.</span><span class="sxs-lookup"><span data-stu-id="eef53-142">When you create your HDInsight cluster, select **Cluster AAD Identity** from the **Data Source** tab.</span></span>

2. <span data-ttu-id="eef53-143">In de **Cluster AAD-identiteit** dialoogvenster onder **AD Service-Principal selecteren**, selecteer **nieuw**.</span><span class="sxs-lookup"><span data-stu-id="eef53-143">In the **Cluster AAD Identity** dialog box, under **Select AD Service Principal**, select **Create new**.</span></span>

<span data-ttu-id="eef53-144">Nadat u de Service-Principal een naam geven en een wachtwoord voor het maken, klikt u op **ADLS-toegang beheren** de Service-Principal koppelen aan uw Data Lake-stores.</span><span class="sxs-lookup"><span data-stu-id="eef53-144">After you give the Service Principal a name and create a password for it, click **Manage ADLS Access** to associate the Service Principal with your Data Lake stores.</span></span>

<span data-ttu-id="eef53-145">Het is ook mogelijk toegang tot cluster toevoegen aan een of meer Data Lake winkels na het maken van de cluster.</span><span class="sxs-lookup"><span data-stu-id="eef53-145">It’s also possible to add cluster access to one or more Data Lake stores following cluster creation.</span></span> <span data-ttu-id="eef53-146">Open de Azure portal-vermelding voor een Data Lake store en Ga naar **Data Explorer > toegang > toevoegen**.</span><span class="sxs-lookup"><span data-stu-id="eef53-146">Open the Azure portal entry for a Data Lake store and go to **Data Explorer > Access > Add**.</span></span> 

### <a name="how-to-access-the-data-lake-store-from-r-server"></a><span data-ttu-id="eef53-147">Toegang tot de Data Lake store van R Server</span><span class="sxs-lookup"><span data-stu-id="eef53-147">How to access the Data Lake store from R Server</span></span>

<span data-ttu-id="eef53-148">Zodra u toegang tot een Data Lake store krijgen hebt, kunt u het archief in R Server op HDInsight de manier waarop u zou een secundair Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="eef53-148">Once you’ve given access to a Data Lake store, you can use the store in R Server on HDInsight the way you would a secondary Azure storage account.</span></span> <span data-ttu-id="eef53-149">Het enige verschil is dat het voorvoegsel **wasb: / /** wijzigingen in **adl: / /** als volgt:</span><span class="sxs-lookup"><span data-stu-id="eef53-149">The only difference is that the prefix **wasb://** changes to **adl://** as follows:</span></span>


    # Point to the ADL store (e.g. ADLtest)
    myNameNode <- "adl://rkadl1.azuredatalakestore.net"
    myPort <- 0

    # Location of the data (assumes a /share directory on the ADL account)
    bigDataDirRoot <- "/share"  

    # Define Spark compute context
    mySparkCluster <- RxSpark(consoleOutput=TRUE, nameNode=myNameNode, port=myPort)

    # Set compute context
    rxSetComputeContext(mySparkCluster)

    # Define HDFS file system
    hdfsFS <- RxHdfsFileSystem(hostName=myNameNode, port=myPort)

    # Specify the input file in HDFS to analyze
    inputFile <-file.path(bigDataDirRoot,"AirlineDemoSmall.csv")

    # Create factors for days of the week
    colInfo <- list(DayOfWeek = list(type = "factor",
               levels = c("Monday", "Tuesday", "Wednesday", "Thursday",
                          "Friday", "Saturday", "Sunday")))

    # Define the data source
    airDS <- RxTextData(file = inputFile, missingValueString = "M",
                    colInfo  = colInfo, fileSystem = hdfsFS)

    # Run a linear regression
    model <- rxLinMod(ArrDelay~CRSDepTime+DayOfWeek, data = airDS)


<span data-ttu-id="eef53-150">De volgende opdrachten worden gebruikt voor het configureren van het Data Lake storage-account met de map RevoShare en het CSV-voorbeeldbestand uit het vorige voorbeeld toevoegen:</span><span class="sxs-lookup"><span data-stu-id="eef53-150">The following commands are used to configure the Data Lake storage account with the RevoShare directory and add the sample .csv file from the previous example:</span></span>


    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare
    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/user/RevoShare/<user>

    hadoop fs -mkdir adl://rkadl1.azuredatalakestore.net/share

    hadoop fs -copyFromLocal /usr/lib64/R Server-7.4.1/library/RevoScaleR/SampleData/AirlineDemoSmall.csv adl://rkadl1.azuredatalakestore.net/share

    hadoop fs –ls adl://rkadl1.azuredatalakestore.net/share


## <a name="use-azure-file-storage-with-r-server"></a><span data-ttu-id="eef53-151">Azure File storage gebruiken met R Server</span><span class="sxs-lookup"><span data-stu-id="eef53-151">Use Azure File storage with R Server</span></span>

<span data-ttu-id="eef53-152">Er is ook een handige gegevens voor de opslagoptie voor gebruik op de edge-knooppunt genoemd Azure Files ((https://azure.microsoft.com/services/storage/files/).</span><span class="sxs-lookup"><span data-stu-id="eef53-152">There is also a convenient data storage option for use on the edge node called [Azure Files]((https://azure.microsoft.com/services/storage/files/).</span></span> <span data-ttu-id="eef53-153">Hiermee kunt u een Azure Storage-bestandsshare naar het bestandssysteem van Linux te koppelen.</span><span class="sxs-lookup"><span data-stu-id="eef53-153">It enables you to mount an Azure Storage file share to the Linux file system.</span></span> <span data-ttu-id="eef53-154">Deze optie is handig voor het opslaan van gegevensbestanden, R-scripts en resultaatobjecten die mogelijk ook later nodig zijn, vooral wanneer het zinvol zijn het systeemeigen bestandssysteem gebruiken op de edge-knooppunt in plaats van HDFS.</span><span class="sxs-lookup"><span data-stu-id="eef53-154">This option can be handy for storing data files, R scripts, and result objects that might be needed later, especially when it makes sense to use the native file system on the edge node rather than HDFS.</span></span> 

<span data-ttu-id="eef53-155">Een belangrijk voordeel van Azure Files is dat de bestandsshares kunnen worden gekoppeld en die wordt gebruikt door een systeem waarop een ondersteund besturingssysteem zoals Windows of Linux.</span><span class="sxs-lookup"><span data-stu-id="eef53-155">A major benefit of Azure Files is that the file shares can be mounted and used by any system that has a supported OS such as Windows or Linux.</span></span> <span data-ttu-id="eef53-156">Het kan bijvoorbeeld worden gebruikt door een andere HDInsight-cluster dat u of iemand in uw team heeft met een virtuele machine in Azure, of zelfs door een on-premises systeem.</span><span class="sxs-lookup"><span data-stu-id="eef53-156">For example, it can be used by another HDInsight cluster that you or someone on your team has, by an Azure VM, or even by an on-premises system.</span></span> <span data-ttu-id="eef53-157">Zie voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="eef53-157">For more information, see:</span></span>

- [<span data-ttu-id="eef53-158">Azure File Storage gebruiken met Linux</span><span class="sxs-lookup"><span data-stu-id="eef53-158">How to use Azure File storage with Linux</span></span>](../storage/files/storage-how-to-use-files-linux.md)
- [<span data-ttu-id="eef53-159">Azure File storage gebruiken in Windows</span><span class="sxs-lookup"><span data-stu-id="eef53-159">How to use Azure File storage on Windows</span></span>](../storage/files/storage-dotnet-how-to-use-files.md)


## <a name="next-steps"></a><span data-ttu-id="eef53-160">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="eef53-160">Next steps</span></span>

<span data-ttu-id="eef53-161">Nu u inzicht in de Azure-opslag-opties, gebruiken de volgende koppelingen voor het detecteren van de manieren om gegevens wetenschappelijke taken uitgevoerd met op HDInsight R Server.</span><span class="sxs-lookup"><span data-stu-id="eef53-161">Now that you understand the Azure storage options, use the following links to discover ways of getting data science tasks done with R Server on HDInsight.</span></span>

* [<span data-ttu-id="eef53-162">Overzicht van op HDInsight R Server</span><span class="sxs-lookup"><span data-stu-id="eef53-162">Overview of R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-overview.md)
* [<span data-ttu-id="eef53-163">Aan de slag met R server op Hadoop</span><span class="sxs-lookup"><span data-stu-id="eef53-163">Get started with R server on Hadoop</span></span>](hdinsight-hadoop-r-server-get-started.md)
* [<span data-ttu-id="eef53-164">RStudio Server toevoegen aan HDInsight (indien niet toegevoegd tijdens het maken van het cluster)</span><span class="sxs-lookup"><span data-stu-id="eef53-164">Add RStudio Server to HDInsight (if not added during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="eef53-165">Opties voor compute-context voor R Server op HDInsight</span><span class="sxs-lookup"><span data-stu-id="eef53-165">Compute context options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-compute-contexts.md)

