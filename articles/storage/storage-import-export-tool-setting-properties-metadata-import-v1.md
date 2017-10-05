---
title: Instellen van eigenschappen en metagegevens met behulp van Azure Import/Export - v1 | Microsoft Docs
description: Informatie over het opgeven van de eigenschappen en metagegevens worden ingesteld op de bestemming blobs bij het uitvoeren van de Azure-hulpprogramma voor importeren/exporteren voor het voorbereiden van uw schijven. Dit verwijst naar v1 van het hulpprogramma voor importeren/exporteren.
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
ms.openlocfilehash: 6455ce57572f9ec36d0ebae88c1ddd9f40f237bf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="setting-properties-and-metadata-during-the-import-process"></a><span data-ttu-id="7f6be-104">Eigenschappen en metagegevens instellen tijdens het importproces</span><span class="sxs-lookup"><span data-stu-id="7f6be-104">Setting properties and metadata during the import process</span></span>
<span data-ttu-id="7f6be-105">Wanneer u het hulpprogramma Microsoft Azure Import/Export voorbereiden van uw schijven uitvoert, kunt u eigenschappen en metagegevens worden ingesteld op de doel-blobs.</span><span class="sxs-lookup"><span data-stu-id="7f6be-105">When you run the Microsoft Azure Import/Export Tool to prepare your drives, you can specify properties and metadata to be set on the destination blobs.</span></span> <span data-ttu-id="7f6be-106">Volg deze stappen:</span><span class="sxs-lookup"><span data-stu-id="7f6be-106">Follow these steps:</span></span>  
  
1.  <span data-ttu-id="7f6be-107">Maak een tekstbestand op uw lokale computer waarmee u de namen en waarden blob eigenschappen ingesteld.</span><span class="sxs-lookup"><span data-stu-id="7f6be-107">To set blob properties, create a text file on your local computer that specifies property names and values.</span></span>  
  
2.  <span data-ttu-id="7f6be-108">Maak een tekstbestand op uw lokale computer waarmee metagegevens namen en waarden blobmetagegevens stelt.</span><span class="sxs-lookup"><span data-stu-id="7f6be-108">To set blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>  
  
3.  <span data-ttu-id="7f6be-109">Het volledige pad doorgeven aan een of beide van deze bestanden naar de Azure-hulpprogramma voor importeren/exporteren als onderdeel van de `PrepImport` bewerking.</span><span class="sxs-lookup"><span data-stu-id="7f6be-109">Pass the full path to one or both of these files to the Azure Import/Export Tool as part of the `PrepImport` operation.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="7f6be-110">Wanneer u een bestand eigenschappen of metagegevens als onderdeel van een sessie exemplaar opgeeft, worden deze eigenschappen of metagegevens zijn ingesteld voor elke blob die is geïmporteerd als onderdeel van die sessie kopiëren.</span><span class="sxs-lookup"><span data-stu-id="7f6be-110">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="7f6be-111">Als u opgeven van een andere set eigenschappen of metagegevens voor enkele van de blobs wordt geïmporteerd wilt, moet u een afzonderlijk exemplaar om sessie te maken met andere eigenschappen of bestanden met metagegevens.</span><span class="sxs-lookup"><span data-stu-id="7f6be-111">If you want to specify a different set of properties or metadata for some of the blobs being imported, you'll need to create a separate copy session with different properties or metadata files.</span></span>  
  
## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="7f6be-112">Blob-eigenschappen opgeven in een tekstbestand</span><span class="sxs-lookup"><span data-stu-id="7f6be-112">Specify Blob Properties in a Text File</span></span>  
<span data-ttu-id="7f6be-113">Blob als eigenschappen wilt opgeven, een lokaal tekstbestand maken en XML-bestand dat wordt opgegeven namen van eigenschappen als elementen en eigenschapswaarden als waarden bevatten.</span><span class="sxs-lookup"><span data-stu-id="7f6be-113">To specify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="7f6be-114">Hier volgt een voorbeeld waarin sommige eigenschapswaarden:</span><span class="sxs-lookup"><span data-stu-id="7f6be-114">Here's an example that specifies some property values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="7f6be-115">Sla het bestand op een lokale locatie zoals `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="7f6be-115">Save the file to a local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>  
  
## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="7f6be-116">Blobmetagegevens opgeven in een tekstbestand</span><span class="sxs-lookup"><span data-stu-id="7f6be-116">Specify Blob Metadata in a Text File</span></span>  
<span data-ttu-id="7f6be-117">Op dezelfde manier als wilt opgeven blobmetagegevens, maakt u een lokaal tekstbestand met namen van metagegevens als elementen en metagegevenswaarden als waarden.</span><span class="sxs-lookup"><span data-stu-id="7f6be-117">Similarly, to specify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="7f6be-118">Hier volgt een voorbeeld waarin enkele metagegevenswaarden:</span><span class="sxs-lookup"><span data-stu-id="7f6be-118">Here's an example that specifies some metadata values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="7f6be-119">Sla het bestand op een lokale locatie zoals `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="7f6be-119">Save the file to a local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>  
  
## <a name="create-a-copy-session-including-the-properties-or-metadata-files"></a><span data-ttu-id="7f6be-120">Een kopieersessie met inbegrip van de eigenschappen of bestanden met metagegevens maken</span><span class="sxs-lookup"><span data-stu-id="7f6be-120">Create a Copy Session Including the Properties or Metadata Files</span></span>  
<span data-ttu-id="7f6be-121">Wanneer u het hulpprogramma Azure Import/Export voorbereiden van de import-taak uitvoert, geeft u het eigenschappenbestand op de opdrachtregel met behulp van de `PropertyFile` parameter.</span><span class="sxs-lookup"><span data-stu-id="7f6be-121">When you run the Azure Import/Export Tool to prepare the import job, specify the properties file on the command line using the `PropertyFile` parameter.</span></span> <span data-ttu-id="7f6be-122">Geef het metagegevensbestand op de opdrachtregel met behulp van de `/MetadataFile` parameter.</span><span class="sxs-lookup"><span data-stu-id="7f6be-122">Specify the metadata file on the command line using the `/MetadataFile` parameter.</span></span> <span data-ttu-id="7f6be-123">Hier volgt een voorbeeld waarin beide bestanden:</span><span class="sxs-lookup"><span data-stu-id="7f6be-123">Here's an example that specifies both files:</span></span>  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a><span data-ttu-id="7f6be-124">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7f6be-124">Next steps</span></span>

* [<span data-ttu-id="7f6be-125">Bestandsindeling van het metagegevens- en eigenschappenbestand van de Import/Export-service</span><span class="sxs-lookup"><span data-stu-id="7f6be-125">Import/Export service metadata and properties file format</span></span>](storage-import-export-file-format-metadata-and-properties.md)
