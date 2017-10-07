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
# <a name="manage-expiration-of-azure-storage-blobs-in-azure-cdn"></a>Vervaldatum van Azure Storage-blobs in Azure CDN beheren
> [!div class="op_single_selector"]
> * [Azure-Web-Apps/Cloud Services, ASP.NET of IIS](cdn-manage-expiration-of-cloud-service-content.md)
> * [Azure blob Storage-service](cdn-manage-expiration-of-blob-content.md)
> 
> 

Hallo [blob-service](../storage/common/storage-introduction.md#blob-storage) in [Azure Storage](../storage/common/storage-introduction.md) is een van de verschillende Azure gebaseerde oorsprongen geïntegreerd met Azure CDN.  Kan een openbaar toegankelijke blob-inhoud in cache worden opgeslagen in Azure CDN totdat de time-to-live (TTL) is verstreken.  Hallo TTL, wordt bepaald door Hallo [ *Cache-Control* header](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9) in Azure Storage Hallo HTTP-antwoord.

> [!TIP]
> U kunt geen TTL voor een blob tooset.  In dit geval past Azure CDN automatisch een standaard-TTL van zeven dagen.
> 
> Zie voor meer informatie over de werking van Azure CDN op toospeed van tooblobs toegang en andere bestanden Hallo [overzicht van Azure CDN](cdn-overview.md).
> 
> Zie voor meer informatie over Azure Storage-blob-service Hallo [concepten van Blob-Service](https://msdn.microsoft.com/library/dd179376.aspx). 
> 
> 

Deze zelfstudie laat zien dat u Hallo TTL op een blob in Azure Storage instellen kunt op verschillende manieren.  

## <a name="azure-powershell"></a>Azure PowerShell
[Azure PowerShell](/powershell/azure/overview) is een van de Hallo snelste, meest krachtige manieren tooadminister uw Azure-services.  Gebruik Hallo `Get-AzureStorageBlob` cmdlet tooget een verwijzing toohello blob, stel Hallo `.ICloudBlob.Properties.CacheControl` eigenschap. 

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
> U kunt ook PowerShell te gebruiken[beheren van uw CDN-profielen en eindpunten](cdn-manage-powershell.md).
> 
> 

## <a name="azure-storage-client-library-for-net"></a>Azure Storage-clientbibliotheek voor .NET
een blob tooset de TTL met .NET, gebruik Hallo [Azure Storage-clientbibliotheek voor .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) tooset hello [CloudBlob.Properties.CacheControl](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.blob.blobproperties.cachecontrol.aspx) eigenschap.

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
> Er zijn veel meer .NET-codevoorbeelden beschikbaar in Hallo [voorbeelden van Azure Blob Storage voor .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/).
> 
> 

## <a name="other-methods"></a>Andere methoden
* [Azure-opdrachtregelinterface](../cli-install-nodejs.md)
  
    Tijdens het uploaden van blob Hallo Hallo ingesteld *cacheControl* eigenschap Hallo met `-p` overschakelen.  In het volgende voorbeeld wordt de Hallo TTL tooone uur (3600 seconden).
  
    ```text
    azure storage blob upload -c <connectionstring> -p cacheControl="public, max-age=3600" .\test.txt myContainer test.txt
    ```
* [REST-API voor Azure Storage-services](https://msdn.microsoft.com/library/azure/dd179355.aspx)
  
    Expliciet set Hallo *x-ms-blob-cache-control* -eigenschap op een [Blob plaatsen](https://msdn.microsoft.com/en-us/library/azure/dd179451.aspx), [blokkeringslijst plaatsen](https://msdn.microsoft.com/en-us/library/azure/dd179467.aspx), of [Blob-eigenschappen instellen](https://msdn.microsoft.com/library/azure/ee691966.aspx) aanvraag.
* Beheerhulpprogramma's voor opslag van derden
  
    Sommige hulpprogramma's van derden Azure Storage management kunnen u tooset hello *CacheControl* -eigenschap op blobs. 

## <a name="testing-hello-cache-control-header"></a>Test Hallo *Cache-Control* koptekst
U kunt eenvoudig hello TTL van uw blobs controleren.  Met behulp van uw browser [hulpprogramma's voor ontwikkelaars](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/), testen van uw blob inbegrip van Hallo *Cache-Control* antwoordheader.  U kunt ook een hulpprogramma zoals **wget**, [Postman](https://www.getpostman.com/), of [Fiddler](http://www.telerik.com/fiddler) tooexamine Hallo antwoordheaders.

## <a name="next-steps"></a>Volgende stappen
* [Meer informatie over Hallo *Cache-Control* koptekst](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.9)
* [Meer informatie over hoe toomanage verlooptijd van Cloudservice-inhoud in Azure CDN](cdn-manage-expiration-of-cloud-service-content.md)

