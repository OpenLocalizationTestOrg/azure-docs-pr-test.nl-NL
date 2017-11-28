---
title: aaaManage vervaldatum van Azure Storage-blobs in Azure CDN | Microsoft Docs
description: Meer informatie over het Hallo-opties voor het beheren van de time-to-live voor blobs in Azure CDN opslaan in cache.
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
ms.openlocfilehash: 9fecae9639deb28977da7f851e1da4a823ddc4e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a><span data-ttu-id="c3a8a-103">Vervaldatum van Azure Storage-blobs in Azure CDN beheren</span><span class="sxs-lookup"><span data-stu-id="c3a8a-103">Manage expiration of Azure Storage blobs in Azure CDN</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c3a8a-104">Azure-Web-Apps/Cloud Services, ASP.NET of IIS</span><span class="sxs-lookup"><span data-stu-id="c3a8a-104">Azure Web Apps/Cloud Services, ASP.NET, or IIS</span></span>](cdn-manage-expiration-of-cloud-service-content.md)
> * [<span data-ttu-id="c3a8a-105">Azure blob Storage-service</span><span class="sxs-lookup"><span data-stu-id="c3a8a-105">Azure Storage blob service</span></span>](cdn-manage-expiration-of-blob-content.md)
> 
> 

<span data-ttu-id="c3a8a-106">Hallo [blob-service](../storage/common/storage-introduction.md#blob-storage) in [Azure Storage](../storage/common/storage-introduction.md) is een van de verschillende Azure gebaseerde oorsprongen geïntegreerd met Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="c3a8a-106">hello [blob service](../storage/common/storage-introduction.md#blob-storage) in [Azure Storage](../storage/common/storage-introduction.md) is one of several Azure-based origins integrated with Azure CDN.</span></span>  <span data-ttu-id="c3a8a-107">Kan een openbaar toegankelijke blob-inhoud in cache worden opgeslagen in Azure CDN totdat de time-to-live (TTL) is verstreken.</span><span class="sxs-lookup"><span data-stu-id="c3a8a-107">Any publicly accessible blob content can be cached in Azure CDN until its time-to-live (TTL) elapses.</span></span>  <span data-ttu-id="c3a8a-108">Hallo TTL, wordt bepaald door Hallo [ *Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in Azure Storage Hallo HTTP-antwoord.</span><span class="sxs-lookup"><span data-stu-id="c3a8a-108">hello TTL is determined by hello [*Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in hello HTTP response from Azure Storage.</span></span>

> [!TIP]
> <span data-ttu-id="c3a8a-109">U kunt geen TTL voor een blob tooset.</span><span class="sxs-lookup"><span data-stu-id="c3a8a-109">You may choose tooset no TTL on a blob.</span></span>  <span data-ttu-id="c3a8a-110">In dit geval past Azure CDN automatisch een standaard-TTL van zeven dagen.</span><span class="sxs-lookup"><span data-stu-id="c3a8a-110">In this case, Azure CDN automatically applies a default TTL of seven days.</span></span>
> 
> <span data-ttu-id="c3a8a-111">Zie voor meer informatie over de werking van Azure CDN op toospeed van tooblobs toegang en andere bestanden Hallo [overzicht van Azure CDN](cdn-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c3a8a-111">For more information about how Azure CDN works toospeed up access tooblobs and other files, see hello [Azure CDN Overview](cdn-overview.md).</span></span>
> 
> <span data-ttu-id="c3a8a-112">Zie voor meer informatie over Azure Storage-blob-service Hallo [concepten van Blob-Service](https://msdn.microsoft.com/library/dd179376.aspx).</span><span class="sxs-lookup"><span data-stu-id="c3a8a-112">For more details on hello Azure Storage blob service, see [Blob Service Concepts](https://msdn.microsoft.com/library/dd179376.aspx).</span></span> 
> 
> 

<span data-ttu-id="c3a8a-113">Deze zelfstudie laat zien dat u Hallo TTL op een blob in Azure Storage instellen kunt op verschillende manieren.</span><span class="sxs-lookup"><span data-stu-id="c3a8a-113">This tutorial demonstrates several ways that you can set hello TTL on a blob in Azure Storage.</span></span>  

## <a name="azure-powershell"></a><span data-ttu-id="c3a8a-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c3a8a-114">Azure PowerShell</span></span>
<span data-ttu-id="c3a8a-115">[Azure PowerShell](/powershell/azure/overview) is een van de Hallo snelste, meest krachtige manieren tooadminister uw Azure-services.</span><span class="sxs-lookup"><span data-stu-id="c3a8a-115">[Azure PowerShell](/powershell/azure/overview) is one of hello quickest, most powerful ways tooadminister your Azure services.</span></span>  <span data-ttu-id="c3a8a-116">Gebruik Hallo `Get-AzureStorageBlob` cmdlet tooget een verwijzing toohello blob, stel Hallo `.ICloudBlob.Properties.CacheControl` eigenschap.</span><span class="sxs-lookup"><span data-stu-id="c3a8a-116">Use hello `Get-AzureStorageBlob` cmdlet tooget a reference toohello blob, then set hello `.ICloudBlob.Properties.CacheControl` property.</span></span> 

```powershell
# Create a storage context
$context = New-AzureStorageContext -StorageAccountName "<storage account name>" -StorageAccountKey "<storage account key>"

# Get a reference toohello blob
$blob = Get-AzureStorageBlob -Context $context -Container "<container name>" -Blob "<blob name>"

# Set hello CacheControl property tooexpire in 1 hour (3600 seconds)
$blob.ICloudBlob.Properties.CacheControl = "public, max-age=3600"

# Send hello update toohello cloud
$blob.ICloudBlob.SetProperties()
```

> [!TIP]
> <span data-ttu-id="c3a8a-117">U kunt ook PowerShell te gebruiken[beheren van uw CDN-profielen en eindpunten](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="c3a8a-117">You can also use PowerShell too[manage your CDN profiles and endpoints](cdn-manage-powershell.md).</span></span>
> 
> 

## <a name="azure-storage-client-library-for-net"></a><span data-ttu-id="c3a8a-118">Azure Storage-clientbibliotheek voor .NET</span><span class="sxs-lookup"><span data-stu-id="c3a8a-118">Azure Storage Client Library for .NET</span></span>
<span data-ttu-id="c3a8a-119">een blob tooset de TTL met .NET, gebruik Hallo [Azure Storage-clientbibliotheek voor .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) eigenschap.</span><span class="sxs-lookup"><span data-stu-id="c3a8a-119">tooset a blob's TTL using .NET, use hello [Azure Storage Client Library for .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) property.</span></span>

```csharp
class Program
{
    const string connectionString = "<storage connection string>";
    static void Main()
    {
        // Retrieve storage account information from connection string
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);

        // Create a blob client for interacting with hello blob service.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

        // Create a reference toohello container
        CloudBlobContainer container = blobClient.GetContainerReference("<container name>");

        // Create a reference toohello blob
        CloudBlob blob = container.GetBlobReference("<blob name>");

        // Set hello CacheControl property tooexpire in 1 hour (3600 seconds)
        blob.Properties.CacheControl = "public, max-age=3600";

        // Update hello blob's properties in hello cloud
        blob.SetProperties();
    }
}
```

> [!TIP]
> <span data-ttu-id="c3a8a-120">Er zijn veel meer .NET-codevoorbeelden beschikbaar in Hallo [voorbeelden van Azure Blob Storage voor .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="c3a8a-120">There are many more .NET code samples available in hello [Azure Blob Storage Samples for .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).</span></span>
> 
> 

## <a name="other-methods"></a><span data-ttu-id="c3a8a-121">Andere methoden</span><span class="sxs-lookup"><span data-stu-id="c3a8a-121">Other methods</span></span>
* [<span data-ttu-id="c3a8a-122">Azure-opdrachtregelinterface</span><span class="sxs-lookup"><span data-stu-id="c3a8a-122">Azure Command-Line Interface</span></span>](../cli-install-nodejs.md)
  
    <span data-ttu-id="c3a8a-123">Tijdens het uploaden van blob Hallo Hallo ingesteld *cacheControl* eigenschap Hallo met `-p` overschakelen.</span><span class="sxs-lookup"><span data-stu-id="c3a8a-123">When uploading hello blob, set hello *cacheControl* property using hello `-p` switch.</span></span>  <span data-ttu-id="c3a8a-124">In het volgende voorbeeld wordt de Hallo TTL tooone uur (3600 seconden).</span><span class="sxs-lookup"><span data-stu-id="c3a8a-124">This example sets hello TTL tooone hour (3600 seconds).</span></span>
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [<span data-ttu-id="c3a8a-125">REST-API voor Azure Storage-services</span><span class="sxs-lookup"><span data-stu-id="c3a8a-125">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    <span data-ttu-id="c3a8a-126">Expliciet set Hallo *x-ms-blob-cache-control* -eigenschap op een [Blob plaatsen](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [blokkeringslijst plaatsen](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), of [Blob-eigenschappen instellen](https://msdn.microsoft.com/library/azure/ee691966.aspx) aanvraag.</span><span class="sxs-lookup"><span data-stu-id="c3a8a-126">Explicitly set hello *x-ms-blob-cache-control* property on a [Put Blob](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [Put Block List](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), or [Set Blob Properties](https://msdn.microsoft.com/library/azure/ee691966.aspx) request.</span></span>
* <span data-ttu-id="c3a8a-127">Beheerhulpprogramma's voor opslag van derden</span><span class="sxs-lookup"><span data-stu-id="c3a8a-127">Third-party storage management tools</span></span>
  
    <span data-ttu-id="c3a8a-128">Sommige hulpprogramma's van derden Azure Storage management kunnen u tooset hello *CacheControl* -eigenschap op blobs.</span><span class="sxs-lookup"><span data-stu-id="c3a8a-128">Some third-party Azure Storage management tools allow you tooset hello *CacheControl* property on blobs.</span></span> 

## <a name="testing-hello-cache-control-header"></a><span data-ttu-id="c3a8a-129">Test Hallo *Cache-Control* koptekst</span><span class="sxs-lookup"><span data-stu-id="c3a8a-129">Testing hello *Cache-Control* header</span></span>
<span data-ttu-id="c3a8a-130">U kunt eenvoudig hello TTL van uw blobs controleren.</span><span class="sxs-lookup"><span data-stu-id="c3a8a-130">You can easily verify hello TTL of your blobs.</span></span>  <span data-ttu-id="c3a8a-131">Met behulp van uw browser [hulpprogramma's voor ontwikkelaars](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), testen van uw blob inbegrip van Hallo *Cache-Control* antwoordheader.</span><span class="sxs-lookup"><span data-stu-id="c3a8a-131">Using your browser's [developer tools](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), test that your blob is including hello *Cache-Control* response header.</span></span>  <span data-ttu-id="c3a8a-132">U kunt ook een hulpprogramma zoals **wget**, [Postman](https://www.getpostman.com/), of [Fiddler](http://www.telerik.com/fiddler) tooexamine Hallo antwoordheaders.</span><span class="sxs-lookup"><span data-stu-id="c3a8a-132">You can also use a tool like **wget**, [Postman](https://www.getpostman.com/), or [Fiddler](http://www.telerik.com/fiddler) tooexamine hello response headers.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3a8a-133">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="c3a8a-133">Next Steps</span></span>
* [<span data-ttu-id="c3a8a-134">Meer informatie over Hallo *Cache-Control* koptekst</span><span class="sxs-lookup"><span data-stu-id="c3a8a-134">Read about hello *Cache-Control* header</span></span>](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [<span data-ttu-id="c3a8a-135">Meer informatie over hoe toomanage verlooptijd van Cloudservice-inhoud in Azure CDN</span><span class="sxs-lookup"><span data-stu-id="c3a8a-135">Learn how toomanage expiration of Cloud Service content in Azure CDN</span></span>](cdn-manage-expiration-of-cloud-service-content.md)

