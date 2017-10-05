---
title: Azure Import/Export metagegevens en eigenschappen bestandsindeling | Microsoft Docs
description: Informatie over het opgeven van metagegevens en eigenschappen voor een of meer blobs die deel uitmaken van een importeren of exporteren van de taak.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 840364c6-d9a8-4b43-a9f3-f7441c625069
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 3f728ad94cdcbd32092b677f11a737ae91376720
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a><span data-ttu-id="b59ff-103">Azure Import/Export-service metagegevens en eigenschappen bestandsindeling</span><span class="sxs-lookup"><span data-stu-id="b59ff-103">Azure Import/Export service metadata and properties file format</span></span>
<span data-ttu-id="b59ff-104">U kunt de eigenschappen voor een of meer blobs en metagegevens als onderdeel van een import-taak of een taak voor exporteren opgeven.</span><span class="sxs-lookup"><span data-stu-id="b59ff-104">You can specify metadata and properties for one or more blobs as part of an import job or an export job.</span></span> <span data-ttu-id="b59ff-105">Metagegevens of eigenschappen voor BLOB's worden gemaakt als onderdeel van een import-taak, stelt opgeven u een bestand eigenschappen of metagegevens op de harde schijf met de gegevens moeten worden geïmporteerd.</span><span class="sxs-lookup"><span data-stu-id="b59ff-105">To set metadata or properties for blobs being created as part of an import job, you provide a metadata or properties file on the hard drive containing the data to be imported.</span></span> <span data-ttu-id="b59ff-106">Voor een exporttaak worden metagegevens en eigenschappen geschreven naar een bestand eigenschappen of metagegevens die is opgenomen op de harde schijf die aan u worden geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="b59ff-106">For an export job, metadata and properties are written to a metadata or properties file that is included on the hard drive returned to you.</span></span>  
  
## <a name="metadata-file-format"></a><span data-ttu-id="b59ff-107">Bestandsindeling voor metagegevens</span><span class="sxs-lookup"><span data-stu-id="b59ff-107">Metadata file format</span></span>  
<span data-ttu-id="b59ff-108">De indeling van een bestand met metagegevens is als volgt:</span><span class="sxs-lookup"><span data-stu-id="b59ff-108">The format of a metadata file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|<span data-ttu-id="b59ff-109">XML-Element</span><span class="sxs-lookup"><span data-stu-id="b59ff-109">XML Element</span></span>|<span data-ttu-id="b59ff-110">Type</span><span class="sxs-lookup"><span data-stu-id="b59ff-110">Type</span></span>|<span data-ttu-id="b59ff-111">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b59ff-111">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Metadata`|<span data-ttu-id="b59ff-112">Hoofdelement</span><span class="sxs-lookup"><span data-stu-id="b59ff-112">Root element</span></span>|<span data-ttu-id="b59ff-113">Het hoofdelement van het bestand met metagegevens.</span><span class="sxs-lookup"><span data-stu-id="b59ff-113">The root element of the metadata file.</span></span>|  
|`metadata-name`|<span data-ttu-id="b59ff-114">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b59ff-114">String</span></span>|<span data-ttu-id="b59ff-115">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="b59ff-115">Optional.</span></span> <span data-ttu-id="b59ff-116">Het XML-element bevat de naam van de metagegevens voor de blob en de waarde geeft de waarde van de instelling voor metagegevens.</span><span class="sxs-lookup"><span data-stu-id="b59ff-116">The XML element specifies the name of the metadata for the blob, and its value specifies the value of the metadata setting.</span></span>|  
  
## <a name="properties-file-format"></a><span data-ttu-id="b59ff-117">Eigenschappen-bestandsindeling</span><span class="sxs-lookup"><span data-stu-id="b59ff-117">Properties file format</span></span>  
<span data-ttu-id="b59ff-118">De indeling van een eigenschappenbestand is als volgt:</span><span class="sxs-lookup"><span data-stu-id="b59ff-118">The format of a properties file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
[<Last-Modified>date-time-value</Last-Modified>]  
[<Etag>etag</Etag>]  
[<Content-Length>size-in-bytes<Content-Length>]  
[<Content-Type>content-type</Content-Type>]  
[<Content-MD5>content-md5</Content-MD5>]  
[<Content-Encoding>content-encoding</Content-Encoding>]  
[<Content-Language>content-language</Content-Language>]  
[<Cache-Control>cache-control</Cache-Control>]  
</Properties>  
```
  
|<span data-ttu-id="b59ff-119">XML-Element</span><span class="sxs-lookup"><span data-stu-id="b59ff-119">XML Element</span></span>|<span data-ttu-id="b59ff-120">Type</span><span class="sxs-lookup"><span data-stu-id="b59ff-120">Type</span></span>|<span data-ttu-id="b59ff-121">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="b59ff-121">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Properties`|<span data-ttu-id="b59ff-122">Hoofdelement</span><span class="sxs-lookup"><span data-stu-id="b59ff-122">Root element</span></span>|<span data-ttu-id="b59ff-123">Het hoofdelement van het eigenschappenbestand.</span><span class="sxs-lookup"><span data-stu-id="b59ff-123">The root element of the properties file.</span></span>|  
|`Last-Modified`|<span data-ttu-id="b59ff-124">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b59ff-124">String</span></span>|<span data-ttu-id="b59ff-125">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="b59ff-125">Optional.</span></span> <span data-ttu-id="b59ff-126">Tijd laatste wijziging voor de blob.</span><span class="sxs-lookup"><span data-stu-id="b59ff-126">The last-modified time for the blob.</span></span> <span data-ttu-id="b59ff-127">Voor exporttaken.</span><span class="sxs-lookup"><span data-stu-id="b59ff-127">For export jobs only.</span></span>|  
|`Etag`|<span data-ttu-id="b59ff-128">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b59ff-128">String</span></span>|<span data-ttu-id="b59ff-129">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="b59ff-129">Optional.</span></span> <span data-ttu-id="b59ff-130">De ETag-waarde van de blob.</span><span class="sxs-lookup"><span data-stu-id="b59ff-130">The blob's ETag value.</span></span> <span data-ttu-id="b59ff-131">Voor exporttaken.</span><span class="sxs-lookup"><span data-stu-id="b59ff-131">For export jobs only.</span></span>|  
|`Content-Length`|<span data-ttu-id="b59ff-132">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b59ff-132">String</span></span>|<span data-ttu-id="b59ff-133">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="b59ff-133">Optional.</span></span> <span data-ttu-id="b59ff-134">De grootte van de blob in bytes.</span><span class="sxs-lookup"><span data-stu-id="b59ff-134">The size of the blob in bytes.</span></span> <span data-ttu-id="b59ff-135">Voor exporttaken.</span><span class="sxs-lookup"><span data-stu-id="b59ff-135">For export jobs only.</span></span>|  
|`Content-Type`|<span data-ttu-id="b59ff-136">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b59ff-136">String</span></span>|<span data-ttu-id="b59ff-137">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="b59ff-137">Optional.</span></span> <span data-ttu-id="b59ff-138">Het inhoudstype van de blob.</span><span class="sxs-lookup"><span data-stu-id="b59ff-138">The content type of the blob.</span></span>|  
|`Content-MD5`|<span data-ttu-id="b59ff-139">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b59ff-139">String</span></span>|<span data-ttu-id="b59ff-140">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="b59ff-140">Optional.</span></span> <span data-ttu-id="b59ff-141">De blob-MD5-hash.</span><span class="sxs-lookup"><span data-stu-id="b59ff-141">The blob's MD5 hash.</span></span>|  
|`Content-Encoding`|<span data-ttu-id="b59ff-142">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b59ff-142">String</span></span>|<span data-ttu-id="b59ff-143">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="b59ff-143">Optional.</span></span> <span data-ttu-id="b59ff-144">De blob-inhoud codering.</span><span class="sxs-lookup"><span data-stu-id="b59ff-144">The blob's content encoding.</span></span>|  
|`Content-Language`|<span data-ttu-id="b59ff-145">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b59ff-145">String</span></span>|<span data-ttu-id="b59ff-146">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="b59ff-146">Optional.</span></span> <span data-ttu-id="b59ff-147">Inhoud van de blob-taal.</span><span class="sxs-lookup"><span data-stu-id="b59ff-147">The blob's content language.</span></span>|  
|`Cache-Control`|<span data-ttu-id="b59ff-148">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="b59ff-148">String</span></span>|<span data-ttu-id="b59ff-149">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="b59ff-149">Optional.</span></span> <span data-ttu-id="b59ff-150">De cache-control-tekenreeks voor de blob.</span><span class="sxs-lookup"><span data-stu-id="b59ff-150">The cache control string for the blob.</span></span>|  

## <a name="next-steps"></a><span data-ttu-id="b59ff-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="b59ff-151">Next steps</span></span>

<span data-ttu-id="b59ff-152">Zie [blob-eigenschappen instellen](/rest/api/storageservices/set-blob-properties), [Blobmetagegevens ingesteld](/rest/api/storageservices/set-blob-metadata), en [instelling en het bij het ophalen van eigenschappen en metagegevens voor blob-bronnen](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) voor gedetailleerde informatie over het instellen van eigenschappen en blobmetagegevens-regels.</span><span class="sxs-lookup"><span data-stu-id="b59ff-152">See [Set blob properties](/rest/api/storageservices/set-blob-properties), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata), and [Setting and retrieving properties and metadata for blob resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) for detailed rules about setting blob metadata and properties.</span></span>
