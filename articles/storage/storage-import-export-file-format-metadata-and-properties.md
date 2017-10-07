---
title: aaaAzure-Import/Export metagegevens en eigenschappen bestandsindeling | Microsoft Docs
description: Meer informatie over hoe toospecify metagegevens en eigenschappen van een of meer blobs die deel uitmaken van een importeren of exporteren van de taak.
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
ms.openlocfilehash: bb13c1f1a27baea77298cb224970cd521d02d8c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a><span data-ttu-id="88f22-103">Azure Import/Export-service metagegevens en eigenschappen bestandsindeling</span><span class="sxs-lookup"><span data-stu-id="88f22-103">Azure Import/Export service metadata and properties file format</span></span>
<span data-ttu-id="88f22-104">U kunt de eigenschappen voor een of meer blobs en metagegevens als onderdeel van een import-taak of een taak voor exporteren opgeven.</span><span class="sxs-lookup"><span data-stu-id="88f22-104">You can specify metadata and properties for one or more blobs as part of an import job or an export job.</span></span> <span data-ttu-id="88f22-105">tooset metagegevens of eigenschappen voor blobs als onderdeel van een import-taak wordt gemaakt, kunt u een bestand met metagegevens of eigenschappen op de harde schijf Hallo Hallo gegevens toobe geïmporteerd met opgeven.</span><span class="sxs-lookup"><span data-stu-id="88f22-105">tooset metadata or properties for blobs being created as part of an import job, you provide a metadata or properties file on hello hard drive containing hello data toobe imported.</span></span> <span data-ttu-id="88f22-106">Voor een exporttaak worden metagegevens en eigenschappen geschreven tooa eigenschappen van metagegevens of bestand dat is opgenomen op de harde schijf Hallo tooyou geretourneerd.</span><span class="sxs-lookup"><span data-stu-id="88f22-106">For an export job, metadata and properties are written tooa metadata or properties file that is included on hello hard drive returned tooyou.</span></span>  
  
## <a name="metadata-file-format"></a><span data-ttu-id="88f22-107">Bestandsindeling voor metagegevens</span><span class="sxs-lookup"><span data-stu-id="88f22-107">Metadata file format</span></span>  
<span data-ttu-id="88f22-108">Hallo-indeling van een bestand met metagegevens is als volgt:</span><span class="sxs-lookup"><span data-stu-id="88f22-108">hello format of a metadata file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|<span data-ttu-id="88f22-109">XML-Element</span><span class="sxs-lookup"><span data-stu-id="88f22-109">XML Element</span></span>|<span data-ttu-id="88f22-110">Type</span><span class="sxs-lookup"><span data-stu-id="88f22-110">Type</span></span>|<span data-ttu-id="88f22-111">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="88f22-111">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Metadata`|<span data-ttu-id="88f22-112">Hoofdelement</span><span class="sxs-lookup"><span data-stu-id="88f22-112">Root element</span></span>|<span data-ttu-id="88f22-113">Hallo-hoofdelement van het metagegevensbestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="88f22-113">hello root element of hello metadata file.</span></span>|  
|`metadata-name`|<span data-ttu-id="88f22-114">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="88f22-114">String</span></span>|<span data-ttu-id="88f22-115">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="88f22-115">Optional.</span></span> <span data-ttu-id="88f22-116">Hallo XML-element Hallo-naam van Hallo metagegevens voor Hallo blob en de waarde geeft aan Hallo-waarde van de instelling voor Hallo-metagegevens.</span><span class="sxs-lookup"><span data-stu-id="88f22-116">hello XML element specifies hello name of hello metadata for hello blob, and its value specifies hello value of hello metadata setting.</span></span>|  
  
## <a name="properties-file-format"></a><span data-ttu-id="88f22-117">Eigenschappen-bestandsindeling</span><span class="sxs-lookup"><span data-stu-id="88f22-117">Properties file format</span></span>  
<span data-ttu-id="88f22-118">Hallo-indeling van een eigenschappenbestand is als volgt:</span><span class="sxs-lookup"><span data-stu-id="88f22-118">hello format of a properties file is as follows:</span></span>  
  
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
  
|<span data-ttu-id="88f22-119">XML-Element</span><span class="sxs-lookup"><span data-stu-id="88f22-119">XML Element</span></span>|<span data-ttu-id="88f22-120">Type</span><span class="sxs-lookup"><span data-stu-id="88f22-120">Type</span></span>|<span data-ttu-id="88f22-121">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="88f22-121">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Properties`|<span data-ttu-id="88f22-122">Hoofdelement</span><span class="sxs-lookup"><span data-stu-id="88f22-122">Root element</span></span>|<span data-ttu-id="88f22-123">Hallo-hoofdelement van Hallo eigenschappenbestand.</span><span class="sxs-lookup"><span data-stu-id="88f22-123">hello root element of hello properties file.</span></span>|  
|`Last-Modified`|<span data-ttu-id="88f22-124">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="88f22-124">String</span></span>|<span data-ttu-id="88f22-125">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="88f22-125">Optional.</span></span> <span data-ttu-id="88f22-126">Hallo tijd laatste wijziging voor Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="88f22-126">hello last-modified time for hello blob.</span></span> <span data-ttu-id="88f22-127">Voor exporttaken.</span><span class="sxs-lookup"><span data-stu-id="88f22-127">For export jobs only.</span></span>|  
|`Etag`|<span data-ttu-id="88f22-128">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="88f22-128">String</span></span>|<span data-ttu-id="88f22-129">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="88f22-129">Optional.</span></span> <span data-ttu-id="88f22-130">Hallo ETag-waarde van de blob.</span><span class="sxs-lookup"><span data-stu-id="88f22-130">hello blob's ETag value.</span></span> <span data-ttu-id="88f22-131">Voor exporttaken.</span><span class="sxs-lookup"><span data-stu-id="88f22-131">For export jobs only.</span></span>|  
|`Content-Length`|<span data-ttu-id="88f22-132">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="88f22-132">String</span></span>|<span data-ttu-id="88f22-133">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="88f22-133">Optional.</span></span> <span data-ttu-id="88f22-134">Hallo grootte van de blob Hallo in bytes.</span><span class="sxs-lookup"><span data-stu-id="88f22-134">hello size of hello blob in bytes.</span></span> <span data-ttu-id="88f22-135">Voor exporttaken.</span><span class="sxs-lookup"><span data-stu-id="88f22-135">For export jobs only.</span></span>|  
|`Content-Type`|<span data-ttu-id="88f22-136">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="88f22-136">String</span></span>|<span data-ttu-id="88f22-137">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="88f22-137">Optional.</span></span> <span data-ttu-id="88f22-138">Hallo-inhoudstype van Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="88f22-138">hello content type of hello blob.</span></span>|  
|`Content-MD5`|<span data-ttu-id="88f22-139">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="88f22-139">String</span></span>|<span data-ttu-id="88f22-140">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="88f22-140">Optional.</span></span> <span data-ttu-id="88f22-141">Hallo MD5-hash van de blob.</span><span class="sxs-lookup"><span data-stu-id="88f22-141">hello blob's MD5 hash.</span></span>|  
|`Content-Encoding`|<span data-ttu-id="88f22-142">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="88f22-142">String</span></span>|<span data-ttu-id="88f22-143">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="88f22-143">Optional.</span></span> <span data-ttu-id="88f22-144">Hallo van blob-inhoud codering.</span><span class="sxs-lookup"><span data-stu-id="88f22-144">hello blob's content encoding.</span></span>|  
|`Content-Language`|<span data-ttu-id="88f22-145">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="88f22-145">String</span></span>|<span data-ttu-id="88f22-146">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="88f22-146">Optional.</span></span> <span data-ttu-id="88f22-147">Hallo inhoud van de blob-taal.</span><span class="sxs-lookup"><span data-stu-id="88f22-147">hello blob's content language.</span></span>|  
|`Cache-Control`|<span data-ttu-id="88f22-148">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="88f22-148">String</span></span>|<span data-ttu-id="88f22-149">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="88f22-149">Optional.</span></span> <span data-ttu-id="88f22-150">Hallo cache besturingselement tekenreeks voor Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="88f22-150">hello cache control string for hello blob.</span></span>|  

## <a name="next-steps"></a><span data-ttu-id="88f22-151">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="88f22-151">Next steps</span></span>

<span data-ttu-id="88f22-152">Zie [blob-eigenschappen instellen](/rest/api/storageservices/set-blob-properties), [Blobmetagegevens ingesteld](/rest/api/storageservices/set-blob-metadata), en [instelling en het bij het ophalen van eigenschappen en metagegevens voor blob-bronnen](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) voor gedetailleerde informatie over het instellen van eigenschappen en blobmetagegevens-regels.</span><span class="sxs-lookup"><span data-stu-id="88f22-152">See [Set blob properties](/rest/api/storageservices/set-blob-properties), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata), and [Setting and retrieving properties and metadata for blob resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) for detailed rules about setting blob metadata and properties.</span></span>
