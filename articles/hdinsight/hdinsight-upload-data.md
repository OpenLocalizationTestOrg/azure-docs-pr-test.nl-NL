---
title: aaaUpload gegevens voor Hadoop-taken in HDInsight | Microsoft Docs
description: Meer informatie over hoe tooupload en toegang tot gegevens voor Hadoop-taken in HDInsight met behulp van Azure CLI, Azure Storage Explorer, Azure PowerShell, Hallo Hadoop vanaf de opdrachtregel of Sqoop Hallo.
keywords: etl-hadoop-gegevens ophalen van gegevens in hadoop, hadoop laden
services: hdinsight,storage
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 56b913ee-0f9a-4e9f-9eaf-c571f8603dd6
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/12/2017
ms.author: jgao
ms.openlocfilehash: 15da602085d41c19789e34800f3d9e238d7d1de8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a><span data-ttu-id="6298c-104">Upload gegevens voor Hadoop-taken in HDInsight</span><span class="sxs-lookup"><span data-stu-id="6298c-104">Upload data for Hadoop jobs in HDInsight</span></span>
<span data-ttu-id="6298c-105">Azure HDInsight biedt een complete Hadoop distributed file system (HDFS) via Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="6298c-105">Azure HDInsight provides a full-featured Hadoop distributed file system (HDFS) over Azure Blob storage.</span></span> <span data-ttu-id="6298c-106">Is bedoeld als een HDFS-extensie tooprovide een naadloze ervaring toocustomers.</span><span class="sxs-lookup"><span data-stu-id="6298c-106">It is designed as an HDFS extension tooprovide a seamless experience toocustomers.</span></span> <span data-ttu-id="6298c-107">Kan de volledige set Hallo van onderdelen in Hallo Hadoop-ecosysteem toooperate rechtstreeks op Hallo gegevens beheert.</span><span class="sxs-lookup"><span data-stu-id="6298c-107">It enables hello full set of components in hello Hadoop ecosystem toooperate directly on hello data it manages.</span></span> <span data-ttu-id="6298c-108">Azure Blob storage en HDFS zijn afzonderlijke bestandssystemen die zijn geoptimaliseerd voor de opslag van gegevens en berekeningen van die gegevens.</span><span class="sxs-lookup"><span data-stu-id="6298c-108">Azure Blob storage and HDFS are distinct file systems that are optimized for storage of data and computations on that data.</span></span> <span data-ttu-id="6298c-109">Zie voor meer informatie over Hallo voordelen van het gebruik van Azure Blob storage [Azure Blob storage gebruiken met HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="6298c-109">For information about hello benefits of using Azure Blob storage, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="6298c-110">**Vereisten**</span><span class="sxs-lookup"><span data-stu-id="6298c-110">**Prerequisites**</span></span>

<span data-ttu-id="6298c-111">Houd er rekening mee Hallo vereiste volgen voordat u begint:</span><span class="sxs-lookup"><span data-stu-id="6298c-111">Note hello following requirement before you begin:</span></span>

* <span data-ttu-id="6298c-112">Een Azure HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6298c-112">An Azure HDInsight cluster.</span></span> <span data-ttu-id="6298c-113">Zie voor instructies [aan de slag met Azure HDInsight] [ hdinsight-get-started] of [HDInsight-clusters inrichten][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="6298c-113">For instructions, see [Get started with Azure HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span>

## <a name="why-blob-storage"></a><span data-ttu-id="6298c-114">Waarom blobopslag?</span><span class="sxs-lookup"><span data-stu-id="6298c-114">Why blob storage?</span></span>
<span data-ttu-id="6298c-115">Azure HDInsight-clusters doorgaans zijn geïmplementeerd toorun MapReduce-taken en Hallo clusters worden verwijderd nadat deze taken hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="6298c-115">Azure HDInsight clusters are typically deployed toorun MapReduce jobs, and hello clusters are dropped after these jobs complete.</span></span> <span data-ttu-id="6298c-116">Behouden van Hallo-gegevens in HDFS-clusters Hallo nadat berekeningen voltooid zijn worden een toostore dure manier deze gegevens.</span><span class="sxs-lookup"><span data-stu-id="6298c-116">Keeping hello data in hello HDFS clusters after computations are complete would be an expensive way toostore this data.</span></span> <span data-ttu-id="6298c-117">Azure Blob storage is een maximaal beschikbare, sterk schaalbare, hoge capaciteit, lage kosten en deelbaar opslagoptie voor gegevens die toobe verwerkt met behulp van HDInsight is.</span><span class="sxs-lookup"><span data-stu-id="6298c-117">Azure Blob storage is a highly available, highly scalable, high capacity, low cost, and shareable storage option for data that is toobe processed using HDInsight.</span></span> <span data-ttu-id="6298c-118">Opslaan van gegevens in een blob kunt Hallo HDInsight-clusters die worden gebruikt voor berekeningen toobe veilig vrijgegeven zonder verlies van gegevens.</span><span class="sxs-lookup"><span data-stu-id="6298c-118">Storing data in a blob enables hello HDInsight clusters that are used for computation toobe safely released without losing data.</span></span>

### <a name="directories"></a><span data-ttu-id="6298c-119">Mappen</span><span class="sxs-lookup"><span data-stu-id="6298c-119">Directories</span></span>
<span data-ttu-id="6298c-120">Azure Blob storage-containers opslaan van gegevens als sleutel-waardeparen en er is geen maphiërarchie.</span><span class="sxs-lookup"><span data-stu-id="6298c-120">Azure Blob storage containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="6298c-121">Echter Hallo '/' teken kan worden gebruikt binnen Hallo sleutelnaam toomake deze weergegeven als een bestand wordt opgeslagen in een mapstructuur.</span><span class="sxs-lookup"><span data-stu-id="6298c-121">However hello "/" character can be used within hello key name toomake it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="6298c-122">HDInsight ziet deze alsof het werkelijke mappen.</span><span class="sxs-lookup"><span data-stu-id="6298c-122">HDInsight sees these as if they are actual directories.</span></span>

<span data-ttu-id="6298c-123">De sleutel van de blob kan bijvoorbeeld *input/log1.txt* zijn.</span><span class="sxs-lookup"><span data-stu-id="6298c-123">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="6298c-124">Er bestaat geen daadwerkelijke 'invoer' map, maar vanwege de aanwezigheid van Hallo toohello teken '/' hello sleutelnaam, is Hallo vormgeving van een bestandspad.</span><span class="sxs-lookup"><span data-stu-id="6298c-124">No actual "input" directory exists, but due toohello presence of hello "/" character in hello key name, it has hello appearance of a file path.</span></span>

<span data-ttu-id="6298c-125">Als gevolg hiervan, als u Azure Explorer hulpprogramma merkt u bepaalde bestanden 0 bytes.</span><span class="sxs-lookup"><span data-stu-id="6298c-125">Because of this, if you use Azure Explorer tools you may notice some 0 byte files.</span></span> <span data-ttu-id="6298c-126">Deze bestanden een tweeledig doel:</span><span class="sxs-lookup"><span data-stu-id="6298c-126">These files serve two purposes:</span></span>

* <span data-ttu-id="6298c-127">Als er lege mappen, worden ze van Hallo bestaan van de map Hallo markeren.</span><span class="sxs-lookup"><span data-stu-id="6298c-127">If there are empty folders, they mark of hello existence of hello folder.</span></span> <span data-ttu-id="6298c-128">Azure Blob-opslag is slimme genoeg tooknow als een blob foo/balk aangeroepen bestaat, er is een map met de naam **foo**.</span><span class="sxs-lookup"><span data-stu-id="6298c-128">Azure Blob storage is clever enough tooknow that if a blob called foo/bar exists, there is a folder called **foo**.</span></span> <span data-ttu-id="6298c-129">Maar de enige manier toosignify een lege map genaamd Hallo **foo** is door in plaats dit bestand speciale 0 bytes.</span><span class="sxs-lookup"><span data-stu-id="6298c-129">But hello only way toosignify an empty folder called **foo** is by having this special 0 byte file in place.</span></span>
* <span data-ttu-id="6298c-130">Ze hebben speciale metagegevens die nodig is door Hallo Hadoop bestand systeem, met name machtigingen Hallo en eigenaren voor Hallo mappen.</span><span class="sxs-lookup"><span data-stu-id="6298c-130">They hold special metadata that is needed by hello Hadoop file system, notably hello permissions and owners for hello folders.</span></span>

## <a name="command-line-utilities"></a><span data-ttu-id="6298c-131">Opdrachtregelprogramma 's</span><span class="sxs-lookup"><span data-stu-id="6298c-131">Command-line utilities</span></span>
<span data-ttu-id="6298c-132">Microsoft biedt de volgende hulpprogramma's toowork met Azure Blob storage Hallo:</span><span class="sxs-lookup"><span data-stu-id="6298c-132">Microsoft provides hello following utilities toowork with Azure Blob storage:</span></span>

| <span data-ttu-id="6298c-133">Hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="6298c-133">Tool</span></span> | <span data-ttu-id="6298c-134">Linux</span><span class="sxs-lookup"><span data-stu-id="6298c-134">Linux</span></span> | <span data-ttu-id="6298c-135">OS X</span><span class="sxs-lookup"><span data-stu-id="6298c-135">OS X</span></span> | <span data-ttu-id="6298c-136">Windows</span><span class="sxs-lookup"><span data-stu-id="6298c-136">Windows</span></span> |
| --- |:---:|:---:|:---:|
| <span data-ttu-id="6298c-137">[Azure-opdrachtregelinterface][azurecli]</span><span class="sxs-lookup"><span data-stu-id="6298c-137">[Azure Command-Line Interface][azurecli]</span></span> |<span data-ttu-id="6298c-138">✔</span><span class="sxs-lookup"><span data-stu-id="6298c-138">✔</span></span> |<span data-ttu-id="6298c-139">✔</span><span class="sxs-lookup"><span data-stu-id="6298c-139">✔</span></span> |<span data-ttu-id="6298c-140">✔</span><span class="sxs-lookup"><span data-stu-id="6298c-140">✔</span></span> |
| <span data-ttu-id="6298c-141">[Azure PowerShell][azure-powershell]</span><span class="sxs-lookup"><span data-stu-id="6298c-141">[Azure PowerShell][azure-powershell]</span></span> | | |<span data-ttu-id="6298c-142">✔</span><span class="sxs-lookup"><span data-stu-id="6298c-142">✔</span></span> |
| <span data-ttu-id="6298c-143">[AzCopy][azure-azcopy]</span><span class="sxs-lookup"><span data-stu-id="6298c-143">[AzCopy][azure-azcopy]</span></span> | | |<span data-ttu-id="6298c-144">✔</span><span class="sxs-lookup"><span data-stu-id="6298c-144">✔</span></span> |
| [<span data-ttu-id="6298c-145">Hadoop-opdracht</span><span class="sxs-lookup"><span data-stu-id="6298c-145">Hadoop command</span></span>](#commandline) |<span data-ttu-id="6298c-146">✔</span><span class="sxs-lookup"><span data-stu-id="6298c-146">✔</span></span> |<span data-ttu-id="6298c-147">✔</span><span class="sxs-lookup"><span data-stu-id="6298c-147">✔</span></span> |<span data-ttu-id="6298c-148">✔</span><span class="sxs-lookup"><span data-stu-id="6298c-148">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="6298c-149">Terwijl hello Azure CLI, Azure PowerShell en AzCopy kunnen alle worden gebruikt vanuit buiten Azure, Hallo Hadoop-opdracht is alleen beschikbaar op Hallo HDInsight-cluster en kunt alleen het laden van gegevens uit het lokale bestandssysteem Hallo in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="6298c-149">While hello Azure CLI, Azure PowerShell, and AzCopy can all be used from outside Azure, hello Hadoop command is only available on hello HDInsight cluster and only allows loading data from hello local file system into Azure Blob storage.</span></span>
>
>

### <span data-ttu-id="6298c-150"><a id="xplatcli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6298c-150"><a id="xplatcli"></a>Azure CLI</span></span>
<span data-ttu-id="6298c-151">Hello Azure CLI is een hulpprogramma voor meerdere platforms waarmee u toomanage Azure services.</span><span class="sxs-lookup"><span data-stu-id="6298c-151">hello Azure CLI is a cross-platform tool that allows you toomanage Azure services.</span></span> <span data-ttu-id="6298c-152">Hallo te volgen stappen tooupload gegevens tooAzure Blob-opslag gebruiken:</span><span class="sxs-lookup"><span data-stu-id="6298c-152">Use hello following steps tooupload data tooAzure Blob storage:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="6298c-153">[Installeer en configureer hello Azure CLI voor Mac, Linux en Windows](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="6298c-153">[Install and configure hello Azure CLI for Mac, Linux and Windows](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="6298c-154">Open een opdrachtprompt, bash of andere shell en gebruik Hallo tooauthenticate tooyour Azure-abonnement te volgen.</span><span class="sxs-lookup"><span data-stu-id="6298c-154">Open a command prompt, bash, or other shell, and use hello following tooauthenticate tooyour Azure subscription.</span></span>

        azure login

    <span data-ttu-id="6298c-155">Wanneer u wordt gevraagd, typt u Hallo-gebruikersnaam en wachtwoord voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="6298c-155">When prompted, enter hello user name and password for your subscription.</span></span>
3. <span data-ttu-id="6298c-156">Voer Hallo opdracht toolist Hallo storage-accounts voor uw abonnement te volgen:</span><span class="sxs-lookup"><span data-stu-id="6298c-156">Enter hello following command toolist hello storage accounts for your subscription:</span></span>

        azure storage account list
4. <span data-ttu-id="6298c-157">Selecteer opslagaccount Hallo Hallo blob toowork met gewenste bevat en voer vervolgens Hallo na de opdracht tooretrieve Hallo sleutel voor dit account gebruiken:</span><span class="sxs-lookup"><span data-stu-id="6298c-157">Select hello storage account that contains hello blob you want toowork with, then use hello following command tooretrieve hello key for this account:</span></span>

        azure storage account keys list <storage-account-name>

    <span data-ttu-id="6298c-158">Dit moet retourneren **primaire** en **secundaire** sleutels.</span><span class="sxs-lookup"><span data-stu-id="6298c-158">This should return **Primary** and **Secondary** keys.</span></span> <span data-ttu-id="6298c-159">Kopiëren Hallo **primaire** sleutelwaarde omdat deze wordt gebruikt in de volgende stappen Hallo.</span><span class="sxs-lookup"><span data-stu-id="6298c-159">Copy hello **Primary** key value because it will be used in hello next steps.</span></span>
5. <span data-ttu-id="6298c-160">Hallo na de opdracht tooretrieve een lijst met blobcontainers in Hallo storage-account gebruiken:</span><span class="sxs-lookup"><span data-stu-id="6298c-160">Use hello following command tooretrieve a list of blob containers within hello storage account:</span></span>

        azure storage container list -a <storage-account-name> -k <primary-key>
6. <span data-ttu-id="6298c-161">Gebruik Hallo opdrachten tooupload te volgen en bestanden toohello blobs downloaden:</span><span class="sxs-lookup"><span data-stu-id="6298c-161">Use hello following commands tooupload and download files toohello blob:</span></span>

   * <span data-ttu-id="6298c-162">een bestand tooupload:</span><span class="sxs-lookup"><span data-stu-id="6298c-162">tooupload a file:</span></span>

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * <span data-ttu-id="6298c-163">een bestand toodownload:</span><span class="sxs-lookup"><span data-stu-id="6298c-163">toodownload a file:</span></span>

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> <span data-ttu-id="6298c-164">Als u altijd met Hallo dezelfde werkt storage-account, stelt u Hallo omgevingsvariabelen in plaats van het opgeven van Hallo rekening te volgen en sleutel voor elke opdracht:</span><span class="sxs-lookup"><span data-stu-id="6298c-164">If you will always be working with hello same storage account, you can set hello following environment variables instead of specifying hello account and key for every command:</span></span>
>
> * <span data-ttu-id="6298c-165">**AZURE\_opslag\_ACCOUNT**: Hallo opslagaccountnaam</span><span class="sxs-lookup"><span data-stu-id="6298c-165">**AZURE\_STORAGE\_ACCOUNT**: hello storage account name</span></span>
> * <span data-ttu-id="6298c-166">**AZURE\_opslag\_toegang\_sleutel**: Hallo opslagaccountsleutel</span><span class="sxs-lookup"><span data-stu-id="6298c-166">**AZURE\_STORAGE\_ACCESS\_KEY**: hello storage account key</span></span>
>
>

### <span data-ttu-id="6298c-167"><a id="powershell"></a>Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6298c-167"><a id="powershell"></a>Azure PowerShell</span></span>
<span data-ttu-id="6298c-168">Azure PowerShell is een scriptomgeving toocontrol gebruiken en automatiseren Hallo-implementatie en beheer van uw workloads in Azure.</span><span class="sxs-lookup"><span data-stu-id="6298c-168">Azure PowerShell is a scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="6298c-169">Zie voor meer informatie over het configureren van uw werkstation toorun Azure PowerShell [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6298c-169">For information about configuring your workstation toorun Azure PowerShell, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="6298c-170">**tooupload een lokaal bestand tooAzure Blob-opslag**</span><span class="sxs-lookup"><span data-stu-id="6298c-170">**tooupload a local file tooAzure Blob storage**</span></span>

1. <span data-ttu-id="6298c-171">Open hello Azure PowerShell-console volgens de instructies in [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="6298c-171">Open hello Azure PowerShell console as instructed in [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="6298c-172">Hallo-waarden van Hallo eerste vijf variabelen in het volgende script Hallo instellen:</span><span class="sxs-lookup"><span data-stu-id="6298c-172">Set hello values of hello first five variables in hello following script:</span></span>

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get hello storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create hello storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy hello file from local workstation toohello Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. <span data-ttu-id="6298c-173">Hallo plakken wordt script in hello Azure PowerShell-console toorun toocopy Hallo-bestand is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="6298c-173">Paste hello script into hello Azure PowerShell console toorun it toocopy hello file.</span></span>

<span data-ttu-id="6298c-174">Bijvoorbeeld toowork van PowerShell-scripts die zijn gemaakt met HDInsight, Zie [HDInsight tools](https://github.com/blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="6298c-174">For example PowerShell scripts created toowork with HDInsight, see [HDInsight tools](https://github.com/blackmist/hdinsight-tools).</span></span>

### <span data-ttu-id="6298c-175"><a id="azcopy"></a>AzCopy</span><span class="sxs-lookup"><span data-stu-id="6298c-175"><a id="azcopy"></a>AzCopy</span></span>
<span data-ttu-id="6298c-176">AzCopy is een opdrachtregelprogramma dat is ontworpen toosimplify Hallo taak van het overbrengen van gegevens naar en van een Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="6298c-176">AzCopy is a command-line tool that is designed toosimplify hello task of transferring data into and out of an Azure Storage account.</span></span> <span data-ttu-id="6298c-177">U kunt gebruiken als een zelfstandige tool of gebruikmaken van dit hulpprogramma in een bestaande toepassing.</span><span class="sxs-lookup"><span data-stu-id="6298c-177">You can use it as a standalone tool or incorporate this tool in an existing application.</span></span> <span data-ttu-id="6298c-178">[Downloaden van AzCopy][azure-azcopy-download].</span><span class="sxs-lookup"><span data-stu-id="6298c-178">[Download AzCopy][azure-azcopy-download].</span></span>

<span data-ttu-id="6298c-179">Hallo AzCopy syntaxis is:</span><span class="sxs-lookup"><span data-stu-id="6298c-179">hello AzCopy syntax is:</span></span>

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

<span data-ttu-id="6298c-180">Zie voor meer informatie [AzCopy - bestanden voor Azure Blobs uploaden/downloaden][azure-azcopy].</span><span class="sxs-lookup"><span data-stu-id="6298c-180">For more information, see [AzCopy - Uploading/Downloading files for Azure Blobs][azure-azcopy].</span></span>

### <span data-ttu-id="6298c-181"><a id="commandline"></a>Hadoop-opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="6298c-181"><a id="commandline"></a>Hadoop command line</span></span>
<span data-ttu-id="6298c-182">Hallo Hadoop vanaf de opdrachtregel is alleen nuttig voor het opslaan van gegevens naar de blobopslag Hallo gegevens is al aanwezig op het hoofdknooppunt Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="6298c-182">hello Hadoop command line is only useful for storing data into blob storage when hello data is already present on hello cluster head node.</span></span>

<span data-ttu-id="6298c-183">In de volgorde toouse Hallo Hadoop-opdracht, moet u eerst toohello headnode met een van de volgende methoden Hallo verbinden:</span><span class="sxs-lookup"><span data-stu-id="6298c-183">In order toouse hello Hadoop command, you must first connect toohello headnode using one of hello following methods:</span></span>

* <span data-ttu-id="6298c-184">**HDInsight op basis van Windows**: [verbinding maken met behulp van extern bureaublad](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="6298c-184">**Windows-based HDInsight**: [Connect using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>
* <span data-ttu-id="6298c-185">**HDInsight op basis van Linux**: verbinding maken met behulp van SSH ([Hallo SSH-opdracht](hdinsight-hadoop-linux-use-ssh-unix.md) of [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span><span class="sxs-lookup"><span data-stu-id="6298c-185">**Linux-based HDInsight**: Connect using SSH ([hello SSH command](hdinsight-hadoop-linux-use-ssh-unix.md) or [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span></span>

<span data-ttu-id="6298c-186">Eenmaal zijn verbonden, kunt u Hallo syntaxis tooupload een bestand toostorage te volgen.</span><span class="sxs-lookup"><span data-stu-id="6298c-186">Once connected, you can use hello following syntax tooupload a file toostorage.</span></span>

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

<span data-ttu-id="6298c-187">Bijvoorbeeld: `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span><span class="sxs-lookup"><span data-stu-id="6298c-187">For example, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span></span>

<span data-ttu-id="6298c-188">Omdat Hallo standaardbestandssysteem voor HDInsight in Azure Blob-opslag, zich /example/data.txt in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="6298c-188">Because hello default file system for HDInsight is in Azure Blob storage, /example/data.txt is actually in Azure Blob storage.</span></span> <span data-ttu-id="6298c-189">U kunt ook toohello-bestand als verwijzen:</span><span class="sxs-lookup"><span data-stu-id="6298c-189">You can also refer toohello file as:</span></span>

    wasb:///example/data/data.txt

<span data-ttu-id="6298c-190">of</span><span class="sxs-lookup"><span data-stu-id="6298c-190">or</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

<span data-ttu-id="6298c-191">Zie voor een lijst met andere Hadoop die werken met bestanden opdrachten, [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span><span class="sxs-lookup"><span data-stu-id="6298c-191">For a list of other Hadoop commands that work with files, see [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span></span>

> [!WARNING]
> <span data-ttu-id="6298c-192">Op de HBase-clusters Hallo Standaardblokgrootte gebruikt bij het schrijven van gegevens is 256KB.</span><span class="sxs-lookup"><span data-stu-id="6298c-192">On HBase clusters, hello default block size used when writing data is 256KB.</span></span> <span data-ttu-id="6298c-193">Hoewel dit goed met HBase APIs of REST-API's werkt, met behulp van Hallo `hadoop` of `hdfs dfs` opdrachten toowrite gegevens groter zijn dan ~ 12 GB in een fout resulteert.</span><span class="sxs-lookup"><span data-stu-id="6298c-193">While this works fine when using HBase APIs or REST APIs, using hello `hadoop` or `hdfs dfs` commands toowrite data larger than ~12GB results in an error.</span></span> <span data-ttu-id="6298c-194">Zie Hallo [uitzondering om te schrijven op blob storage](#storageexception) sectie hieronder voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="6298c-194">See hello [storage exception for write on blob](#storageexception) section below for more information.</span></span>
>
>

## <a name="graphical-clients"></a><span data-ttu-id="6298c-195">Grafische clients</span><span class="sxs-lookup"><span data-stu-id="6298c-195">Graphical clients</span></span>
<span data-ttu-id="6298c-196">Er zijn ook enkele toepassingen die een grafische interface bieden voor het werken met Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="6298c-196">There are also several applications that provide a graphical interface for working with Azure Storage.</span></span> <span data-ttu-id="6298c-197">Hallo Hier volgt een lijst met enkele van deze toepassingen:</span><span class="sxs-lookup"><span data-stu-id="6298c-197">hello following is a list of a few of these applications:</span></span>

| <span data-ttu-id="6298c-198">Client</span><span class="sxs-lookup"><span data-stu-id="6298c-198">Client</span></span> | <span data-ttu-id="6298c-199">Linux</span><span class="sxs-lookup"><span data-stu-id="6298c-199">Linux</span></span> | <span data-ttu-id="6298c-200">OS X</span><span class="sxs-lookup"><span data-stu-id="6298c-200">OS X</span></span> | <span data-ttu-id="6298c-201">Windows</span><span class="sxs-lookup"><span data-stu-id="6298c-201">Windows</span></span> |
| --- |:---:|:---:|:---:|
| [<span data-ttu-id="6298c-202">Microsoft Visual Studio-hulpprogramma's voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="6298c-202">Microsoft Visual Studio Tools for HDInsight</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |<span data-ttu-id="6298c-203">✔</span><span class="sxs-lookup"><span data-stu-id="6298c-203">✔</span></span> |<span data-ttu-id="6298c-204">✔</span><span class="sxs-lookup"><span data-stu-id="6298c-204">✔</span></span> |<span data-ttu-id="6298c-205">✔</span><span class="sxs-lookup"><span data-stu-id="6298c-205">✔</span></span> |
| [<span data-ttu-id="6298c-206">Azure-opslagverkenner</span><span class="sxs-lookup"><span data-stu-id="6298c-206">Azure Storage Explorer</span></span>](http://storageexplorer.com/) |<span data-ttu-id="6298c-207">✔</span><span class="sxs-lookup"><span data-stu-id="6298c-207">✔</span></span> |<span data-ttu-id="6298c-208">✔</span><span class="sxs-lookup"><span data-stu-id="6298c-208">✔</span></span> |<span data-ttu-id="6298c-209">✔</span><span class="sxs-lookup"><span data-stu-id="6298c-209">✔</span></span> |
| [<span data-ttu-id="6298c-210">Cloud-opslag Studio 2</span><span class="sxs-lookup"><span data-stu-id="6298c-210">Cloud Storage Studio 2</span></span>](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |<span data-ttu-id="6298c-211">✔</span><span class="sxs-lookup"><span data-stu-id="6298c-211">✔</span></span> |
| [<span data-ttu-id="6298c-212">CloudXplorer</span><span class="sxs-lookup"><span data-stu-id="6298c-212">CloudXplorer</span></span>](http://clumsyleaf.com/products/cloudxplorer) | | |<span data-ttu-id="6298c-213">✔</span><span class="sxs-lookup"><span data-stu-id="6298c-213">✔</span></span> |
| [<span data-ttu-id="6298c-214">Azure Explorer</span><span class="sxs-lookup"><span data-stu-id="6298c-214">Azure Explorer</span></span>](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |<span data-ttu-id="6298c-215">✔</span><span class="sxs-lookup"><span data-stu-id="6298c-215">✔</span></span> |
| [<span data-ttu-id="6298c-216">Cyberduck</span><span class="sxs-lookup"><span data-stu-id="6298c-216">Cyberduck</span></span>](https://cyberduck.io/) | |<span data-ttu-id="6298c-217">✔</span><span class="sxs-lookup"><span data-stu-id="6298c-217">✔</span></span> |<span data-ttu-id="6298c-218">✔</span><span class="sxs-lookup"><span data-stu-id="6298c-218">✔</span></span> |

### <a name="visual-studio-tools-for-hdinsight"></a><span data-ttu-id="6298c-219">Visual Studio-hulpprogramma's voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="6298c-219">Visual Studio Tools for HDInsight</span></span>
<span data-ttu-id="6298c-220">Zie voor meer informatie [navigeren Hallo gekoppelde resources](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span><span class="sxs-lookup"><span data-stu-id="6298c-220">For more information, see [Navigate hello linked resources](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span></span>

### <span data-ttu-id="6298c-221"><a id="storageexplorer"></a>Azure Opslagverkenner</span><span class="sxs-lookup"><span data-stu-id="6298c-221"><a id="storageexplorer"></a>Azure Storage Explorer</span></span>
<span data-ttu-id="6298c-222">*Azure Storage Explorer* is een nuttig hulpmiddel om te bekijken en wijzigen van Hallo-gegevens in BLOB's.</span><span class="sxs-lookup"><span data-stu-id="6298c-222">*Azure Storage Explorer* is a useful tool for inspecting and altering hello data in blobs.</span></span> <span data-ttu-id="6298c-223">Het is een gratis, open source-hulpprogramma dat kan worden gedownload vanaf [http://storageexplorer.com/](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="6298c-223">It is a free, open source tool that can be downloaded from [http://storageexplorer.com/](http://storageexplorer.com/).</span></span> <span data-ttu-id="6298c-224">Hallo broncode is beschikbaar via deze koppeling ook.</span><span class="sxs-lookup"><span data-stu-id="6298c-224">hello source code is available from this link as well.</span></span>

<span data-ttu-id="6298c-225">Voordat u Hallo-hulpprogramma gebruiken, moet u weten Azure naam en sleutel van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="6298c-225">Before using hello tool, you must know your Azure storage account name and account key.</span></span> <span data-ttu-id="6298c-226">Zie voor instructies over het ophalen van deze informatie Hallo ' How to: toegangssleutels voor opslag weergeven, kopiëren en opnieuw genereren ' sectie van [maken, beheren of verwijderen van een opslagaccount][azure-create-storage-account].</span><span class="sxs-lookup"><span data-stu-id="6298c-226">For instructions about getting this information, see hello "How to: View, copy and regenerate storage access keys" section of [Create, manage, or delete a storage account][azure-create-storage-account].</span></span>

1. <span data-ttu-id="6298c-227">Azure Storage Explorer uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="6298c-227">Run Azure Storage Explorer.</span></span> <span data-ttu-id="6298c-228">Als dit Hallo eerst u Hallo Opslagverkenner hebt uitgevoerd, wordt u gevraagd om Hallo **_Storage accountnaam** en **opslagaccountsleutel**.</span><span class="sxs-lookup"><span data-stu-id="6298c-228">If this is hello first time you have run hello Storage Explorer, you will be prompted for hello **_Storage account name** and **Storage account key**.</span></span> <span data-ttu-id="6298c-229">Als u het eerder hebt uitgevoerd, gebruikt u Hallo **toevoegen** knop tooadd naam van een nieuw opslagaccount en de sleutel.</span><span class="sxs-lookup"><span data-stu-id="6298c-229">If you have run it before, use hello **Add** button tooadd a new storage account name and key.</span></span>

    <span data-ttu-id="6298c-230">Voer Hallo naam en sleutel voor Hallo storage-account die wordt gebruikt door uw HDInsight-cluster en selecteert u vervolgens **opslaan en openen**.</span><span class="sxs-lookup"><span data-stu-id="6298c-230">Enter hello name and key for hello storage account used by your HDInsight cluster and then select **SAVE & OPEN**.</span></span>

    ![HDI. AzureStorageExplorer][image-azure-storage-explorer]
2. <span data-ttu-id="6298c-232">Klik in de lijst van de Hallo van containers toohello links van Hallo interface, op Hallo-naam van Hallo-container die is gekoppeld aan uw HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6298c-232">In hello list of containers toohello left of hello interface, click hello name of hello container that is associated with your HDInsight cluster.</span></span> <span data-ttu-id="6298c-233">Standaard kunt dit Hallo-naam van Hallo HDInsight-cluster is, maar mogelijk anders als u een specifieke naam hebt ingevoerd bij het maken van Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="6298c-233">By default, this is hello name of hello HDInsight cluster, but may be different if you entered a specific name when creating hello cluster.</span></span>
3. <span data-ttu-id="6298c-234">Selecteer in de werkbalk hello, Hallo uploaden pictogram.</span><span class="sxs-lookup"><span data-stu-id="6298c-234">From hello tool bar, select hello upload icon.</span></span>

    ![Werkbalk met uploaden pictogram gemarkeerd](./media/hdinsight-upload-data/toolbar.png)
4. <span data-ttu-id="6298c-236">Geef een bestand tooupload en klik vervolgens op **Open**.</span><span class="sxs-lookup"><span data-stu-id="6298c-236">Specify a file tooupload, and then click **Open**.</span></span> <span data-ttu-id="6298c-237">Wanneer u wordt gevraagd, selecteert u **uploaden** tooupload Hallo bestand toohello hoofdmap van Hallo storage-container.</span><span class="sxs-lookup"><span data-stu-id="6298c-237">When prompted, select **Upload** tooupload hello file toohello root of hello storage container.</span></span> <span data-ttu-id="6298c-238">Als u wilt dat tooupload hello tooa specifieke bestandspad, voert u Hallo pad in Hallo **bestemming** veld en selecteer vervolgens **uploaden**.</span><span class="sxs-lookup"><span data-stu-id="6298c-238">If you want tooupload hello file tooa specific path, enter hello path in hello **Destination** field and then select **Upload**.</span></span>

    ![Bestand uploaden dialoogvenster](./media/hdinsight-upload-data/fileupload.png)

    <span data-ttu-id="6298c-240">Zodra het Hallo-bestand is klaar met uploaden, kunt u deze uit taken op Hallo HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="6298c-240">Once hello file has finished uploading, you can use it from jobs on hello HDInsight cluster.</span></span>

## <a name="mount-azure-blob-storage-as-local-drive"></a><span data-ttu-id="6298c-241">Azure Blob-opslag als lokale schijf koppelen</span><span class="sxs-lookup"><span data-stu-id="6298c-241">Mount Azure Blob Storage as Local Drive</span></span>
<span data-ttu-id="6298c-242">Zie [koppelpunt Azure Blob Storage als lokaal station](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span><span class="sxs-lookup"><span data-stu-id="6298c-242">See [Mount Azure Blob Storage as Local Drive](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span></span>

## <a name="services"></a><span data-ttu-id="6298c-243">Services</span><span class="sxs-lookup"><span data-stu-id="6298c-243">Services</span></span>
### <a name="azure-data-factory"></a><span data-ttu-id="6298c-244">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="6298c-244">Azure Data Factory</span></span>
<span data-ttu-id="6298c-245">Hello Azure Data Factory-service is een volledig beheerde service voor het opstellen van services voor opslag, verwerking van gegevens en gegevens gegevensverplaatsing in productie met gestroomlijnde, schaalbare en betrouwbare gegevenspijplijnen.</span><span class="sxs-lookup"><span data-stu-id="6298c-245">hello Azure Data Factory service is a fully managed service for composing data storage, data processing, and data movement services into streamlined, scalable, and reliable data production pipelines.</span></span>

<span data-ttu-id="6298c-246">Azure Data Factory kan gebruikte toomove gegevens in Azure Blob-opslag of toocreate gegevenspijplijnen dat rechtstreeks HDInsight functies zoals Hive en varkens.</span><span class="sxs-lookup"><span data-stu-id="6298c-246">Azure Data Factory can be used toomove data into Azure Blob storage, or toocreate data pipelines that directly use HDInsight features such as Hive and Pig.</span></span>

<span data-ttu-id="6298c-247">Zie voor meer informatie, Hallo [documentatie Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="6298c-247">For more information, see hello [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/).</span></span>

### <span data-ttu-id="6298c-248"><a id="sqoop"></a>Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="6298c-248"><a id="sqoop"></a>Apache Sqoop</span></span>
<span data-ttu-id="6298c-249">Sqoop is een hulpprogramma waarmee u tootransfer gegevens tussen Hadoop en relationele databases.</span><span class="sxs-lookup"><span data-stu-id="6298c-249">Sqoop is a tool designed tootransfer data between Hadoop and relational databases.</span></span> <span data-ttu-id="6298c-250">U kunt deze tooimport gegevens uit een relationele databasebeheersysteem (RDBMS), zoals SQL Server, MySQL of Oracle in Hallo Hadoop distributed file system (HDFS) gegevens in Hadoop met MapReduce of Hive Hallo transformeren en vervolgens exporteren Hallo gegevens terug in een RDBMS.</span><span class="sxs-lookup"><span data-stu-id="6298c-250">You can use it tooimport data from a relational database management system (RDBMS), such as SQL Server, MySQL, or Oracle into hello Hadoop distributed file system (HDFS), transform hello data in Hadoop with MapReduce or Hive, and then export hello data back into an RDBMS.</span></span>

<span data-ttu-id="6298c-251">Zie voor meer informatie [Sqoop gebruiken met HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="6298c-251">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

## <a name="development-sdks"></a><span data-ttu-id="6298c-252">Ontwikkeling van SDK 's</span><span class="sxs-lookup"><span data-stu-id="6298c-252">Development SDKs</span></span>
<span data-ttu-id="6298c-253">Azure Blob-opslag kan ook worden geopend met een Azure-SDK van Hallo programmeertalen te volgen:</span><span class="sxs-lookup"><span data-stu-id="6298c-253">Azure Blob storage can also be accessed using an Azure SDK from hello following programming languages:</span></span>

* <span data-ttu-id="6298c-254">.NET</span><span class="sxs-lookup"><span data-stu-id="6298c-254">.NET</span></span>
* <span data-ttu-id="6298c-255">Java</span><span class="sxs-lookup"><span data-stu-id="6298c-255">Java</span></span>
* <span data-ttu-id="6298c-256">Node.js</span><span class="sxs-lookup"><span data-stu-id="6298c-256">Node.js</span></span>
* <span data-ttu-id="6298c-257">PHP</span><span class="sxs-lookup"><span data-stu-id="6298c-257">PHP</span></span>
* <span data-ttu-id="6298c-258">Python</span><span class="sxs-lookup"><span data-stu-id="6298c-258">Python</span></span>
* <span data-ttu-id="6298c-259">Ruby</span><span class="sxs-lookup"><span data-stu-id="6298c-259">Ruby</span></span>

<span data-ttu-id="6298c-260">Zie voor meer informatie over het installeren van hello Azure-SDK's [Azure downloads](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="6298c-260">For more information on installing hello Azure SDKs, see [Azure downloads](https://azure.microsoft.com/downloads/)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="6298c-261">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="6298c-261">Troubleshooting</span></span>
### <span data-ttu-id="6298c-262"><a id="storageexception"></a>Uitzondering voor schrijven in blob Storage</span><span class="sxs-lookup"><span data-stu-id="6298c-262"><a id="storageexception"></a>Storage exception for write on blob</span></span>
<span data-ttu-id="6298c-263">**Symptomen**: bij gebruik van Hallo `hadoop` of `hdfs dfs` opdrachten toowrite bestanden die zijn ~ 12 GB of groter op een HBase-cluster kunnen Hallo volgende fout optreden:</span><span class="sxs-lookup"><span data-stu-id="6298c-263">**Symptoms**: When using hello `hadoop` or `hdfs dfs` commands toowrite files that are ~12GB or larger on an HBase cluster, you may encounter hello following error:</span></span>

    ERROR azure.NativeAzureFileSystem: Encountered Storage Exception for write on Blob : example/test_large_file.bin._COPYING_ Exception details: null Error Code : RequestBodyTooLarge
    copyFromLocal: java.io.IOException
            at com.microsoft.azure.storage.core.Utility.initIOException(Utility.java:661)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:366)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:350)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:471)
            at java.util.concurrent.FutureTask.run(FutureTask.java:262)
            at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
            at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
            at java.lang.Thread.run(Thread.java:745)
    Caused by: com.microsoft.azure.storage.StorageException: hello request body is too large and exceeds hello maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

<span data-ttu-id="6298c-264">**Oorzaak**: HBase op HDInsight-clusters standaard tooa blokgrootte van 256 KB bij het schrijven van tooAzure opslag.</span><span class="sxs-lookup"><span data-stu-id="6298c-264">**Cause**: HBase on HDInsight clusters default tooa block size of 256KB when writing tooAzure storage.</span></span> <span data-ttu-id="6298c-265">Terwijl dit voor HBase APIs of REST-API's werkt, het zal leiden tot een fout opgetreden bij het gebruik van Hallo `hadoop` of `hdfs dfs` opdrachtregelprogramma's.</span><span class="sxs-lookup"><span data-stu-id="6298c-265">While this works for HBase APIs or REST APIs, it will result in an error when using hello `hadoop` or `hdfs dfs` command-line utilities.</span></span>

<span data-ttu-id="6298c-266">**Resolutie**: Gebruik `fs.azure.write.request.size` toospecify een groter blok.</span><span class="sxs-lookup"><span data-stu-id="6298c-266">**Resolution**: Use `fs.azure.write.request.size` toospecify a larger block size.</span></span> <span data-ttu-id="6298c-267">U kunt dit doen op basis van per gebruik met behulp van Hallo `-D` parameter.</span><span class="sxs-lookup"><span data-stu-id="6298c-267">You can do this on a per-use basis by using hello `-D` parameter.</span></span> <span data-ttu-id="6298c-268">Hallo Hieronder volgt een voorbeeld met deze parameter Hello `hadoop` opdracht:</span><span class="sxs-lookup"><span data-stu-id="6298c-268">hello following is an example using this parameter with hello `hadoop` command:</span></span>

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

<span data-ttu-id="6298c-269">U kunt ook de waarde van Hallo vergroten `fs.azure.write.request.size` globaal via Ambari.</span><span class="sxs-lookup"><span data-stu-id="6298c-269">You can also increase hello value of `fs.azure.write.request.size` globally by using Ambari.</span></span> <span data-ttu-id="6298c-270">Hallo volgende stappen kunnen worden gebruikt toochange Hallo waarde in Hallo Ambari-Webgebruikersinterface:</span><span class="sxs-lookup"><span data-stu-id="6298c-270">hello following steps can be used toochange hello value in hello Ambari Web UI:</span></span>

1. <span data-ttu-id="6298c-271">Ga in uw browser toohello Ambari-Webgebruikersinterface voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="6298c-271">In your browser, go toohello Ambari Web UI for your cluster.</span></span> <span data-ttu-id="6298c-272">Dit is https://CLUSTERNAME.azurehdinsight.net, waarbij **CLUSTERNAME** Hallo-naam van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="6298c-272">This is https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of your cluster.</span></span>

    <span data-ttu-id="6298c-273">Voer desgevraagd Hallo beheerder naam en het wachtwoord voor Hallo-cluster.</span><span class="sxs-lookup"><span data-stu-id="6298c-273">When prompted, enter hello admin name and password for hello cluster.</span></span>
2. <span data-ttu-id="6298c-274">Selecteer in het Hallo-zijde van welkomstscherm links, **HDFS**, en selecteer vervolgens Hallo **Configs** tabblad.</span><span class="sxs-lookup"><span data-stu-id="6298c-274">From hello left side of hello screen, select **HDFS**, and then select hello **Configs** tab.</span></span>
3. <span data-ttu-id="6298c-275">In Hallo **Filter...**  veld `fs.azure.write.request.size`.</span><span class="sxs-lookup"><span data-stu-id="6298c-275">In hello **Filter...** field, enter `fs.azure.write.request.size`.</span></span> <span data-ttu-id="6298c-276">Hiermee wordt de Hallo veld en de huidige waarde in het midden van de Hallo van Hallo pagina weergegeven.</span><span class="sxs-lookup"><span data-stu-id="6298c-276">This will display hello field and current value in hello middle of hello page.</span></span>
4. <span data-ttu-id="6298c-277">Hallo-waarde van 262144 (256KB) toohello nieuwe waarde wijzigen.</span><span class="sxs-lookup"><span data-stu-id="6298c-277">Change hello value from 262144 (256KB) toohello new value.</span></span> <span data-ttu-id="6298c-278">Bijvoorbeeld: 4194304 (4MB).</span><span class="sxs-lookup"><span data-stu-id="6298c-278">For example, 4194304 (4MB).</span></span>

![Afbeelding van het Hallo-waarde via Ambari-Webgebruikersinterface wijzigen](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

<span data-ttu-id="6298c-280">Zie voor meer informatie over het gebruik van Ambari [beheren HDInsight-clusters met Ambari-Webgebruikersinterface Hallo](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="6298c-280">For more information on using Ambari, see [Manage HDInsight clusters using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6298c-281">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6298c-281">Next steps</span></span>
<span data-ttu-id="6298c-282">Nu dat u begrijpt hoe tooget gegevens in HDInsight, lees Hallo artikelen toolearn hoe na tooperform analyse:</span><span class="sxs-lookup"><span data-stu-id="6298c-282">Now that you understand how tooget data into HDInsight, read hello following articles toolearn how tooperform analysis:</span></span>

* <span data-ttu-id="6298c-283">[Aan de slag met Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="6298c-283">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="6298c-284">[Hadoop-taken programmatisch verzenden][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="6298c-284">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="6298c-285">[Hive gebruiken met HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="6298c-285">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="6298c-286">[Pig gebruiken met HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="6298c-286">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>

[azure-management-portal]: https://porta.azure.com
[azure-powershell]: http://msdn.microsoft.com/library/windowsazure/jj152841.aspx

[azure-storage-client-library]: /develop/net/how-to-guides/blob-storage/
[azure-create-storage-account]:../storage/common/storage-create-storage-account.md
[azure-azcopy-download]:../storage/common/storage-use-azcopy.md
[azure-azcopy]:../storage/common/storage-use-azcopy.md

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md

[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md

[sqldatabase-create-configure]: ../sql-database-create-configure.md

[apache-sqoop-guide]: http://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[azurecli]: ../cli-install-nodejs.md


[image-azure-storage-explorer]: ./media/hdinsight-upload-data/HDI.AzureStorageExplorer.png
[image-ase-addaccount]: ./media/hdinsight-upload-data/HDI.ASEAddAccount.png
[image-ase-blob]: ./media/hdinsight-upload-data/HDI.ASEBlob.png
