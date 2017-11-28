---
title: De Azure CLI 1.0 gebruiken met Azure Storage | Microsoft Docs
description: Informatie over het gebruik van de Azure-opdrachtregelinterface (Azure CLI) 1.0 met Azure Storage te maken en beheren van storage-accounts en werken met Azure BLOB's en bestanden. De Azure CLI is een hulpprogramma voor meerdere platforms
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: b502232a-e8f6-4d6c-befd-3476592e0e35
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: seguler
ms.openlocfilehash: b246d8813a41d353a9c0fa31fe838e025fc93046
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-cli-10-with-azure-storage"></a><span data-ttu-id="6c800-104">De Azure CLI 1.0 gebruiken met Azure Storage</span><span class="sxs-lookup"><span data-stu-id="6c800-104">Using the Azure CLI 1.0 with Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="6c800-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="6c800-105">Overview</span></span>

<span data-ttu-id="6c800-106">De Azure CLI biedt een set van open-source platformoverschrijdende opdrachten voor het werken met de Azure-Platform.</span><span class="sxs-lookup"><span data-stu-id="6c800-106">The Azure CLI provides a set of open source, cross-platform commands for working with the Azure Platform.</span></span> <span data-ttu-id="6c800-107">Het biedt veel van dezelfde functionaliteit gevonden in de [Azure-portal](https://portal.azure.com) ook zo uitgebreid data access-functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="6c800-107">It provides much of the same functionality found in the [Azure portal](https://portal.azure.com) as well as rich data access functionality.</span></span>

<span data-ttu-id="6c800-108">In deze handleiding wordt besproken voor het gebruik van [Azure-opdrachtregelinterface (Azure CLI)](../cli-install-nodejs.md) om uit te voeren een verscheidenheid aan taken voor ontwikkeling en het beheer met Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="6c800-108">In this guide, we'll explore how to use [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md) to perform a variety of development and administration tasks with Azure Storage.</span></span> <span data-ttu-id="6c800-109">U wordt aangeraden dat u downloaden en installeren of naar de nieuwste Azure CLI upgraden voordat u deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="6c800-109">We recommend that you download and install or upgrade to the latest Azure CLI before using this guide.</span></span>

<span data-ttu-id="6c800-110">Deze handleiding wordt ervan uitgegaan dat u de basisconcepten van Azure Storage begrijpt.</span><span class="sxs-lookup"><span data-stu-id="6c800-110">This guide assumes that you understand the basic concepts of Azure Storage.</span></span> <span data-ttu-id="6c800-111">De handleiding bevat een aantal scripts voor het demonstreren van het gebruik van de Azure CLI met Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="6c800-111">The guide provides a number of scripts to demonstrate the usage of the Azure CLI with Azure Storage.</span></span> <span data-ttu-id="6c800-112">Zorg ervoor dat de scriptvariabelen op basis van uw configuratie voordat elk script wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6c800-112">Be sure to update the script variables based on your configuration before running each script.</span></span>

> [!NOTE]
> <span data-ttu-id="6c800-113">De handleiding bevat de Azure CLI-opdracht en het script voorbeelden voor klassieke opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="6c800-113">The guide provides the Azure CLI command and script examples for classic storage accounts.</span></span> <span data-ttu-id="6c800-114">Zie [met de Azure CLI voor Mac, Linux en Windows met Azure Resource Management](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) voor Azure CLI-opdrachten voor Resource Manager-opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="6c800-114">See [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) for Azure CLI commands for Resource Manager storage accounts.</span></span>
>
>

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-the-azure-cli-in-5-minutes"></a><span data-ttu-id="6c800-115">Aan de slag met Azure Storage en Azure CLI in vijf minuten</span><span class="sxs-lookup"><span data-stu-id="6c800-115">Get started with Azure Storage and the Azure CLI in 5 minutes</span></span>
<span data-ttu-id="6c800-116">Deze handleiding gebruikt Ubuntu voor voorbeelden, maar andere platforms OS moeten op dezelfde manier worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="6c800-116">This guide uses Ubuntu for examples, but other OS platforms should perform similarly.</span></span>

<span data-ttu-id="6c800-117">**Nieuwe naar Azure:** ophalen van een Microsoft Azure-abonnement en een Microsoft-account die is gekoppeld aan dat abonnement.</span><span class="sxs-lookup"><span data-stu-id="6c800-117">**New to Azure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="6c800-118">Zie voor informatie over Azure-Aankoopopties, [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/), [kopen opties](https://azure.microsoft.com/pricing/purchase-options/), en [lid biedt](https://azure.microsoft.com/pricing/member-offers/) (voor leden van MSDN, Microsoft Partner Network BizSpark en andere Microsoft-programma's).</span><span class="sxs-lookup"><span data-stu-id="6c800-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="6c800-119">Zie [beheerdersrollen toewijzen in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) voor meer informatie over Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="6c800-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="6c800-120">**Na het maken van een Microsoft Azure-abonnement en -account:**</span><span class="sxs-lookup"><span data-stu-id="6c800-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="6c800-121">Download en installeer de Azure CLI de aanwijzingen in [Azure CLI installeren](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="6c800-121">Download and install the Azure CLI following the instructions outlined in [Install the Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="6c800-122">Zodra de Azure CLI is geïnstalleerd, zich u op de azure-opdracht van de opdrachtregelinterface (Bash, Terminal-opdrachtprompt) voor toegang tot de Azure CLI-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="6c800-122">Once the Azure CLI has been installed, you will be able to use the azure command from your command-line interface (Bash, Terminal, Command prompt) to access the Azure CLI commands.</span></span> <span data-ttu-id="6c800-123">Typ de _azure_ opdracht en u ziet de volgende uitvoer.</span><span class="sxs-lookup"><span data-stu-id="6c800-123">Type the _azure_ command and you should see the following output.</span></span>

    ![Azure opdrachtuitvoer][Image1]
3. <span data-ttu-id="6c800-125">Typ in de opdrachtregelinterface `azure storage` lijst met alle azure-opslag-opdrachten en ophalen van een eerste indruk van de functies van de Azure CLI biedt.</span><span class="sxs-lookup"><span data-stu-id="6c800-125">In the command-line interface, type `azure storage` to list out all the azure storage commands and get a first impression of the functionalities the Azure CLI provides.</span></span> <span data-ttu-id="6c800-126">U kunt de naam van de opdracht met typen **-h** parameter (bijvoorbeeld `azure storage share create -h`) om de details van de opdrachtsyntaxis te bekijken.</span><span class="sxs-lookup"><span data-stu-id="6c800-126">You can type command name with **-h** parameter (for example, `azure storage share create -h`) to see details of command syntax.</span></span>
4. <span data-ttu-id="6c800-127">Nu geven we u een eenvoudig script waarin basic Azure CLI-opdrachten voor toegang tot Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="6c800-127">Now, we'll give you a simple script that shows basic Azure CLI commands to access Azure Storage.</span></span> <span data-ttu-id="6c800-128">Het script eerst vragen u twee variabelen voor uw opslagaccount en de sleutel instellen.</span><span class="sxs-lookup"><span data-stu-id="6c800-128">The script will first ask you to set two variables for your storage account and key.</span></span> <span data-ttu-id="6c800-129">Het script wordt vervolgens een nieuwe container in deze nieuwe opslagaccount maken en uploaden van een bestaand installatiekopiebestand (blob) op die container.</span><span class="sxs-lookup"><span data-stu-id="6c800-129">Then, the script will create a new container in this new storage account and upload an existing image file (blob) to that container.</span></span> <span data-ttu-id="6c800-130">Nadat het script geeft een lijst van alle blobs in de container, zal deze het installatiekopiebestand downloaden naar de doelmap dat op de lokale computer bestaat.</span><span class="sxs-lookup"><span data-stu-id="6c800-130">After the script lists all blobs in that container, it will download the image file to the destination directory which exists on the local computer.</span></span>

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating the container..."
    azure storage container create $container_name

    echo "Uploading the image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing the blobs..."
    azure storage blob list $container_name

    echo "Downloading the image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. <span data-ttu-id="6c800-131">Open uw voorkeur teksteditor (vim voor voorbeeld) in uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="6c800-131">In your local computer, open your preferred text editor (vim for example).</span></span> <span data-ttu-id="6c800-132">Typ het bovenstaande script in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="6c800-132">Type the above script into your text editor.</span></span>
6. <span data-ttu-id="6c800-133">Nu moet u de scriptvariabelen op basis van uw configuratie-instellingen bijwerken.</span><span class="sxs-lookup"><span data-stu-id="6c800-133">Now, you need to update the script variables based on your configuration settings.</span></span>

   * <span data-ttu-id="6c800-134">**< Storage_account_name >** de voornaam in het script of geef een nieuwe naam voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="6c800-134">**<storage_account_name>** Use the given name in the script or enter a new name for your storage account.</span></span> <span data-ttu-id="6c800-135">**Belangrijk:** de naam van het opslagaccount moet uniek zijn in Azure.</span><span class="sxs-lookup"><span data-stu-id="6c800-135">**Important:** The name of the storage account must be unique in Azure.</span></span> <span data-ttu-id="6c800-136">Er moet een kleine letter, te!</span><span class="sxs-lookup"><span data-stu-id="6c800-136">It must be lowercase, too!</span></span>
   * <span data-ttu-id="6c800-137">**< Storage_account_key >** de toegangssleutel van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="6c800-137">**<storage_account_key>** The access key of your storage account.</span></span>
   * <span data-ttu-id="6c800-138">**< Container_name >** de voornaam in het script of geef een nieuwe naam voor de container.</span><span class="sxs-lookup"><span data-stu-id="6c800-138">**<container_name>** Use the given name in the script or enter a new name for your container.</span></span>
   * <span data-ttu-id="6c800-139">**< Image_to_upload >** Voer een pad naar een afbeelding op uw lokale computer, zoals: ' ~ / images/HelloWorld.png '.</span><span class="sxs-lookup"><span data-stu-id="6c800-139">**<image_to_upload>** Enter a path to a picture on your local computer, such as: "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="6c800-140">**< Destination_folder >** een pad opgeven naar een lokale map voor het opslaan van bestanden die zijn gedownload van Azure Storage, zoals: '~/downloadImages'.</span><span class="sxs-lookup"><span data-stu-id="6c800-140">**<destination_folder>** Enter a path to a local directory to store files downloaded from Azure Storage, such as: "~/downloadImages".</span></span>
7. <span data-ttu-id="6c800-141">Nadat u de benodigde variabelen in vim hebt bijgewerkt, drukt u op toetsencombinaties `ESC`, `:`, `wq!` om op te slaan van het script.</span><span class="sxs-lookup"><span data-stu-id="6c800-141">After you've updated the necessary variables in vim, press key combinations `ESC`, `:`, `wq!` to save the script.</span></span>
8. <span data-ttu-id="6c800-142">Als u wilt dit script uitvoert, typt u de naam van het script in de console bash.</span><span class="sxs-lookup"><span data-stu-id="6c800-142">To run this script, simply type the script file name in the bash console.</span></span> <span data-ttu-id="6c800-143">Nadat u dit script wordt uitgevoerd, moet u een lokale doelmap met het gedownloade bestand hebben.</span><span class="sxs-lookup"><span data-stu-id="6c800-143">After this script runs, you should have a local destination folder that includes the downloaded image file.</span></span> <span data-ttu-id="6c800-144">De volgende schermafbeelding ziet een voorbeeld van uitvoer:</span><span class="sxs-lookup"><span data-stu-id="6c800-144">The following screenshot shows an example output:</span></span>

<span data-ttu-id="6c800-145">Nadat het script wordt uitgevoerd, moet u een lokale doelmap met het gedownloade bestand hebben.</span><span class="sxs-lookup"><span data-stu-id="6c800-145">After the script runs, you should have a local destination folder that includes the downloaded image file.</span></span>

## <a name="manage-storage-accounts-with-the-azure-cli"></a><span data-ttu-id="6c800-146">Storage-accounts met de Azure CLI beheren</span><span class="sxs-lookup"><span data-stu-id="6c800-146">Manage storage accounts with the Azure CLI</span></span>
### <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="6c800-147">Verbinding maken met uw Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="6c800-147">Connect to your Azure subscription</span></span>
<span data-ttu-id="6c800-148">Hoewel de meeste van de opdrachten opslag zonder een Azure-abonnement werkt, wordt aangeraden u verbinding maken met uw abonnement met Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="6c800-148">While most of the storage commands will work without an Azure subscription, we recommend you to connect to your subscription from the Azure CLI.</span></span> <span data-ttu-id="6c800-149">Volg de stappen in de Azure CLI werkt met uw abonnement configureren [verbinding maken met een Azure-abonnement met de Azure CLI](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="6c800-149">To configure the Azure CLI to work with your subscription, follow the steps in [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="6c800-150">Een nieuw opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="6c800-150">Create a new storage account</span></span>
<span data-ttu-id="6c800-151">Voor het gebruik van Azure-opslag, moet u een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="6c800-151">To use Azure storage, you will need a storage account.</span></span> <span data-ttu-id="6c800-152">Nadat u uw computer verbinding maken met uw abonnement hebt geconfigureerd, kunt u een nieuwe Azure storage-account maken.</span><span class="sxs-lookup"><span data-stu-id="6c800-152">You can create a new Azure storage account after you have configured your computer to connect to your subscription.</span></span>

```azurecli
azure storage account create <account_name>
```

<span data-ttu-id="6c800-153">De naam van uw opslagaccount moet tussen 3 en 24 tekens lang zijn en alleen cijfers en kleine letters te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="6c800-153">The name of your storage account must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a><span data-ttu-id="6c800-154">Een Azure storage-standaardaccount in omgevingsvariabelen instellen</span><span class="sxs-lookup"><span data-stu-id="6c800-154">Set a default Azure storage account in environment variables</span></span>
<span data-ttu-id="6c800-155">U kunt meerdere opslagaccounts hebben in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="6c800-155">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="6c800-156">U kunt kiezen één van deze en stel deze in de omgevingsvariabelen voor alle opslag-opdrachten in dezelfde sessie.</span><span class="sxs-lookup"><span data-stu-id="6c800-156">You can choose one of them and set it in the environment variables for all the storage commands in the same session.</span></span> <span data-ttu-id="6c800-157">Hiermee kunt u voor het uitvoeren van de Azure CLI-opdrachten voor opslag zonder op te geven van het opslagaccount en expliciet sleutel.</span><span class="sxs-lookup"><span data-stu-id="6c800-157">This enables you to run the Azure CLI storage commands without specifying the storage account and key explicitly.</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="6c800-158">Verbindingsreeks maakt gebruik van een andere manier om een storage-standaardaccount.</span><span class="sxs-lookup"><span data-stu-id="6c800-158">Another way to set a default storage account is using connection string.</span></span> <span data-ttu-id="6c800-159">Ten eerste de verbindingsreeks ophalen door de opdracht:</span><span class="sxs-lookup"><span data-stu-id="6c800-159">Firstly get the connection string by command:</span></span>

```azurecli
azure storage account connectionstring show <account_name>
```

<span data-ttu-id="6c800-160">Vervolgens Kopieer de verbindingsreeks van de uitvoer en stel deze in op de omgevingsvariabele:</span><span class="sxs-lookup"><span data-stu-id="6c800-160">Then copy the output connection string and set it to environment variable:</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a><span data-ttu-id="6c800-161">Maken en blobs beheren</span><span class="sxs-lookup"><span data-stu-id="6c800-161">Create and manage blobs</span></span>
<span data-ttu-id="6c800-162">Azure Blob storage is een service voor het opslaan van grote hoeveelheden ongestructureerde gegevens, zoals tekst of binaire gegevens, die toegankelijk zijn vanuit overal ter wereld via HTTP of HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6c800-162">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="6c800-163">Deze sectie wordt ervan uitgegaan dat u al bekend met de Azure Blob storage-concepten bent.</span><span class="sxs-lookup"><span data-stu-id="6c800-163">This section assumes that you are already familiar with the Azure Blob storage concepts.</span></span> <span data-ttu-id="6c800-164">Zie voor gedetailleerde informatie [aan de slag met Azure Blob storage met .NET](storage-dotnet-how-to-use-blobs.md) en [concepten van Blob-Service](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="6c800-164">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="6c800-165">Een container maken</span><span class="sxs-lookup"><span data-stu-id="6c800-165">Create a container</span></span>
<span data-ttu-id="6c800-166">Elke blob in Azure-opslag moet zich in een container.</span><span class="sxs-lookup"><span data-stu-id="6c800-166">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="6c800-167">U kunt maken met een privé-container met de `azure storage container create` opdracht:</span><span class="sxs-lookup"><span data-stu-id="6c800-167">You can create a private container using the `azure storage container create` command:</span></span>

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> <span data-ttu-id="6c800-168">Er zijn drie niveaus van anonieme toegang voor lezen: **uit**, **Blob**, en **Container**.</span><span class="sxs-lookup"><span data-stu-id="6c800-168">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="6c800-169">Als u wilt voorkomen dat anonieme toegang tot blobs, stelt u de machtiging-parameter in op **uit**.</span><span class="sxs-lookup"><span data-stu-id="6c800-169">To prevent anonymous access to blobs, set the Permission parameter to **Off**.</span></span> <span data-ttu-id="6c800-170">Standaard worden de nieuwe container privé is en kan alleen worden geopend door de eigenaar van het account.</span><span class="sxs-lookup"><span data-stu-id="6c800-170">By default, the new container is private and can be accessed only by the account owner.</span></span> <span data-ttu-id="6c800-171">Anonieme toegang toestaan openbare leestoegang tot blob-bronnen, maar niet aan de metagegevens van de container of aan de lijst met blobs in de container, stelt u de parameter machtiging op **Blob**.</span><span class="sxs-lookup"><span data-stu-id="6c800-171">To allow anonymous public read access to blob resources, but not to container metadata or to the list of blobs in the container, set the Permission parameter to **Blob**.</span></span> <span data-ttu-id="6c800-172">Stel de parameter machtiging op wilt toestaan volledige openbare leestoegang tot de blob-bronnen, container metagegevens en de lijst met blobs in de container, **Container**.</span><span class="sxs-lookup"><span data-stu-id="6c800-172">To allow full public read access to blob resources, container metadata, and the list of blobs in the container, set the Permission parameter to **Container**.</span></span> <span data-ttu-id="6c800-173">Zie voor meer informatie [anonieme leestoegang tot containers en blobs beheren](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="6c800-173">For more information, see [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>
>
>

### <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="6c800-174">Een blob uploaden naar een container</span><span class="sxs-lookup"><span data-stu-id="6c800-174">Upload a blob into a container</span></span>
<span data-ttu-id="6c800-175">Azure Blob Storage ondersteunt blok-blobs en pagina-blobs.</span><span class="sxs-lookup"><span data-stu-id="6c800-175">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="6c800-176">Zie voor meer informatie [blok-Blobs, toevoeg-Blobs en pagina-Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="6c800-176">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="6c800-177">Blobs in als u wilt uploaden een container, kunt u de `azure storage blob upload`.</span><span class="sxs-lookup"><span data-stu-id="6c800-177">To upload blobs in to a container, you can use the `azure storage blob upload`.</span></span> <span data-ttu-id="6c800-178">Standaard wordt met deze opdracht de lokale bestanden naar een blok-blob geüpload.</span><span class="sxs-lookup"><span data-stu-id="6c800-178">By default, this command uploads the local files to a block blob.</span></span> <span data-ttu-id="6c800-179">Als u wilt opgeven welk type voor de blob, kunt u de `--blobtype` parameter.</span><span class="sxs-lookup"><span data-stu-id="6c800-179">To specify the type for the blob, you can use the `--blobtype` parameter.</span></span>

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a><span data-ttu-id="6c800-180">Blobs downloaden uit een container</span><span class="sxs-lookup"><span data-stu-id="6c800-180">Download blobs from a container</span></span>
<span data-ttu-id="6c800-181">Het volgende voorbeeld laat zien hoe blobs downloaden uit een container.</span><span class="sxs-lookup"><span data-stu-id="6c800-181">The following example demonstrates how to download blobs from a container.</span></span>

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a><span data-ttu-id="6c800-182">Blobs kopiëren</span><span class="sxs-lookup"><span data-stu-id="6c800-182">Copy blobs</span></span>
<span data-ttu-id="6c800-183">U kunt blobs binnen of tussen opslagaccounts en regio's asynchroon kopiëren.</span><span class="sxs-lookup"><span data-stu-id="6c800-183">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="6c800-184">In het volgende voorbeeld ziet u hoe u blobs van één opslagaccount naar een ander kopieert.</span><span class="sxs-lookup"><span data-stu-id="6c800-184">The following example demonstrates how to copy blobs from one storage account to another.</span></span> <span data-ttu-id="6c800-185">In dit voorbeeld maken we een container waarin blobs openbaar zijn, anoniem toegankelijk.</span><span class="sxs-lookup"><span data-stu-id="6c800-185">In this sample we create a container where blobs are publicly, anonymously accessible.</span></span>

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

<span data-ttu-id="6c800-186">Dit voorbeeld voert een asynchrone kopie.</span><span class="sxs-lookup"><span data-stu-id="6c800-186">This sample performs an asynchronous copy.</span></span> <span data-ttu-id="6c800-187">U kunt de status van elke kopieerbewerking bewaken door het uitvoeren van de `azure storage blob copy show` bewerking.</span><span class="sxs-lookup"><span data-stu-id="6c800-187">You can monitor the status of each copy operation by running the `azure storage blob copy show` operation.</span></span>

<span data-ttu-id="6c800-188">Let op de bron-URL voor de kopieerbewerking opgegeven moet openbaar toegankelijk, of een SAS (shared access signature)-token omvatten.</span><span class="sxs-lookup"><span data-stu-id="6c800-188">Note that the source URL provided for the copy operation must either be publicly accessible, or include a SAS (shared access signature) token.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="6c800-189">Een blob verwijderen</span><span class="sxs-lookup"><span data-stu-id="6c800-189">Delete a blob</span></span>
<span data-ttu-id="6c800-190">Als u wilt verwijderen van een blob, gebruiken de onderstaande opdracht:</span><span class="sxs-lookup"><span data-stu-id="6c800-190">To delete a blob, use the below command:</span></span>

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="6c800-191">Maken en beheren van bestandsshares</span><span class="sxs-lookup"><span data-stu-id="6c800-191">Create and manage file shares</span></span>
<span data-ttu-id="6c800-192">Azure File storage biedt gedeelde opslag voor toepassingen die gebruikmaken van het standaard SMB-protocol.</span><span class="sxs-lookup"><span data-stu-id="6c800-192">Azure File storage offers shared storage for applications using the standard SMB protocol.</span></span> <span data-ttu-id="6c800-193">Microsoft Azure virtuele machines en cloud-services, evenals de on-premises toepassingen kunnen bestandsgegevens via gekoppelde shares delen.</span><span class="sxs-lookup"><span data-stu-id="6c800-193">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="6c800-194">U kunt bestandsshares en bestandsgegevens via de Azure CLI kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="6c800-194">You can manage file shares and file data via the Azure CLI.</span></span> <span data-ttu-id="6c800-195">Zie voor meer informatie over Azure File storage [aan de slag met Azure File storage in Windows](storage-dotnet-how-to-use-files.md) of [Azure File storage gebruiken met Linux](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="6c800-195">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How to use Azure File storage with Linux](storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="6c800-196">Een bestandsshare maken</span><span class="sxs-lookup"><span data-stu-id="6c800-196">Create a file share</span></span>
<span data-ttu-id="6c800-197">Een Azure-bestandsshare is een SMB-bestandsshare in Azure.</span><span class="sxs-lookup"><span data-stu-id="6c800-197">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="6c800-198">Alle mappen en bestanden moeten worden gemaakt in een bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="6c800-198">All directories and files must be created in a file share.</span></span> <span data-ttu-id="6c800-199">Een account kan een onbeperkt aantal shares bevatten en een bestandsshare kan een onbeperkt aantal bestanden, tot de capaciteitslimiet van het opslagaccount opslaan.</span><span class="sxs-lookup"><span data-stu-id="6c800-199">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up to the capacity limits of the storage account.</span></span> <span data-ttu-id="6c800-200">Het volgende voorbeeld wordt een bestandsshare met de naam **mijnshare**.</span><span class="sxs-lookup"><span data-stu-id="6c800-200">The following example creates a file share named **myshare**.</span></span>

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="6c800-201">Een map maken</span><span class="sxs-lookup"><span data-stu-id="6c800-201">Create a directory</span></span>
<span data-ttu-id="6c800-202">Een directory biedt een optionele hiërarchische structuur voor een Azure-bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="6c800-202">A directory provides an optional hierarchical structure for an Azure file share.</span></span> <span data-ttu-id="6c800-203">Het volgende voorbeeld wordt een map met de naam **myDir** in de bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="6c800-203">The following example creates a directory named **myDir** in the file share.</span></span>

```azurecli
azure storage directory create myshare myDir
```

<span data-ttu-id="6c800-204">Opmerking die directorypad kan bestaan uit meerdere niveaus *bijvoorbeeld*, **een / b**.</span><span class="sxs-lookup"><span data-stu-id="6c800-204">Note that directory path can include multiple levels, *e.g.*, **a/b**.</span></span> <span data-ttu-id="6c800-205">Echter, moet u ervoor zorgen dat alle bovenliggende mappen bestaan.</span><span class="sxs-lookup"><span data-stu-id="6c800-205">However, you must ensure that all parent directories exist.</span></span> <span data-ttu-id="6c800-206">Bijvoorbeeld: voor pad **een / b**, moet u directory **een** vervolgens Maak eerst map **b**.</span><span class="sxs-lookup"><span data-stu-id="6c800-206">For example, for path **a/b**, you must create directory **a** first, then create directory **b**.</span></span>

### <a name="upload-a-local-file-to-directory"></a><span data-ttu-id="6c800-207">Een lokaal bestand uploaden naar de directory</span><span class="sxs-lookup"><span data-stu-id="6c800-207">Upload a local file to directory</span></span>
<span data-ttu-id="6c800-208">Het volgende voorbeeld wordt een bestand uit geüpload **~/temp/samplefile.txt** naar de **myDir** directory.</span><span class="sxs-lookup"><span data-stu-id="6c800-208">The following example uploads a file from **~/temp/samplefile.txt** to the **myDir** directory.</span></span> <span data-ttu-id="6c800-209">Bewerk het bestandspad, zodat deze naar een geldig bestand op uw lokale machine verwijst:</span><span class="sxs-lookup"><span data-stu-id="6c800-209">Edit the file path so that it points to a valid file on your local machine:</span></span>

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

<span data-ttu-id="6c800-210">Houd er rekening mee dat een bestand in de share mag maximaal 1 TB groot.</span><span class="sxs-lookup"><span data-stu-id="6c800-210">Note that a file in the share can be up to 1 TB in size.</span></span>

### <a name="list-the-files-in-the-share-root-or-directory"></a><span data-ttu-id="6c800-211">Lijst van de bestanden in de hoofdmap van de share of map</span><span class="sxs-lookup"><span data-stu-id="6c800-211">List the files in the share root or directory</span></span>
<span data-ttu-id="6c800-212">U kunt een lijst met de bestanden en submappen in de hoofdmap van een share of map met de volgende opdracht:</span><span class="sxs-lookup"><span data-stu-id="6c800-212">You can list the files and subdirectories in a share root or a directory using the following command:</span></span>

```azurecli
azure storage file list myshare myDir
```

<span data-ttu-id="6c800-213">Houd er rekening mee dat de mapnaam optioneel voor de bewerking van de aanbieding is.</span><span class="sxs-lookup"><span data-stu-id="6c800-213">Note that the directory name is optional for the listing operation.</span></span> <span data-ttu-id="6c800-214">Als u dit weglaat, wordt de opdracht de inhoud van de hoofdmap van de share.</span><span class="sxs-lookup"><span data-stu-id="6c800-214">If omitted, the command lists the contents of the root directory of the share.</span></span>

### <a name="copy-files"></a><span data-ttu-id="6c800-215">Bestanden kopiëren</span><span class="sxs-lookup"><span data-stu-id="6c800-215">Copy files</span></span>
<span data-ttu-id="6c800-216">Vanaf versie 0.9.8 van Azure CLI, kunt u een bestand kopiëren naar een ander bestand, een bestand naar een blob of een blob naar een bestand.</span><span class="sxs-lookup"><span data-stu-id="6c800-216">Beginning with version 0.9.8 of Azure CLI, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="6c800-217">Hieronder ziet u hoe u deze kopieerbewerkingen uitvoert met behulp van de CLI-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="6c800-217">Below we demonstrate how to perform these copy operations using CLI commands.</span></span> <span data-ttu-id="6c800-218">Een bestand naar de nieuwe map kopiëren:</span><span class="sxs-lookup"><span data-stu-id="6c800-218">To copy a file to the new directory:</span></span>

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

<span data-ttu-id="6c800-219">Een blob kopieert naar een map:</span><span class="sxs-lookup"><span data-stu-id="6c800-219">To copy a blob to a file directory:</span></span>

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a><span data-ttu-id="6c800-220">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="6c800-220">Next Steps</span></span>

<span data-ttu-id="6c800-221">U vindt de Azure CLI 1.0-opdrachtregelprogramma voor het werken met opslagbronnen hier:</span><span class="sxs-lookup"><span data-stu-id="6c800-221">You can find Azure CLI 1.0 command reference for working with Storage resources here:</span></span>

* [<span data-ttu-id="6c800-222">Azure CLI-opdrachten in de modus Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6c800-222">Azure CLI commands in Resource Manager mode</span></span>](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [<span data-ttu-id="6c800-223">Azure CLI-opdrachten in de Azure Service Management-modus</span><span class="sxs-lookup"><span data-stu-id="6c800-223">Azure CLI commands in Azure Service Management mode</span></span>](../cli-install-nodejs.md)

<span data-ttu-id="6c800-224">Ook wilt proberen de [Azure CLI 2.0](storage-azure-cli.md), de volgende generatie CLI geschreven in Python, voor gebruik met het implementatiemodel van Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6c800-224">You may also like to try the [Azure CLI 2.0](storage-azure-cli.md), our next-generation CLI written in Python, for use with the Resource Manager deployment model.</span></span>

[Image1]: ./media/storage-azure-cli/azure_command.png
