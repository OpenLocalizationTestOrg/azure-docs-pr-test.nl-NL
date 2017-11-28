---
title: aaaQuery gegevens uit HDFS-compatibele Azure-opslag - Azure HDInsight | Microsoft Docs
description: Meer informatie over hoe tooquery gegevens uit Azure storage en Azure Data Lake Store toostore resultaten van de analyse.
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
ms.openlocfilehash: 1032d60424b65e3c0c54a25c7c15970b017a788f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-with-azure-hdinsight-clusters"></a><span data-ttu-id="74de9-104">Azure-opslag gebruiken met Azure HDInsight-clusters</span><span class="sxs-lookup"><span data-stu-id="74de9-104">Use Azure storage with Azure HDInsight clusters</span></span>

<span data-ttu-id="74de9-105">tooanalyze gegevens in HDInsight-cluster, kunt u Hallo gegevens in Azure Storage of Azure Data Lake Store opslaan.</span><span class="sxs-lookup"><span data-stu-id="74de9-105">tooanalyze data in HDInsight cluster, you can store hello data either in Azure Storage, Azure Data Lake Store, or both.</span></span> <span data-ttu-id="74de9-106">Beide opties voor opslag kunnen u toosafely verwijdert u het die hdinsight-clusters worden gebruikt voor berekeningen zonder verlies van gebruikersgegevens.</span><span class="sxs-lookup"><span data-stu-id="74de9-106">Both storage options enable you toosafely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="74de9-107">Hadoop ondersteunt een notatie van het standaardbestandssysteem Hallo.</span><span class="sxs-lookup"><span data-stu-id="74de9-107">Hadoop supports a notion of hello default file system.</span></span> <span data-ttu-id="74de9-108">Hallo standaardbestandssysteem impliceert een standaardschema en instantie.</span><span class="sxs-lookup"><span data-stu-id="74de9-108">hello default file system implies a default scheme and authority.</span></span> <span data-ttu-id="74de9-109">Het kan ook gebruikte tooresolve relatieve paden zijn.</span><span class="sxs-lookup"><span data-stu-id="74de9-109">It can also be used tooresolve relative paths.</span></span> <span data-ttu-id="74de9-110">Tijdens het Hallo-proces voor het HDInsight-cluster maken, kunt u een blob-container in Azure Storage als het standaardbestandssysteem Hallo of met HDInsight 3.5, kunt u Azure Storage of Azure Data Lake Store als Hallo bestanden van het systeem met een paar uitzonderingen.</span><span class="sxs-lookup"><span data-stu-id="74de9-110">During hello HDInsight cluster creation process, you can specify a blob container in Azure Storage as hello default file system, or with HDInsight 3.5, you can select either Azure Storage or Azure Data Lake Store as hello default files system with a few exceptions.</span></span> <span data-ttu-id="74de9-111">Zie voor Hallo ondersteuningsmogelijkheden van het gebruik van Data Lake Store als Hallo standaard en gekoppelde opslag, [beschikbaarheid van HDInsight-cluster](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).</span><span class="sxs-lookup"><span data-stu-id="74de9-111">For hello supportability of using Data Lake Store as both hello default and linked storage, see [Availabilities for HDInsight cluster](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).</span></span>

<span data-ttu-id="74de9-112">In dit artikel wordt uitgelegd hoe Azure Storage werkt met HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="74de9-112">In this article, you learn how Azure Storage works with HDInsight clusters.</span></span> <span data-ttu-id="74de9-113">toolearn hoe Data Lake Store werkt met HDInsight-clusters, Zie [gebruik Azure Data Lake Store met Azure HDInsight-clusters](hdinsight-hadoop-use-data-lake-store.md).</span><span class="sxs-lookup"><span data-stu-id="74de9-113">toolearn how Data Lake Store works with HDInsight clusters, see [Use Azure Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> <span data-ttu-id="74de9-114">Zie [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md) (Hadoop-clusters maken in HDInsight) voor meer informatie over het maken van HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="74de9-114">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="74de9-115">Azure Storage is een robuuste, algemene opslagoplossing die naadloos kan worden geïntegreerd met HDInsight.</span><span class="sxs-lookup"><span data-stu-id="74de9-115">Azure storage is a robust, general-purpose storage solution that integrates seamlessly with HDInsight.</span></span> <span data-ttu-id="74de9-116">HDInsight kunt gebruiken een blob-container in Azure Storage als het standaardbestandssysteem Hallo voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="74de9-116">HDInsight can use a blob container in Azure Storage as hello default file system for hello cluster.</span></span> <span data-ttu-id="74de9-117">Hallo volledige set onderdelen in HDInsight kan via een Hadoop distributed file system (HDFS)-interface werken rechtstreeks op gestructureerde of ongestructureerde gegevens als blobs worden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="74de9-117">Through a Hadoop distributed file system (HDFS) interface, hello full set of components in HDInsight can operate directly on structured or unstructured data stored as blobs.</span></span>

> [!WARNING]
> <span data-ttu-id="74de9-118">Er zijn verschillende opties beschikbaar bij het maken van een Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="74de9-118">There are several options available when creating an Azure Storage account.</span></span> <span data-ttu-id="74de9-119">Hallo volgende tabel bevat informatie over welke opties worden ondersteund met HDInsight:</span><span class="sxs-lookup"><span data-stu-id="74de9-119">hello following table provides information on what options are supported with HDInsight:</span></span>
> 
> | <span data-ttu-id="74de9-120">Type opslagaccount</span><span class="sxs-lookup"><span data-stu-id="74de9-120">Storage account type</span></span> | <span data-ttu-id="74de9-121">Opslaglaag</span><span class="sxs-lookup"><span data-stu-id="74de9-121">Storage tier</span></span> | <span data-ttu-id="74de9-122">Ondersteund met HDInsight</span><span class="sxs-lookup"><span data-stu-id="74de9-122">Supported with HDInsight</span></span> |
> | ------- | ------- | ------- |
> | <span data-ttu-id="74de9-123">Storage-account voor algemeen gebruik</span><span class="sxs-lookup"><span data-stu-id="74de9-123">General-purpose Storage Account</span></span> | <span data-ttu-id="74de9-124">Standard</span><span class="sxs-lookup"><span data-stu-id="74de9-124">Standard</span></span> | <span data-ttu-id="74de9-125">__Ja__</span><span class="sxs-lookup"><span data-stu-id="74de9-125">__Yes__</span></span> |
> | &nbsp; | <span data-ttu-id="74de9-126">Premium</span><span class="sxs-lookup"><span data-stu-id="74de9-126">Premium</span></span> | <span data-ttu-id="74de9-127">Nee</span><span class="sxs-lookup"><span data-stu-id="74de9-127">No</span></span> |
> | <span data-ttu-id="74de9-128">Blob Storage-account</span><span class="sxs-lookup"><span data-stu-id="74de9-128">Blob Storage Account</span></span> | <span data-ttu-id="74de9-129">Warm</span><span class="sxs-lookup"><span data-stu-id="74de9-129">Hot</span></span> | <span data-ttu-id="74de9-130">Nee</span><span class="sxs-lookup"><span data-stu-id="74de9-130">No</span></span> |
> | &nbsp; | <span data-ttu-id="74de9-131">Koud</span><span class="sxs-lookup"><span data-stu-id="74de9-131">Cool</span></span> | <span data-ttu-id="74de9-132">Nee</span><span class="sxs-lookup"><span data-stu-id="74de9-132">No</span></span> |

<span data-ttu-id="74de9-133">We raden niet Hallo standaard blob-container te gebruiken voor het opslaan van bedrijfsgegevens.</span><span class="sxs-lookup"><span data-stu-id="74de9-133">We do not recommend that you use hello default blob container for storing business data.</span></span> <span data-ttu-id="74de9-134">Hallo standaard blob-container verwijderen na elke tooreduce gebruik is opslagkosten een goede gewoonte.</span><span class="sxs-lookup"><span data-stu-id="74de9-134">Deleting hello default blob container after each use tooreduce storage cost is a good practice.</span></span> <span data-ttu-id="74de9-135">Opmerking die standaardcontainer Hallo bevat toepassings- en Logboeken.</span><span class="sxs-lookup"><span data-stu-id="74de9-135">Note that hello default container contains application and system logs.</span></span> <span data-ttu-id="74de9-136">Zorg ervoor tooretrieve Hallo logboeken voordat Hallo container worden verwijderd.</span><span class="sxs-lookup"><span data-stu-id="74de9-136">Make sure tooretrieve hello logs before deleting hello container.</span></span>

<span data-ttu-id="74de9-137">Het delen van een blobcontainer voor meerdere clusters wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="74de9-137">Sharing one blob container for multiple clusters is not supported.</span></span>

## <a name="hdinsight-storage-architecture"></a><span data-ttu-id="74de9-138">HDInsight-opslagarchitectuur</span><span class="sxs-lookup"><span data-stu-id="74de9-138">HDInsight storage architecture</span></span>
<span data-ttu-id="74de9-139">Hallo volgende diagram biedt een abstracte weergave van Hallo HDInsight-opslagarchitectuur van het gebruik van Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="74de9-139">hello following diagram provides an abstract view of hello HDInsight storage architecture of using Azure Storage:</span></span>

<span data-ttu-id="74de9-140">![Hadoop-clusters Hallo HDFS API tooaccess gebruik en opslaan van gestructureerde en ongestructureerde gegevens in Blob-opslag. ] (./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "HDInsight-opslagarchitectuur")</span><span class="sxs-lookup"><span data-stu-id="74de9-140">![Hadoop clusters use hello HDFS API tooaccess and store structured and unstructured data in Blob storage.](./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "HDInsight Storage Architecture")</span></span>

<span data-ttu-id="74de9-141">HDInsight biedt toegang toohello distributed file system dat lokaal is gekoppeld toohello rekenknooppunten.</span><span class="sxs-lookup"><span data-stu-id="74de9-141">HDInsight provides access toohello distributed file system that is locally attached toohello compute nodes.</span></span> <span data-ttu-id="74de9-142">Dit bestandssysteem toegankelijk zijn voor het gebruik van volledig gekwalificeerde URI, bijvoorbeeld Hallo:</span><span class="sxs-lookup"><span data-stu-id="74de9-142">This file system can be accessed by using hello fully qualified URI, for example:</span></span>

    hdfs://<namenodehost>/<path>

<span data-ttu-id="74de9-143">Bovendien kunt HDInsight u tooaccess gegevens die zijn opgeslagen in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="74de9-143">In addition, HDInsight allows you tooaccess data that is stored in Azure Storage.</span></span> <span data-ttu-id="74de9-144">Hallo-syntaxis is:</span><span class="sxs-lookup"><span data-stu-id="74de9-144">hello syntax is:</span></span>

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

<span data-ttu-id="74de9-145">Hier volgen enkele overwegingen bij het gebruik van een Azure Storage-account met HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="74de9-145">Here are some considerations when using Azure Storage account with HDInsight clusters.</span></span>

* <span data-ttu-id="74de9-146">**Containers in opslagaccounts Hallo die verbonden tooa cluster zijn:** omdat het Hallo-accountnaam en de sleutel gekoppeld aan cluster Hallo tijdens het maken zijn, hebt u volledige toegang toohello blobs in deze containers.</span><span class="sxs-lookup"><span data-stu-id="74de9-146">**Containers in hello storage accounts that are connected tooa cluster:** Because hello account name and key are associated with hello cluster during creation, you have full access toohello blobs in those containers.</span></span>

* <span data-ttu-id="74de9-147">**Openbare containers of openbare blobs in opslagaccounts die niet zijn verbonden tooa cluster:** hebt u alleen-lezen toegang toohello blobs in Hallo-containers.</span><span class="sxs-lookup"><span data-stu-id="74de9-147">**Public containers or public blobs in storage accounts that are NOT connected tooa cluster:** You have read-only permission toohello blobs in hello containers.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="74de9-148">Openbare containers kunt u een lijst met alle blobs die zijn beschikbaar in de container en containermetagegevens tooget.</span><span class="sxs-lookup"><span data-stu-id="74de9-148">Public containers allow you tooget a list of all blobs that are available in that container and get container metadata.</span></span> <span data-ttu-id="74de9-149">Openbare blobs kunnen u tooaccess Hallo blobs alleen als u Hallo exacte URL weet.</span><span class="sxs-lookup"><span data-stu-id="74de9-149">Public blobs allow you tooaccess hello blobs only if you know hello exact URL.</span></span> <span data-ttu-id="74de9-150">Zie voor meer informatie <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">toegang toocontainers en blobs beperken</a>.</span><span class="sxs-lookup"><span data-stu-id="74de9-150">For more information, see <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">Restrict access toocontainers and blobs</a>.</span></span>
  > 
  > 
* <span data-ttu-id="74de9-151">**Persoonlijke containers in opslagaccounts die niet verbonden tooa cluster:** Hallo blobs in Hallo containers niet meer toegankelijk tenzij u Hallo opslagaccount definieert wanneer u Hallo WebHCat-taken verzendt.</span><span class="sxs-lookup"><span data-stu-id="74de9-151">**Private containers in storage accounts that are NOT connected tooa cluster:** You can't access hello blobs in hello containers unless you define hello storage account when you submit hello WebHCat jobs.</span></span> <span data-ttu-id="74de9-152">Dit wordt verderop in dit artikel uitgelegd.</span><span class="sxs-lookup"><span data-stu-id="74de9-152">This is explained later in this article.</span></span>

<span data-ttu-id="74de9-153">Hallo storage-accounts die zijn gedefinieerd in het proces voor het maken van Hallo en de sleutels worden opgeslagen in %HADOOP_HOME%/conf/core-site.xml op Hallo clusterknooppunten.</span><span class="sxs-lookup"><span data-stu-id="74de9-153">hello storage accounts that are defined in hello creation process and their keys are stored in %HADOOP_HOME%/conf/core-site.xml on hello cluster nodes.</span></span> <span data-ttu-id="74de9-154">Hallo standaardgedrag van HDInsight is gedefinieerd in de bestand core site.xml Hallo van toouse Hallo storage-accounts.</span><span class="sxs-lookup"><span data-stu-id="74de9-154">hello default behavior of HDInsight is toouse hello storage accounts defined in hello core-site.xml file.</span></span> <span data-ttu-id="74de9-155">U kunt deze instelling wijzigen instellen met [Ambari](./hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="74de9-155">You can modify this setting using [Ambari](./hdinsight-hadoop-manage-ambari.md)</span></span>

<span data-ttu-id="74de9-156">Meerdere WebHCat-taken, waaronder Hive, MapReduce, Hadoop-streaming en Pig, kunnen een beschrijving van opslagaccounts en metagegevens bevatten.</span><span class="sxs-lookup"><span data-stu-id="74de9-156">Multiple WebHCat jobs, including Hive, MapReduce, Hadoop streaming, and Pig, can carry a description of storage accounts and metadata with them.</span></span> <span data-ttu-id="74de9-157">(Dit werkt momenteel voor Pig met opslagaccounts, maar niet voor metagegevens.) Zie [Using an HDInsight Cluster with Alternate Storage Accounts and Metastores](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx) (Een HDInsight-cluster gebruiken met alternatieve opslagaccounts en metastores) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="74de9-157">(This currently works for Pig with storage accounts, but not for metadata.) For more information, see [Using an HDInsight Cluster with Alternate Storage Accounts and Metastores](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).</span></span>

<span data-ttu-id="74de9-158">Blobs kunnen worden gebruikt voor gestructureerde en ongestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="74de9-158">Blobs can be used for structured and unstructured data.</span></span> <span data-ttu-id="74de9-159">De gegevens in blobcontainers worden opgeslagen als sleutel-waardeparen en er is geen maphiërarchie.</span><span class="sxs-lookup"><span data-stu-id="74de9-159">Blob containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="74de9-160">Maar Hallo slash-teken (/) kan worden gebruikt binnen Hallo toomake van sleutelnaam deze weergegeven als een bestand wordt opgeslagen in een mapstructuur.</span><span class="sxs-lookup"><span data-stu-id="74de9-160">However hello slash character ( / ) can be used within hello key name toomake it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="74de9-161">De sleutel van de blob kan bijvoorbeeld *input/log1.txt* zijn.</span><span class="sxs-lookup"><span data-stu-id="74de9-161">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="74de9-162">Er is niet echt *invoer* directory bestaat, maar vanwege de aanwezigheid van de toohello van Hallo slash-teken in naam van de hello, heeft Hallo vormgeving van een bestandspad.</span><span class="sxs-lookup"><span data-stu-id="74de9-162">No actual *input* directory exists, but due toohello presence of hello slash character in hello key name, it has hello appearance of a file path.</span></span>

## <span data-ttu-id="74de9-163"><a id="benefits"></a>Voordelen van Azure Storage</span><span class="sxs-lookup"><span data-stu-id="74de9-163"><a id="benefits"></a>Benefits of Azure Storage</span></span>
<span data-ttu-id="74de9-164">Hallo geïmpliceerde kosten als gevolg van elkaar niet plaatsen rekenclusters en opslagbronnen wordt verholpen door Hallo manier Hallo rekenclusters sluiten toohello opslagbronnen account in Azure-regio waar Hallo snel netwerk het maakt Hallo efficiënte rekenknooppunten hello tooaccess Hallo gegevens in Azure storage.</span><span class="sxs-lookup"><span data-stu-id="74de9-164">hello implied performance cost of not co-locating compute clusters and storage resources is mitigated by hello way hello compute clusters are created close toohello storage account resources inside hello Azure region, where hello high-speed network makes it efficient for hello compute nodes tooaccess hello data inside Azure storage.</span></span>

<span data-ttu-id="74de9-165">Er zijn enkele voordelen Hallo gegevens opslaan in Azure storage in plaats van HDFS:</span><span class="sxs-lookup"><span data-stu-id="74de9-165">There are several benefits associated with storing hello data in Azure storage instead of HDFS:</span></span>

* <span data-ttu-id="74de9-166">**Gegevens hergebruik en delen:** Hallo-gegevens in HDFS is te vinden in Hallo compute cluster.</span><span class="sxs-lookup"><span data-stu-id="74de9-166">**Data reuse and sharing:** hello data in HDFS is located inside hello compute cluster.</span></span> <span data-ttu-id="74de9-167">Alleen Hallo-toepassingen waarvoor toegang toohello compute cluster Hallo gegevens met HDFS API's kunt gebruiken.</span><span class="sxs-lookup"><span data-stu-id="74de9-167">Only hello applications that have access toohello compute cluster can use hello data by using HDFS APIs.</span></span> <span data-ttu-id="74de9-168">Hallo-gegevens in Azure storage zijn toegankelijk via Hallo HDFS API's of via Hallo [Blob Storage REST-API's][blob-storage-restAPI].</span><span class="sxs-lookup"><span data-stu-id="74de9-168">hello data in Azure storage can be accessed either through hello HDFS APIs or through hello [Blob Storage REST APIs][blob-storage-restAPI].</span></span> <span data-ttu-id="74de9-169">Dus een grotere set toepassingen (inclusief andere HDInsight-clusters) en hulpprogramma's worden gebruikt tooproduce en Hallo gegevens gebruiken.</span><span class="sxs-lookup"><span data-stu-id="74de9-169">Thus, a larger set of applications (including other HDInsight clusters) and tools can be used tooproduce and consume hello data.</span></span>
* <span data-ttu-id="74de9-170">**Gegevensarchivering:** opslaan van gegevens in Azure-opslag kunt Hallo HDInsight-clusters gebruikt voor berekeningen toobe veilig worden verwijderd zonder verlies van gebruikersgegevens.</span><span class="sxs-lookup"><span data-stu-id="74de9-170">**Data archiving:** Storing data in Azure storage enables hello HDInsight clusters used for computation toobe safely deleted without losing user data.</span></span>
* <span data-ttu-id="74de9-171">**Opslagkosten voor gegevens:** opslaan van gegevens in DFS voor de lange termijn Hallo duurder is dan de Hallo gegevens opslaan in Azure-opslag omdat Hallo kosten van een rekencluster hoger dan Hallo kosten van Azure-opslag is.</span><span class="sxs-lookup"><span data-stu-id="74de9-171">**Data storage cost:** Storing data in DFS for hello long term is more costly than storing hello data in Azure storage because hello cost of a compute cluster is higher than hello cost of Azure storage.</span></span> <span data-ttu-id="74de9-172">Bovendien omdat Hallo gegevens geen toobe geladen voor elk rekencluster dat wordt gegenereerd heeft, bespaart u kosten voor het laden van gegevens.</span><span class="sxs-lookup"><span data-stu-id="74de9-172">In addition, because hello data does not have toobe reloaded for every compute cluster generation, you are also saving data loading costs.</span></span>
* <span data-ttu-id="74de9-173">**Elastisch uitbreiden:** Hoewel HDFS u met een uitgebreid bestandssysteem biedt, Hallo schaal bepaald door Hallo aantal knooppunten dat u voor uw cluster maakt.</span><span class="sxs-lookup"><span data-stu-id="74de9-173">**Elastic scale-out:** Although HDFS provides you with a scaled-out file system, hello scale is determined by hello number of nodes that you create for your cluster.</span></span> <span data-ttu-id="74de9-174">Hallo schaal wijzigen, kan worden een complexer proces dan te vertrouwen op Hallo elastische schalingsmogelijkheden waarover u automatisch in Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="74de9-174">Changing hello scale can become a more complicated process than relying on hello elastic scaling capabilities that you get automatically in Azure storage.</span></span>
* <span data-ttu-id="74de9-175">**Geo-replicatie:** uw Azure-opslag kan geografisch worden gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="74de9-175">**Geo-replication:** Your Azure storage can be geo-replicated.</span></span> <span data-ttu-id="74de9-176">Hoewel dit u geografisch herstel en gegevensredundantie biedt, een failover toohello geografisch gerepliceerde locatie grote invloed zijn op de prestaties van uw en deze mogelijk extra kosten.</span><span class="sxs-lookup"><span data-stu-id="74de9-176">Although this gives you geographic recovery and data redundancy, a failover toohello geo-replicated location severely impacts your performance, and it may incur additional costs.</span></span> <span data-ttu-id="74de9-177">U wordt daarom aangeraden toochoose Hallo geo-replicatie goed en alleen als de waarde Hallo van Hallo gegevens waard Hallo extra kosten.</span><span class="sxs-lookup"><span data-stu-id="74de9-177">So our recommendation is toochoose hello geo-replication wisely and only if hello value of hello data is worth hello additional cost.</span></span>

<span data-ttu-id="74de9-178">Bepaalde MapReduce-taken en pakketten kunnen tussenliggende resultaten die u echt toostore in Azure-opslag niet wilt maken.</span><span class="sxs-lookup"><span data-stu-id="74de9-178">Certain MapReduce jobs and packages may create intermediate results that you don't really want toostore in Azure storage.</span></span> <span data-ttu-id="74de9-179">In dat geval kunt u aangeven of toostore Hallo gegevens in Hallo lokale HDFS.</span><span class="sxs-lookup"><span data-stu-id="74de9-179">In that case, you can elect toostore hello data in hello local HDFS.</span></span> <span data-ttu-id="74de9-180">HDInsight gebruikt DFS voor verschillende tussenliggende resultaten in Hive-taken en andere processen.</span><span class="sxs-lookup"><span data-stu-id="74de9-180">In fact, HDInsight uses DFS for several of these intermediate results in Hive jobs and other processes.</span></span>

> [!NOTE]
> <span data-ttu-id="74de9-181">De meeste HDFS-opdrachten (bijvoorbeeld <b>ls</b>, <b>copyFromLocal</b> en <b>mkdir</b>) blijven gewoon naar verwachting werken.</span><span class="sxs-lookup"><span data-stu-id="74de9-181">Most HDFS commands (for example, <b>ls</b>, <b>copyFromLocal</b> and <b>mkdir</b>) still work as expected.</span></span> <span data-ttu-id="74de9-182">Alleen opdrachten die specifieke toohello systeemeigen HDFS-implementatie (dit is bedoeld tooas DFS), zoals Hallo <b>fschk</b> en <b>dfsadmin</b>, vertonen afwijkend gedrag in Azure storage.</span><span class="sxs-lookup"><span data-stu-id="74de9-182">Only hello commands that are specific toohello native HDFS implementation (which is referred tooas DFS), such as <b>fschk</b> and <b>dfsadmin</b>, show different behavior in Azure storage.</span></span>
> 
> 

## <a name="create-blob-containers"></a><span data-ttu-id="74de9-183">Blob-containers maken</span><span class="sxs-lookup"><span data-stu-id="74de9-183">Create Blob containers</span></span>
<span data-ttu-id="74de9-184">toouse blobs, maakt u eerst een [Azure Storage-account][azure-storage-create].</span><span class="sxs-lookup"><span data-stu-id="74de9-184">toouse blobs, you first create an [Azure Storage account][azure-storage-create].</span></span> <span data-ttu-id="74de9-185">Als onderdeel hiervan geeft u een Azure-regio waar Hallo storage-account wordt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="74de9-185">As part of this, you specify an Azure region where hello storage account is created.</span></span> <span data-ttu-id="74de9-186">Hallo-cluster en Hallo storage-account moeten worden gehost in Hallo dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="74de9-186">hello cluster and hello storage account must be hosted in hello same region.</span></span> <span data-ttu-id="74de9-187">SQL Server-database voor Hallo Hive metastore en Oozie-metastore SQL Server-database ook moet zich bevinden in Hallo dezelfde regio.</span><span class="sxs-lookup"><span data-stu-id="74de9-187">hello Hive metastore SQL Server database and Oozie metastore SQL Server database must also be located in hello same region.</span></span>

<span data-ttu-id="74de9-188">Ongeacht de locatie wordt door elke blob die u maakt tooa-container in uw Azure Storage-account hoort.</span><span class="sxs-lookup"><span data-stu-id="74de9-188">Wherever it lives, each blob you create belongs tooa container in your Azure Storage account.</span></span> <span data-ttu-id="74de9-189">Deze container kan een bestaande blob zijn die buiten HDInsight is gemaakt. Het kan echter ook een container zijn die is gemaakt voor een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="74de9-189">This container may be an existing blob that was created outside of HDInsight, or it may be a container that is created for an HDInsight cluster.</span></span>

<span data-ttu-id="74de9-190">Hallo standaard Blob-container wordt clusterspecifieke informatie zoals de taakgeschiedenis en logboekbestanden opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="74de9-190">hello default Blob container stores cluster-specific information such as job history and logs.</span></span> <span data-ttu-id="74de9-191">Deel een standaard blob-container niet met meerdere HDInsight-clusters.</span><span class="sxs-lookup"><span data-stu-id="74de9-191">Don't share a default Blob container with multiple HDInsight clusters.</span></span> <span data-ttu-id="74de9-192">Hierdoor kan de taakgeschiedenis beschadigd raken.</span><span class="sxs-lookup"><span data-stu-id="74de9-192">This might corrupt job history.</span></span> <span data-ttu-id="74de9-193">Het verdient aanbeveling toouse een andere container voor elk cluster en de gedeelde gegevens op een gekoppelde storage-account opgegeven in de implementatie van alle relevante clusters in plaats van het standaardopslagaccount Hallo plaatsen.</span><span class="sxs-lookup"><span data-stu-id="74de9-193">It is recommended toouse a different container for each cluster and put shared data on a linked storage account specified in deployment of all relevant clusters rather than hello default storage account.</span></span> <span data-ttu-id="74de9-194">Zie [HDInsight-clusters maken][hdinsight-creation] voor meer informatie over het configureren van gekoppelde opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="74de9-194">For more information on configuring linked storage accounts, see [Create HDInsight clusters][hdinsight-creation].</span></span> <span data-ttu-id="74de9-195">U kunt een standaardopslagcontainer echter hergebruiken nadat Hallo oorspronkelijke HDInsight-cluster is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="74de9-195">However you can reuse a default storage container after hello original HDInsight cluster has been deleted.</span></span> <span data-ttu-id="74de9-196">Voor HBase-clusters, kunt u daadwerkelijk Hallo HBase-tabelschema en gegevens behouden door het maken van een nieuw HBase-cluster met Hallo standaard blob-container die wordt gebruikt door een HBase-cluster dat is verwijderd.</span><span class="sxs-lookup"><span data-stu-id="74de9-196">For HBase clusters, you can actually retain hello HBase table schema and data by creating a new HBase cluster using hello default blob container that is used by an HBase cluster that has been deleted.</span></span>

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]

### <a name="use-hello-azure-portal"></a><span data-ttu-id="74de9-197">Gebruik hello Azure-portal</span><span class="sxs-lookup"><span data-stu-id="74de9-197">Use hello Azure portal</span></span>
<span data-ttu-id="74de9-198">Wanneer u een HDInsight-cluster van Hallo Portal maakt, kunt u accountdetails Hallo opties (zoals hieronder wordt weergegeven) tooprovide Hallo opslag hebben.</span><span class="sxs-lookup"><span data-stu-id="74de9-198">When creating an HDInsight cluster from hello Portal, you have hello options (as shown below) tooprovide hello storage account details.</span></span> <span data-ttu-id="74de9-199">U kunt ook opgeven of u wilt een extra storage-account die is gekoppeld aan het Hallo-cluster, en zo ja, kiezen uit Data Lake Store of een andere Azure Storage-blob als Hallo extra opslagruimte.</span><span class="sxs-lookup"><span data-stu-id="74de9-199">You can also specify whether you want an additional storage account associated with hello cluster, and if so, choose from Data Lake Store or another Azure Storage blob as hello additional storage.</span></span>

![Gegevensbron voor het maken van HDInsight Hadoop](./media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> <span data-ttu-id="74de9-201">Met een account extra opslagruimte in een andere locatie dan Hallo HDInsight-cluster wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="74de9-201">Using an additional storage account in a different location than hello HDInsight cluster is not supported.</span></span>


### <a name="use-azure-powershell"></a><span data-ttu-id="74de9-202">Azure PowerShell gebruiken</span><span class="sxs-lookup"><span data-stu-id="74de9-202">Use Azure PowerShell</span></span>
<span data-ttu-id="74de9-203">Als u [geïnstalleerd en geconfigureerd Azure PowerShell][powershell-install], kunt u Hallo van hello Azure PowerShell-prompt toocreate een opslagaccount en container te volgen:</span><span class="sxs-lookup"><span data-stu-id="74de9-203">If you [installed and configured Azure PowerShell][powershell-install], you can use hello following from hello Azure PowerShell prompt toocreate a storage account and container:</span></span>

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

### <a name="use-azure-cli"></a><span data-ttu-id="74de9-204">Azure CLI gebruiken</span><span class="sxs-lookup"><span data-stu-id="74de9-204">Use Azure CLI</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

<span data-ttu-id="74de9-205">Als u hebt [geïnstalleerd en geconfigureerd hello Azure CLI](../cli-install-nodejs.md), Hallo volgende opdracht kan worden gebruikt tooa opslagaccount en container.</span><span class="sxs-lookup"><span data-stu-id="74de9-205">If you have [installed and configured hello Azure CLI](../cli-install-nodejs.md), hello following command can be used tooa storage account and container.</span></span>

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> <span data-ttu-id="74de9-206">Hallo `--type` parameter geeft aan hoe Hallo storage-account worden gerepliceerd.</span><span class="sxs-lookup"><span data-stu-id="74de9-206">hello `--type` parameter indicates how hello storage account is replicated.</span></span> <span data-ttu-id="74de9-207">Zie [Azure Storage-replicatie](../storage/storage-redundancy.md) voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="74de9-207">For more information, see [Azure Storage Replication](../storage/storage-redundancy.md).</span></span> <span data-ttu-id="74de9-208">U kunt ZRS beter niet gebruiken, aangezien ZRS de pagina-blob, het bestand, de tabel of de wachtrij niet ondersteunt.</span><span class="sxs-lookup"><span data-stu-id="74de9-208">Don't use ZRS as ZRS doesn't support page blob, file, table, or queue.</span></span>
> 
> 

<span data-ttu-id="74de9-209">U bent na vragen aan gebruiker toospecify Hallo geografische regio waarin Hallo storage-account is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="74de9-209">You are prompted toospecify hello geographic region that hello storage account is created in.</span></span> <span data-ttu-id="74de9-210">U kunt Hallo storage-account maken in Hallo dezelfde regio die u van plan bent over het maken van uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="74de9-210">You should create hello storage account in hello same region that you plan on creating your HDInsight cluster.</span></span>

<span data-ttu-id="74de9-211">Zodra het Hallo storage-account is gemaakt, gebruikt u Hallo opdracht tooretrieve hello opslagaccountsleutels te volgen:</span><span class="sxs-lookup"><span data-stu-id="74de9-211">Once hello storage account is created, use hello following command tooretrieve hello storage account keys:</span></span>

    azure storage account keys list <storageaccountname>

<span data-ttu-id="74de9-212">toocreate een container Hallo volgende opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="74de9-212">toocreate a container, use hello following command:</span></span>

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="address-files-in-azure-storage"></a><span data-ttu-id="74de9-213">Bestanden in Azure Storage adresseren</span><span class="sxs-lookup"><span data-stu-id="74de9-213">Address files in Azure storage</span></span>
<span data-ttu-id="74de9-214">Hallo-URI-schema voor toegang tot bestanden in Azure storage vanuit HDInsight is:</span><span class="sxs-lookup"><span data-stu-id="74de9-214">hello URI scheme for accessing files in Azure storage from HDInsight is:</span></span>

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

<span data-ttu-id="74de9-215">Hallo-URI-schema biedt niet-versleutelde toegang (Hello *wasb:* voorvoegsel) en SSL-versleutelde toegang (met *wasbs*).</span><span class="sxs-lookup"><span data-stu-id="74de9-215">hello URI scheme provides unencrypted access (with hello *wasb:* prefix) and SSL encrypted access (with *wasbs*).</span></span> <span data-ttu-id="74de9-216">Wordt u aangeraden *wasbs* waar mogelijk, zelfs wanneer toegang tot gegevens die zich in dezelfde regio in Azure Hallo.</span><span class="sxs-lookup"><span data-stu-id="74de9-216">We recommend using *wasbs* wherever possible, even when accessing data that lives inside hello same region in Azure.</span></span>

<span data-ttu-id="74de9-217">Hallo &lt;BlobStorageContainerName&gt; identificeert Hallo-naam van Hallo blob-container in Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="74de9-217">hello &lt;BlobStorageContainerName&gt; identifies hello name of hello blob container in Azure storage.</span></span>
<span data-ttu-id="74de9-218">Hallo &lt;StorageAccountName&gt; hello Azure Storage-accountnaam identificeert.</span><span class="sxs-lookup"><span data-stu-id="74de9-218">hello &lt;StorageAccountName&gt; identifies hello Azure Storage account name.</span></span> <span data-ttu-id="74de9-219">Een FQDN (Fully Qualified Domain Name) is vereist.</span><span class="sxs-lookup"><span data-stu-id="74de9-219">A fully qualified domain name (FQDN) is required.</span></span>

<span data-ttu-id="74de9-220">Als geen van beide &lt;BlobStorageContainerName&gt; noch &lt;StorageAccountName&gt; is opgegeven, Hallo standaardbestandssysteem wordt gebruikt.</span><span class="sxs-lookup"><span data-stu-id="74de9-220">If neither &lt;BlobStorageContainerName&gt; nor &lt;StorageAccountName&gt; has been specified, hello default file system is used.</span></span> <span data-ttu-id="74de9-221">Hallo-bestanden op het standaardbestandssysteem hello, kunt u een relatief pad of een absoluut pad.</span><span class="sxs-lookup"><span data-stu-id="74de9-221">For hello files on hello default file system, you can use a relative path or an absolute path.</span></span> <span data-ttu-id="74de9-222">Bijvoorbeeld, Hallo *hadoop-mapreduce-examples.jar* -bestand dat wordt geleverd met HDInsight-clusters kan worden waarnaar wordt verwezen tooby met behulp van een van de volgende Hallo:</span><span class="sxs-lookup"><span data-stu-id="74de9-222">For example, hello *hadoop-mapreduce-examples.jar* file that comes with HDInsight clusters can be referred tooby using one of hello following:</span></span>

    wasb://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasb:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="74de9-223">Hallo-bestandsnaam is <i>hadoop examples.jar</i> in HDInsight versie 2.1- en 1.6-clusters.</span><span class="sxs-lookup"><span data-stu-id="74de9-223">hello file name is <i>hadoop-examples.jar</i> in HDInsight versions 2.1 and 1.6 clusters.</span></span>
> 
> 

<span data-ttu-id="74de9-224">Hallo &lt;pad&gt; Hallo bestand of map HDFS-padnaam is.</span><span class="sxs-lookup"><span data-stu-id="74de9-224">hello &lt;path&gt; is hello file or directory HDFS path name.</span></span> <span data-ttu-id="74de9-225">Aangezien containers in Azure Storage gewoon sleutel-waardearchieven zijn, is er geen echt hiërarchisch bestandssysteem.</span><span class="sxs-lookup"><span data-stu-id="74de9-225">Because containers in Azure storage are simply key-value stores, there is no true hierarchical file system.</span></span> <span data-ttu-id="74de9-226">Een slash (/) in een blob-sleutel wordt geïnterpreteerd als een teken voor mapscheiding.</span><span class="sxs-lookup"><span data-stu-id="74de9-226">A slash character ( / ) inside a blob key is interpreted as a directory separator.</span></span> <span data-ttu-id="74de9-227">Bijvoorbeeld, Hallo blob-naam *hadoop-mapreduce-examples.jar* is:</span><span class="sxs-lookup"><span data-stu-id="74de9-227">For example, hello blob name for *hadoop-mapreduce-examples.jar* is:</span></span>

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="74de9-228">Als u werkt buiten HDInsight met blobs, hulpprogramma's voor de meeste niet herkent de indeling WASB hello en in plaats daarvan een standaardpadindeling zoals verwacht `example/jars/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="74de9-228">When working with blobs outside of HDInsight, most utilities do not recognize hello WASB format and instead expect a basic path format, such as `example/jars/hadoop-mapreduce-examples.jar`.</span></span>
> 
> 

## <a name="access-blobs"></a><span data-ttu-id="74de9-229">Toegang tot blobs</span><span class="sxs-lookup"><span data-stu-id="74de9-229">Access blobs</span></span> 


### <span data-ttu-id="74de9-230"><a name="access-blobs-using-azure-powershell"></a> Azure PowerShell gebruiken</span><span class="sxs-lookup"><span data-stu-id="74de9-230"><a name="access-blobs-using-azure-powershell"></a> Use Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="74de9-231">Hallo-opdrachten in deze sectie bieden een eenvoudige voorbeeld van het gebruik van PowerShell tooaccess gegevens opgeslagen in blobs.</span><span class="sxs-lookup"><span data-stu-id="74de9-231">hello commands in this section provide a basic example of using PowerShell tooaccess data stored in blobs.</span></span> <span data-ttu-id="74de9-232">Zie voor een uitgebreider voorbeeld dat is aangepast voor het werken met HDInsight hello [HDInsight Tools](https://github.com/Blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="74de9-232">For a more full-featured example that is customized for working with HDInsight, see hello [HDInsight Tools](https://github.com/Blackmist/hdinsight-tools).</span></span>
> 
> 

<span data-ttu-id="74de9-233">Gebruik Hallo volgende opdracht toolist Hallo blob-gerelateerde cmdlets:</span><span class="sxs-lookup"><span data-stu-id="74de9-233">Use hello following command toolist hello blob-related cmdlets:</span></span>

    Get-Command *blob*

![Lijst met blob-gerelateerde PowerShell-cmdlets.][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a><span data-ttu-id="74de9-235">Bestanden uploaden</span><span class="sxs-lookup"><span data-stu-id="74de9-235">Upload files</span></span>
<span data-ttu-id="74de9-236">Zie [uploaden van gegevens tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="74de9-236">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

#### <a name="download-files"></a><span data-ttu-id="74de9-237">Bestanden downloaden</span><span class="sxs-lookup"><span data-stu-id="74de9-237">Download files</span></span>
<span data-ttu-id="74de9-238">Hallo downloadt volgende script een blok-blob toohello huidige map.</span><span class="sxs-lookup"><span data-stu-id="74de9-238">hello following script downloads a block blob toohello current folder.</span></span> <span data-ttu-id="74de9-239">Voordat Hallo-script wordt uitgevoerd, moet u Hallo tooa map waar u schrijfmachtigingen hebt.</span><span class="sxs-lookup"><span data-stu-id="74de9-239">Before running hello script, change hello directory tooa folder where you have write permissions.</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $storageAccountName = "<AzureStorageAccountName>"   # hello storage account used for hello default file system specified at creation.
    $containerName = "<BlobStorageContainerName>"  # hello default file system container has hello same name as hello cluster.
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    # Use Add-AzureAccount if you haven't connected tooyour Azure subscription
    Login-AzureRmAccount 
    Select-AzureRmSubscription -SubscriptionID "<Your Azure Subscription ID>"

    Write-Host "Create a context object ... " -ForegroundColor Green
    $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey  

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $ContainerName -Blob $blob -Context $storageContext -Force

    Write-Host "List hello downloaded file ..." -ForegroundColor Green
    cat "./$blob"

<span data-ttu-id="74de9-240">Hallo Resourcegroepnaam en de clusternaam Hallo geven, kunt u Hallo volgende code gebruiken:</span><span class="sxs-lookup"><span data-stu-id="74de9-240">Providing hello resource group name and hello cluster name, you can use hello following code:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"
    $clusterName = "<HDInsightClusterName>"
    $blob = "example/data/sample.log" # hello name of hello blob toobe downloaded.

    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey 

    Write-Host "Download hello blob ..." -ForegroundColor Green
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob $blob -Context $storageContext -Force


#### <a name="delete-files"></a><span data-ttu-id="74de9-241">Bestanden verwijderen</span><span class="sxs-lookup"><span data-stu-id="74de9-241">Delete files</span></span>
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a><span data-ttu-id="74de9-242">Bestanden in een lijst weergeven</span><span class="sxs-lookup"><span data-stu-id="74de9-242">List files</span></span>
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a><span data-ttu-id="74de9-243">Hive-query's uitvoeren met een niet-gedefinieerd opslagaccount</span><span class="sxs-lookup"><span data-stu-id="74de9-243">Run Hive queries using an undefined storage account</span></span>
<span data-ttu-id="74de9-244">Dit voorbeeld toont hoe toolist een map van de storage-account is niet gedefinieerd tijdens het creatieproces Hallo.</span><span class="sxs-lookup"><span data-stu-id="74de9-244">This example shows how toolist a folder from storage account that is not defined during hello creating process.</span></span>
<span data-ttu-id="74de9-245">$clusterName = <HDInsightClusterName></span><span class="sxs-lookup"><span data-stu-id="74de9-245">$clusterName = "<HDInsightClusterName>"</span></span>

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasb://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"

### <a name="use-azure-cli"></a><span data-ttu-id="74de9-246">Azure CLI gebruiken</span><span class="sxs-lookup"><span data-stu-id="74de9-246">Use Azure CLI</span></span>
<span data-ttu-id="74de9-247">Gebruik Hallo volgende opdracht toolist Hallo blob-gerelateerde opdrachten:</span><span class="sxs-lookup"><span data-stu-id="74de9-247">Use hello following command toolist hello blob-related commands:</span></span>

    azure storage blob

<span data-ttu-id="74de9-248">**Voorbeeld van het gebruik van Azure CLI tooupload een bestand**</span><span class="sxs-lookup"><span data-stu-id="74de9-248">**Example of using Azure CLI tooupload a file**</span></span>

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="74de9-249">**Voorbeeld van het gebruik van Azure CLI toodownload een bestand**</span><span class="sxs-lookup"><span data-stu-id="74de9-249">**Example of using Azure CLI toodownload a file**</span></span>

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="74de9-250">**Voorbeeld van het gebruik van Azure CLI toodelete een bestand**</span><span class="sxs-lookup"><span data-stu-id="74de9-250">**Example of using Azure CLI toodelete a file**</span></span>

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="74de9-251">**Voorbeeld van het gebruik van Azure CLI toolist bestanden**</span><span class="sxs-lookup"><span data-stu-id="74de9-251">**Example of using Azure CLI toolist files**</span></span>

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="use-additional-storage-accounts"></a><span data-ttu-id="74de9-252">Extra opslagaccounts gebruiken</span><span class="sxs-lookup"><span data-stu-id="74de9-252">Use additional storage accounts</span></span>

<span data-ttu-id="74de9-253">Tijdens het maken van een HDInsight-cluster, moet u Hallo gewenste tooassociate aan Azure Storage-account opgeven.</span><span class="sxs-lookup"><span data-stu-id="74de9-253">While creating an HDInsight cluster, you specify hello Azure Storage account you want tooassociate with it.</span></span> <span data-ttu-id="74de9-254">Bovendien toothis storage-account, kunt u toevoegen extra opslagaccounts van Hallo dezelfde Azure-abonnement of verschillende Azure-abonnementen tijdens het maken van een Hallo of nadat een cluster is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="74de9-254">In addition toothis storage account, you can add additional storage accounts from hello same Azure subscription or different Azure subscriptions during hello creation process or after a cluster has been created.</span></span> <span data-ttu-id="74de9-255">Zie [HDInsight-clusters maken](hdinsight-hadoop-provision-linux-clusters.md) voor instructies over het toevoegen van extra opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="74de9-255">For instructions about adding additional storage accounts, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!WARNING]
> <span data-ttu-id="74de9-256">Met een account extra opslagruimte in een andere locatie dan Hallo HDInsight-cluster wordt niet ondersteund.</span><span class="sxs-lookup"><span data-stu-id="74de9-256">Using an additional storage account in a different location than hello HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="74de9-257">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="74de9-257">Next steps</span></span>
<span data-ttu-id="74de9-258">In dit artikel hebt u geleerd hoe toouse HDFS-compatibele Azure storage met HDInsight.</span><span class="sxs-lookup"><span data-stu-id="74de9-258">In this article, you learned how toouse HDFS-compatible Azure storage with HDInsight.</span></span> <span data-ttu-id="74de9-259">Hiermee kunt u toobuild schaalbare, op lange termijn, archiveren voor gegevensverzameling en gebruik HDInsight toounlock Hallo informatie binnen Hallo opgeslagen gestructureerde en ongestructureerde gegevens.</span><span class="sxs-lookup"><span data-stu-id="74de9-259">This allows you toobuild scalable, long-term, archiving data acquisition solutions and use HDInsight toounlock hello information inside hello stored structured and unstructured data.</span></span>

<span data-ttu-id="74de9-260">Zie voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="74de9-260">For more information, see:</span></span>

* <span data-ttu-id="74de9-261">[Aan de slag met Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="74de9-261">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="74de9-262">Aan de slag met Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="74de9-262">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="74de9-263">[Uploaden van gegevens tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="74de9-263">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="74de9-264">[Hive gebruiken met HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="74de9-264">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="74de9-265">[Pig gebruiken met HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="74de9-265">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="74de9-266">[Azure Storage Shared Access Signatures toorestrict toegang toodata gebruiken met HDInsight][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="74de9-266">[Use Azure Storage Shared Access Signatures toorestrict access toodata with HDInsight][hdinsight-use-sas]</span></span>

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
