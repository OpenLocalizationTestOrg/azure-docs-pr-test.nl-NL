---
title: aaaSetting eigenschappen en metagegevens met behulp van Azure Import/Export - v1 | Microsoft Docs
description: Meer informatie over hoe de eigenschappen en metagegevens toobe toospecify ingesteld op Hallo bestemming blobs wanneer uitgevoerd hello Azure-hulpprogramma voor importeren/exporteren tooprepare uw schijven. Dit verwijst toov1 Hallo hulpprogramma voor importeren/exporteren.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: e8541695-bcfb-4bf0-84d9-72c9de32a0a8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 5b7b1c346ecde8a26d985bd5de7efcf7d86eb9e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a><span data-ttu-id="e3979-104">Instellen van eigenschappen en metagegevens tijdens Hallo importeren</span><span class="sxs-lookup"><span data-stu-id="e3979-104">Setting properties and metadata during hello import process</span></span>
<span data-ttu-id="e3979-105">Wanneer u op uw stations Hallo Microsoft Azure-hulpprogramma voor importeren/exporteren tooprepare uitvoert, kunt u eigenschappen en metagegevens toobe ingesteld op Hallo bestemming blobs.</span><span class="sxs-lookup"><span data-stu-id="e3979-105">When you run hello Microsoft Azure Import/Export Tool tooprepare your drives, you can specify properties and metadata toobe set on hello destination blobs.</span></span> <span data-ttu-id="e3979-106">Volg deze stappen:</span><span class="sxs-lookup"><span data-stu-id="e3979-106">Follow these steps:</span></span>  
  
1.  <span data-ttu-id="e3979-107">Eigenschappen van de blob tooset, maak een tekstbestand op uw lokale computer waarmee u de namen en waarden.</span><span class="sxs-lookup"><span data-stu-id="e3979-107">tooset blob properties, create a text file on your local computer that specifies property names and values.</span></span>  
  
2.  <span data-ttu-id="e3979-108">tooset blob-metagegevens, maak een tekstbestand op uw lokale computer waarmee metagegevens namen en waarden.</span><span class="sxs-lookup"><span data-stu-id="e3979-108">tooset blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>  
  
3.  <span data-ttu-id="e3979-109">Hallo volledig pad tooone of beide van deze bestanden toohello Azure-hulpprogramma voor importeren/exporteren doorgeven als onderdeel van Hallo `PrepImport` bewerking.</span><span class="sxs-lookup"><span data-stu-id="e3979-109">Pass hello full path tooone or both of these files toohello Azure Import/Export Tool as part of hello `PrepImport` operation.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="e3979-110">Wanneer u een bestand eigenschappen of metagegevens als onderdeel van een sessie exemplaar opgeeft, worden deze eigenschappen of metagegevens zijn ingesteld voor elke blob die is geïmporteerd als onderdeel van die sessie kopiëren.</span><span class="sxs-lookup"><span data-stu-id="e3979-110">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="e3979-111">Als u een andere set eigenschappen of metagegevens toospecify voor een aantal Hallo BLOB's worden geïmporteerd wilt, moet u een afzonderlijke kopiëren een sessie met andere eigenschappen of bestanden met metagegevens toocreate.</span><span class="sxs-lookup"><span data-stu-id="e3979-111">If you want toospecify a different set of properties or metadata for some of hello blobs being imported, you'll need toocreate a separate copy session with different properties or metadata files.</span></span>  
  
## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="e3979-112">Blob-eigenschappen opgeven in een tekstbestand</span><span class="sxs-lookup"><span data-stu-id="e3979-112">Specify Blob Properties in a Text File</span></span>  
<span data-ttu-id="e3979-113">Eigenschappen van de blob toospecify, een lokaal tekstbestand maken en XML waarmee de namen van eigenschappen als elementen en eigenschapswaarden als waarden bevatten.</span><span class="sxs-lookup"><span data-stu-id="e3979-113">toospecify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="e3979-114">Hier volgt een voorbeeld waarin sommige eigenschapswaarden:</span><span class="sxs-lookup"><span data-stu-id="e3979-114">Here's an example that specifies some property values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="e3979-115">Hallo tooa lokale bestandslocatie zoals opslaan `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="e3979-115">Save hello file tooa local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>  
  
## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="e3979-116">Blobmetagegevens opgeven in een tekstbestand</span><span class="sxs-lookup"><span data-stu-id="e3979-116">Specify Blob Metadata in a Text File</span></span>  
<span data-ttu-id="e3979-117">Op deze manier toospecify blob-metagegevens, maakt u een lokaal tekstbestand met namen van metagegevens als elementen en metagegevenswaarden als waarden.</span><span class="sxs-lookup"><span data-stu-id="e3979-117">Similarly, toospecify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="e3979-118">Hier volgt een voorbeeld waarin enkele metagegevenswaarden:</span><span class="sxs-lookup"><span data-stu-id="e3979-118">Here's an example that specifies some metadata values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="e3979-119">Hallo tooa lokale bestandslocatie zoals opslaan `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="e3979-119">Save hello file tooa local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>  
  
## <a name="create-a-copy-session-including-hello-properties-or-metadata-files"></a><span data-ttu-id="e3979-120">Een kopie sessie inclusief Hallo eigenschappen of bestanden met metagegevens maken</span><span class="sxs-lookup"><span data-stu-id="e3979-120">Create a Copy Session Including hello Properties or Metadata Files</span></span>  
<span data-ttu-id="e3979-121">Wanneer u hello Azure-hulpprogramma voor importeren/exporteren tooprepare Hallo import-taak uitvoert, geef Hallo eigenschappenbestand op Hallo-opdrachtregel met behulp van Hallo `PropertyFile` parameter.</span><span class="sxs-lookup"><span data-stu-id="e3979-121">When you run hello Azure Import/Export Tool tooprepare hello import job, specify hello properties file on hello command line using hello `PropertyFile` parameter.</span></span> <span data-ttu-id="e3979-122">Geef Hallo metagegevensbestand op Hallo-opdrachtregel met behulp van Hallo `/MetadataFile` parameter.</span><span class="sxs-lookup"><span data-stu-id="e3979-122">Specify hello metadata file on hello command line using hello `/MetadataFile` parameter.</span></span> <span data-ttu-id="e3979-123">Hier volgt een voorbeeld waarin beide bestanden:</span><span class="sxs-lookup"><span data-stu-id="e3979-123">Here's an example that specifies both files:</span></span>  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a><span data-ttu-id="e3979-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="e3979-124">Next steps</span></span>

* [<span data-ttu-id="e3979-125">Bestandsindeling van het metagegevens- en eigenschappenbestand van de Import/Export-service</span><span class="sxs-lookup"><span data-stu-id="e3979-125">Import/Export service metadata and properties file format</span></span>](../storage-import-export-file-format-metadata-and-properties.md)
