---
title: aaaUsing hello Azure CLI 1.0 met Azure Storage | Microsoft Docs
description: Informatie over hoe toouse hello Azure-opdrachtregelinterface (Azure CLI) 1.0 met Azure Storage toocreate en storage-accounts beheren en werken met Azure BLOB's en bestanden. Hello Azure CLI is een hulpprogramma voor meerdere platforms
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
ms.openlocfilehash: 25e459403dde631741403c8722ed07beafac35c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-10-with-azure-storage"></a><span data-ttu-id="53bac-104">Hallo 1.0 van Azure CLI gebruiken met Azure Storage</span><span class="sxs-lookup"><span data-stu-id="53bac-104">Using hello Azure CLI 1.0 with Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="53bac-105">Overzicht</span><span class="sxs-lookup"><span data-stu-id="53bac-105">Overview</span></span>

<span data-ttu-id="53bac-106">Hello Azure CLI biedt een set van open-source platformoverschrijdende opdrachten voor het werken met hello Azure-Platform.</span><span class="sxs-lookup"><span data-stu-id="53bac-106">hello Azure CLI provides a set of open source, cross-platform commands for working with hello Azure Platform.</span></span> <span data-ttu-id="53bac-107">Het biedt veel van dezelfde functionaliteit in Hallo gevonden Hallo [Azure-portal](https://portal.azure.com) ook zo uitgebreid data access-functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="53bac-107">It provides much of hello same functionality found in hello [Azure portal](https://portal.azure.com) as well as rich data access functionality.</span></span>

<span data-ttu-id="53bac-108">In deze handleiding wordt besproken hoe toouse [Azure-opdrachtregelinterface (Azure CLI)](../../cli-install-nodejs.md) tooperform tal van ontwikkeling en het beheer van taken met Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="53bac-108">In this guide, we'll explore how toouse [Azure Command-Line Interface (Azure CLI)](../../cli-install-nodejs.md) tooperform a variety of development and administration tasks with Azure Storage.</span></span> <span data-ttu-id="53bac-109">Het is raadzaam dat u downloaden en installeren of upgraden van toohello nieuwste Azure CLI voordat u deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="53bac-109">We recommend that you download and install or upgrade toohello latest Azure CLI before using this guide.</span></span>

<span data-ttu-id="53bac-110">Deze handleiding wordt ervan uitgegaan dat u Hallo basisconcepten van Azure Storage begrijpt.</span><span class="sxs-lookup"><span data-stu-id="53bac-110">This guide assumes that you understand hello basic concepts of Azure Storage.</span></span> <span data-ttu-id="53bac-111">Hallo handleiding biedt een aantal scripts toodemonstrate Hallo gebruik van hello Azure CLI met Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="53bac-111">hello guide provides a number of scripts toodemonstrate hello usage of hello Azure CLI with Azure Storage.</span></span> <span data-ttu-id="53bac-112">Niet zeker tooupdate Hallo scriptvariabelen op basis van uw configuratie voordat elk script wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="53bac-112">Be sure tooupdate hello script variables based on your configuration before running each script.</span></span>

> [!NOTE]
> <span data-ttu-id="53bac-113">Hallo handleiding bevat hello Azure CLI opdracht en het script voorbeelden voor klassieke opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="53bac-113">hello guide provides hello Azure CLI command and script examples for classic storage accounts.</span></span> <span data-ttu-id="53bac-114">Zie [Using hello Azure CLI voor Mac, Linux en Windows met Azure Resource Management](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) voor Azure CLI-opdrachten voor Resource Manager-opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="53bac-114">See [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) for Azure CLI commands for Resource Manager storage accounts.</span></span>
>
>

[!INCLUDE [storage-cli-versions](../../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-hello-azure-cli-in-5-minutes"></a><span data-ttu-id="53bac-115">Aan de slag met Azure Storage en Azure CLI Hallo in vijf minuten</span><span class="sxs-lookup"><span data-stu-id="53bac-115">Get started with Azure Storage and hello Azure CLI in 5 minutes</span></span>
<span data-ttu-id="53bac-116">Deze handleiding gebruikt Ubuntu voor voorbeelden, maar andere platforms OS moeten op dezelfde manier worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="53bac-116">This guide uses Ubuntu for examples, but other OS platforms should perform similarly.</span></span>

<span data-ttu-id="53bac-117">**Nieuwe tooAzure:** ophalen van een Microsoft Azure-abonnement en een Microsoft-account die is gekoppeld aan dat abonnement.</span><span class="sxs-lookup"><span data-stu-id="53bac-117">**New tooAzure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="53bac-118">Zie voor informatie over Azure-Aankoopopties, [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/), [kopen opties](https://azure.microsoft.com/pricing/purchase-options/), en [lid biedt](https://azure.microsoft.com/pricing/member-offers/) (voor leden van MSDN, Microsoft Partner Network BizSpark en andere Microsoft-programma's).</span><span class="sxs-lookup"><span data-stu-id="53bac-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="53bac-119">Zie [beheerdersrollen toewijzen in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) voor meer informatie over Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="53bac-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="53bac-120">**Na het maken van een Microsoft Azure-abonnement en -account:**</span><span class="sxs-lookup"><span data-stu-id="53bac-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="53bac-121">Download en installeer Azure CLI Hallo instructies te volgen die worden beschreven in Hallo [installeren hello Azure CLI](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="53bac-121">Download and install hello Azure CLI following hello instructions outlined in [Install hello Azure CLI](../../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="53bac-122">Zodra hello Azure CLI is geïnstalleerd, kunt u zich kunt toouse hello azure opdracht vanaf de opdrachtregel-interface (Bash, Terminal-opdrachtprompt) tooaccess hello Azure CLI-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="53bac-122">Once hello Azure CLI has been installed, you will be able toouse hello azure command from your command-line interface (Bash, Terminal, Command prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="53bac-123">Type Hallo _azure_ opdracht en u ziet Hallo na uitvoer.</span><span class="sxs-lookup"><span data-stu-id="53bac-123">Type hello _azure_ command and you should see hello following output.</span></span>

    ![Azure opdrachtuitvoer](./media/storage-azure-cli/azure_command.png)   
3. <span data-ttu-id="53bac-125">Typ in het Hallo-opdrachtregelinterface `azure storage` toolist uit alle azure-opslag-opdrachten Hallo en krijgt u een eerste indruk Hallo functionaliteiten Hallo Azure CLI wordt verstrekt.</span><span class="sxs-lookup"><span data-stu-id="53bac-125">In hello command-line interface, type `azure storage` toolist out all hello azure storage commands and get a first impression of hello functionalities hello Azure CLI provides.</span></span> <span data-ttu-id="53bac-126">U kunt de naam van de opdracht met typen **-h** parameter (bijvoorbeeld `azure storage share create -h`) toosee details van de opdrachtsyntaxis.</span><span class="sxs-lookup"><span data-stu-id="53bac-126">You can type command name with **-h** parameter (for example, `azure storage share create -h`) toosee details of command syntax.</span></span>
4. <span data-ttu-id="53bac-127">Nu geven we u een eenvoudig script waarin basic Azure CLI-opdrachten tooaccess Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="53bac-127">Now, we'll give you a simple script that shows basic Azure CLI commands tooaccess Azure Storage.</span></span> <span data-ttu-id="53bac-128">Hallo script eerst vragen u de twee variabelen tooset voor uw opslagaccount en de sleutel.</span><span class="sxs-lookup"><span data-stu-id="53bac-128">hello script will first ask you tooset two variables for your storage account and key.</span></span> <span data-ttu-id="53bac-129">Hallo-script wordt vervolgens een nieuwe container in deze nieuwe opslagaccount maken en uploaden van een bestaande installatiekopie-bestand (blob) toothat container.</span><span class="sxs-lookup"><span data-stu-id="53bac-129">Then, hello script will create a new container in this new storage account and upload an existing image file (blob) toothat container.</span></span> <span data-ttu-id="53bac-130">Nadat het Hallo-script geeft een lijst van alle blobs in de container, zal deze Hallo installatiekopie bestand toohello doelmap dat op de lokale computer Hallo bestaat downloaden.</span><span class="sxs-lookup"><span data-stu-id="53bac-130">After hello script lists all blobs in that container, it will download hello image file toohello destination directory which exists on hello local computer.</span></span>

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating hello container..."
    azure storage container create $container_name

    echo "Uploading hello image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing hello blobs..."
    azure storage blob list $container_name

    echo "Downloading hello image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. <span data-ttu-id="53bac-131">Open uw voorkeur teksteditor (vim voor voorbeeld) in uw lokale computer.</span><span class="sxs-lookup"><span data-stu-id="53bac-131">In your local computer, open your preferred text editor (vim for example).</span></span> <span data-ttu-id="53bac-132">Typ Hallo hierboven script in een teksteditor.</span><span class="sxs-lookup"><span data-stu-id="53bac-132">Type hello above script into your text editor.</span></span>
6. <span data-ttu-id="53bac-133">U moet nu tooupdate Hallo scriptvariabelen op basis van uw configuratie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="53bac-133">Now, you need tooupdate hello script variables based on your configuration settings.</span></span>

   * <span data-ttu-id="53bac-134">**< Storage_account_name >** Hallo naam die in het Hallo-script gebruiken of voer een nieuwe naam voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="53bac-134">**<storage_account_name>** Use hello given name in hello script or enter a new name for your storage account.</span></span> <span data-ttu-id="53bac-135">**Belangrijk:** Hallo-naam van Hallo opslagaccount moet uniek zijn in Azure.</span><span class="sxs-lookup"><span data-stu-id="53bac-135">**Important:** hello name of hello storage account must be unique in Azure.</span></span> <span data-ttu-id="53bac-136">Er moet een kleine letter, te!</span><span class="sxs-lookup"><span data-stu-id="53bac-136">It must be lowercase, too!</span></span>
   * <span data-ttu-id="53bac-137">**< storage_account_key >** Hallo toegangssleutel van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="53bac-137">**<storage_account_key>** hello access key of your storage account.</span></span>
   * <span data-ttu-id="53bac-138">**< Container_name >** Hallo naam die in het Hallo-script gebruiken of voer een nieuwe naam voor de container.</span><span class="sxs-lookup"><span data-stu-id="53bac-138">**<container_name>** Use hello given name in hello script or enter a new name for your container.</span></span>
   * <span data-ttu-id="53bac-139">**< Image_to_upload >** Voer een pad tooa afbeelding op uw lokale computer, zoals: ' ~ / images/HelloWorld.png '.</span><span class="sxs-lookup"><span data-stu-id="53bac-139">**<image_to_upload>** Enter a path tooa picture on your local computer, such as: "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="53bac-140">**< Destination_folder >** Enter een pad tooa lokale directory toostore bestanden gedownload van Azure Storage, zoals: '~/downloadImages'.</span><span class="sxs-lookup"><span data-stu-id="53bac-140">**<destination_folder>** Enter a path tooa local directory toostore files downloaded from Azure Storage, such as: "~/downloadImages".</span></span>
7. <span data-ttu-id="53bac-141">Nadat u Hallo nodig variabelen in vim hebt bijgewerkt, drukt u op toetsencombinaties `ESC`, `:`, `wq!` toosave Hallo script.</span><span class="sxs-lookup"><span data-stu-id="53bac-141">After you've updated hello necessary variables in vim, press key combinations `ESC`, `:`, `wq!` toosave hello script.</span></span>
8. <span data-ttu-id="53bac-142">toorun dit script gewoon type Hallo Scriptbestandsnaam in Hallo bash-console.</span><span class="sxs-lookup"><span data-stu-id="53bac-142">toorun this script, simply type hello script file name in hello bash console.</span></span> <span data-ttu-id="53bac-143">Nadat u dit script wordt uitgevoerd, moet u een lokale doelmap met Hallo gedownload bestand hebben.</span><span class="sxs-lookup"><span data-stu-id="53bac-143">After this script runs, you should have a local destination folder that includes hello downloaded image file.</span></span> <span data-ttu-id="53bac-144">Hallo volgende schermafbeelding ziet u een voorbeeld van uitvoer:</span><span class="sxs-lookup"><span data-stu-id="53bac-144">hello following screenshot shows an example output:</span></span>

<span data-ttu-id="53bac-145">Nadat het Hallo-script wordt uitgevoerd, moet u een lokale doelmap met Hallo gedownload bestand hebben.</span><span class="sxs-lookup"><span data-stu-id="53bac-145">After hello script runs, you should have a local destination folder that includes hello downloaded image file.</span></span>

## <a name="manage-storage-accounts-with-hello-azure-cli"></a><span data-ttu-id="53bac-146">Storage-accounts met hello Azure CLI beheren</span><span class="sxs-lookup"><span data-stu-id="53bac-146">Manage storage accounts with hello Azure CLI</span></span>
### <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="53bac-147">Verbinding maken met tooyour Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="53bac-147">Connect tooyour Azure subscription</span></span>
<span data-ttu-id="53bac-148">Hoewel de meeste van Hallo opslag opdrachten zonder een Azure-abonnement werkt, wordt aangeraden u tooconnect tooyour abonnement hello Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="53bac-148">While most of hello storage commands will work without an Azure subscription, we recommend you tooconnect tooyour subscription from hello Azure CLI.</span></span> <span data-ttu-id="53bac-149">tooconfigure hello Azure CLI toowork bij uw abonnement, Hallo stappen in [tooan Azure-abonnement verbinden van hello Azure CLI](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="53bac-149">tooconfigure hello Azure CLI toowork with your subscription, follow hello steps in [Connect tooan Azure subscription from hello Azure CLI](../../xplat-cli-connect.md).</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="53bac-150">Een nieuw opslagaccount maken</span><span class="sxs-lookup"><span data-stu-id="53bac-150">Create a new storage account</span></span>
<span data-ttu-id="53bac-151">toouse Azure-opslag, moet u een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="53bac-151">toouse Azure storage, you will need a storage account.</span></span> <span data-ttu-id="53bac-152">Nadat u uw computer tooconnect tooyour-abonnement hebt geconfigureerd, kunt u een nieuwe Azure storage-account maken.</span><span class="sxs-lookup"><span data-stu-id="53bac-152">You can create a new Azure storage account after you have configured your computer tooconnect tooyour subscription.</span></span>

```azurecli
azure storage account create <account_name>
```

<span data-ttu-id="53bac-153">Hallo-naam van uw opslagaccount moet tussen 3 en 24 tekens lang zijn en alleen cijfers en kleine letters gebruiken.</span><span class="sxs-lookup"><span data-stu-id="53bac-153">hello name of your storage account must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a><span data-ttu-id="53bac-154">Een Azure storage-standaardaccount in omgevingsvariabelen instellen</span><span class="sxs-lookup"><span data-stu-id="53bac-154">Set a default Azure storage account in environment variables</span></span>
<span data-ttu-id="53bac-155">U kunt meerdere opslagaccounts hebben in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="53bac-155">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="53bac-156">U kunt kiezen één van beide en deze eigenschap instellen in Hallo omgevingsvariabelen voor alle Hallo-opslag-in Hallo dezelfde opdrachten sessie.</span><span class="sxs-lookup"><span data-stu-id="53bac-156">You can choose one of them and set it in hello environment variables for all hello storage commands in hello same session.</span></span> <span data-ttu-id="53bac-157">Hiermee kunt u toorun hello Azure CLI opslag opdrachten zonder op te geven Hallo storage-account en expliciet sleutel.</span><span class="sxs-lookup"><span data-stu-id="53bac-157">This enables you toorun hello Azure CLI storage commands without specifying hello storage account and key explicitly.</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="53bac-158">Verbindingsreeks maakt gebruik van een andere manier tooset storage-standaardaccount.</span><span class="sxs-lookup"><span data-stu-id="53bac-158">Another way tooset a default storage account is using connection string.</span></span> <span data-ttu-id="53bac-159">Ten eerste Hallo-verbindingsreeks ophalen door de opdracht:</span><span class="sxs-lookup"><span data-stu-id="53bac-159">Firstly get hello connection string by command:</span></span>

```azurecli
azure storage account connectionstring show <account_name>
```

<span data-ttu-id="53bac-160">Kopieer Hallo uitvoer verbindingsreeks en stel deze tooenvironment variabele:</span><span class="sxs-lookup"><span data-stu-id="53bac-160">Then copy hello output connection string and set it tooenvironment variable:</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a><span data-ttu-id="53bac-161">Maken en blobs beheren</span><span class="sxs-lookup"><span data-stu-id="53bac-161">Create and manage blobs</span></span>
<span data-ttu-id="53bac-162">Azure Blob storage is een service voor het opslaan van grote hoeveelheden ongestructureerde gegevens, zoals tekst of binaire gegevens, die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via HTTP of HTTPS.</span><span class="sxs-lookup"><span data-stu-id="53bac-162">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="53bac-163">Deze sectie wordt ervan uitgegaan dat u al bekend met concepten voor hello Azure Blob storage bent.</span><span class="sxs-lookup"><span data-stu-id="53bac-163">This section assumes that you are already familiar with hello Azure Blob storage concepts.</span></span> <span data-ttu-id="53bac-164">Zie voor gedetailleerde informatie [aan de slag met Azure Blob storage met .NET](../blobs/storage-dotnet-how-to-use-blobs.md) en [concepten van Blob-Service](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="53bac-164">For detailed information, see [Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="53bac-165">Een container maken</span><span class="sxs-lookup"><span data-stu-id="53bac-165">Create a container</span></span>
<span data-ttu-id="53bac-166">Elke blob in Azure-opslag moet zich in een container.</span><span class="sxs-lookup"><span data-stu-id="53bac-166">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="53bac-167">U kunt een persoonlijke container met Hallo maken `azure storage container create` opdracht:</span><span class="sxs-lookup"><span data-stu-id="53bac-167">You can create a private container using hello `azure storage container create` command:</span></span>

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> <span data-ttu-id="53bac-168">Er zijn drie niveaus van anonieme toegang voor lezen: **uit**, **Blob**, en **Container**.</span><span class="sxs-lookup"><span data-stu-id="53bac-168">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="53bac-169">tooprevent anonieme toegang tot tooblobs, setparameter Hallo machtiging te**uit**.</span><span class="sxs-lookup"><span data-stu-id="53bac-169">tooprevent anonymous access tooblobs, set hello Permission parameter too**Off**.</span></span> <span data-ttu-id="53bac-170">Standaard Hallo nieuwe container privé is en toegankelijk zijn alleen voor de accounteigenaar Hallo.</span><span class="sxs-lookup"><span data-stu-id="53bac-170">By default, hello new container is private and can be accessed only by hello account owner.</span></span> <span data-ttu-id="53bac-171">anonieme openbare tooallow lezen toegang tot tooblob bronnen, maar niet toocontainer metagegevens of toohello lijst met blobs in de container hello, stelt u Hallo machtiging parameter te**Blob**.</span><span class="sxs-lookup"><span data-stu-id="53bac-171">tooallow anonymous public read access tooblob resources, but not toocontainer metadata or toohello list of blobs in hello container, set hello Permission parameter too**Blob**.</span></span> <span data-ttu-id="53bac-172">volledige openbare tooallow lezen toegang tot tooblob bronnen, container metagegevens en Hallo lijst met blobs in de container hello, stelt u Hallo machtiging parameter te**Container**.</span><span class="sxs-lookup"><span data-stu-id="53bac-172">tooallow full public read access tooblob resources, container metadata, and hello list of blobs in hello container, set hello Permission parameter too**Container**.</span></span> <span data-ttu-id="53bac-173">Zie voor meer informatie [anonieme leestoegang toocontainers en blobs beheren](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="53bac-173">For more information, see [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>
>
>

### <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="53bac-174">Een blob uploaden naar een container</span><span class="sxs-lookup"><span data-stu-id="53bac-174">Upload a blob into a container</span></span>
<span data-ttu-id="53bac-175">Azure Blob Storage ondersteunt blok-blobs en pagina-blobs.</span><span class="sxs-lookup"><span data-stu-id="53bac-175">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="53bac-176">Zie voor meer informatie [blok-Blobs, toevoeg-Blobs en pagina-Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="53bac-176">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="53bac-177">tooupload blobs in tooa container, kunt u Hallo `azure storage blob upload`.</span><span class="sxs-lookup"><span data-stu-id="53bac-177">tooupload blobs in tooa container, you can use hello `azure storage blob upload`.</span></span> <span data-ttu-id="53bac-178">Standaard uploadt u deze opdracht Hallo lokale bestanden tooa blok-blob.</span><span class="sxs-lookup"><span data-stu-id="53bac-178">By default, this command uploads hello local files tooa block blob.</span></span> <span data-ttu-id="53bac-179">Hallo-type toospecify voor Hallo blob, kunt u Hallo `--blobtype` parameter.</span><span class="sxs-lookup"><span data-stu-id="53bac-179">toospecify hello type for hello blob, you can use hello `--blobtype` parameter.</span></span>

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a><span data-ttu-id="53bac-180">Blobs downloaden uit een container</span><span class="sxs-lookup"><span data-stu-id="53bac-180">Download blobs from a container</span></span>
<span data-ttu-id="53bac-181">Hallo volgende voorbeeld laat zien hoe toodownload blobs uit een container.</span><span class="sxs-lookup"><span data-stu-id="53bac-181">hello following example demonstrates how toodownload blobs from a container.</span></span>

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a><span data-ttu-id="53bac-182">Blobs kopiëren</span><span class="sxs-lookup"><span data-stu-id="53bac-182">Copy blobs</span></span>
<span data-ttu-id="53bac-183">U kunt blobs binnen of tussen opslagaccounts en regio's asynchroon kopiëren.</span><span class="sxs-lookup"><span data-stu-id="53bac-183">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="53bac-184">Hallo volgende voorbeeld laat zien hoe toocopy blobs uit één opslag tooanother account.</span><span class="sxs-lookup"><span data-stu-id="53bac-184">hello following example demonstrates how toocopy blobs from one storage account tooanother.</span></span> <span data-ttu-id="53bac-185">In dit voorbeeld maken we een container waarin blobs openbaar zijn, anoniem toegankelijk.</span><span class="sxs-lookup"><span data-stu-id="53bac-185">In this sample we create a container where blobs are publicly, anonymously accessible.</span></span>

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

<span data-ttu-id="53bac-186">Dit voorbeeld voert een asynchrone kopie.</span><span class="sxs-lookup"><span data-stu-id="53bac-186">This sample performs an asynchronous copy.</span></span> <span data-ttu-id="53bac-187">U kunt Hallo status van elke kopieerbewerking bewaken door het uitvoeren van Hallo `azure storage blob copy show` bewerking.</span><span class="sxs-lookup"><span data-stu-id="53bac-187">You can monitor hello status of each copy operation by running hello `azure storage blob copy show` operation.</span></span>

<span data-ttu-id="53bac-188">Houd er rekening mee dat Hallo bron-URL opgegeven voor de kopieerbewerking Hallo moet openbaar toegankelijk, of een SAS (shared access signature)-token omvatten.</span><span class="sxs-lookup"><span data-stu-id="53bac-188">Note that hello source URL provided for hello copy operation must either be publicly accessible, or include a SAS (shared access signature) token.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="53bac-189">Een blob verwijderen</span><span class="sxs-lookup"><span data-stu-id="53bac-189">Delete a blob</span></span>
<span data-ttu-id="53bac-190">toodelete een blob Hallo onder opdracht gebruiken:</span><span class="sxs-lookup"><span data-stu-id="53bac-190">toodelete a blob, use hello below command:</span></span>

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="53bac-191">Maken en beheren van bestandsshares</span><span class="sxs-lookup"><span data-stu-id="53bac-191">Create and manage file shares</span></span>
<span data-ttu-id="53bac-192">Azure File storage biedt gedeelde opslag voor toepassingen die gebruikmaken van Hallo standaard SMB-protocol.</span><span class="sxs-lookup"><span data-stu-id="53bac-192">Azure File storage offers shared storage for applications using hello standard SMB protocol.</span></span> <span data-ttu-id="53bac-193">Microsoft Azure virtuele machines en cloud-services, evenals de on-premises toepassingen kunnen bestandsgegevens via gekoppelde shares delen.</span><span class="sxs-lookup"><span data-stu-id="53bac-193">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="53bac-194">U kunt bestandsshares en bestandsgegevens via hello Azure CLI kunt beheren.</span><span class="sxs-lookup"><span data-stu-id="53bac-194">You can manage file shares and file data via hello Azure CLI.</span></span> <span data-ttu-id="53bac-195">Zie voor meer informatie over Azure File storage [aan de slag met Azure File storage in Windows](../storage-dotnet-how-to-use-files.md) of [hoe toouse Azure File storage met Linux](../storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="53bac-195">For more information on Azure File storage, see [Get started with Azure File storage on Windows](../storage-dotnet-how-to-use-files.md) or [How toouse Azure File storage with Linux](../storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="53bac-196">Een bestandsshare maken</span><span class="sxs-lookup"><span data-stu-id="53bac-196">Create a file share</span></span>
<span data-ttu-id="53bac-197">Een Azure-bestandsshare is een SMB-bestandsshare in Azure.</span><span class="sxs-lookup"><span data-stu-id="53bac-197">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="53bac-198">Alle mappen en bestanden moeten worden gemaakt in een bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="53bac-198">All directories and files must be created in a file share.</span></span> <span data-ttu-id="53bac-199">Een account kan een onbeperkt aantal shares bevatten en een bestandsshare kan een onbeperkt aantal bestanden van toohello capaciteitslimiet van het opslagaccount Hallo opslaan.</span><span class="sxs-lookup"><span data-stu-id="53bac-199">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up toohello capacity limits of hello storage account.</span></span> <span data-ttu-id="53bac-200">Hallo volgende voorbeeld wordt een bestandsshare met de naam **mijnshare**.</span><span class="sxs-lookup"><span data-stu-id="53bac-200">hello following example creates a file share named **myshare**.</span></span>

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="53bac-201">Een map maken</span><span class="sxs-lookup"><span data-stu-id="53bac-201">Create a directory</span></span>
<span data-ttu-id="53bac-202">Een directory biedt een optionele hiërarchische structuur voor een Azure-bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="53bac-202">A directory provides an optional hierarchical structure for an Azure file share.</span></span> <span data-ttu-id="53bac-203">Hallo volgende voorbeeld maakt u een map met de naam **myDir** in Hallo-bestandsshare.</span><span class="sxs-lookup"><span data-stu-id="53bac-203">hello following example creates a directory named **myDir** in hello file share.</span></span>

```azurecli
azure storage directory create myshare myDir
```

<span data-ttu-id="53bac-204">Opmerking die directorypad kan bestaan uit meerdere niveaus *bijvoorbeeld*, **een / b**.</span><span class="sxs-lookup"><span data-stu-id="53bac-204">Note that directory path can include multiple levels, *e.g.*, **a/b**.</span></span> <span data-ttu-id="53bac-205">Echter, moet u ervoor zorgen dat alle bovenliggende mappen bestaan.</span><span class="sxs-lookup"><span data-stu-id="53bac-205">However, you must ensure that all parent directories exist.</span></span> <span data-ttu-id="53bac-206">Bijvoorbeeld: voor pad **een / b**, moet u directory **een** vervolgens Maak eerst map **b**.</span><span class="sxs-lookup"><span data-stu-id="53bac-206">For example, for path **a/b**, you must create directory **a** first, then create directory **b**.</span></span>

### <a name="upload-a-local-file-toodirectory"></a><span data-ttu-id="53bac-207">De toodirectory van een lokaal bestand uploaden</span><span class="sxs-lookup"><span data-stu-id="53bac-207">Upload a local file toodirectory</span></span>
<span data-ttu-id="53bac-208">Hallo volgende voorbeeld wordt een bestand geüpload vanuit **~/temp/samplefile.txt** toohello **myDir** directory.</span><span class="sxs-lookup"><span data-stu-id="53bac-208">hello following example uploads a file from **~/temp/samplefile.txt** toohello **myDir** directory.</span></span> <span data-ttu-id="53bac-209">Hallo-bestandspad bewerken zodat deze tooa geldig bestand op uw lokale machine verwijst:</span><span class="sxs-lookup"><span data-stu-id="53bac-209">Edit hello file path so that it points tooa valid file on your local machine:</span></span>

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

<span data-ttu-id="53bac-210">Let op: een bestand in de share Hallo kan up too1 TB groot zijn.</span><span class="sxs-lookup"><span data-stu-id="53bac-210">Note that a file in hello share can be up too1 TB in size.</span></span>

### <a name="list-hello-files-in-hello-share-root-or-directory"></a><span data-ttu-id="53bac-211">Hallo-bestanden in basis Hallo-share of map weergeven</span><span class="sxs-lookup"><span data-stu-id="53bac-211">List hello files in hello share root or directory</span></span>
<span data-ttu-id="53bac-212">U kunt Hallo bestanden en submappen in de hoofdmap van een share of map met behulp van de volgende opdracht Hallo weergeven:</span><span class="sxs-lookup"><span data-stu-id="53bac-212">You can list hello files and subdirectories in a share root or a directory using hello following command:</span></span>

```azurecli
azure storage file list myshare myDir
```

<span data-ttu-id="53bac-213">Houd er rekening mee dat Hallo mapnaam is optioneel voor Hallo aanbieding bewerking.</span><span class="sxs-lookup"><span data-stu-id="53bac-213">Note that hello directory name is optional for hello listing operation.</span></span> <span data-ttu-id="53bac-214">Als u dit weglaat, weergegeven Hallo Hallo inhoud van de hoofdmap Hallo van Hallo share.</span><span class="sxs-lookup"><span data-stu-id="53bac-214">If omitted, hello command lists hello contents of hello root directory of hello share.</span></span>

### <a name="copy-files"></a><span data-ttu-id="53bac-215">Bestanden kopiëren</span><span class="sxs-lookup"><span data-stu-id="53bac-215">Copy files</span></span>
<span data-ttu-id="53bac-216">Vanaf versie 0.9.8 van Azure CLI, kunt u een bestand tooanother, een bestand tooa blob of een blob tooa-bestand kopiëren.</span><span class="sxs-lookup"><span data-stu-id="53bac-216">Beginning with version 0.9.8 of Azure CLI, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="53bac-217">Hieronder ziet u hoe tooperform die deze kopiëren bewerkingen met behulp van de CLI-opdrachten.</span><span class="sxs-lookup"><span data-stu-id="53bac-217">Below we demonstrate how tooperform these copy operations using CLI commands.</span></span> <span data-ttu-id="53bac-218">een nieuwe map toohello toocopy:</span><span class="sxs-lookup"><span data-stu-id="53bac-218">toocopy a file toohello new directory:</span></span>

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

<span data-ttu-id="53bac-219">een map voor blob tooa toocopy:</span><span class="sxs-lookup"><span data-stu-id="53bac-219">toocopy a blob tooa file directory:</span></span>

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a><span data-ttu-id="53bac-220">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="53bac-220">Next Steps</span></span>

<span data-ttu-id="53bac-221">U vindt de Azure CLI 1.0-opdrachtregelprogramma voor het werken met opslagbronnen hier:</span><span class="sxs-lookup"><span data-stu-id="53bac-221">You can find Azure CLI 1.0 command reference for working with Storage resources here:</span></span>

* [<span data-ttu-id="53bac-222">Azure CLI-opdrachten in de modus Resource Manager</span><span class="sxs-lookup"><span data-stu-id="53bac-222">Azure CLI commands in Resource Manager mode</span></span>](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [<span data-ttu-id="53bac-223">Azure CLI-opdrachten in de Azure Service Management-modus</span><span class="sxs-lookup"><span data-stu-id="53bac-223">Azure CLI commands in Azure Service Management mode</span></span>](../../cli-install-nodejs.md)

<span data-ttu-id="53bac-224">U kunt ook graag tootry Hallo [Azure CLI 2.0](../storage-azure-cli.md), de volgende generatie CLI geschreven in Python, voor gebruik met Hallo Resource Manager-implementatiemodel.</span><span class="sxs-lookup"><span data-stu-id="53bac-224">You may also like tootry hello [Azure CLI 2.0](../storage-azure-cli.md), our next-generation CLI written in Python, for use with hello Resource Manager deployment model.</span></span>
