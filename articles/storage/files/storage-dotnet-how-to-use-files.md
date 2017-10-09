---
title: aaaDevelop voor Azure File storage met .NET | Microsoft Docs
description: Meer informatie over hoe toodevelop .NET-toepassingen en services die gebruikmaken van Azure File storage toostore bestandsgegevens.
services: storage
documentationcenter: .net
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6a889ee1-1e60-46ec-a592-ae854f9fb8b6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 79855f178111483edea13014b8eeecc3376dd4e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-net"></a><span data-ttu-id="5e4de-103">Ontwikkelen voor Azure File Storage met .NET</span><span class="sxs-lookup"><span data-stu-id="5e4de-103">Develop for Azure File storage with .NET</span></span> 
> [!NOTE]
> <span data-ttu-id="5e4de-104">Dit artikel laat zien hoe toomanage Azure File storage met .NET-code.</span><span class="sxs-lookup"><span data-stu-id="5e4de-104">This article shows how toomanage Azure File storage with .NET code.</span></span> <span data-ttu-id="5e4de-105">Raadpleeg Hallo toolearn meer informatie over Azure File storage [inleiding tooAzure bestandsopslag](storage-files-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="5e4de-105">toolearn more about Azure File storage, please see hello [Introduction tooAzure File storage](storage-files-introduction.md).</span></span>
>

[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="5e4de-106">Over deze zelfstudie</span><span class="sxs-lookup"><span data-stu-id="5e4de-106">About this tutorial</span></span>
<span data-ttu-id="5e4de-107">Deze zelfstudie wordt gedemonstreerd Hallo grondbeginselen van het gebruik van .NET-toodevelop toepassingen of services die gebruikmaken van Azure File storage toostore bestandsgegevens.</span><span class="sxs-lookup"><span data-stu-id="5e4de-107">This tutorial will demonstrate hello basics of using .NET toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="5e4de-108">In deze zelfstudie wordt een eenvoudige consoletoepassing maken en weergeven hoe tooperform basisbewerkingen uitvoeren met .NET- en Azure File storage:</span><span class="sxs-lookup"><span data-stu-id="5e4de-108">In this tutorial, we will create a simple console application and show how tooperform basic actions with .NET and Azure File storage:</span></span>

* <span data-ttu-id="5e4de-109">Hallo-inhoud van een bestand ophalen</span><span class="sxs-lookup"><span data-stu-id="5e4de-109">Get hello contents of a file</span></span>
* <span data-ttu-id="5e4de-110">Hallo quotum (maximumgrootte) voor bestandsshare Hallo instellen.</span><span class="sxs-lookup"><span data-stu-id="5e4de-110">Set hello quota (maximum size) for hello file share.</span></span>
* <span data-ttu-id="5e4de-111">Maak een shared access signature (SAS-sleutel) voor een bestand dat gebruikmaakt van een gedeeld toegangsbeleid dat is gedefinieerd op Hallo-share.</span><span class="sxs-lookup"><span data-stu-id="5e4de-111">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on hello share.</span></span>
* <span data-ttu-id="5e4de-112">Kopieer een bestand tooanother in Hallo hetzelfde opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="5e4de-112">Copy a file tooanother file in hello same storage account.</span></span>
* <span data-ttu-id="5e4de-113">Kopieer een bestand tooa blob in Hallo hetzelfde opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="5e4de-113">Copy a file tooa blob in hello same storage account.</span></span>
* <span data-ttu-id="5e4de-114">Metrische gegevens van Azure Storage gebruiken voor het oplossen van problemen</span><span class="sxs-lookup"><span data-stu-id="5e4de-114">Use Azure Storage Metrics for troubleshooting</span></span>

> [!Note]  
> <span data-ttu-id="5e4de-115">Omdat Azure File storage zijn toegankelijk via SMB, is het mogelijk toowrite eenvoudige toepassingen die toegang hebben tot hello Azure bestandsshare met behulp van Hallo standaardklassen System.IO voor i/o-bestand.</span><span class="sxs-lookup"><span data-stu-id="5e4de-115">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard System.IO classes for File I/O.</span></span> <span data-ttu-id="5e4de-116">In dit artikel wordt beschreven hoe toowrite toepassingen die gebruikmaken van Azure Storage .NET SDK, die gebruikmaakt van Hallo Hallo [Azure File storage REST-API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span><span class="sxs-lookup"><span data-stu-id="5e4de-116">This article will describe how toowrite applications that use hello Azure Storage .NET SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span> 


## <a name="create-hello-console-application-and-obtain-hello-assembly"></a><span data-ttu-id="5e4de-117">Hallo-consoletoepassing maken en Hallo assembly verkrijgen</span><span class="sxs-lookup"><span data-stu-id="5e4de-117">Create hello console application and obtain hello assembly</span></span>
<span data-ttu-id="5e4de-118">Maak in Visual Studio een nieuwe Windows-consoletoepassing.</span><span class="sxs-lookup"><span data-stu-id="5e4de-118">In Visual Studio, create a new Windows console application.</span></span> <span data-ttu-id="5e4de-119">Hallo stappen ziet u hoe toocreate een consoletoepassing in Visual Studio 2017 echter Hallo stappen zijn vergelijkbaar in andere versies van Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5e4de-119">hello following steps show you how toocreate a console application in Visual Studio 2017, however, hello steps are similar in other versions of Visual Studio.</span></span>

1. <span data-ttu-id="5e4de-120">Selecteer **Bestand** > **Nieuw** > **Project**</span><span class="sxs-lookup"><span data-stu-id="5e4de-120">Select **File** > **New** > **Project**</span></span>
2. <span data-ttu-id="5e4de-121">Selecteer **Geïnstalleerd** > **Sjablonen** > **Visual C#** > **Klassiek Windows-bureaublad**</span><span class="sxs-lookup"><span data-stu-id="5e4de-121">Select **Installed** > **Templates** > **Visual C#** > **Windows Classic Desktop**</span></span>
3. <span data-ttu-id="5e4de-122">Selecteer **Consoletoepassing (.NET Framework)**</span><span class="sxs-lookup"><span data-stu-id="5e4de-122">Select **Console App (.NET Framework)**</span></span>
4. <span data-ttu-id="5e4de-123">Voer een naam voor uw toepassing in Hallo **naam:** veld</span><span class="sxs-lookup"><span data-stu-id="5e4de-123">Enter a name for your application in hello **Name:** field</span></span>
5. <span data-ttu-id="5e4de-124">Selecteer **OK**</span><span class="sxs-lookup"><span data-stu-id="5e4de-124">Select **OK**</span></span>

<span data-ttu-id="5e4de-125">Alle codevoorbeelden in deze zelfstudie kunnen worden toegevoegd toohello `Main()` methode van uw consoletoepassing `Program.cs` bestand.</span><span class="sxs-lookup"><span data-stu-id="5e4de-125">All code examples in this tutorial can be added toohello `Main()` method of your console application's `Program.cs` file.</span></span>

<span data-ttu-id="5e4de-126">U kunt hello Azure Storage-clientbibliotheek gebruiken in elk type .NET-toepassing, met inbegrip van een Azure-cloud service of web-app en desktop- en mobiele toepassingen.</span><span class="sxs-lookup"><span data-stu-id="5e4de-126">You can use hello Azure Storage Client Library in any type of .NET application, including an Azure cloud service or web app, and desktop and mobile applications.</span></span> <span data-ttu-id="5e4de-127">In deze gids gebruiken we een consoletoepassing voor de eenvoud.</span><span class="sxs-lookup"><span data-stu-id="5e4de-127">In this guide, we use a console application for simplicity.</span></span>

## <a name="use-nuget-tooinstall-hello-required-packages"></a><span data-ttu-id="5e4de-128">Gebruik NuGet tooinstall vereist hello-pakketten</span><span class="sxs-lookup"><span data-stu-id="5e4de-128">Use NuGet tooinstall hello required packages</span></span>
<span data-ttu-id="5e4de-129">Er zijn twee pakketten die u in deze zelfstudie tooreference in uw project toocomplete nodig:</span><span class="sxs-lookup"><span data-stu-id="5e4de-129">There are two packages you need tooreference in your project toocomplete this tutorial:</span></span>

* <span data-ttu-id="5e4de-130">[Microsoft Azure Storage-clientbibliotheek voor .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): dit pakket biedt programmatisch toegang toodata resources in uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="5e4de-130">[Microsoft Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): This package provides programmatic access toodata resources in your storage account.</span></span>
* <span data-ttu-id="5e4de-131">[Configuration Manager-bibliotheek van Microsoft Azure voor .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): dit pakket biedt een klasse voor het parseren van een verbindingsreeks in een configuratiebestand, ongeacht waar de toepassing wordt uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5e4de-131">[Microsoft Azure Configuration Manager library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): This package provides a class for parsing a connection string in a configuration file, regardless of where your application is running.</span></span>

<span data-ttu-id="5e4de-132">U kunt beide pakketten NuGet tooobtain.</span><span class="sxs-lookup"><span data-stu-id="5e4de-132">You can use NuGet tooobtain both packages.</span></span> <span data-ttu-id="5e4de-133">Volg deze stappen:</span><span class="sxs-lookup"><span data-stu-id="5e4de-133">Follow these steps:</span></span>

1. <span data-ttu-id="5e4de-134">Klik met de rechtermuisknop op het project in **Solution Explorer** en kies **NuGet-pakketten beheren**.</span><span class="sxs-lookup"><span data-stu-id="5e4de-134">Right-click your project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="5e4de-135">Zoek online naar 'WindowsAzure.Storage' en klik op **installeren** tooinstall Hallo Storage-clientbibliotheek en de bijbehorende afhankelijkheden.</span><span class="sxs-lookup"><span data-stu-id="5e4de-135">Search online for "WindowsAzure.Storage" and click **Install** tooinstall hello Storage Client Library and its dependencies.</span></span>
3. <span data-ttu-id="5e4de-136">Zoek online naar 'WindowsAzure.ConfigurationManager' en klik op **installeren** tooinstall hello Azure Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="5e4de-136">Search online for "WindowsAzure.ConfigurationManager" and click **Install** tooinstall hello Azure Configuration Manager.</span></span>

## <a name="save-your-storage-account-credentials-toohello-appconfig-file"></a><span data-ttu-id="5e4de-137">Het storage-account referenties toohello app.config-bestand opslaan</span><span class="sxs-lookup"><span data-stu-id="5e4de-137">Save your storage account credentials toohello app.config file</span></span>
<span data-ttu-id="5e4de-138">Vervolgens slaat u uw referenties op in het bestand app.config van het project.</span><span class="sxs-lookup"><span data-stu-id="5e4de-138">Next, save your credentials in your project's app.config file.</span></span> <span data-ttu-id="5e4de-139">Hallo app.config-bestand bewerken zodat het lijkt of vergelijkbare toohello voorbeeld te volgen en vervangt `myaccount` met de naam van uw opslagaccount, en `mykey` door de sleutel van uw opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="5e4de-139">Edit hello app.config file so that it appears similar toohello following example, replacing `myaccount` with your storage account name, and `mykey` with your storage account key.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    <appSettings>
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=StorageAccountKeyEndingIn==" />
    </appSettings>
</configuration>
```

> [!NOTE]
> Hallo meest recente versie van hello Azure-opslagemulator biedt geen ondersteuning voor Azure File storage. <span data-ttu-id="5e4de-141">De verbindingsreeks moet gericht zijn op een Azure Storage-Account in Hallo cloud toowork met Azure File storage.</span><span class="sxs-lookup"><span data-stu-id="5e4de-141">Your connection string must target an Azure Storage Account in hello cloud toowork with Azure File storage.</span></span>

## <a name="add-using-directives"></a><span data-ttu-id="5e4de-142">Using-instructies toevoegen</span><span class="sxs-lookup"><span data-stu-id="5e4de-142">Add using directives</span></span>
<span data-ttu-id="5e4de-143">Open Hallo `Program.cs` bestand van Solution Explorer, en voeg de volgende Hallo met richtlijnen toohello boven in Hallo-bestand.</span><span class="sxs-lookup"><span data-stu-id="5e4de-143">Open hello `Program.cs` file from Solution Explorer, and add hello following using directives toohello top of hello file.</span></span>

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-hello-file-share-programmatically"></a><span data-ttu-id="5e4de-144">Toegang tot Hallo-bestand delen via een programma</span><span class="sxs-lookup"><span data-stu-id="5e4de-144">Access hello file share programmatically</span></span>
<span data-ttu-id="5e4de-145">Vervolgens voegt u code toohello na Hallo `Main()` methode (na de hierboven weergegeven code Hallo) tooretrieve Hallo-verbindingsreeks.</span><span class="sxs-lookup"><span data-stu-id="5e4de-145">Next, add hello following code toohello `Main()` method (after hello code shown above) tooretrieve hello connection string.</span></span> <span data-ttu-id="5e4de-146">Deze code wordt een referentiebestand toohello die we eerder hebben gemaakt en levert het consolevenster van inhoud toohello.</span><span class="sxs-lookup"><span data-stu-id="5e4de-146">This code gets a reference toohello file we created earlier and outputs its contents toohello console window.</span></span>

```csharp
// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Get a reference toohello root directory for hello share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference toohello directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that hello directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference toohello file we created previously.
        CloudFile file = sampleDir.GetFileReference("Log1.txt");

        // Ensure that hello file exists.
        if (file.Exists())
        {
            // Write hello contents of hello file toohello console window.
            Console.WriteLine(file.DownloadTextAsync().Result);
        }
    }
}
```

<span data-ttu-id="5e4de-147">Hallo console toepassing toosee Hallo-uitvoer worden uitgevoerd.</span><span class="sxs-lookup"><span data-stu-id="5e4de-147">Run hello console application toosee hello output.</span></span>

## <a name="set-hello-maximum-size-for-a-file-share"></a><span data-ttu-id="5e4de-148">Hallo maximale grootte voor een bestandsshare instellen</span><span class="sxs-lookup"><span data-stu-id="5e4de-148">Set hello maximum size for a file share</span></span>
<span data-ttu-id="5e4de-149">Vanaf versie 5.x van hello Azure Storage-clientbibliotheek kunt u instellen set Hallo quotum (of maximumgrootte) voor een bestandsshare in gigabytes.</span><span class="sxs-lookup"><span data-stu-id="5e4de-149">Beginning with version 5.x of hello Azure Storage Client Library, you can set set hello quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="5e4de-150">U kunt ook controleren hoeveel gegevens er momenteel zijn opgeslagen op Hallo share toosee.</span><span class="sxs-lookup"><span data-stu-id="5e4de-150">You can also check toosee how much data is currently stored on hello share.</span></span>

<span data-ttu-id="5e4de-151">Door de instelling Hallo quotum voor een share, kunt u Hallo totale grootte van bestanden op Hallo share Hallo beperken.</span><span class="sxs-lookup"><span data-stu-id="5e4de-151">By setting hello quota for a share, you can limit hello total size of hello files stored on hello share.</span></span> <span data-ttu-id="5e4de-152">Als Hallo totale grootte van bestanden op Hallo share overschrijdt Hallo quota ingesteld voor de share Hallo en clients worden niet kan tooincrease Hallo grootte van de bestaande bestanden of nieuwe bestanden maken, tenzij deze bestanden leeg zijn.</span><span class="sxs-lookup"><span data-stu-id="5e4de-152">If hello total size of files on hello share exceeds hello quota set on hello share, then clients will be unable tooincrease hello size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="5e4de-153">Hallo voorbeeld hieronder ziet u hoe toocheck huidige gebruik voor een share Hallo en hoe tooset quotum voor de share Hallo Hallo.</span><span class="sxs-lookup"><span data-stu-id="5e4de-153">hello example below shows how toocheck hello current usage for a share and how tooset hello quota for hello share.</span></span>

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Check current usage stats for hello share.
    // Note that hello ShareStats object is part of hello protocol layer for hello File service.
    Microsoft.WindowsAzure.Storage.File.Protocol.ShareStats stats = share.GetStats();
    Console.WriteLine("Current share usage: {0} GB", stats.Usage.ToString());

    // Specify hello maximum size of hello share, in GB.
    // This line sets hello quota toobe 10 GB greater than hello current usage of hello share.
    share.Properties.Quota = 10 + stats.Usage;
    share.SetProperties();

    // Now check hello quota for hello share. Call FetchAttributes() toopopulate hello share's properties.
    share.FetchAttributes();
    Console.WriteLine("Current share quota: {0} GB", share.Properties.Quota);
}
```

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="5e4de-154">Een Shared Access Signature genereren voor een bestand of bestandsshare</span><span class="sxs-lookup"><span data-stu-id="5e4de-154">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="5e4de-155">Vanaf versie 5.x van Azure Storage-clientbibliotheek Hallo, kunt u een shared access signature (SAS) voor een bestandsshare of voor een afzonderlijk bestand genereren.</span><span class="sxs-lookup"><span data-stu-id="5e4de-155">Beginning with version 5.x of hello Azure Storage Client Library, you can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="5e4de-156">U kunt ook een gedeeld toegangsbeleid op een bestandsshare-toomanage gedeelde toegang handtekeningen maken.</span><span class="sxs-lookup"><span data-stu-id="5e4de-156">You can also create a shared access policy on a file share toomanage shared access signatures.</span></span> <span data-ttu-id="5e4de-157">Maken van een gedeeld toegangsbeleid wordt aanbevolen, aangezien deze een manier om Hallo SAS intrekken biedt als deze verdacht.</span><span class="sxs-lookup"><span data-stu-id="5e4de-157">Creating a shared access policy is recommended, as it provides a means of revoking hello SAS if it should be compromised.</span></span>

<span data-ttu-id="5e4de-158">Hallo volgende voorbeeld wordt een beleid voor gedeelde toegang gemaakt op een bestandsshare op en gebruikt u vervolgens dat tooprovide Hallo beleidsbeperkingen voor een SAS voor een bestand in Hallo delen.</span><span class="sxs-lookup"><span data-stu-id="5e4de-158">hello following example creates a shared access policy on a share, and then uses that policy tooprovide hello constraints for a SAS on a file in hello share.</span></span>

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    string policyName = "sampleSharePolicy" + DateTime.UtcNow.Ticks;

    // Create a new shared access policy and define its constraints.
    SharedAccessFilePolicy sharedPolicy = new SharedAccessFilePolicy()
        {
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessFilePermissions.Read | SharedAccessFilePermissions.Write
        };

    // Get existing permissions for hello share.
    FileSharePermissions permissions = share.GetPermissions();

    // Add hello shared access policy toohello share's policies. Note that each policy must have a unique name.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    share.SetPermissions(permissions);

    // Generate a SAS for a file in hello share and associate this access policy with it.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");
    CloudFile file = sampleDir.GetFileReference("Log1.txt");
    string sasToken = file.GetSharedAccessSignature(null, policyName);
    Uri fileSasUri = new Uri(file.StorageUri.PrimaryUri.ToString() + sasToken);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.
    CloudFile fileSas = new CloudFile(fileSasUri);
    fileSas.UploadText("This write operation is authenticated via SAS.");
    Console.WriteLine(fileSas.DownloadText());
}
```

<span data-ttu-id="5e4de-159">Voor meer informatie over het maken en gebruiken van handtekeningen voor gedeelde toegang, raadpleegt u [Using Shared Access Signatures (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) (Shared Access Signatures (SAS) gebruiken) en [Create and use a SAS with Azure Blobs](../blobs/storage-dotnet-shared-access-signature-part-2.md) (Een SAS maken en gebruiken met Azure Blobs).</span><span class="sxs-lookup"><span data-stu-id="5e4de-159">For more information about creating and using shared access signatures, see [Using Shared Access Signatures (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) and [Create and use a SAS with Azure Blobs](../blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span>

## <a name="copy-files"></a><span data-ttu-id="5e4de-160">Bestanden kopiëren</span><span class="sxs-lookup"><span data-stu-id="5e4de-160">Copy files</span></span>
<span data-ttu-id="5e4de-161">Vanaf versie 5.x van Azure Storage-clientbibliotheek hello, kunt u een bestand tooanother, een bestand tooa blob of een blob tooa-bestand kopiëren.</span><span class="sxs-lookup"><span data-stu-id="5e4de-161">Beginning with version 5.x of hello Azure Storage Client Library, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="5e4de-162">In de volgende secties hello, ziet u hoe tooperform die deze kopiëren bewerkingen via een programma.</span><span class="sxs-lookup"><span data-stu-id="5e4de-162">In hello next sections, we demonstrate how tooperform these copy operations programmatically.</span></span>

<span data-ttu-id="5e4de-163">U kunt ook AzCopy toocopy één bestand tooanother of toocopy een blob tooa bestand of vice versa.</span><span class="sxs-lookup"><span data-stu-id="5e4de-163">You can also use AzCopy toocopy one file tooanother or toocopy a blob tooa file or vice versa.</span></span> <span data-ttu-id="5e4de-164">Zie [gegevensoverdracht met het AzCopy-opdrachtregelprogramma Hallo](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5e4de-164">See [Transfer data with hello AzCopy Command-Line Utility](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="5e4de-165">Als u een blob tooa-bestand of een bestand tooa blob kopieert, moet u een shared access signature (SAS) tooauthenticate Hallo bronobject, zelfs als u binnen Hallo dezelfde kopieert storage-account.</span><span class="sxs-lookup"><span data-stu-id="5e4de-165">If you are copying a blob tooa file, or a file tooa blob, you must use a shared access signature (SAS) tooauthenticate hello source object, even if you are copying within hello same storage account.</span></span>
> 
> 

<span data-ttu-id="5e4de-166">**Kopieer een bestand tooanother** hello volgende voorbeeld wordt een bestand tooanother in Hallo dezelfde share.</span><span class="sxs-lookup"><span data-stu-id="5e4de-166">**Copy a file tooanother file** hello following example copies a file tooanother file in hello same share.</span></span> <span data-ttu-id="5e4de-167">Omdat deze kopieerbewerking gekopieerd tussen de bestanden in hetzelfde opslagaccount Hallo, kunt u gedeelde sleutel verificatie tooperform Hallo kopiëren.</span><span class="sxs-lookup"><span data-stu-id="5e4de-167">Because this copy operation copies between files in hello same storage account, you can use Shared Key authentication tooperform hello copy.</span></span>

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Get a reference toohello root directory for hello share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference toohello directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that hello directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference toohello file we created previously.
        CloudFile sourceFile = sampleDir.GetFileReference("Log1.txt");

        // Ensure that hello source file exists.
        if (sourceFile.Exists())
        {
            // Get a reference toohello destination file.
            CloudFile destFile = sampleDir.GetFileReference("Log1Copy.txt");

            // Start hello copy operation.
            destFile.StartCopy(sourceFile);

            // Write hello contents of hello destination file toohello console window.
            Console.WriteLine(destFile.DownloadText());
        }
    }
}
```

<span data-ttu-id="5e4de-168">**Kopieer een bestand tooa blob** hello volgende voorbeeld wordt een bestand gemaakt en gekopieerd tooa blob in Hallo hetzelfde opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="5e4de-168">**Copy a file tooa blob** hello following example creates a file and copies it tooa blob within hello same storage account.</span></span> <span data-ttu-id="5e4de-169">Hallo-voorbeeld wordt een SAS voor bronbestand hello, welke service Hallo tooauthenticate toegang toohello bronbestand tijdens de kopieerbewerking Hallo gebruikt gemaakt.</span><span class="sxs-lookup"><span data-stu-id="5e4de-169">hello example creates a SAS for hello source file, which hello service uses tooauthenticate access toohello source file during hello copy operation.</span></span>

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Create a new file share, if it does not already exist.
CloudFileShare share = fileClient.GetShareReference("sample-share");
share.CreateIfNotExists();

// Create a new file in hello root directory.
CloudFile sourceFile = share.GetRootDirectoryReference().GetFileReference("sample-file.txt");
sourceFile.UploadText("A sample file in hello root directory.");

// Get a reference toohello blob toowhich hello file will be copied.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();
CloudBlockBlob destBlob = container.GetBlockBlobReference("sample-blob.txt");

// Create a SAS for hello file that's valid for 24 hours.
// Note that when you are copying a file tooa blob, or a blob tooa file, you must use a SAS
// tooauthenticate access toohello source object, even if you are copying within hello same
// storage account.
string fileSas = sourceFile.GetSharedAccessSignature(new SharedAccessFilePolicy()
{
    // Only read permissions are required for hello source file.
    Permissions = SharedAccessFilePermissions.Read,
    SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24)
});

// Construct hello URI toohello source file, including hello SAS token.
Uri fileSasUri = new Uri(sourceFile.StorageUri.PrimaryUri.ToString() + fileSas);

// Copy hello file toohello blob.
destBlob.StartCopy(fileSasUri);

// Write hello contents of hello file toohello console window.
Console.WriteLine("Source file contents: {0}", sourceFile.DownloadText());
Console.WriteLine("Destination blob contents: {0}", destBlob.DownloadText());
```

<span data-ttu-id="5e4de-170">U kunt een blob tooa-bestand kopiëren in Hallo dezelfde manier.</span><span class="sxs-lookup"><span data-stu-id="5e4de-170">You can copy a blob tooa file in hello same way.</span></span> <span data-ttu-id="5e4de-171">Als Hallo bronobject een blob is, maakt u een blob SAS tooauthenticate toegang toothat tijdens de kopieerbewerking Hallo.</span><span class="sxs-lookup"><span data-stu-id="5e4de-171">If hello source object is a blob, then create a SAS tooauthenticate access toothat blob during hello copy operation.</span></span>

## <a name="troubleshooting-azure-file-storage-using-metrics"></a><span data-ttu-id="5e4de-172">Problemen met Azure File Storage oplossen met metrische gegevens</span><span class="sxs-lookup"><span data-stu-id="5e4de-172">Troubleshooting Azure File storage using metrics</span></span>
<span data-ttu-id="5e4de-173">Azure Storage Analytics ondersteunt nu metrische gegevens voor Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="5e4de-173">Azure Storage Analytics now supports metrics for Azure File storage.</span></span> <span data-ttu-id="5e4de-174">Met metrische gegevens kunt u aanvragen volgen en problemen diagnosticeren.</span><span class="sxs-lookup"><span data-stu-id="5e4de-174">With metrics data, you can trace requests and diagnose issues.</span></span>


<span data-ttu-id="5e4de-175">U kunt metrische gegevens voor Azure File storage uit Hallo inschakelen [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5e4de-175">You can enable metrics for Azure File storage from hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="5e4de-176">U kunt ook de metrische gegevens via een programma door de aanroepende Hallo bewerking Set File Service Properties via Hallo REST-API of een van de analogen daarvan in Hallo Storage-clientbibliotheek inschakelen.</span><span class="sxs-lookup"><span data-stu-id="5e4de-176">You can also enable metrics programmatically by calling hello Set File Service Properties operation via hello REST API, or one of its analogues in hello Storage Client Library.</span></span>


<span data-ttu-id="5e4de-177">Hallo volgende codevoorbeeld toont hoe toouse Storage-clientbibliotheek voor .NET tooenable metrische gegevens voor Azure File storage Hallo.</span><span class="sxs-lookup"><span data-stu-id="5e4de-177">hello following code example shows how toouse hello Storage Client Library for .NET tooenable metrics for Azure File storage.</span></span>

<span data-ttu-id="5e4de-178">Voeg eerst de volgende Hallo `using` richtlijnen tooyour `Program.cs` bestand bovendien toothose die u hebt toegevoegd:</span><span class="sxs-lookup"><span data-stu-id="5e4de-178">First, add hello following `using` directives tooyour `Program.cs` file, in addition toothose you added above:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

<span data-ttu-id="5e4de-179">Denk eraan dat bij Azure Blobs, Azure Table en Azure wachtrijen Hallo gedeeld gebruiken `ServiceProperties` type in Hallo `Microsoft.WindowsAzure.Storage.Shared.Protocol` naamruimte, Azure File storage heeft een eigen type, hello `FileServiceProperties` type in Hallo `Microsoft.WindowsAzure.Storage.File.Protocol` naamruimte.</span><span class="sxs-lookup"><span data-stu-id="5e4de-179">Note that while Azure Blobs, Azure Table, and Azure Queues use hello shared `ServiceProperties` type in hello `Microsoft.WindowsAzure.Storage.Shared.Protocol` namespace, Azure File storage uses its own type, hello `FileServiceProperties` type in hello `Microsoft.WindowsAzure.Storage.File.Protocol` namespace.</span></span> <span data-ttu-id="5e4de-180">Beide naamruimten moet worden verwezen vanuit uw code echter voor Hallo code toocompile te volgen.</span><span class="sxs-lookup"><span data-stu-id="5e4de-180">Both namespaces must be referenced from your code, however, for hello following code toocompile.</span></span>

```csharp
// Parse your storage connection string from your application's configuration file.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));
// Create hello File service client.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Set metrics properties for File service.
// Note that hello File service currently uses its own service properties type,
// available in hello Microsoft.WindowsAzure.Storage.File.Protocol namespace.
fileClient.SetServiceProperties(new FileServiceProperties()
{
    // Set hour metrics
    HourMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 14,
        Version = "1.0"
    },
    // Set minute metrics
    MinuteMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 7,
        Version = "1.0"
    }
});

// Read hello metrics properties we just set.
FileServiceProperties serviceProperties = fileClient.GetServiceProperties();
Console.WriteLine("Hour metrics:");
Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
Console.WriteLine(serviceProperties.HourMetrics.Version);
Console.WriteLine();
Console.WriteLine("Minute metrics:");
Console.WriteLine(serviceProperties.MinuteMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.MinuteMetrics.RetentionDays);
Console.WriteLine(serviceProperties.MinuteMetrics.Version);
```

<span data-ttu-id="5e4de-181">Bovendien kunt u verwijzen te[Azure File storage probleemoplossing artikel](storage-troubleshoot-windows-file-connection-problems.md) voor richtlijnen voor probleemoplossing voor end-to-end.</span><span class="sxs-lookup"><span data-stu-id="5e4de-181">Also, you can refer too[Azure File storage Troubleshooting Article](storage-troubleshoot-windows-file-connection-problems.md) for end-to-end troubleshooting guidance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e4de-182">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5e4de-182">Next steps</span></span>
<span data-ttu-id="5e4de-183">Raadpleeg de volgende koppelingen voor meer informatie over Azure File Storage.</span><span class="sxs-lookup"><span data-stu-id="5e4de-183">See these links for more information about Azure File storage.</span></span>

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="5e4de-184">Conceptuele artikelen en video's</span><span class="sxs-lookup"><span data-stu-id="5e4de-184">Conceptual articles and videos</span></span>
* [<span data-ttu-id="5e4de-185">Azure File Storage: een naadloos SMB-bestandssysteem voor Windows en Linux</span><span class="sxs-lookup"><span data-stu-id="5e4de-185">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="5e4de-186">Hoe toouse Azure File storage met Linux</span><span class="sxs-lookup"><span data-stu-id="5e4de-186">How toouse Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a><span data-ttu-id="5e4de-187">Hulpprogramma-ondersteuning voor File Storage</span><span class="sxs-lookup"><span data-stu-id="5e4de-187">Tooling support for File storage</span></span>
* [<span data-ttu-id="5e4de-188">Hoe toouse AzCopy met Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5e4de-188">How toouse AzCopy with Microsoft Azure Storage</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="5e4de-189">Hello Azure CLI gebruiken met Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5e4de-189">Using hello Azure CLI with Azure Storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [<span data-ttu-id="5e4de-190">Problemen met betrekking tot Azure File Storage oplossen</span><span class="sxs-lookup"><span data-stu-id="5e4de-190">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a><span data-ttu-id="5e4de-191">Naslaginformatie</span><span class="sxs-lookup"><span data-stu-id="5e4de-191">Reference</span></span>
* [<span data-ttu-id="5e4de-192">Naslaginformatie over de Storage-clientbibliotheek voor .NET</span><span class="sxs-lookup"><span data-stu-id="5e4de-192">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="5e4de-193">Naslaginformatie over REST API voor bestandsservices</span><span class="sxs-lookup"><span data-stu-id="5e4de-193">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a><span data-ttu-id="5e4de-194">Blogberichten</span><span class="sxs-lookup"><span data-stu-id="5e4de-194">Blog posts</span></span>
* [<span data-ttu-id="5e4de-195">Azure File storage is now generally available (Azure File Storage is nu algemeen beschikbaar)</span><span class="sxs-lookup"><span data-stu-id="5e4de-195">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="5e4de-196">Inside Azure File Storage (Een kijkje achter de schermen van Azure File Storage)</span><span class="sxs-lookup"><span data-stu-id="5e4de-196">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="5e4de-197">Introducing Microsoft Azure File Service (Introductie van Microsoft Azure File-service)</span><span class="sxs-lookup"><span data-stu-id="5e4de-197">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="5e4de-198">Persistente verbindingen tooMicrosoft Azure File storage</span><span class="sxs-lookup"><span data-stu-id="5e4de-198">Persisting connections tooMicrosoft Azure File storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)
