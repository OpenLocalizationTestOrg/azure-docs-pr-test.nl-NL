---
title: Instellen van eigenschappen en metagegevens met behulp van Azure Import/Export | Microsoft Docs
description: Informatie over het opgeven van de eigenschappen en metagegevens worden ingesteld op de bestemming blobs bij het uitvoeren van de Azure-hulpprogramma voor importeren/exporteren voor het voorbereiden van uw schijven.
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
ms.openlocfilehash: 1ba6d157402fae0c7d7bf841d2b4e4f6b1ee1084
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="setting-properties-and-metadata-during-the-import-process"></a><span data-ttu-id="5a04c-103">Eigenschappen en metagegevens instellen tijdens het importproces</span><span class="sxs-lookup"><span data-stu-id="5a04c-103">Setting properties and metadata during the import process</span></span>

<span data-ttu-id="5a04c-104">Wanneer u het hulpprogramma Microsoft Azure Import/Export voorbereiden van uw schijven uitvoert, kunt u eigenschappen en metagegevens worden ingesteld op de doel-blobs.</span><span class="sxs-lookup"><span data-stu-id="5a04c-104">When you run the Microsoft Azure Import/Export Tool to prepare your drives, you can specify properties and metadata to be set on the destination blobs.</span></span> <span data-ttu-id="5a04c-105">Volg deze stappen:</span><span class="sxs-lookup"><span data-stu-id="5a04c-105">Follow these steps:</span></span>

1.  <span data-ttu-id="5a04c-106">Maak een tekstbestand op uw lokale computer waarmee u de namen en waarden blob eigenschappen ingesteld.</span><span class="sxs-lookup"><span data-stu-id="5a04c-106">To set blob properties, create a text file on your local computer that specifies property names and values.</span></span>
2.  <span data-ttu-id="5a04c-107">Maak een tekstbestand op uw lokale computer waarmee metagegevens namen en waarden blobmetagegevens stelt.</span><span class="sxs-lookup"><span data-stu-id="5a04c-107">To set blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>
3.  <span data-ttu-id="5a04c-108">Het volledige pad doorgeven aan een of beide van deze bestanden naar de Azure-hulpprogramma voor importeren/exporteren als onderdeel van de `PrepImport` bewerking.</span><span class="sxs-lookup"><span data-stu-id="5a04c-108">Pass the full path to one or both of these files to the Azure Import/Export Tool as part of the `PrepImport` operation.</span></span>

> [!NOTE]
>  <span data-ttu-id="5a04c-109">Wanneer u een bestand eigenschappen of metagegevens als onderdeel van een sessie exemplaar opgeeft, worden deze eigenschappen of metagegevens zijn ingesteld voor elke blob die is geïmporteerd als onderdeel van die sessie kopiëren.</span><span class="sxs-lookup"><span data-stu-id="5a04c-109">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="5a04c-110">Als u opgeven van een andere set eigenschappen of metagegevens voor enkele van de blobs wordt geïmporteerd wilt, moet u een afzonderlijk exemplaar om sessie te maken met andere eigenschappen of bestanden met metagegevens.</span><span class="sxs-lookup"><span data-stu-id="5a04c-110">If you want to specify a different set of properties or metadata for some of the blobs being imported, you'll need to create a separate copy session with different properties or metadata files.</span></span>

## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="5a04c-111">Blob-eigenschappen opgeven in een tekstbestand</span><span class="sxs-lookup"><span data-stu-id="5a04c-111">Specify blob properties in a text file</span></span>

<span data-ttu-id="5a04c-112">Blob als eigenschappen wilt opgeven, een lokaal tekstbestand maken en XML-bestand dat wordt opgegeven namen van eigenschappen als elementen en eigenschapswaarden als waarden bevatten.</span><span class="sxs-lookup"><span data-stu-id="5a04c-112">To specify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="5a04c-113">Hier volgt een voorbeeld waarin sommige eigenschapswaarden:</span><span class="sxs-lookup"><span data-stu-id="5a04c-113">Here's an example that specifies some property values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

<span data-ttu-id="5a04c-114">Sla het bestand op een lokale locatie zoals `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="5a04c-114">Save the file to a local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>

## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="5a04c-115">Blobmetagegevens opgeven in een tekstbestand</span><span class="sxs-lookup"><span data-stu-id="5a04c-115">Specify blob metadata in a text file</span></span>

<span data-ttu-id="5a04c-116">Op dezelfde manier als wilt opgeven blobmetagegevens, maakt u een lokaal tekstbestand met namen van metagegevens als elementen en metagegevenswaarden als waarden.</span><span class="sxs-lookup"><span data-stu-id="5a04c-116">Similarly, to specify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="5a04c-117">Hier volgt een voorbeeld waarin enkele metagegevenswaarden:</span><span class="sxs-lookup"><span data-stu-id="5a04c-117">Here's an example that specifies some metadata values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="5a04c-118">Sla het bestand op een lokale locatie zoals `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="5a04c-118">Save the file to a local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>

## <a name="add-the-path-to-properties-and-metadata-files-in-datasetcsv"></a><span data-ttu-id="5a04c-119">Het pad naar de eigenschappen en bestanden met metagegevens in dataset.csv toevoegen</span><span class="sxs-lookup"><span data-stu-id="5a04c-119">Add the path to properties and metadata files in dataset.csv</span></span>

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,https://mystorageaccount.blob.core.windows.net/video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,https://mystorageaccount.blob.core.windows.net/photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,https://mystorageaccount.blob.core.windows.net/music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

## <a name="next-steps"></a><span data-ttu-id="5a04c-120">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="5a04c-120">Next steps</span></span>

* [<span data-ttu-id="5a04c-121">Bestandsindeling van het metagegevens- en eigenschappenbestand van de Import/Export-service</span><span class="sxs-lookup"><span data-stu-id="5a04c-121">Import/Export service metadata and properties file format</span></span>](../storage-import-export-file-format-metadata-and-properties.md)
