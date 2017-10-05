---
title: "Gegevens kopiëren naar en van WASB naar Data Lake Store met Distcp | Microsoft Docs"
description: "Distcp hulpprogramma gebruiken om gegevens te kopiëren naar en van Azure Storage-Blobs naar Data Lake Store"
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
ms.openlocfilehash: 356a93d330e9e8ce3eb3c6c982fc5c2e087846a6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="use-distcp-to-copy-data-between-azure-storage-blobs-and-data-lake-store"></a><span data-ttu-id="f0733-103">Distcp gebruiken om gegevens te kopiëren tussen Azure Storage-blobs en Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f0733-103">Use Distcp to copy data between Azure Storage Blobs and Data Lake Store</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f0733-104">DistCp gebruiken</span><span class="sxs-lookup"><span data-stu-id="f0733-104">Using DistCp</span></span>](data-lake-store-copy-data-wasb-distcp.md)
> * [<span data-ttu-id="f0733-105">AdlCopy gebruiken</span><span class="sxs-lookup"><span data-stu-id="f0733-105">Using AdlCopy</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
>
>

<span data-ttu-id="f0733-106">Wanneer u een HDInsight-cluster dat toegang tot een Data Lake Store-account heeft hebt gemaakt, kunt u de Hadoop-ecosysteem-hulpprogramma's zoals Distcp gebruiken om gegevens te kopiëren **naar en uit** een HDInsight-cluster storage (WASB) naar een Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="f0733-106">Once you have created an HDInsight cluster that has access to a Data Lake Store account, you can use Hadoop ecosystem tools like Distcp to copy data **to and from** an HDInsight cluster storage (WASB) into a Data Lake Store account.</span></span> <span data-ttu-id="f0733-107">In dit artikel vindt instructies voor het om dit te bereiken.</span><span class="sxs-lookup"><span data-stu-id="f0733-107">This article provides instructions on how to achieve this.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0733-108">Vereisten</span><span class="sxs-lookup"><span data-stu-id="f0733-108">Prerequisites</span></span>
<span data-ttu-id="f0733-109">Voordat u dit artikel gaat lezen, moet u beschikken over het volgende:</span><span class="sxs-lookup"><span data-stu-id="f0733-109">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="f0733-110">**Een Azure-abonnement**.</span><span class="sxs-lookup"><span data-stu-id="f0733-110">**An Azure subscription**.</span></span> <span data-ttu-id="f0733-111">Zie [Gratis proefversie van Azure ophalen](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f0733-111">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f0733-112">**Een Azure Data Lake Store-account**.</span><span class="sxs-lookup"><span data-stu-id="f0733-112">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="f0733-113">Zie voor instructies over het maken van een [aan de slag met Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="f0733-113">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="f0733-114">**Azure HDInsight-cluster** met toegang tot een Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="f0733-114">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="f0733-115">Zie [een HDInsight-cluster maken met Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f0733-115">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="f0733-116">Zorg ervoor dat u extern bureaublad inschakelen voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="f0733-116">Make sure you enable Remote Desktop for the cluster.</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="f0733-117">Leert u snel met video's?</span><span class="sxs-lookup"><span data-stu-id="f0733-117">Do you learn fast with videos?</span></span>
<span data-ttu-id="f0733-118">[Bekijk deze video](https://mix.office.com/watch/1liuojvdx6sie) voor het kopiëren van gegevens tussen Azure Storage-Blobs en Data Lake Store met DistCp.</span><span class="sxs-lookup"><span data-stu-id="f0733-118">[Watch this video](https://mix.office.com/watch/1liuojvdx6sie) on how to copy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="use-distcp-from-an-hdinsight-linux-cluster"></a><span data-ttu-id="f0733-119">Distcp gebruik van een cluster met HDInsight Linux</span><span class="sxs-lookup"><span data-stu-id="f0733-119">Use Distcp from an HDInsight Linux cluster</span></span>

<span data-ttu-id="f0733-120">Een HDInsight-cluster wordt geleverd met het hulpprogramma Distcp die kan worden gebruikt om gegevens te kopiëren uit verschillende bronnen in een HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="f0733-120">An HDInsight cluster comes with the Distcp utility, which can be used to copy data from different sources into an HDInsight cluster.</span></span> <span data-ttu-id="f0733-121">Als u het HDInsight-cluster voor het gebruik van Data Lake Store als extra opslag hebt geconfigureerd, kan het hulpprogramma Distcp gebruikte out-of-the-box om gegevens te kopiëren naar en van een Data Lake Store-account zijn.</span><span class="sxs-lookup"><span data-stu-id="f0733-121">If you have configured the HDInsight cluster to use Data Lake Store as an additional storage, the Distcp utility can be used out-of-the-box to copy data to and from a Data Lake Store account as well.</span></span> <span data-ttu-id="f0733-122">In dit gedeelte kijken we hoe u het hulpprogramma Distcp.</span><span class="sxs-lookup"><span data-stu-id="f0733-122">In this section we look at how to use the Distcp utility.</span></span>

1. <span data-ttu-id="f0733-123">Op het bureaublad SSH verbinding maken met het cluster te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="f0733-123">From your desktop, use SSH to connect to the cluster.</span></span> <span data-ttu-id="f0733-124">Zie [verbinding maken met een Linux gebaseerde HDInsight-cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f0733-124">See [Connect to a Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span> <span data-ttu-id="f0733-125">Voer de opdrachten van de SSH-prompt.</span><span class="sxs-lookup"><span data-stu-id="f0733-125">Run the commands from the SSH prompt.</span></span>

2. <span data-ttu-id="f0733-126">Controleer of u toegang hebt tot de Azure Storage-Blobs (WASB).</span><span class="sxs-lookup"><span data-stu-id="f0733-126">Verify whether you can access the Azure Storage Blobs (WASB).</span></span> <span data-ttu-id="f0733-127">Voer de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="f0733-127">Run the following command:</span></span>

        hdfs dfs –ls wasb://<container_name>@<storage_account_name>.blob.core.windows.net/

    <span data-ttu-id="f0733-128">Dit moet een lijst verstrekken van inhoud in de blob storage.</span><span class="sxs-lookup"><span data-stu-id="f0733-128">This should provide a list of contents in the storage blob.</span></span>
3. <span data-ttu-id="f0733-129">Daarnaast moet worden gecontroleerd of u toegang hebt tot het Data Lake Store-account van het cluster.</span><span class="sxs-lookup"><span data-stu-id="f0733-129">Similarly, verify whether you can access the Data Lake Store account from the cluster.</span></span> <span data-ttu-id="f0733-130">Voer de volgende opdracht uit:</span><span class="sxs-lookup"><span data-stu-id="f0733-130">Run the following command:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net:443/

    <span data-ttu-id="f0733-131">Dit moet een lijst met bestanden/mappen in het Data Lake Store-account op te geven.</span><span class="sxs-lookup"><span data-stu-id="f0733-131">This should provide a list of files/folders in the Data Lake Store account.</span></span>
4. <span data-ttu-id="f0733-132">Distcp gebruiken om gegevens van WASB kopiëren naar een Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="f0733-132">Use Distcp to copy data from WASB to a Data Lake Store account.</span></span>

        hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder

    <span data-ttu-id="f0733-133">Hiermee kopieert de inhoud van de **voorbeeld/data/gutenberg/** map in WASB naar **/myfolder** in het Data Lake Store-account.</span><span class="sxs-lookup"><span data-stu-id="f0733-133">This will copy the contents of the **/example/data/gutenberg/** folder in WASB to **/myfolder** in the Data Lake Store account.</span></span>
5. <span data-ttu-id="f0733-134">Op deze manier Distcp gebruiken om gegevens van Data Lake Store-account te WASB kopiëren.</span><span class="sxs-lookup"><span data-stu-id="f0733-134">Similarly, use Distcp to copy data from Data Lake Store account to WASB.</span></span>

        hadoop distcp adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg

    <span data-ttu-id="f0733-135">Hiermee wordt de inhoud van gekopieerd **/myfolder** Data Lake Store-account dat **voorbeeld/data/gutenberg/** map in WASB.</span><span class="sxs-lookup"><span data-stu-id="f0733-135">This will copy the contents of **/myfolder** in the Data Lake Store account to **/example/data/gutenberg/** folder in WASB.</span></span>

## <a name="performance-considerations-while-using-distcp"></a><span data-ttu-id="f0733-136">Prestatie-overwegingen bij het gebruik van DistCp</span><span class="sxs-lookup"><span data-stu-id="f0733-136">Performance considerations while using DistCp</span></span>

<span data-ttu-id="f0733-137">Omdat de laagste granulatie DistCp van één bestand is, is voor het instellen van het maximum aantal gelijktijdige exemplaren de belangrijkste parameter optimaliseren op basis van Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f0733-137">Because DistCp’s lowest granularity is a single file, setting the maximum number of simultaneous copies is the most important parameter to optimize it against Data Lake Store.</span></span> <span data-ttu-id="f0733-138">Dit wordt bepaald door het aantal mappers ('M ') parameter op de opdrachtregel.</span><span class="sxs-lookup"><span data-stu-id="f0733-138">This is controlled by setting the number of mappers (‘m’) parameter on the command line.</span></span> <span data-ttu-id="f0733-139">Deze parameter bepaalt het maximum aantal mappers dat wordt gebruikt om gegevens te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="f0733-139">This parameter specifies the maximum number of mappers that will be used to copy data.</span></span> <span data-ttu-id="f0733-140">Standaardwaarde is 20.</span><span class="sxs-lookup"><span data-stu-id="f0733-140">Default value is 20.</span></span>

<span data-ttu-id="f0733-141">**Voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="f0733-141">**Example**</span></span>

    hadoop distcp wasb://<container_name>@<storage_account_name>.blob.core.windows.net/example/data/gutenberg adl://<data_lake_store_account>.azuredatalakestore.net:443/myfolder -m 100

### <a name="how-do-i-determine-the-number-of-mappers-to-use"></a><span data-ttu-id="f0733-142">Hoe bepaal ik het aantal mappers gebruiken?</span><span class="sxs-lookup"><span data-stu-id="f0733-142">How do I determine the number of mappers to use?</span></span>

<span data-ttu-id="f0733-143">Hier volgen een aantal richtlijnen.</span><span class="sxs-lookup"><span data-stu-id="f0733-143">Here's some guidance that you can use.</span></span>

* <span data-ttu-id="f0733-144">**Stap 1: Bepalen totale YARN geheugen** -de eerste stap is om te bepalen van de YARN-geheugen beschikbaar voor het cluster waarop u de taak DistCp uitvoert.</span><span class="sxs-lookup"><span data-stu-id="f0733-144">**Step 1: Determine total YARN memory** - The first step is to determine the YARN memory available to the cluster where you run the DistCp job.</span></span> <span data-ttu-id="f0733-145">Deze informatie is beschikbaar in de Ambari-portal die zijn gekoppeld aan het cluster.</span><span class="sxs-lookup"><span data-stu-id="f0733-145">This information is available in the Ambari portal associated with the cluster.</span></span> <span data-ttu-id="f0733-146">Navigeer naar YARN en Raadpleeg het tabblad configuraties om te zien van het geheugen YARN.</span><span class="sxs-lookup"><span data-stu-id="f0733-146">Navigate to YARN and view the Configs tab to see the YARN memory.</span></span> <span data-ttu-id="f0733-147">Als u het totale YARN-geheugen, Vermenigvuldig de YARN-geheugen per knooppunt met het aantal knooppunten dat u hebt in uw cluster.</span><span class="sxs-lookup"><span data-stu-id="f0733-147">To get the total YARN memory, multiply the YARN memory per node with the number of nodes you have in your cluster.</span></span>

* <span data-ttu-id="f0733-148">**Stap 2: Het aantal mappers berekenen** -de waarde van **m** gelijk is aan het quotiënt van totale YARN-geheugen, gedeeld door de grootte van de container YARN.</span><span class="sxs-lookup"><span data-stu-id="f0733-148">**Step 2: Calculate the number of mappers** - The value of **m** is equal to the quotient of total YARN memory divided by the YARN container size.</span></span> <span data-ttu-id="f0733-149">Informatie over de grootte van de YARN-container is beschikbaar in de Ambari-portal.</span><span class="sxs-lookup"><span data-stu-id="f0733-149">The YARN container size information is available in the Ambari portal as well.</span></span> <span data-ttu-id="f0733-150">Navigeer naar YARN en Raadpleeg het tabblad Configs.</span><span class="sxs-lookup"><span data-stu-id="f0733-150">Navigate to YARN and view the Configs tab.</span></span> <span data-ttu-id="f0733-151">De grootte van de container YARN wordt in dit venster weergegeven.</span><span class="sxs-lookup"><span data-stu-id="f0733-151">The YARN container size is displayed in this window.</span></span> <span data-ttu-id="f0733-152">De vergelijking moet worden uitgevoerd op het aantal mappers (**m**) is</span><span class="sxs-lookup"><span data-stu-id="f0733-152">The equation to arrive at the number of mappers (**m**) is</span></span>

        m = (number of nodes * YARN memory for each node) / YARN container size

<span data-ttu-id="f0733-153">**Voorbeeld**</span><span class="sxs-lookup"><span data-stu-id="f0733-153">**Example**</span></span>

<span data-ttu-id="f0733-154">Stel dat u een 4 D14v2s knooppunten in het cluster hebt en u probeert 10TB gegevens overzetten van 10 andere mappen.</span><span class="sxs-lookup"><span data-stu-id="f0733-154">Let’s assume that you have a 4 D14v2s nodes in the cluster and you are trying to transfer 10TB of data from 10 different folders.</span></span> <span data-ttu-id="f0733-155">Elk van de mappen verschillende hoeveelheden gegevens bevatten en de bestandsgrootte in elke map verschillen.</span><span class="sxs-lookup"><span data-stu-id="f0733-155">Each of the folders contain varying amounts of data and the file sizes within each folder are different.</span></span>

* <span data-ttu-id="f0733-156">Totale YARN geheugen - portal van de Ambari dat u vaststelt dat het geheugen YARN 96GB voor een D14-knooppunt.</span><span class="sxs-lookup"><span data-stu-id="f0733-156">Total YARN memory - From the Ambari portal you determine that the YARN memory is 96GB for a D14 node.</span></span> <span data-ttu-id="f0733-157">Ja, is de totale YARN-geheugen voor cluster met 4 knooppunten:</span><span class="sxs-lookup"><span data-stu-id="f0733-157">So, total YARN memory for 4 node cluster is:</span></span> 

        YARN memory = 4 * 96GB = 384GB

* <span data-ttu-id="f0733-158">Aantal mappers - u hebt vastgesteld dat de grootte van de container YARN 3072 voor een clusterknooppunt D14 uit de Ambari-portal.</span><span class="sxs-lookup"><span data-stu-id="f0733-158">Number of mappers - From the Ambari portal you determine that the YARN container size is 3072 for a D14 cluster node.</span></span> <span data-ttu-id="f0733-159">Dus is aantal mappers:</span><span class="sxs-lookup"><span data-stu-id="f0733-159">So, number of mappers is:</span></span>

        m = (4 nodes * 96GB) / 3072MB = 128 mappers

<span data-ttu-id="f0733-160">Als andere toepassingen geheugen gebruikt, kunt klikt u vervolgens u alleen een deel van uw cluster YARN-geheugen voor DistCp worden gebruikt.</span><span class="sxs-lookup"><span data-stu-id="f0733-160">If other applications are using memory, then you can choose to only use a portion of your cluster’s YARN memory for DistCp.</span></span>

### <a name="copying-large-datasets"></a><span data-ttu-id="f0733-161">Kopiëren van grote gegevenssets</span><span class="sxs-lookup"><span data-stu-id="f0733-161">Copying large datasets</span></span>

<span data-ttu-id="f0733-162">Wanneer de grootte van de gegevensset moet worden verplaatst erg groot is (bijvoorbeeld > 1TB) of als u tal van verschillende mappen hebt, overweeg het gebruik van meerdere DistCp taken.</span><span class="sxs-lookup"><span data-stu-id="f0733-162">When the size of the dataset to be moved is very large (e.g. >1TB) or if you have many different folders, you should consider using multiple DistCp jobs.</span></span> <span data-ttu-id="f0733-163">Er is waarschijnlijk geen prestatieverbetering te bereiken, maar wordt deze de taken verdeeld, zodat als een taak mislukt, u alleen hoeft wordt op te starten die specifieke taak in plaats van de hele taak.</span><span class="sxs-lookup"><span data-stu-id="f0733-163">There is likely no performance gain, but it will spread out the jobs so that if any job fails, you will only need to restart that specific job rather than the entire job.</span></span>

### <a name="limitations"></a><span data-ttu-id="f0733-164">Beperkingen</span><span class="sxs-lookup"><span data-stu-id="f0733-164">Limitations</span></span>

* <span data-ttu-id="f0733-165">DistCp probeert te maken van mappers met dezelfde grootte om prestaties te optimaliseren.</span><span class="sxs-lookup"><span data-stu-id="f0733-165">DistCp tries to create mappers that are similar in size to optimize performance.</span></span> <span data-ttu-id="f0733-166">Het aantal mappers mogelijk niet altijd betere prestaties.</span><span class="sxs-lookup"><span data-stu-id="f0733-166">Increasing the number of mappers may not always increase performance.</span></span>

* <span data-ttu-id="f0733-167">DistCp is beperkt tot slechts één toewijzen per bestand.</span><span class="sxs-lookup"><span data-stu-id="f0733-167">DistCp is limited to only one mapper per file.</span></span> <span data-ttu-id="f0733-168">Daarom moet u niet meer mappers dan er bestanden hebben.</span><span class="sxs-lookup"><span data-stu-id="f0733-168">Therefore, you should not have more mappers than you have files.</span></span> <span data-ttu-id="f0733-169">Aangezien DistCp alleen een toewijzen aan een bestand toewijzen kunt, beperkt dit de hoeveelheid gelijktijdigheid van taken die kan worden gebruikt voor het kopiëren van grote bestanden.</span><span class="sxs-lookup"><span data-stu-id="f0733-169">Since DistCp can only assign one mapper to a file, this limits the amount of concurrency that can be used to copy large files.</span></span>

* <span data-ttu-id="f0733-170">Als u een klein aantal grote bestanden hebt, moet klikt u vervolgens u gesplitst in 256MB bestand segmenten zodat u meer potentiële gelijktijdigheid van taken.</span><span class="sxs-lookup"><span data-stu-id="f0733-170">If you have a small number of large files, then you should split them into 256MB file chunks to give you more potential concurrency.</span></span> 
 
* <span data-ttu-id="f0733-171">Als u uit een Azure Blob Storage-account kopiëren wilt, kan uw taak kopiëren aan de kant van blob storage worden beperkt.</span><span class="sxs-lookup"><span data-stu-id="f0733-171">If you are copying from an Azure Blob Storage account, your copy job may be throttled on the blob storage side.</span></span> <span data-ttu-id="f0733-172">De prestaties van uw project kopiëren afnemen.</span><span class="sxs-lookup"><span data-stu-id="f0733-172">This will degrade the performance of your copy job.</span></span> <span data-ttu-id="f0733-173">Zie voor meer informatie over de beperkingen van Azure Blob Storage, Azure Storage-limieten op [Azure-abonnement en Servicelimieten](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="f0733-173">To learn more about the limits of Azure Blob Storage, see Azure Storage limits at [Azure subscription and service limits](../azure-subscription-service-limits.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="f0733-174">Zie ook</span><span class="sxs-lookup"><span data-stu-id="f0733-174">See also</span></span>
* [<span data-ttu-id="f0733-175">Gegevens kopiëren van Azure Storage-Blobs naar Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f0733-175">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="f0733-176">Gegevens in Data Lake Store beveiligen</span><span class="sxs-lookup"><span data-stu-id="f0733-176">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="f0733-177">Azure Data Lake Analytics gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f0733-177">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="f0733-178">Azure HDInsight gebruiken met Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="f0733-178">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
