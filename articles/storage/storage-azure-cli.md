---
title: aaaUsing hello Azure CLI 2.0 met Azure Storage | Microsoft Docs
description: Informatie over hoe toouse hello Azure-opdrachtregelinterface (Azure CLI) 2.0 met Azure Storage toocreate en storage-accounts beheren en werken met Azure BLOB's en bestanden. Hello Azure CLI 2.0 is een cross-platform-hulpprogramma dat is geschreven in Python.
services: storage
documentationcenter: na
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 06/02/2017
ms.author: marsma
ms.openlocfilehash: 38402373dcd87f1ef05471a02353c77d58f1a9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-20-with-azure-storage"></a><span data-ttu-id="3a131-104">Hello Azure CLI 2.0 gebruiken met Azure Storage</span><span class="sxs-lookup"><span data-stu-id="3a131-104">Using hello Azure CLI 2.0 with Azure Storage</span></span>

<span data-ttu-id="3a131-105">Hallo open-source platformoverschrijdende Azure CLI 2.0 biedt een reeks opdrachten voor het werken met hello Azure-platform.</span><span class="sxs-lookup"><span data-stu-id="3a131-105">hello open-source, cross-platform Azure CLI 2.0 provides a set of commands for working with hello Azure platform.</span></span> <span data-ttu-id="3a131-106">Het biedt veel van dezelfde functionaliteit in Hallo gevonden Hallo [Azure-portal](https://portal.azure.com), met inbegrip van toegang tot uitgebreide gegevens.</span><span class="sxs-lookup"><span data-stu-id="3a131-106">It provides much of hello same functionality found in hello [Azure portal](https://portal.azure.com), including rich data access.</span></span>

<span data-ttu-id="3a131-107">In deze handleiding wordt uitgelegd hoe u dat toouse hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform verschillende taken die werken met resources in uw Azure Storage-account.</span><span class="sxs-lookup"><span data-stu-id="3a131-107">In this guide, we show you how toouse hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform several tasks working with resources in your Azure Storage account.</span></span> <span data-ttu-id="3a131-108">U wordt aangeraden dat u downloaden en installeren of upgraden van de meest recente versie toohello Hallo CLI 2.0 voordat u deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="3a131-108">We recommend that you download and install or upgrade toohello latest version of hello CLI 2.0 before using this guide.</span></span>

<span data-ttu-id="3a131-109">Hallo-voorbeelden in Hallo handleiding wordt ervan uitgegaan Hallo gebruik van Hallo Bash-shell op Ubuntu, maar andere platforms op dezelfde manier moeten uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3a131-109">hello examples in hello guide assume hello use of hello Bash shell on Ubuntu, but other platforms should perform similarly.</span></span> 

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a><span data-ttu-id="3a131-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="3a131-110">Prerequisites</span></span>
<span data-ttu-id="3a131-111">Deze handleiding wordt ervan uitgegaan dat u Hallo basisconcepten van Azure Storage begrijpt.</span><span class="sxs-lookup"><span data-stu-id="3a131-111">This guide assumes that you understand hello basic concepts of Azure Storage.</span></span> <span data-ttu-id="3a131-112">Ook wordt ervan uitgegaan dat u kunnen toosatisfy Hallo-account maken vereisten die bent hieronder zijn opgegeven voor Azure en Hallo Storage-service.</span><span class="sxs-lookup"><span data-stu-id="3a131-112">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Storage service.</span></span>

### <a name="accounts"></a><span data-ttu-id="3a131-113">Accounts</span><span class="sxs-lookup"><span data-stu-id="3a131-113">Accounts</span></span>
* <span data-ttu-id="3a131-114">**Azure-account**: als u nog een Azure-abonnement hebt [maken van een gratis Azure-account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="3a131-114">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="3a131-115">**Opslagaccount**: zie [Een opslagaccount maken](../storage/storage-create-storage-account.md#create-a-storage-account) in [Over Azure-opslagaccounts](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="3a131-115">**Storage account**: See [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/storage-create-storage-account.md).</span></span>

### <a name="install-hello-azure-cli-20"></a><span data-ttu-id="3a131-116">Hello Azure CLI 2.0 installeren</span><span class="sxs-lookup"><span data-stu-id="3a131-116">Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="3a131-117">Download en installeer hello Azure CLI 2.0 door Hallo aanwijzingen [2.0 voor Azure CLI installeren](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="3a131-117">Download and install hello Azure CLI 2.0 by following hello instructions outlined in [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

> [!TIP]
> <span data-ttu-id="3a131-118">Als u problemen met de installatie Hallo ondervindt, bekijk Hallo [installatie probleemoplossing](/cli/azure/install-az-cli2#installation-troubleshooting) sectie van Hallo artikel en Hallo [installeren probleemoplossing](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) handleiding op GitHub.</span><span class="sxs-lookup"><span data-stu-id="3a131-118">If you have trouble with hello installation, check out hello [Installation Troubleshooting](/cli/azure/install-az-cli2#installation-troubleshooting) section of hello article, and hello [Install Troubleshooting](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guide on GitHub.</span></span>
>

## <a name="working-with-hello-cli"></a><span data-ttu-id="3a131-119">Werken met Hallo CLI</span><span class="sxs-lookup"><span data-stu-id="3a131-119">Working with hello CLI</span></span>

<span data-ttu-id="3a131-120">Zodra u Hallo CLI hebt geïnstalleerd, kunt u Hallo `az` opdracht in de opdrachtregelinterface (Bash, Terminal, opdrachtprompt) tooaccess hello Azure CLI-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="3a131-120">Once you've installed hello CLI, you can use hello `az` command in your command-line interface (Bash, Terminal, Command Prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="3a131-121">Type Hallo `az` toosee opdracht een volledige lijst met base Hallo-opdrachten (Hallo volgende voorbeelduitvoer afgekapt):</span><span class="sxs-lookup"><span data-stu-id="3a131-121">Type hello `az` command toosee a full list of hello base commands (hello following example output has been truncated):</span></span>

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome toohello cool new Azure CLI!

Here are hello base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

<span data-ttu-id="3a131-122">In de opdrachtregelinterface Hallo-opdracht uitvoeren `az storage --help` toolist hello `storage` opdracht subgroepen.</span><span class="sxs-lookup"><span data-stu-id="3a131-122">In your command-line interface, execute hello command `az storage --help` toolist hello `storage` command subgroups.</span></span> <span data-ttu-id="3a131-123">Hallo beschrijvingen van Hallo subgroepen bieden een overzicht van Hallo functionaliteit hello die Azure CLI wordt verstrekt voor het werken met uw opslagresources.</span><span class="sxs-lookup"><span data-stu-id="3a131-123">hello descriptions of hello subgroups provide an overview of hello functionality hello Azure CLI provides for working with your storage resources.</span></span>

```
Group
    az storage: Durable, highly available, and massively scalable cloud storage.

Subgroups:
    account  : Manage storage accounts.
    blob     : Object storage for unstructured data.
    container: Manage blob storage containers.
    cors     : Manage Storage service Cross-Origin Resource Sharing (CORS).
    directory: Manage file storage directories.
    entity   : Manage table storage entities.
    file     : File shares that use hello standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues tooeffectively scale applications according tootraffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-hello-cli-tooyour-azure-subscription"></a><span data-ttu-id="3a131-124">Verbinding maken met de Hallo CLI tooyour Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="3a131-124">Connect hello CLI tooyour Azure subscription</span></span>

<span data-ttu-id="3a131-125">toowork met Hallo resources in uw Azure-abonnement, moet u zich eerst in tooyour Azure-account met `az login`.</span><span class="sxs-lookup"><span data-stu-id="3a131-125">toowork with hello resources in your Azure subscription, you must first log in tooyour Azure account with `az login`.</span></span> <span data-ttu-id="3a131-126">Er zijn verschillende manieren die kunt u zich aanmeldt:</span><span class="sxs-lookup"><span data-stu-id="3a131-126">There are several ways you can log in:</span></span>

* <span data-ttu-id="3a131-127">**Interactieve aanmelding**:`az login`</span><span class="sxs-lookup"><span data-stu-id="3a131-127">**Interactive login**: `az login`</span></span>
* <span data-ttu-id="3a131-128">**Meld u aan met de gebruikersnaam en wachtwoord**:`az login -u johndoe@contoso.com -p VerySecret`</span><span class="sxs-lookup"><span data-stu-id="3a131-128">**Log in with user name and password**: `az login -u johndoe@contoso.com -p VerySecret`</span></span>
  * <span data-ttu-id="3a131-129">Dit werkt niet met Microsoft-accounts of -mailaccounts die gebruikmaken van multi-factor authentication-server.</span><span class="sxs-lookup"><span data-stu-id="3a131-129">This doesn't work with Microsoft accounts or accounts that use multi-factor authentication.</span></span>
* <span data-ttu-id="3a131-130">**Meld u aan met een service-principal**:`az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="3a131-130">**Log in with a service principal**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span></span>

## <a name="azure-cli-20-sample-script"></a><span data-ttu-id="3a131-131">Azure CLI 2.0-voorbeeldscript</span><span class="sxs-lookup"><span data-stu-id="3a131-131">Azure CLI 2.0 sample script</span></span>

<span data-ttu-id="3a131-132">Vervolgens werkt we met een kleine shellscript dat een paar eenvoudige Azure CLI 2.0 opdrachten toointeract met een Azure Storage-resources problemen.</span><span class="sxs-lookup"><span data-stu-id="3a131-132">Next, we'll work with a small shell script that issues a few basic Azure CLI 2.0 commands toointeract with Azure Storage resources.</span></span> <span data-ttu-id="3a131-133">Hallo script eerst maakt een nieuwe container in uw opslagaccount en vervolgens een bestaand bestand (als een blob) toothat container uploadt.</span><span class="sxs-lookup"><span data-stu-id="3a131-133">hello script first creates a new container in your storage account, then uploads an existing file (as a blob) toothat container.</span></span> <span data-ttu-id="3a131-134">Deze vervolgens een lijst met alle blobs in Hallo-container en ten slotte downloadt Hallo tooa bestemming op uw lokale computer die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="3a131-134">It then lists all blobs in hello container, and finally, downloads hello file tooa destination on your local computer that you specify.</span></span>

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating hello container..."
az storage container create --name $container_name

echo "Uploading hello file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing hello blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading hello file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

<span data-ttu-id="3a131-135">**Configureren en het Hallo-script uitvoeren**</span><span class="sxs-lookup"><span data-stu-id="3a131-135">**Configure and run hello script**</span></span>

1. <span data-ttu-id="3a131-136">Uw favoriete teksteditor openen en vervolgens kopieert en plakt Hallo vóór het script in Hallo-editor.</span><span class="sxs-lookup"><span data-stu-id="3a131-136">Open your favorite text editor, then copy and paste hello preceding script into hello editor.</span></span>

2. <span data-ttu-id="3a131-137">Werk van het script Hallo variabelen tooreflect vervolgens uw configuratie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="3a131-137">Next, update hello script's variables tooreflect your configuration settings.</span></span> <span data-ttu-id="3a131-138">Vervang Hallo waarden zoals opgegeven te volgen:</span><span class="sxs-lookup"><span data-stu-id="3a131-138">Replace hello following values as specified:</span></span>

   * <span data-ttu-id="3a131-139">**\<storage_account_name\>**  Hallo-naam van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="3a131-139">**\<storage_account_name\>** hello name of your storage account.</span></span>
   * <span data-ttu-id="3a131-140">**\<storage_account_key\>**  Hallo primaire of secundaire toegangssleutel voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="3a131-140">**\<storage_account_key\>** hello primary or secondary access key for your storage account.</span></span>
   * <span data-ttu-id="3a131-141">**\<container_name\>**  naam van een nieuwe container toocreate, zoals "azure-cli-voorbeeld-container" Hallo.</span><span class="sxs-lookup"><span data-stu-id="3a131-141">**\<container_name\>** A name hello new container toocreate, such as "azure-cli-sample-container".</span></span>
   * <span data-ttu-id="3a131-142">**\<blob_name\>**  een naam voor de bestemmings-blob Hallo in Hallo-container.</span><span class="sxs-lookup"><span data-stu-id="3a131-142">**\<blob_name\>** A name for hello destination blob in hello container.</span></span>
   * <span data-ttu-id="3a131-143">**\<file_to_upload\>**  Hallo pad toosmall bestand op uw lokale computer, zoals ' ~ / images/HelloWorld.png '.</span><span class="sxs-lookup"><span data-stu-id="3a131-143">**\<file_to_upload\>** hello path toosmall file on your local computer, such as "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="3a131-144">**\<destination_file\>**  Hallo bestemmingspad, zoals ' ~ / downloadedImage.png '.</span><span class="sxs-lookup"><span data-stu-id="3a131-144">**\<destination_file\>** hello destination file path, such as "~/downloadedImage.png".</span></span>

3. <span data-ttu-id="3a131-145">Nadat u de benodigde variabelen Hallo hebt bijgewerkt, Hallo script opslaat en sluit de editor af.</span><span class="sxs-lookup"><span data-stu-id="3a131-145">After you've updated hello necessary variables, save hello script and exit your editor.</span></span> <span data-ttu-id="3a131-146">Hallo volgende stappen wordt ervan uitgegaan dat u hebt uw script genoemd **my_storage_sample.sh**.</span><span class="sxs-lookup"><span data-stu-id="3a131-146">hello next steps assume you've named your script **my_storage_sample.sh**.</span></span>

4. <span data-ttu-id="3a131-147">U markeert Hallo script als uitvoerbare, indien nodig:`chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="3a131-147">Mark hello script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>

5. <span data-ttu-id="3a131-148">Hallo-script uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="3a131-148">Execute hello script.</span></span> <span data-ttu-id="3a131-149">Bijvoorbeeld in Bash:`./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="3a131-149">For example, in Bash: `./my_storage_sample.sh`</span></span>

<span data-ttu-id="3a131-150">U moet uitvoer vergelijkbare toohello volgende Zie en Hallo  **\<destination_file\>**  u hebt opgegeven in Hallo script moet worden weergegeven op de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="3a131-150">You should see output similar toohello following, and hello **\<destination_file\>** you specified in hello script should appear on your local computer.</span></span>

```
Creating hello container...
{
  "created": true
}
Uploading hello file...
Percent complete: %100.0
Listing hello blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading hello file...
Name
---------
README.md
Done
```

> [!TIP]
> <span data-ttu-id="3a131-151">Hallo voorgaande uitvoer is in **tabel** indeling.</span><span class="sxs-lookup"><span data-stu-id="3a131-151">hello preceding output is in **table** format.</span></span> <span data-ttu-id="3a131-152">U kunt opgeven dat indeling toouse uitvoer door te geven Hallo `--output` argument in de CLI-opdrachten of stel deze globaal met `az configure`.</span><span class="sxs-lookup"><span data-stu-id="3a131-152">You can specify which output format toouse by specifying hello `--output` argument in your CLI commands, or set it globally using `az configure`.</span></span>
>

## <a name="manage-storage-accounts"></a><span data-ttu-id="3a131-153">Opslagaccounts beheren</span><span class="sxs-lookup"><span data-stu-id="3a131-153">Manage storage accounts</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="3a131-154">Een nieuw opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="3a131-154">Create a new storage account</span></span>
<span data-ttu-id="3a131-155">toouse Azure Storage, moet u een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="3a131-155">toouse Azure Storage, you need a storage account.</span></span> <span data-ttu-id="3a131-156">U kunt een nieuw Azure-opslagaccount maken nadat u uw computer te hebt geconfigureerd[tooyour abonnement verbinding](#connect-to-your-azure-subscription).</span><span class="sxs-lookup"><span data-stu-id="3a131-156">You can create a new Azure Storage account after you've configured your computer too[connect tooyour subscription](#connect-to-your-azure-subscription).</span></span>

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* <span data-ttu-id="3a131-157">`--location`[Vereist]: locatie.</span><span class="sxs-lookup"><span data-stu-id="3a131-157">`--location` [Required]: Location.</span></span> <span data-ttu-id="3a131-158">Bijvoorbeeld "VS-West'.</span><span class="sxs-lookup"><span data-stu-id="3a131-158">For example, "West US".</span></span>
* <span data-ttu-id="3a131-159">`--name`[Vereist]: Hallo opslagaccountnaam.</span><span class="sxs-lookup"><span data-stu-id="3a131-159">`--name` [Required]: hello storage account name.</span></span> <span data-ttu-id="3a131-160">Hallo-naam moet 3 too24 tekens bestaan en gebruik alleen kleine letters alfanumerieke tekens.</span><span class="sxs-lookup"><span data-stu-id="3a131-160">hello name must be 3 too24 characters in length, and use only lowercase alphanumeric characters.</span></span>
* <span data-ttu-id="3a131-161">`--resource-group`[Vereist]: naam van resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="3a131-161">`--resource-group` [Required]: Name of resource group.</span></span>
* <span data-ttu-id="3a131-162">`--sku`[Vereist]: Hallo opslagaccount SKU.</span><span class="sxs-lookup"><span data-stu-id="3a131-162">`--sku` [Required]: hello storage account SKU.</span></span> <span data-ttu-id="3a131-163">Toegestane waarden:</span><span class="sxs-lookup"><span data-stu-id="3a131-163">Allowed values:</span></span>
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a><span data-ttu-id="3a131-164">Azure storage-standaardaccount omgevingsvariabelen worden ingesteld</span><span class="sxs-lookup"><span data-stu-id="3a131-164">Set default Azure storage account environment variables</span></span>
<span data-ttu-id="3a131-165">U kunt meerdere opslagaccounts in uw Azure-abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="3a131-165">You can have multiple storage accounts in your Azure subscription.</span></span> <span data-ttu-id="3a131-166">tooselect één van deze opdrachten toouse voor alle daaropvolgende opslag, kunt u deze omgevingsvariabelen instellen:</span><span class="sxs-lookup"><span data-stu-id="3a131-166">tooselect one of them toouse for all subsequent storage commands, you can set these environment variables:</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="3a131-167">Er is een andere manier tooset storage-standaardaccount met behulp van een verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="3a131-167">Another way tooset a default storage account is by using a connection string.</span></span> <span data-ttu-id="3a131-168">De verbindingsreeks Hallo Hello eerst ophalen `show-connection-string` opdracht:</span><span class="sxs-lookup"><span data-stu-id="3a131-168">First, get hello connection string with hello `show-connection-string` command:</span></span>

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

<span data-ttu-id="3a131-169">Vervolgens kopiëren Hallo verbindingsreeks uitvoer en stelt u Hallo `AZURE_STORAGE_CONNECTION_STRING` omgevingsvariabele (mogelijk moet u het Hallo-verbindingsreeks tooenclose aanhalingstekens):</span><span class="sxs-lookup"><span data-stu-id="3a131-169">Then copy hello output connection string and set hello `AZURE_STORAGE_CONNECTION_STRING` environment variable (you might need tooenclose hello connection string in quotes):</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> <span data-ttu-id="3a131-170">Alle voorbeelden in Hallo volgende secties in dit artikel wordt ervan uitgegaan dat u hebt ingesteld dat Hallo `AZURE_STORAGE_ACCOUNT` en `AZURE_STORAGE_ACCESS_KEY` omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="3a131-170">All examples in hello following sections of this article assume that you've set hello `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY` environment variables.</span></span>
>

## <a name="create-and-manage-blobs"></a><span data-ttu-id="3a131-171">Maken en blobs beheren</span><span class="sxs-lookup"><span data-stu-id="3a131-171">Create and manage blobs</span></span>
<span data-ttu-id="3a131-172">Azure Blob storage is een service voor het opslaan van grote hoeveelheden ongestructureerde gegevens, zoals tekst of binaire gegevens, die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via HTTP of HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3a131-172">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="3a131-173">Deze sectie wordt ervan uitgegaan dat u al bekend met concepten voor Azure Blob-opslag bent.</span><span class="sxs-lookup"><span data-stu-id="3a131-173">This section assumes that you are already familiar with Azure Blob storage concepts.</span></span> <span data-ttu-id="3a131-174">Zie voor gedetailleerde informatie [aan de slag met Azure Blob storage met .NET](storage-dotnet-how-to-use-blobs.md) en [concepten van Blob-Service](/rest/api/storageservices/blob-service-concepts).</span><span class="sxs-lookup"><span data-stu-id="3a131-174">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](/rest/api/storageservices/blob-service-concepts).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="3a131-175">Een container maken</span><span class="sxs-lookup"><span data-stu-id="3a131-175">Create a container</span></span>
<span data-ttu-id="3a131-176">Elke blob in Azure-opslag moet zich in een container.</span><span class="sxs-lookup"><span data-stu-id="3a131-176">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="3a131-177">U kunt een container maken met behulp van Hallo `az storage container create` opdracht:</span><span class="sxs-lookup"><span data-stu-id="3a131-177">You can create a container by using hello `az storage container create` command:</span></span>

```azurecli
az storage container create --name <container_name>
```

<span data-ttu-id="3a131-178">U kunt een van drie niveaus van leestoegang voor een nieuwe container instellen door te geven Hallo optionele `--public-access` argument:</span><span class="sxs-lookup"><span data-stu-id="3a131-178">You can set one of three levels of read access for a new container by specifying hello optional  `--public-access` argument:</span></span>

* <span data-ttu-id="3a131-179">`off`(standaard): gegevens van de Container is eigenaar van de persoonlijke toohello-account.</span><span class="sxs-lookup"><span data-stu-id="3a131-179">`off` (default): Container data is private toohello account owner.</span></span>
* <span data-ttu-id="3a131-180">`blob`: Openbare leestoegang voor blobs.</span><span class="sxs-lookup"><span data-stu-id="3a131-180">`blob`: Public read access for blobs.</span></span>
* <span data-ttu-id="3a131-181">`container`: Toegang tot de volledige container toohello openbare lees- en lijst.</span><span class="sxs-lookup"><span data-stu-id="3a131-181">`container`: Public read and list access toohello entire container.</span></span>

<span data-ttu-id="3a131-182">Zie voor meer informatie [anonieme leestoegang toocontainers en blobs beheren](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="3a131-182">For more information, see [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md).</span></span>

### <a name="upload-a-blob-tooa-container"></a><span data-ttu-id="3a131-183">Een blob-container tooa uploaden</span><span class="sxs-lookup"><span data-stu-id="3a131-183">Upload a blob tooa container</span></span>
<span data-ttu-id="3a131-184">Azure Blob storage ondersteunt blok, toevoegen en pagina-blobs.</span><span class="sxs-lookup"><span data-stu-id="3a131-184">Azure Blob storage supports block, append, and page blobs.</span></span> <span data-ttu-id="3a131-185">Het uploaden van blobs tooa container via Hallo `blob upload` opdracht:</span><span class="sxs-lookup"><span data-stu-id="3a131-185">Upload blobs tooa container by using hello `blob upload` command:</span></span>

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 <span data-ttu-id="3a131-186">Standaard Hallo `blob upload` opdracht uploadt *.vhd bestanden toopage blobs of anderszins blok-blobs.</span><span class="sxs-lookup"><span data-stu-id="3a131-186">By default, hello `blob upload` command uploads *.vhd files toopage blobs, or block blobs otherwise.</span></span> <span data-ttu-id="3a131-187">toospecify een ander type wanneer u een blob uploaden, kunt u Hallo `--type` argument--toegestane waarden zijn `append`, `block`, en `page`.</span><span class="sxs-lookup"><span data-stu-id="3a131-187">toospecify another type when you upload a blob, you can use hello `--type` argument--allowed values are `append`, `block`, and `page`.</span></span>

 <span data-ttu-id="3a131-188">Zie voor meer informatie over Hallo andere blob-typen [blok-Blobs, toevoeg-Blobs en pagina-Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span><span class="sxs-lookup"><span data-stu-id="3a131-188">For more information on hello different blob types, see [Understanding Block Blobs, Append Blobs, and Page Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span></span>


### <a name="download-a-blob-from-a-container"></a><span data-ttu-id="3a131-189">Een blob downloaden uit een container</span><span class="sxs-lookup"><span data-stu-id="3a131-189">Download a blob from a container</span></span>
<span data-ttu-id="3a131-190">In dit voorbeeld laat zien hoe toodownload een blob uit een container:</span><span class="sxs-lookup"><span data-stu-id="3a131-190">This example demonstrates how toodownload a blob from a container:</span></span>

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="3a131-191">Lijst Hallo blobs in een container</span><span class="sxs-lookup"><span data-stu-id="3a131-191">List hello blobs in a container</span></span>

<span data-ttu-id="3a131-192">Hallo blobs in een container met Hallo lijst [lijst met blob storage az](/cli/azure/storage/blob#list) opdracht.</span><span class="sxs-lookup"><span data-stu-id="3a131-192">List hello blobs in a container with hello [az storage blob list](/cli/azure/storage/blob#list) command.</span></span>

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a><span data-ttu-id="3a131-193">Blobs kopiëren</span><span class="sxs-lookup"><span data-stu-id="3a131-193">Copy blobs</span></span>
<span data-ttu-id="3a131-194">U kunt blobs binnen of tussen opslagaccounts en regio's asynchroon kopiëren.</span><span class="sxs-lookup"><span data-stu-id="3a131-194">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="3a131-195">Hallo volgende voorbeeld laat zien hoe toocopy blobs uit één opslag tooanother account.</span><span class="sxs-lookup"><span data-stu-id="3a131-195">hello following example demonstrates how toocopy blobs from one storage account tooanother.</span></span> <span data-ttu-id="3a131-196">We eerst een container maken in Hallo bron storage-account, openbare leestoegang voor de blobs opgeven.</span><span class="sxs-lookup"><span data-stu-id="3a131-196">We first create a container in hello source storage account, specifying public read-access for its blobs.</span></span> <span data-ttu-id="3a131-197">Vervolgens uploaden we een bestandscontainer toohello en ten slotte kopie Hallo blob uit die container naar een container in Hallo doelopslagaccount.</span><span class="sxs-lookup"><span data-stu-id="3a131-197">Next, we upload a file toohello container, and finally, copy hello blob from that container into a container in hello destination storage account.</span></span>

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob toocontainer in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account toodestination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

<span data-ttu-id="3a131-198">Hallo doelcontainer moet Hallo hierboven voorbeeld, al aanwezig in Hallo doelopslagaccount voor Hallo kopie bewerking toosucceed.</span><span class="sxs-lookup"><span data-stu-id="3a131-198">In hello above example, hello destination container must already exist in hello destination storage account for hello copy operation toosucceed.</span></span> <span data-ttu-id="3a131-199">Bovendien Hallo bron-blob opgegeven in Hallo `--source-uri` argument moet een shared access signature (SAS)-token Neem of openbaar toegankelijk zijn, zoals in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="3a131-199">Additionally, hello source blob specified in hello `--source-uri` argument must either include a shared access signature (SAS) token, or be publicly accessible, as in this example.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="3a131-200">Een blob verwijderen</span><span class="sxs-lookup"><span data-stu-id="3a131-200">Delete a blob</span></span>
<span data-ttu-id="3a131-201">een blob toodelete gebruiken Hallo `blob delete` opdracht:</span><span class="sxs-lookup"><span data-stu-id="3a131-201">toodelete a blob, use hello `blob delete` command:</span></span>

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="3a131-202">Maken en beheren van bestandsshares</span><span class="sxs-lookup"><span data-stu-id="3a131-202">Create and manage file shares</span></span>
<span data-ttu-id="3a131-203">Azure File storage biedt gedeelde opslag voor toepassingen met behulp van Hallo Server Message Block (SMB)-protocol.</span><span class="sxs-lookup"><span data-stu-id="3a131-203">Azure File storage offers shared storage for applications using hello Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="3a131-204">Microsoft Azure virtuele machines en cloud-services, evenals de on-premises toepassingen kunnen bestandsgegevens via gekoppelde shares delen.</span><span class="sxs-lookup"><span data-stu-id="3a131-204">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="3a131-205">U kunt bestandsshares en bestandsgegevens via hello Azure CLI kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="3a131-205">You can manage file shares and file data via hello Azure CLI.</span></span> <span data-ttu-id="3a131-206">Zie voor meer informatie over Azure File storage [aan de slag met Azure File storage in Windows](storage-dotnet-how-to-use-files.md) of [hoe toouse Azure File storage met Linux](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="3a131-206">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How toouse Azure File storage with Linux](storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="3a131-207">Een bestandsshare maken</span><span class="sxs-lookup"><span data-stu-id="3a131-207">Create a file share</span></span>
<span data-ttu-id="3a131-208">Een Azure-bestandsshare is een SMB-bestandsshare in Azure.</span><span class="sxs-lookup"><span data-stu-id="3a131-208">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="3a131-209">Alle mappen en bestanden moeten worden gemaakt in een bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="3a131-209">All directories and files must be created in a file share.</span></span> <span data-ttu-id="3a131-210">Een account kan een onbeperkt aantal shares bevatten en een bestandsshare kan een onbeperkt aantal bestanden van toohello capaciteitslimiet van het opslagaccount Hallo opslaan.</span><span class="sxs-lookup"><span data-stu-id="3a131-210">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up toohello capacity limits of hello storage account.</span></span> <span data-ttu-id="3a131-211">Hallo volgende voorbeeld wordt een bestandsshare met de naam **mijnshare**.</span><span class="sxs-lookup"><span data-stu-id="3a131-211">hello following example creates a file share named **myshare**.</span></span>

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="3a131-212">Een map maken</span><span class="sxs-lookup"><span data-stu-id="3a131-212">Create a directory</span></span>
<span data-ttu-id="3a131-213">Een directory biedt een hiërarchische structuur in een Azure-bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="3a131-213">A directory provides a hierarchical structure in an Azure file share.</span></span> <span data-ttu-id="3a131-214">Hallo volgende voorbeeld maakt u een map met de naam **myDir** in Hallo-bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="3a131-214">hello following example creates a directory named **myDir** in hello file share.</span></span>

```azurecli
az storage directory create --name myDir --share-name myshare
```

<span data-ttu-id="3a131-215">Een pad kan bijvoorbeeld meerdere niveaus bevatten **dir1/dir2**.</span><span class="sxs-lookup"><span data-stu-id="3a131-215">A directory path can include multiple levels, for example **dir1/dir2**.</span></span> <span data-ttu-id="3a131-216">Echter, moet u ervoor zorgen dat alle bovenliggende mappen bestaan voordat u een submap maakt.</span><span class="sxs-lookup"><span data-stu-id="3a131-216">However, you must ensure that all parent directories exist before creating a subdirectory.</span></span> <span data-ttu-id="3a131-217">Bijvoorbeeld: voor pad **dir1/dir2**, moet u eerst directory maken **dir1**, maak vervolgens de directory **dir2**.</span><span class="sxs-lookup"><span data-stu-id="3a131-217">For example, for path **dir1/dir2**, you must first create directory **dir1**, then create directory **dir2**.</span></span>

### <a name="upload-a-local-file-tooa-share"></a><span data-ttu-id="3a131-218">Uploaden van een lokale tooa bestandsshare</span><span class="sxs-lookup"><span data-stu-id="3a131-218">Upload a local file tooa share</span></span>
<span data-ttu-id="3a131-219">Hallo volgende voorbeeld wordt een bestand geüpload vanuit **~/temp/samplefile.txt** tooroot Hallo **mijnshare** bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="3a131-219">hello following example uploads a file from **~/temp/samplefile.txt** tooroot of hello **myshare** file share.</span></span> <span data-ttu-id="3a131-220">Hallo `--source` geeft Hallo bestaande lokale bestand tooupload argument.</span><span class="sxs-lookup"><span data-stu-id="3a131-220">hello `--source` argument specifies hello existing local file tooupload.</span></span>

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

<span data-ttu-id="3a131-221">Net als bij het maken van de directory, kunt u een mappad binnen Hallo share tooupload Hallo bestand tooan bestaande map in Hallo share opgeven:</span><span class="sxs-lookup"><span data-stu-id="3a131-221">As with directory creation, you can specify a directory path within hello share tooupload hello file tooan existing directory within hello share:</span></span>

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

<span data-ttu-id="3a131-222">Een bestand in de share Hallo kan up too1 TB groot zijn.</span><span class="sxs-lookup"><span data-stu-id="3a131-222">A file in hello share can be up too1 TB in size.</span></span>

### <a name="list-hello-files-in-a-share"></a><span data-ttu-id="3a131-223">Hallo-bestanden weergeven in een share</span><span class="sxs-lookup"><span data-stu-id="3a131-223">List hello files in a share</span></span>
<span data-ttu-id="3a131-224">U kunt bestanden en mappen in een share weergeven met behulp van Hallo `az storage file list` opdracht:</span><span class="sxs-lookup"><span data-stu-id="3a131-224">You can list files and directories in a share by using hello `az storage file list` command:</span></span>

```azurecli
# List hello files in hello root of a share
az storage file list --share-name myshare --output table

# List hello files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List hello files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a><span data-ttu-id="3a131-225">Bestanden kopiëren</span><span class="sxs-lookup"><span data-stu-id="3a131-225">Copy files</span></span>      
<span data-ttu-id="3a131-226">U kunt een bestand tooanother, een bestand tooa blob of een blob tooa-bestand kopiëren.</span><span class="sxs-lookup"><span data-stu-id="3a131-226">You can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="3a131-227">Bijvoorbeeld, een map in een andere share tooa toocopy:</span><span class="sxs-lookup"><span data-stu-id="3a131-227">For example, toocopy a file tooa directory in a different share:</span></span>        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a><span data-ttu-id="3a131-228">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="3a131-228">Next steps</span></span>
<span data-ttu-id="3a131-229">Hier volgen enkele aanvullende resources voor meer informatie over het werken met hello Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="3a131-229">Here are some additional resources for learning more about working with hello Azure CLI 2.0.</span></span>

* [<span data-ttu-id="3a131-230">Aan de slag met Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="3a131-230">Get started with Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="3a131-231">Azure CLI 2.0-opdrachtenreferentie</span><span class="sxs-lookup"><span data-stu-id="3a131-231">Azure CLI 2.0 command reference</span></span>](/cli/azure)
* [<span data-ttu-id="3a131-232">Azure CLI 2.0 op GitHub</span><span class="sxs-lookup"><span data-stu-id="3a131-232">Azure CLI 2.0 on GitHub</span></span>](https://github.com/Azure/azure-cli)
