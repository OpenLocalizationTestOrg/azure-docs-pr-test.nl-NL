---
title: Azure PowerShell gebruiken met Azure Storage | Microsoft Docs
description: Informatie over het gebruik van de Azure PowerShell-cmdlets voor Azure Storage maken en beheren van opslagaccounts; werken met blobs, tabellen, wachtrijen en bestanden. configureren en storage analytics query en handtekeningen voor gedeelde toegang maken.
services: storage
documentationcenter: na
author: robinsh
manager: timlt
ms.assetid: f4704f58-abc6-4f89-8b6d-1b1659746f5a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/03/2017
ms.author: robinsh
ms.openlocfilehash: 51e3e93ebedd31370857e61a00139294bcee9237
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a><span data-ttu-id="5b682-103">Azure PowerShell gebruiken met Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5b682-103">Using Azure PowerShell with Azure Storage</span></span>
## <a name="overview"></a><span data-ttu-id="5b682-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="5b682-104">Overview</span></span>
<span data-ttu-id="5b682-105">Azure PowerShell is een module die biedt voor het beheren van Azure via Windows PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="5b682-105">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="5b682-106">Het is een op taken gebaseerde opdrachtregelshell en scripttaal die speciaal is ontworpen voor systeembeheer.</span><span class="sxs-lookup"><span data-stu-id="5b682-106">It is a task-based command-line shell and scripting language designed especially for system administration.</span></span> <span data-ttu-id="5b682-107">U kunt eenvoudig beheren en het beheer van uw Azure-services en toepassingen te automatiseren met PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b682-107">With PowerShell, you can easily control and automate the administration of your Azure services and applications.</span></span> <span data-ttu-id="5b682-108">U kunt bijvoorbeeld de cmdlets gebruiken om uit te voeren dezelfde taken die u via uitvoeren kunt de [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5b682-108">For example, you can use the cmdlets to perform the same tasks that you can perform through the [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="5b682-109">In deze handleiding wordt besproken voor het gebruik van de [Azure-opslag-Cmdlets](/powershell/module/azurerm.storage/#storage) om uit te voeren een verscheidenheid aan taken voor ontwikkeling en het beheer met Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="5b682-109">In this guide, we'll explore how to use the [Azure Storage Cmdlets](/powershell/module/azurerm.storage/#storage) to perform a variety of development and administration tasks with Azure Storage.</span></span>

<span data-ttu-id="5b682-110">Deze handleiding wordt ervan uitgegaan dat u ervaring met behulp van [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) en [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span><span class="sxs-lookup"><span data-stu-id="5b682-110">This guide assumes that you have prior experience using [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) and [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span></span> <span data-ttu-id="5b682-111">De handleiding bevat een aantal scripts voor het demonstreren van het gebruik van PowerShell met Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="5b682-111">The guide provides a number of scripts to demonstrate the usage of PowerShell with Azure Storage.</span></span> <span data-ttu-id="5b682-112">De scriptvariabelen op basis van uw configuratie voordat elk script wordt uitgevoerd, moet u bijwerken.</span><span class="sxs-lookup"><span data-stu-id="5b682-112">You should update the script variables based on your configuration before running each script.</span></span>

<span data-ttu-id="5b682-113">De eerste sectie in deze handleiding biedt een kijkje Azure Storage en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b682-113">The first section in this guide provides a quick glance at Azure Storage and PowerShell.</span></span> <span data-ttu-id="5b682-114">Voor gedetailleerde informatie en instructies starten vanuit de [vereisten voor het gebruik van Azure PowerShell met Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="5b682-114">For detailed information and instructions, start from the [Prerequisites for using Azure PowerShell with Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span></span>

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a><span data-ttu-id="5b682-115">Aan de slag met Azure Storage en PowerShell in vijf minuten</span><span class="sxs-lookup"><span data-stu-id="5b682-115">Getting started with Azure Storage and PowerShell in 5 minutes</span></span>
<span data-ttu-id="5b682-116">Deze sectie wordt beschreven hoe u toegang tot Azure Storage via PowerShell in vijf minuten.</span><span class="sxs-lookup"><span data-stu-id="5b682-116">This section shows you how to access Azure Storage via PowerShell in 5 minutes.</span></span>

<span data-ttu-id="5b682-117">**Nieuwe naar Azure:** ophalen van een Microsoft Azure-abonnement en een Microsoft-account die is gekoppeld aan dat abonnement.</span><span class="sxs-lookup"><span data-stu-id="5b682-117">**New to Azure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="5b682-118">Zie voor informatie over Azure-Aankoopopties, [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/), [kopen opties](https://azure.microsoft.com/pricing/purchase-options/), en [lid biedt](https://azure.microsoft.com/pricing/member-offers/) (voor leden van MSDN, Microsoft Partner Network BizSpark en andere Microsoft-programma's).</span><span class="sxs-lookup"><span data-stu-id="5b682-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="5b682-119">Zie [beheerdersrollen toewijzen in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) voor meer informatie over Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="5b682-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="5b682-120">**Na het maken van een Microsoft Azure-abonnement en -account:**</span><span class="sxs-lookup"><span data-stu-id="5b682-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="5b682-121">Download en installeer de meest recente [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span><span class="sxs-lookup"><span data-stu-id="5b682-121">Download and install the latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span></span>
2. <span data-ttu-id="5b682-122">Start Windows PowerShell Integrated Scripting Environment (ISE): In de lokale computer, gaat u naar de **Start** menu.</span><span class="sxs-lookup"><span data-stu-id="5b682-122">Start Windows PowerShell Integrated Scripting Environment (ISE): In your local computer, go to the **Start** menu.</span></span> <span data-ttu-id="5b682-123">Type **Systeembeheer** en klikt u op uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="5b682-123">Type **Administrative Tools** and click to run it.</span></span> <span data-ttu-id="5b682-124">In de **Systeembeheer** venster met de rechtermuisknop op **Windows PowerShell ISE**, klikt u op **als Administrator uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="5b682-124">In the **Administrative Tools** window, right-click **Windows PowerShell ISE**, click **Run as Administrator**.</span></span>
3. <span data-ttu-id="5b682-125">In **Windows PowerShell ISE**, klikt u op **bestand** > **nieuw** voor het maken van een script.</span><span class="sxs-lookup"><span data-stu-id="5b682-125">In **Windows PowerShell ISE**, click **File** > **New** to create a new script file.</span></span>
4. <span data-ttu-id="5b682-126">Nu geven we u een eenvoudig script waarin basic PowerShell-opdrachten voor toegang tot Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="5b682-126">Now, we'll give you a simple script that shows basic PowerShell commands to access Azure Storage.</span></span> <span data-ttu-id="5b682-127">Het script vraagt eerst uw Azure-accountreferenties voor het toevoegen van uw Azure-account aan de lokale PowerShell-omgeving.</span><span class="sxs-lookup"><span data-stu-id="5b682-127">The script will first ask your Azure account credentials to add your Azure account to the local PowerShell environment.</span></span> <span data-ttu-id="5b682-128">Het script wordt vervolgens de Azure-abonnement instellen en een nieuw opslagaccount maken in Azure.</span><span class="sxs-lookup"><span data-stu-id="5b682-128">Then, the script will set the default Azure subscription and create a new storage account in Azure.</span></span> <span data-ttu-id="5b682-129">Het script wordt vervolgens een nieuwe container in deze nieuwe opslagaccount maken en uploaden van een bestaand installatiekopiebestand (blob) op die container.</span><span class="sxs-lookup"><span data-stu-id="5b682-129">Next, the script will create a new container in this new storage account and upload an existing image file (blob) to that container.</span></span> <span data-ttu-id="5b682-130">Nadat het script geeft een lijst van alle blobs in de container, worden een nieuwe bestemming-map maken in uw lokale computer en het installatiekopiebestand te downloaden.</span><span class="sxs-lookup"><span data-stu-id="5b682-130">After the script lists all blobs in that container, it will create a new destination directory in your local computer and download the image file.</span></span>
5. <span data-ttu-id="5b682-131">Selecteer het script tussen de opmerkingen in de volgende sectie van de code **#beginnen** en **#end**.</span><span class="sxs-lookup"><span data-stu-id="5b682-131">In the following code section, select the script between the remarks **#begin** and **#end**.</span></span> <span data-ttu-id="5b682-132">Druk op CTRL + C om naar het Klembord kopiëren.</span><span class="sxs-lookup"><span data-stu-id="5b682-132">Press CTRL+C to copy it to the clipboard.</span></span>

    ```powershell
    # begin
    # Update with the name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name to your new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name to your new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account to the local PowerShell environment.
    Add-AzureAccount
       
    # Set a default Azure subscription.
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
       
    # Create a new storage account.
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $Location
       
    # Set a default storage account.
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
       
    # Create a new container.
    New-AzureStorageContainer -Name $ContainerName -Permission Off
       
    # Upload a blob into a container.
    Set-AzureStorageBlobContent -Container $ContainerName -File $ImageToUpload
       
    # List all blobs in a container.
    Get-AzureStorageBlob -Container $ContainerName
       
    # Download blobs from the container:
    # Get a reference to a list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create the destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into the local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. <span data-ttu-id="5b682-133">In **Windows PowerShell ISE**, druk op CTRL + V om te kopiëren van het script.</span><span class="sxs-lookup"><span data-stu-id="5b682-133">In **Windows PowerShell ISE**, press CTRL+V to copy the script.</span></span> <span data-ttu-id="5b682-134">Klik op **bestand** > **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="5b682-134">Click **File** > **Save**.</span></span> <span data-ttu-id="5b682-135">In de **OpslaanAls** dialoogvenster, typ de naam van het scriptbestand, zoals 'mystoragescript'.</span><span class="sxs-lookup"><span data-stu-id="5b682-135">In the **Save As** dialog window, type the name of the script file, such as "mystoragescript."</span></span> <span data-ttu-id="5b682-136">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="5b682-136">Click **Save**.</span></span>
7. <span data-ttu-id="5b682-137">Nu moet u de scriptvariabelen op basis van uw configuratie-instellingen bijwerken.</span><span class="sxs-lookup"><span data-stu-id="5b682-137">Now, you need to update the script variables based on your configuration settings.</span></span> <span data-ttu-id="5b682-138">U moet bijwerken de **$SubscriptionName** variabele met uw eigen abonnement.</span><span class="sxs-lookup"><span data-stu-id="5b682-138">You must update the **$SubscriptionName** variable with your own subscription.</span></span> <span data-ttu-id="5b682-139">U kunt de andere variabelen zoals opgegeven in het script behouden of deze als u wilt bijwerken.</span><span class="sxs-lookup"><span data-stu-id="5b682-139">You can keep the other variables as specified in the script or update them as you wish.</span></span>
   
   * <span data-ttu-id="5b682-140">**$SubscriptionName:** moet u deze variabele bijwerken met de naam van uw eigen abonnement.</span><span class="sxs-lookup"><span data-stu-id="5b682-140">**$SubscriptionName:** You must update this variable with your own subscription name.</span></span> <span data-ttu-id="5b682-141">Ga als volgt op een van de volgende drie manieren vinden van de naam van uw abonnement:</span><span class="sxs-lookup"><span data-stu-id="5b682-141">Follow one of the following three ways to locate the name of your subscription:</span></span>
     
    <span data-ttu-id="5b682-142">a.</span><span class="sxs-lookup"><span data-stu-id="5b682-142">a.</span></span> <span data-ttu-id="5b682-143">In **Windows PowerShell ISE**, klikt u op **bestand** > **nieuw** voor het maken van een script.</span><span class="sxs-lookup"><span data-stu-id="5b682-143">In **Windows PowerShell ISE**, click **File** > **New** to create a new script file.</span></span> <span data-ttu-id="5b682-144">Het volgende script kopiëren naar het nieuwe script en klik op **Debug** > **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="5b682-144">Copy the following script to the new script file and click **Debug** > **Run**.</span></span> <span data-ttu-id="5b682-145">Het volgende script wordt eerst vraagt u uw Azure-accountreferenties voor het toevoegen van uw Azure account toe aan de lokale PowerShell-omgeving en alle abonnementen die zijn verbonden met de lokale PowerShell-sessie wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="5b682-145">The following script will first ask your Azure account credentials to add your Azure account to the local PowerShell environment and then show all the subscriptions that are connected to the local PowerShell session.</span></span> <span data-ttu-id="5b682-146">Noteer de naam van het abonnement dat u gebruiken wilt tijdens deze zelfstudie te volgen:</span><span class="sxs-lookup"><span data-stu-id="5b682-146">Take a note of the name of the subscription that you want to use while following this tutorial:</span></span>
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    <span data-ttu-id="5b682-147">b.</span><span class="sxs-lookup"><span data-stu-id="5b682-147">b.</span></span> <span data-ttu-id="5b682-148">Om te zoeken en kopieert u de abonnementsnaam van uw in de [Azure-portal](https://portal.azure.com), klik in het Hub-menu aan de linkerkant op **abonnementen**.</span><span class="sxs-lookup"><span data-stu-id="5b682-148">To locate and copy your subscription name in the [Azure portal](https://portal.azure.com), in the Hub menu on the left, click **Subscriptions**.</span></span> <span data-ttu-id="5b682-149">Kopieer de naam van het abonnement dat u gebruiken wilt tijdens het uitvoeren van de scripts in deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="5b682-149">Copy the name of subscription that you want to use while running the scripts in this guide.</span></span>
     
     ![Azure Portal](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    <span data-ttu-id="5b682-151">c.</span><span class="sxs-lookup"><span data-stu-id="5b682-151">c.</span></span> <span data-ttu-id="5b682-152">Om te zoeken en kopieert u de abonnementsnaam van uw in de [klassieke Azure-Portal](https://manage.windowsazure.com/), schuif naar beneden en klik op **instellingen** aan de linkerkant van de portal.</span><span class="sxs-lookup"><span data-stu-id="5b682-152">To locate and copy your subscription name in the [Azure Classic Portal](https://manage.windowsazure.com/), scroll down and click **Settings** on the left side of the portal.</span></span> <span data-ttu-id="5b682-153">Klik op **abonnementen** voor een overzicht van uw abonnementen.</span><span class="sxs-lookup"><span data-stu-id="5b682-153">Click **Subscriptions** to see a list of your subscriptions.</span></span> <span data-ttu-id="5b682-154">Kopieer de naam van het abonnement dat u gebruiken wilt tijdens het uitvoeren van de scripts die zijn opgegeven in deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="5b682-154">Copy the name of subscription that you want to use while running the scripts given in this guide.</span></span>
     
     ![Klassieke Azure-portal](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * <span data-ttu-id="5b682-156">**$StorageAccountName:** de voornaam in het script of geef een nieuwe naam voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="5b682-156">**$StorageAccountName:** Use the given name in the script or enter a new name for your storage account.</span></span> <span data-ttu-id="5b682-157">**Belangrijk:** de naam van het opslagaccount moet uniek zijn in Azure.</span><span class="sxs-lookup"><span data-stu-id="5b682-157">**Important:** The name of the storage account must be unique in Azure.</span></span> <span data-ttu-id="5b682-158">Er moet een kleine letter, te!</span><span class="sxs-lookup"><span data-stu-id="5b682-158">It must be lowercase, too!</span></span>
   * <span data-ttu-id="5b682-159">**$Location:** gebruik van de opgegeven 'VS-West' in het script of kies andere Azure locaties, zoals VS-Oost, Noord-Europa, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="5b682-159">**$Location:** Use the given "West US" in the script or choose other Azure locations, such as East US, North Europe, and so on.</span></span>
   * <span data-ttu-id="5b682-160">**$ContainerName:** de voornaam in het script of geef een nieuwe naam voor de container.</span><span class="sxs-lookup"><span data-stu-id="5b682-160">**$ContainerName:** Use the given name in the script or enter a new name for your container.</span></span>
   * <span data-ttu-id="5b682-161">**$ImageToUpload:** Voer een pad naar een afbeelding op uw lokale computer, zoals: 'C:\Images\HelloWorld.png'.</span><span class="sxs-lookup"><span data-stu-id="5b682-161">**$ImageToUpload:** Enter a path to a picture on your local computer, such as: "C:\Images\HelloWorld.png".</span></span>
   * <span data-ttu-id="5b682-162">**$DestinationFolder:** een pad opgeven naar een lokale map voor het opslaan van bestanden die zijn gedownload van Azure Storage, zoals: 'C:\DownloadImages'.</span><span class="sxs-lookup"><span data-stu-id="5b682-162">**$DestinationFolder:** Enter a path to a local directory to store files downloaded from Azure Storage, such as: "C:\DownloadImages".</span></span>
8. <span data-ttu-id="5b682-163">Klik na het bijwerken van de scriptvariabelen in het bestand 'mystoragescript.ps1' **bestand** > **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="5b682-163">After updating the script variables in the "mystoragescript.ps1" file, click **File** > **Save**.</span></span> <span data-ttu-id="5b682-164">Klik vervolgens op **Debug** > **uitvoeren** of druk op **F5** het script uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="5b682-164">Then, click **Debug** > **Run** or press **F5** to run the script.</span></span>  

<span data-ttu-id="5b682-165">Nadat het script wordt uitgevoerd, moet u een lokale doelmap met het gedownloade bestand hebben.</span><span class="sxs-lookup"><span data-stu-id="5b682-165">After the script runs, you should have a local destination folder that includes the downloaded image file.</span></span> <span data-ttu-id="5b682-166">De volgende schermafbeelding ziet een voorbeeld van uitvoer:</span><span class="sxs-lookup"><span data-stu-id="5b682-166">The following screenshot shows an example output:</span></span>

![Blobs downloaden](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> <span data-ttu-id="5b682-168">De sectie 'Aan de slag met Azure Storage en PowerShell in vijf minuten' verstrekt een korte inleiding op Azure PowerShell gebruiken met Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="5b682-168">The "Getting started with Azure Storage and PowerShell in 5 minutes" section provided a quick introduction on how to use Azure PowerShell with Azure Storage.</span></span> <span data-ttu-id="5b682-169">Voor gedetailleerde informatie en instructies raden we u aan het lezen van de volgende secties.</span><span class="sxs-lookup"><span data-stu-id="5b682-169">For detailed information and instructions, we encourage you to read the following sections.</span></span>
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a><span data-ttu-id="5b682-170">Vereisten voor het gebruik van Azure PowerShell met Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5b682-170">Prerequisites for using Azure PowerShell with Azure Storage</span></span>
<span data-ttu-id="5b682-171">U moet een Azure-abonnement en de account voor het uitvoeren van de PowerShell-cmdlets die is opgegeven in deze handleiding, zoals hierboven beschreven.</span><span class="sxs-lookup"><span data-stu-id="5b682-171">You need an Azure subscription and account to run the PowerShell cmdlets given in this guide, as described above.</span></span>

<span data-ttu-id="5b682-172">Azure PowerShell is een module die biedt voor het beheren van Azure via Windows PowerShell-cmdlets.</span><span class="sxs-lookup"><span data-stu-id="5b682-172">Azure PowerShell is a module that provides cmdlets to manage Azure through Windows PowerShell.</span></span> <span data-ttu-id="5b682-173">Zie voor meer informatie over het installeren en instellen van Azure PowerShell [installeren en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5b682-173">For information on installing and setting up Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="5b682-174">U wordt aangeraden dat u downloaden en installeren of naar de nieuwste Azure PowerShell-module upgraden voordat u deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="5b682-174">We recommend that you download and install or upgrade to the latest Azure PowerShell module before using this guide.</span></span>

<span data-ttu-id="5b682-175">U kunt de cmdlets uitvoeren in de standaard Windows PowerShell-console of de Windows PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="5b682-175">You can run the cmdlets in the standard Windows PowerShell console or the Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="5b682-176">Om bijvoorbeeld te openen **Windows PowerShell ISE**, gaat u naar het menu Start, typt u de beheerprogramma's en klikt u op uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="5b682-176">For example, to open **Windows PowerShell ISE**, go to the Start menu, type Administrative Tools and click to run it.</span></span> <span data-ttu-id="5b682-177">In het venster Systeembeheer met de rechtermuisknop op Windows PowerShell ISE, klik op uitvoeren als Administrator.</span><span class="sxs-lookup"><span data-stu-id="5b682-177">In the Administrative Tools window, right-click Windows PowerShell ISE, click Run as Administrator.</span></span>

## <a name="how-to-manage-storage-accounts-in-azure"></a><span data-ttu-id="5b682-178">Storage-accounts in Azure beheren</span><span class="sxs-lookup"><span data-stu-id="5b682-178">How to manage storage accounts in Azure</span></span>

<span data-ttu-id="5b682-179">We gaan verdiepen in de storage-accounts in Azure met PowerShell beheren</span><span class="sxs-lookup"><span data-stu-id="5b682-179">Let's take a look at managing storage accounts in Azure with PowerShell</span></span>

### <a name="how-to-set-a-default-azure-subscription"></a><span data-ttu-id="5b682-180">Het instellen van een standaard Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="5b682-180">How to set a default Azure subscription</span></span>
<span data-ttu-id="5b682-181">Voor het beheren van Azure Storage met Azure PowerShell, moet u uw clientomgeving met Azure via Azure Active Directory-verificatie of verificatie op basis van certificaten verifiëren.</span><span class="sxs-lookup"><span data-stu-id="5b682-181">To manage Azure Storage using Azure PowerShell, you need to authenticate your client environment with Azure via Azure Active Directory authentication or certificate-based authentication.</span></span> <span data-ttu-id="5b682-182">Zie voor gedetailleerde informatie [installeren en configureren van Azure PowerShell](/powershell/azure/overview) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="5b682-182">For detailed information, see [How to install and configure Azure PowerShell](/powershell/azure/overview) tutorial.</span></span> <span data-ttu-id="5b682-183">Deze handleiding bevat de Azure Active Directory-verificatie.</span><span class="sxs-lookup"><span data-stu-id="5b682-183">This guide uses the Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="5b682-184">Typ de volgende opdracht voor het toevoegen van uw Azure in Windows PowerShell ISE account toe aan de lokale PowerShell-omgeving:</span><span class="sxs-lookup"><span data-stu-id="5b682-184">In Windows PowerShell ISE, type the following command to add your Azure account to the local PowerShell environment:</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="5b682-185">Typ de e-mailadres en het wachtwoord die zijn gekoppeld aan uw account in het venster 'Aanmelding in voor Microsoft Azure'.</span><span class="sxs-lookup"><span data-stu-id="5b682-185">In the "Sign in to Microsoft Azure" window, type the email address and password associated with your account.</span></span> <span data-ttu-id="5b682-186">Azure verifieert de referentiegegevens en slaat deze op. Vervolgens wordt het venster gesloten.</span><span class="sxs-lookup"><span data-stu-id="5b682-186">Azure authenticates and saves the credential information, and then closes the window.</span></span>

3. <span data-ttu-id="5b682-187">Voer de volgende opdracht om de Azure-accounts in uw lokale PowerShell-omgeving weergeven en controleer of uw account wordt vermeld:</span><span class="sxs-lookup"><span data-stu-id="5b682-187">Next, run the following command to view the Azure accounts in your local PowerShell environment, and verify that your account is listed:</span></span>
   
    ```powershell
    Get-AzureAccount
    ```
4. <span data-ttu-id="5b682-188">Vervolgens voert u de volgende cmdlet als u wilt weergeven van alle abonnementen die zijn verbonden met de lokale PowerShell-sessie en controleert u of uw abonnement wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="5b682-188">Then, run the following cmdlet to view all the subscriptions that are connected to the local PowerShell session, and verify that your subscription is listed:</span></span>

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. <span data-ttu-id="5b682-189">Als u wilt instellen op een standaard Azure-abonnement, voer de Select-AzureSubscription-cmdlet:</span><span class="sxs-lookup"><span data-stu-id="5b682-189">To set a default Azure subscription, run the Select-AzureSubscription cmdlet:</span></span>

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. <span data-ttu-id="5b682-190">Controleer de naam van het standaardabonnement door de cmdlet Get-AzureSubscription:</span><span class="sxs-lookup"><span data-stu-id="5b682-190">Verify the name of the default subscription by running the Get-AzureSubscription cmdlet:</span></span>

    ```powershell
    Get-AzureSubscription -Default
    ```

7. <span data-ttu-id="5b682-191">Alle beschikbare PowerShell-cmdlets voor Azure Storage vindt uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="5b682-191">To see all the available PowerShell cmdlets for Azure Storage, run:</span></span>
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-to-create-a-new-azure-storage-account"></a><span data-ttu-id="5b682-192">Het maken van een nieuwe Azure storage-account</span><span class="sxs-lookup"><span data-stu-id="5b682-192">How to create a new Azure storage account</span></span>
<span data-ttu-id="5b682-193">Voor het gebruik van Azure-opslag, moet u een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="5b682-193">To use Azure storage, you will need a storage account.</span></span> <span data-ttu-id="5b682-194">Nadat u uw computer verbinding maken met uw abonnement hebt geconfigureerd, kunt u een nieuwe Azure storage-account maken.</span><span class="sxs-lookup"><span data-stu-id="5b682-194">You can create a new Azure storage account after you have configured your computer to connect to your subscription.</span></span>

1. <span data-ttu-id="5b682-195">Voer de cmdlet Get-AzureLocation om alle beschikbare datacenterlocaties vinden:</span><span class="sxs-lookup"><span data-stu-id="5b682-195">Run the Get-AzureLocation cmdlet to find all the available datacenter locations:</span></span>

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. <span data-ttu-id="5b682-196">Voer de cmdlet New-AzureStorageAccount voor het maken van een nieuw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="5b682-196">Next, run the New-AzureStorageAccount cmdlet to create a new storage account.</span></span> <span data-ttu-id="5b682-197">Het volgende voorbeeld wordt een nieuw opslagaccount gemaakt in het datacenter 'VS-West'.</span><span class="sxs-lookup"><span data-stu-id="5b682-197">The following example creates a new storage account in the "West US" datacenter.</span></span>
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> <span data-ttu-id="5b682-198">De naam van uw opslagaccount moet uniek zijn binnen Azure en moet een kleine letter.</span><span class="sxs-lookup"><span data-stu-id="5b682-198">The name of your storage account must be unique within Azure and must be lowercase.</span></span> <span data-ttu-id="5b682-199">Zie voor naamconventies en beperkingen [over Azure Storage-Accounts](storage-create-storage-account.md) en [Naming en verwijzen naar Containers, Blobs en metagegevens](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span><span class="sxs-lookup"><span data-stu-id="5b682-199">For naming conventions and restrictions, see [About Azure Storage Accounts](storage-create-storage-account.md) and [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span></span>
> 
> 

### <a name="how-to-set-a-default-azure-storage-account"></a><span data-ttu-id="5b682-200">Het instellen van een Azure storage-standaardaccount</span><span class="sxs-lookup"><span data-stu-id="5b682-200">How to set a default Azure storage account</span></span>
<span data-ttu-id="5b682-201">U kunt meerdere opslagaccounts hebben in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="5b682-201">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="5b682-202">U kunt kiezen één van deze en stel dit in als het standaardopslagaccount voor alle opslag-opdrachten in dezelfde PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="5b682-202">You can choose one of them and set it as the default storage account for all the storage commands in the same PowerShell session.</span></span> <span data-ttu-id="5b682-203">Hiermee kunt u de Azure PowerShell-opslag-opdrachten uitvoeren zonder expliciet opgeven van de context van de opslag.</span><span class="sxs-lookup"><span data-stu-id="5b682-203">This enables you to run the Azure PowerShell storage commands without specifying the storage context explicitly.</span></span>

1. <span data-ttu-id="5b682-204">Om in te stellen een standaardopslagaccount voor uw abonnement, kunt u de cmdlet Set-AzureSubscription uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="5b682-204">To set a default storage account for your subscription, you can run the Set-AzureSubscription cmdlet.</span></span>

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. <span data-ttu-id="5b682-205">Voer de cmdlet Get-AzureSubscription om te controleren of het opslagaccount gekoppeld aan uw abonnement standaardaccount is.</span><span class="sxs-lookup"><span data-stu-id="5b682-205">Next, run the Get-AzureSubscription cmdlet to verify that the storage account is associated with your default subscription account.</span></span> <span data-ttu-id="5b682-206">Met deze opdracht retourneert de eigenschappen van het abonnement op het huidige abonnement met inbegrip van de huidige opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="5b682-206">This command returns the subscription properties on the current subscription including its current storage account.</span></span>

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-to-list-all-azure-storage-accounts-in-a-subscription"></a><span data-ttu-id="5b682-207">Hoe u alle Azure storage-accounts in een abonnement</span><span class="sxs-lookup"><span data-stu-id="5b682-207">How to list all Azure storage accounts in a subscription</span></span>
<span data-ttu-id="5b682-208">Elk Azure-abonnement kan maximaal 100 opslagaccounts hebben.</span><span class="sxs-lookup"><span data-stu-id="5b682-208">Each Azure subscription can have up to 100 storage accounts.</span></span> <span data-ttu-id="5b682-209">Zie voor de meest actuele informatie van limieten [Azure-abonnement en Service-limieten, quota's en beperkingen](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="5b682-209">For the most up-to-date information on limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="5b682-210">Voer de volgende cmdlet om erachter te komen met de naam en de status van de storage-accounts in het huidige abonnement:</span><span class="sxs-lookup"><span data-stu-id="5b682-210">Run the following cmdlet to find out the name and status of the storage accounts in the current subscription:</span></span>

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-to-create-an-azure-storage-context"></a><span data-ttu-id="5b682-211">Het maken van een Azure-opslag-context</span><span class="sxs-lookup"><span data-stu-id="5b682-211">How to create an Azure storage context</span></span>
<span data-ttu-id="5b682-212">Azure-opslag-context is een object in PowerShell inkapselen de storage-referenties.</span><span class="sxs-lookup"><span data-stu-id="5b682-212">Azure storage context is an object in PowerShell to encapsulate the storage credentials.</span></span> <span data-ttu-id="5b682-213">Met behulp van een context opslag terwijl alle volgende cmdlet wordt uitgevoerd, u uw aanvraag verifiëren kunt zonder het expliciet opgeven van het opslagaccount en de toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="5b682-213">Using a storage context while running any subsequent cmdlet enables you to authenticate your request without specifying the storage account and its access key explicitly.</span></span> <span data-ttu-id="5b682-214">U kunt een context opslag maken op vele manieren, zoals het gebruik van naam en toegangssleutel van storage-account, de shared access signature (SAS)-token, de verbindingsreeks, of anonieme.</span><span class="sxs-lookup"><span data-stu-id="5b682-214">You can create a storage context in many ways, such as using storage account name and access key, shared access signature (SAS) token, connection string, or anonymous.</span></span> <span data-ttu-id="5b682-215">Zie voor meer informatie [nieuw AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span><span class="sxs-lookup"><span data-stu-id="5b682-215">For more information, see [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span></span>  

<span data-ttu-id="5b682-216">Gebruik een van de volgende drie manieren voor het maken van een context opslag:</span><span class="sxs-lookup"><span data-stu-id="5b682-216">Use one of the following three ways to create a storage context:</span></span>

* <span data-ttu-id="5b682-217">Voer de [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet om erachter te komen de opslag van primaire toegangssleutel voor uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="5b682-217">Run the [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet to find out the primary storage access key for your Azure storage account.</span></span> <span data-ttu-id="5b682-218">Daarna roept de [nieuw AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet voor het maken van een context opslag:</span><span class="sxs-lookup"><span data-stu-id="5b682-218">Next, call the [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet to create a storage context:</span></span>

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* <span data-ttu-id="5b682-219">Genereren van een shared access signature-token voor een Azure storage-container en de context van een opslagruimte maken:</span><span class="sxs-lookup"><span data-stu-id="5b682-219">Generate a shared access signature token for an Azure storage container and use it to create a storage context:</span></span>

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    <span data-ttu-id="5b682-220">Zie voor meer informatie [nieuw AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) en [met behulp van Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="5b682-220">For more information, see [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) and [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span></span>

* <span data-ttu-id="5b682-221">In sommige gevallen wilt u mogelijk de service-eindpunten opgeven bij het maken van een nieuwe opslag-context.</span><span class="sxs-lookup"><span data-stu-id="5b682-221">In some cases, you may want to specify the service endpoints when you create a new storage context.</span></span> <span data-ttu-id="5b682-222">Dit kan noodzakelijk zijn wanneer u een aangepaste domeinnaam voor uw opslagaccount hebt geregistreerd met de Blob-service of u gebruiken een shared access signature wilt voor toegang tot de opslagbronnen.</span><span class="sxs-lookup"><span data-stu-id="5b682-222">This might be necessary when you have registered a custom domain name for your storage account with the Blob service or you want to use a shared access signature for accessing storage resources.</span></span> <span data-ttu-id="5b682-223">De service-eindpunten in een verbindingsreeks instellen en deze gebruiken voor het maken van een nieuwe opslag-context, zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="5b682-223">Set the service endpoints in a connection string and use it to create a new storage context as shown below:</span></span>

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

<span data-ttu-id="5b682-224">Zie voor meer informatie over het configureren van een verbindingsreeks voor opslag [configureren van verbindingsreeksen](storage-configure-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="5b682-224">For more information on how to configure a storage connection string, see [Configuring Connection Strings](storage-configure-connection-string.md).</span></span>

<span data-ttu-id="5b682-225">Nu dat u hebt uw computer instellen en hebt geleerd hoe u abonnementen en opslagaccounts met Azure PowerShell beheren, gaat u naar de volgende sectie voor informatie over het beheren van Azure blobs en blob-momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="5b682-225">Now that you have set up your computer and learned how to manage subscriptions and storage accounts using Azure PowerShell, go to the next section to learn how to manage Azure blobs and blob snapshots.</span></span>

### <a name="how-to-retrieve-and-regenerate-azure-storage-keys"></a><span data-ttu-id="5b682-226">Ophalen en opnieuw genereren van sleutels voor Azure-opslag</span><span class="sxs-lookup"><span data-stu-id="5b682-226">How to retrieve and regenerate Azure storage keys</span></span>
<span data-ttu-id="5b682-227">Een Azure Storage-account wordt geleverd met twee sleutels.</span><span class="sxs-lookup"><span data-stu-id="5b682-227">An Azure Storage account comes with two account keys.</span></span> <span data-ttu-id="5b682-228">U kunt de volgende cmdlet gebruiken voor het ophalen van uw sleutels.</span><span class="sxs-lookup"><span data-stu-id="5b682-228">You can use the following cmdlet to retrieve your keys.</span></span>

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

<span data-ttu-id="5b682-229">Gebruik de volgende cmdlet voor het ophalen van een specifieke sleutel.</span><span class="sxs-lookup"><span data-stu-id="5b682-229">Use the following cmdlet to retrieve a specific key.</span></span> <span data-ttu-id="5b682-230">Geldige waarden zijn primair en secundair.</span><span class="sxs-lookup"><span data-stu-id="5b682-230">Valid values are Primary and Secondary.</span></span>  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

<span data-ttu-id="5b682-231">Gebruik de volgende cmdlet als u wilt uw sleutels genereren.</span><span class="sxs-lookup"><span data-stu-id="5b682-231">If you would like to regenerate your keys, use the following cmdlet.</span></span> <span data-ttu-id="5b682-232">Geldige waarden voor KeyType - zijn 'Primaire' en 'Secundaire'</span><span class="sxs-lookup"><span data-stu-id="5b682-232">Valid values for -KeyType are "Primary" and "Secondary"</span></span>

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-to-manage-azure-blobs"></a><span data-ttu-id="5b682-233">Azure BLOB's beheren</span><span class="sxs-lookup"><span data-stu-id="5b682-233">How to manage Azure blobs</span></span>
<span data-ttu-id="5b682-234">Azure Blob storage is een service voor het opslaan van grote hoeveelheden ongestructureerde gegevens, zoals tekst of binaire gegevens, die toegankelijk zijn vanuit overal ter wereld via HTTP of HTTPS.</span><span class="sxs-lookup"><span data-stu-id="5b682-234">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="5b682-235">Deze sectie wordt ervan uitgegaan dat u al bekend met de concepten van Azure Blob Storage-Service bent.</span><span class="sxs-lookup"><span data-stu-id="5b682-235">This section assumes that you are already familiar with the Azure Blob Storage Service concepts.</span></span> <span data-ttu-id="5b682-236">Zie voor gedetailleerde informatie [aan de slag met Blob storage met .NET](storage-dotnet-how-to-use-blobs.md) en [concepten van Blob-Service](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="5b682-236">For detailed information, see [Get started with Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="how-to-create-a-container"></a><span data-ttu-id="5b682-237">Het maken van een container</span><span class="sxs-lookup"><span data-stu-id="5b682-237">How to create a container</span></span>
<span data-ttu-id="5b682-238">Elke blob in Azure-opslag moet zich in een container.</span><span class="sxs-lookup"><span data-stu-id="5b682-238">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="5b682-239">U kunt een privé-container met de cmdlet New-AzureStorageContainer maken:</span><span class="sxs-lookup"><span data-stu-id="5b682-239">You can create a private container using the New-AzureStorageContainer cmdlet:</span></span>

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> <span data-ttu-id="5b682-240">Er zijn drie niveaus van anonieme toegang voor lezen: **uit**, **Blob**, en **Container**.</span><span class="sxs-lookup"><span data-stu-id="5b682-240">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="5b682-241">Als u wilt voorkomen dat anonieme toegang tot blobs, stelt u de machtiging-parameter in op **uit**.</span><span class="sxs-lookup"><span data-stu-id="5b682-241">To prevent anonymous access to blobs, set the Permission parameter to **Off**.</span></span> <span data-ttu-id="5b682-242">Standaard worden de nieuwe container privé is en kan alleen worden geopend door de eigenaar van het account.</span><span class="sxs-lookup"><span data-stu-id="5b682-242">By default, the new container is private and can be accessed only by the account owner.</span></span> <span data-ttu-id="5b682-243">Anonieme toegang toestaan openbare leestoegang tot blob-bronnen, maar niet aan de metagegevens van de container of aan de lijst met blobs in de container, stelt u de parameter machtiging op **Blob**.</span><span class="sxs-lookup"><span data-stu-id="5b682-243">To allow anonymous public read access to blob resources, but not to container metadata or to the list of blobs in the container, set the Permission parameter to **Blob**.</span></span> <span data-ttu-id="5b682-244">Stel de parameter machtiging op wilt toestaan volledige openbare leestoegang tot de blob-bronnen, container metagegevens en de lijst met blobs in de container, **Container**.</span><span class="sxs-lookup"><span data-stu-id="5b682-244">To allow full public read access to blob resources, container metadata, and the list of blobs in the container, set the Permission parameter to **Container**.</span></span> <span data-ttu-id="5b682-245">Zie voor meer informatie [anonieme leestoegang tot containers en blobs beheren](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="5b682-245">For more information, see [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>
> 
> 

### <a name="how-to-upload-a-blob-into-a-container"></a><span data-ttu-id="5b682-246">Het uploaden van een blob naar een container</span><span class="sxs-lookup"><span data-stu-id="5b682-246">How to upload a blob into a container</span></span>
<span data-ttu-id="5b682-247">Azure Blob Storage ondersteunt blok-blobs en pagina-blobs.</span><span class="sxs-lookup"><span data-stu-id="5b682-247">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="5b682-248">Zie voor meer informatie [blok-Blobs, toevoeg-BLobs en pagina-Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="5b682-248">For more information, see [Understanding Block Blobs, Append BLobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="5b682-249">Blobs in als u wilt uploaden een container, kunt u de [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b682-249">To upload blobs in to a container, you can use the [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span></span> <span data-ttu-id="5b682-250">Standaard wordt met deze opdracht de lokale bestanden naar een blok-blob geüpload.</span><span class="sxs-lookup"><span data-stu-id="5b682-250">By default, this command uploads the local files to a block blob.</span></span> <span data-ttu-id="5b682-251">Als u wilt opgeven welk type voor de blob, kunt u de parameter - BlobType.</span><span class="sxs-lookup"><span data-stu-id="5b682-251">To specify the type for the blob, you can use the -BlobType parameter.</span></span>

<span data-ttu-id="5b682-252">Het volgende voorbeeld wordt uitgevoerd de [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet ophalen van alle bestanden in de opgegeven map en vervolgens doorgegeven aan de volgende cmdlet met behulp van de pijplijn-operator.</span><span class="sxs-lookup"><span data-stu-id="5b682-252">The following example runs the [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet to get all the files in the specified folder, and then passes them to the next cmdlet by using the pipeline operator.</span></span> <span data-ttu-id="5b682-253">De [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet wordt de lokale bestanden geüpload naar de container:</span><span class="sxs-lookup"><span data-stu-id="5b682-253">The [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet uploads the local files to your container:</span></span>

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-to-download-blobs-from-a-container"></a><span data-ttu-id="5b682-254">Blobs downloaden uit een container</span><span class="sxs-lookup"><span data-stu-id="5b682-254">How to download blobs from a container</span></span>
<span data-ttu-id="5b682-255">Het volgende voorbeeld laat zien hoe blobs downloaden uit een container.</span><span class="sxs-lookup"><span data-stu-id="5b682-255">The following example demonstrates how to download blobs from a container.</span></span> <span data-ttu-id="5b682-256">In het voorbeeld maakt eerst een verbinding met Azure Storage met context van het opslagaccount, waaronder de opslagaccountnaam en de primaire toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="5b682-256">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its primary access key.</span></span> <span data-ttu-id="5b682-257">Klik in het voorbeeld haalt een blob-verwijzing met de [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b682-257">Then, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span></span> <span data-ttu-id="5b682-258">Vervolgens in het voorbeeld wordt de [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet blobs downloaden naar de map lokale bestemming.</span><span class="sxs-lookup"><span data-stu-id="5b682-258">Next, the example uses the [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet to download blobs into the local destination folder.</span></span>

```powershell
#Define the variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-to-copy-blobs-from-one-storage-container-to-another"></a><span data-ttu-id="5b682-259">Blobs uit een opslagcontainer naar de andere kopiëren</span><span class="sxs-lookup"><span data-stu-id="5b682-259">How to copy blobs from one storage container to another</span></span>
<span data-ttu-id="5b682-260">U kunt BLOB's tussen opslagaccounts en regio's asynchroon kopiëren.</span><span class="sxs-lookup"><span data-stu-id="5b682-260">You can copy blobs across storage accounts and regions asynchronously.</span></span> <span data-ttu-id="5b682-261">Het volgende voorbeeld laat zien hoe blobs van één opslagcontainer kopieert naar een andere in twee verschillende opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="5b682-261">The following example demonstrates how to copy blobs from one storage container to another in two different storage accounts.</span></span> <span data-ttu-id="5b682-262">In het voorbeeld stelt eerst de variabelen voor de bron- en storage-accounts, en maakt vervolgens een context opslag voor elke account.</span><span class="sxs-lookup"><span data-stu-id="5b682-262">The example first sets variables for source and destination storage accounts, and then creates a storage context for each account.</span></span> <span data-ttu-id="5b682-263">Vervolgens in het voorbeeld blobs opgehaald uit de Broncontainer met de doel-container via de [Start AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b682-263">Next, the example copies blobs from the source container to the destination container using the [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span></span> <span data-ttu-id="5b682-264">In het voorbeeld wordt ervan uitgegaan dat de bron- en storage-accounts en containers al bestaan.</span><span class="sxs-lookup"><span data-stu-id="5b682-264">The example assumes that the source and destination storage accounts and containers already exist.</span></span>

```powershell
#Define the source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define the destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference to blobs in the source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container to another.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

<span data-ttu-id="5b682-265">Houd er rekening mee dat dit voorbeeld wordt een kopie van de asynchrone uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5b682-265">Note that this example performs an asynchronous copy.</span></span> <span data-ttu-id="5b682-266">U kunt de status van elk exemplaar bewaken door het uitvoeren van de [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b682-266">You can monitor the status of each copy by running the [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span></span>

### <a name="how-to-copy-blobs-from-a-secondary-location"></a><span data-ttu-id="5b682-267">Blobs kopiëren vanaf een secundaire locatie</span><span class="sxs-lookup"><span data-stu-id="5b682-267">How to copy blobs from a secondary location</span></span>
<span data-ttu-id="5b682-268">U kunt de blobs kopiëren vanaf de secundaire locatie van een account RA-GRS-functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="5b682-268">You can copy blobs from the secondary location of a RA-GRS-enabled account.</span></span>

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-to-delete-a-blob"></a><span data-ttu-id="5b682-269">Het verwijderen van een blob</span><span class="sxs-lookup"><span data-stu-id="5b682-269">How to delete a blob</span></span>
<span data-ttu-id="5b682-270">Als u wilt verwijderen van een blob, eerst een blobverwijzing ophalen en roept u vervolgens de cmdlet Remove-AzureStorageBlob erop.</span><span class="sxs-lookup"><span data-stu-id="5b682-270">To delete a blob, first get a blob reference and then call the Remove-AzureStorageBlob cmdlet on it.</span></span> <span data-ttu-id="5b682-271">Het volgende voorbeeld verwijdert alle blobs in een bepaalde container.</span><span class="sxs-lookup"><span data-stu-id="5b682-271">The following example deletes all the blobs in a given container.</span></span> <span data-ttu-id="5b682-272">Het voorbeeld stelt eerst de variabelen voor een opslagaccount en maakt vervolgens een opslag-context.</span><span class="sxs-lookup"><span data-stu-id="5b682-272">The example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="5b682-273">Vervolgens in het voorbeeld haalt een blob-referentie met de [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet en wordt uitgevoerd de [verwijderen AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet blobs verwijderen uit een container in Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="5b682-273">Next, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet to remove blobs from a container in Azure storage.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference to all the blobs in the container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-to-manage-azure-blob-snapshots"></a><span data-ttu-id="5b682-274">Het beheren van Azure blob-momentopnamen</span><span class="sxs-lookup"><span data-stu-id="5b682-274">How to manage Azure blob snapshots</span></span>
<span data-ttu-id="5b682-275">Azure maakt u een momentopname van een blob.</span><span class="sxs-lookup"><span data-stu-id="5b682-275">Azure lets you create a snapshot of a blob.</span></span> <span data-ttu-id="5b682-276">Een momentopname is een alleen-lezen-versie van een blob die wordt uitgevoerd op een punt in tijd.</span><span class="sxs-lookup"><span data-stu-id="5b682-276">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="5b682-277">Wanneer een momentopname is gemaakt, kan deze worden gelezen, gekopieerd, of verwijderd, maar niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="5b682-277">Once a snapshot has been created, it can be read, copied, or deleted, but not modified.</span></span> <span data-ttu-id="5b682-278">Momentopnamen bieden een manier om back-up van een blob zoals deze wordt weergegeven op een moment.</span><span class="sxs-lookup"><span data-stu-id="5b682-278">Snapshots provide a way to back up a blob as it appears at a moment in time.</span></span> <span data-ttu-id="5b682-279">Zie voor meer informatie [maken van een momentopname van een Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="5b682-279">For more information, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span>

### <a name="how-to-create-a-blob-snapshot"></a><span data-ttu-id="5b682-280">Het maken van een momentopname van een blob</span><span class="sxs-lookup"><span data-stu-id="5b682-280">How to create a blob snapshot</span></span>
<span data-ttu-id="5b682-281">Voor het maken van een snaphot van een blob, eerst een blobverwijzing ophalen en roept u vervolgens de `ICloudBlob.CreateSnapshot` methode erop.</span><span class="sxs-lookup"><span data-stu-id="5b682-281">To create a snaphot of a blob, first get a blob reference and then call the `ICloudBlob.CreateSnapshot` method on it.</span></span> <span data-ttu-id="5b682-282">Het volgende voorbeeld stelt eerst de variabelen voor een opslagaccount en maakt vervolgens een opslag-context.</span><span class="sxs-lookup"><span data-stu-id="5b682-282">The following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="5b682-283">Vervolgens in het voorbeeld haalt een blob-referentie met de [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet en wordt uitgevoerd de [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) methode om een momentopname te maken.</span><span class="sxs-lookup"><span data-stu-id="5b682-283">Next, the example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method to create a snapshot.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference to a blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of the blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-to-list-a-blobs-snapshots"></a><span data-ttu-id="5b682-284">Hoe u een blob-momentopnamen</span><span class="sxs-lookup"><span data-stu-id="5b682-284">How to list a blob's snapshots</span></span>
<span data-ttu-id="5b682-285">U kunt zoveel momentopnamen als u voor een blob wilt maken.</span><span class="sxs-lookup"><span data-stu-id="5b682-285">You can create as many snapshots as you want for a blob.</span></span> <span data-ttu-id="5b682-286">U kunt de momentopnamen die zijn gekoppeld aan uw blob om bij te houden van uw huidige momentopnamen aanbieden.</span><span class="sxs-lookup"><span data-stu-id="5b682-286">You can list the snapshots associated with your blob to track your current snapshots.</span></span> <span data-ttu-id="5b682-287">Het volgende voorbeeld wordt een vooraf gedefinieerde blob en aanroepen de [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet voor het weergeven van de momentopnamen van de blob.</span><span class="sxs-lookup"><span data-stu-id="5b682-287">The following example uses a predefined blob and calls the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet to list the snapshots of that blob.</span></span>  

```powershell
#Define the blob name.
$BlobName = "yourblobname"

#List the snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-to-copy-a-snapshot-of-a-blob"></a><span data-ttu-id="5b682-288">Het kopiëren van een momentopname van een blob</span><span class="sxs-lookup"><span data-stu-id="5b682-288">How to copy a snapshot of a blob</span></span>
<span data-ttu-id="5b682-289">U kunt een momentopname van een blob om te herstellen van de momentopname kopiëren.</span><span class="sxs-lookup"><span data-stu-id="5b682-289">You can copy a snapshot of a blob to restore the snapshot.</span></span> <span data-ttu-id="5b682-290">Zie voor gedetailleerde informatie en beperkingen [maken van een momentopname van een Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="5b682-290">For detailed information and restrictions, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span> <span data-ttu-id="5b682-291">Het volgende voorbeeld stelt eerst de variabelen voor een opslagaccount en maakt vervolgens een opslag-context.</span><span class="sxs-lookup"><span data-stu-id="5b682-291">The following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="5b682-292">In het voorbeeld definieert vervolgens de naam van container en blob variabelen.</span><span class="sxs-lookup"><span data-stu-id="5b682-292">Next, the example defines the container and blob name variables.</span></span> <span data-ttu-id="5b682-293">In het voorbeeld haalt een blob-referentie met de [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet en wordt uitgevoerd de [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) methode om een momentopname te maken.</span><span class="sxs-lookup"><span data-stu-id="5b682-293">The example retrieves a blob reference using the [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs the [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method to create a snapshot.</span></span> <span data-ttu-id="5b682-294">Klik in het voorbeeld wordt uitgevoerd de [Start AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet voor het kopiëren van de momentopname van een blob met behulp van het object ICloudBlob voor de bron-blob.</span><span class="sxs-lookup"><span data-stu-id="5b682-294">Then, the example runs the [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet to copy the snapshot of a blob using the ICloudBlob object for the source blob.</span></span> <span data-ttu-id="5b682-295">Zorg ervoor dat de variabelen op basis van uw configuratie voordat u het voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="5b682-295">Be sure to update the variables based on your configuration before running the example.</span></span> <span data-ttu-id="5b682-296">Houd er rekening mee dat het volgende voorbeeld wordt verondersteld dat de bron en bestemming containers en de bron-blob al bestaat.</span><span class="sxs-lookup"><span data-stu-id="5b682-296">Note that the following example assumes that the source and destination containers, and the source blob already exist.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define the variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference to a blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy the snapshot to another container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

<span data-ttu-id="5b682-297">U hebt geleerd hoe u Azure blobs beheren en blob-momentopnamen met Azure PowerShell, gaat u naar de volgende sectie voor informatie over het beheren van tabellen, wachtrijen en -bestanden.</span><span class="sxs-lookup"><span data-stu-id="5b682-297">Now that you have learned how to manage Azure blobs and blob snapshots with Azure PowerShell, go to the next section to learn how to manage tables, queues, and files.</span></span>

## <a name="how-to-manage-azure-tables-and-table-entities"></a><span data-ttu-id="5b682-298">Azure-tabellen en tabelentiteiten beheren</span><span class="sxs-lookup"><span data-stu-id="5b682-298">How to manage Azure tables and table entities</span></span>
<span data-ttu-id="5b682-299">Azure Table storage-service is een NoSQL-gegevensarchief, waarin u kunt opslaan en grote sets gestructureerde, niet-relationele gegevens opvragen.</span><span class="sxs-lookup"><span data-stu-id="5b682-299">Azure Table storage service is a NoSQL datastore, which you can use to store and query huge sets of structured, non-relational data.</span></span> <span data-ttu-id="5b682-300">De belangrijkste onderdelen van de service zijn tabellen, entiteiten en eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="5b682-300">The main components of the service are tables, entities, and properties.</span></span> <span data-ttu-id="5b682-301">Een tabel is een verzameling entiteiten.</span><span class="sxs-lookup"><span data-stu-id="5b682-301">A table is a collection of entities.</span></span> <span data-ttu-id="5b682-302">Een entiteit is een set eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="5b682-302">An entity is a set of properties.</span></span> <span data-ttu-id="5b682-303">Elke entiteit kan maximaal 252 eigenschappen die alle naam / waarde-paren hebben.</span><span class="sxs-lookup"><span data-stu-id="5b682-303">Each entity can have up to 252 properties, which are all name-value pairs.</span></span> <span data-ttu-id="5b682-304">Deze sectie wordt ervan uitgegaan dat u al bekend met de concepten met Azure Table Storage-Service bent.</span><span class="sxs-lookup"><span data-stu-id="5b682-304">This section assumes that you are already familiar with the Azure Table Storage Service concepts.</span></span> <span data-ttu-id="5b682-305">Zie voor gedetailleerde informatie [inzicht in de tabel Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) en [aan de slag met Azure Table storage met .NET](storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="5b682-305">For detailed information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) and [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="5b682-306">In de volgende subsecties leert u hoe Azure Table storage-service met Azure PowerShell beheren.</span><span class="sxs-lookup"><span data-stu-id="5b682-306">In the following subsections, you'll learn how to manage Azure Table storage service using Azure PowerShell.</span></span> <span data-ttu-id="5b682-307">De scenario's worden behandeld: **maken**, **verwijderen**, en **bij het ophalen van** **tabellen**, evenals **toe te voegen**, **opvragen**, en **tabelentiteiten verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="5b682-307">The scenarios covered include **creating**, **deleting**, and **retrieving** **tables**, as well as **adding**, **querying**, and **deleting table entities**.</span></span>

### <a name="how-to-create-a-table"></a><span data-ttu-id="5b682-308">Het maken van een tabel</span><span class="sxs-lookup"><span data-stu-id="5b682-308">How to create a table</span></span>
<span data-ttu-id="5b682-309">Elke tabel moet zich bevinden in een Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="5b682-309">Every table must reside in an Azure storage account.</span></span> <span data-ttu-id="5b682-310">Het volgende voorbeeld laat zien hoe u een tabel maken in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="5b682-310">The following example demonstrates how to create a table in Azure Storage.</span></span> <span data-ttu-id="5b682-311">In het voorbeeld maakt eerst een verbinding met Azure Storage met context van het opslagaccount, waaronder de opslagaccountnaam en de toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="5b682-311">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="5b682-312">Vervolgens wordt de [nieuw AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet om een tabel maken in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="5b682-312">Next, it uses the [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet to create a table in Azure Storage.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-retrieve-a-table"></a><span data-ttu-id="5b682-313">Het ophalen van een tabel</span><span class="sxs-lookup"><span data-stu-id="5b682-313">How to retrieve a table</span></span>
<span data-ttu-id="5b682-314">U kunt een query en ophalen van een of alle tabellen in een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="5b682-314">You can query and retrieve one or all tables in a Storage account.</span></span> <span data-ttu-id="5b682-315">Het volgende voorbeeld toont hoe voor het ophalen van een tabel met de [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b682-315">The following example demonstrates how to retrieve a given table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span>

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

<span data-ttu-id="5b682-316">Als u de cmdlet Get-AzureStorageTable zonder parameters aanroept, krijgt alle opslagtabellen voor een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="5b682-316">If you call the Get-AzureStorageTable cmdlet without any parameters, it gets all storage tables for a Storage account.</span></span>

### <a name="how-to-delete-a-table"></a><span data-ttu-id="5b682-317">Het verwijderen van een tabel</span><span class="sxs-lookup"><span data-stu-id="5b682-317">How to delete a table</span></span>
<span data-ttu-id="5b682-318">U kunt een tabel uit een opslagaccount verwijderen met behulp van de [verwijderen AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b682-318">You can delete a table from a storage account by using the [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span></span>  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-to-manage-table-entities"></a><span data-ttu-id="5b682-319">Tabelentiteiten beheren</span><span class="sxs-lookup"><span data-stu-id="5b682-319">How to manage table entities</span></span>
<span data-ttu-id="5b682-320">Azure PowerShell biedt momenteel geen cmdlets voor het beheren van tabelentiteiten rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="5b682-320">Currently, Azure PowerShell does not provide cmdlets to manage table entities directly.</span></span> <span data-ttu-id="5b682-321">Om bewerkingen uitvoeren op tabelentiteiten, kunt u de klassen die zijn opgegeven in de [Azure Storage-clientbibliotheek voor .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span><span class="sxs-lookup"><span data-stu-id="5b682-321">To perform operations on table entities, you can use the classes given in the [Azure Storage Client Library for .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span></span>

#### <a name="how-to-add-table-entities"></a><span data-ttu-id="5b682-322">Het toevoegen van tabelentiteiten</span><span class="sxs-lookup"><span data-stu-id="5b682-322">How to add table entities</span></span>
<span data-ttu-id="5b682-323">Als u wilt een entiteit toevoegen aan een tabel, moet u eerst een object dat de entiteitseigenschappen van uw bepaalt maken.</span><span class="sxs-lookup"><span data-stu-id="5b682-323">To add an entity to a table, first create an object that defines your entity properties.</span></span> <span data-ttu-id="5b682-324">Een entiteit kan maximaal 255 eigenschappen, waaronder 3 eigenschappen hebben: **PartitionKey**, **RowKey**, en **tijdstempel**.</span><span class="sxs-lookup"><span data-stu-id="5b682-324">An entity can have up to 255 properties, including 3 system properties: **PartitionKey**, **RowKey**, and **Timestamp**.</span></span> <span data-ttu-id="5b682-325">U bent zelf verantwoordelijk voor het invoegen en het bijwerken van de waarden van **PartitionKey** en **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="5b682-325">You are responsible for inserting and updating the values of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="5b682-326">De server beheert de waarde van **tijdstempel**, die niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="5b682-326">The server manages the value of **Timestamp**, which cannot be modified.</span></span> <span data-ttu-id="5b682-327">Samen de **PartitionKey** en **RowKey** unieke identificatie van elke entiteit in een tabel.</span><span class="sxs-lookup"><span data-stu-id="5b682-327">Together the **PartitionKey** and **RowKey** uniquely identify every entity within a table.</span></span>

* <span data-ttu-id="5b682-328">**PartitionKey**: bepaalt de partitie die de entiteit is opgeslagen in.</span><span class="sxs-lookup"><span data-stu-id="5b682-328">**PartitionKey**: Determines the partition that the entity is stored in.</span></span>
* <span data-ttu-id="5b682-329">**RowKey**: een unieke identificatie van de entiteit in de partitie.</span><span class="sxs-lookup"><span data-stu-id="5b682-329">**RowKey**: Uniquely identifies the entity within the partition.</span></span>

<span data-ttu-id="5b682-330">U kunt maximaal 252 aangepaste eigenschappen voor een entiteit kan definiëren.</span><span class="sxs-lookup"><span data-stu-id="5b682-330">You may define up to 252 custom properties for an entity.</span></span> <span data-ttu-id="5b682-331">Zie voor meer informatie [inzicht in de tabel Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="5b682-331">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="5b682-332">Het volgende voorbeeld laat zien hoe entiteiten toevoegen aan een tabel.</span><span class="sxs-lookup"><span data-stu-id="5b682-332">The following example demonstrates how to add entities to a table.</span></span> <span data-ttu-id="5b682-333">In het voorbeeld laat zien hoe op te halen van de werknemerstabel en verschillende entiteiten in de App toevoegen.</span><span class="sxs-lookup"><span data-stu-id="5b682-333">The example shows how to retrieve the employee table and add several entities into it.</span></span> <span data-ttu-id="5b682-334">Deze maakt eerst een verbinding met Azure Storage met context van het opslagaccount, waaronder de opslagaccountnaam en de toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="5b682-334">First, it establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="5b682-335">Vervolgens haalt de opgegeven tabel met behulp van de [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b682-335">Next, it retrieves the given table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="5b682-336">Als de tabel niet bestaat, de [nieuw AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet gebruikt voor het maken van een tabel in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="5b682-336">If the table does not exist, the [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet is used to create a table in Azure Storage.</span></span> <span data-ttu-id="5b682-337">Het voorbeeld wordt vervolgens een aangepaste functie toevoegen-entiteit entiteiten toevoegen aan de tabel door elke entiteit partitie en rijsleutel te geven.</span><span class="sxs-lookup"><span data-stu-id="5b682-337">Next, the example defines a custom function Add-Entity to add entities to the table by specifying each entity's partition and row key.</span></span> <span data-ttu-id="5b682-338">De Add-entiteit functieaanroepen de [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet uit op de [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) klasse voor het maken van een entiteitsobject.</span><span class="sxs-lookup"><span data-stu-id="5b682-338">The Add-Entity function calls the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on the [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) class to create an entity object.</span></span> <span data-ttu-id="5b682-339">Later in het voorbeeld wordt de [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) methode voor dit entiteitsobject toe te voegen aan een tabel.</span><span class="sxs-lookup"><span data-stu-id="5b682-339">Later, the example calls the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) method on this entity object to add it to a table.</span></span>

```powershell
#Function Add-Entity: Adds an employee entity to a table.
function Add-Entity() {
    [CmdletBinding()]
    param(
       $table,
       [String]$partitionKey,
       [String]$rowKey,
       [String]$name,
       [Int]$id
    )

  $entity = New-Object -TypeName Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity -ArgumentList $partitionKey, $rowKey
  $entity.Properties.Add("Name", $name)
  $entity.Properties.Add("ID", $id)

  $result = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Insert($entity))
}

#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve the table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities to a table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-to-query-table-entities"></a><span data-ttu-id="5b682-340">Een query tabelentiteiten</span><span class="sxs-lookup"><span data-stu-id="5b682-340">How to query table entities</span></span>
<span data-ttu-id="5b682-341">Om te vragen een tabel, gebruikt u de [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) klasse.</span><span class="sxs-lookup"><span data-stu-id="5b682-341">To query a table, use the [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) class.</span></span> <span data-ttu-id="5b682-342">Het volgende voorbeeld wordt ervan uitgegaan dat u het script dat is opgegeven in de manier waarop al hebt uitgevoerd om toe te voegen entiteiten gedeelte van deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="5b682-342">The following example assumes that you've already run the script given in the How to add entities section of this guide.</span></span> <span data-ttu-id="5b682-343">In het voorbeeld maakt eerst een verbinding met Azure Storage met de opslag-context, waaronder de opslagaccountnaam en de toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="5b682-343">The example first establishes a connection to Azure Storage using the storage context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="5b682-344">Vervolgens wordt geprobeerd om op te halen van de eerder gemaakte 'werknemers' tabel met behulp van de [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b682-344">Next, it tries to retrieve the previously created "Employees" table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="5b682-345">Het aanroepen van de [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet uit op de klasse Microsoft.WindowsAzure.Storage.Table.TableQuery maakt een nieuwe query-object.</span><span class="sxs-lookup"><span data-stu-id="5b682-345">Calling the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on the Microsoft.WindowsAzure.Storage.Table.TableQuery class creates a new query object.</span></span> <span data-ttu-id="5b682-346">In het voorbeeld wordt gezocht naar de entiteiten die een 'ID-kolom waarvan de waarde 1 zoals opgegeven in een tekenreeks-filter is.</span><span class="sxs-lookup"><span data-stu-id="5b682-346">The example looks for the entities that have an 'ID' column whose value is 1 as specified in a string filter.</span></span> <span data-ttu-id="5b682-347">Zie voor gedetailleerde informatie [opvragen van tabellen en entiteiten](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span><span class="sxs-lookup"><span data-stu-id="5b682-347">For detailed information, see [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span></span> <span data-ttu-id="5b682-348">Wanneer u deze query uitvoert, wordt alle entiteiten die overeenkomen met de filtercriteria.</span><span class="sxs-lookup"><span data-stu-id="5b682-348">When you run this query, it returns all entities that match the filter criteria.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference to a table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns to select.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute the query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with the table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-to-delete-table-entities"></a><span data-ttu-id="5b682-349">Het verwijderen van de tabelentiteiten</span><span class="sxs-lookup"><span data-stu-id="5b682-349">How to delete table entities</span></span>
<span data-ttu-id="5b682-350">U kunt een entiteit met behulp van de sleutels van de partitie en rij verwijderen.</span><span class="sxs-lookup"><span data-stu-id="5b682-350">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="5b682-351">Het volgende voorbeeld wordt ervan uitgegaan dat u het script dat is opgegeven in de manier waarop al hebt uitgevoerd om toe te voegen entiteiten gedeelte van deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="5b682-351">The following example assumes that you've already run the script given in the How to add entities section of this guide.</span></span> <span data-ttu-id="5b682-352">In het voorbeeld maakt eerst een verbinding met Azure Storage met de opslag-context, waaronder de opslagaccountnaam en de toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="5b682-352">The example first establishes a connection to Azure Storage using the storage context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="5b682-353">Vervolgens wordt geprobeerd om op te halen van de eerder gemaakte 'werknemers' tabel met behulp van de [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b682-353">Next, it tries to retrieve the previously created "Employees" table using the [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="5b682-354">Als de tabel bestaat, in het voorbeeld wordt de [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) methode voor het ophalen van een entiteit op basis van de bijbehorende sleutelwaarden partitie en rij.</span><span class="sxs-lookup"><span data-stu-id="5b682-354">If the table exists, the example calls the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) method to retrieve an entity based on its partition and row key values.</span></span> <span data-ttu-id="5b682-355">Geeft u de entiteit de [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) methode om te verwijderen.</span><span class="sxs-lookup"><span data-stu-id="5b682-355">Then, pass the entity to the [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) method to delete.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve the table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If the table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together the PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete the entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-to-manage-azure-queues-and-queue-messages"></a><span data-ttu-id="5b682-356">Het beheren van Azure-wachtrijen en -berichten in wachtrij plaatsen</span><span class="sxs-lookup"><span data-stu-id="5b682-356">How to manage Azure queues and queue messages</span></span>
<span data-ttu-id="5b682-357">Azure Queue Storage is een service voor de opslag van grote aantallen berichten die via HTTP of HTTPS overal vandaan kunnen worden opgevraagd met geverifieerde aanroepen.</span><span class="sxs-lookup"><span data-stu-id="5b682-357">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in the world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="5b682-358">Deze sectie wordt ervan uitgegaan dat u al bekend met de concepten met Azure Queue Storage-Service bent.</span><span class="sxs-lookup"><span data-stu-id="5b682-358">This section assumes that you are already familiar with the Azure Queue Storage Service concepts.</span></span> <span data-ttu-id="5b682-359">Zie voor gedetailleerde informatie [aan de slag met Azure Queue storage met .NET](storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="5b682-359">For detailed information, see [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md).</span></span>

<span data-ttu-id="5b682-360">Deze sectie wordt beschreven hoe u voor het beheren van Azure Queue storage-service met Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b682-360">This section will show you how to manage Azure Queue storage service using Azure PowerShell.</span></span> <span data-ttu-id="5b682-361">De scenario's worden behandeld: **invoegen** en **verwijderen** wachtrij berichten, evenals **maken**, **verwijderen**, en **bij het ophalen van wachtrijen**.</span><span class="sxs-lookup"><span data-stu-id="5b682-361">The scenarios covered include **inserting** and **deleting** queue messages, as well as **creating**, **deleting**, and **retrieving queues**.</span></span>

### <a name="how-to-create-a-queue"></a><span data-ttu-id="5b682-362">Een wachtrij maken</span><span class="sxs-lookup"><span data-stu-id="5b682-362">How to create a queue</span></span>
<span data-ttu-id="5b682-363">Het volgende voorbeeld maakt eerst een verbinding met Azure Storage met context van het opslagaccount, waaronder de opslagaccountnaam en de toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="5b682-363">The following example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="5b682-364">Vervolgens roept [nieuw AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet voor het maken van een wachtrij met de naam 'wachtrijnaam'.</span><span class="sxs-lookup"><span data-stu-id="5b682-364">Next, it calls [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet to create a queue named 'queuename'.</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

<span data-ttu-id="5b682-365">Zie voor informatie over naamgevingsregels voor Azure Queue-Service, [naamgeving van wachtrijen en metagegevens](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="5b682-365">For information on naming conventions for Azure Queue Service, see [Naming Queues and Metadata](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

### <a name="how-to-retrieve-a-queue"></a><span data-ttu-id="5b682-366">Het ophalen van een wachtrij</span><span class="sxs-lookup"><span data-stu-id="5b682-366">How to retrieve a queue</span></span>
<span data-ttu-id="5b682-367">U kunt een query en ophalen van een specifieke wachtrij of een lijst met alle wachtrijen in een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="5b682-367">You can query and retrieve a specific queue or a list of all the queues in a Storage account.</span></span> <span data-ttu-id="5b682-368">Het volgende voorbeeld toont hoe voor het ophalen van een opgegeven wachtrij met de [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b682-368">The following example demonstrates how to retrieve a specified queue using the [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span></span>

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

<span data-ttu-id="5b682-369">Als u de [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet zonder parameters voor het ophalen van een lijst met alle wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="5b682-369">If you call the [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet without any parameters, it gets a list of all the queues.</span></span>

### <a name="how-to-delete-a-queue"></a><span data-ttu-id="5b682-370">Het verwijderen van een wachtrij</span><span class="sxs-lookup"><span data-stu-id="5b682-370">How to delete a queue</span></span>
<span data-ttu-id="5b682-371">Roep de cmdlet Remove-AzureStorageQueue voor het verwijderen van een wachtrij en alle berichten hierin.</span><span class="sxs-lookup"><span data-stu-id="5b682-371">To delete a queue and all the messages contained in it, call the Remove-AzureStorageQueue cmdlet.</span></span> <span data-ttu-id="5b682-372">Het volgende voorbeeld laat zien hoe een opgegeven wachtrij met de cmdlet Remove-AzureStorageQueue verwijderen.</span><span class="sxs-lookup"><span data-stu-id="5b682-372">The following example shows how to delete a specified queue using the Remove-AzureStorageQueue cmdlet.</span></span>

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-to-insert-a-message-into-a-queue"></a><span data-ttu-id="5b682-373">Het invoegen van een bericht in een wachtrij</span><span class="sxs-lookup"><span data-stu-id="5b682-373">How to insert a message into a queue</span></span>
<span data-ttu-id="5b682-374">Als u wilt invoegen van een bericht in een bestaande wachtrij maakt een nieuw exemplaar van de [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) klasse.</span><span class="sxs-lookup"><span data-stu-id="5b682-374">To insert a message into an existing queue, first create a new instance of the [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="5b682-375">Daarna roept u de methode [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) aan.</span><span class="sxs-lookup"><span data-stu-id="5b682-375">Next, call the [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method.</span></span> <span data-ttu-id="5b682-376">Een CloudQueueMessage kan worden gemaakt vanuit een tekenreeks (in UTF-8-indeling) of een byte-matrix.</span><span class="sxs-lookup"><span data-stu-id="5b682-376">A CloudQueueMessage can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="5b682-377">Het volgende voorbeeld laat zien hoe bericht toevoegen aan een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="5b682-377">The following example demonstrates how to add message to a queue.</span></span> <span data-ttu-id="5b682-378">In het voorbeeld maakt eerst een verbinding met Azure Storage met context van het opslagaccount, waaronder de opslagaccountnaam en de toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="5b682-378">The example first establishes a connection to Azure Storage using the storage account context, which includes the storage account name and its access key.</span></span> <span data-ttu-id="5b682-379">Vervolgens haalt de opgegeven wachtrij met behulp van de [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="5b682-379">Next, it retrieves the specified queue using the [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span></span> <span data-ttu-id="5b682-380">Als de wachtrij bestaat, de [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet gebruikt voor het maken van een exemplaar van de [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) klasse.</span><span class="sxs-lookup"><span data-stu-id="5b682-380">If the queue exists, the [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet is used to create an instance of the [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="5b682-381">Later in het voorbeeld wordt de [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) methode voor dit berichtobject toe te voegen aan een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="5b682-381">Later, the example calls the [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method on this message object to add it to a queue.</span></span> <span data-ttu-id="5b682-382">Hier volgt een code die een wachtrij opgehaald en het bericht 'MessageInfo':</span><span class="sxs-lookup"><span data-stu-id="5b682-382">Here is code which retrieves a queue and inserts the message 'MessageInfo':</span></span>

```powershell
#Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve the queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If the queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of the CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message to the queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-to-de-queue-at-the-next-message"></a><span data-ttu-id="5b682-383">Hoe u het volgende bericht uit de wachtrij</span><span class="sxs-lookup"><span data-stu-id="5b682-383">How to de-queue at the next message</span></span>
<span data-ttu-id="5b682-384">Met uw code wordt een bericht in twee stappen uit de wachtrij verwijderd.</span><span class="sxs-lookup"><span data-stu-id="5b682-384">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="5b682-385">Als u aanroept de [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) methode, krijgt u het volgende bericht in een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="5b682-385">When you call the [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) method, you get the next message in a queue.</span></span> <span data-ttu-id="5b682-386">Een bericht dat wordt geretourneerd door **GetMessage**, wordt onzichtbaar voor andere codes die berichten lezen uit deze wachtrij.</span><span class="sxs-lookup"><span data-stu-id="5b682-386">A message returned from **GetMessage** becomes invisible to any other code reading messages from this queue.</span></span> <span data-ttu-id="5b682-387">Voor het voltooien van het bericht uit de wachtrij te verwijderen, moet u ook aanroepen de [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) methode.</span><span class="sxs-lookup"><span data-stu-id="5b682-387">To finish removing the message from the queue, you must also call the [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) method.</span></span> <span data-ttu-id="5b682-388">Dit proces in twee stappen voor het verwijderen van een bericht zorgt ervoor dat als de code er niet in slaagt een bericht te verwerken vanwege hardware- of softwareproblemen, een ander exemplaar van uw code hetzelfde bericht kan ophalen en het opnieuw kan proberen.</span><span class="sxs-lookup"><span data-stu-id="5b682-388">This two-step process of removing a message assures that if your code fails to process a message due to hardware or software failure, another instance of your code can get the same message and try again.</span></span> <span data-ttu-id="5b682-389">Uw code haalt **DeleteMessage** op zodra het bericht is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="5b682-389">Your code calls **DeleteMessage** right after the message has been processed.</span></span>

```powershell
# Define the storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve the queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get the message object from the queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete the message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-to-manage-azure-file-shares-and-files"></a><span data-ttu-id="5b682-390">Azure-bestandsshares en bestanden beheren</span><span class="sxs-lookup"><span data-stu-id="5b682-390">How to manage Azure file shares and files</span></span>
<span data-ttu-id="5b682-391">Azure File storage biedt gedeelde opslag voor toepassingen die gebruikmaken van het standaard SMB-protocol.</span><span class="sxs-lookup"><span data-stu-id="5b682-391">Azure File storage offers shared storage for applications using the standard SMB protocol.</span></span> <span data-ttu-id="5b682-392">Microsoft Azure virtuele machines en cloudservices kunnen bestandsgegevens delen tussen toepassingsonderdelen via gekoppelde shares en on-premises toepassingen hebben toegang tot bestandsgegevens in een share via de API van File storage of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="5b682-392">Microsoft Azure virtual machines and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share via the File storage API or Azure PowerShell.</span></span>

<span data-ttu-id="5b682-393">Zie voor meer informatie over Azure File storage [aan de slag met Azure File storage in Windows](storage-dotnet-how-to-use-files.md) en [REST-API van bestand](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span><span class="sxs-lookup"><span data-stu-id="5b682-393">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) and [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span></span>

## <a name="how-to-set-and-query-storage-analytics"></a><span data-ttu-id="5b682-394">Het instellen en query storage analytics</span><span class="sxs-lookup"><span data-stu-id="5b682-394">How to set and query storage analytics</span></span>
<span data-ttu-id="5b682-395">U kunt [Azure Storage Analytics](storage-analytics.md) voor het verzamelen van metrische gegevens voor uw Azure storage-accounts en meld u gegevens over aanvragen die worden verzonden naar uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="5b682-395">You can use [Azure Storage Analytics](storage-analytics.md) to collect metrics for your Azure storage accounts and log data about requests sent to your storage account.</span></span> <span data-ttu-id="5b682-396">Metrische gegevens storage kunt u de status van een opslagaccount en opslag logboekregistratie voor het diagnosticeren en oplossen van problemen met uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="5b682-396">You can use storage metrics to monitor the health of a storage account, and storage logging to diagnose and troubleshoot issues with your storage account.</span></span> <span data-ttu-id="5b682-397">U kunt configureren met behulp van de Azure-portal of de Windows PowerShell of programmatisch met behulp van de storage-clientbibliotheek bewaking.</span><span class="sxs-lookup"><span data-stu-id="5b682-397">You can configure monitoring using the Azure portal or Windows PowerShell, or programmatically using the storage client library.</span></span> <span data-ttu-id="5b682-398">Opslag logboekregistratie gebeurt serverzijde en kunt u de details van de records voor geslaagde en mislukte aanvragen in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="5b682-398">Storage logging happens server-side and enables you to record details for both successful and failed requests in your storage account.</span></span> <span data-ttu-id="5b682-399">Deze logboeken kunnen u de details van lezen, schrijven en verwijderen van bewerkingen op tabellen, wachtrijen en blobs, evenals de redenen voor mislukte aanvragen.</span><span class="sxs-lookup"><span data-stu-id="5b682-399">These logs enable you to see details of read, write, and delete operations against your tables, queues, and blobs as well as the reasons for failed requests.</span></span>

<span data-ttu-id="5b682-400">Zie voor meer informatie over het inschakelen en weergeven van metrische gegevens Storage-gegevens met behulp van PowerShell, [inschakelen met behulp van PowerShell metrische gegevens Storage](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span><span class="sxs-lookup"><span data-stu-id="5b682-400">To learn how to enable and view Storage Metrics data using PowerShell, see [How to enable Storage Metrics using PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span></span>

<span data-ttu-id="5b682-401">Zie voor meer informatie over het inschakelen en ophalen van gegevens van registratie van opslag met behulp van PowerShell, [opslag logboekregistratie met behulp van PowerShell inschakelen](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) en [zoeken naar uw logboekgegevens opslag logboekregistratie](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span><span class="sxs-lookup"><span data-stu-id="5b682-401">To learn how to enable and retrieve Storage Logging data using PowerShell, see [How to enable Storage Logging using PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) and [Finding your Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span></span>
<span data-ttu-id="5b682-402">Zie voor gedetailleerde informatie over het gebruik van opslag metrische gegevens en opslag logboekregistratie met opslag oplossen [bewaking, diagnose en het oplossen van Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="5b682-402">For detailed information on using Storage Metrics and Storage Logging to troubleshoot storage issues, see [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).</span></span>

## <a name="how-to-manage-shared-access-signature-sas-and-stored-access-policy"></a><span data-ttu-id="5b682-403">Shared Access Signature (SAS) en opgeslagen toegangsbeleid beheren</span><span class="sxs-lookup"><span data-stu-id="5b682-403">How to manage Shared Access Signature (SAS) and Stored Access Policy</span></span>
<span data-ttu-id="5b682-404">Shared access signatures zijn een belangrijk onderdeel van het beveiligingsmodel voor elke toepassing met behulp van Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="5b682-404">Shared access signatures are an important part of the security model for any application using Azure Storage.</span></span> <span data-ttu-id="5b682-405">Ze zijn nuttig voor het bieden van beperkte machtigingen naar uw opslagaccount aan clients die niet de accountsleutel moeten hebben.</span><span class="sxs-lookup"><span data-stu-id="5b682-405">They are useful for providing limited permissions to your storage account to clients that should not have the account key.</span></span> <span data-ttu-id="5b682-406">Standaard kan alleen de eigenaar van het storage-account toegang tot blobs, tabellen en wachtrijen in dat account.</span><span class="sxs-lookup"><span data-stu-id="5b682-406">By default, only the owner of the storage account may access blobs, tables, and queues within that account.</span></span> <span data-ttu-id="5b682-407">Als uw service of toepassing moet deze resources beschikbaar te maken voor andere clients zonder het delen van uw toegangssleutel, hebt u drie opties:</span><span class="sxs-lookup"><span data-stu-id="5b682-407">If your service or application needs to make these resources available to other clients without sharing your access key, you have three options:</span></span>

* <span data-ttu-id="5b682-408">Stel de machtigingen van een container toe te staan anonieme leestoegang tot de container en de blobs.</span><span class="sxs-lookup"><span data-stu-id="5b682-408">Set a container's permissions to permit anonymous read access to the container and its blobs.</span></span> <span data-ttu-id="5b682-409">Dit is niet toegestaan voor tabellen of wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="5b682-409">This is not allowed for tables or queues.</span></span>
* <span data-ttu-id="5b682-410">Gebruik een shared access signature die verleent rechten voor containers, blobs, wachtrijen en tabellen voor een bepaald tijdsinterval beperkte.</span><span class="sxs-lookup"><span data-stu-id="5b682-410">Use a shared access signature that grants restricted access rights to containers, blobs, queues, and tables for a specific time interval.</span></span>
* <span data-ttu-id="5b682-411">Met een opgeslagen toegangsbeleid kunt u een extra verificatieniveau controle over handtekeningen voor gedeelde toegang voor een container of de blobs, voor een wachtrij of voor een tabel.</span><span class="sxs-lookup"><span data-stu-id="5b682-411">Use a stored access policy to obtain an additional level of control over shared access signatures for a container or its blobs, for a queue, or for a table.</span></span> <span data-ttu-id="5b682-412">Het opgeslagen toegangsbeleid kunt u de begintijd, de verlooptijd of de machtigingen voor een handtekening te wijzigen of om af te trekken nadat deze is uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="5b682-412">The stored access policy allows you to change the start time, expiry time, or permissions for a signature, or to revoke it after it has been issued.</span></span>

<span data-ttu-id="5b682-413">Een shared access signature kan worden gebruikt in een van twee vormen:</span><span class="sxs-lookup"><span data-stu-id="5b682-413">A shared access signature can be in one of two forms:</span></span>

* <span data-ttu-id="5b682-414">**Ad-hoc SAS**: wanneer u een ad-hoc SAS, de begintijd, de verlooptijd, maakt en machtigingen voor de SAS zijn opgegeven op de SAS-URI.</span><span class="sxs-lookup"><span data-stu-id="5b682-414">**Ad hoc SAS**: When you create an ad hoc SAS, the start time, expiry time, and permissions for the SAS are all specified on the SAS URI.</span></span> <span data-ttu-id="5b682-415">Dit type SAS kan worden gemaakt op een container, blob, table of wachtrij en het is niet worden ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="5b682-415">This type of SAS may be created on a container, blob, table, or queue and it is non-revocable.</span></span>
* <span data-ttu-id="5b682-416">**SAS met opgeslagen toegangsbeleid**: een opgeslagen-beleid is gedefinieerd in een resourcecontainer een blob-container, een tabel of een wachtrij - en u kunt deze gebruiken voor het beheren van beperkingen voor een of meer handtekeningen voor gedeelde toegang.</span><span class="sxs-lookup"><span data-stu-id="5b682-416">**SAS with stored access policy**: A stored access policy is defined on a resource container a blob container, table, or queue - and you can use it to manage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="5b682-417">Wanneer u een SAS aan een opgeslagen toegangsbeleid koppelt, neemt de SAS de beperkingen - de begintijd, verlooptijd en machtigingen - gedefinieerd voor het opgeslagen toegangsbeleid.</span><span class="sxs-lookup"><span data-stu-id="5b682-417">When you associate a SAS with a stored access policy, the SAS inherits the constraints - the start time, expiry time, and permissions - defined for the stored access policy.</span></span> <span data-ttu-id="5b682-418">Dit type SAS is worden ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="5b682-418">This type of SAS is revocable.</span></span>

<span data-ttu-id="5b682-419">Zie voor meer informatie [met behulp van Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) en [anonieme leestoegang tot containers en blobs beheren](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="5b682-419">For more information, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) and [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>

<span data-ttu-id="5b682-420">In de volgende gedeelten leert u hoe u een beleid voor gedeelde toegang handtekening access token en de opslag voor Azure-tabellen maakt.</span><span class="sxs-lookup"><span data-stu-id="5b682-420">In the next sections, you will learn how to create a shared access signature token and stored access policy for Azure tables.</span></span> <span data-ttu-id="5b682-421">Azure PowerShell biedt vergelijkbare cmdlets voor containers, blobs en wachtrijen ook.</span><span class="sxs-lookup"><span data-stu-id="5b682-421">Azure PowerShell provides similar cmdlets for containers, blobs, and queues as well.</span></span> <span data-ttu-id="5b682-422">Als u wilt de scripts uitvoeren in deze sectie, downloaden de [Azure PowerShell versie 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) of hoger.</span><span class="sxs-lookup"><span data-stu-id="5b682-422">To run the scripts in this section, download the [Azure PowerShell version 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) or later.</span></span>

### <a name="how-to-create-a-policy-based-shared-access-signature-token"></a><span data-ttu-id="5b682-423">Het maken van een op beleid gebaseerde Shared Access Signature-token</span><span class="sxs-lookup"><span data-stu-id="5b682-423">How to create a policy-based Shared Access Signature token</span></span>
<span data-ttu-id="5b682-424">Gebruik de cmdlet New-AzureStorageTableStoredAccessPolicy voor het maken van een nieuw opgeslagen-beleid.</span><span class="sxs-lookup"><span data-stu-id="5b682-424">Use the New-AzureStorageTableStoredAccessPolicy cmdlet to create a new stored access policy.</span></span> <span data-ttu-id="5b682-425">Roep vervolgens de [nieuw AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet voor het maken van een nieuw token van de handtekening gedeelde toegang op basis van beleid voor een Azure Storage-tabel.</span><span class="sxs-lookup"><span data-stu-id="5b682-425">Then, call the [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet to create a new policy-based shared access signature token for an Azure Storage table.</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-to-create-an-ad-hoc-non-revocable-shared-access-signature-token"></a><span data-ttu-id="5b682-426">Het maken van een ad-hoc (niet terughalen) Shared Access Signature-token</span><span class="sxs-lookup"><span data-stu-id="5b682-426">How to create an ad hoc (non-revocable) Shared Access Signature token</span></span>
<span data-ttu-id="5b682-427">Gebruik de [nieuw AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet voor het maken van een nieuw ad-hoc (niet terughalen) Shared Access Signature-token voor een Azure Storage-tabel:</span><span class="sxs-lookup"><span data-stu-id="5b682-427">Use the [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet to create a new ad hoc (non-revocable) Shared Access Signature token for an Azure Storage table:</span></span>

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-to-create-a-stored-access-policy"></a><span data-ttu-id="5b682-428">Het maken van een opgeslagen-beleid</span><span class="sxs-lookup"><span data-stu-id="5b682-428">How to create a stored access policy</span></span>
<span data-ttu-id="5b682-429">Gebruik de cmdlet New-AzureStorageTableStoredAccessPolicy voor het maken van een nieuwe opgeslagen toegangsbeleid voor een Azure Storage-tabel:</span><span class="sxs-lookup"><span data-stu-id="5b682-429">Use the New-AzureStorageTableStoredAccessPolicy cmdlet to create a new stored access policy for an Azure Storage table:</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-to-update-a-stored-access-policy"></a><span data-ttu-id="5b682-430">Het bijwerken van een opgeslagen-beleid</span><span class="sxs-lookup"><span data-stu-id="5b682-430">How to update a stored access policy</span></span>
<span data-ttu-id="5b682-431">Gebruik de cmdlet Set-AzureStorageTableStoredAccessPolicy een bestaand opgeslagen toegangsbeleid voor een Azure Storage-tabel bijwerken:</span><span class="sxs-lookup"><span data-stu-id="5b682-431">Use the Set-AzureStorageTableStoredAccessPolicy cmdlet to update an existing stored access policy for an Azure Storage table:</span></span>

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-to-delete-a-stored-access-policy"></a><span data-ttu-id="5b682-432">Het verwijderen van een opgeslagen-beleid</span><span class="sxs-lookup"><span data-stu-id="5b682-432">How to delete a stored access policy</span></span>
<span data-ttu-id="5b682-433">Gebruik de cmdlet Remove-AzureStorageTableStoredAccessPolicy verwijderen van een opgeslagen-beleid in de tabel in een Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="5b682-433">Use the Remove-AzureStorageTableStoredAccessPolicy cmdlet to delete a stored access policy on an Azure Storage table:</span></span>

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-to-use-azure-storage-for-us-government-and-azure-china"></a><span data-ttu-id="5b682-434">Azure Storage gebruiken voor de Amerikaanse overheid en Azure voor China</span><span class="sxs-lookup"><span data-stu-id="5b682-434">How to use Azure Storage for U.S. government and Azure China</span></span>
<span data-ttu-id="5b682-435">Een Azure-omgeving is een onafhankelijke implementatie van Microsoft Azure, zoals [Azure Government voor de overheid van de VS](https://azure.microsoft.com/features/gov/), [AzureCloud voor globale Azure](https://portal.azure.com), en [AzureChinaCloud voor Azure wordt beheerd door 21Vianet in China](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="5b682-435">An Azure environment is an independent deployment of Microsoft Azure, such as [Azure Government for U.S. government](https://azure.microsoft.com/features/gov/), [AzureCloud for global Azure](https://portal.azure.com), and [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span> <span data-ttu-id="5b682-436">U kunt nieuwe Azure-omgevingen voor Amerikaanse overheid en Azure voor China implementeren.</span><span class="sxs-lookup"><span data-stu-id="5b682-436">You can deploy new Azure environments for U.S government and Azure China.</span></span>

<span data-ttu-id="5b682-437">Voor het gebruik van Azure Storage met AzureChinaCloud, moet u een opslag-context die is gekoppeld aan AzureChinaCloud maken.</span><span class="sxs-lookup"><span data-stu-id="5b682-437">To use Azure Storage with AzureChinaCloud, you need to create a storage context that is associated with AzureChinaCloud.</span></span> <span data-ttu-id="5b682-438">Volg deze stappen om u aan de slag:</span><span class="sxs-lookup"><span data-stu-id="5b682-438">Follow these steps to get you started:</span></span>

1. <span data-ttu-id="5b682-439">Voer de [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet om te controleren van de beschikbare Azure-omgevingen:</span><span class="sxs-lookup"><span data-stu-id="5b682-439">Run the [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet to see the available Azure environments:</span></span>
   
    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="5b682-440">Een Azure China-account toevoegen aan Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5b682-440">Add an Azure China account to Windows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. <span data-ttu-id="5b682-441">Maak een context opslag voor een account AzureChinaCloud:</span><span class="sxs-lookup"><span data-stu-id="5b682-441">Create a storage context for an AzureChinaCloud account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

<span data-ttu-id="5b682-442">Azure Storage met gebruiken [VS Azure Government](https://azure.microsoft.com/features/gov/), moet u een nieuwe omgeving definiëren en vervolgens een nieuwe opslag context maken met deze omgeving:</span><span class="sxs-lookup"><span data-stu-id="5b682-442">To use Azure Storage with [U.S. Azure Government](https://azure.microsoft.com/features/gov/), you should define a new environment and then create a new storage context with this environment:</span></span>

1. <span data-ttu-id="5b682-443">Voer de [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet om te controleren van de beschikbare Azure-omgevingen:</span><span class="sxs-lookup"><span data-stu-id="5b682-443">Run the [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet to see the available Azure environments:</span></span>

    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="5b682-444">Een Azure US Government-account toevoegen aan Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="5b682-444">Add an Azure US Government account to Windows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. <span data-ttu-id="5b682-445">Maak een context opslag voor een account AzureUSGovernment:</span><span class="sxs-lookup"><span data-stu-id="5b682-445">Create a storage context for an AzureUSGovernment account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
<span data-ttu-id="5b682-446">Zie voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="5b682-446">For more information, see:</span></span>

* <span data-ttu-id="5b682-447">[Ontwikkelaarshandleiding voor Microsoft Azure Government](../azure-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="5b682-447">[Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>
* [<span data-ttu-id="5b682-448">Overzicht van verschillen bij het maken van een toepassing op China Service</span><span class="sxs-lookup"><span data-stu-id="5b682-448">Overview of Differences When Creating an Application on China Service</span></span>](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a><span data-ttu-id="5b682-449">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5b682-449">Next Steps</span></span>
<span data-ttu-id="5b682-450">In deze handleiding hebt u geleerd hoe Azure Storage met Azure PowerShell beheren.</span><span class="sxs-lookup"><span data-stu-id="5b682-450">In this guide, you've learned how to manage Azure Storage with Azure PowerShell.</span></span> <span data-ttu-id="5b682-451">Hier volgen enkele verwante artikelen en resources voor meer informatie hierover.</span><span class="sxs-lookup"><span data-stu-id="5b682-451">Here are some related articles and resources for learning more about them.</span></span>

* [<span data-ttu-id="5b682-452">Documentatie bij Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5b682-452">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="5b682-453">PowerShell-Cmdlets voor Azure-opslag</span><span class="sxs-lookup"><span data-stu-id="5b682-453">Azure Storage PowerShell Cmdlets</span></span>](/powershell/module/azurerm.storage/#storage)
* [<span data-ttu-id="5b682-454">Windows PowerShell-referentie</span><span class="sxs-lookup"><span data-stu-id="5b682-454">Windows PowerShell Reference</span></span>](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How to manage storage accounts in Azure]: #manageaccount
[How to set a default Azure subscription]: #setdefsub
[How to create a new Azure storage account]: #createaccount
[How to set a default Azure storage account]: #defaultaccount
[How to list all Azure storage accounts in a subscription]: #listaccounts
[How to create an Azure storage context]: #createctx
[How to manage Azure blobs and blob snapshots]: #manageblobs
[How to create a container]: #container
[How to upload a blob into a container]: #uploadblob
[How to download blobs from a container]: #downblob
[How to copy blobs from one storage container to another]: #copyblob
[How to delete a blob]: #deleteblob
[How to manage Azure blob snapshots]: #manageshots
[How to create a blob snapshot]: #createshot
[How to list snapshots of a blob]: #listshot
[How to copy a snapshot of a blob]: #copyshot
[How to manage Azure tables and table entities]: #managetables
[How to create a table]: #createtable
[How to retrieve a table]: #gettable
[How to delete a table]: #remtable
[How to manage table entities]: #mngentity
[How to add table entities]: #addentity
[How to query table entities]: #queryentity
[How to delete table entities]: #deleteentity
[How to manage Azure queues and queue messages]: #managequeues
[How to create a queue]: #createqueue
[How to retrieve a queue]: #getqueue
[How to delete a queue]: #remqueue
[How to manage queue messages]: #mngqueuemsg
[How to insert a message into a queue]: #addqueuemsg
[How to de-queue at the next message]: #dequeuemsg
[How to manage Azure file shares and files]: #files
[How to set and query storage analytics]: #stganalytics
[How to manage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How to use Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
