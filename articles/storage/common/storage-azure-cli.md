---
title: De Azure CLI 2.0 gebruiken met Azure Storage | Microsoft Docs
description: Informatie over het gebruik van de Azure-opdrachtregelinterface (Azure CLI) 2.0 met Azure Storage te maken en beheren van storage-accounts en werken met Azure BLOB's en bestanden. De Azure CLI 2.0 is een cross-platform-hulpprogramma dat is geschreven in Python.
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
ms.openlocfilehash: 8dfa91de25eadb93186d994095f0a0107fe1a9d0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="using-the-azure-cli-20-with-azure-storage"></a><span data-ttu-id="c0dd1-104">De Azure CLI 2.0 gebruiken met Azure Storage</span><span class="sxs-lookup"><span data-stu-id="c0dd1-104">Using the Azure CLI 2.0 with Azure Storage</span></span>

<span data-ttu-id="c0dd1-105">De open source, platformoverschrijdende Azure CLI 2.0 biedt een reeks opdrachten voor het werken met de Azure-platform.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-105">The open-source, cross-platform Azure CLI 2.0 provides a set of commands for working with the Azure platform.</span></span> <span data-ttu-id="c0dd1-106">Het biedt veel van dezelfde functionaliteit gevonden in de [Azure-portal](https://portal.azure.com), met inbegrip van toegang tot uitgebreide gegevens.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-106">It provides much of the same functionality found in the [Azure portal](https://portal.azure.com), including rich data access.</span></span>

<span data-ttu-id="c0dd1-107">In deze handleiding wordt beschreven hoe u gebruikt de [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) verschillende taken die werken met resources in uw Azure Storage-account uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-107">In this guide, we show you how to use the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) to perform several tasks working with resources in your Azure Storage account.</span></span> <span data-ttu-id="c0dd1-108">U wordt aangeraden dat u downloaden en installeren of naar de nieuwste versie van de CLI 2.0 upgraden voordat u deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-108">We recommend that you download and install or upgrade to the latest version of the CLI 2.0 before using this guide.</span></span>

<span data-ttu-id="c0dd1-109">De voorbeelden in deze handleiding wordt ervan uitgegaan dat het gebruik van de Bash-shell op Ubuntu, maar andere platforms op dezelfde manier moeten uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-109">The examples in the guide assume the use of the Bash shell on Ubuntu, but other platforms should perform similarly.</span></span> 

[!INCLUDE [storage-cli-versions](../../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a><span data-ttu-id="c0dd1-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="c0dd1-110">Prerequisites</span></span>
<span data-ttu-id="c0dd1-111">Deze handleiding wordt ervan uitgegaan dat u de basisconcepten van Azure Storage begrijpt.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-111">This guide assumes that you understand the basic concepts of Azure Storage.</span></span> <span data-ttu-id="c0dd1-112">Ook wordt ervan uitgegaan dat u kunnen voldoen aan de vereisten voor het maken van account die bent hieronder zijn opgegeven voor Azure en de Storage-service.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-112">It also assumes that you're able to satisfy the account creation requirements that are specified below for Azure and the Storage service.</span></span>

### <a name="accounts"></a><span data-ttu-id="c0dd1-113">Accounts</span><span class="sxs-lookup"><span data-stu-id="c0dd1-113">Accounts</span></span>
* <span data-ttu-id="c0dd1-114">**Azure-account**: als u nog een Azure-abonnement hebt [maken van een gratis Azure-account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="c0dd1-114">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="c0dd1-115">**Opslagaccount**: zie [Een opslagaccount maken](storage-create-storage-account.md#create-a-storage-account) in [Over Azure-opslagaccounts](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="c0dd1-115">**Storage account**: See [Create a storage account](storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](storage-create-storage-account.md).</span></span>

### <a name="install-the-azure-cli-20"></a><span data-ttu-id="c0dd1-116">Azure CLI 2.0 installeren</span><span class="sxs-lookup"><span data-stu-id="c0dd1-116">Install the Azure CLI 2.0</span></span>

<span data-ttu-id="c0dd1-117">Download en installeer de Azure CLI 2.0 door de instructies die worden beschreven in [2.0 voor Azure CLI installeren](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="c0dd1-117">Download and install the Azure CLI 2.0 by following the instructions outlined in [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

> [!TIP]
> <span data-ttu-id="c0dd1-118">Als u problemen met de installatie ondervindt, bekijk de [installatie probleemoplossing](/cli/azure/install-az-cli2#installation-troubleshooting) sectie van het artikel en de [installeren probleemoplossing](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) handleiding op GitHub.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-118">If you have trouble with the installation, check out the [Installation Troubleshooting](/cli/azure/install-az-cli2#installation-troubleshooting) section of the article, and the [Install Troubleshooting](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guide on GitHub.</span></span>
>

## <a name="working-with-the-cli"></a><span data-ttu-id="c0dd1-119">Werken met de CLI</span><span class="sxs-lookup"><span data-stu-id="c0dd1-119">Working with the CLI</span></span>

<span data-ttu-id="c0dd1-120">Nadat u de CLI hebt geïnstalleerd, kunt u de `az` opdracht in de opdrachtregelinterface (Bash, Terminal, opdrachtprompt) voor toegang tot de Azure CLI-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-120">Once you've installed the CLI, you can use the `az` command in your command-line interface (Bash, Terminal, Command Prompt) to access the Azure CLI commands.</span></span> <span data-ttu-id="c0dd1-121">Typ de `az` opdracht voor een volledig overzicht van de basis-opdrachten (de volgende voorbeelduitvoer afgekapt):</span><span class="sxs-lookup"><span data-stu-id="c0dd1-121">Type the `az` command to see a full list of the base commands (the following example output has been truncated):</span></span>

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome to the cool new Azure CLI!

Here are the base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

<span data-ttu-id="c0dd1-122">Voer de opdracht uit in de opdrachtregelinterface `az storage --help` aan lijst met de `storage` opdracht subgroepen.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-122">In your command-line interface, execute the command `az storage --help` to list the `storage` command subgroups.</span></span> <span data-ttu-id="c0dd1-123">De beschrijvingen van de subgroepen bevatten een overzicht van de functionaliteit van die de Azure CLI wordt verstrekt voor het werken met uw opslagresources.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-123">The descriptions of the subgroups provide an overview of the functionality the Azure CLI provides for working with your storage resources.</span></span>

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
    file     : File shares that use the standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues to effectively scale applications according to traffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-the-cli-to-your-azure-subscription"></a><span data-ttu-id="c0dd1-124">De CLI verbinding met uw Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="c0dd1-124">Connect the CLI to your Azure subscription</span></span>

<span data-ttu-id="c0dd1-125">Om te werken met de resources in uw Azure-abonnement, u moet eerst aanmelden bij uw Azure-account met `az login`.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-125">To work with the resources in your Azure subscription, you must first log in to your Azure account with `az login`.</span></span> <span data-ttu-id="c0dd1-126">Er zijn verschillende manieren die kunt u zich aanmeldt:</span><span class="sxs-lookup"><span data-stu-id="c0dd1-126">There are several ways you can log in:</span></span>

* <span data-ttu-id="c0dd1-127">**Interactieve aanmelding**:`az login`</span><span class="sxs-lookup"><span data-stu-id="c0dd1-127">**Interactive login**: `az login`</span></span>
* <span data-ttu-id="c0dd1-128">**Meld u aan met de gebruikersnaam en wachtwoord**:`az login -u johndoe@contoso.com -p VerySecret`</span><span class="sxs-lookup"><span data-stu-id="c0dd1-128">**Log in with user name and password**: `az login -u johndoe@contoso.com -p VerySecret`</span></span>
  * <span data-ttu-id="c0dd1-129">Dit werkt niet met Microsoft-accounts of -mailaccounts die gebruikmaken van multi-factor authentication-server.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-129">This doesn't work with Microsoft accounts or accounts that use multi-factor authentication.</span></span>
* <span data-ttu-id="c0dd1-130">**Meld u aan met een service-principal**:`az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="c0dd1-130">**Log in with a service principal**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span></span>

## <a name="azure-cli-20-sample-script"></a><span data-ttu-id="c0dd1-131">Azure CLI 2.0-voorbeeldscript</span><span class="sxs-lookup"><span data-stu-id="c0dd1-131">Azure CLI 2.0 sample script</span></span>

<span data-ttu-id="c0dd1-132">Vervolgens werkt we met een kleine shellscript dat problemen van enkele elementaire 2.0 voor Azure CLI-opdrachten om te communiceren met een Azure Storage-resources.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-132">Next, we'll work with a small shell script that issues a few basic Azure CLI 2.0 commands to interact with Azure Storage resources.</span></span> <span data-ttu-id="c0dd1-133">Het script eerst maakt een nieuwe container in uw opslagaccount en uploadt een bestaand bestand (als een blob) op die container.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-133">The script first creates a new container in your storage account, then uploads an existing file (as a blob) to that container.</span></span> <span data-ttu-id="c0dd1-134">Deze vervolgens een lijst met alle blobs in de container en ten slotte wordt het bestand wordt gedownload naar een bestemming op uw lokale computer die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-134">It then lists all blobs in the container, and finally, downloads the file to a destination on your local computer that you specify.</span></span>

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating the container..."
az storage container create --name $container_name

echo "Uploading the file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing the blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading the file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

<span data-ttu-id="c0dd1-135">**Configureren en voer het script**</span><span class="sxs-lookup"><span data-stu-id="c0dd1-135">**Configure and run the script**</span></span>

1. <span data-ttu-id="c0dd1-136">Uw favoriete teksteditor openen en vervolgens kopieert en plakt u dit script in de editor.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-136">Open your favorite text editor, then copy and paste the preceding script into the editor.</span></span>

2. <span data-ttu-id="c0dd1-137">Werk vervolgens de scriptvariabelen om uw configuratie-instellingen weer te geven.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-137">Next, update the script's variables to reflect your configuration settings.</span></span> <span data-ttu-id="c0dd1-138">Vervang de volgende waarden zoals opgegeven:</span><span class="sxs-lookup"><span data-stu-id="c0dd1-138">Replace the following values as specified:</span></span>

   * <span data-ttu-id="c0dd1-139">**\<storage_account_name\>**  de naam van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-139">**\<storage_account_name\>** The name of your storage account.</span></span>
   * <span data-ttu-id="c0dd1-140">**\<storage_account_key\>**  de primaire of secundaire toegangssleutel voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-140">**\<storage_account_key\>** The primary or secondary access key for your storage account.</span></span>
   * <span data-ttu-id="c0dd1-141">**\<container_name\>**  A Noem de nieuwe container te maken, zoals "azure-cli-voorbeeld-container".</span><span class="sxs-lookup"><span data-stu-id="c0dd1-141">**\<container_name\>** A name the new container to create, such as "azure-cli-sample-container".</span></span>
   * <span data-ttu-id="c0dd1-142">**\<blob_name\>**  een naam voor de bestemmings-blob in de container.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-142">**\<blob_name\>** A name for the destination blob in the container.</span></span>
   * <span data-ttu-id="c0dd1-143">**\<file_to_upload\>**  het pad naar een klein bestand op uw lokale computer, zoals ' ~ / images/HelloWorld.png '.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-143">**\<file_to_upload\>** The path to small file on your local computer, such as "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="c0dd1-144">**\<destination_file\>**  het doelbestand pad, zoals ' ~ / downloadedImage.png '.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-144">**\<destination_file\>** The destination file path, such as "~/downloadedImage.png".</span></span>

3. <span data-ttu-id="c0dd1-145">Nadat u de benodigde variabelen hebt bijgewerkt, sla het script op en sluit de editor af.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-145">After you've updated the necessary variables, save the script and exit your editor.</span></span> <span data-ttu-id="c0dd1-146">De volgende stappen wordt ervan uitgegaan dat u hebt uw script genoemd **my_storage_sample.sh**.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-146">The next steps assume you've named your script **my_storage_sample.sh**.</span></span>

4. <span data-ttu-id="c0dd1-147">Markeer het script als uitvoerbare, indien nodig:`chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="c0dd1-147">Mark the script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>

5. <span data-ttu-id="c0dd1-148">Voer het script.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-148">Execute the script.</span></span> <span data-ttu-id="c0dd1-149">Bijvoorbeeld in Bash:`./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="c0dd1-149">For example, in Bash: `./my_storage_sample.sh`</span></span>

<span data-ttu-id="c0dd1-150">Ziet u uitvoer die vergelijkbaar is met het volgende, en de  **\<destination_file\>**  u hebt opgegeven in het script moet worden weergegeven op de lokale computer.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-150">You should see output similar to the following, and the **\<destination_file\>** you specified in the script should appear on your local computer.</span></span>

```
Creating the container...
{
  "created": true
}
Uploading the file...
Percent complete: %100.0
Listing the blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading the file...
Name
---------
README.md
Done
```

> [!TIP]
> <span data-ttu-id="c0dd1-151">De voorgaande uitvoer is in **tabel** indeling.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-151">The preceding output is in **table** format.</span></span> <span data-ttu-id="c0dd1-152">U kunt opgeven dat uitvoer indeling moet worden gebruikt door te geven de `--output` argument in de CLI-opdrachten of stel deze globaal met `az configure`.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-152">You can specify which output format to use by specifying the `--output` argument in your CLI commands, or set it globally using `az configure`.</span></span>
>

## <a name="manage-storage-accounts"></a><span data-ttu-id="c0dd1-153">Opslagaccounts beheren</span><span class="sxs-lookup"><span data-stu-id="c0dd1-153">Manage storage accounts</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="c0dd1-154">Een nieuw opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="c0dd1-154">Create a new storage account</span></span>
<span data-ttu-id="c0dd1-155">U hebt een opslagaccount nodig om Azure Storage te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-155">To use Azure Storage, you need a storage account.</span></span> <span data-ttu-id="c0dd1-156">U kunt een nieuw Azure-opslagaccount maken nadat u uw computer hebt geconfigureerd [verbinding maken met uw abonnement](#connect-to-your-azure-subscription).</span><span class="sxs-lookup"><span data-stu-id="c0dd1-156">You can create a new Azure Storage account after you've configured your computer to [connect to your subscription](#connect-to-your-azure-subscription).</span></span>

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* <span data-ttu-id="c0dd1-157">`--location`[Vereist]: locatie.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-157">`--location` [Required]: Location.</span></span> <span data-ttu-id="c0dd1-158">Bijvoorbeeld "VS-West'.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-158">For example, "West US".</span></span>
* <span data-ttu-id="c0dd1-159">`--name`[Vereist]: naam van het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-159">`--name` [Required]: The storage account name.</span></span> <span data-ttu-id="c0dd1-160">De naam moet 3 tot 24 tekens lang zijn, en gebruik alleen kleine letters alfanumerieke tekens.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-160">The name must be 3 to 24 characters in length, and use only lowercase alphanumeric characters.</span></span>
* <span data-ttu-id="c0dd1-161">`--resource-group`[Vereist]: naam van resourcegroep.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-161">`--resource-group` [Required]: Name of resource group.</span></span>
* <span data-ttu-id="c0dd1-162">`--sku`[Vereist]: de SKU-opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-162">`--sku` [Required]: The storage account SKU.</span></span> <span data-ttu-id="c0dd1-163">Toegestane waarden:</span><span class="sxs-lookup"><span data-stu-id="c0dd1-163">Allowed values:</span></span>
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a><span data-ttu-id="c0dd1-164">Azure storage-standaardaccount omgevingsvariabelen worden ingesteld</span><span class="sxs-lookup"><span data-stu-id="c0dd1-164">Set default Azure storage account environment variables</span></span>
<span data-ttu-id="c0dd1-165">U kunt meerdere opslagaccounts in uw Azure-abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-165">You can have multiple storage accounts in your Azure subscription.</span></span> <span data-ttu-id="c0dd1-166">Selecteer een van de twee moet worden gebruikt voor alle daaropvolgende opslag opdrachten, kunt u deze omgevingsvariabelen instellen:</span><span class="sxs-lookup"><span data-stu-id="c0dd1-166">To select one of them to use for all subsequent storage commands, you can set these environment variables:</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="c0dd1-167">Er is een andere manier om een standaardopslagaccount met behulp van een verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-167">Another way to set a default storage account is by using a connection string.</span></span> <span data-ttu-id="c0dd1-168">Eerst ophalen van de verbindingsreeks met het `show-connection-string` opdracht:</span><span class="sxs-lookup"><span data-stu-id="c0dd1-168">First, get the connection string with the `show-connection-string` command:</span></span>

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

<span data-ttu-id="c0dd1-169">Vervolgens kopieert u de verbindingsreeks van de uitvoer en stelt u de `AZURE_STORAGE_CONNECTION_STRING` omgevingsvariabele (mogelijk moet u de verbindingsreeks plaats tussen aanhalingstekens):</span><span class="sxs-lookup"><span data-stu-id="c0dd1-169">Then copy the output connection string and set the `AZURE_STORAGE_CONNECTION_STRING` environment variable (you might need to enclose the connection string in quotes):</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> <span data-ttu-id="c0dd1-170">Alle voorbeelden in de volgende secties van dit artikel wordt ervan uitgegaan dat u hebt ingesteld de `AZURE_STORAGE_ACCOUNT` en `AZURE_STORAGE_ACCESS_KEY` omgevingsvariabelen.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-170">All examples in the following sections of this article assume that you've set the `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY` environment variables.</span></span>
>

## <a name="create-and-manage-blobs"></a><span data-ttu-id="c0dd1-171">Maken en blobs beheren</span><span class="sxs-lookup"><span data-stu-id="c0dd1-171">Create and manage blobs</span></span>
<span data-ttu-id="c0dd1-172">Azure Blob storage is een service voor het opslaan van grote hoeveelheden ongestructureerde gegevens, zoals tekst of binaire gegevens, die toegankelijk zijn vanuit overal ter wereld via HTTP of HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-172">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="c0dd1-173">Deze sectie wordt ervan uitgegaan dat u al bekend met concepten voor Azure Blob-opslag bent.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-173">This section assumes that you are already familiar with Azure Blob storage concepts.</span></span> <span data-ttu-id="c0dd1-174">Zie voor gedetailleerde informatie [aan de slag met Azure Blob storage met .NET](../blobs/storage-dotnet-how-to-use-blobs.md) en [concepten van Blob-Service](/rest/api/storageservices/blob-service-concepts).</span><span class="sxs-lookup"><span data-stu-id="c0dd1-174">For detailed information, see [Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](/rest/api/storageservices/blob-service-concepts).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="c0dd1-175">Een container maken</span><span class="sxs-lookup"><span data-stu-id="c0dd1-175">Create a container</span></span>
<span data-ttu-id="c0dd1-176">Elke blob in Azure-opslag moet zich in een container.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-176">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="c0dd1-177">U kunt een container maken met behulp van de `az storage container create` opdracht:</span><span class="sxs-lookup"><span data-stu-id="c0dd1-177">You can create a container by using the `az storage container create` command:</span></span>

```azurecli
az storage container create --name <container_name>
```

<span data-ttu-id="c0dd1-178">U kunt een van drie niveaus van leestoegang voor een nieuwe container instellen door te geven de optionele `--public-access` argument:</span><span class="sxs-lookup"><span data-stu-id="c0dd1-178">You can set one of three levels of read access for a new container by specifying the optional  `--public-access` argument:</span></span>

* <span data-ttu-id="c0dd1-179">`off`(standaard): gegevens van de Container privé eigenaar van het account is.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-179">`off` (default): Container data is private to the account owner.</span></span>
* <span data-ttu-id="c0dd1-180">`blob`: Openbare leestoegang voor blobs.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-180">`blob`: Public read access for blobs.</span></span>
* <span data-ttu-id="c0dd1-181">`container`: Openbare lees- en toegang tot de volledige container.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-181">`container`: Public read and list access to the entire container.</span></span>

<span data-ttu-id="c0dd1-182">Zie voor meer informatie [anonieme leestoegang tot containers en blobs beheren](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="c0dd1-182">For more information, see [Manage anonymous read access to containers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>

### <a name="upload-a-blob-to-a-container"></a><span data-ttu-id="c0dd1-183">Een blob uploaden naar een container</span><span class="sxs-lookup"><span data-stu-id="c0dd1-183">Upload a blob to a container</span></span>
<span data-ttu-id="c0dd1-184">Azure Blob storage ondersteunt blok, toevoegen en pagina-blobs.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-184">Azure Blob storage supports block, append, and page blobs.</span></span> <span data-ttu-id="c0dd1-185">BLOB's uploaden naar een container met behulp van de `blob upload` opdracht:</span><span class="sxs-lookup"><span data-stu-id="c0dd1-185">Upload blobs to a container by using the `blob upload` command:</span></span>

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 <span data-ttu-id="c0dd1-186">Standaard de `blob upload` opdracht *.vhd bestanden uploadt naar de pagina-blobs of anderszins blok-blobs.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-186">By default, the `blob upload` command uploads *.vhd files to page blobs, or block blobs otherwise.</span></span> <span data-ttu-id="c0dd1-187">Als u wilt een ander type opgeven wanneer u een blob uploadt, kunt u de `--type` argument--toegestane waarden zijn `append`, `block`, en `page`.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-187">To specify another type when you upload a blob, you can use the `--type` argument--allowed values are `append`, `block`, and `page`.</span></span>

 <span data-ttu-id="c0dd1-188">Zie voor meer informatie over de typen andere blob- [blok-Blobs, toevoeg-Blobs en pagina-Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span><span class="sxs-lookup"><span data-stu-id="c0dd1-188">For more information on the different blob types, see [Understanding Block Blobs, Append Blobs, and Page Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span></span>


### <a name="download-a-blob-from-a-container"></a><span data-ttu-id="c0dd1-189">Een blob downloaden uit een container</span><span class="sxs-lookup"><span data-stu-id="c0dd1-189">Download a blob from a container</span></span>
<span data-ttu-id="c0dd1-190">In dit voorbeeld wordt getoond hoe een blob downloaden uit een container:</span><span class="sxs-lookup"><span data-stu-id="c0dd1-190">This example demonstrates how to download a blob from a container:</span></span>

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="c0dd1-191">De blobs in een container in een lijst weergeven</span><span class="sxs-lookup"><span data-stu-id="c0dd1-191">List the blobs in a container</span></span>

<span data-ttu-id="c0dd1-192">Lijst van de blobs in een container met de [lijst met blob storage az](/cli/azure/storage/blob#list) opdracht.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-192">List the blobs in a container with the [az storage blob list](/cli/azure/storage/blob#list) command.</span></span>

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a><span data-ttu-id="c0dd1-193">Blobs kopiëren</span><span class="sxs-lookup"><span data-stu-id="c0dd1-193">Copy blobs</span></span>
<span data-ttu-id="c0dd1-194">U kunt blobs binnen of tussen opslagaccounts en regio's asynchroon kopiëren.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-194">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="c0dd1-195">In het volgende voorbeeld ziet u hoe u blobs van één opslagaccount naar een ander kopieert.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-195">The following example demonstrates how to copy blobs from one storage account to another.</span></span> <span data-ttu-id="c0dd1-196">Eerst wordt er een container in het bronopslagaccount gemaakt en openbare leestoegang opgegeven voor de blobs.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-196">We first create a container in the source storage account, specifying public read-access for its blobs.</span></span> <span data-ttu-id="c0dd1-197">Daarna wordt er een bestand naar de container geüpload en wordt de blob vanuit die container naar een container in het doelopslagaccount gekopieerd.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-197">Next, we upload a file to the container, and finally, copy the blob from that container into a container in the destination storage account.</span></span>

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob to container in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account to destination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

<span data-ttu-id="c0dd1-198">In het bovenstaande voorbeeld worden de doelcontainer moet al bestaan in de storage-account van de bestemming voor de kopieerbewerking is mislukt.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-198">In the above example, the destination container must already exist in the destination storage account for the copy operation to succeed.</span></span> <span data-ttu-id="c0dd1-199">Bovendien moet de bron-blob die in het argument `--source-uri` is opgegeven, een SAS-token (Shared Access Signature) bevatten of openbaar toegankelijk zijn, zoals in dit voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-199">Additionally, the source blob specified in the `--source-uri` argument must either include a shared access signature (SAS) token, or be publicly accessible, as in this example.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="c0dd1-200">Een blob verwijderen</span><span class="sxs-lookup"><span data-stu-id="c0dd1-200">Delete a blob</span></span>
<span data-ttu-id="c0dd1-201">Als u wilt verwijderen van een blob, gebruiken de `blob delete` opdracht:</span><span class="sxs-lookup"><span data-stu-id="c0dd1-201">To delete a blob, use the `blob delete` command:</span></span>

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="c0dd1-202">Maken en beheren van bestandsshares</span><span class="sxs-lookup"><span data-stu-id="c0dd1-202">Create and manage file shares</span></span>
<span data-ttu-id="c0dd1-203">Azure File storage biedt gedeelde opslag voor toepassingen die gebruikmaken van het protocol Server Message Block (SMB).</span><span class="sxs-lookup"><span data-stu-id="c0dd1-203">Azure File storage offers shared storage for applications using the Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="c0dd1-204">Microsoft Azure virtuele machines en cloud-services, evenals de on-premises toepassingen kunnen bestandsgegevens via gekoppelde shares delen.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-204">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="c0dd1-205">U kunt bestandsshares en bestandsgegevens via de Azure CLI kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-205">You can manage file shares and file data via the Azure CLI.</span></span> <span data-ttu-id="c0dd1-206">Zie voor meer informatie over Azure File storage [aan de slag met Azure File storage in Windows](../storage-dotnet-how-to-use-files.md) of [Azure File storage gebruiken met Linux](../storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c0dd1-206">For more information on Azure File storage, see [Get started with Azure File storage on Windows](../storage-dotnet-how-to-use-files.md) or [How to use Azure File storage with Linux](../storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="c0dd1-207">Een bestandsshare maken</span><span class="sxs-lookup"><span data-stu-id="c0dd1-207">Create a file share</span></span>
<span data-ttu-id="c0dd1-208">Een Azure-bestandsshare is een SMB-bestandsshare in Azure.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-208">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="c0dd1-209">Alle mappen en bestanden moeten worden gemaakt in een bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-209">All directories and files must be created in a file share.</span></span> <span data-ttu-id="c0dd1-210">Een account kan een onbeperkt aantal shares bevatten en een bestandsshare kan een onbeperkt aantal bestanden, tot de capaciteitslimiet van het opslagaccount opslaan.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-210">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up to the capacity limits of the storage account.</span></span> <span data-ttu-id="c0dd1-211">Het volgende voorbeeld wordt een bestandsshare met de naam **mijnshare**.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-211">The following example creates a file share named **myshare**.</span></span>

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="c0dd1-212">Een map maken</span><span class="sxs-lookup"><span data-stu-id="c0dd1-212">Create a directory</span></span>
<span data-ttu-id="c0dd1-213">Een directory biedt een hiërarchische structuur in een Azure-bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-213">A directory provides a hierarchical structure in an Azure file share.</span></span> <span data-ttu-id="c0dd1-214">Het volgende voorbeeld wordt een map met de naam **myDir** in de bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-214">The following example creates a directory named **myDir** in the file share.</span></span>

```azurecli
az storage directory create --name myDir --share-name myshare
```

<span data-ttu-id="c0dd1-215">Een pad kan bijvoorbeeld meerdere niveaus bevatten **dir1/dir2**.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-215">A directory path can include multiple levels, for example **dir1/dir2**.</span></span> <span data-ttu-id="c0dd1-216">Echter, moet u ervoor zorgen dat alle bovenliggende mappen bestaan voordat u een submap maakt.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-216">However, you must ensure that all parent directories exist before creating a subdirectory.</span></span> <span data-ttu-id="c0dd1-217">Bijvoorbeeld: voor pad **dir1/dir2**, moet u eerst directory maken **dir1**, maak vervolgens de directory **dir2**.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-217">For example, for path **dir1/dir2**, you must first create directory **dir1**, then create directory **dir2**.</span></span>

### <a name="upload-a-local-file-to-a-share"></a><span data-ttu-id="c0dd1-218">Een lokaal bestand uploaden naar een share</span><span class="sxs-lookup"><span data-stu-id="c0dd1-218">Upload a local file to a share</span></span>
<span data-ttu-id="c0dd1-219">Het volgende voorbeeld wordt een bestand uit geüpload **~/temp/samplefile.txt** aan hoofdmap van de **mijnshare** bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-219">The following example uploads a file from **~/temp/samplefile.txt** to root of the **myshare** file share.</span></span> <span data-ttu-id="c0dd1-220">De `--source` argument Hiermee geeft u het bestaande lokale bestand te uploaden.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-220">The `--source` argument specifies the existing local file to upload.</span></span>

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

<span data-ttu-id="c0dd1-221">Als met maken van de directory, kunt u een pad in de share het bestand te uploaden naar een bestaande map in de share opgeven:</span><span class="sxs-lookup"><span data-stu-id="c0dd1-221">As with directory creation, you can specify a directory path within the share to upload the file to an existing directory within the share:</span></span>

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

<span data-ttu-id="c0dd1-222">Een bestand in de share mag maximaal 1 TB groot zijn.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-222">A file in the share can be up to 1 TB in size.</span></span>

### <a name="list-the-files-in-a-share"></a><span data-ttu-id="c0dd1-223">Lijst van de bestanden in een share</span><span class="sxs-lookup"><span data-stu-id="c0dd1-223">List the files in a share</span></span>
<span data-ttu-id="c0dd1-224">U kunt bestanden en mappen in een share weergeven met behulp van de `az storage file list` opdracht:</span><span class="sxs-lookup"><span data-stu-id="c0dd1-224">You can list files and directories in a share by using the `az storage file list` command:</span></span>

```azurecli
# List the files in the root of a share
az storage file list --share-name myshare --output table

# List the files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List the files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a><span data-ttu-id="c0dd1-225">Bestanden kopiëren</span><span class="sxs-lookup"><span data-stu-id="c0dd1-225">Copy files</span></span>      
<span data-ttu-id="c0dd1-226">U kunt een bestand kopiëren naar een ander bestand, een bestand naar een blob of een blob naar een bestand.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-226">You can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="c0dd1-227">Als u bijvoorbeeld een bestand te kopiëren naar een map in een andere share:</span><span class="sxs-lookup"><span data-stu-id="c0dd1-227">For example, to copy a file to a directory in a different share:</span></span>        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a><span data-ttu-id="c0dd1-228">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c0dd1-228">Next steps</span></span>
<span data-ttu-id="c0dd1-229">Hier volgen enkele aanvullende resources voor meer informatie over het werken met de Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="c0dd1-229">Here are some additional resources for learning more about working with the Azure CLI 2.0.</span></span>

* [<span data-ttu-id="c0dd1-230">Aan de slag met Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="c0dd1-230">Get started with Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="c0dd1-231">Azure CLI 2.0-opdrachtenreferentie</span><span class="sxs-lookup"><span data-stu-id="c0dd1-231">Azure CLI 2.0 command reference</span></span>](/cli/azure)
* [<span data-ttu-id="c0dd1-232">Azure CLI 2.0 op GitHub</span><span class="sxs-lookup"><span data-stu-id="c0dd1-232">Azure CLI 2.0 on GitHub</span></span>](https://github.com/Azure/azure-cli)
