---
title: Vervaldatum van Azure Storage-blobs in Azure CDN beheren | Microsoft Docs
description: Meer informatie over de opties voor het beheren van time to live voor blobs in Azure CDN opslaan in cache.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: ad4801e9-d09a-49bf-b35c-efdc4e6034e8
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: d4741921806e443d92c385a04b781cec296c2ae8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a><span data-ttu-id="cb729-103">Vervaldatum van Azure Storage-blobs in Azure CDN beheren</span><span class="sxs-lookup"><span data-stu-id="cb729-103">Manage expiration of Azure Storage blobs in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cb729-104">Azure-Web-Apps/Cloud Services, ASP.NET of IIS</span><span class="sxs-lookup"><span data-stu-id="cb729-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="cb729-105">Azure blob Storage-service</span><span class="sxs-lookup"><span data-stu-id="cb729-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="cb729-106">De [blob-service](../storage/common/storage-introduction.md#blob-storage) in [Azure Storage](../storage/common/storage-introduction.md) is een van de verschillende Azure gebaseerde oorsprongen geïntegreerd met Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="cb729-106">The [blob service](../storage/common/storage-introduction.md#blob-storage) in [Azure Storage](../storage/common/storage-introduction.md) is one of several Azure-based origins integrated with Azure CDN.</span></span>  <span data-ttu-id="cb729-107">Kan een openbaar toegankelijke blob-inhoud in cache worden opgeslagen in Azure CDN totdat de time-to-live (TTL) is verstreken.</span><span class="sxs-lookup"><span data-stu-id="cb729-107">Any publicly accessible blob content can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="cb729-108">De TTL-waarde wordt bepaald door de [ *Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in de HTTP-antwoord uit Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="cb729-108">The TTL is determined by the [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in the HTTP response from Azure Storage.</span></span>

> [!TIP]
> <span data-ttu-id="cb729-109">U kunt geen TTL instellen voor een blob.</span><span class="sxs-lookup"><span data-stu-id="cb729-109">You may choose to set no TTL on a blob.</span></span>  <span data-ttu-id="cb729-110">In dit geval past Azure CDN automatisch een standaard-TTL van zeven dagen.</span><span class="sxs-lookup"><span data-stu-id="cb729-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="cb729-111">Zie voor meer informatie over de werking van Azure CDN om sneller toegang tot blobs en andere bestanden de [overzicht van Azure CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cb729-111">For more information about how Azure CDN works to speed up access to blobs and other files, see the [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> <span data-ttu-id="cb729-112">Zie voor meer informatie over de Azure Storage-blob-service, [concepten van Blob-Service](https://msdn.microsoft.com/library/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb729-112">For more details on the Azure Storage blob service, see [Blob Service Concepts](https://msdn.microsoft.com/library/dd179376.aspx).</span></span> 
> 
> 

<span data-ttu-id="cb729-113">Deze zelfstudie laat zien dat verschillende manieren waarop u de TTL-waarde op een blob in Azure Storage instellen kunt.</span><span class="sxs-lookup"><span data-stu-id="cb729-113">This tutorial demonstrates several ways that you can set the TTL on a blob in Azure Storage.</span></span>  

## <a name="azure-powershell"></a><span data-ttu-id="cb729-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb729-114">Azure PowerShell</span></span>
<span data-ttu-id="cb729-115">[Azure PowerShell](/powershell/azure/overview) is een van de snelste, meest krachtige manieren voor het beheren van uw Azure-services.</span><span class="sxs-lookup"><span data-stu-id="cb729-115">[Azure PowerShell](/powershell/azure/overview) is one of the quickest, most powerful ways to administer your Azure services.</span></span>  <span data-ttu-id="cb729-116">Gebruik de `Get-AzureStorageBlob` cmdlet verwijst naar de blob, stel de `.ICloudBlob.Properties.CacheControl` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="cb729-116">Use the `Get-AzureStorageBlob` cmdlet to get a reference to the blob, then set the `.ICloudBlob.Properties.CacheControl` property.</span></span> 

```powershell
# Create a storage context
$context = New-AzureStorageContext -StorageAccountName "<storage account name>" -StorageAccountKey "<storage account key>"

# Get a reference to the blob
$blob = Get-AzureStorageBlob -Context $context -Container "<container name>" -Blob "<blob name>"

# Set the CacheControl property to expire in 1 hour (3600 seconds)
$blob.ICloudBlob.Properties.CacheControl = "public, max-age=3600"

# Send the update to the cloud
$blob.ICloudBlob.SetProperties()
```

> [!TIP]
> <span data-ttu-id="cb729-117">U kunt ook PowerShell om te gebruiken [beheren van uw CDN-profielen en eindpunten](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="cb729-117">You can also use PowerShell to [manage your CDN profiles and endpoints](cdn-manage-powershell.md).</span></span>
> 
> 

## <a name="azure-storage-client-library-for-net"></a><span data-ttu-id="cb729-118">Azure Storage-clientbibliotheek voor .NET</span><span class="sxs-lookup"><span data-stu-id="cb729-118">Azure Storage Client Library for .NET</span></span>
<span data-ttu-id="cb729-119">U stelt een blob-TTL met .NET met de [Azure Storage-clientbibliotheek voor .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) om in te stellen de [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) eigenschap.</span><span class="sxs-lookup"><span data-stu-id="cb729-119">To set a blob's TTL using .NET, use the [Azure Storage Client Library for .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) to set the [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) property.</span></span>

```csharp
class Program
{
    const string connectionString = "<storage connection string>";
    static void Main()
    {
        // Retrieve storage account information from connection string
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);

        // Create a blob client for interacting with the blob service.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Create a reference to the container
        CloudBlobContainer container = blobClient.GetContainerReference("<container name>");

        // Create a reference to the blob
        CloudBlob blob = container.GetBlobReference("<blob name>");

        // Set the CacheControl property to expire in 1 hour (3600 seconds)
        blob.Properties.CacheControl = "public, max-age=3600";

        // Update the blob's properties in the cloud
        blob.SetProperties();
    }
}
```

> [!TIP]
> <span data-ttu-id="cb729-120">Er zijn veel meer .NET-codevoorbeelden beschikbaar in de [voorbeelden van Azure Blob Storage voor .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="cb729-120">There are many more .NET code samples available in the [Azure Blob Storage Samples for .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span>
> 
> 

## <a name="other-methods"></a><span data-ttu-id="cb729-121">Andere methoden</span><span class="sxs-lookup"><span data-stu-id="cb729-121">Other methods</span></span>
* [<span data-ttu-id="cb729-122">Azure-opdrachtregelinterface</span><span class="sxs-lookup"><span data-stu-id="cb729-122">Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)
  
    <span data-ttu-id="cb729-123">Tijdens het uploaden van de blob, stel de *cacheControl* met behulp van de eigenschap de `-p` overschakelen.</span><span class="sxs-lookup"><span data-stu-id="cb729-123">When uploading the blob, set the *cacheControl* property using the `-p` switch.</span></span>  <span data-ttu-id="cb729-124">In het volgende voorbeeld wordt de TTL aan één uur (3600 seconden).</span><span class="sxs-lookup"><span data-stu-id="cb729-124">This example sets the TTL to one hour (3600 seconds).</span></span>
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [<span data-ttu-id="cb729-125">REST-API voor Azure Storage-services</span><span class="sxs-lookup"><span data-stu-id="cb729-125">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    <span data-ttu-id="cb729-126">Expliciet ingesteld de *x-ms-blob-cache-control* -eigenschap op een [Blob plaatsen](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [blokkeringslijst plaatsen](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), of [Blob-eigenschappen instellen](https://msdn.microsoft.com/library/azure/ee691966.aspx) aanvraag.</span><span class="sxs-lookup"><span data-stu-id="cb729-126">Explicitly set the *x-ms-blob-cache-control* property on a [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [Put Block List](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), or [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx) request.</span></span>
* <span data-ttu-id="cb729-127">Beheerhulpprogramma's voor opslag van derden</span><span class="sxs-lookup"><span data-stu-id="cb729-127">Third-party storage management tools</span></span>
  
    <span data-ttu-id="cb729-128">Sommige hulpprogramma's van derden Azure Storage management kunnen u instellen de *CacheControl* -eigenschap op blobs.</span><span class="sxs-lookup"><span data-stu-id="cb729-128">Some third-party Azure Storage management tools allow you to set the *CacheControl* property on blobs.</span></span> 

## <a name="testing-the-cache-control-header"></a><span data-ttu-id="cb729-129">Testen van de *Cache-Control* koptekst</span><span class="sxs-lookup"><span data-stu-id="cb729-129">Testing the *Cache-Control* header</span></span>
<span data-ttu-id="cb729-130">U kunt eenvoudig de TTL van uw blobs controleren.</span><span class="sxs-lookup"><span data-stu-id="cb729-130">You can easily verify the TTL of your blobs.</span></span>  <span data-ttu-id="cb729-131">Met behulp van uw browser [hulpprogramma's voor ontwikkelaars](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), test die uw blob is inclusief de *Cache-Control* antwoordheader.</span><span class="sxs-lookup"><span data-stu-id="cb729-131">Using your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), test that your blob is including the *Cache-Control* response header.</span></span>  <span data-ttu-id="cb729-132">U kunt ook een hulpprogramma zoals **wget**, [Postman](https://www.getpostman.com/), of [Fiddler](http://www.telerik.com/fiddler) om te onderzoeken de antwoordheaders.</span><span class="sxs-lookup"><span data-stu-id="cb729-132">You can also use a tool like **wget**, [Postman](https://www.getpostman.com/), or [Fiddler](http://www.telerik.com/fiddler) to examine the response headers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb729-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="cb729-133">Next Steps</span></span>
* [<span data-ttu-id="cb729-134">Meer informatie over de *Cache-Control* koptekst</span><span class="sxs-lookup"><span data-stu-id="cb729-134">Read about the *Cache-Control* header</span></span>](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [<span data-ttu-id="cb729-135">Informatie over het beheren van de verlooptijd van Cloudservice-inhoud in Azure CDN</span><span class="sxs-lookup"><span data-stu-id="cb729-135">Learn how to manage expiration of Cloud Service content in Azure CDN</span></span>](cdn-manage-expiration-of-cloud-service-content.md)

