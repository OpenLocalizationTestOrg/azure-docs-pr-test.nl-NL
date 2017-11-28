---
title: aaaCopy gegevens tooand van WASB in Data Lake Store met Distcp | Microsoft Docs
description: Distcp hulpprogramma toocopy gegevens tooand gebruiken uit Azure Storage Blobs tooData Lake Store
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ae2e9506-69dd-4b95-8759-4dadca37ea70
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: ec23410bbab0f82449a475412bc3b097c4a8fccd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="use-distcp-toocopy-data-between-azure-storage-blobs-and-data-lake-store"></a><span data-ttu-id="1f01b-103">Gebruik Distcp toocopy gegevens tussen Azure Storage-Blobs en Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1f01b-103">Use Distcp toocopy data between Azure Storage Blobs and Data Lake Store</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1f01b-104">DistCp gebruiken</span><span class="sxs-lookup"><span data-stu-id="1f01b-104">Using DistCp</span></span>](data-lake-store-copy-data-wasb-distcp.md)
> * [<span data-ttu-id="1f01b-105">AdlCopy gebruiken</span><span class="sxs-lookup"><span data-stu-id="1f01b-105">Using AdlCopy</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
>
>

<span data-ttu-id="1f01b-106">Nadat u een HDInsight-cluster met toegang tooa Data Lake Store-account hebt gemaakt, kunt u Hadoop-ecosysteem-hulpprogramma's zoals Distcp toocopy gegevens **tooand van** een HDInsight-cluster storage (WASB) naar een Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="1f01b-106">Once you have created an HDInsight cluster that has access tooa Data Lake Store account, you can use Hadoop ecosystem tools like Distcp toocopy data **tooand from** an HDInsight cluster storage (WASB) into a Data Lake Store account.</span></span> <span data-ttu-id="1f01b-107">In dit artikel bevat instructies voor het tooachieve dit.</span><span class="sxs-lookup"><span data-stu-id="1f01b-107">This article provides instructions on how tooachieve this.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1f01b-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="1f01b-108">Prerequisites</span></span>
<span data-ttu-id="1f01b-109">Voordat u dit artikel, moet u de volgende Hallo hebben:</span><span class="sxs-lookup"><span data-stu-id="1f01b-109">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="1f01b-110">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="1f01b-110">**An Azure subscription**.</span></span> <span data-ttu-id="1f01b-111">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="1f01b-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="1f01b-112">**Een Azure Data Lake Store-account**.</span><span class="sxs-lookup"><span data-stu-id="1f01b-112">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="1f01b-113">Voor instructies over het toocreate één, Zie [aan de slag met Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="1f01b-113">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="1f01b-114">**Azure HDInsight-cluster** met toegang tooa Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="1f01b-114">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="1f01b-115">Zie [een HDInsight-cluster maken met Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1f01b-115">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="1f01b-116">Zorg ervoor dat u extern bureaublad inschakelen voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="1f01b-116">Make sure you enable Remote Desktop for hello cluster.</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="1f01b-117">Leert u snel met video's?</span><span class="sxs-lookup"><span data-stu-id="1f01b-117">Do you learn fast with videos?</span></span>
<span data-ttu-id="1f01b-118">[Bekijk deze video](https://mix.office.com/watch/1liuojvdx6sie) over het toocopy gegevens tussen Azure Storage-Blobs en Data Lake Store met DistCp.</span><span class="sxs-lookup"><span data-stu-id="1f01b-118">[Watch this video](https://mix.office.com/watch/1liuojvdx6sie) on how toocopy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a><span data-ttu-id="1f01b-119">Distcp gebruik van een cluster met HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="1f01b-119">Use Distcp from an HDInsight Linux cluster</span></span>

<span data-ttu-id="1f01b-120">Een HDInsight-cluster wordt geleverd met Hallo Distcp hulpprogramma gebruikt toocopy gegevens uit verschillende bronnen in een HDInsight-cluster worden kan.</span><span class="sxs-lookup"><span data-stu-id="1f01b-120">An HDInsight cluster comes with hello Distcp utility, which can be used toocopy data from different sources into an HDInsight cluster.</span></span> <span data-ttu-id="1f01b-121">Als u hebt Hallo HDInsight cluster toouse Data Lake Store als extra opslag geconfigureerd, hello Distcp hulpprogramma kan worden gebruikt out-of-the-box toocopy gegevens tooand uit een Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="1f01b-121">If you have configured hello HDInsight cluster toouse Data Lake Store as an additional storage, hello Distcp utility can be used out-of-the-box toocopy data tooand from a Data Lake Store account as well.</span></span> <span data-ttu-id="1f01b-122">In dit gedeelte kijken we hoe toouse Hallo Distcp hulpprogramma.</span><span class="sxs-lookup"><span data-stu-id="1f01b-122">In this section we look at how toouse hello Distcp utility.</span></span>

1. <span data-ttu-id="1f01b-123">Op het bureaublad SSH tooconnect toohello cluster te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1f01b-123">From your desktop, use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="1f01b-124">Zie [Connect tooa Linux gebaseerde HDInsight-cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="1f01b-124">See [Connect tooa Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="1f01b-125">Hallo-opdrachten uitvoeren vanaf Hallo SSH-prompt.</span><span class="sxs-lookup"><span data-stu-id="1f01b-125">Run hello commands from hello SSH prompt.</span></span>

2. <span data-ttu-id="1f01b-126">Controleer of u toegang hebt tot hello Azure Storage-Blobs (WASB).</span><span class="sxs-lookup"><span data-stu-id="1f01b-126">Verify whether you can access hello Azure Storage Blobs (WASB).</span></span> <span data-ttu-id="1f01b-127">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="1f01b-127">Run hello following command:</span></span>

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    <span data-ttu-id="1f01b-128">Dit moet een lijst verstrekken van inhoud in Hallo storage-blob.</span><span class="sxs-lookup"><span data-stu-id="1f01b-128">This should provide a list of contents in hello storage blob.</span></span>
3. <span data-ttu-id="1f01b-129">Daarnaast moet worden gecontroleerd of u toegang hebt tot Hallo Data Lake Store-account uit Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="1f01b-129">Similarly, verify whether you can access hello Data Lake Store account from hello cluster.</span></span> <span data-ttu-id="1f01b-130">Hallo volgende opdracht uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="1f01b-130">Run hello following command:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    <span data-ttu-id="1f01b-131">Dit moet een lijst met bestanden/mappen in Hallo Data Lake Store-account op te geven.</span><span class="sxs-lookup"><span data-stu-id="1f01b-131">This should provide a list of files/folders in hello Data Lake Store account.</span></span>
4. <span data-ttu-id="1f01b-132">Distcp toocopy gegevens uit WASB tooa Data Lake Store-account gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1f01b-132">Use Distcp toocopy data from WASB tooa Data Lake Store account.</span></span>

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    <span data-ttu-id="1f01b-133">Hiermee worden gekopieerd Hallo inhoud Hallo **voorbeeld/data/gutenberg/** map in WASB te**/myfolder** in Hallo Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="1f01b-133">This will copy hello contents of hello **/example/data/gutenberg/** folder in WASB too**/myfolder** in hello Data Lake Store account.</span></span>
5. <span data-ttu-id="1f01b-134">Distcp toocopy gegevens uit Data Lake Store-account tooWASB op dezelfde manier gebruiken.</span><span class="sxs-lookup"><span data-stu-id="1f01b-134">Similarly, use Distcp toocopy data from Data Lake Store account tooWASB.</span></span>

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    <span data-ttu-id="1f01b-135">Hiermee worden gekopieerd Hallo inhoud van **/myfolder** in Hallo Data Lake Store-account te**voorbeeld/data/gutenberg/** map in WASB.</span><span class="sxs-lookup"><span data-stu-id="1f01b-135">This will copy hello contents of **/myfolder** in hello Data Lake Store account too**/example/data/gutenberg/** folder in WASB.</span></span>

## <a name="performance-considerations-while-using-distcp"></a><span data-ttu-id="1f01b-136">Prestatie-overwegingen bij het gebruik van DistCp</span><span class="sxs-lookup"><span data-stu-id="1f01b-136">Performance considerations while using DistCp</span></span>

<span data-ttu-id="1f01b-137">Omdat DistCp's laagste granulatie is een enkel bestand, instelling Hallo maximumaantal gelijktijdige exemplaren Hallo belangrijkste parameter toooptimize deze tegen Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="1f01b-137">Because DistCp’s lowest granularity is a single file, setting hello maximum number of simultaneous copies is hello most important parameter toooptimize it against Data Lake Store.</span></span> <span data-ttu-id="1f01b-138">Dit wordt bepaald door het aantal mappers hello ('M ') parameter op Hallo-opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="1f01b-138">This is controlled by setting hello number of mappers (‘m’) parameter on hello command line.</span></span> <span data-ttu-id="1f01b-139">Deze parameter bepaalt Hallo kunt u het maximum aantal mappers die gebruikt toocopy gegevens worden.</span><span class="sxs-lookup"><span data-stu-id="1f01b-139">This parameter specifies hello maximum number of mappers that will be used toocopy data.</span></span> <span data-ttu-id="1f01b-140">Standaardwaarde is 20.</span><span class="sxs-lookup"><span data-stu-id="1f01b-140">Default value is 20.</span></span>

<span data-ttu-id="1f01b-141">**Voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="1f01b-141">**Example**</span></span>

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-hello-number-of-mappers-toouse"></a><span data-ttu-id="1f01b-142">Hoe bepaal ik Hallo aantal mappers toouse?</span><span class="sxs-lookup"><span data-stu-id="1f01b-142">How do I determine hello number of mappers toouse?</span></span>

<span data-ttu-id="1f01b-143">Hier volgen een aantal richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="1f01b-143">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="1f01b-144">**Stap 1: Bepalen totale YARN geheugen** -Hallo eerste stap is toodetermine hello YARN geheugen beschikbaar toohello cluster waarop u Hallo DistCp taak uitvoert.</span><span class="sxs-lookup"><span data-stu-id="1f01b-144">**Step 1: Determine total YARN memory** - hello first step is toodetermine hello YARN memory available toohello cluster where you run hello DistCp job.</span></span> <span data-ttu-id="1f01b-145">Deze informatie is beschikbaar in Hallo Ambari portal die zijn gekoppeld aan het Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="1f01b-145">This information is available in hello Ambari portal associated with hello cluster.</span></span> <span data-ttu-id="1f01b-146">Navigeer tooYARN en Hallo Configs tabblad toosee hello YARN geheugen weergeven.</span><span class="sxs-lookup"><span data-stu-id="1f01b-146">Navigate tooYARN and view hello Configs tab toosee hello YARN memory.</span></span> <span data-ttu-id="1f01b-147">tooget hello totale YARN geheugen, Vermenigvuldig Hallo YARN-geheugen per knooppunt met het aantal knooppunten Hallo hebt in uw cluster.</span><span class="sxs-lookup"><span data-stu-id="1f01b-147">tooget hello total YARN memory, multiply hello YARN memory per node with hello number of nodes you have in your cluster.</span></span>

* <span data-ttu-id="1f01b-148">**Stap 2: Het aantal mappers Hallo berekenen** -waarde van Hallo **m** is gelijk toohello quotiënt van het totale YARN-geheugen, gedeeld door Hallo YARN container grootte.</span><span class="sxs-lookup"><span data-stu-id="1f01b-148">**Step 2: Calculate hello number of mappers** - hello value of **m** is equal toohello quotient of total YARN memory divided by hello YARN container size.</span></span> <span data-ttu-id="1f01b-149">Hallo informatie over de grootte van de YARN-container is beschikbaar in ook Hallo Ambari-portal.</span><span class="sxs-lookup"><span data-stu-id="1f01b-149">hello YARN container size information is available in hello Ambari portal as well.</span></span> <span data-ttu-id="1f01b-150">Navigeer tooYARN en weergave Hallo Configs tabblad Hallo YARN container grootte in dit venster wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="1f01b-150">Navigate tooYARN and view hello Configs tab. hello YARN container size is displayed in this window.</span></span> <span data-ttu-id="1f01b-151">Hallo vergelijking tooarrive Hallo aantal mappers (**m**) is</span><span class="sxs-lookup"><span data-stu-id="1f01b-151">hello equation tooarrive at hello number of mappers (**m**) is</span></span>

        m = (number of nodes * YARN memory for each node) / YARN container size

<span data-ttu-id="1f01b-152">**Voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="1f01b-152">**Example**</span></span>

<span data-ttu-id="1f01b-153">Stel dat u een 4 D14v2s knooppunten in cluster Hallo hebt en u tootransfer 10TB probeert van gegevens van 10 andere mappen.</span><span class="sxs-lookup"><span data-stu-id="1f01b-153">Let’s assume that you have a 4 D14v2s nodes in hello cluster and you are trying tootransfer 10TB of data from 10 different folders.</span></span> <span data-ttu-id="1f01b-154">Elk van de mappen Hallo verschillende hoeveelheden gegevens bevatten en de bestandsgrootte Hallo binnen elke map verschillen.</span><span class="sxs-lookup"><span data-stu-id="1f01b-154">Each of hello folders contain varying amounts of data and hello file sizes within each folder are different.</span></span>

* <span data-ttu-id="1f01b-155">Totale geheugen van de YARN - van Hallo Ambari portal u bepalen dat Hallo YARN-geheugen is 96GB voor een D14-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="1f01b-155">Total YARN memory - From hello Ambari portal you determine that hello YARN memory is 96GB for a D14 node.</span></span> <span data-ttu-id="1f01b-156">Ja, is de totale YARN-geheugen voor cluster met 4 knooppunten:</span><span class="sxs-lookup"><span data-stu-id="1f01b-156">So, total YARN memory for 4 node cluster is:</span></span> 

        YARN memory = 4 * 96GB = 384GB

* <span data-ttu-id="1f01b-157">Het aantal mappers - van Hallo u bepalen dat Hallo YARN container grootte is 3072 voor een clusterknooppunt D14 Ambari-portal.</span><span class="sxs-lookup"><span data-stu-id="1f01b-157">Number of mappers - From hello Ambari portal you determine that hello YARN container size is 3072 for a D14 cluster node.</span></span> <span data-ttu-id="1f01b-158">Dus is aantal mappers:</span><span class="sxs-lookup"><span data-stu-id="1f01b-158">So, number of mappers is:</span></span>

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

<span data-ttu-id="1f01b-159">Als andere toepassingen geheugen gebruikt, kunt klikt u vervolgens u kiezen tooonly gebruik een deel van uw cluster YARN-geheugen voor DistCp.</span><span class="sxs-lookup"><span data-stu-id="1f01b-159">If other applications are using memory, then you can choose tooonly use a portion of your cluster’s YARN memory for DistCp.</span></span>

### <a name="copying-large-datasets"></a><span data-ttu-id="1f01b-160">Kopiëren van grote gegevenssets</span><span class="sxs-lookup"><span data-stu-id="1f01b-160">Copying large datasets</span></span>

<span data-ttu-id="1f01b-161">Als de grootte van Hallo gegevensset toobe Hallo verplaatst erg groot is (bijvoorbeeld > 1TB) of als u tal van verschillende mappen hebt, overweeg het gebruik van meerdere DistCp taken.</span><span class="sxs-lookup"><span data-stu-id="1f01b-161">When hello size of hello dataset toobe moved is very large (e.g. >1TB) or if you have many different folders, you should consider using multiple DistCp jobs.</span></span> <span data-ttu-id="1f01b-162">Er is waarschijnlijk geen prestatieverbetering te bereiken, maar wordt het Hallo-taken verdeeld zodat als een taak mislukt, u alleen toorestart die specifieke taak in plaats van volledige Hallo-taak hoeft.</span><span class="sxs-lookup"><span data-stu-id="1f01b-162">There is likely no performance gain, but it will spread out hello jobs so that if any job fails, you will only need toorestart that specific job rather than hello entire job.</span></span>

### <a name="limitations"></a><span data-ttu-id="1f01b-163">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="1f01b-163">Limitations</span></span>

* <span data-ttu-id="1f01b-164">DistCp probeert toocreate mappers die in de prestaties van de grootte van toooptimize vergelijkbaar zijn.</span><span class="sxs-lookup"><span data-stu-id="1f01b-164">DistCp tries toocreate mappers that are similar in size toooptimize performance.</span></span> <span data-ttu-id="1f01b-165">Het aantal mappers Hallo mogelijk niet altijd vergroot, prestaties.</span><span class="sxs-lookup"><span data-stu-id="1f01b-165">Increasing hello number of mappers may not always increase performance.</span></span>

* <span data-ttu-id="1f01b-166">DistCp is beperkt tooonly één toewijzen per bestand.</span><span class="sxs-lookup"><span data-stu-id="1f01b-166">DistCp is limited tooonly one mapper per file.</span></span> <span data-ttu-id="1f01b-167">Daarom moet u niet meer mappers dan er bestanden hebben.</span><span class="sxs-lookup"><span data-stu-id="1f01b-167">Therefore, you should not have more mappers than you have files.</span></span> <span data-ttu-id="1f01b-168">Aangezien DistCp een-toewijzing alleen tooa bestand toewijzen kunt, wordt dit Hallo en de hoeveelheid gelijktijdigheid van taken die gebruikte toocopy grote bestanden kan worden beperkt.</span><span class="sxs-lookup"><span data-stu-id="1f01b-168">Since DistCp can only assign one mapper tooa file, this limits hello amount of concurrency that can be used toocopy large files.</span></span>

* <span data-ttu-id="1f01b-169">Als u een klein aantal grote bestanden hebt, hebt u ze in 256MB bestand segmenten toogive splitsen moet u meer potentiële gelijktijdigheid van taken.</span><span class="sxs-lookup"><span data-stu-id="1f01b-169">If you have a small number of large files, then you should split them into 256MB file chunks toogive you more potential concurrency.</span></span> 
 
* <span data-ttu-id="1f01b-170">Als u uit een Azure Blob Storage-account kopiëren wilt, kan uw taak kopiëren Hallo blob storage-zijde worden beperkt.</span><span class="sxs-lookup"><span data-stu-id="1f01b-170">If you are copying from an Azure Blob Storage account, your copy job may be throttled on hello blob storage side.</span></span> <span data-ttu-id="1f01b-171">Hallo-prestaties van uw project kopiëren afnemen.</span><span class="sxs-lookup"><span data-stu-id="1f01b-171">This will degrade hello performance of your copy job.</span></span> <span data-ttu-id="1f01b-172">toolearn meer informatie over het Hallo-limieten van Azure Blob Storage, Azure Storage-limieten op Zie [Azure-abonnement en Servicelimieten](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="1f01b-172">toolearn more about hello limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="1f01b-173">Zie ook</span><span class="sxs-lookup"><span data-stu-id="1f01b-173">See also</span></span>
* [<span data-ttu-id="1f01b-174">Gegevens kopiëren van Azure Storage Blobs tooData Lake Store</span><span class="sxs-lookup"><span data-stu-id="1f01b-174">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="1f01b-175">Gegevens in Data Lake Store beveiligen</span><span class="sxs-lookup"><span data-stu-id="1f01b-175">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="1f01b-176">Azure Data Lake Analytics gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1f01b-176">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="1f01b-177">Azure HDInsight gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="1f01b-177">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
