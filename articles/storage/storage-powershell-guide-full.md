---
title: aaaUsing Azure PowerShell gebruiken met Azure Storage | Microsoft Docs
description: Meer informatie over hoe toouse hello Azure PowerShell-cmdlets voor Azure Storage toocreate en beheren van opslagaccounts; werken met blobs, tabellen, wachtrijen en bestanden. configureren en storage analytics query en handtekeningen voor gedeelde toegang maken.
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
ms.openlocfilehash: befe7adda2384f8bcdb8b9f1a063e4eafc158271
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-azure-powershell-with-azure-storage"></a><span data-ttu-id="25c31-103">Azure PowerShell gebruiken met Azure Storage</span><span class="sxs-lookup"><span data-stu-id="25c31-103">Using Azure PowerShell with Azure Storage</span></span>
## <a name="overview"></a><span data-ttu-id="25c31-104">Overzicht</span><span class="sxs-lookup"><span data-stu-id="25c31-104">Overview</span></span>
<span data-ttu-id="25c31-105">Azure PowerShell is een module die cmdlets toomanage Azure via Windows PowerShell biedt.</span><span class="sxs-lookup"><span data-stu-id="25c31-105">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="25c31-106">Het is een op taken gebaseerde opdrachtregelshell en scripttaal die speciaal is ontworpen voor systeembeheer.</span><span class="sxs-lookup"><span data-stu-id="25c31-106">It is a task-based command-line shell and scripting language designed especially for system administration.</span></span> <span data-ttu-id="25c31-107">Met PowerShell, kunt u eenvoudig beheren en automatiseren Hallo beheer van uw Azure-services en toepassingen.</span><span class="sxs-lookup"><span data-stu-id="25c31-107">With PowerShell, you can easily control and automate hello administration of your Azure services and applications.</span></span> <span data-ttu-id="25c31-108">Bijvoorbeeld, kunt u Hallo cmdlets tooperform Hallo dezelfde taken kunt u uitvoeren via Hallo [Azure-portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="25c31-108">For example, you can use hello cmdlets tooperform hello same tasks that you can perform through hello [Azure portal](https://portal.azure.com).</span></span>

<span data-ttu-id="25c31-109">In deze handleiding wordt besproken hoe toouse hello [Azure-opslag-Cmdlets](/powershell/module/azurerm.storage/#storage) tooperform tal van ontwikkeling en het beheer van taken met Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="25c31-109">In this guide, we'll explore how toouse hello [Azure Storage Cmdlets](/powershell/module/azurerm.storage/#storage) tooperform a variety of development and administration tasks with Azure Storage.</span></span>

<span data-ttu-id="25c31-110">Deze handleiding wordt ervan uitgegaan dat u ervaring met behulp van [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) en [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span><span class="sxs-lookup"><span data-stu-id="25c31-110">This guide assumes that you have prior experience using [Azure Storage](https://azure.microsoft.com/documentation/services/storage/) and [Windows PowerShell](http://technet.microsoft.com/library/bb978526.aspx).</span></span> <span data-ttu-id="25c31-111">Hallo handleiding biedt een aantal scripts toodemonstrate Hallo informatie over het gebruik van PowerShell met Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="25c31-111">hello guide provides a number of scripts toodemonstrate hello usage of PowerShell with Azure Storage.</span></span> <span data-ttu-id="25c31-112">Hallo scriptvariabelen op basis van uw configuratie voordat elk script wordt uitgevoerd, moet u bijwerken.</span><span class="sxs-lookup"><span data-stu-id="25c31-112">You should update hello script variables based on your configuration before running each script.</span></span>

<span data-ttu-id="25c31-113">de eerste sectie Hallo in deze handleiding biedt een kijkje Azure Storage en PowerShell.</span><span class="sxs-lookup"><span data-stu-id="25c31-113">hello first section in this guide provides a quick glance at Azure Storage and PowerShell.</span></span> <span data-ttu-id="25c31-114">Voor gedetailleerde informatie en instructies starten vanuit Hallo [vereisten voor het gebruik van Azure PowerShell met Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span><span class="sxs-lookup"><span data-stu-id="25c31-114">For detailed information and instructions, start from hello [Prerequisites for using Azure PowerShell with Azure Storage](#prerequisites-for-using-azure-powershell-with-azure-storage).</span></span>

## <a name="getting-started-with-azure-storage-and-powershell-in-5-minutes"></a><span data-ttu-id="25c31-115">Aan de slag met Azure Storage en PowerShell in vijf minuten</span><span class="sxs-lookup"><span data-stu-id="25c31-115">Getting started with Azure Storage and PowerShell in 5 minutes</span></span>
<span data-ttu-id="25c31-116">Deze sectie leest u hoe tooaccess Azure Storage via PowerShell in vijf minuten.</span><span class="sxs-lookup"><span data-stu-id="25c31-116">This section shows you how tooaccess Azure Storage via PowerShell in 5 minutes.</span></span>

<span data-ttu-id="25c31-117">**Nieuwe tooAzure:** ophalen van een Microsoft Azure-abonnement en een Microsoft-account die is gekoppeld aan dat abonnement.</span><span class="sxs-lookup"><span data-stu-id="25c31-117">**New tooAzure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="25c31-118">Zie voor informatie over Azure-Aankoopopties, [gratis proefversie](https://azure.microsoft.com/pricing/free-trial/), [kopen opties](https://azure.microsoft.com/pricing/purchase-options/), en [lid biedt](https://azure.microsoft.com/pricing/member-offers/) (voor leden van MSDN, Microsoft Partner Network BizSpark en andere Microsoft-programma's).</span><span class="sxs-lookup"><span data-stu-id="25c31-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="25c31-119">Zie [beheerdersrollen toewijzen in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) voor meer informatie over Azure-abonnementen.</span><span class="sxs-lookup"><span data-stu-id="25c31-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="25c31-120">**Na het maken van een Microsoft Azure-abonnement en -account:**</span><span class="sxs-lookup"><span data-stu-id="25c31-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="25c31-121">Download en installeer Hallo nieuwste [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span><span class="sxs-lookup"><span data-stu-id="25c31-121">Download and install hello latest [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/latest).</span></span>
2. <span data-ttu-id="25c31-122">Start Windows PowerShell Integrated Scripting Environment (ISE): Ga In uw lokale computer toohello **Start** menu.</span><span class="sxs-lookup"><span data-stu-id="25c31-122">Start Windows PowerShell Integrated Scripting Environment (ISE): In your local computer, go toohello **Start** menu.</span></span> <span data-ttu-id="25c31-123">Type **Systeembeheer** en toorun op deze.</span><span class="sxs-lookup"><span data-stu-id="25c31-123">Type **Administrative Tools** and click toorun it.</span></span> <span data-ttu-id="25c31-124">In Hallo **Systeembeheer** venster met de rechtermuisknop op **Windows PowerShell ISE**, klikt u op **als Administrator uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="25c31-124">In hello **Administrative Tools** window, right-click **Windows PowerShell ISE**, click **Run as Administrator**.</span></span>
3. <span data-ttu-id="25c31-125">In **Windows PowerShell ISE**, klikt u op **bestand** > **nieuw** toocreate een nieuwe scriptbestand.</span><span class="sxs-lookup"><span data-stu-id="25c31-125">In **Windows PowerShell ISE**, click **File** > **New** toocreate a new script file.</span></span>
4. <span data-ttu-id="25c31-126">Nu geven we u een eenvoudig script waarin basic PowerShell-opdrachten tooaccess Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="25c31-126">Now, we'll give you a simple script that shows basic PowerShell commands tooaccess Azure Storage.</span></span> <span data-ttu-id="25c31-127">Hallo script vraagt uw Azure-account referenties tooadd eerst uw Azure-account toohello lokale PowerShell-omgeving.</span><span class="sxs-lookup"><span data-stu-id="25c31-127">hello script will first ask your Azure account credentials tooadd your Azure account toohello local PowerShell environment.</span></span> <span data-ttu-id="25c31-128">Hallo-script wordt vervolgens Hallo standaard Azure-abonnement instellen en een nieuw opslagaccount maken in Azure.</span><span class="sxs-lookup"><span data-stu-id="25c31-128">Then, hello script will set hello default Azure subscription and create a new storage account in Azure.</span></span> <span data-ttu-id="25c31-129">Hallo-script wordt vervolgens een nieuwe container in deze nieuwe opslagaccount maken en uploaden van een bestaande installatiekopie-bestand (blob) toothat container.</span><span class="sxs-lookup"><span data-stu-id="25c31-129">Next, hello script will create a new container in this new storage account and upload an existing image file (blob) toothat container.</span></span> <span data-ttu-id="25c31-130">Nadat het Hallo-script geeft een lijst van alle blobs in de container, worden een nieuwe bestemming-map maken in uw lokale computer en Hallo installatiekopiebestand downloaden.</span><span class="sxs-lookup"><span data-stu-id="25c31-130">After hello script lists all blobs in that container, it will create a new destination directory in your local computer and download hello image file.</span></span>
5. <span data-ttu-id="25c31-131">Selecteer in de Hallo volgende sectie code, Hallo script tussen Opmerking Hallo **#beginnen** en **#end**.</span><span class="sxs-lookup"><span data-stu-id="25c31-131">In hello following code section, select hello script between hello remarks **#begin** and **#end**.</span></span> <span data-ttu-id="25c31-132">Druk op CTRL + C toocopy het toohello Klembord.</span><span class="sxs-lookup"><span data-stu-id="25c31-132">Press CTRL+C toocopy it toohello clipboard.</span></span>

    ```powershell
    # begin
    # Update with hello name of your subscription.
    $SubscriptionName = "YourSubscriptionName"
       
    # Give a name tooyour new storage account. It must be lowercase!
    $StorageAccountName = "yourstorageaccountname"
       
    # Choose "West US" as an example.
    $Location = "West US"
       
    # Give a name tooyour new container.
    $ContainerName = "imagecontainer"
       
    # Have an image file and a source directory in your local computer.
    $ImageToUpload = "C:\Images\HelloWorld.png"
       
    # A destination directory in your local computer.
    $DestinationFolder = "C:\DownloadImages"
       
    # Add your Azure account toohello local PowerShell environment.
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
       
    # Download blobs from hello container:
    # Get a reference tooa list of all blobs in a container.
    $blobs = Get-AzureStorageBlob -Container $ContainerName
       
    # Create hello destination directory.
    New-Item -Path $DestinationFolder -ItemType Directory -Force  
       
    # Download blobs into hello local destination directory.
    $blobs | Get-AzureStorageBlobContent –Destination $DestinationFolder
       
    # end
    ```

6. <span data-ttu-id="25c31-133">In **Windows PowerShell ISE**, druk op CTRL + V toocopy Hallo script.</span><span class="sxs-lookup"><span data-stu-id="25c31-133">In **Windows PowerShell ISE**, press CTRL+V toocopy hello script.</span></span> <span data-ttu-id="25c31-134">Klik op **bestand** > **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="25c31-134">Click **File** > **Save**.</span></span> <span data-ttu-id="25c31-135">In Hallo **OpslaanAls** dialoogvenster, Hallo-typenaam van Hallo scriptbestand, zoals 'mystoragescript'.</span><span class="sxs-lookup"><span data-stu-id="25c31-135">In hello **Save As** dialog window, type hello name of hello script file, such as "mystoragescript."</span></span> <span data-ttu-id="25c31-136">Klik op **Opslaan**.</span><span class="sxs-lookup"><span data-stu-id="25c31-136">Click **Save**.</span></span>
7. <span data-ttu-id="25c31-137">U moet nu tooupdate Hallo scriptvariabelen op basis van uw configuratie-instellingen.</span><span class="sxs-lookup"><span data-stu-id="25c31-137">Now, you need tooupdate hello script variables based on your configuration settings.</span></span> <span data-ttu-id="25c31-138">U moet bijwerken Hallo **$SubscriptionName** variabele met uw eigen abonnement.</span><span class="sxs-lookup"><span data-stu-id="25c31-138">You must update hello **$SubscriptionName** variable with your own subscription.</span></span> <span data-ttu-id="25c31-139">U kunt behouden Hallo andere variabelen zoals opgegeven in het Hallo-script of deze als u wilt bijwerken.</span><span class="sxs-lookup"><span data-stu-id="25c31-139">You can keep hello other variables as specified in hello script or update them as you wish.</span></span>
   
   * <span data-ttu-id="25c31-140">**$SubscriptionName:** moet u deze variabele bijwerken met de naam van uw eigen abonnement.</span><span class="sxs-lookup"><span data-stu-id="25c31-140">**$SubscriptionName:** You must update this variable with your own subscription name.</span></span> <span data-ttu-id="25c31-141">Voer een van de Hallo drie manieren toolocate Hallo naam van uw abonnement te volgen:</span><span class="sxs-lookup"><span data-stu-id="25c31-141">Follow one of hello following three ways toolocate hello name of your subscription:</span></span>
     
    <span data-ttu-id="25c31-142">a.</span><span class="sxs-lookup"><span data-stu-id="25c31-142">a.</span></span> <span data-ttu-id="25c31-143">In **Windows PowerShell ISE**, klikt u op **bestand** > **nieuw** toocreate een nieuwe scriptbestand.</span><span class="sxs-lookup"><span data-stu-id="25c31-143">In **Windows PowerShell ISE**, click **File** > **New** toocreate a new script file.</span></span> <span data-ttu-id="25c31-144">Kopiëren Hallo hieronder nieuwe scriptbestand toohello script en klik **Debug** > **uitvoeren**.</span><span class="sxs-lookup"><span data-stu-id="25c31-144">Copy hello following script toohello new script file and click **Debug** > **Run**.</span></span> <span data-ttu-id="25c31-145">Hallo volgende script wordt eerst vraagt u uw Azure-account referenties tooadd uw Azure-account toohello lokale PowerShell-omgeving en alle Hallo-abonnementen die verbonden toohello lokale PowerShell-sessie zijn wordt weergegeven.</span><span class="sxs-lookup"><span data-stu-id="25c31-145">hello following script will first ask your Azure account credentials tooadd your Azure account toohello local PowerShell environment and then show all hello subscriptions that are connected toohello local PowerShell session.</span></span> <span data-ttu-id="25c31-146">Noteer Hallo-naam van het Hallo-abonnement dat u wilt dat toouse tijdens deze zelfstudie te volgen:</span><span class="sxs-lookup"><span data-stu-id="25c31-146">Take a note of hello name of hello subscription that you want toouse while following this tutorial:</span></span>
     
    ```powershell
    Add-AzureAccount 
      Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName
    ```

    <span data-ttu-id="25c31-147">b.</span><span class="sxs-lookup"><span data-stu-id="25c31-147">b.</span></span> <span data-ttu-id="25c31-148">toolocate en kopieert u uw abonnement een naam in Hallo [Azure-portal](https://portal.azure.com), Hallo Hub-menu op Hallo links in, klik op **abonnementen**.</span><span class="sxs-lookup"><span data-stu-id="25c31-148">toolocate and copy your subscription name in hello [Azure portal](https://portal.azure.com), in hello Hub menu on hello left, click **Subscriptions**.</span></span> <span data-ttu-id="25c31-149">Hallo-naam van het abonnement dat u tijdens het uitvoeren van scripts Hallo in deze handleiding toouse wilt kopiëren.</span><span class="sxs-lookup"><span data-stu-id="25c31-149">Copy hello name of subscription that you want toouse while running hello scripts in this guide.</span></span>
     
     ![Azure Portal](./media/storage-powershell-guide-full/Subscription_Previewportal.png)

    <span data-ttu-id="25c31-151">c.</span><span class="sxs-lookup"><span data-stu-id="25c31-151">c.</span></span> <span data-ttu-id="25c31-152">toolocate en kopieert u uw abonnement een naam in Hallo [klassieke Azure-Portal](https://manage.windowsazure.com/), schuif naar beneden en klik op **instellingen** op Hallo linkerkant van Hallo-portal.</span><span class="sxs-lookup"><span data-stu-id="25c31-152">toolocate and copy your subscription name in hello [Azure Classic Portal](https://manage.windowsazure.com/), scroll down and click **Settings** on hello left side of hello portal.</span></span> <span data-ttu-id="25c31-153">Klik op **abonnementen** toosee een lijst van uw abonnementen.</span><span class="sxs-lookup"><span data-stu-id="25c31-153">Click **Subscriptions** toosee a list of your subscriptions.</span></span> <span data-ttu-id="25c31-154">Hallo-naam van het abonnement dat u toouse tijdens het uitvoeren van Hallo-scripts die zijn opgegeven in deze handleiding wilt kopiëren.</span><span class="sxs-lookup"><span data-stu-id="25c31-154">Copy hello name of subscription that you want toouse while running hello scripts given in this guide.</span></span>
     
     ![Klassieke Azure-portal](./media/storage-powershell-guide-full/Subscription_currentportal.png)

   * <span data-ttu-id="25c31-156">**$StorageAccountName:** Hallo naam die in het Hallo-script gebruiken of voer een nieuwe naam voor uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="25c31-156">**$StorageAccountName:** Use hello given name in hello script or enter a new name for your storage account.</span></span> <span data-ttu-id="25c31-157">**Belangrijk:** Hallo-naam van Hallo opslagaccount moet uniek zijn in Azure.</span><span class="sxs-lookup"><span data-stu-id="25c31-157">**Important:** hello name of hello storage account must be unique in Azure.</span></span> <span data-ttu-id="25c31-158">Er moet een kleine letter, te!</span><span class="sxs-lookup"><span data-stu-id="25c31-158">It must be lowercase, too!</span></span>
   * <span data-ttu-id="25c31-159">**$Location:** Hallo 'VS-West' opgegeven in Hallo script gebruiken of kies andere Azure locaties, zoals VS-Oost, Noord-Europa, enzovoort.</span><span class="sxs-lookup"><span data-stu-id="25c31-159">**$Location:** Use hello given "West US" in hello script or choose other Azure locations, such as East US, North Europe, and so on.</span></span>
   * <span data-ttu-id="25c31-160">**$ContainerName:** Hallo naam die in het Hallo-script gebruiken of voer een nieuwe naam voor de container.</span><span class="sxs-lookup"><span data-stu-id="25c31-160">**$ContainerName:** Use hello given name in hello script or enter a new name for your container.</span></span>
   * <span data-ttu-id="25c31-161">**$ImageToUpload:** Voer een pad tooa afbeelding op uw lokale computer, zoals: 'C:\Images\HelloWorld.png'.</span><span class="sxs-lookup"><span data-stu-id="25c31-161">**$ImageToUpload:** Enter a path tooa picture on your local computer, such as: "C:\Images\HelloWorld.png".</span></span>
   * <span data-ttu-id="25c31-162">**$DestinationFolder:** Enter een pad tooa lokale directory toostore bestanden gedownload van Azure Storage, zoals: 'C:\DownloadImages'.</span><span class="sxs-lookup"><span data-stu-id="25c31-162">**$DestinationFolder:** Enter a path tooa local directory toostore files downloaded from Azure Storage, such as: "C:\DownloadImages".</span></span>
8. <span data-ttu-id="25c31-163">Klik na het bijwerken van Hallo scriptvariabelen in Hallo 'mystoragescript.ps1' bestand **bestand** > **opslaan**.</span><span class="sxs-lookup"><span data-stu-id="25c31-163">After updating hello script variables in hello "mystoragescript.ps1" file, click **File** > **Save**.</span></span> <span data-ttu-id="25c31-164">Klik vervolgens op **Debug** > **uitvoeren** of druk op **F5** toorun Hallo script.</span><span class="sxs-lookup"><span data-stu-id="25c31-164">Then, click **Debug** > **Run** or press **F5** toorun hello script.</span></span>  

<span data-ttu-id="25c31-165">Nadat het Hallo-script wordt uitgevoerd, moet u een lokale doelmap met Hallo gedownload bestand hebben.</span><span class="sxs-lookup"><span data-stu-id="25c31-165">After hello script runs, you should have a local destination folder that includes hello downloaded image file.</span></span> <span data-ttu-id="25c31-166">Hallo volgende schermafbeelding ziet u een voorbeeld van uitvoer:</span><span class="sxs-lookup"><span data-stu-id="25c31-166">hello following screenshot shows an example output:</span></span>

![Blobs downloaden](./media/storage-powershell-guide-full/Blobdownload.png)

> [!NOTE]
> <span data-ttu-id="25c31-168">Hallo "Aan de slag met Azure Storage en PowerShell in vijf minuten" sectie opgegeven een korte inleiding voor het toouse Azure PowerShell gebruiken met Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="25c31-168">hello "Getting started with Azure Storage and PowerShell in 5 minutes" section provided a quick introduction on how toouse Azure PowerShell with Azure Storage.</span></span> <span data-ttu-id="25c31-169">Voor gedetailleerde informatie en instructies raden we u tooread Hallo uit te voeren.</span><span class="sxs-lookup"><span data-stu-id="25c31-169">For detailed information and instructions, we encourage you tooread hello following sections.</span></span>
> 

## <a name="prerequisites-for-using-azure-powershell-with-azure-storage"></a><span data-ttu-id="25c31-170">Vereisten voor het gebruik van Azure PowerShell met Azure Storage</span><span class="sxs-lookup"><span data-stu-id="25c31-170">Prerequisites for using Azure PowerShell with Azure Storage</span></span>
<span data-ttu-id="25c31-171">U moet een Azure-abonnement en account toorun Hallo PowerShell-cmdlets die in deze handleiding, zoals hierboven is beschreven.</span><span class="sxs-lookup"><span data-stu-id="25c31-171">You need an Azure subscription and account toorun hello PowerShell cmdlets given in this guide, as described above.</span></span>

<span data-ttu-id="25c31-172">Azure PowerShell is een module die cmdlets toomanage Azure via Windows PowerShell biedt.</span><span class="sxs-lookup"><span data-stu-id="25c31-172">Azure PowerShell is a module that provides cmdlets toomanage Azure through Windows PowerShell.</span></span> <span data-ttu-id="25c31-173">Zie voor meer informatie over het installeren en instellen van Azure PowerShell [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="25c31-173">For information on installing and setting up Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> <span data-ttu-id="25c31-174">U wordt aangeraden dat u downloaden en installeren of upgraden van de meest recente Azure PowerShell-module toohello voordat u deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="25c31-174">We recommend that you download and install or upgrade toohello latest Azure PowerShell module before using this guide.</span></span>

<span data-ttu-id="25c31-175">U kunt Hallo-cmdlets uitvoeren in Hallo Windows PowerShell-console of Hallo Windows PowerShell Integrated Scripting Environment (ISE).</span><span class="sxs-lookup"><span data-stu-id="25c31-175">You can run hello cmdlets in hello standard Windows PowerShell console or hello Windows PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="25c31-176">Bijvoorbeeld: tooopen **Windows PowerShell ISE**toohello startmenu gaat, typt u Systeembeheer en toorun op deze.</span><span class="sxs-lookup"><span data-stu-id="25c31-176">For example, tooopen **Windows PowerShell ISE**, go toohello Start menu, type Administrative Tools and click toorun it.</span></span> <span data-ttu-id="25c31-177">Hallo-beheerprogramma's-venster met de rechtermuisknop op Windows PowerShell ISE, klikt u op als Administrator uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="25c31-177">In hello Administrative Tools window, right-click Windows PowerShell ISE, click Run as Administrator.</span></span>

## <a name="how-toomanage-storage-accounts-in-azure"></a><span data-ttu-id="25c31-178">Hoe toomanage opslagaccounts in Azure</span><span class="sxs-lookup"><span data-stu-id="25c31-178">How toomanage storage accounts in Azure</span></span>

<span data-ttu-id="25c31-179">We gaan verdiepen in de storage-accounts in Azure met PowerShell beheren</span><span class="sxs-lookup"><span data-stu-id="25c31-179">Let's take a look at managing storage accounts in Azure with PowerShell</span></span>

### <a name="how-tooset-a-default-azure-subscription"></a><span data-ttu-id="25c31-180">Hoe tooset standaard Azure-abonnement</span><span class="sxs-lookup"><span data-stu-id="25c31-180">How tooset a default Azure subscription</span></span>
<span data-ttu-id="25c31-181">toomanage Azure Storage met Azure PowerShell, moet u tooauthenticate uw clientomgeving met Azure via Azure Active Directory-verificatie of verificatie op basis van certificaten.</span><span class="sxs-lookup"><span data-stu-id="25c31-181">toomanage Azure Storage using Azure PowerShell, you need tooauthenticate your client environment with Azure via Azure Active Directory authentication or certificate-based authentication.</span></span> <span data-ttu-id="25c31-182">Zie voor gedetailleerde informatie [hoe tooinstall en configureren van Azure PowerShell](/powershell/azure/overview) zelfstudie.</span><span class="sxs-lookup"><span data-stu-id="25c31-182">For detailed information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tutorial.</span></span> <span data-ttu-id="25c31-183">Deze handleiding gebruikt hello Azure Active Directory-verificatie.</span><span class="sxs-lookup"><span data-stu-id="25c31-183">This guide uses hello Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="25c31-184">Typ in Windows PowerShell ISE Hallo opdracht tooadd na uw Azure-account toohello lokale PowerShell-omgeving:</span><span class="sxs-lookup"><span data-stu-id="25c31-184">In Windows PowerShell ISE, type hello following command tooadd your Azure account toohello local PowerShell environment:</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="25c31-185">In 'tooMicrosoft Azure aanmelden' Hallo-venster, type Hallo e-mailadres en wachtwoord die zijn gekoppeld aan uw account.</span><span class="sxs-lookup"><span data-stu-id="25c31-185">In hello "Sign in tooMicrosoft Azure" window, type hello email address and password associated with your account.</span></span> <span data-ttu-id="25c31-186">Azure verifieert Hallo referentie-informatie wordt opgeslagen en vervolgens Hallo-venster wordt gesloten.</span><span class="sxs-lookup"><span data-stu-id="25c31-186">Azure authenticates and saves hello credential information, and then closes hello window.</span></span>

3. <span data-ttu-id="25c31-187">Voer vervolgens Hallo na de opdracht tooview hello Azure accounts in uw lokale PowerShell-omgeving en controleer of uw account wordt vermeld:</span><span class="sxs-lookup"><span data-stu-id="25c31-187">Next, run hello following command tooview hello Azure accounts in your local PowerShell environment, and verify that your account is listed:</span></span>
   
    ```powershell
    Get-AzureAccount
    ```
4. <span data-ttu-id="25c31-188">Vervolgens Hallo cmdlet tooview na alle Hallo-abonnementen die verbonden toohello lokale PowerShell-sessie zijn uitvoeren en controleer of uw abonnement wordt vermeld:</span><span class="sxs-lookup"><span data-stu-id="25c31-188">Then, run hello following cmdlet tooview all hello subscriptions that are connected toohello local PowerShell session, and verify that your subscription is listed:</span></span>

    ```powershell
    Get-AzureSubscription | Format-Table SubscriptionName, IsDefault, IsCurrent, CurrentStorageAccountName`
    ```
5. <span data-ttu-id="25c31-189">tooset standaard Azure-abonnement, Hallo Select-AzureSubscription cmdlet uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="25c31-189">tooset a default Azure subscription, run hello Select-AzureSubscription cmdlet:</span></span>

    ```powershell
    $SubscriptionName = 'Your subscription Name'
    Select-AzureSubscription -SubscriptionName $SubscriptionName –Default
    ```

6. <span data-ttu-id="25c31-190">Controleer de naam van de Hallo van Hallo standaardabonnement door Hallo Get-AzureSubscription cmdlet:</span><span class="sxs-lookup"><span data-stu-id="25c31-190">Verify hello name of hello default subscription by running hello Get-AzureSubscription cmdlet:</span></span>

    ```powershell
    Get-AzureSubscription -Default
    ```

7. <span data-ttu-id="25c31-191">toosee uitvoeren voor alle Hallo beschikbare PowerShell-cmdlets voor Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="25c31-191">toosee all hello available PowerShell cmdlets for Azure Storage, run:</span></span>
    
    ```powershell
    Get-Command -Module Azure -Noun *Storage*`
    ```

### <a name="how-toocreate-a-new-azure-storage-account"></a><span data-ttu-id="25c31-192">Hoe toocreate een nieuwe Azure storage-account</span><span class="sxs-lookup"><span data-stu-id="25c31-192">How toocreate a new Azure storage account</span></span>
<span data-ttu-id="25c31-193">toouse Azure-opslag, moet u een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="25c31-193">toouse Azure storage, you will need a storage account.</span></span> <span data-ttu-id="25c31-194">Nadat u uw computer tooconnect tooyour-abonnement hebt geconfigureerd, kunt u een nieuwe Azure storage-account maken.</span><span class="sxs-lookup"><span data-stu-id="25c31-194">You can create a new Azure storage account after you have configured your computer tooconnect tooyour subscription.</span></span>

1. <span data-ttu-id="25c31-195">Hallo Get-AzureLocation cmdlet toofind alle Hallo beschikbaar datacenterlocaties uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="25c31-195">Run hello Get-AzureLocation cmdlet toofind all hello available datacenter locations:</span></span>

    ```powershell
    Get-AzureLocation | Format-Table -Property Name, AvailableServices, StorageAccountTypes
    ```

2. <span data-ttu-id="25c31-196">Voer Hallo nieuw AzureStorageAccount cmdlet toocreate vervolgens een nieuw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="25c31-196">Next, run hello New-AzureStorageAccount cmdlet toocreate a new storage account.</span></span> <span data-ttu-id="25c31-197">Hallo volgende voorbeeld wordt een nieuw opslagaccount in Hallo 'VS-West' datacenter.</span><span class="sxs-lookup"><span data-stu-id="25c31-197">hello following example creates a new storage account in hello "West US" datacenter.</span></span>
   
    ```powershell
    $location = "West US"
    $StorageAccountName = "yourstorageaccount"
    New-AzureStorageAccount –StorageAccountName $StorageAccountName -Location $location
    ```

> [!IMPORTANT]
> <span data-ttu-id="25c31-198">Hallo-naam van uw opslagaccount moet uniek zijn binnen Azure en moet een kleine letter.</span><span class="sxs-lookup"><span data-stu-id="25c31-198">hello name of your storage account must be unique within Azure and must be lowercase.</span></span> <span data-ttu-id="25c31-199">Zie voor naamconventies en beperkingen [over Azure Storage-Accounts](storage-create-storage-account.md) en [Naming en verwijzen naar Containers, Blobs en metagegevens](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span><span class="sxs-lookup"><span data-stu-id="25c31-199">For naming conventions and restrictions, see [About Azure Storage Accounts](storage-create-storage-account.md) and [Naming and Referencing Containers, Blobs, and Metadata](http://msdn.microsoft.com/library/azure/dd135715.aspx).</span></span>
> 
> 

### <a name="how-tooset-a-default-azure-storage-account"></a><span data-ttu-id="25c31-200">Hoe een Azure storage-standaardaccount tooset</span><span class="sxs-lookup"><span data-stu-id="25c31-200">How tooset a default Azure storage account</span></span>
<span data-ttu-id="25c31-201">U kunt meerdere opslagaccounts hebben in uw abonnement.</span><span class="sxs-lookup"><span data-stu-id="25c31-201">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="25c31-202">U kunt kiezen één van beide en zijn ingesteld dat deze zoals Hallo storage-standaardaccount voor alle opslag Hallo-in Hallo dezelfde opdrachten PowerShell-sessie.</span><span class="sxs-lookup"><span data-stu-id="25c31-202">You can choose one of them and set it as hello default storage account for all hello storage commands in hello same PowerShell session.</span></span> <span data-ttu-id="25c31-203">Hiermee kunt u toorun opslag hello Azure PowerShell-opdrachten zonder op te geven Hallo opslag context expliciet.</span><span class="sxs-lookup"><span data-stu-id="25c31-203">This enables you toorun hello Azure PowerShell storage commands without specifying hello storage context explicitly.</span></span>

1. <span data-ttu-id="25c31-204">tooset een standaardopslagaccount voor uw abonnement, kunt u Hallo Set-AzureSubscription cmdlet uitvoeren.</span><span class="sxs-lookup"><span data-stu-id="25c31-204">tooset a default storage account for your subscription, you can run hello Set-AzureSubscription cmdlet.</span></span>

    ```powershell
    $SubscriptionName = "Your subscription name"
    $StorageAccountName = "yourstorageaccount"  
    Set-AzureSubscription -CurrentStorageAccountName $StorageAccountName -SubscriptionName $SubscriptionName
    ```

2. <span data-ttu-id="25c31-205">Voer Get-AzureSubscription Hallo cmdlet tooverify of Hallo storage-account gekoppeld aan uw abonnement standaardaccount is.</span><span class="sxs-lookup"><span data-stu-id="25c31-205">Next, run hello Get-AzureSubscription cmdlet tooverify that hello storage account is associated with your default subscription account.</span></span> <span data-ttu-id="25c31-206">Deze opdracht retourneert de abonnementseigenschappen Hallo op Hallo van de huidige abonnement met inbegrip van de huidige opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="25c31-206">This command returns hello subscription properties on hello current subscription including its current storage account.</span></span>

    ```powershell
    Get-AzureSubscription –Current
    ```

### <a name="how-toolist-all-azure-storage-accounts-in-a-subscription"></a><span data-ttu-id="25c31-207">Hoe toolist alle Azure storage-accounts in een abonnement</span><span class="sxs-lookup"><span data-stu-id="25c31-207">How toolist all Azure storage accounts in a subscription</span></span>
<span data-ttu-id="25c31-208">Elk Azure-abonnement kan up too100 storage-accounts hebben.</span><span class="sxs-lookup"><span data-stu-id="25c31-208">Each Azure subscription can have up too100 storage accounts.</span></span> <span data-ttu-id="25c31-209">Zie voor Hallo meest actuele informatie over limieten, [Azure-abonnement en Service-limieten, quota's en beperkingen](../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="25c31-209">For hello most up-to-date information on limits, see [Azure Subscription and Service Limits, Quotas, and Constraints](../azure-subscription-service-limits.md).</span></span>

<span data-ttu-id="25c31-210">Voer Hallo cmdlet toofind uit Hallo naam en status van de storage-accounts in het huidige abonnement Hallo Hallo te volgen:</span><span class="sxs-lookup"><span data-stu-id="25c31-210">Run hello following cmdlet toofind out hello name and status of hello storage accounts in hello current subscription:</span></span>

```powershell
Get-AzureStorageAccount | Format-Table -Property StorageAccountName, Location, AccountType, StorageAccountStatus
```

### <a name="how-toocreate-an-azure-storage-context"></a><span data-ttu-id="25c31-211">Hoe toocreate de context van een Azure-opslag</span><span class="sxs-lookup"><span data-stu-id="25c31-211">How toocreate an Azure storage context</span></span>
<span data-ttu-id="25c31-212">Azure-opslag-context is een object in PowerShell tooencapsulate Hallo storage-referenties.</span><span class="sxs-lookup"><span data-stu-id="25c31-212">Azure storage context is an object in PowerShell tooencapsulate hello storage credentials.</span></span> <span data-ttu-id="25c31-213">Met een opslag-context tijdens het uitvoeren van een van de volgende cmdlets, kunt u tooauthenticate uw aanvraag zonder op te geven Hallo storage-account en de toegangssleutel expliciet.</span><span class="sxs-lookup"><span data-stu-id="25c31-213">Using a storage context while running any subsequent cmdlet enables you tooauthenticate your request without specifying hello storage account and its access key explicitly.</span></span> <span data-ttu-id="25c31-214">U kunt een context opslag maken op vele manieren, zoals het gebruik van naam en toegangssleutel van storage-account, de shared access signature (SAS)-token, de verbindingsreeks, of anonieme.</span><span class="sxs-lookup"><span data-stu-id="25c31-214">You can create a storage context in many ways, such as using storage account name and access key, shared access signature (SAS) token, connection string, or anonymous.</span></span> <span data-ttu-id="25c31-215">Zie voor meer informatie [nieuw AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span><span class="sxs-lookup"><span data-stu-id="25c31-215">For more information, see [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext).</span></span>  

<span data-ttu-id="25c31-216">Gebruik een van de volgende drie manieren toocreate Hallo een opslag-context:</span><span class="sxs-lookup"><span data-stu-id="25c31-216">Use one of hello following three ways toocreate a storage context:</span></span>

* <span data-ttu-id="25c31-217">Voer Hallo [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet toofind uit Hallo opslag primaire toegangssleutel voor uw Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="25c31-217">Run hello [Get-AzureStorageKey](/powershell/module/azure.storage/get-azurestoragekey) cmdlet toofind out hello primary storage access key for your Azure storage account.</span></span> <span data-ttu-id="25c31-218">Daarna roept Hallo [nieuw AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet toocreate een context opslag:</span><span class="sxs-lookup"><span data-stu-id="25c31-218">Next, call hello [New-AzureStorageContext](/powershell/module/azure.storage/new-azurestoragecontext) cmdlet toocreate a storage context:</span></span>

    ```powershell
    $StorageAccountName = "yourstorageaccount"
    $StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
    $Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
    ```

* <span data-ttu-id="25c31-219">Genereren van een shared access signature-token voor een Azure storage-container en toocreate een opslag-context worden gebruikt:</span><span class="sxs-lookup"><span data-stu-id="25c31-219">Generate a shared access signature token for an Azure storage container and use it toocreate a storage context:</span></span>

    ```powershell
    $sasToken = New-AzureStorageContainerSASToken -Container abc -Permission rl
    $Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -SasToken $sasToken
    ```

    <span data-ttu-id="25c31-220">Zie voor meer informatie [nieuw AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) en [met behulp van Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span><span class="sxs-lookup"><span data-stu-id="25c31-220">For more information, see [New-AzureStorageContainerSASToken](/powershell/module/azure.storage/new-azurestoragecontainersastoken) and [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md).</span></span>

* <span data-ttu-id="25c31-221">In sommige gevallen kunt u toospecify Hallo service-eindpunten bij het maken van een nieuwe opslag-context.</span><span class="sxs-lookup"><span data-stu-id="25c31-221">In some cases, you may want toospecify hello service endpoints when you create a new storage context.</span></span> <span data-ttu-id="25c31-222">Dit kan noodzakelijk zijn wanneer u een aangepaste domeinnaam voor uw opslagaccount hebt geregistreerd met Hallo Blob-service of het gewenste toouse een shared access signature voor toegang tot de opslagbronnen.</span><span class="sxs-lookup"><span data-stu-id="25c31-222">This might be necessary when you have registered a custom domain name for your storage account with hello Blob service or you want toouse a shared access signature for accessing storage resources.</span></span> <span data-ttu-id="25c31-223">Hallo-service-eindpunten in een verbindingsreeks instellen en deze toocreate een nieuwe opslag context gebruiken zoals hieronder wordt weergegeven:</span><span class="sxs-lookup"><span data-stu-id="25c31-223">Set hello service endpoints in a connection string and use it toocreate a new storage context as shown below:</span></span>

    ```powershell
    $ConnectionString = "DefaultEndpointsProtocol=http;BlobEndpoint=<blobEndpoint>;QueueEndpoint=<QueueEndpoint>;TableEndpoint=<TableEndpoint>;AccountName=<AccountName>;AccountKey=<AccountKey>"
    $Ctx = New-AzureStorageContext -ConnectionString $ConnectionString
    ```

<span data-ttu-id="25c31-224">Voor meer informatie over het tooconfigure een verbindingsreeks voor opslag, Zie [configureren van verbindingsreeksen](storage-configure-connection-string.md).</span><span class="sxs-lookup"><span data-stu-id="25c31-224">For more information on how tooconfigure a storage connection string, see [Configuring Connection Strings](storage-configure-connection-string.md).</span></span>

<span data-ttu-id="25c31-225">Nu dat u hebt uw computer instellen en hebt geleerd hoe toomanage-abonnementen en opslagaccounts met Azure PowerShell, Ga toohello volgende sectie toolearn hoe toomanage Azure blobs en blob-momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="25c31-225">Now that you have set up your computer and learned how toomanage subscriptions and storage accounts using Azure PowerShell, go toohello next section toolearn how toomanage Azure blobs and blob snapshots.</span></span>

### <a name="how-tooretrieve-and-regenerate-azure-storage-keys"></a><span data-ttu-id="25c31-226">Hoe Azure-opslag-sleutels tooretrieve en opnieuw genereren</span><span class="sxs-lookup"><span data-stu-id="25c31-226">How tooretrieve and regenerate Azure storage keys</span></span>
<span data-ttu-id="25c31-227">Een Azure Storage-account wordt geleverd met twee sleutels.</span><span class="sxs-lookup"><span data-stu-id="25c31-227">An Azure Storage account comes with two account keys.</span></span> <span data-ttu-id="25c31-228">U kunt uw sleutels Hallo cmdlet tooretrieve te volgen.</span><span class="sxs-lookup"><span data-stu-id="25c31-228">You can use hello following cmdlet tooretrieve your keys.</span></span>

```powershell
Get-AzureStorageKey -StorageAccountName "yourstorageaccount"
```

<span data-ttu-id="25c31-229">Hallo volgende cmdlet tooretrieve een specifieke sleutel gebruiken.</span><span class="sxs-lookup"><span data-stu-id="25c31-229">Use hello following cmdlet tooretrieve a specific key.</span></span> <span data-ttu-id="25c31-230">Geldige waarden zijn primair en secundair.</span><span class="sxs-lookup"><span data-stu-id="25c31-230">Valid values are Primary and Secondary.</span></span>  

```powershell
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Primary
    
(Get-AzureStorageKey -StorageAccountName $StorageAccountName).Secondary
```

<span data-ttu-id="25c31-231">Als u tooregenerate wilt uw sleutels Hallo volgende cmdlet gebruiken.</span><span class="sxs-lookup"><span data-stu-id="25c31-231">If you would like tooregenerate your keys, use hello following cmdlet.</span></span> <span data-ttu-id="25c31-232">Geldige waarden voor KeyType - zijn 'Primaire' en 'Secundaire'</span><span class="sxs-lookup"><span data-stu-id="25c31-232">Valid values for -KeyType are "Primary" and "Secondary"</span></span>

```powershell
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Primary"
    
New-AzureStorageKey -StorageAccountName $StorageAccountName -KeyType "Secondary"
```

## <a name="how-toomanage-azure-blobs"></a><span data-ttu-id="25c31-233">Hoe toomanage Azure blobs</span><span class="sxs-lookup"><span data-stu-id="25c31-233">How toomanage Azure blobs</span></span>
<span data-ttu-id="25c31-234">Azure Blob storage is een service voor het opslaan van grote hoeveelheden ongestructureerde gegevens, zoals tekst of binaire gegevens, die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via HTTP of HTTPS.</span><span class="sxs-lookup"><span data-stu-id="25c31-234">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="25c31-235">Deze sectie wordt ervan uitgegaan dat u al bekend met concepten voor hello Azure Blob Storage-Service bent.</span><span class="sxs-lookup"><span data-stu-id="25c31-235">This section assumes that you are already familiar with hello Azure Blob Storage Service concepts.</span></span> <span data-ttu-id="25c31-236">Zie voor gedetailleerde informatie [aan de slag met Blob storage met .NET](storage-dotnet-how-to-use-blobs.md) en [concepten van Blob-Service](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="25c31-236">For detailed information, see [Get started with Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="how-toocreate-a-container"></a><span data-ttu-id="25c31-237">Hoe toocreate een container</span><span class="sxs-lookup"><span data-stu-id="25c31-237">How toocreate a container</span></span>
<span data-ttu-id="25c31-238">Elke blob in Azure-opslag moet zich in een container.</span><span class="sxs-lookup"><span data-stu-id="25c31-238">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="25c31-239">U kunt een privé-container met de cmdlet New-AzureStorageContainer Hallo maken:</span><span class="sxs-lookup"><span data-stu-id="25c31-239">You can create a private container using hello New-AzureStorageContainer cmdlet:</span></span>

```powershell
$StorageContainerName = "yourcontainername"
New-AzureStorageContainer -Name $StorageContainerName -Permission Off
```

> [!NOTE]
> <span data-ttu-id="25c31-240">Er zijn drie niveaus van anonieme toegang voor lezen: **uit**, **Blob**, en **Container**.</span><span class="sxs-lookup"><span data-stu-id="25c31-240">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="25c31-241">tooprevent anonieme toegang tot tooblobs, setparameter Hallo machtiging te**uit**.</span><span class="sxs-lookup"><span data-stu-id="25c31-241">tooprevent anonymous access tooblobs, set hello Permission parameter too**Off**.</span></span> <span data-ttu-id="25c31-242">Standaard Hallo nieuwe container privé is en toegankelijk zijn alleen voor de accounteigenaar Hallo.</span><span class="sxs-lookup"><span data-stu-id="25c31-242">By default, hello new container is private and can be accessed only by hello account owner.</span></span> <span data-ttu-id="25c31-243">anonieme openbare tooallow lezen toegang tot tooblob bronnen, maar niet toocontainer metagegevens of toohello lijst met blobs in de container hello, stelt u Hallo machtiging parameter te**Blob**.</span><span class="sxs-lookup"><span data-stu-id="25c31-243">tooallow anonymous public read access tooblob resources, but not toocontainer metadata or toohello list of blobs in hello container, set hello Permission parameter too**Blob**.</span></span> <span data-ttu-id="25c31-244">volledige openbare tooallow lezen toegang tot tooblob bronnen, container metagegevens en Hallo lijst met blobs in de container hello, stelt u Hallo machtiging parameter te**Container**.</span><span class="sxs-lookup"><span data-stu-id="25c31-244">tooallow full public read access tooblob resources, container metadata, and hello list of blobs in hello container, set hello Permission parameter too**Container**.</span></span> <span data-ttu-id="25c31-245">Zie voor meer informatie [anonieme leestoegang toocontainers en blobs beheren](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="25c31-245">For more information, see [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md).</span></span>
> 
> 

### <a name="how-tooupload-a-blob-into-a-container"></a><span data-ttu-id="25c31-246">Hoe tooupload een blob naar een container</span><span class="sxs-lookup"><span data-stu-id="25c31-246">How tooupload a blob into a container</span></span>
<span data-ttu-id="25c31-247">Azure Blob Storage ondersteunt blok-blobs en pagina-blobs.</span><span class="sxs-lookup"><span data-stu-id="25c31-247">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="25c31-248">Zie voor meer informatie [blok-Blobs, toevoeg-BLobs en pagina-Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="25c31-248">For more information, see [Understanding Block Blobs, Append BLobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="25c31-249">tooupload blobs in tooa container, kunt u Hallo [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="25c31-249">tooupload blobs in tooa container, you can use hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet.</span></span> <span data-ttu-id="25c31-250">Standaard uploadt u deze opdracht Hallo lokale bestanden tooa blok-blob.</span><span class="sxs-lookup"><span data-stu-id="25c31-250">By default, this command uploads hello local files tooa block blob.</span></span> <span data-ttu-id="25c31-251">Hallo-type toospecify voor Hallo blob, kunt u Hallo BlobType - parameter.</span><span class="sxs-lookup"><span data-stu-id="25c31-251">toospecify hello type for hello blob, you can use hello -BlobType parameter.</span></span>

<span data-ttu-id="25c31-252">Hallo volgende voorbeeld wordt uitgevoerd Hallo [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet tooget alle hello-bestanden in de opgegeven map Hallo en vervolgens geeft deze door de volgende cmdlet toohello met behulp van Hallo pipeline-operator.</span><span class="sxs-lookup"><span data-stu-id="25c31-252">hello following example runs hello [Get-ChildItem](http://technet.microsoft.com/library/hh849800.aspx) cmdlet tooget all hello files in hello specified folder, and then passes them toohello next cmdlet by using hello pipeline operator.</span></span> <span data-ttu-id="25c31-253">Hallo [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet uploadt Hallo lokale bestanden tooyour container:</span><span class="sxs-lookup"><span data-stu-id="25c31-253">hello [Set-AzureStorageBlobContent](/powershell/module/azure.storage/set-azurestorageblobcontent) cmdlet uploads hello local files tooyour container:</span></span>

```powershell
Get-ChildItem –Path C:\Images\* | Set-AzureStorageBlobContent -Container "yourcontainername"
```

### <a name="how-toodownload-blobs-from-a-container"></a><span data-ttu-id="25c31-254">Hoe toodownload blobs uit een container</span><span class="sxs-lookup"><span data-stu-id="25c31-254">How toodownload blobs from a container</span></span>
<span data-ttu-id="25c31-255">Hallo volgende voorbeeld laat zien hoe toodownload blobs uit een container.</span><span class="sxs-lookup"><span data-stu-id="25c31-255">hello following example demonstrates how toodownload blobs from a container.</span></span> <span data-ttu-id="25c31-256">Hallo-voorbeeld wordt eerst een verbinding tooAzure opslag met Hallo storage account context, waaronder Hallo opslagaccountnaam en de primaire toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="25c31-256">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its primary access key.</span></span> <span data-ttu-id="25c31-257">Vervolgens Hallo voorbeeld verwijzing naar een blob met Hallo haalt [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="25c31-257">Then, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet.</span></span> <span data-ttu-id="25c31-258">Vervolgens Hallo voorbeeld maakt gebruik van Hallo [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet toodownload blobs in de lokale doelmap Hallo.</span><span class="sxs-lookup"><span data-stu-id="25c31-258">Next, hello example uses hello [Get-AzureStorageBlobContent](/powershell/module/azure.storage/get-azurestorageblobcontent) cmdlet toodownload blobs into hello local destination folder.</span></span>

```powershell
#Define hello variables.
$ContainerName = "yourcontainername"
$DestinationFolder = "C:\DownloadImages"

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#List all blobs in a container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Download blobs from a container.
New-Item -Path $DestinationFolder -ItemType Directory -Force
$blobs | Get-AzureStorageBlobContent -Destination $DestinationFolder -Context $Ctx
```

### <a name="how-toocopy-blobs-from-one-storage-container-tooanother"></a><span data-ttu-id="25c31-259">Hoe toocopy blobs uit één opslag container tooanother</span><span class="sxs-lookup"><span data-stu-id="25c31-259">How toocopy blobs from one storage container tooanother</span></span>
<span data-ttu-id="25c31-260">U kunt BLOB's tussen opslagaccounts en regio's asynchroon kopiëren.</span><span class="sxs-lookup"><span data-stu-id="25c31-260">You can copy blobs across storage accounts and regions asynchronously.</span></span> <span data-ttu-id="25c31-261">Hallo volgende voorbeeld laat zien hoe toocopy blobs uit één opslag container tooanother in twee verschillende opslagaccounts.</span><span class="sxs-lookup"><span data-stu-id="25c31-261">hello following example demonstrates how toocopy blobs from one storage container tooanother in two different storage accounts.</span></span> <span data-ttu-id="25c31-262">Hallo voorbeeld stelt eerst de variabelen voor de bron- en storage-accounts en maakt vervolgens een context opslag voor elke account.</span><span class="sxs-lookup"><span data-stu-id="25c31-262">hello example first sets variables for source and destination storage accounts, and then creates a storage context for each account.</span></span> <span data-ttu-id="25c31-263">Vervolgens Hallo voorbeeld blobs kopieert van Hallo bron container toohello doelcontainer Hallo met [Start AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="25c31-263">Next, hello example copies blobs from hello source container toohello destination container using hello [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet.</span></span> <span data-ttu-id="25c31-264">Hallo-voorbeeld wordt ervan uitgegaan dat Hallo bron- en storage-accounts en containers bestaan al.</span><span class="sxs-lookup"><span data-stu-id="25c31-264">hello example assumes that hello source and destination storage accounts and containers already exist.</span></span>

```powershell
#Define hello source storage account and context.
$SourceStorageAccountName = "yoursourcestorageaccount"
$SourceStorageAccountKey = "Storage key for yoursourcestorageaccount"
$SrcContainerName = "yoursrccontainername"
$SourceContext = New-AzureStorageContext -StorageAccountName $SourceStorageAccountName -StorageAccountKey $SourceStorageAccountKey

#Define hello destination storage account and context.
$DestStorageAccountName = "yourdeststorageaccount"
$DestStorageAccountKey = "Storage key for yourdeststorageaccount"
$DestContainerName = "destcontainername"
$DestContext = New-AzureStorageContext -StorageAccountName $DestStorageAccountName -StorageAccountKey $DestStorageAccountKey

#Get a reference tooblobs in hello source container.
$blobs = Get-AzureStorageBlob -Container $SrcContainerName -Context $SourceContext

#Copy blobs from one container tooanother.
$blobs| Start-AzureStorageBlobCopy -DestContainer $DestContainerName -DestContext $DestContext
```

<span data-ttu-id="25c31-265">Houd er rekening mee dat dit voorbeeld wordt een kopie van de asynchrone uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="25c31-265">Note that this example performs an asynchronous copy.</span></span> <span data-ttu-id="25c31-266">U kunt Hallo status van elk exemplaar bewaken door het uitvoeren van Hallo [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="25c31-266">You can monitor hello status of each copy by running hello [Get-AzureStorageBlobCopyState](/powershell/module/azure.storage/start-azurestorageblobcopystate) cmdlet.</span></span>

### <a name="how-toocopy-blobs-from-a-secondary-location"></a><span data-ttu-id="25c31-267">Hoe toocopy blobs vanaf een secundaire locatie</span><span class="sxs-lookup"><span data-stu-id="25c31-267">How toocopy blobs from a secondary location</span></span>
<span data-ttu-id="25c31-268">U kunt blobs kopiëren vanaf de secundaire locatie Hallo van een account RA-GRS-functionaliteit.</span><span class="sxs-lookup"><span data-stu-id="25c31-268">You can copy blobs from hello secondary location of a RA-GRS-enabled account.</span></span>

```powershell
#define secondary storage context using a connection string constructed from secondary endpoints.
$SrcContext = New-AzureStorageContext -ConnectionString "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***;BlobEndpoint=http://***-secondary.blob.core.windows.net;FileEndpoint=http://***-secondary.file.core.windows.net;QueueEndpoint=http://***-secondary.queue.core.windows.net; TableEndpoint=http://***-secondary.table.core.windows.net;"
Start-AzureStorageBlobCopy –Container *** -Blob *** -Context $SrcContext –DestContainer *** -DestBlob *** -DestContext $DestContext
```

### <a name="how-toodelete-a-blob"></a><span data-ttu-id="25c31-269">Hoe toodelete een blob</span><span class="sxs-lookup"><span data-stu-id="25c31-269">How toodelete a blob</span></span>
<span data-ttu-id="25c31-270">een blob toodelete eerst een blobverwijzing ophalen en roept u vervolgens Hallo verwijderen AzureStorageBlob cmdlet erop.</span><span class="sxs-lookup"><span data-stu-id="25c31-270">toodelete a blob, first get a blob reference and then call hello Remove-AzureStorageBlob cmdlet on it.</span></span> <span data-ttu-id="25c31-271">Hallo volgende voorbeeld worden alle Hallo blobs in een bepaalde container verwijderd.</span><span class="sxs-lookup"><span data-stu-id="25c31-271">hello following example deletes all hello blobs in a given container.</span></span> <span data-ttu-id="25c31-272">Hallo voorbeeld stelt eerst de variabelen voor een opslagaccount en maakt vervolgens een opslag-context.</span><span class="sxs-lookup"><span data-stu-id="25c31-272">hello example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="25c31-273">Vervolgens Hallo voorbeeld verwijzing naar een blob met Hallo haalt [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet en wordt uitgevoerd Hallo [verwijderen AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet tooremove blobs uit een container in Azure-opslag.</span><span class="sxs-lookup"><span data-stu-id="25c31-273">Next, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [Remove-AzureStorageBlob](/powershell/module/azure.storage/remove-azurestorageblob) cmdlet tooremove blobs from a container in Azure storage.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "containername"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooall hello blobs in hello container.
$blobs = Get-AzureStorageBlob -Container $ContainerName -Context $Ctx

#Delete blobs in a specified container.
$blobs| Remove-AzureStorageBlob
```

## <a name="how-toomanage-azure-blob-snapshots"></a><span data-ttu-id="25c31-274">Hoe toomanage Azure blob-momentopnamen</span><span class="sxs-lookup"><span data-stu-id="25c31-274">How toomanage Azure blob snapshots</span></span>
<span data-ttu-id="25c31-275">Azure maakt u een momentopname van een blob.</span><span class="sxs-lookup"><span data-stu-id="25c31-275">Azure lets you create a snapshot of a blob.</span></span> <span data-ttu-id="25c31-276">Een momentopname is een alleen-lezen-versie van een blob die wordt uitgevoerd op een punt in tijd.</span><span class="sxs-lookup"><span data-stu-id="25c31-276">A snapshot is a read-only version of a blob that's taken at a point in time.</span></span> <span data-ttu-id="25c31-277">Wanneer een momentopname is gemaakt, kan deze worden gelezen, gekopieerd, of verwijderd, maar niet gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="25c31-277">Once a snapshot has been created, it can be read, copied, or deleted, but not modified.</span></span> <span data-ttu-id="25c31-278">Momentopnamen bieden een manier tooback van een blob, zoals deze wordt weergegeven op een moment.</span><span class="sxs-lookup"><span data-stu-id="25c31-278">Snapshots provide a way tooback up a blob as it appears at a moment in time.</span></span> <span data-ttu-id="25c31-279">Zie voor meer informatie [maken van een momentopname van een Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="25c31-279">For more information, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span>

### <a name="how-toocreate-a-blob-snapshot"></a><span data-ttu-id="25c31-280">Hoe toocreate een momentopname van een blob</span><span class="sxs-lookup"><span data-stu-id="25c31-280">How toocreate a blob snapshot</span></span>
<span data-ttu-id="25c31-281">een snaphot van een blob toocreate eerst een blobverwijzing ophalen en vervolgens aanroepen Hallo `ICloudBlob.CreateSnapshot` methode erop.</span><span class="sxs-lookup"><span data-stu-id="25c31-281">toocreate a snaphot of a blob, first get a blob reference and then call hello `ICloudBlob.CreateSnapshot` method on it.</span></span> <span data-ttu-id="25c31-282">Hallo volgende voorbeeld stelt eerst de variabelen voor een opslagaccount, en maakt vervolgens een opslag-context.</span><span class="sxs-lookup"><span data-stu-id="25c31-282">hello following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="25c31-283">Vervolgens Hallo voorbeeld verwijzing naar een blob met Hallo haalt [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet en wordt uitgevoerd Hallo [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) methode toocreate een momentopname.</span><span class="sxs-lookup"><span data-stu-id="25c31-283">Next, hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method toocreate a snapshot.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$ContainerName = "yourcontainername"
$BlobName = "yourblobname"
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $ContainerName -Blob $BlobName

#Create a snapshot of hello blob.
$snap = $blob.ICloudBlob.CreateSnapshot()
```

### <a name="how-toolist-a-blobs-snapshots"></a><span data-ttu-id="25c31-284">Hoe toolist een blob van momentopnamen</span><span class="sxs-lookup"><span data-stu-id="25c31-284">How toolist a blob's snapshots</span></span>
<span data-ttu-id="25c31-285">U kunt zoveel momentopnamen als u voor een blob wilt maken.</span><span class="sxs-lookup"><span data-stu-id="25c31-285">You can create as many snapshots as you want for a blob.</span></span> <span data-ttu-id="25c31-286">Je kunt aanbieden Hallo momentopnamen die zijn gekoppeld aan uw tootrack blob uw huidige momentopnamen.</span><span class="sxs-lookup"><span data-stu-id="25c31-286">You can list hello snapshots associated with your blob tootrack your current snapshots.</span></span> <span data-ttu-id="25c31-287">Hallo volgende voorbeeld wordt een vooraf gedefinieerde blob en aanroepen Hallo [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet toolist Hallo momentopnamen van de blob.</span><span class="sxs-lookup"><span data-stu-id="25c31-287">hello following example uses a predefined blob and calls hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet toolist hello snapshots of that blob.</span></span>  

```powershell
#Define hello blob name.
$BlobName = "yourblobname"

#List hello snapshots of a blob.
Get-AzureStorageBlob –Context $Ctx -Prefix $BlobName -Container $ContainerName  | Where-Object  { $_.ICloudBlob.IsSnapshot -and $_.Name -eq $BlobName }
```

### <a name="how-toocopy-a-snapshot-of-a-blob"></a><span data-ttu-id="25c31-288">Hoe toocopy een momentopname van een blob</span><span class="sxs-lookup"><span data-stu-id="25c31-288">How toocopy a snapshot of a blob</span></span>
<span data-ttu-id="25c31-289">U kunt een momentopname van een momentopname van een blob toorestore Hallo kopiëren.</span><span class="sxs-lookup"><span data-stu-id="25c31-289">You can copy a snapshot of a blob toorestore hello snapshot.</span></span> <span data-ttu-id="25c31-290">Zie voor gedetailleerde informatie en beperkingen [maken van een momentopname van een Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span><span class="sxs-lookup"><span data-stu-id="25c31-290">For detailed information and restrictions, see [Creating a Snapshot of a Blob](http://msdn.microsoft.com/library/azure/hh488361.aspx).</span></span> <span data-ttu-id="25c31-291">Hallo volgende voorbeeld stelt eerst de variabelen voor een opslagaccount, en maakt vervolgens een opslag-context.</span><span class="sxs-lookup"><span data-stu-id="25c31-291">hello following example first sets variables for a storage account, and then creates a storage context.</span></span> <span data-ttu-id="25c31-292">Vervolgens definieert Hallo voorbeeld Hallo-container en blob naam variabelen.</span><span class="sxs-lookup"><span data-stu-id="25c31-292">Next, hello example defines hello container and blob name variables.</span></span> <span data-ttu-id="25c31-293">Hallo-voorbeeld wordt een blobverwijzing met Hallo opgehaald [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet en wordt uitgevoerd Hallo [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) methode toocreate een momentopname.</span><span class="sxs-lookup"><span data-stu-id="25c31-293">hello example retrieves a blob reference using hello [Get-AzureStorageBlob](/powershell/module/azure.storage/get-azurestorageblob) cmdlet and runs hello [ICloudBlob.CreateSnapshot](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.blob.icloudblob.aspx) method toocreate a snapshot.</span></span> <span data-ttu-id="25c31-294">Vervolgens Hallo-voorbeeld Hallo uitgevoerd [Start AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet toocopy Hallo momentopname van een blob Hallo ICloudBlob-object voor de bron-blob hello gebruiken.</span><span class="sxs-lookup"><span data-stu-id="25c31-294">Then, hello example runs hello [Start-AzureStorageBlobCopy](/powershell/module/azure.storage/start-azurestorageblobcopy) cmdlet toocopy hello snapshot of a blob using hello ICloudBlob object for hello source blob.</span></span> <span data-ttu-id="25c31-295">Controleer of tooupdate Hallo variabelen gebaseerd zijn op uw configuratie voordat actieve Hallo-voorbeeld.</span><span class="sxs-lookup"><span data-stu-id="25c31-295">Be sure tooupdate hello variables based on your configuration before running hello example.</span></span> <span data-ttu-id="25c31-296">Houd er rekening mee dat Hallo volgende voorbeeld wordt ervan uitgegaan dat Hallo bron- en doelserver containers en Hallo bron blob bestaat al.</span><span class="sxs-lookup"><span data-stu-id="25c31-296">Note that hello following example assumes that hello source and destination containers, and hello source blob already exist.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext -StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey

#Define hello variables.
$SrcContainerName = "yoursourcecontainername"
$DestContainerName = "yourdestcontainername"
$SrcBlobName = "yourblobname"
$DestBlobName = "CopyBlobName"

#Get a reference tooa blob.
$blob = Get-AzureStorageBlob -Context $Ctx -Container $SrcContainerName -Blob $SrcBlobName

#Create a snapshot of a blob.
$snap = $blob.ICloudBlob.CreateSnapshot()

#Copy hello snapshot tooanother container.
Start-AzureStorageBlobCopy –Context $Ctx -ICloudBlob $snap -DestBlob $DestBlobName -DestContainer $DestContainerName
```

<span data-ttu-id="25c31-297">Nu dat u hebt geleerd hoe toomanage Azure blobs en blob-momentopnamen met Azure PowerShell, gaat u toohello volgende sectie toolearn hoe toomanage tabellen, wachtrijen en bestanden.</span><span class="sxs-lookup"><span data-stu-id="25c31-297">Now that you have learned how toomanage Azure blobs and blob snapshots with Azure PowerShell, go toohello next section toolearn how toomanage tables, queues, and files.</span></span>

## <a name="how-toomanage-azure-tables-and-table-entities"></a><span data-ttu-id="25c31-298">Hoe toomanage Azure-tabellen en entiteiten tabel</span><span class="sxs-lookup"><span data-stu-id="25c31-298">How toomanage Azure tables and table entities</span></span>
<span data-ttu-id="25c31-299">Azure Table storage-service is een NoSQL-gegevensarchief kunt u toostore en query grote sets gestructureerde, niet-relationele gegevens.</span><span class="sxs-lookup"><span data-stu-id="25c31-299">Azure Table storage service is a NoSQL datastore, which you can use toostore and query huge sets of structured, non-relational data.</span></span> <span data-ttu-id="25c31-300">Hallo hoofdonderdelen van Hallo service zijn tabellen, entiteiten en eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="25c31-300">hello main components of hello service are tables, entities, and properties.</span></span> <span data-ttu-id="25c31-301">Een tabel is een verzameling entiteiten.</span><span class="sxs-lookup"><span data-stu-id="25c31-301">A table is a collection of entities.</span></span> <span data-ttu-id="25c31-302">Een entiteit is een set eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="25c31-302">An entity is a set of properties.</span></span> <span data-ttu-id="25c31-303">Elke entiteit kan hebben too252-eigenschappen die alle naam / waarde-paren.</span><span class="sxs-lookup"><span data-stu-id="25c31-303">Each entity can have up too252 properties, which are all name-value pairs.</span></span> <span data-ttu-id="25c31-304">Deze sectie wordt ervan uitgegaan dat u al bekend met concepten voor hello Azure Table Storage-Service bent.</span><span class="sxs-lookup"><span data-stu-id="25c31-304">This section assumes that you are already familiar with hello Azure Table Storage Service concepts.</span></span> <span data-ttu-id="25c31-305">Zie voor gedetailleerde informatie [Understanding Hallo Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) en [aan de slag met Azure Table storage met .NET](storage-dotnet-how-to-use-tables.md).</span><span class="sxs-lookup"><span data-stu-id="25c31-305">For detailed information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx) and [Get started with Azure Table storage using .NET](storage-dotnet-how-to-use-tables.md).</span></span>

<span data-ttu-id="25c31-306">In de Hallo volgende subsecties, leert u hoe toomanage Azure Table storage-service met Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="25c31-306">In hello following subsections, you'll learn how toomanage Azure Table storage service using Azure PowerShell.</span></span> <span data-ttu-id="25c31-307">Hallo scenario's worden behandeld: **maken**, **verwijderen**, en **bij het ophalen van** **tabellen**, evenals **toevoegen**, **opvragen**, en **tabelentiteiten verwijderen**.</span><span class="sxs-lookup"><span data-stu-id="25c31-307">hello scenarios covered include **creating**, **deleting**, and **retrieving** **tables**, as well as **adding**, **querying**, and **deleting table entities**.</span></span>

### <a name="how-toocreate-a-table"></a><span data-ttu-id="25c31-308">Hoe toocreate een tabel</span><span class="sxs-lookup"><span data-stu-id="25c31-308">How toocreate a table</span></span>
<span data-ttu-id="25c31-309">Elke tabel moet zich bevinden in een Azure storage-account.</span><span class="sxs-lookup"><span data-stu-id="25c31-309">Every table must reside in an Azure storage account.</span></span> <span data-ttu-id="25c31-310">Hallo volgende voorbeeld laat zien hoe toocreate een tabel in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="25c31-310">hello following example demonstrates how toocreate a table in Azure Storage.</span></span> <span data-ttu-id="25c31-311">Hallo-voorbeeld wordt eerst een verbinding tooAzure opslag met Hallo storage account context, waaronder Hallo opslagaccountnaam en de toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="25c31-311">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="25c31-312">Vervolgens wordt Hallo [nieuw AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet toocreate een tabel in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="25c31-312">Next, it uses hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet toocreate a table in Azure Storage.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = "Storage key for yourstorageaccount ends with =="
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey

#Create a new table.
$tabName = "yourtablename"
New-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-tooretrieve-a-table"></a><span data-ttu-id="25c31-313">Hoe tooretrieve een tabel</span><span class="sxs-lookup"><span data-stu-id="25c31-313">How tooretrieve a table</span></span>
<span data-ttu-id="25c31-314">U kunt een query en ophalen van een of alle tabellen in een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="25c31-314">You can query and retrieve one or all tables in a Storage account.</span></span> <span data-ttu-id="25c31-315">Hallo volgende voorbeeld laat zien hoe een tabel met tooretrieve Hallo [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="25c31-315">hello following example demonstrates how tooretrieve a given table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span>

```powershell
#Retrieve a table.
$tabName = "yourtablename"
Get-AzureStorageTable –Name $tabName –Context $Ctx
```

<span data-ttu-id="25c31-316">Als u Hallo Get AzureStorageTable cmdlet zonder parameters aanroept, krijgt alle opslagtabellen voor een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="25c31-316">If you call hello Get-AzureStorageTable cmdlet without any parameters, it gets all storage tables for a Storage account.</span></span>

### <a name="how-toodelete-a-table"></a><span data-ttu-id="25c31-317">Hoe toodelete een tabel</span><span class="sxs-lookup"><span data-stu-id="25c31-317">How toodelete a table</span></span>
<span data-ttu-id="25c31-318">U kunt een tabel uit een opslagaccount verwijderen met behulp van Hallo [verwijderen AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="25c31-318">You can delete a table from a storage account by using hello [Remove-AzureStorageTable](/powershell/module/azure.storage/remove-azurestoragetable) cmdlet.</span></span>  

```powershell
#Delete a table.
$tabName = "yourtablename"
Remove-AzureStorageTable –Name $tabName –Context $Ctx
```

### <a name="how-toomanage-table-entities"></a><span data-ttu-id="25c31-319">Hoe toomanage tabel entiteiten</span><span class="sxs-lookup"><span data-stu-id="25c31-319">How toomanage table entities</span></span>
<span data-ttu-id="25c31-320">Op dit moment biedt Azure PowerShell geen tabelentiteiten voor cmdlets toomanage rechtstreeks.</span><span class="sxs-lookup"><span data-stu-id="25c31-320">Currently, Azure PowerShell does not provide cmdlets toomanage table entities directly.</span></span> <span data-ttu-id="25c31-321">tooperform bewerkingen op tabelentiteiten, kunt u Hallo klassen die in het Hallo [Azure Storage-clientbibliotheek voor .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span><span class="sxs-lookup"><span data-stu-id="25c31-321">tooperform operations on table entities, you can use hello classes given in hello [Azure Storage Client Library for .NET](http://msdn.microsoft.com/library/azure/wa_storage_30_reference_home.aspx).</span></span>

#### <a name="how-tooadd-table-entities"></a><span data-ttu-id="25c31-322">Hoe tooadd tabel entiteiten</span><span class="sxs-lookup"><span data-stu-id="25c31-322">How tooadd table entities</span></span>
<span data-ttu-id="25c31-323">een tabel entity tooa tooadd eerst een object dat bepaalt de entiteitseigenschappen van uw maken.</span><span class="sxs-lookup"><span data-stu-id="25c31-323">tooadd an entity tooa table, first create an object that defines your entity properties.</span></span> <span data-ttu-id="25c31-324">Een entiteit kan hebben too255 eigenschappen, met inbegrip van de eigenschappen van 3: **PartitionKey**, **RowKey**, en **tijdstempel**.</span><span class="sxs-lookup"><span data-stu-id="25c31-324">An entity can have up too255 properties, including 3 system properties: **PartitionKey**, **RowKey**, and **Timestamp**.</span></span> <span data-ttu-id="25c31-325">U bent zelf verantwoordelijk voor het invoegen en het bijwerken van Hallo waarden van **PartitionKey** en **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="25c31-325">You are responsible for inserting and updating hello values of **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="25c31-326">Hallo server wordt beheerd Hallo-waarde van **tijdstempel**, die niet worden gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="25c31-326">hello server manages hello value of **Timestamp**, which cannot be modified.</span></span> <span data-ttu-id="25c31-327">Samen Hallo **PartitionKey** en **RowKey** unieke identificatie van elke entiteit in een tabel.</span><span class="sxs-lookup"><span data-stu-id="25c31-327">Together hello **PartitionKey** and **RowKey** uniquely identify every entity within a table.</span></span>

* <span data-ttu-id="25c31-328">**PartitionKey**: Hallo partitie die de entiteit Hallo is opgeslagen in bepaalt.</span><span class="sxs-lookup"><span data-stu-id="25c31-328">**PartitionKey**: Determines hello partition that hello entity is stored in.</span></span>
* <span data-ttu-id="25c31-329">**RowKey**: Hallo entiteit binnen Hallo partitie wordt aangeduid.</span><span class="sxs-lookup"><span data-stu-id="25c31-329">**RowKey**: Uniquely identifies hello entity within hello partition.</span></span>

<span data-ttu-id="25c31-330">U kunt definiëren too252 aangepaste eigenschappen voor een entiteit.</span><span class="sxs-lookup"><span data-stu-id="25c31-330">You may define up too252 custom properties for an entity.</span></span> <span data-ttu-id="25c31-331">Zie voor meer informatie [Understanding Hallo Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="25c31-331">For more information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="25c31-332">Hallo volgende voorbeeld laat zien hoe tooadd entiteiten tooa tabel.</span><span class="sxs-lookup"><span data-stu-id="25c31-332">hello following example demonstrates how tooadd entities tooa table.</span></span> <span data-ttu-id="25c31-333">Hallo-voorbeeld ziet u hoe tooretrieve Hallo werknemerstabel en verschillende entiteiten in de App toevoegen.</span><span class="sxs-lookup"><span data-stu-id="25c31-333">hello example shows how tooretrieve hello employee table and add several entities into it.</span></span> <span data-ttu-id="25c31-334">Eerst het vaststelt dat een verbinding tooAzure opslag met Hallo storage account context, waaronder Hallo opslagaccountnaam en de toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="25c31-334">First, it establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="25c31-335">Vervolgens wordt het ophalen van Hallo gegeven van de tabel met behulp van Hallo [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="25c31-335">Next, it retrieves hello given table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="25c31-336">Als Hallo tabel niet bestaat, Hallo [nieuw AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet is gebruikte toocreate een tabel in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="25c31-336">If hello table does not exist, hello [New-AzureStorageTable](/powershell/module/azure.storage/new-azurestoragetable) cmdlet is used toocreate a table in Azure Storage.</span></span> <span data-ttu-id="25c31-337">Hallo voorbeeld wordt vervolgens een aangepaste functie toevoegen entiteit tooadd entiteiten toohello tabel gedefinieerd door partitie voor elke entiteit en rijsleutel te geven.</span><span class="sxs-lookup"><span data-stu-id="25c31-337">Next, hello example defines a custom function Add-Entity tooadd entities toohello table by specifying each entity's partition and row key.</span></span> <span data-ttu-id="25c31-338">Hallo toevoegen entiteit functie aanroepen Hallo [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet op Hallo [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) klasse toocreate een entiteitsobject.</span><span class="sxs-lookup"><span data-stu-id="25c31-338">hello Add-Entity function calls hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on hello [Microsoft.WindowsAzure.Storage.Table.DynamicTableEntity](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.dynamictableentity.aspx) class toocreate an entity object.</span></span> <span data-ttu-id="25c31-339">Later Hallo voorbeeld Hallo roept [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) methode voor deze entiteit object tooadd het tooa tabel.</span><span class="sxs-lookup"><span data-stu-id="25c31-339">Later, hello example calls hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Insert](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.insert.aspx) method on this entity object tooadd it tooa table.</span></span>

```powershell
#Function Add-Entity: Adds an employee entity tooa table.
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

#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Retrieve hello table if it already exists.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx -ErrorAction Ignore

#Create a new table if it does not exist.
if ($table -eq $null)
{
   $table = New-AzureStorageTable –Name $TableName -Context $Ctx
}

#Add multiple entities tooa table.
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row1 -Name Chris -Id 1
Add-Entity -Table $table -PartitionKey Partition1 -RowKey Row2 -Name Jessie -Id 2
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row1 -Name Christine -Id 3
Add-Entity -Table $table -PartitionKey Partition2 -RowKey Row2 -Name Steven -Id 4
```

#### <a name="how-tooquery-table-entities"></a><span data-ttu-id="25c31-340">Hoe tooquery tabel entiteiten</span><span class="sxs-lookup"><span data-stu-id="25c31-340">How tooquery table entities</span></span>
<span data-ttu-id="25c31-341">een tabel tooquery gebruiken Hallo [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) klasse.</span><span class="sxs-lookup"><span data-stu-id="25c31-341">tooquery a table, use hello [Microsoft.WindowsAzure.Storage.Table.TableQuery](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tablequery.aspx) class.</span></span> <span data-ttu-id="25c31-342">Hallo volgende voorbeeld wordt ervan uitgegaan dat u al hoe gegeven in Hallo Hallo-script hebt uitgevoerd tooadd entiteiten gedeelte van deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="25c31-342">hello following example assumes that you've already run hello script given in hello How tooadd entities section of this guide.</span></span> <span data-ttu-id="25c31-343">Hallo-voorbeeld wordt eerst een verbinding tooAzure opslag met Hallo opslag context, waaronder Hallo opslagaccountnaam en de toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="25c31-343">hello example first establishes a connection tooAzure Storage using hello storage context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="25c31-344">Vervolgens probeert tooretrieve Hallo eerder hebt gemaakt 'werknemers' tabel met behulp van Hallo [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="25c31-344">Next, it tries tooretrieve hello previously created "Employees" table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="25c31-345">Aanroepen Hallo [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet op Hallo Microsoft.WindowsAzure.Storage.Table.TableQuery klasse maakt een nieuwe query-object.</span><span class="sxs-lookup"><span data-stu-id="25c31-345">Calling hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet on hello Microsoft.WindowsAzure.Storage.Table.TableQuery class creates a new query object.</span></span> <span data-ttu-id="25c31-346">Hallo voorbeeld gezocht Hallo entiteiten met een 'ID-kolom waarvan de waarde 1 zoals opgegeven in een tekenreeks-filter is.</span><span class="sxs-lookup"><span data-stu-id="25c31-346">hello example looks for hello entities that have an 'ID' column whose value is 1 as specified in a string filter.</span></span> <span data-ttu-id="25c31-347">Zie voor gedetailleerde informatie [opvragen van tabellen en entiteiten](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span><span class="sxs-lookup"><span data-stu-id="25c31-347">For detailed information, see [Querying Tables and Entities](http://msdn.microsoft.com/library/azure/dd894031.aspx).</span></span> <span data-ttu-id="25c31-348">Wanneer u deze query uitvoert, wordt alle entiteiten die overeenkomen met de filtercriteria Hallo.</span><span class="sxs-lookup"><span data-stu-id="25c31-348">When you run this query, it returns all entities that match hello filter criteria.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$TableName = "Employees"

#Get a reference tooa table.
$table = Get-AzureStorageTable –Name $TableName -Context $Ctx

#Create a table query.
$query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery

#Define columns tooselect.
$list = New-Object System.Collections.Generic.List[string]
$list.Add("RowKey")
$list.Add("ID")
$list.Add("Name")

#Set query details.
$query.FilterString = "ID gt 0"
$query.SelectColumns = $list
$query.TakeCount = 20

#Execute hello query.
$entities = $table.CloudTable.ExecuteQuery($query)

#Display entity properties with hello table format.
$entities  | Format-Table PartitionKey, RowKey, @{ Label = "Name"; Expression={$_.Properties["Name"].StringValue}}, @{ Label = "ID"; Expression={$_.Properties["ID"].Int32Value}} -AutoSize
```

#### <a name="how-toodelete-table-entities"></a><span data-ttu-id="25c31-349">Hoe toodelete tabel entiteiten</span><span class="sxs-lookup"><span data-stu-id="25c31-349">How toodelete table entities</span></span>
<span data-ttu-id="25c31-350">U kunt een entiteit met behulp van de sleutels van de partitie en rij verwijderen.</span><span class="sxs-lookup"><span data-stu-id="25c31-350">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="25c31-351">Hallo volgende voorbeeld wordt ervan uitgegaan dat u al hoe gegeven in Hallo Hallo-script hebt uitgevoerd tooadd entiteiten gedeelte van deze handleiding.</span><span class="sxs-lookup"><span data-stu-id="25c31-351">hello following example assumes that you've already run hello script given in hello How tooadd entities section of this guide.</span></span> <span data-ttu-id="25c31-352">Hallo-voorbeeld wordt eerst een verbinding tooAzure opslag met Hallo opslag context, waaronder Hallo opslagaccountnaam en de toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="25c31-352">hello example first establishes a connection tooAzure Storage using hello storage context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="25c31-353">Vervolgens probeert tooretrieve Hallo eerder hebt gemaakt 'werknemers' tabel met behulp van Hallo [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="25c31-353">Next, it tries tooretrieve hello previously created "Employees" table using hello [Get-AzureStorageTable](/powershell/module/azure.storage/get-azurestoragetable) cmdlet.</span></span> <span data-ttu-id="25c31-354">Als Hallo tabel bestaat, Hallo voorbeeld Hallo roept [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) methode tooretrieve een entiteit op basis van de bijbehorende sleutelwaarden partitie en rij.</span><span class="sxs-lookup"><span data-stu-id="25c31-354">If hello table exists, hello example calls hello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Retrieve](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.retrieve.aspx) method tooretrieve an entity based on its partition and row key values.</span></span> <span data-ttu-id="25c31-355">Vervolgens moet worden doorgegeven Hallo entiteit toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) toodelete methode.</span><span class="sxs-lookup"><span data-stu-id="25c31-355">Then, pass hello entity toohello [Microsoft.WindowsAzure.Storage.Table.TableOperation.Delete](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.table.tableoperation.delete.aspx) method toodelete.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello table.
$TableName = "Employees"
$table = Get-AzureStorageTable -Name $TableName -Context $Ctx -ErrorAction Ignore

#If hello table exists, start deleting its entities.
if ($table -ne $null) 
{
    #Together hello PartitionKey and RowKey uniquely identify every  
    #entity within a table.
    $tableResult = $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Retrieve("Partition2", "Row1"))
    $entity = $tableResult.Result
    if ($entity -ne $null)
    {
        #Delete hello entity.
        $table.CloudTable.Execute([Microsoft.WindowsAzure.Storage.Table.TableOperation]::Delete($entity))
    }
}
```

## <a name="how-toomanage-azure-queues-and-queue-messages"></a><span data-ttu-id="25c31-356">Hoe toomanage Azure wachtrijen en berichten in een wachtrij</span><span class="sxs-lookup"><span data-stu-id="25c31-356">How toomanage Azure queues and queue messages</span></span>
<span data-ttu-id="25c31-357">Azure Queue storage is een service voor het opslaan van grote aantallen berichten die toegankelijk zijn vanaf een willekeurige plaats in Hallo wereld via geverifieerde aanroepen via HTTP of HTTPS.</span><span class="sxs-lookup"><span data-stu-id="25c31-357">Azure Queue storage is a service for storing large numbers of messages that can be accessed from anywhere in hello world via authenticated calls using HTTP or HTTPS.</span></span> <span data-ttu-id="25c31-358">Deze sectie wordt ervan uitgegaan dat u al bekend met concepten voor hello Azure Queue Storage-Service bent.</span><span class="sxs-lookup"><span data-stu-id="25c31-358">This section assumes that you are already familiar with hello Azure Queue Storage Service concepts.</span></span> <span data-ttu-id="25c31-359">Zie voor gedetailleerde informatie [aan de slag met Azure Queue storage met .NET](storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="25c31-359">For detailed information, see [Get started with Azure Queue storage using .NET](storage-dotnet-how-to-use-queues.md).</span></span>

<span data-ttu-id="25c31-360">Deze sectie wordt uitgelegd hoe toomanage Azure Queue storage-service met Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="25c31-360">This section will show you how toomanage Azure Queue storage service using Azure PowerShell.</span></span> <span data-ttu-id="25c31-361">Hallo scenario's worden behandeld: **invoegen** en **verwijderen** wachtrij berichten, evenals **maken**, **verwijderen**, en **bij het ophalen van wachtrijen**.</span><span class="sxs-lookup"><span data-stu-id="25c31-361">hello scenarios covered include **inserting** and **deleting** queue messages, as well as **creating**, **deleting**, and **retrieving queues**.</span></span>

### <a name="how-toocreate-a-queue"></a><span data-ttu-id="25c31-362">Hoe een wachtrij toocreate</span><span class="sxs-lookup"><span data-stu-id="25c31-362">How toocreate a queue</span></span>
<span data-ttu-id="25c31-363">Hallo volgende voorbeeld eerst wordt een verbinding tooAzure opslag met Hallo storage account context, waaronder Hallo opslagaccountnaam en de toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="25c31-363">hello following example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="25c31-364">Vervolgens roept [nieuw AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet toocreate een wachtrij met de naam 'wachtrijnaam'.</span><span class="sxs-lookup"><span data-stu-id="25c31-364">Next, it calls [New-AzureStorageQueue](/powershell/module/azure.storage/new-azurestoragequeue) cmdlet toocreate a queue named 'queuename'.</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary
$QueueName = "queuename"
$Queue = New-AzureStorageQueue –Name $QueueName -Context $Ctx
```

<span data-ttu-id="25c31-365">Zie voor informatie over naamgevingsregels voor Azure Queue-Service, [naamgeving van wachtrijen en metagegevens](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span><span class="sxs-lookup"><span data-stu-id="25c31-365">For information on naming conventions for Azure Queue Service, see [Naming Queues and Metadata](http://msdn.microsoft.com/library/azure/dd179349.aspx).</span></span>

### <a name="how-tooretrieve-a-queue"></a><span data-ttu-id="25c31-366">Hoe een wachtrij tooretrieve</span><span class="sxs-lookup"><span data-stu-id="25c31-366">How tooretrieve a queue</span></span>
<span data-ttu-id="25c31-367">U kunt een query en ophalen van een specifieke wachtrij of een lijst met alle Hallo wachtrijen in een opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="25c31-367">You can query and retrieve a specific queue or a list of all hello queues in a Storage account.</span></span> <span data-ttu-id="25c31-368">Hallo volgende voorbeeld laat zien hoe een opgegeven wachtrij met tooretrieve Hallo [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="25c31-368">hello following example demonstrates how tooretrieve a specified queue using hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet.</span></span>

```powershell
#Retrieve a queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue –Name $QueueName –Context $Ctx
```

<span data-ttu-id="25c31-369">Als u Hallo aanroepen [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet zonder parameters voor het ophalen van een lijst met alle Hallo wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="25c31-369">If you call hello [Get-AzureStorageQueue](/powershell/module/azure.storage/get-azurestoragequeue) cmdlet without any parameters, it gets a list of all hello queues.</span></span>

### <a name="how-toodelete-a-queue"></a><span data-ttu-id="25c31-370">Hoe een wachtrij toodelete</span><span class="sxs-lookup"><span data-stu-id="25c31-370">How toodelete a queue</span></span>
<span data-ttu-id="25c31-371">toodelete een wachtrij en alle Hallo-berichten opgenomen in deze aanroep Hallo verwijderen AzureStorageQueue cmdlet.</span><span class="sxs-lookup"><span data-stu-id="25c31-371">toodelete a queue and all hello messages contained in it, call hello Remove-AzureStorageQueue cmdlet.</span></span> <span data-ttu-id="25c31-372">Hallo volgende voorbeeld ziet u hoe toodelete een opgegeven wachtrij met de cmdlet Remove-AzureStorageQueue Hallo.</span><span class="sxs-lookup"><span data-stu-id="25c31-372">hello following example shows how toodelete a specified queue using hello Remove-AzureStorageQueue cmdlet.</span></span>

```powershell
#Delete a queue.
$QueueName = "yourqueuename"
Remove-AzureStorageQueue –Name $QueueName –Context $Ctx
```

#### <a name="how-tooinsert-a-message-into-a-queue"></a><span data-ttu-id="25c31-373">Hoe tooinsert een bericht in een wachtrij</span><span class="sxs-lookup"><span data-stu-id="25c31-373">How tooinsert a message into a queue</span></span>
<span data-ttu-id="25c31-374">tooinsert een bericht in een bestaande wachtrij maakt eerst een nieuw exemplaar van Hallo [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) klasse.</span><span class="sxs-lookup"><span data-stu-id="25c31-374">tooinsert a message into an existing queue, first create a new instance of hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="25c31-375">Daarna roept Hallo [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) methode.</span><span class="sxs-lookup"><span data-stu-id="25c31-375">Next, call hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method.</span></span> <span data-ttu-id="25c31-376">Een CloudQueueMessage kan worden gemaakt vanuit een tekenreeks (in UTF-8-indeling) of een byte-matrix.</span><span class="sxs-lookup"><span data-stu-id="25c31-376">A CloudQueueMessage can be created from either a string (in UTF-8 format) or a byte array.</span></span>

<span data-ttu-id="25c31-377">Hallo volgende voorbeeld laat zien hoe tooadd tooa wachtrij bericht.</span><span class="sxs-lookup"><span data-stu-id="25c31-377">hello following example demonstrates how tooadd message tooa queue.</span></span> <span data-ttu-id="25c31-378">Hallo-voorbeeld wordt eerst een verbinding tooAzure opslag met Hallo storage account context, waaronder Hallo opslagaccountnaam en de toegangssleutel.</span><span class="sxs-lookup"><span data-stu-id="25c31-378">hello example first establishes a connection tooAzure Storage using hello storage account context, which includes hello storage account name and its access key.</span></span> <span data-ttu-id="25c31-379">Vervolgens wordt het ophalen van Hallo van de opgegeven wachtrij met Hallo [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="25c31-379">Next, it retrieves hello specified queue using hello [Get-AzureStorageQueue](https://msdn.microsoft.com/library/azure/dn806377.aspx) cmdlet.</span></span> <span data-ttu-id="25c31-380">Als Hallo wachtrij, hello bestaat [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet is gebruikte toocreate een exemplaar van Hallo [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) klasse.</span><span class="sxs-lookup"><span data-stu-id="25c31-380">If hello queue exists, hello [New-Object](http://technet.microsoft.com/library/hh849885.aspx) cmdlet is used toocreate an instance of hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage](http://msdn.microsoft.com/library/azure/jj732474.aspx) class.</span></span> <span data-ttu-id="25c31-381">Later Hallo voorbeeld Hallo roept [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) methode voor dit bericht object tooadd het tooa wachtrij.</span><span class="sxs-lookup"><span data-stu-id="25c31-381">Later, hello example calls hello [AddMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.addmessage.aspx) method on this message object tooadd it tooa queue.</span></span> <span data-ttu-id="25c31-382">Hier volgt een code die een wachtrij opgehaald en voegt het Hallo-bericht 'MessageInfo':</span><span class="sxs-lookup"><span data-stu-id="25c31-382">Here is code which retrieves a queue and inserts hello message 'MessageInfo':</span></span>

```powershell
#Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

#Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

#If hello queue exists, add a new message.
if ($Queue -ne $null) {
   # Create a new message using a constructor of hello CloudQueueMessage class.
   $QueueMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList MessageInfo

   # Add a new message toohello queue.
   $Queue.CloudQueue.AddMessage($QueueMessage)
}
```

#### <a name="how-toode-queue-at-hello-next-message"></a><span data-ttu-id="25c31-383">Hoe toode-wachtrij op Hallo volgend bericht</span><span class="sxs-lookup"><span data-stu-id="25c31-383">How toode-queue at hello next message</span></span>
<span data-ttu-id="25c31-384">Met uw code wordt een bericht in twee stappen uit de wachtrij verwijderd.</span><span class="sxs-lookup"><span data-stu-id="25c31-384">Your code de-queues a message from a queue in two steps.</span></span> <span data-ttu-id="25c31-385">Wanneer u Hallo aanroepen [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) methode, krijgt u het volgende Hallo-bericht in een wachtrij.</span><span class="sxs-lookup"><span data-stu-id="25c31-385">When you call hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.GetMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.getmessage.aspx) method, you get hello next message in a queue.</span></span> <span data-ttu-id="25c31-386">Een bericht dat wordt geretourneerd door **GetMessage** wordt onzichtbaar tooany andere codes die berichten lezen uit deze wachtrij.</span><span class="sxs-lookup"><span data-stu-id="25c31-386">A message returned from **GetMessage** becomes invisible tooany other code reading messages from this queue.</span></span> <span data-ttu-id="25c31-387">toofinish verwijderen Hallo-bericht uit de wachtrij hello, moet u ook Hallo aanroepen [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) methode.</span><span class="sxs-lookup"><span data-stu-id="25c31-387">toofinish removing hello message from hello queue, you must also call hello [Microsoft.WindowsAzure.Storage.Queue.CloudQueue.DeleteMessage](http://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.queue.cloudqueue.deletemessage.aspx) method.</span></span> <span data-ttu-id="25c31-388">Dit proces in twee stappen van het verwijderen van een bericht zorgt ervoor dat als uw code mislukt tooprocess een bericht vanwege problemen toohardware of software, een ander exemplaar van uw code krijgt hetzelfde bericht Hallo en probeer het opnieuw.</span><span class="sxs-lookup"><span data-stu-id="25c31-388">This two-step process of removing a message assures that if your code fails tooprocess a message due toohardware or software failure, another instance of your code can get hello same message and try again.</span></span> <span data-ttu-id="25c31-389">Uw code haalt **DeleteMessage** direct nadat het Hallo-bericht is verwerkt.</span><span class="sxs-lookup"><span data-stu-id="25c31-389">Your code calls **DeleteMessage** right after hello message has been processed.</span></span>

```powershell
# Define hello storage account and context.
$StorageAccountName = "yourstorageaccount"
$StorageAccountKey = Get-AzureStorageKey -StorageAccountName $StorageAccountName
$Ctx = New-AzureStorageContext –StorageAccountName $StorageAccountName -StorageAccountKey $StorageAccountKey.Primary

# Retrieve hello queue.
$QueueName = "queuename"
$Queue = Get-AzureStorageQueue -Name $QueueName -Context $ctx

$InvisibleTimeout = [System.TimeSpan]::FromSeconds(10)

# Get hello message object from hello queue.
$QueueMessage = $Queue.CloudQueue.GetMessage($InvisibleTimeout)
# Delete hello message.
$Queue.CloudQueue.DeleteMessage($QueueMessage)
```

## <a name="how-toomanage-azure-file-shares-and-files"></a><span data-ttu-id="25c31-390">Hoe toomanage Azure-bestand deelt, en bestanden</span><span class="sxs-lookup"><span data-stu-id="25c31-390">How toomanage Azure file shares and files</span></span>
<span data-ttu-id="25c31-391">Azure File storage biedt gedeelde opslag voor toepassingen die gebruikmaken van Hallo standaard SMB-protocol.</span><span class="sxs-lookup"><span data-stu-id="25c31-391">Azure File storage offers shared storage for applications using hello standard SMB protocol.</span></span> <span data-ttu-id="25c31-392">Microsoft Azure virtuele machines en cloudservices kunnen bestandsgegevens delen tussen toepassingsonderdelen via gekoppelde shares en on-premises toepassingen hebben toegang tot bestandsgegevens in een share via Hallo bestands-API voor storage of Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="25c31-392">Microsoft Azure virtual machines and cloud services can share file data across application components via mounted shares, and on-premises applications can access file data in a share via hello File storage API or Azure PowerShell.</span></span>

<span data-ttu-id="25c31-393">Zie voor meer informatie over Azure File storage [aan de slag met Azure File storage in Windows](storage-dotnet-how-to-use-files.md) en [REST-API van bestand](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span><span class="sxs-lookup"><span data-stu-id="25c31-393">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) and [File Service REST API](http://msdn.microsoft.com/library/azure/dn167006.aspx).</span></span>

## <a name="how-tooset-and-query-storage-analytics"></a><span data-ttu-id="25c31-394">Hoe tooset en query storage analytics</span><span class="sxs-lookup"><span data-stu-id="25c31-394">How tooset and query storage analytics</span></span>
<span data-ttu-id="25c31-395">U kunt [Azure Storage Analytics](storage-analytics.md) toocollect metrische gegevens voor uw Azure storage-accounts en logboekgegevens over aanvragen verzonden tooyour storage-account.</span><span class="sxs-lookup"><span data-stu-id="25c31-395">You can use [Azure Storage Analytics](storage-analytics.md) toocollect metrics for your Azure storage accounts and log data about requests sent tooyour storage account.</span></span> <span data-ttu-id="25c31-396">U kunt opslag metrische gegevens toomonitor Hallo status van een opslagaccount en opslag logboekregistratie toodiagnose gebruiken en oplossen van problemen met uw storage-account.</span><span class="sxs-lookup"><span data-stu-id="25c31-396">You can use storage metrics toomonitor hello health of a storage account, and storage logging toodiagnose and troubleshoot issues with your storage account.</span></span> <span data-ttu-id="25c31-397">U kunt configureren met behulp van bewaking hello Azure-portal of met Windows PowerShell of programmatisch met Hallo storage-clientbibliotheek.</span><span class="sxs-lookup"><span data-stu-id="25c31-397">You can configure monitoring using hello Azure portal or Windows PowerShell, or programmatically using hello storage client library.</span></span> <span data-ttu-id="25c31-398">Opslag logboekregistratie gebeurt serverzijde en kunt u toorecord details voor geslaagde en mislukte aanvragen in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="25c31-398">Storage logging happens server-side and enables you toorecord details for both successful and failed requests in your storage account.</span></span> <span data-ttu-id="25c31-399">Deze logboeken inschakelen toosee details van lees-, schrijf- en delete-bewerkingen op basis van uw tabellen, wachtrijen en blobs, evenals Hallo redenen voor mislukte aanvragen.</span><span class="sxs-lookup"><span data-stu-id="25c31-399">These logs enable you toosee details of read, write, and delete operations against your tables, queues, and blobs as well as hello reasons for failed requests.</span></span>

<span data-ttu-id="25c31-400">hoe tooenable en bekijk metrische gegevens voor opslag van gegevens met behulp van PowerShell, Zie toolearn [hoe tooenable metrische gegevens Storage met behulp van PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span><span class="sxs-lookup"><span data-stu-id="25c31-400">toolearn how tooenable and view Storage Metrics data using PowerShell, see [How tooenable Storage Metrics using PowerShell](http://msdn.microsoft.com/library/azure/dn782843.aspx#HowtoenableStorageMetricsusingPowerShell).</span></span>

<span data-ttu-id="25c31-401">hoe tooenable en ophalen logboekregistratie van opslag van gegevens met behulp van PowerShell, Zie toolearn [hoe tooenable opslag logboekregistratie met behulp van PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) en [zoeken naar uw logboekgegevens opslag logboekregistratie](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span><span class="sxs-lookup"><span data-stu-id="25c31-401">toolearn how tooenable and retrieve Storage Logging data using PowerShell, see [How tooenable Storage Logging using PowerShell](http://msdn.microsoft.com/library/azure/dn782840.aspx#HowtoenableStorageLoggingusingPowerShell) and [Finding your Storage Logging log data](http://msdn.microsoft.com/library/azure/dn782840.aspx#FindingyourStorageLogginglogdata).</span></span>
<span data-ttu-id="25c31-402">Zie voor gedetailleerde informatie over het gebruik van opslag metrische gegevens en opslag logboekregistratie opslagproblemen tootroubleshoot [bewaking, diagnose en het oplossen van Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="25c31-402">For detailed information on using Storage Metrics and Storage Logging tootroubleshoot storage issues, see [Monitoring, Diagnosing, and Troubleshooting Microsoft Azure Storage](storage-monitoring-diagnosing-troubleshooting.md).</span></span>

## <a name="how-toomanage-shared-access-signature-sas-and-stored-access-policy"></a><span data-ttu-id="25c31-403">Hoe toomanage Shared Access Signature (SAS) en toegangsbeleid opgeslagen</span><span class="sxs-lookup"><span data-stu-id="25c31-403">How toomanage Shared Access Signature (SAS) and Stored Access Policy</span></span>
<span data-ttu-id="25c31-404">Shared access signatures zijn een belangrijk onderdeel van het beveiligingsmodel Hallo voor elke toepassing met behulp van Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="25c31-404">Shared access signatures are an important part of hello security model for any application using Azure Storage.</span></span> <span data-ttu-id="25c31-405">Ze zijn nuttig voor het leveren van beperkte machtigingen tooyour storage account tooclients Hallo accountsleutel niet hebben.</span><span class="sxs-lookup"><span data-stu-id="25c31-405">They are useful for providing limited permissions tooyour storage account tooclients that should not have hello account key.</span></span> <span data-ttu-id="25c31-406">Standaard hebben alleen de eigenaar van het opslagaccount Hallo Hallo mogelijk toegang tot blobs, tabellen en wachtrijen in dat account.</span><span class="sxs-lookup"><span data-stu-id="25c31-406">By default, only hello owner of hello storage account may access blobs, tables, and queues within that account.</span></span> <span data-ttu-id="25c31-407">Als uw service of toepassing moet toomake deze resources beschikbaar tooother clients zonder het delen van uw toegangssleutel, hebt u drie opties:</span><span class="sxs-lookup"><span data-stu-id="25c31-407">If your service or application needs toomake these resources available tooother clients without sharing your access key, you have three options:</span></span>

* <span data-ttu-id="25c31-408">Een container machtigingen toopermit anonieme leestoegang toohello container en de bijbehorende blobs instellen.</span><span class="sxs-lookup"><span data-stu-id="25c31-408">Set a container's permissions toopermit anonymous read access toohello container and its blobs.</span></span> <span data-ttu-id="25c31-409">Dit is niet toegestaan voor tabellen of wachtrijen.</span><span class="sxs-lookup"><span data-stu-id="25c31-409">This is not allowed for tables or queues.</span></span>
* <span data-ttu-id="25c31-410">Gebruik een shared access signature die beperkte toegang rechten toocontainers, blobs, wachtrijen en tabellen voor een bepaald tijdsinterval verleent.</span><span class="sxs-lookup"><span data-stu-id="25c31-410">Use a shared access signature that grants restricted access rights toocontainers, blobs, queues, and tables for a specific time interval.</span></span>
* <span data-ttu-id="25c31-411">Gebruik een opgeslagen toegang beleid tooobtain een extra verificatieniveau controle over handtekeningen voor gedeelde toegang voor een container of de blobs, voor een wachtrij of voor een tabel.</span><span class="sxs-lookup"><span data-stu-id="25c31-411">Use a stored access policy tooobtain an additional level of control over shared access signatures for a container or its blobs, for a queue, or for a table.</span></span> <span data-ttu-id="25c31-412">Hallo opgeslagen toegangsbeleid kunt u toochange Hallo begintijd, verlooptijd of machtigingen voor een handtekening of toorevoke deze nadat deze is uitgegeven.</span><span class="sxs-lookup"><span data-stu-id="25c31-412">hello stored access policy allows you toochange hello start time, expiry time, or permissions for a signature, or toorevoke it after it has been issued.</span></span>

<span data-ttu-id="25c31-413">Een shared access signature kan worden gebruikt in een van twee vormen:</span><span class="sxs-lookup"><span data-stu-id="25c31-413">A shared access signature can be in one of two forms:</span></span>

* <span data-ttu-id="25c31-414">**Ad-hoc SAS**: wanneer u een ad-hoc SAS, begintijd hello, verlooptijd maken en machtigingen voor Hallo SAS zijn opgegeven op Hallo SAS-URI.</span><span class="sxs-lookup"><span data-stu-id="25c31-414">**Ad hoc SAS**: When you create an ad hoc SAS, hello start time, expiry time, and permissions for hello SAS are all specified on hello SAS URI.</span></span> <span data-ttu-id="25c31-415">Dit type SAS kan worden gemaakt op een container, blob, table of wachtrij en het is niet worden ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="25c31-415">This type of SAS may be created on a container, blob, table, or queue and it is non-revocable.</span></span>
* <span data-ttu-id="25c31-416">**SAS met opgeslagen toegangsbeleid**: een opgeslagen-beleid is gedefinieerd in een resourcecontainer een blob-container, een tabel of een wachtrij - en u kunt deze gebruiken toomanage beperkingen voor een of meer handtekeningen voor gedeelde toegang.</span><span class="sxs-lookup"><span data-stu-id="25c31-416">**SAS with stored access policy**: A stored access policy is defined on a resource container a blob container, table, or queue - and you can use it toomanage constraints for one or more shared access signatures.</span></span> <span data-ttu-id="25c31-417">Wanneer u een SAS aan een opgeslagen toegangsbeleid koppelt, Hallo SAS neemt over Hallo beperkingen - Hallo starttijd, verlooptijd en machtigingen - zijn opgegeven voor toegangsbeleid Hallo opgeslagen.</span><span class="sxs-lookup"><span data-stu-id="25c31-417">When you associate a SAS with a stored access policy, hello SAS inherits hello constraints - hello start time, expiry time, and permissions - defined for hello stored access policy.</span></span> <span data-ttu-id="25c31-418">Dit type SAS is worden ingetrokken.</span><span class="sxs-lookup"><span data-stu-id="25c31-418">This type of SAS is revocable.</span></span>

<span data-ttu-id="25c31-419">Zie voor meer informatie [met behulp van Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) en [anonieme leestoegang toocontainers en blobs beheren](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="25c31-419">For more information, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) and [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md).</span></span>

<span data-ttu-id="25c31-420">In de volgende secties hello, leert u hoe toocreate een beleid voor gedeelde toegang handtekening access token en de opslag voor Azure-tabellen.</span><span class="sxs-lookup"><span data-stu-id="25c31-420">In hello next sections, you will learn how toocreate a shared access signature token and stored access policy for Azure tables.</span></span> <span data-ttu-id="25c31-421">Azure PowerShell biedt vergelijkbare cmdlets voor containers, blobs en wachtrijen ook.</span><span class="sxs-lookup"><span data-stu-id="25c31-421">Azure PowerShell provides similar cmdlets for containers, blobs, and queues as well.</span></span> <span data-ttu-id="25c31-422">toorun hello scripts in deze sectie download Hallo [Azure PowerShell versie 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) of hoger.</span><span class="sxs-lookup"><span data-stu-id="25c31-422">toorun hello scripts in this section, download hello [Azure PowerShell version 0.8.14](http://go.microsoft.com/?linkid=9811175&clcid=0x409) or later.</span></span>

### <a name="how-toocreate-a-policy-based-shared-access-signature-token"></a><span data-ttu-id="25c31-423">Hoe een op beleid gebaseerde toocreate Shared Access Signature-token</span><span class="sxs-lookup"><span data-stu-id="25c31-423">How toocreate a policy-based Shared Access Signature token</span></span>
<span data-ttu-id="25c31-424">Hallo nieuw AzureStorageTableStoredAccessPolicy cmdlet toocreate een nieuw opgeslagen-beleid gebruiken.</span><span class="sxs-lookup"><span data-stu-id="25c31-424">Use hello New-AzureStorageTableStoredAccessPolicy cmdlet toocreate a new stored access policy.</span></span> <span data-ttu-id="25c31-425">Roep vervolgens Hallo [nieuw AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate een nieuw token van de handtekening gedeelde toegang op basis van beleid voor een Azure Storage-tabel.</span><span class="sxs-lookup"><span data-stu-id="25c31-425">Then, call hello [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate a new policy-based shared access signature token for an Azure Storage table.</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
New-AzureStorageTableSASToken -Name $tableName -Policy $policy -Context $Ctx
```

### <a name="how-toocreate-an-ad-hoc-non-revocable-shared-access-signature-token"></a><span data-ttu-id="25c31-426">Hoe toocreate een ad-hoc (niet terughalen) Shared Access Signature-token</span><span class="sxs-lookup"><span data-stu-id="25c31-426">How toocreate an ad hoc (non-revocable) Shared Access Signature token</span></span>
<span data-ttu-id="25c31-427">Gebruik Hallo [nieuw AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate een nieuw ad-hoc (niet terughalen) Shared Access Signature-token voor een Azure Storage-tabel:</span><span class="sxs-lookup"><span data-stu-id="25c31-427">Use hello [New-AzureStorageTableSASToken](/powershell/module/azure.storage/new-azurestoragetablesastoken) cmdlet toocreate a new ad hoc (non-revocable) Shared Access Signature token for an Azure Storage table:</span></span>

```powershell
New-AzureStorageTableSASToken -Name $tableName -Permission "rqud" -StartTime "2015-01-01" -ExpiryTime "2015-02-01" -Context $Ctx
```
    
### <a name="how-toocreate-a-stored-access-policy"></a><span data-ttu-id="25c31-428">Hoe toocreate een opgeslagen-beleid</span><span class="sxs-lookup"><span data-stu-id="25c31-428">How toocreate a stored access policy</span></span>
<span data-ttu-id="25c31-429">Hallo nieuw AzureStorageTableStoredAccessPolicy cmdlet toocreate een nieuw opgeslagen-beleid gebruiken voor een Azure Storage-tabel:</span><span class="sxs-lookup"><span data-stu-id="25c31-429">Use hello New-AzureStorageTableStoredAccessPolicy cmdlet toocreate a new stored access policy for an Azure Storage table:</span></span>

```powershell
$policy = "policy1"
New-AzureStorageTableStoredAccessPolicy -Name $tableName -Policy $policy -Permission "rd" -StartTime "2015-01-01" -ExpiryTime "2016-01-01" -Context $Ctx
```
    
### <a name="how-tooupdate-a-stored-access-policy"></a><span data-ttu-id="25c31-430">Hoe tooupdate een opgeslagen-beleid</span><span class="sxs-lookup"><span data-stu-id="25c31-430">How tooupdate a stored access policy</span></span>
<span data-ttu-id="25c31-431">Hallo Set AzureStorageTableStoredAccessPolicy cmdlet tooupdate een bestaand opgeslagen toegangsbeleid gebruiken voor een Azure Storage-tabel:</span><span class="sxs-lookup"><span data-stu-id="25c31-431">Use hello Set-AzureStorageTableStoredAccessPolicy cmdlet tooupdate an existing stored access policy for an Azure Storage table:</span></span>

```powershell
Set-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Permission "rd" -NoExpiryTime -NoStartTime -Context $Ctx
```

### <a name="how-toodelete-a-stored-access-policy"></a><span data-ttu-id="25c31-432">Hoe toodelete een opgeslagen-beleid</span><span class="sxs-lookup"><span data-stu-id="25c31-432">How toodelete a stored access policy</span></span>
<span data-ttu-id="25c31-433">Hallo verwijderen AzureStorageTableStoredAccessPolicy cmdlet toodelete een opgeslagen-beleid gebruiken in de tabel in een Azure Storage:</span><span class="sxs-lookup"><span data-stu-id="25c31-433">Use hello Remove-AzureStorageTableStoredAccessPolicy cmdlet toodelete a stored access policy on an Azure Storage table:</span></span>

```powershell
Remove-AzureStorageTableStoredAccessPolicy -Policy $policy -Table $tableName -Context $Ctx
```

## <a name="how-toouse-azure-storage-for-us-government-and-azure-china"></a><span data-ttu-id="25c31-434">Hoe toouse Azure Storage voor de Amerikaanse overheid en Azure voor China</span><span class="sxs-lookup"><span data-stu-id="25c31-434">How toouse Azure Storage for U.S. government and Azure China</span></span>
<span data-ttu-id="25c31-435">Een Azure-omgeving is een onafhankelijke implementatie van Microsoft Azure, zoals [Azure Government voor de overheid van de VS](https://azure.microsoft.com/features/gov/), [AzureCloud voor globale Azure](https://portal.azure.com), en [AzureChinaCloud voor Azure wordt beheerd door 21Vianet in China](http://www.windowsazure.cn/).</span><span class="sxs-lookup"><span data-stu-id="25c31-435">An Azure environment is an independent deployment of Microsoft Azure, such as [Azure Government for U.S. government](https://azure.microsoft.com/features/gov/), [AzureCloud for global Azure](https://portal.azure.com), and [AzureChinaCloud for Azure operated by 21Vianet in China](http://www.windowsazure.cn/).</span></span> <span data-ttu-id="25c31-436">U kunt nieuwe Azure-omgevingen voor Amerikaanse overheid en Azure voor China implementeren.</span><span class="sxs-lookup"><span data-stu-id="25c31-436">You can deploy new Azure environments for U.S government and Azure China.</span></span>

<span data-ttu-id="25c31-437">Azure Storage met AzureChinaCloud toouse, moet u een opslag-context die is gekoppeld aan AzureChinaCloud toocreate.</span><span class="sxs-lookup"><span data-stu-id="25c31-437">toouse Azure Storage with AzureChinaCloud, you need toocreate a storage context that is associated with AzureChinaCloud.</span></span> <span data-ttu-id="25c31-438">Volg deze stappen tooget u gestart:</span><span class="sxs-lookup"><span data-stu-id="25c31-438">Follow these steps tooget you started:</span></span>

1. <span data-ttu-id="25c31-439">Voer Hallo [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee Hallo beschikbare Azure-omgevingen:</span><span class="sxs-lookup"><span data-stu-id="25c31-439">Run hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello available Azure environments:</span></span>
   
    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="25c31-440">Een Azure China account tooWindows PowerShell toevoegen:</span><span class="sxs-lookup"><span data-stu-id="25c31-440">Add an Azure China account tooWindows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureChinaCloud
    ```

3. <span data-ttu-id="25c31-441">Maak een context opslag voor een account AzureChinaCloud:</span><span class="sxs-lookup"><span data-stu-id="25c31-441">Create a storage context for an AzureChinaCloud account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureChinaCloud
    ```

<span data-ttu-id="25c31-442">toouse Azure Storage met [VS Azure Government](https://azure.microsoft.com/features/gov/), moet u een nieuwe omgeving definiëren en vervolgens een nieuwe opslag context maken met deze omgeving:</span><span class="sxs-lookup"><span data-stu-id="25c31-442">toouse Azure Storage with [U.S. Azure Government](https://azure.microsoft.com/features/gov/), you should define a new environment and then create a new storage context with this environment:</span></span>

1. <span data-ttu-id="25c31-443">Voer Hallo [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee Hallo beschikbare Azure-omgevingen:</span><span class="sxs-lookup"><span data-stu-id="25c31-443">Run hello [Get-AzureEnvironment](/powershell/module/azure/get-azureenvironment?view=azuresmps-3.7.0) cmdlet toosee hello available Azure environments:</span></span>

    ```powershell
    Get-AzureEnvironment
    ```

2. <span data-ttu-id="25c31-444">Een Azure US Government account tooWindows PowerShell toevoegen:</span><span class="sxs-lookup"><span data-stu-id="25c31-444">Add an Azure US Government account tooWindows PowerShell:</span></span>
   
    ```powershell
    Add-AzureAccount –Environment AzureUSGovernment
    ```

3. <span data-ttu-id="25c31-445">Maak een context opslag voor een account AzureUSGovernment:</span><span class="sxs-lookup"><span data-stu-id="25c31-445">Create a storage context for an AzureUSGovernment account:</span></span>
   
    ```powershell
    $Ctx = New-AzureStorageContext -StorageAccountName $AccountName -StorageAccountKey $AccountKey> -Environment AzureUSGovernment
    ```
     
<span data-ttu-id="25c31-446">Zie voor meer informatie:</span><span class="sxs-lookup"><span data-stu-id="25c31-446">For more information, see:</span></span>

* <span data-ttu-id="25c31-447">[Ontwikkelaarshandleiding voor Microsoft Azure Government](../azure-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="25c31-447">[Microsoft Azure Government Developer Guide](../azure-government-developer-guide.md).</span></span>
* [<span data-ttu-id="25c31-448">Overzicht van verschillen bij het maken van een toepassing op China Service</span><span class="sxs-lookup"><span data-stu-id="25c31-448">Overview of Differences When Creating an Application on China Service</span></span>](https://msdn.microsoft.com/library/azure/dn578439.aspx)

## <a name="next-steps"></a><span data-ttu-id="25c31-449">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="25c31-449">Next Steps</span></span>
<span data-ttu-id="25c31-450">In deze handleiding hebt u geleerd hoe toomanage Azure Storage met Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="25c31-450">In this guide, you've learned how toomanage Azure Storage with Azure PowerShell.</span></span> <span data-ttu-id="25c31-451">Hier volgen enkele verwante artikelen en resources voor meer informatie hierover.</span><span class="sxs-lookup"><span data-stu-id="25c31-451">Here are some related articles and resources for learning more about them.</span></span>

* [<span data-ttu-id="25c31-452">Documentatie bij Azure Storage</span><span class="sxs-lookup"><span data-stu-id="25c31-452">Azure Storage Documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
* [<span data-ttu-id="25c31-453">PowerShell-Cmdlets voor Azure-opslag</span><span class="sxs-lookup"><span data-stu-id="25c31-453">Azure Storage PowerShell Cmdlets</span></span>](/powershell/module/azurerm.storage/#storage)
* [<span data-ttu-id="25c31-454">Windows PowerShell-referentie</span><span class="sxs-lookup"><span data-stu-id="25c31-454">Windows PowerShell Reference</span></span>](https://msdn.microsoft.com/library/ms714469.aspx)

[Getting started with Azure Storage and PowerShell in 5 minutes]: #getstart
[Prerequisites for using Azure PowerShell with Azure Storage]: #pre
[How toomanage storage accounts in Azure]: #manageaccount
[How tooset a default Azure subscription]: #setdefsub
[How toocreate a new Azure storage account]: #createaccount
[How tooset a default Azure storage account]: #defaultaccount
[How toolist all Azure storage accounts in a subscription]: #listaccounts
[How toocreate an Azure storage context]: #createctx
[How toomanage Azure blobs and blob snapshots]: #manageblobs
[How toocreate a container]: #container
[How tooupload a blob into a container]: #uploadblob
[How toodownload blobs from a container]: #downblob
[How toocopy blobs from one storage container tooanother]: #copyblob
[How toodelete a blob]: #deleteblob
[How toomanage Azure blob snapshots]: #manageshots
[How toocreate a blob snapshot]: #createshot
[How toolist snapshots of a blob]: #listshot
[How toocopy a snapshot of a blob]: #copyshot
[How toomanage Azure tables and table entities]: #managetables
[How toocreate a table]: #createtable
[How tooretrieve a table]: #gettable
[How toodelete a table]: #remtable
[How toomanage table entities]: #mngentity
[How tooadd table entities]: #addentity
[How tooquery table entities]: #queryentity
[How toodelete table entities]: #deleteentity
[How toomanage Azure queues and queue messages]: #managequeues
[How toocreate a queue]: #createqueue
[How tooretrieve a queue]: #getqueue
[How toodelete a queue]: #remqueue
[How toomanage queue messages]: #mngqueuemsg
[How tooinsert a message into a queue]: #addqueuemsg
[How toode-queue at hello next message]: #dequeuemsg
[How toomanage Azure file shares and files]: #files
[How tooset and query storage analytics]: #stganalytics
[How toomanage Shared Access Signature (SAS) and Stored Access Policy]: #sas
[How toouse Azure Storage for U.S. government and Azure China]: #gov
[Next Steps]: #next
