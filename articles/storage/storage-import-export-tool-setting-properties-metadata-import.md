---
title: aaaSetting eigenschappen en metagegevens met behulp van Azure Import/Export | Microsoft Docs
description: Meer informatie over hoe de eigenschappen en metagegevens toobe toospecify ingesteld op Hallo bestemming blobs wanneer uitgevoerd hello Azure-hulpprogramma voor importeren/exporteren tooprepare uw schijven.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 05c2b13bead793c8ab5aac6ce25816be97fffb14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a><span data-ttu-id="4dae3-103">Instellen van eigenschappen en metagegevens tijdens Hallo importeren</span><span class="sxs-lookup"><span data-stu-id="4dae3-103">Setting properties and metadata during hello import process</span></span>

<span data-ttu-id="4dae3-104">Wanneer u op uw stations Hallo Microsoft Azure-hulpprogramma voor importeren/exporteren tooprepare uitvoert, kunt u eigenschappen en metagegevens toobe ingesteld op Hallo bestemming blobs.</span><span class="sxs-lookup"><span data-stu-id="4dae3-104">When you run hello Microsoft Azure Import/Export Tool tooprepare your drives, you can specify properties and metadata toobe set on hello destination blobs.</span></span> <span data-ttu-id="4dae3-105">Volg deze stappen:</span><span class="sxs-lookup"><span data-stu-id="4dae3-105">Follow these steps:</span></span>

1.  <span data-ttu-id="4dae3-106">Eigenschappen van de blob tooset, maak een tekstbestand op uw lokale computer waarmee u de namen en waarden.</span><span class="sxs-lookup"><span data-stu-id="4dae3-106">tooset blob properties, create a text file on your local computer that specifies property names and values.</span></span>
2.  <span data-ttu-id="4dae3-107">tooset blob-metagegevens, maak een tekstbestand op uw lokale computer waarmee metagegevens namen en waarden.</span><span class="sxs-lookup"><span data-stu-id="4dae3-107">tooset blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>
3.  <span data-ttu-id="4dae3-108">Hallo volledig pad tooone of beide van deze bestanden toohello Azure-hulpprogramma voor importeren/exporteren doorgeven als onderdeel van Hallo `PrepImport` bewerking.</span><span class="sxs-lookup"><span data-stu-id="4dae3-108">Pass hello full path tooone or both of these files toohello Azure Import/Export Tool as part of hello `PrepImport` operation.</span></span>

> [!NOTE]
>  <span data-ttu-id="4dae3-109">Wanneer u een bestand eigenschappen of metagegevens als onderdeel van een sessie exemplaar opgeeft, worden deze eigenschappen of metagegevens zijn ingesteld voor elke blob die is geïmporteerd als onderdeel van die sessie kopiëren.</span><span class="sxs-lookup"><span data-stu-id="4dae3-109">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="4dae3-110">Als u een andere set eigenschappen of metagegevens toospecify voor een aantal Hallo BLOB's worden geïmporteerd wilt, moet u een afzonderlijke kopiëren een sessie met andere eigenschappen of bestanden met metagegevens toocreate.</span><span class="sxs-lookup"><span data-stu-id="4dae3-110">If you want toospecify a different set of properties or metadata for some of hello blobs being imported, you'll need toocreate a separate copy session with different properties or metadata files.</span></span>

## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="4dae3-111">Blob-eigenschappen opgeven in een tekstbestand</span><span class="sxs-lookup"><span data-stu-id="4dae3-111">Specify blob properties in a text file</span></span>

<span data-ttu-id="4dae3-112">Eigenschappen van de blob toospecify, een lokaal tekstbestand maken en XML waarmee de namen van eigenschappen als elementen en eigenschapswaarden als waarden bevatten.</span><span class="sxs-lookup"><span data-stu-id="4dae3-112">toospecify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="4dae3-113">Hier volgt een voorbeeld waarin sommige eigenschapswaarden:</span><span class="sxs-lookup"><span data-stu-id="4dae3-113">Here's an example that specifies some property values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

<span data-ttu-id="4dae3-114">Hallo tooa lokale bestandslocatie zoals opslaan `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="4dae3-114">Save hello file tooa local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>

## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="4dae3-115">Blobmetagegevens opgeven in een tekstbestand</span><span class="sxs-lookup"><span data-stu-id="4dae3-115">Specify blob metadata in a text file</span></span>

<span data-ttu-id="4dae3-116">Op deze manier toospecify blob-metagegevens, maakt u een lokaal tekstbestand met namen van metagegevens als elementen en metagegevenswaarden als waarden.</span><span class="sxs-lookup"><span data-stu-id="4dae3-116">Similarly, toospecify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="4dae3-117">Hier volgt een voorbeeld waarin enkele metagegevenswaarden:</span><span class="sxs-lookup"><span data-stu-id="4dae3-117">Here's an example that specifies some metadata values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="4dae3-118">Hallo tooa lokale bestandslocatie zoals opslaan `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="4dae3-118">Save hello file tooa local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>

## <a name="add-hello-path-tooproperties-and-metadata-files-in-datasetcsv"></a><span data-ttu-id="4dae3-119">Hallo pad tooproperties en metagegevens van de bestanden in dataset.csv toevoegen</span><span class="sxs-lookup"><span data-stu-id="4dae3-119">Add hello path tooproperties and metadata files in dataset.csv</span></span>

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,https://mystorageaccount.blob.core.windows.net/video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,https://mystorageaccount.blob.core.windows.net/photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,https://mystorageaccount.blob.core.windows.net/music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

## <a name="next-steps"></a><span data-ttu-id="4dae3-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="4dae3-120">Next steps</span></span>

* [<span data-ttu-id="4dae3-121">Bestandsindeling van het metagegevens- en eigenschappenbestand van de Import/Export-service</span><span class="sxs-lookup"><span data-stu-id="4dae3-121">Import/Export service metadata and properties file format</span></span>](storage-import-export-file-format-metadata-and-properties.md)
