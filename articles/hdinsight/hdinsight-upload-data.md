---
title: Uploaden van gegevens voor Hadoop-taken in HDInsight | Microsoft Docs
description: Informatie over het uploaden en toegang tot gegevens voor Hadoop-taken in HDInsight met behulp van de Azure CLI, Azure Storage Explorer, Azure PowerShell, de opdrachtregel voor Hadoop of Sqoop.
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
ms.openlocfilehash: 6867f96c8ea0e31ed0e682cef48e7aa5e3f65f86
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="upload-data-for-hadoop-jobs-in-hdinsight"></a><span data-ttu-id="b951f-104">Upload gegevens voor Hadoop-taken in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b951f-104">Upload data for Hadoop jobs in HDInsight</span></span>
<span data-ttu-id="b951f-105">Azure HDInsight biedt een complete Hadoop distributed file system (HDFS) via Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="b951f-105">Azure HDInsight provides a full-featured Hadoop distributed file system (HDFS) over Azure Blob storage.</span></span> <span data-ttu-id="b951f-106">Het is bedoeld als een HDFS-uitbreiding een naadloze ervaring te bieden aan klanten.</span><span class="sxs-lookup"><span data-stu-id="b951f-106">It is designed as an HDFS extension to provide a seamless experience to customers.</span></span> <span data-ttu-id="b951f-107">Hiermee kunt de volledige set onderdelen in het Hadoop-ecosysteem werken rechtstreeks op de gegevens die Hiermee worden beheerd.</span><span class="sxs-lookup"><span data-stu-id="b951f-107">It enables the full set of components in the Hadoop ecosystem to operate directly on the data it manages.</span></span> <span data-ttu-id="b951f-108">Azure Blob storage en HDFS zijn afzonderlijke bestandssystemen die zijn geoptimaliseerd voor de opslag van gegevens en berekeningen van die gegevens.</span><span class="sxs-lookup"><span data-stu-id="b951f-108">Azure Blob storage and HDFS are distinct file systems that are optimized for storage of data and computations on that data.</span></span> <span data-ttu-id="b951f-109">Zie voor meer informatie over de voordelen van het gebruik van Azure Blob storage [Azure Blob storage gebruiken met HDInsight][hdinsight-storage].</span><span class="sxs-lookup"><span data-stu-id="b951f-109">For information about the benefits of using Azure Blob storage, see [Use Azure Blob storage with HDInsight][hdinsight-storage].</span></span>

<span data-ttu-id="b951f-110">**Vereisten**</span><span class="sxs-lookup"><span data-stu-id="b951f-110">**Prerequisites**</span></span>

<span data-ttu-id="b951f-111">Houd rekening met de volgende vereiste voordat u begint:</span><span class="sxs-lookup"><span data-stu-id="b951f-111">Note the following requirement before you begin:</span></span>

* <span data-ttu-id="b951f-112">Een Azure HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="b951f-112">An Azure HDInsight cluster.</span></span> <span data-ttu-id="b951f-113">Zie voor instructies [aan de slag met Azure HDInsight] [ hdinsight-get-started] of [HDInsight-clusters inrichten][hdinsight-provision].</span><span class="sxs-lookup"><span data-stu-id="b951f-113">For instructions, see [Get started with Azure HDInsight][hdinsight-get-started] or [Provision HDInsight clusters][hdinsight-provision].</span></span>

## <a name="why-blob-storage"></a><span data-ttu-id="b951f-114">Waarom blobopslag?</span><span class="sxs-lookup"><span data-stu-id="b951f-114">Why blob storage?</span></span>
<span data-ttu-id="b951f-115">Azure HDInsight-clusters worden doorgaans geïmplementeerd voor MapReduce-taken uitvoeren en de clusters zijn verwijderd nadat deze taken hebt voltooid.</span><span class="sxs-lookup"><span data-stu-id="b951f-115">Azure HDInsight clusters are typically deployed to run MapReduce jobs, and the clusters are dropped after these jobs complete.</span></span> <span data-ttu-id="b951f-116">Behouden van de gegevens in de HDFS zou clusters nadat berekeningen voltooid zijn een dure manier voor het opslaan van deze gegevens zijn.</span><span class="sxs-lookup"><span data-stu-id="b951f-116">Keeping the data in the HDFS clusters after computations are complete would be an expensive way to store this data.</span></span> <span data-ttu-id="b951f-117">Azure Blob storage is een maximaal beschikbare, sterk schaalbare, hoge capaciteit, lage kosten en deelbaar opslagoptie voor gegevens die moeten worden verwerkt met behulp van HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b951f-117">Azure Blob storage is a highly available, highly scalable, high capacity, low cost, and shareable storage option for data that is to be processed using HDInsight.</span></span> <span data-ttu-id="b951f-118">Opslaan van gegevens in een blob, kunt de HDInsight-clusters die worden gebruikt voor berekeningen, veilig zonder verlies van gegevens worden vrijgegeven.</span><span class="sxs-lookup"><span data-stu-id="b951f-118">Storing data in a blob enables the HDInsight clusters that are used for computation to be safely released without losing data.</span></span>

### <a name="directories"></a><span data-ttu-id="b951f-119">Mappen</span><span class="sxs-lookup"><span data-stu-id="b951f-119">Directories</span></span>
<span data-ttu-id="b951f-120">Azure Blob storage-containers opslaan van gegevens als sleutel-waardeparen en er is geen maphiërarchie.</span><span class="sxs-lookup"><span data-stu-id="b951f-120">Azure Blob storage containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="b951f-121">Maar het teken '/' worden gebruikt binnen de sleutelnaam zodat het lijkt alsof een bestand wordt opgeslagen in een mapstructuur.</span><span class="sxs-lookup"><span data-stu-id="b951f-121">However the "/" character can be used within the key name to make it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="b951f-122">HDInsight ziet deze alsof het werkelijke mappen.</span><span class="sxs-lookup"><span data-stu-id="b951f-122">HDInsight sees these as if they are actual directories.</span></span>

<span data-ttu-id="b951f-123">De sleutel van de blob kan bijvoorbeeld *input/log1.txt* zijn.</span><span class="sxs-lookup"><span data-stu-id="b951f-123">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="b951f-124">Geen daadwerkelijke 'invoer' map bestaat, maar vanwege de aanwezigheid van het teken '/' in de naam van de sleutel heeft de vormgeving van een bestandspad.</span><span class="sxs-lookup"><span data-stu-id="b951f-124">No actual "input" directory exists, but due to the presence of the "/" character in the key name, it has the appearance of a file path.</span></span>

<span data-ttu-id="b951f-125">Als gevolg hiervan, als u Azure Explorer hulpprogramma merkt u bepaalde bestanden 0 bytes.</span><span class="sxs-lookup"><span data-stu-id="b951f-125">Because of this, if you use Azure Explorer tools you may notice some 0 byte files.</span></span> <span data-ttu-id="b951f-126">Deze bestanden een tweeledig doel:</span><span class="sxs-lookup"><span data-stu-id="b951f-126">These files serve two purposes:</span></span>

* <span data-ttu-id="b951f-127">Als er lege mappen, worden ze gemarkeerd van het bestaan van de map.</span><span class="sxs-lookup"><span data-stu-id="b951f-127">If there are empty folders, they mark of the existence of the folder.</span></span> <span data-ttu-id="b951f-128">Azure Blob-opslag is slimme om te weten dat als een blob foo/balk aangeroepen bestaat, er een map met de naam is **foo**.</span><span class="sxs-lookup"><span data-stu-id="b951f-128">Azure Blob storage is clever enough to know that if a blob called foo/bar exists, there is a folder called **foo**.</span></span> <span data-ttu-id="b951f-129">Maar de enige manier om een lege map geven aangeroepen **foo** is door in plaats dit bestand speciale 0 bytes.</span><span class="sxs-lookup"><span data-stu-id="b951f-129">But the only way to signify an empty folder called **foo** is by having this special 0 byte file in place.</span></span>
* <span data-ttu-id="b951f-130">Ze hebben speciale metagegevens die nodig is voor het Hadoop-bestandssysteem, met name de machtigingen en eigenaars voor de mappen.</span><span class="sxs-lookup"><span data-stu-id="b951f-130">They hold special metadata that is needed by the Hadoop file system, notably the permissions and owners for the folders.</span></span>

## <a name="command-line-utilities"></a><span data-ttu-id="b951f-131">Opdrachtregelprogramma 's</span><span class="sxs-lookup"><span data-stu-id="b951f-131">Command-line utilities</span></span>
<span data-ttu-id="b951f-132">Microsoft biedt de volgende hulpprogramma's om te werken met Azure Blob storage:</span><span class="sxs-lookup"><span data-stu-id="b951f-132">Microsoft provides the following utilities to work with Azure Blob storage:</span></span>

| <span data-ttu-id="b951f-133">Hulpprogramma</span><span class="sxs-lookup"><span data-stu-id="b951f-133">Tool</span></span> | <span data-ttu-id="b951f-134">Linux</span><span class="sxs-lookup"><span data-stu-id="b951f-134">Linux</span></span> | <span data-ttu-id="b951f-135">OS X</span><span class="sxs-lookup"><span data-stu-id="b951f-135">OS X</span></span> | <span data-ttu-id="b951f-136">Windows</span><span class="sxs-lookup"><span data-stu-id="b951f-136">Windows</span></span> |
| --- |:---:|:---:|:---:|
| <span data-ttu-id="b951f-137">[Azure-opdrachtregelinterface][azurecli]</span><span class="sxs-lookup"><span data-stu-id="b951f-137">[Azure Command-Line Interface][azurecli]</span></span> |<span data-ttu-id="b951f-138">✔</span><span class="sxs-lookup"><span data-stu-id="b951f-138">✔</span></span> |<span data-ttu-id="b951f-139">✔</span><span class="sxs-lookup"><span data-stu-id="b951f-139">✔</span></span> |<span data-ttu-id="b951f-140">✔</span><span class="sxs-lookup"><span data-stu-id="b951f-140">✔</span></span> |
| <span data-ttu-id="b951f-141">[Azure PowerShell][azure-powershell]</span><span class="sxs-lookup"><span data-stu-id="b951f-141">[Azure PowerShell][azure-powershell]</span></span> | | |<span data-ttu-id="b951f-142">✔</span><span class="sxs-lookup"><span data-stu-id="b951f-142">✔</span></span> |
| <span data-ttu-id="b951f-143">[AzCopy][azure-azcopy]</span><span class="sxs-lookup"><span data-stu-id="b951f-143">[AzCopy][azure-azcopy]</span></span> | | |<span data-ttu-id="b951f-144">✔</span><span class="sxs-lookup"><span data-stu-id="b951f-144">✔</span></span> |
| [<span data-ttu-id="b951f-145">Hadoop-opdracht</span><span class="sxs-lookup"><span data-stu-id="b951f-145">Hadoop command</span></span>](#commandline) |<span data-ttu-id="b951f-146">✔</span><span class="sxs-lookup"><span data-stu-id="b951f-146">✔</span></span> |<span data-ttu-id="b951f-147">✔</span><span class="sxs-lookup"><span data-stu-id="b951f-147">✔</span></span> |<span data-ttu-id="b951f-148">✔</span><span class="sxs-lookup"><span data-stu-id="b951f-148">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="b951f-149">Terwijl de Azure CLI, Azure PowerShell en AzCopy alle kunnen worden gebruikt vanuit buiten Azure, het Hadoop-opdracht is alleen beschikbaar op het HDInsight-cluster en kunt alleen het laden van gegevens uit het lokale bestandssysteem in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="b951f-149">While the Azure CLI, Azure PowerShell, and AzCopy can all be used from outside Azure, the Hadoop command is only available on the HDInsight cluster and only allows loading data from the local file system into Azure Blob storage.</span></span>
>
>

### <span data-ttu-id="b951f-150"><a id="xplatcli"></a>Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b951f-150"><a id="xplatcli"></a>Azure CLI</span></span>
<span data-ttu-id="b951f-151">De Azure CLI is een hulpprogramma voor meerdere platforms waarmee u voor het beheren van Azure-services.</span><span class="sxs-lookup"><span data-stu-id="b951f-151">The Azure CLI is a cross-platform tool that allows you to manage Azure services.</span></span> <span data-ttu-id="b951f-152">Gebruik de volgende stappen uit om gegevens te uploaden naar Azure Blob-opslag:</span><span class="sxs-lookup"><span data-stu-id="b951f-152">Use the following steps to upload data to Azure Blob storage:</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

1. <span data-ttu-id="b951f-153">[Installeren en configureren van de Azure CLI voor Mac, Linux en Windows](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="b951f-153">[Install and configure the Azure CLI for Mac, Linux and Windows](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="b951f-154">Open een opdrachtprompt, bash of andere shell en gebruik het volgende bij de verificatie voor uw Azure-abonnement.</span><span class="sxs-lookup"><span data-stu-id="b951f-154">Open a command prompt, bash, or other shell, and use the following to authenticate to your Azure subscription.</span></span>

        azure login

    <span data-ttu-id="b951f-155">Wanneer u wordt gevraagd, typt u de gebruikersnaam en het wachtwoord voor uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="b951f-155">When prompted, enter the user name and password for your subscription.</span></span>
3. <span data-ttu-id="b951f-156">Voer de volgende opdracht voor een lijst met de storage-accounts voor uw abonnement:</span><span class="sxs-lookup"><span data-stu-id="b951f-156">Enter the following command to list the storage accounts for your subscription:</span></span>

        azure storage account list
4. <span data-ttu-id="b951f-157">Selecteer het opslagaccount met de blob die u werken wilt met en gebruik de volgende opdracht voor het ophalen van de sleutel voor dit account:</span><span class="sxs-lookup"><span data-stu-id="b951f-157">Select the storage account that contains the blob you want to work with, then use the following command to retrieve the key for this account:</span></span>

        azure storage account keys list <storage-account-name>

    <span data-ttu-id="b951f-158">Dit moet retourneren **primaire** en **secundaire** sleutels.</span><span class="sxs-lookup"><span data-stu-id="b951f-158">This should return **Primary** and **Secondary** keys.</span></span> <span data-ttu-id="b951f-159">Kopieer de **primaire** sleutelwaarde omdat deze wordt gebruikt in de volgende stappen.</span><span class="sxs-lookup"><span data-stu-id="b951f-159">Copy the **Primary** key value because it will be used in the next steps.</span></span>
5. <span data-ttu-id="b951f-160">Gebruik de volgende opdracht voor het ophalen van een lijst met blobcontainers in het opslagaccount:</span><span class="sxs-lookup"><span data-stu-id="b951f-160">Use the following command to retrieve a list of blob containers within the storage account:</span></span>

        azure storage container list -a <storage-account-name> -k <primary-key>
6. <span data-ttu-id="b951f-161">Gebruik de volgende opdrachten om te uploaden en downloaden van bestanden naar de blob:</span><span class="sxs-lookup"><span data-stu-id="b951f-161">Use the following commands to upload and download files to the blob:</span></span>

   * <span data-ttu-id="b951f-162">Een bestand te uploaden:</span><span class="sxs-lookup"><span data-stu-id="b951f-162">To upload a file:</span></span>

           azure storage blob upload -a <storage-account-name> -k <primary-key> <source-file> <container-name> <blob-name>
   * <span data-ttu-id="b951f-163">Een bestand te downloaden:</span><span class="sxs-lookup"><span data-stu-id="b951f-163">To download a file:</span></span>

           azure storage blob download -a <storage-account-name> -k <primary-key> <container-name> <blob-name> <destination-file>

> [!NOTE]
> <span data-ttu-id="b951f-164">Als u altijd met hetzelfde opslagaccount gebruikt werkt, kunt u de volgende omgevingsvariabelen in plaats van het account en sleutel voor elke opdracht:</span><span class="sxs-lookup"><span data-stu-id="b951f-164">If you will always be working with the same storage account, you can set the following environment variables instead of specifying the account and key for every command:</span></span>
>
> * <span data-ttu-id="b951f-165">**AZURE\_opslag\_ACCOUNT**: naam van het opslagaccount</span><span class="sxs-lookup"><span data-stu-id="b951f-165">**AZURE\_STORAGE\_ACCOUNT**: The storage account name</span></span>
> * <span data-ttu-id="b951f-166">**AZURE\_opslag\_toegang\_sleutel**: de sleutel van het opslagaccount</span><span class="sxs-lookup"><span data-stu-id="b951f-166">**AZURE\_STORAGE\_ACCESS\_KEY**: The storage account key</span></span>
>
>

### <span data-ttu-id="b951f-167"><a id="powershell"></a>Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b951f-167"><a id="powershell"></a>Azure PowerShell</span></span>
<span data-ttu-id="b951f-168">Azure PowerShell is een scriptomgeving op servers die u gebruiken kunt om te beheren en de implementatie en beheer van uw workloads in Azure automatiseren.</span><span class="sxs-lookup"><span data-stu-id="b951f-168">Azure PowerShell is a scripting environment that you can use to control and automate the deployment and management of your workloads in Azure.</span></span> <span data-ttu-id="b951f-169">Zie voor meer informatie over het configureren van uw werkstation om uit te voeren van Azure PowerShell [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b951f-169">For information about configuring your workstation to run Azure PowerShell, see [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-powershell.md)]

<span data-ttu-id="b951f-170">**Een lokaal bestand uploaden naar Azure Blob-opslag**</span><span class="sxs-lookup"><span data-stu-id="b951f-170">**To upload a local file to Azure Blob storage**</span></span>

1. <span data-ttu-id="b951f-171">Open de Azure PowerShell-console volgens de instructies in [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b951f-171">Open the Azure PowerShell console as instructed in [Install and configure Azure PowerShell](/powershell/azure/overview).</span></span>
2. <span data-ttu-id="b951f-172">Stel de waarden van de eerste vijf variabelen in het volgende script:</span><span class="sxs-lookup"><span data-stu-id="b951f-172">Set the values of the first five variables in the following script:</span></span>

        $resourceGroupName = "<AzureResourceGroupName>"
        $storageAccountName = "<StorageAccountName>"
        $containerName = "<ContainerName>"

        $fileName ="<LocalFileName>"
        $blobName = "<BlobName>"

        # Get the storage account key
        $storageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName)[0].Value
        # Create the storage context object
        $destContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageaccountkey

        # Copy the file from local workstation to the Blob container
        Set-AzureStorageBlobContent -File $fileName -Container $containerName -Blob $blobName -context $destContext
3. <span data-ttu-id="b951f-173">Plak het script in de Azure PowerShell-console uit te voeren om het bestand te kopiëren.</span><span class="sxs-lookup"><span data-stu-id="b951f-173">Paste the script into the Azure PowerShell console to run it to copy the file.</span></span>

<span data-ttu-id="b951f-174">Bijvoorbeeld de PowerShell-scripts die zijn gemaakt om te werken met HDInsight, Zie [HDInsight tools](https://github.com/blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="b951f-174">For example PowerShell scripts created to work with HDInsight, see [HDInsight tools](https://github.com/blackmist/hdinsight-tools).</span></span>

### <span data-ttu-id="b951f-175"><a id="azcopy"></a>AzCopy</span><span class="sxs-lookup"><span data-stu-id="b951f-175"><a id="azcopy"></a>AzCopy</span></span>
<span data-ttu-id="b951f-176">AzCopy is een opdrachtregelprogramma dat is ontworpen voor het vereenvoudigen van de taak van de overdracht van gegevens naar en van een Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="b951f-176">AzCopy is a command-line tool that is designed to simplify the task of transferring data into and out of an Azure Storage account.</span></span> <span data-ttu-id="b951f-177">U kunt gebruiken als een zelfstandige tool of gebruikmaken van dit hulpprogramma in een bestaande toepassing.</span><span class="sxs-lookup"><span data-stu-id="b951f-177">You can use it as a standalone tool or incorporate this tool in an existing application.</span></span> <span data-ttu-id="b951f-178">[Downloaden van AzCopy][azure-azcopy-download].</span><span class="sxs-lookup"><span data-stu-id="b951f-178">[Download AzCopy][azure-azcopy-download].</span></span>

<span data-ttu-id="b951f-179">De syntaxis van AzCopy is:</span><span class="sxs-lookup"><span data-stu-id="b951f-179">The AzCopy syntax is:</span></span>

    AzCopy <Source> <Destination> [filePattern [filePattern...]] [Options]

<span data-ttu-id="b951f-180">Zie voor meer informatie [AzCopy - bestanden voor Azure Blobs uploaden/downloaden][azure-azcopy].</span><span class="sxs-lookup"><span data-stu-id="b951f-180">For more information, see [AzCopy - Uploading/Downloading files for Azure Blobs][azure-azcopy].</span></span>

### <span data-ttu-id="b951f-181"><a id="commandline"></a>Hadoop-opdrachtregel</span><span class="sxs-lookup"><span data-stu-id="b951f-181"><a id="commandline"></a>Hadoop command line</span></span>
<span data-ttu-id="b951f-182">De Hadoop-opdrachtregel is alleen nuttig voor het opslaan van gegevens naar de blobopslag, wanneer de gegevens al aanwezig op het hoofdknooppunt van het cluster is.</span><span class="sxs-lookup"><span data-stu-id="b951f-182">The Hadoop command line is only useful for storing data into blob storage when the data is already present on the cluster head node.</span></span>

<span data-ttu-id="b951f-183">Om de Hadoop-opdracht gebruikt, moet u eerst verbinding maken met de headnode met behulp van een van de volgende methoden:</span><span class="sxs-lookup"><span data-stu-id="b951f-183">In order to use the Hadoop command, you must first connect to the headnode using one of the following methods:</span></span>

* <span data-ttu-id="b951f-184">**HDInsight op basis van Windows**: [verbinding maken met behulp van extern bureaublad](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span><span class="sxs-lookup"><span data-stu-id="b951f-184">**Windows-based HDInsight**: [Connect using Remote Desktop](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)</span></span>
* <span data-ttu-id="b951f-185">**HDInsight op basis van Linux**: verbinding maken met behulp van SSH ([de SSH-opdracht](hdinsight-hadoop-linux-use-ssh-unix.md) of [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span><span class="sxs-lookup"><span data-stu-id="b951f-185">**Linux-based HDInsight**: Connect using SSH ([the SSH command](hdinsight-hadoop-linux-use-ssh-unix.md) or [PuTTY](hdinsight-hadoop-linux-use-ssh-windows.md))</span></span>

<span data-ttu-id="b951f-186">Eenmaal zijn verbonden, kunt u de volgende syntaxis voor het uploaden van een bestand naar de opslag.</span><span class="sxs-lookup"><span data-stu-id="b951f-186">Once connected, you can use the following syntax to upload a file to storage.</span></span>

    hadoop -copyFromLocal <localFilePath> <storageFilePath>

<span data-ttu-id="b951f-187">Bijvoorbeeld: `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span><span class="sxs-lookup"><span data-stu-id="b951f-187">For example, `hadoop fs -copyFromLocal data.txt /example/data/data.txt`</span></span>

<span data-ttu-id="b951f-188">Omdat het standaardbestandssysteem voor HDInsight in Azure Blob-opslag, zich /example/data.txt in Azure Blob-opslag.</span><span class="sxs-lookup"><span data-stu-id="b951f-188">Because the default file system for HDInsight is in Azure Blob storage, /example/data.txt is actually in Azure Blob storage.</span></span> <span data-ttu-id="b951f-189">U kunt ook verwijzen naar het bestand als:</span><span class="sxs-lookup"><span data-stu-id="b951f-189">You can also refer to the file as:</span></span>

    wasb:///example/data/data.txt

<span data-ttu-id="b951f-190">of</span><span class="sxs-lookup"><span data-stu-id="b951f-190">or</span></span>

    wasb://<ContainerName>@<StorageAccountName>.blob.core.windows.net/example/data/davinci.txt

<span data-ttu-id="b951f-191">Zie voor een lijst met andere Hadoop die werken met bestanden opdrachten, [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span><span class="sxs-lookup"><span data-stu-id="b951f-191">For a list of other Hadoop commands that work with files, see [http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html](http://hadoop.apache.org/docs/r2.7.0/hadoop-project-dist/hadoop-common/FileSystemShell.html)</span></span>

> [!WARNING]
> <span data-ttu-id="b951f-192">Op de HBase-clusters standaard blokgrootte gebruikt bij het schrijven van gegevens is 256KB.</span><span class="sxs-lookup"><span data-stu-id="b951f-192">On HBase clusters, the default block size used when writing data is 256KB.</span></span> <span data-ttu-id="b951f-193">Hoewel dit goed met HBase APIs of REST-API's werkt, gebruiken de `hadoop` of `hdfs dfs` opdrachten voor het schrijven van gegevens is groter dan ~ 12 GB in een fout resulteert.</span><span class="sxs-lookup"><span data-stu-id="b951f-193">While this works fine when using HBase APIs or REST APIs, using the `hadoop` or `hdfs dfs` commands to write data larger than ~12GB results in an error.</span></span> <span data-ttu-id="b951f-194">Zie de [uitzondering om te schrijven op blob storage](#storageexception) sectie hieronder voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="b951f-194">See the [storage exception for write on blob](#storageexception) section below for more information.</span></span>
>
>

## <a name="graphical-clients"></a><span data-ttu-id="b951f-195">Grafische clients</span><span class="sxs-lookup"><span data-stu-id="b951f-195">Graphical clients</span></span>
<span data-ttu-id="b951f-196">Er zijn ook enkele toepassingen die een grafische interface bieden voor het werken met Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="b951f-196">There are also several applications that provide a graphical interface for working with Azure Storage.</span></span> <span data-ttu-id="b951f-197">Hier volgt een lijst met enkele van deze toepassingen:</span><span class="sxs-lookup"><span data-stu-id="b951f-197">The following is a list of a few of these applications:</span></span>

| <span data-ttu-id="b951f-198">Client</span><span class="sxs-lookup"><span data-stu-id="b951f-198">Client</span></span> | <span data-ttu-id="b951f-199">Linux</span><span class="sxs-lookup"><span data-stu-id="b951f-199">Linux</span></span> | <span data-ttu-id="b951f-200">OS X</span><span class="sxs-lookup"><span data-stu-id="b951f-200">OS X</span></span> | <span data-ttu-id="b951f-201">Windows</span><span class="sxs-lookup"><span data-stu-id="b951f-201">Windows</span></span> |
| --- |:---:|:---:|:---:|
| [<span data-ttu-id="b951f-202">Microsoft Visual Studio-hulpprogramma's voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="b951f-202">Microsoft Visual Studio Tools for HDInsight</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources) |<span data-ttu-id="b951f-203">✔</span><span class="sxs-lookup"><span data-stu-id="b951f-203">✔</span></span> |<span data-ttu-id="b951f-204">✔</span><span class="sxs-lookup"><span data-stu-id="b951f-204">✔</span></span> |<span data-ttu-id="b951f-205">✔</span><span class="sxs-lookup"><span data-stu-id="b951f-205">✔</span></span> |
| [<span data-ttu-id="b951f-206">Azure-opslagverkenner</span><span class="sxs-lookup"><span data-stu-id="b951f-206">Azure Storage Explorer</span></span>](http://storageexplorer.com/) |<span data-ttu-id="b951f-207">✔</span><span class="sxs-lookup"><span data-stu-id="b951f-207">✔</span></span> |<span data-ttu-id="b951f-208">✔</span><span class="sxs-lookup"><span data-stu-id="b951f-208">✔</span></span> |<span data-ttu-id="b951f-209">✔</span><span class="sxs-lookup"><span data-stu-id="b951f-209">✔</span></span> |
| [<span data-ttu-id="b951f-210">Cloud-opslag Studio 2</span><span class="sxs-lookup"><span data-stu-id="b951f-210">Cloud Storage Studio 2</span></span>](http://www.cerebrata.com/Products/CloudStorageStudio/) | | |<span data-ttu-id="b951f-211">✔</span><span class="sxs-lookup"><span data-stu-id="b951f-211">✔</span></span> |
| [<span data-ttu-id="b951f-212">CloudXplorer</span><span class="sxs-lookup"><span data-stu-id="b951f-212">CloudXplorer</span></span>](http://clumsyleaf.com/products/cloudxplorer) | | |<span data-ttu-id="b951f-213">✔</span><span class="sxs-lookup"><span data-stu-id="b951f-213">✔</span></span> |
| [<span data-ttu-id="b951f-214">Azure Explorer</span><span class="sxs-lookup"><span data-stu-id="b951f-214">Azure Explorer</span></span>](http://www.cloudberrylab.com/free-microsoft-azure-explorer.aspx) | | |<span data-ttu-id="b951f-215">✔</span><span class="sxs-lookup"><span data-stu-id="b951f-215">✔</span></span> |
| [<span data-ttu-id="b951f-216">Cyberduck</span><span class="sxs-lookup"><span data-stu-id="b951f-216">Cyberduck</span></span>](https://cyberduck.io/) | |<span data-ttu-id="b951f-217">✔</span><span class="sxs-lookup"><span data-stu-id="b951f-217">✔</span></span> |<span data-ttu-id="b951f-218">✔</span><span class="sxs-lookup"><span data-stu-id="b951f-218">✔</span></span> |

### <a name="visual-studio-tools-for-hdinsight"></a><span data-ttu-id="b951f-219">Visual Studio-hulpprogramma's voor HDInsight</span><span class="sxs-lookup"><span data-stu-id="b951f-219">Visual Studio Tools for HDInsight</span></span>
<span data-ttu-id="b951f-220">Zie voor meer informatie [de gekoppelde resources navigeren](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span><span class="sxs-lookup"><span data-stu-id="b951f-220">For more information, see [Navigate the linked resources](hdinsight-hadoop-visual-studio-tools-get-started.md#navigate-the-linked-resources).</span></span>

### <span data-ttu-id="b951f-221"><a id="storageexplorer"></a>Azure Opslagverkenner</span><span class="sxs-lookup"><span data-stu-id="b951f-221"><a id="storageexplorer"></a>Azure Storage Explorer</span></span>
<span data-ttu-id="b951f-222">*Azure Storage Explorer* is een nuttig hulpmiddel om te bekijken en wijzigen van de gegevens in BLOB's.</span><span class="sxs-lookup"><span data-stu-id="b951f-222">*Azure Storage Explorer* is a useful tool for inspecting and altering the data in blobs.</span></span> <span data-ttu-id="b951f-223">Het is een gratis, open source-hulpprogramma dat kan worden gedownload vanaf [http://storageexplorer.com/](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="b951f-223">It is a free, open source tool that can be downloaded from [http://storageexplorer.com/](http://storageexplorer.com/).</span></span> <span data-ttu-id="b951f-224">De broncode is beschikbaar via deze koppeling ook.</span><span class="sxs-lookup"><span data-stu-id="b951f-224">The source code is available from this link as well.</span></span>

<span data-ttu-id="b951f-225">Voordat u het hulpprogramma gebruikt, moet u weten Azure naam en sleutel van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="b951f-225">Before using the tool, you must know your Azure storage account name and account key.</span></span> <span data-ttu-id="b951f-226">Zie voor instructies over het ophalen van deze informatie de ' How to: toegangssleutels voor opslag weergeven, kopiëren en opnieuw genereren ' sectie van [maken, beheren of verwijderen van een opslagaccount][azure-create-storage-account].</span><span class="sxs-lookup"><span data-stu-id="b951f-226">For instructions about getting this information, see the "How to: View, copy and regenerate storage access keys" section of [Create, manage, or delete a storage account][azure-create-storage-account].</span></span>

1. <span data-ttu-id="b951f-227">Azure Storage Explorer uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="b951f-227">Run Azure Storage Explorer.</span></span> <span data-ttu-id="b951f-228">Als dit de eerste keer dat u Opslagverkenner hebt uitgevoerd, wordt u gevraagd om de **_Storage accountnaam** en **opslagaccountsleutel**.</span><span class="sxs-lookup"><span data-stu-id="b951f-228">If this is the first time you have run the Storage Explorer, you will be prompted for the **_Storage account name** and **Storage account key**.</span></span> <span data-ttu-id="b951f-229">Als u het eerder hebt uitgevoerd, gebruikt u de **toevoegen** om toe te voegen een naam van nieuw opslagaccount en de sleutel.</span><span class="sxs-lookup"><span data-stu-id="b951f-229">If you have run it before, use the **Add** button to add a new storage account name and key.</span></span>

    <span data-ttu-id="b951f-230">Voer de naam en sleutel voor het opslagaccount door uw HDInsight-cluster gebruikt en selecteer vervolgens **opslaan en openen**.</span><span class="sxs-lookup"><span data-stu-id="b951f-230">Enter the name and key for the storage account used by your HDInsight cluster and then select **SAVE & OPEN**.</span></span>

    ![HDI. AzureStorageExplorer][image-azure-storage-explorer]
2. <span data-ttu-id="b951f-232">Klik op de naam van de container die is gekoppeld aan uw HDInsight-cluster in de lijst van containers naar links van de interface.</span><span class="sxs-lookup"><span data-stu-id="b951f-232">In the list of containers to the left of the interface, click the name of the container that is associated with your HDInsight cluster.</span></span> <span data-ttu-id="b951f-233">Standaard, dit is de naam van het HDInsight-cluster, maar mogelijk anders als u een specifieke naam hebt ingevoerd bij het maken van het cluster.</span><span class="sxs-lookup"><span data-stu-id="b951f-233">By default, this is the name of the HDInsight cluster, but may be different if you entered a specific name when creating the cluster.</span></span>
3. <span data-ttu-id="b951f-234">Selecteer het pictogram voor het uploaden van de werkbalk.</span><span class="sxs-lookup"><span data-stu-id="b951f-234">From the tool bar, select the upload icon.</span></span>

    ![Werkbalk met uploaden pictogram gemarkeerd](./media/hdinsight-upload-data/toolbar.png)
4. <span data-ttu-id="b951f-236">Geef een bestand om te uploaden en klik vervolgens op **Open**.</span><span class="sxs-lookup"><span data-stu-id="b951f-236">Specify a file to upload, and then click **Open**.</span></span> <span data-ttu-id="b951f-237">Wanneer u wordt gevraagd, selecteert u **uploaden** het bestand te uploaden naar de hoofdmap van de storage-container.</span><span class="sxs-lookup"><span data-stu-id="b951f-237">When prompted, select **Upload** to upload the file to the root of the storage container.</span></span> <span data-ttu-id="b951f-238">Als u het bestand te uploaden naar een specifiek pad wilt, voert u het pad in de **bestemming** veld en selecteer vervolgens **uploaden**.</span><span class="sxs-lookup"><span data-stu-id="b951f-238">If you want to upload the file to a specific path, enter the path in the **Destination** field and then select **Upload**.</span></span>

    ![Bestand uploaden dialoogvenster](./media/hdinsight-upload-data/fileupload.png)

    <span data-ttu-id="b951f-240">Zodra het bestand is klaar met uploaden, kunt u deze uit taken op het HDInsight-cluster.</span><span class="sxs-lookup"><span data-stu-id="b951f-240">Once the file has finished uploading, you can use it from jobs on the HDInsight cluster.</span></span>

## <a name="mount-azure-blob-storage-as-local-drive"></a><span data-ttu-id="b951f-241">Azure Blob-opslag als lokale schijf koppelen</span><span class="sxs-lookup"><span data-stu-id="b951f-241">Mount Azure Blob Storage as Local Drive</span></span>
<span data-ttu-id="b951f-242">Zie [koppelpunt Azure Blob Storage als lokaal station](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span><span class="sxs-lookup"><span data-stu-id="b951f-242">See [Mount Azure Blob Storage as Local Drive](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/09/mount-azure-blob-storage-as-local-drive.aspx).</span></span>

## <a name="services"></a><span data-ttu-id="b951f-243">Services</span><span class="sxs-lookup"><span data-stu-id="b951f-243">Services</span></span>
### <a name="azure-data-factory"></a><span data-ttu-id="b951f-244">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="b951f-244">Azure Data Factory</span></span>
<span data-ttu-id="b951f-245">De Azure Data Factory-service is een volledig beheerde service voor het opstellen van services voor opslag, verwerking van gegevens en gegevens gegevensverplaatsing in productie met gestroomlijnde, schaalbare en betrouwbare gegevenspijplijnen.</span><span class="sxs-lookup"><span data-stu-id="b951f-245">The Azure Data Factory service is a fully managed service for composing data storage, data processing, and data movement services into streamlined, scalable, and reliable data production pipelines.</span></span>

<span data-ttu-id="b951f-246">Azure Data Factory kan worden gebruikt om gegevens te verplaatsen naar de Azure Blob-opslag of gegevenspijplijnen die gebruikmaken van HDInsight-functies zoals Hive en Pig rechtstreeks te maken.</span><span class="sxs-lookup"><span data-stu-id="b951f-246">Azure Data Factory can be used to move data into Azure Blob storage, or to create data pipelines that directly use HDInsight features such as Hive and Pig.</span></span>

<span data-ttu-id="b951f-247">Zie voor meer informatie de [documentatie Azure Data Factory](https://azure.microsoft.com/documentation/services/data-factory/).</span><span class="sxs-lookup"><span data-stu-id="b951f-247">For more information, see the [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/).</span></span>

### <span data-ttu-id="b951f-248"><a id="sqoop"></a>Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="b951f-248"><a id="sqoop"></a>Apache Sqoop</span></span>
<span data-ttu-id="b951f-249">Sqoop is een hulpprogramma waarmee gegevens worden overgebracht tussen Hadoop en relationele databases.</span><span class="sxs-lookup"><span data-stu-id="b951f-249">Sqoop is a tool designed to transfer data between Hadoop and relational databases.</span></span> <span data-ttu-id="b951f-250">U kunt deze gebruiken om gegevens te importeren uit een relationele databasebeheersysteem (RDBMS), zoals SQL Server, MySQL of Oracle in het Hadoop distributed file system (HDFS), de gegevens in Hadoop met MapReduce of Hive transformeren en de gegevens vervolgens exporteren naar een RDBMS.</span><span class="sxs-lookup"><span data-stu-id="b951f-250">You can use it to import data from a relational database management system (RDBMS), such as SQL Server, MySQL, or Oracle into the Hadoop distributed file system (HDFS), transform the data in Hadoop with MapReduce or Hive, and then export the data back into an RDBMS.</span></span>

<span data-ttu-id="b951f-251">Zie voor meer informatie [Sqoop gebruiken met HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="b951f-251">For more information, see [Use Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

## <a name="development-sdks"></a><span data-ttu-id="b951f-252">Ontwikkeling van SDK 's</span><span class="sxs-lookup"><span data-stu-id="b951f-252">Development SDKs</span></span>
<span data-ttu-id="b951f-253">Azure Blob-opslag kan ook worden geopend met een Azure-SDK van de volgende programmeertalen:</span><span class="sxs-lookup"><span data-stu-id="b951f-253">Azure Blob storage can also be accessed using an Azure SDK from the following programming languages:</span></span>

* <span data-ttu-id="b951f-254">.NET</span><span class="sxs-lookup"><span data-stu-id="b951f-254">.NET</span></span>
* <span data-ttu-id="b951f-255">Java</span><span class="sxs-lookup"><span data-stu-id="b951f-255">Java</span></span>
* <span data-ttu-id="b951f-256">Node.js</span><span class="sxs-lookup"><span data-stu-id="b951f-256">Node.js</span></span>
* <span data-ttu-id="b951f-257">PHP</span><span class="sxs-lookup"><span data-stu-id="b951f-257">PHP</span></span>
* <span data-ttu-id="b951f-258">Python</span><span class="sxs-lookup"><span data-stu-id="b951f-258">Python</span></span>
* <span data-ttu-id="b951f-259">Ruby</span><span class="sxs-lookup"><span data-stu-id="b951f-259">Ruby</span></span>

<span data-ttu-id="b951f-260">Zie voor meer informatie over het installeren van de Azure SDK's [Azure downloads](https://azure.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="b951f-260">For more information on installing the Azure SDKs, see [Azure downloads](https://azure.microsoft.com/downloads/)</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b951f-261">Problemen oplossen</span><span class="sxs-lookup"><span data-stu-id="b951f-261">Troubleshooting</span></span>
### <span data-ttu-id="b951f-262"><a id="storageexception"></a>Uitzondering voor schrijven in blob Storage</span><span class="sxs-lookup"><span data-stu-id="b951f-262"><a id="storageexception"></a>Storage exception for write on blob</span></span>
<span data-ttu-id="b951f-263">**Symptomen**: bij gebruik van de `hadoop` of `hdfs dfs` opdrachten voor het schrijven van bestanden die ~ 12 GB zijn of groter op een HBase-cluster, kunnen de volgende fout optreden:</span><span class="sxs-lookup"><span data-stu-id="b951f-263">**Symptoms**: When using the `hadoop` or `hdfs dfs` commands to write files that are ~12GB or larger on an HBase cluster, you may encounter the following error:</span></span>

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
    Caused by: com.microsoft.azure.storage.StorageException: The request body is too large and exceeds the maximum permissible limit.
            at com.microsoft.azure.storage.StorageException.translateException(StorageException.java:89)
            at com.microsoft.azure.storage.core.StorageRequest.materializeException(StorageRequest.java:307)
            at com.microsoft.azure.storage.core.ExecutionEngine.executeWithRetry(ExecutionEngine.java:182)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlockInternal(CloudBlockBlob.java:816)
            at com.microsoft.azure.storage.blob.CloudBlockBlob.uploadBlock(CloudBlockBlob.java:788)
            at com.microsoft.azure.storage.blob.BlobOutputStream$1.call(BlobOutputStream.java:354)
            ... 7 more

<span data-ttu-id="b951f-264">**Oorzaak**: HBase in HDInsight serverclusters standaard naar een blokgrootte van 256 KB bij het schrijven naar Azure storage.</span><span class="sxs-lookup"><span data-stu-id="b951f-264">**Cause**: HBase on HDInsight clusters default to a block size of 256KB when writing to Azure storage.</span></span> <span data-ttu-id="b951f-265">Hoewel dit voor HBase APIs of REST-API's werkt, het zal leiden tot een fout bij gebruik van de `hadoop` of `hdfs dfs` opdrachtregelprogramma's.</span><span class="sxs-lookup"><span data-stu-id="b951f-265">While this works for HBase APIs or REST APIs, it will result in an error when using the `hadoop` or `hdfs dfs` command-line utilities.</span></span>

<span data-ttu-id="b951f-266">**Resolutie**: Gebruik `fs.azure.write.request.size` om op te geven van een groter blok.</span><span class="sxs-lookup"><span data-stu-id="b951f-266">**Resolution**: Use `fs.azure.write.request.size` to specify a larger block size.</span></span> <span data-ttu-id="b951f-267">U kunt dit doen op basis van per gebruik met behulp van de `-D` parameter.</span><span class="sxs-lookup"><span data-stu-id="b951f-267">You can do this on a per-use basis by using the `-D` parameter.</span></span> <span data-ttu-id="b951f-268">Hieronder volgt een voorbeeld met deze parameter met de `hadoop` opdracht:</span><span class="sxs-lookup"><span data-stu-id="b951f-268">The following is an example using this parameter with the `hadoop` command:</span></span>

    hadoop -fs -D fs.azure.write.request.size=4194304 -copyFromLocal test_large_file.bin /example/data

<span data-ttu-id="b951f-269">U kunt ook de waarde van vergroten `fs.azure.write.request.size` globaal via Ambari.</span><span class="sxs-lookup"><span data-stu-id="b951f-269">You can also increase the value of `fs.azure.write.request.size` globally by using Ambari.</span></span> <span data-ttu-id="b951f-270">De volgende stappen kunnen worden gebruikt om de waarde in de Ambari-Webgebruikersinterface te wijzigen:</span><span class="sxs-lookup"><span data-stu-id="b951f-270">The following steps can be used to change the value in the Ambari Web UI:</span></span>

1. <span data-ttu-id="b951f-271">Ga in uw browser naar de Ambari-Webgebruikersinterface voor uw cluster.</span><span class="sxs-lookup"><span data-stu-id="b951f-271">In your browser, go to the Ambari Web UI for your cluster.</span></span> <span data-ttu-id="b951f-272">Dit is https://CLUSTERNAME.azurehdinsight.net, waarbij **CLUSTERNAME** is de naam van uw cluster.</span><span class="sxs-lookup"><span data-stu-id="b951f-272">This is https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of your cluster.</span></span>

    <span data-ttu-id="b951f-273">Wanneer u wordt gevraagd, typt u de naam van de serverbeheerder en het wachtwoord voor het cluster.</span><span class="sxs-lookup"><span data-stu-id="b951f-273">When prompted, enter the admin name and password for the cluster.</span></span>
2. <span data-ttu-id="b951f-274">Selecteer in de linkerkant van het scherm **HDFS**, en selecteer vervolgens de **Configs** tabblad.</span><span class="sxs-lookup"><span data-stu-id="b951f-274">From the left side of the screen, select **HDFS**, and then select the **Configs** tab.</span></span>
3. <span data-ttu-id="b951f-275">In de **Filter...**  veld `fs.azure.write.request.size`.</span><span class="sxs-lookup"><span data-stu-id="b951f-275">In the **Filter...** field, enter `fs.azure.write.request.size`.</span></span> <span data-ttu-id="b951f-276">Hiermee wordt het veld en de huidige waarde in het midden van de pagina weergegeven.</span><span class="sxs-lookup"><span data-stu-id="b951f-276">This will display the field and current value in the middle of the page.</span></span>
4. <span data-ttu-id="b951f-277">Wijzig de waarde van 262144 (256KB) op de nieuwe waarde.</span><span class="sxs-lookup"><span data-stu-id="b951f-277">Change the value from 262144 (256KB) to the new value.</span></span> <span data-ttu-id="b951f-278">Bijvoorbeeld: 4194304 (4MB).</span><span class="sxs-lookup"><span data-stu-id="b951f-278">For example, 4194304 (4MB).</span></span>

![Afbeelding van het wijzigen van de waarde via Ambari-Webgebruikersinterface](./media/hdinsight-upload-data/hbase-change-block-write-size.png)

<span data-ttu-id="b951f-280">Zie voor meer informatie over het gebruik van Ambari [HDInsight-clusters beheren met de Ambari-Webgebruikersinterface](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="b951f-280">For more information on using Ambari, see [Manage HDInsight clusters using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b951f-281">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b951f-281">Next steps</span></span>
<span data-ttu-id="b951f-282">Nu dat u hoe u gegevens in HDInsight begrijpt, leest u de volgende artikelen voor meer informatie over analyse van de:</span><span class="sxs-lookup"><span data-stu-id="b951f-282">Now that you understand how to get data into HDInsight, read the following articles to learn how to perform analysis:</span></span>

* <span data-ttu-id="b951f-283">[Aan de slag met Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="b951f-283">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* <span data-ttu-id="b951f-284">[Hadoop-taken programmatisch verzenden][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="b951f-284">[Submit Hadoop jobs programmatically][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="b951f-285">[Hive gebruiken met HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="b951f-285">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="b951f-286">[Pig gebruiken met HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="b951f-286">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>

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
