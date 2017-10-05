---
title: Gegevens opvragen uit HDFS-compatibele Azure-opslag - Azure HDInsight | Microsoft Docs
description: Informatie over hoe u gegevens opvraagt uit Azure Storage en Azure Data Lake Store om resultaten van uw analyse op te slaan.
keywords: blob storage, hdfs, gestructureerde gegevens, ongestructureerde gegevens, data lake store, Hadoop-invoer, Hadoop-uitvoer, hadoop-opslag, hdfs-invoer, hdfs-uitvoer, hdfs-opslag, wasb azure
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1d2e65f2-16de-449e-915f-3ffbc230f815
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/09/2017
ms.author: jgao
ms.openlocfilehash: a44c2b363f7ebb593b9a9c5bd9e0d4fc3b4c31bb
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="use-azure-storage-with-azure-hdinsight-clusters"></a><span data-ttu-id="dc8c7-104">Azure-opslag gebruiken met Azure HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="dc8c7-104">Use Azure storage with Azure HDInsight clusters</span></span>

<span data-ttu-id="dc8c7-105">Als u gegevens wilt analyseren in een HDInsight-cluster, kunt u de gegevens opslaan in Azure Storage, Azure Data Lake Store of beide.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-105">To analyze data in HDInsight cluster, you can store the data either in Azure Storage, Azure Data Lake Store, or both.</span></span> <span data-ttu-id="dc8c7-106">Met beide opslagopties kunt u de HDInsight-clusters die worden gebruikt voor berekeningen, veilig verwijderen zonder dat er gebruikersgegevens verloren gaan.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-106">Both storage options enable you to safely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="dc8c7-107">Hadoop ondersteunt een notatie van het standaardbestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-107">Hadoop supports a notion of the default file system.</span></span> <span data-ttu-id="dc8c7-108">Het standaardbestandssysteem impliceert een standaardschema en instantie.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-108">The default file system implies a default scheme and authority.</span></span> <span data-ttu-id="dc8c7-109">De toepassing kan ook worden gebruikt om relatieve paden om te zetten.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-109">It can also be used to resolve relative paths.</span></span> <span data-ttu-id="dc8c7-110">Wanneer u een HDInsight-cluster maakt, kunt u in Azure Storage een blobcontainer opgeven als het standaardbestandssysteem. Met HDInsight 3.5 kunt u ook Azure Storage of Azure Data Lake Store als het standaardbestandssysteem selecteren, met een paar uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-110">During the HDInsight cluster creation process, you can specify a blob container in Azure Storage as the default file system, or with HDInsight 3.5, you can select either Azure Storage or Azure Data Lake Store as the default files system with a few exceptions.</span></span> <span data-ttu-id="dc8c7-111">Zie [Beschikbaarheid voor HDInsight-cluster](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters) voor de ondersteuning van het gebruik van Data Lake Store als de standaard- en de gekoppelde opslag.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-111">For the supportability of using Data Lake Store as both the default and linked storage, see [Availabilities for HDInsight cluster](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).</span></span>

<span data-ttu-id="dc8c7-112">In dit artikel wordt uitgelegd hoe Azure Storage werkt met HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-112">In this article, you learn how Azure Storage works with HDInsight clusters.</span></span> <span data-ttu-id="dc8c7-113">Zie [Azure Data Lake Store gebruiken met Azure HDInsight-clusters](hdinsight-hadoop-use-data-lake-store.md) voor meer informatie over de werking van Data Lake Store met HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-113">To learn how Data Lake Store works with HDInsight clusters, see [Use Azure Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> <span data-ttu-id="dc8c7-114">Zie [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) (Hadoop-clusters maken in HDInsight) voor meer informatie over het maken van HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-114">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="dc8c7-115">Azure Storage is een robuuste, algemene opslagoplossing die naadloos kan worden geïntegreerd met HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-115">Azure storage is a robust, general-purpose storage solution that integrates seamlessly with HDInsight.</span></span> <span data-ttu-id="dc8c7-116">HDInsight kan een blobcontainer in Azure Storage gebruiken als het standaardbestandssysteem voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-116">HDInsight can use a blob container in Azure Storage as the default file system for the cluster.</span></span> <span data-ttu-id="dc8c7-117">Via een HDFS-interface (Hadoop Distributed File System) kan de volledige set onderdelen in HDInsight rechtstreeks als blobs op gestructureerde of ongestructureerde gegevens worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-117">Through a Hadoop distributed file system (HDFS) interface, the full set of components in HDInsight can operate directly on structured or unstructured data stored as blobs.</span></span>

> [!WARNING]
> <span data-ttu-id="dc8c7-118">Er zijn verschillende opties beschikbaar bij het maken van een Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-118">There are several options available when creating an Azure Storage account.</span></span> <span data-ttu-id="dc8c7-119">De volgende tabel bevat informatie over de opties die met HDInsight worden ondersteund:</span><span class="sxs-lookup"><span data-stu-id="dc8c7-119">The following table provides information on what options are supported with HDInsight:</span></span>
> 
> | <span data-ttu-id="dc8c7-120">Type opslagaccount</span><span class="sxs-lookup"><span data-stu-id="dc8c7-120">Storage account type</span></span> | <span data-ttu-id="dc8c7-121">Opslaglaag</span><span class="sxs-lookup"><span data-stu-id="dc8c7-121">Storage tier</span></span> | <span data-ttu-id="dc8c7-122">Ondersteund met HDInsight</span><span class="sxs-lookup"><span data-stu-id="dc8c7-122">Supported with HDInsight</span></span> |
> | ------- | ------- | ------- |
> | <span data-ttu-id="dc8c7-123">Storage-account voor algemeen gebruik</span><span class="sxs-lookup"><span data-stu-id="dc8c7-123">General-purpose Storage Account</span></span> | <span data-ttu-id="dc8c7-124">Standard</span><span class="sxs-lookup"><span data-stu-id="dc8c7-124">Standard</span></span> | <span data-ttu-id="dc8c7-125">__Ja__</span><span class="sxs-lookup"><span data-stu-id="dc8c7-125">__Yes__</span></span> |
> | &nbsp; | <span data-ttu-id="dc8c7-126">Premium</span><span class="sxs-lookup"><span data-stu-id="dc8c7-126">Premium</span></span> | <span data-ttu-id="dc8c7-127">Nee</span><span class="sxs-lookup"><span data-stu-id="dc8c7-127">No</span></span> |
> | <span data-ttu-id="dc8c7-128">Blob Storage-account</span><span class="sxs-lookup"><span data-stu-id="dc8c7-128">Blob Storage Account</span></span> | <span data-ttu-id="dc8c7-129">Warm</span><span class="sxs-lookup"><span data-stu-id="dc8c7-129">Hot</span></span> | <span data-ttu-id="dc8c7-130">Nee</span><span class="sxs-lookup"><span data-stu-id="dc8c7-130">No</span></span> |
> | &nbsp; | <span data-ttu-id="dc8c7-131">Koud</span><span class="sxs-lookup"><span data-stu-id="dc8c7-131">Cool</span></span> | <span data-ttu-id="dc8c7-132">Nee</span><span class="sxs-lookup"><span data-stu-id="dc8c7-132">No</span></span> |

<span data-ttu-id="dc8c7-133">Het wordt afgeraden om de standaard- blobcontainer te gebruiken voor het opslaan van bedrijfsgegevens.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-133">We do not recommend that you use the default blob container for storing business data.</span></span> <span data-ttu-id="dc8c7-134">Het is een goede gewoonte om de standaard-blobcontainer na ieder gebruik te verwijderen om de opslagkosten te verlagen.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-134">Deleting the default blob container after each use to reduce storage cost is a good practice.</span></span> <span data-ttu-id="dc8c7-135">De standaardcontainer bevat toepassings- en systeemlogboeken.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-135">Note that the default container contains application and system logs.</span></span> <span data-ttu-id="dc8c7-136">Breng de logboeken over naar een andere locatie voordat u de container verwijdert.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-136">Make sure to retrieve the logs before deleting the container.</span></span>

<span data-ttu-id="dc8c7-137">Het delen van een blobcontainer voor meerdere clusters wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-137">Sharing one blob container for multiple clusters is not supported.</span></span>

## <a name="hdinsight-storage-architecture"></a><span data-ttu-id="dc8c7-138">HDInsight-opslagarchitectuur</span><span class="sxs-lookup"><span data-stu-id="dc8c7-138">HDInsight storage architecture</span></span>
<span data-ttu-id="dc8c7-139">Het volgende diagram biedt een abstracte weergave van de HDInsight-opslagarchitectuur bij gebruik van Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="dc8c7-139">The following diagram provides an abstract view of the HDInsight storage architecture of using Azure Storage:</span></span>

<span data-ttu-id="dc8c7-140">![Hadoop-clusters gebruiken de HDFS-API voor toegang tot en opslag van gestructureerde en ongestructureerde gegevens in Blob Storage.](./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "HDInsight Storage-architectuur")</span><span class="sxs-lookup"><span data-stu-id="dc8c7-140">![Hadoop clusters use the HDFS API to access and store structured and unstructured data in Blob storage.](./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "HDInsight Storage Architecture")</span></span>

<span data-ttu-id="dc8c7-141">HDInsight biedt toegang tot het Distributed File System dat lokaal wordt gekoppeld aan de rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-141">HDInsight provides access to the distributed file system that is locally attached to the compute nodes.</span></span> <span data-ttu-id="dc8c7-142">Dit bestandssysteem is toegankelijk via de volledig gekwalificeerde URI, bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="dc8c7-142">This file system can be accessed by using the fully qualified URI, for example:</span></span>

    hdfs://<namenodehost>/<path>

<span data-ttu-id="dc8c7-143">Daarnaast biedt HDInsight toegang tot gegevens die zijn opgeslagen in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-143">In addition, HDInsight allows you to access data that is stored in Azure Storage.</span></span> <span data-ttu-id="dc8c7-144">De syntaxis is:</span><span class="sxs-lookup"><span data-stu-id="dc8c7-144">The syntax is:</span></span>

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

<span data-ttu-id="dc8c7-145">Hier volgen enkele overwegingen bij het gebruik van een Azure Storage-account met HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-145">Here are some considerations when using Azure Storage account with HDInsight clusters.</span></span>

* <span data-ttu-id="dc8c7-146">**Containers in de opslagaccounts die zijn verbonden met een cluster:** omdat de accountnaam en de sleutel tijdens het maken worden gekoppeld aan het cluster, hebt u volledige toegang tot de blobs in deze containers.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-146">**Containers in the storage accounts that are connected to a cluster:** Because the account name and key are associated with the cluster during creation, you have full access to the blobs in those containers.</span></span>

* <span data-ttu-id="dc8c7-147">**Openbare containers of openbare blobs in opslagaccounts die NIET zijn verbonden met een cluster:** u hebt een alleen-lezen-machtiging voor de blobs in de containers.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-147">**Public containers or public blobs in storage accounts that are NOT connected to a cluster:** You have read-only permission to the blobs in the containers.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="dc8c7-148">Met openbare containers kunt u een lijst met alle beschikbare blobs in de desbetreffende container en containermetagegevens ophalen.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-148">Public containers allow you to get a list of all blobs that are available in that container and get container metadata.</span></span> <span data-ttu-id="dc8c7-149">Openbare blobs zijn alleen toegankelijk als u de exacte URL weet.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-149">Public blobs allow you to access the blobs only if you know the exact URL.</span></span> <span data-ttu-id="dc8c7-150">Zie <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">Restrict access to containers and blobs</a> (De toegang tot containers en blobs beperken) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-150">For more information, see <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">Restrict access to containers and blobs</a>.</span></span>
  > 
  > 
* <span data-ttu-id="dc8c7-151">**Persoonlijke containers in opslagaccounts die NIET zijn verbonden met een cluster:** u hebt geen toegang tot de blobs in de containers, tenzij u het opslagaccount definieert wanneer u de WebHCat-taken verzendt.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-151">**Private containers in storage accounts that are NOT connected to a cluster:** You can't access the blobs in the containers unless you define the storage account when you submit the WebHCat jobs.</span></span> <span data-ttu-id="dc8c7-152">Dit wordt verderop in dit artikel uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-152">This is explained later in this article.</span></span>

<span data-ttu-id="dc8c7-153">De opslagaccounts die worden gedefinieerd tijdens het creatieproces en de bijbehorende sleutels worden opgeslagen in %HADOOP_HOME%/conf/core-site.xml op de clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-153">The storage accounts that are defined in the creation process and their keys are stored in %HADOOP_HOME%/conf/core-site.xml on the cluster nodes.</span></span> <span data-ttu-id="dc8c7-154">HDInsight gebruikt standaard de opslagaccounts die zijn gedefinieerd in het bestand core-site.xml.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-154">The default behavior of HDInsight is to use the storage accounts defined in the core-site.xml file.</span></span> <span data-ttu-id="dc8c7-155">U kunt deze instelling wijzigen instellen met [Ambari](./hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="dc8c7-155">You can modify this setting using [Ambari](./hdinsight-hadoop-manage-ambari.md)</span></span>

<span data-ttu-id="dc8c7-156">Meerdere WebHCat-taken, waaronder Hive, MapReduce, Hadoop-streaming en Pig, kunnen een beschrijving van opslagaccounts en metagegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-156">Multiple WebHCat jobs, including Hive, MapReduce, Hadoop streaming, and Pig, can carry a description of storage accounts and metadata with them.</span></span> <span data-ttu-id="dc8c7-157">(Dit werkt momenteel voor Pig met opslagaccounts, maar niet voor metagegevens.) Zie [Using an HDInsight Cluster with Alternate Storage Accounts and Metastores](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx) (Een HDInsight-cluster gebruiken met alternatieve opslagaccounts en metastores) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-157">(This currently works for Pig with storage accounts, but not for metadata.) For more information, see [Using an HDInsight Cluster with Alternate Storage Accounts and Metastores](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).</span></span>

<span data-ttu-id="dc8c7-158">Blobs kunnen worden gebruikt voor gestructureerde en ongestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-158">Blobs can be used for structured and unstructured data.</span></span> <span data-ttu-id="dc8c7-159">De gegevens in blobcontainers worden opgeslagen als sleutel-waardeparen en er is geen maphiërarchie.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-159">Blob containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="dc8c7-160">Maar het slash-teken (/) kan echter worden gebruikt binnen de sleutelnaam deze weergegeven, zodat het lijkt alsof een bestand is opgeslagen in een mapstructuur.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-160">However the slash character ( / ) can be used within the key name to make it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="dc8c7-161">De sleutel van de blob kan bijvoorbeeld *input/log1.txt* zijn.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-161">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="dc8c7-162">Er is niet echt een *invoermap* aanwezig, maar als gevolg van de aanwezigheid van het slash-teken in de naam van de sleutel ziet dit eruit als een bestandspad.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-162">No actual *input* directory exists, but due to the presence of the slash character in the key name, it has the appearance of a file path.</span></span>

## <span data-ttu-id="dc8c7-163"><a id="benefits"></a>Voordelen van Azure Storage</span><span class="sxs-lookup"><span data-stu-id="dc8c7-163"><a id="benefits"></a>Benefits of Azure Storage</span></span>
<span data-ttu-id="dc8c7-164">De kosten als gevolg van de verschillende locaties voor de rekenclusters en opslagresources worden beperkt door de manier waarop de rekenclusters dicht bij de resources van het opslagaccount in de Azure-regio worden geplaatst. Dankzij het netwerk met hoge snelheid kunnen de rekenknooppunten zich op efficiënte wijze toegang verschaffen tot de gegevens in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-164">The implied performance cost of not co-locating compute clusters and storage resources is mitigated by the way the compute clusters are created close to the storage account resources inside the Azure region, where the high-speed network makes it efficient for the compute nodes to access the data inside Azure storage.</span></span>

<span data-ttu-id="dc8c7-165">Het opslaan van gegevens in Azure Storage in plaats van HDFS heeft enkele voordelen:</span><span class="sxs-lookup"><span data-stu-id="dc8c7-165">There are several benefits associated with storing the data in Azure storage instead of HDFS:</span></span>

* <span data-ttu-id="dc8c7-166">**Hergebruik en delen van gegevens:** de gegevens in HDFS bevinden zich in het rekencluster.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-166">**Data reuse and sharing:** The data in HDFS is located inside the compute cluster.</span></span> <span data-ttu-id="dc8c7-167">Alleen de toepassingen die toegang tot het rekencluster hebben, kunnen de gegevens met HDFS API's gebruiken.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-167">Only the applications that have access to the compute cluster can use the data by using HDFS APIs.</span></span> <span data-ttu-id="dc8c7-168">De gegevens in Azure Storage zijn toegankelijk via de HDFS API's of via de [Blob Storage REST API's][blob-storage-restAPI].</span><span class="sxs-lookup"><span data-stu-id="dc8c7-168">The data in Azure storage can be accessed either through the HDFS APIs or through the [Blob Storage REST APIs][blob-storage-restAPI].</span></span> <span data-ttu-id="dc8c7-169">Zo kan een grotere set toepassingen (inclusief andere HDInsight-clusters) en hulpprogramma's worden gebruikt om de gegevens te produceren en te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-169">Thus, a larger set of applications (including other HDInsight clusters) and tools can be used to produce and consume the data.</span></span>
* <span data-ttu-id="dc8c7-170">**Gegevensarchivering:** door gegevens op te slaan in Azure Storage, kunnen de HDInsight-clusters die worden gebruikt voor berekeningen, veilig worden verwijderd zonder dat er gegevens verloren gaan.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-170">**Data archiving:** Storing data in Azure storage enables the HDInsight clusters used for computation to be safely deleted without losing user data.</span></span>
* <span data-ttu-id="dc8c7-171">**Kosten voor gegevensopslag:** het langdurig opslaan van gegevens in DFS is duurder dan wanneer de gegevens worden opgeslagen in Azure Storage, omdat de kosten van een rekencluster hoger zijn dan de kosten van Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-171">**Data storage cost:** Storing data in DFS for the long term is more costly than storing the data in Azure storage because the cost of a compute cluster is higher than the cost of Azure storage.</span></span> <span data-ttu-id="dc8c7-172">Daarnaast bespaart u op de kosten voor het laden van gegevens omdat de gegevens niet opnieuw hoeven te worden geladen voor elk rekencluster dat wordt gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-172">In addition, because the data does not have to be reloaded for every compute cluster generation, you are also saving data loading costs.</span></span>
* <span data-ttu-id="dc8c7-173">**Elastisch uitbreiden:** hoewel HDFS u een uitgebreid bestandssysteem biedt, wordt de schaal bepaald door het aantal knooppunten dat u voor het cluster maakt.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-173">**Elastic scale-out:** Although HDFS provides you with a scaled-out file system, the scale is determined by the number of nodes that you create for your cluster.</span></span> <span data-ttu-id="dc8c7-174">Het wijzigen van de schaal is mogelijk een complexer proces dan. Vertrouw hiervoor niet zonder meer op de elastische schalingsmogelijkheden waarover u automatisch beschikt in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-174">Changing the scale can become a more complicated process than relying on the elastic scaling capabilities that you get automatically in Azure storage.</span></span>
* <span data-ttu-id="dc8c7-175">**Geo-replicatie:** uw Azure-opslag kan geografisch worden gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-175">**Geo-replication:** Your Azure storage can be geo-replicated.</span></span> <span data-ttu-id="dc8c7-176">Hoewel u dit de mogelijkheid van geografisch herstel en gegevensredundantie biedt, zal een failover naar de geografisch gerepliceerde locatie van grote invloed zijn op uw prestaties en kan dit tot extra kosten leiden.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-176">Although this gives you geographic recovery and data redundancy, a failover to the geo-replicated location severely impacts your performance, and it may incur additional costs.</span></span> <span data-ttu-id="dc8c7-177">U wordt daarom aangeraden de keuze van geo-replicatie goed te overwegen en alleen te gebruiken als de waarde van de gegevens de extra kosten waard zijn.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-177">So our recommendation is to choose the geo-replication wisely and only if the value of the data is worth the additional cost.</span></span>

<span data-ttu-id="dc8c7-178">Bepaalde MapReduce-taken en -pakketten kunnen tussenliggende resultaten genereren die u niet wilt opslaan in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-178">Certain MapReduce jobs and packages may create intermediate results that you don't really want to store in Azure storage.</span></span> <span data-ttu-id="dc8c7-179">In dat geval kunt u ervoor kiezen de gegevens op te slaan in de lokale HDFS.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-179">In that case, you can elect to store the data in the local HDFS.</span></span> <span data-ttu-id="dc8c7-180">HDInsight gebruikt DFS voor verschillende tussenliggende resultaten in Hive-taken en andere processen.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-180">In fact, HDInsight uses DFS for several of these intermediate results in Hive jobs and other processes.</span></span>

> [!NOTE]
> <span data-ttu-id="dc8c7-181">De meeste HDFS-opdrachten (bijvoorbeeld <b>ls</b>, <b>copyFromLocal</b> en <b>mkdir</b>) blijven gewoon naar verwachting werken.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-181">Most HDFS commands (for example, <b>ls</b>, <b>copyFromLocal</b> and <b>mkdir</b>) still work as expected.</span></span> <span data-ttu-id="dc8c7-182">Alleen de opdrachten die specifiek voor de systeemeigen HDFS-implementatie zijn (ook wel DFS genoemd), zoals <b>fschk</b> en <b>dfsadmin</b>, vertonen afwijkend gedrag in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-182">Only the commands that are specific to the native HDFS implementation (which is referred to as DFS), such as <b>fschk</b> and <b>dfsadmin</b>, show different behavior in Azure storage.</span></span>
> 
> 

## <a name="create-blob-containers"></a><span data-ttu-id="dc8c7-183">Blob-containers maken</span><span class="sxs-lookup"><span data-stu-id="dc8c7-183">Create Blob containers</span></span>
<span data-ttu-id="dc8c7-184">Als u blobs wilt gebruiken, maakt u eerst een [Azure Storage-account][azure-storage-create].</span><span class="sxs-lookup"><span data-stu-id="dc8c7-184">To use blobs, you first create an [Azure Storage account][azure-storage-create].</span></span> <span data-ttu-id="dc8c7-185">Als onderdeel hiervan geeft u een Azure-regio op waar het opslagaccount wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-185">As part of this, you specify an Azure region where the storage account is created.</span></span> <span data-ttu-id="dc8c7-186">Het cluster en het opslagaccount moeten worden gehost in dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-186">The cluster and the storage account must be hosted in the same region.</span></span> <span data-ttu-id="dc8c7-187">De SQL Server-database van de Hive-metastore en Oozie-metastore moeten zich ook in dezelfde regio bevinden.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-187">The Hive metastore SQL Server database and Oozie metastore SQL Server database must also be located in the same region.</span></span>

<span data-ttu-id="dc8c7-188">Elke blob die u maakt, behoort tot een container in uw Azure Storage-account, ongeacht de locatie van de blob.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-188">Wherever it lives, each blob you create belongs to a container in your Azure Storage account.</span></span> <span data-ttu-id="dc8c7-189">Deze container kan een bestaande blob zijn die buiten HDInsight is gemaakt. Het kan echter ook een container zijn die is gemaakt voor een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-189">This container may be an existing blob that was created outside of HDInsight, or it may be a container that is created for an HDInsight cluster.</span></span>

<span data-ttu-id="dc8c7-190">In de standaard-blobcontainer worden clusterspecifieke gegevens opgeslagen, zoals taakgeschiedenis en logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-190">The default Blob container stores cluster-specific information such as job history and logs.</span></span> <span data-ttu-id="dc8c7-191">Deel een standaard blob-container niet met meerdere HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-191">Don't share a default Blob container with multiple HDInsight clusters.</span></span> <span data-ttu-id="dc8c7-192">Hierdoor kan de taakgeschiedenis beschadigd raken.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-192">This might corrupt job history.</span></span> <span data-ttu-id="dc8c7-193">U kunt voor elk cluster het beste een andere container gebruiken en de gedeelde gegevens in een gekoppeld opslagaccount plaatsen dat is opgegeven in de implementatie van alle relevante cluster, in plaats van het standaardopslagaccount.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-193">It is recommended to use a different container for each cluster and put shared data on a linked storage account specified in deployment of all relevant clusters rather than the default storage account.</span></span> <span data-ttu-id="dc8c7-194">Zie [HDInsight-clusters maken][hdinsight-creation] voor meer informatie over het configureren van gekoppelde opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-194">For more information on configuring linked storage accounts, see [Create HDInsight clusters][hdinsight-creation].</span></span> <span data-ttu-id="dc8c7-195">U kunt een standaardopslagcontainer echter opnieuw gebruiken nadat het oorspronkelijke HDInsight-cluster is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-195">However you can reuse a default storage container after the original HDInsight cluster has been deleted.</span></span> <span data-ttu-id="dc8c7-196">Voor HBase-clusters kunt u het HBase-tabelschema en de bijbehorende gegevens behouden door een nieuw HBase-cluster te maken met de standaard-blobcontainer die wordt gebruikt door een verwijderd HBase-cluster.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-196">For HBase clusters, you can actually retain the HBase table schema and data by creating a new HBase cluster using the default blob container that is used by an HBase cluster that has been deleted.</span></span>

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]

### <a name="use-the-azure-portal"></a><span data-ttu-id="dc8c7-197">Azure Portal gebruiken</span><span class="sxs-lookup"><span data-stu-id="dc8c7-197">Use the Azure portal</span></span>
<span data-ttu-id="dc8c7-198">Wanneer u een HDInsight-cluster maakt vanuit de portal, kunt u (zoals hieronder wordt getoond) de details van het opslagaccount opgeven.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-198">When creating an HDInsight cluster from the Portal, you have the options (as shown below) to provide the storage account details.</span></span> <span data-ttu-id="dc8c7-199">U kunt ook opgeven of u een extra opslagaccount aan het cluster wilt koppelen en, zo ja, Data Lake Store of een andere Azure Storage-blob als de extra opslagruimte kiezen.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-199">You can also specify whether you want an additional storage account associated with the cluster, and if so, choose from Data Lake Store or another Azure Storage blob as the additional storage.</span></span>

![Gegevensbron voor het maken van HDInsight Hadoop](./media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> <span data-ttu-id="dc8c7-201">Het gebruik van een extra opslagaccount op een andere locatie dan het HDInsight-cluster wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-201">Using an additional storage account in a different location than the HDInsight cluster is not supported.</span></span>


### <a name="use-azure-powershell"></a><span data-ttu-id="dc8c7-202">Azure PowerShell gebruiken</span><span class="sxs-lookup"><span data-stu-id="dc8c7-202">Use Azure PowerShell</span></span>
<span data-ttu-id="dc8c7-203">Als u [Azure PowerShell hebt geïnstalleerd en geconfigureerd][powershell-install], kunt u het volgende achter de Azure PowerShell-prompt typen om een opslagaccount en container te maken:</span><span class="sxs-lookup"><span data-stu-id="dc8c7-203">If you [installed and configured Azure PowerShell][powershell-install], you can use the following from the Azure PowerShell prompt to create a storage account and container:</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

    $SubscriptionID = "<Your Azure Subscription ID>"
    $ResourceGroupName = "<New Azure Resource Group Name>"
    $Location = "EAST US 2"

    $StorageAccountName = "<New Azure Storage Account Name>"
    $containerName = "<New Azure Blob Container Name>"

    Add-AzureRmAccount
    Select-AzureRmSubscription -SubscriptionId $SubscriptionID

    # Create resource group
    New-AzureRmResourceGroup -name $ResourceGroupName -Location $Location

    # Create default storage account
    New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageAccountName -Location $Location -Type Standard_LRS 

    # Create default blob containers
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -StorageAccountName $StorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  
    New-AzureStorageContainer -Name $containerName -Context $destContext

### <a name="use-azure-cli"></a><span data-ttu-id="dc8c7-204">Azure CLI gebruiken</span><span class="sxs-lookup"><span data-stu-id="dc8c7-204">Use Azure CLI</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

<span data-ttu-id="dc8c7-205">Als u [de Azure CLI hebt geïnstalleerd en geconfigureerd](../cli-install-nodejs.md), kan de volgende opdracht worden gebruikt om een opslagaccount en container te maken.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-205">If you have [installed and configured the Azure CLI](../cli-install-nodejs.md), the following command can be used to a storage account and container.</span></span>

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> <span data-ttu-id="dc8c7-206">De parameter `--type` geeft aan hoe het opslagaccount wordt gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-206">The `--type` parameter indicates how the storage account is replicated.</span></span> <span data-ttu-id="dc8c7-207">Zie [Azure Storage-replicatie](../storage/storage-redundancy.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-207">For more information, see [Azure Storage Replication](../storage/storage-redundancy.md).</span></span> <span data-ttu-id="dc8c7-208">U kunt ZRS beter niet gebruiken, aangezien ZRS de pagina-blob, het bestand, de tabel of de wachtrij niet ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-208">Don't use ZRS as ZRS doesn't support page blob, file, table, or queue.</span></span>
> 
> 

<span data-ttu-id="dc8c7-209">U wordt gevraagd de geografische regio op te geven waar het opslagaccount is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-209">You are prompted to specify the geographic region that the storage account is created in.</span></span> <span data-ttu-id="dc8c7-210">U moet de opslagaccount in dezelfde regio maken waarin u ook uw HDInsight-cluster wilt maken.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-210">You should create the storage account in the same region that you plan on creating your HDInsight cluster.</span></span>

<span data-ttu-id="dc8c7-211">Zodra het opslagaccount is gemaakt, gebruikt u de volgende opdracht om de sleutels voor de opslagaccount op te halen:</span><span class="sxs-lookup"><span data-stu-id="dc8c7-211">Once the storage account is created, use the following command to retrieve the storage account keys:</span></span>

    azure storage account keys list <storageaccountname>

<span data-ttu-id="dc8c7-212">Gebruik de volgende opdracht om een container te maken:</span><span class="sxs-lookup"><span data-stu-id="dc8c7-212">To create a container, use the following command:</span></span>

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="address-files-in-azure-storage"></a><span data-ttu-id="dc8c7-213">Bestanden in Azure Storage adresseren</span><span class="sxs-lookup"><span data-stu-id="dc8c7-213">Address files in Azure storage</span></span>
<span data-ttu-id="dc8c7-214">Het URI-schema om bestanden in Azure Storage vanuit HDInsight te openen:</span><span class="sxs-lookup"><span data-stu-id="dc8c7-214">The URI scheme for accessing files in Azure storage from HDInsight is:</span></span>

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

<span data-ttu-id="dc8c7-215">Het URI-schema biedt niet-versleutelde toegang (met het voorvoegsel *wasb:*) en SSL-versleutelde toegang (met *wasbs*).</span><span class="sxs-lookup"><span data-stu-id="dc8c7-215">The URI scheme provides unencrypted access (with the *wasb:* prefix) and SSL encrypted access (with *wasbs*).</span></span> <span data-ttu-id="dc8c7-216">Waar mogelijk kunt u het beste *wasbs* gebruiken, zelfs voor de toegang tot gegevens die zich in dezelfde regio in Azure bevinden.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-216">We recommend using *wasbs* wherever possible, even when accessing data that lives inside the same region in Azure.</span></span>

<span data-ttu-id="dc8c7-217">Met &lt;BlobStorageContainerName&gt; wordt de naam van de blobcontainer in Azure Storage aangeduid.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-217">The &lt;BlobStorageContainerName&gt; identifies the name of the blob container in Azure storage.</span></span>
<span data-ttu-id="dc8c7-218">Met &lt;StorageAccountName&gt; wordt de naam van het Azure Storage-account aangeduid.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-218">The &lt;StorageAccountName&gt; identifies the Azure Storage account name.</span></span> <span data-ttu-id="dc8c7-219">Een FQDN (Fully Qualified Domain Name) is vereist.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-219">A fully qualified domain name (FQDN) is required.</span></span>

<span data-ttu-id="dc8c7-220">Als &lt;BlobStorageContainerName&gt; of &lt;StorageAccountName&gt; niet zijn opgegeven, wordt het standaardbestandssysteem gebruikt.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-220">If neither &lt;BlobStorageContainerName&gt; nor &lt;StorageAccountName&gt; has been specified, the default file system is used.</span></span> <span data-ttu-id="dc8c7-221">Voor de bestand op het standaardbestandssysteem kunt u een relatief of een absoluut pad gebruiken.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-221">For the files on the default file system, you can use a relative path or an absolute path.</span></span> <span data-ttu-id="dc8c7-222">U kunt bijvoorbeeld als volgt verwijzen naar het bestand *hadoop-mapreduce-examples.jar* dat bij HDInsight-clusters wordt geleverd:</span><span class="sxs-lookup"><span data-stu-id="dc8c7-222">For example, the *hadoop-mapreduce-examples.jar* file that comes with HDInsight clusters can be referred to by using one of the following:</span></span>

    wasb://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasb:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="dc8c7-223">De bestandsnaam is <i>hadoop examples.jar</i> in HDInsight versie 2.1- en 1.6-clusters.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-223">The file name is <i>hadoop-examples.jar</i> in HDInsight versions 2.1 and 1.6 clusters.</span></span>
> 
> 

<span data-ttu-id="dc8c7-224">Het &lt;pad&gt; is de HDFS-padnaam van het bestand of de map.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-224">The &lt;path&gt; is the file or directory HDFS path name.</span></span> <span data-ttu-id="dc8c7-225">Aangezien containers in Azure Storage gewoon sleutel-waardearchieven zijn, is er geen echt hiërarchisch bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-225">Because containers in Azure storage are simply key-value stores, there is no true hierarchical file system.</span></span> <span data-ttu-id="dc8c7-226">Een slash (/) in een blob-sleutel wordt geïnterpreteerd als een teken voor mapscheiding.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-226">A slash character ( / ) inside a blob key is interpreted as a directory separator.</span></span> <span data-ttu-id="dc8c7-227">De blob-naam voor bijvoorbeeld *hadoop-mapreduce-examples.jar* is:</span><span class="sxs-lookup"><span data-stu-id="dc8c7-227">For example, the blob name for *hadoop-mapreduce-examples.jar* is:</span></span>

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="dc8c7-228">Als u buiten HDInsight met blobs werkt, zullen de meeste hulpprogramma's de indeling WASB niet herkennen en wordt er in plaats daarvan een standaardpadindeling verwacht, zoals `example/jars/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-228">When working with blobs outside of HDInsight, most utilities do not recognize the WASB format and instead expect a basic path format, such as `example/jars/hadoop-mapreduce-examples.jar`.</span></span>
> 
> 

## <a name="access-blobs"></a><span data-ttu-id="dc8c7-229">Toegang tot blobs</span><span class="sxs-lookup"><span data-stu-id="dc8c7-229">Access blobs</span></span> 


### <span data-ttu-id="dc8c7-230"><a name="access-blobs-using-azure-powershell"></a> Azure PowerShell gebruiken</span><span class="sxs-lookup"><span data-stu-id="dc8c7-230"><a name="access-blobs-using-azure-powershell"></a> Use Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="dc8c7-231">De opdrachten in deze sectie bieden een eenvoudige voorbeeld van het gebruik van PowerShell voor toegang tot gegevens die zijn opgeslagen in blobs.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-231">The commands in this section provide a basic example of using PowerShell to access data stored in blobs.</span></span> <span data-ttu-id="dc8c7-232">Zie de [HDInsight Tools](https://github.com/Blackmist/hdinsight-tools) voor een uitgebreider voorbeeld dat is aangepast voor het werken met HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-232">For a more full-featured example that is customized for working with HDInsight, see the [HDInsight Tools](https://github.com/Blackmist/hdinsight-tools).</span></span>
> 
> 

<span data-ttu-id="dc8c7-233">Gebruik de volgende opdracht voor een lijst met blob-gerelateerde cmdlets:</span><span class="sxs-lookup"><span data-stu-id="dc8c7-233">Use the following command to list the blob-related cmdlets:</span></span>

    Get-Command *blob*

![Lijst met blob-gerelateerde PowerShell-cmdlets.][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a><span data-ttu-id="dc8c7-235">Bestanden uploaden</span><span class="sxs-lookup"><span data-stu-id="dc8c7-235">Upload files</span></span>
<span data-ttu-id="dc8c7-236">Zie [Gegevens uploaden naar HDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="dc8c7-236">See [Upload data to HDInsight][hdinsight-upload-data].</span></span>

#### <a name="download-files"></a><span data-ttu-id="dc8c7-237">Bestanden downloaden</span><span class="sxs-lookup"><span data-stu-id="dc8c7-237">Download files</span></span>
<span data-ttu-id="dc8c7-238">Met het volgende script wordt een blok-blob gedownload naar de huidige map.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-238">The following script downloads a block blob to the current folder.</span></span> <span data-ttu-id="dc8c7-239">Voordat u het script uitvoert, wijzigt u de directory in een map waarvoor u over schrijfmachtiging beschikt.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-239">Before running the script, change the directory to a folder where you have write permissions.</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $storageAccountName = "<AzureStorageAccountName>"   # The storage account used for the default file system specified at creation.
    $containerName = "<BlobStorageContainerName>"  # The default file system container has the same name as the cluster.
    $blob = "example/data/sample.log" # The name of the blob to be downloaded.

    # Use Add-AzureAccount if you haven't connected to your Azure subscription
    Login-AzureRmAccount 
    Select-AzureRmSubscription -SubscriptionID "<Your Azure Subscription ID>"

    Write-Host "Create a context object ... " -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  

    Write-Host "Download the blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $ContainerName -Blob $blob -Context $storageContext -Force

    Write-Host "List the downloaded file ..." -ForegroundColor Green
    cat "./$blob"

<span data-ttu-id="dc8c7-240">U kunt de volgende code gebruiken om de naam van de resourcegroep en de clusternaam op te geven:</span><span class="sxs-lookup"><span data-stu-id="dc8c7-240">Providing the resource group name and the cluster name, you can use the following code:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $clusterName = "<HDInsightClusterName>"
    $blob = "example/data/sample.log" # The name of the blob to be downloaded.

    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey 

    Write-Host "Download the blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob $blob -Context $storageContext -Force


#### <a name="delete-files"></a><span data-ttu-id="dc8c7-241">Bestanden verwijderen</span><span class="sxs-lookup"><span data-stu-id="dc8c7-241">Delete files</span></span>
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a><span data-ttu-id="dc8c7-242">Bestanden in een lijst weergeven</span><span class="sxs-lookup"><span data-stu-id="dc8c7-242">List files</span></span>
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a><span data-ttu-id="dc8c7-243">Hive-query's uitvoeren met een niet-gedefinieerd opslagaccount</span><span class="sxs-lookup"><span data-stu-id="dc8c7-243">Run Hive queries using an undefined storage account</span></span>
<span data-ttu-id="dc8c7-244">In dit voorbeeld ziet u hoe u een map uit het opslagaccount weergeeft die niet is gedefinieerd tijdens het creatieproces.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-244">This example shows how to list a folder from storage account that is not defined during the creating process.</span></span>
<span data-ttu-id="dc8c7-245">$clusterName = <HDInsightClusterName></span><span class="sxs-lookup"><span data-stu-id="dc8c7-245">$clusterName = "<HDInsightClusterName>"</span></span>

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasb://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"

### <a name="use-azure-cli"></a><span data-ttu-id="dc8c7-246">Azure CLI gebruiken</span><span class="sxs-lookup"><span data-stu-id="dc8c7-246">Use Azure CLI</span></span>
<span data-ttu-id="dc8c7-247">Gebruik de volgende opdracht voor een lijst met blob-gerelateerde opdrachten:</span><span class="sxs-lookup"><span data-stu-id="dc8c7-247">Use the following command to list the blob-related commands:</span></span>

    azure storage blob

<span data-ttu-id="dc8c7-248">**Voorbeeld van het gebruik van Azure CLI om een bestand te uploaden**</span><span class="sxs-lookup"><span data-stu-id="dc8c7-248">**Example of using Azure CLI to upload a file**</span></span>

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="dc8c7-249">**Voorbeeld van het gebruik van Azure CLI om een bestand te downloaden**</span><span class="sxs-lookup"><span data-stu-id="dc8c7-249">**Example of using Azure CLI to download a file**</span></span>

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="dc8c7-250">**Voorbeeld van het gebruik van Azure CLI om een bestand te verwijderen**</span><span class="sxs-lookup"><span data-stu-id="dc8c7-250">**Example of using Azure CLI to delete a file**</span></span>

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="dc8c7-251">**Voorbeeld van het gebruik van Azure CLI om een lijst met bestanden weer te geven**</span><span class="sxs-lookup"><span data-stu-id="dc8c7-251">**Example of using Azure CLI to list files**</span></span>

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="use-additional-storage-accounts"></a><span data-ttu-id="dc8c7-252">Extra opslagaccounts gebruiken</span><span class="sxs-lookup"><span data-stu-id="dc8c7-252">Use additional storage accounts</span></span>

<span data-ttu-id="dc8c7-253">Tijdens het maken van een HDInsight-cluster geeft u het Azure Storage-account op dat u ermee wilt koppelen.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-253">While creating an HDInsight cluster, you specify the Azure Storage account you want to associate with it.</span></span> <span data-ttu-id="dc8c7-254">Naast dit opslagaccount kunt u tijdens het maakproces of nadat een cluster is gemaakt extra opslagaccounts toevoegen uit hetzelfde Azure-abonnement of uit andere Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-254">In addition to this storage account, you can add additional storage accounts from the same Azure subscription or different Azure subscriptions during the creation process or after a cluster has been created.</span></span> <span data-ttu-id="dc8c7-255">Zie [HDInsight-clusters maken](hdinsight-hadoop-provision-linux-clusters.md) voor instructies over het toevoegen van extra opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-255">For instructions about adding additional storage accounts, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!WARNING]
> <span data-ttu-id="dc8c7-256">Het gebruik van een extra opslagaccount op een andere locatie dan het HDInsight-cluster wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-256">Using an additional storage account in a different location than the HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dc8c7-257">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dc8c7-257">Next steps</span></span>
<span data-ttu-id="dc8c7-258">In dit artikel hebt u geleerd hoe u HDFS-compatibele Azure-opslag kunt gebruiken met HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-258">In this article, you learned how to use HDFS-compatible Azure storage with HDInsight.</span></span> <span data-ttu-id="dc8c7-259">Zodoende kunt u een schaalbare, duurzame, archiveringsoplossing voor gegevensverzameling bouwen en HDInsight gebruiken om de informatie te ontsluiten in de opgeslagen gestructureerde en ongestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="dc8c7-259">This allows you to build scalable, long-term, archiving data acquisition solutions and use HDInsight to unlock the information inside the stored structured and unstructured data.</span></span>

<span data-ttu-id="dc8c7-260">Zie voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="dc8c7-260">For more information, see:</span></span>

* <span data-ttu-id="dc8c7-261">[Aan de slag met Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="dc8c7-261">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="dc8c7-262">Aan de slag met Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="dc8c7-262">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="dc8c7-263">[Gegevens uploaden naar HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="dc8c7-263">[Upload data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="dc8c7-264">[Hive gebruiken met HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="dc8c7-264">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="dc8c7-265">[Pig gebruiken met HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="dc8c7-265">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="dc8c7-266">[Handtekeningen voor gedeelde toegang van Azure Storage gebruiken om de toegang tot gegevens te beperken met HDInsight][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="dc8c7-266">[Use Azure Storage Shared Access Signatures to restrict access to data with HDInsight][hdinsight-use-sas]</span></span>

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
