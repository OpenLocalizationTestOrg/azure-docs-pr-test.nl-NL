---
title: Azure Import/Export-logboekindeling | Microsoft Docs
description: Meer informatie over de indeling van de logboekbestanden gemaakt wanneer de stappen worden uitgevoerd voor een taak van Import/Export-service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 16234ccaf13ce1d85cfd207ed4734e683070faa6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="azure-importexport-service-log-file-format"></a><span data-ttu-id="0dba3-103">Azure Import/Export-service indeling van logboekbestand</span><span class="sxs-lookup"><span data-stu-id="0dba3-103">Azure Import/Export service log file format</span></span>
<span data-ttu-id="0dba3-104">Wanneer een actie in de Microsoft Azure Import/Export-service op een station dat als onderdeel van een import-taak of een taak voor het exporteren wordt uitgevoerd, worden logboeken geschreven naar blok-blobs in de storage-account dat is gekoppeld met deze taak.</span><span class="sxs-lookup"><span data-stu-id="0dba3-104">When the Microsoft Azure Import/Export service performs an action on a drive as part of an import job or an export job, logs are written to block blobs in the storage account associated with that job.</span></span>  
  
<span data-ttu-id="0dba3-105">Er zijn twee logboekbestanden die kunnen worden geschreven door de Import/Export-service:</span><span class="sxs-lookup"><span data-stu-id="0dba3-105">There are two logs that may be written by the Import/Export service:</span></span>  
  
-   <span data-ttu-id="0dba3-106">Het foutenlogboek wordt altijd in het geval van een fout gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="0dba3-106">The error log is always generated in the event of an error.</span></span>  
  
-   <span data-ttu-id="0dba3-107">Het uitgebreide logboek is standaard niet ingeschakeld, maar kan worden ingeschakeld door in te stellen de `EnableVerboseLog` -eigenschap op een [taak plaatsen](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) of [Update taakeigenschappen](/rest/api/storageimportexport/jobs#Jobs_Update) bewerking.</span><span class="sxs-lookup"><span data-stu-id="0dba3-107">The verbose log is not enabled by default, but may be enabled by setting the `EnableVerboseLog` property on a [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation.</span></span>  
  
## <a name="log-file-location"></a><span data-ttu-id="0dba3-108">De locatie van logboekbestand</span><span class="sxs-lookup"><span data-stu-id="0dba3-108">Log file location</span></span>  
<span data-ttu-id="0dba3-109">De logboeken worden geschreven naar het blok-blobs in de container of de virtuele map die is opgegeven door de `ImportExportStatesPath` instelling, die u kunt instellen op een `Put Job` bewerking.</span><span class="sxs-lookup"><span data-stu-id="0dba3-109">The logs are written to block blobs in the container or virtual directory specified by the `ImportExportStatesPath` setting, which you can set on a `Put Job` operation.</span></span> <span data-ttu-id="0dba3-110">De locatie waarop de logboeken geschreven is afhankelijk van hoe de verificatie is opgegeven voor de taak, samen met de opgegeven waarde voor `ImportExportStatesPath`.</span><span class="sxs-lookup"><span data-stu-id="0dba3-110">The location to which the logs are written depends on how authentication is specified for the job, together with the value specified for `ImportExportStatesPath`.</span></span> <span data-ttu-id="0dba3-111">Verificatie voor de taak kan worden opgegeven via de sleutel van een opslagaccount of een container SAS (shared access signature).</span><span class="sxs-lookup"><span data-stu-id="0dba3-111">Authentication for the job may be specified via a storage account key, or a container SAS (shared access signature).</span></span>  
  
<span data-ttu-id="0dba3-112">De naam van de container of de virtuele map kan ofwel worden de standaardnaam van `waimportexport`, of een andere container of de naam van de virtuele map die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="0dba3-112">The name of the container or virtual directory may either be the default name of `waimportexport`, or another container or virtual directory name that you specify.</span></span>  
  
<span data-ttu-id="0dba3-113">De onderstaande tabel ziet u de mogelijke opties:</span><span class="sxs-lookup"><span data-stu-id="0dba3-113">The table below shows the possible options:</span></span>  
  
|<span data-ttu-id="0dba3-114">Verificatiemethode</span><span class="sxs-lookup"><span data-stu-id="0dba3-114">Authentication Method</span></span>|<span data-ttu-id="0dba3-115">Waarde van `ImportExportStatesPath`Element</span><span class="sxs-lookup"><span data-stu-id="0dba3-115">Value of `ImportExportStatesPath`Element</span></span>|<span data-ttu-id="0dba3-116">Locatie van het logboek Blobs</span><span class="sxs-lookup"><span data-stu-id="0dba3-116">Location of Log Blobs</span></span>|  
|---------------------------|----------------------------------------------|---------------------------|  
|<span data-ttu-id="0dba3-117">De sleutel van opslagaccount</span><span class="sxs-lookup"><span data-stu-id="0dba3-117">Storage account key</span></span>|<span data-ttu-id="0dba3-118">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="0dba3-118">Default value</span></span>|<span data-ttu-id="0dba3-119">Een container met de naam `waimportexport`, dit is de standaard-container.</span><span class="sxs-lookup"><span data-stu-id="0dba3-119">A container named `waimportexport`, which is the default container.</span></span> <span data-ttu-id="0dba3-120">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0dba3-120">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|<span data-ttu-id="0dba3-121">De sleutel van opslagaccount</span><span class="sxs-lookup"><span data-stu-id="0dba3-121">Storage account key</span></span>|<span data-ttu-id="0dba3-122">Gebruiker opgegeven waarde</span><span class="sxs-lookup"><span data-stu-id="0dba3-122">User-specified value</span></span>|<span data-ttu-id="0dba3-123">Een container met de naam door de gebruiker.</span><span class="sxs-lookup"><span data-stu-id="0dba3-123">A container named by the user.</span></span> <span data-ttu-id="0dba3-124">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="0dba3-124">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|<span data-ttu-id="0dba3-125">Container SAS</span><span class="sxs-lookup"><span data-stu-id="0dba3-125">Container SAS</span></span>|<span data-ttu-id="0dba3-126">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="0dba3-126">Default value</span></span>|<span data-ttu-id="0dba3-127">Een virtuele map met de naam `waimportexport`, dit is de naam van de standaard onder de container die is opgegeven in de SAS.</span><span class="sxs-lookup"><span data-stu-id="0dba3-127">A virtual directory named `waimportexport`, which is the default name, beneath the container specified in the SAS.</span></span><br /><br /> <span data-ttu-id="0dba3-128">Bijvoorbeeld, als de SA's worden opgegeven voor de taak is `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, en vervolgens de locatie van het logboek zijn`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span><span class="sxs-lookup"><span data-stu-id="0dba3-128">For example, if the SAS specified for the job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, then the log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span></span>|  
|<span data-ttu-id="0dba3-129">Container SAS</span><span class="sxs-lookup"><span data-stu-id="0dba3-129">Container SAS</span></span>|<span data-ttu-id="0dba3-130">Gebruiker opgegeven waarde</span><span class="sxs-lookup"><span data-stu-id="0dba3-130">User-specified value</span></span>|<span data-ttu-id="0dba3-131">Een virtuele map met de naam door de gebruiker, onder de container die is opgegeven in de SAS.</span><span class="sxs-lookup"><span data-stu-id="0dba3-131">A virtual directory named by the user, beneath the container specified in the SAS.</span></span><br /><br /> <span data-ttu-id="0dba3-132">Bijvoorbeeld, als de SA's worden opgegeven voor de taak is `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, en de naam van de opgegeven virtuele map `mylogblobs`, wordt de locatie van het logboekbestand zou `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span><span class="sxs-lookup"><span data-stu-id="0dba3-132">For example, if the SAS specified for the job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, and the specified virtual directory is named `mylogblobs`, then the log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span></span>|  
  
<span data-ttu-id="0dba3-133">U kunt de URL voor de fout en de uitgebreide logboeken ophalen door het aanroepen van de [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) bewerking.</span><span class="sxs-lookup"><span data-stu-id="0dba3-133">You can retrieve the URL for the error and verbose logs by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="0dba3-134">De logboeken zijn beschikbaar nadat de verwerking van het station is voltooid.</span><span class="sxs-lookup"><span data-stu-id="0dba3-134">The logs are available after processing of the drive is complete.</span></span>  
  
## <a name="log-file-format"></a><span data-ttu-id="0dba3-135">Indeling van logboekbestand</span><span class="sxs-lookup"><span data-stu-id="0dba3-135">Log file format</span></span>  
<span data-ttu-id="0dba3-136">De indeling voor beide logboeken is hetzelfde: een blob met XML-beschrijvingen van de gebeurtenissen die zijn opgetreden tijdens het kopiëren van BLOB's tussen de vaste schijf en het account van de klant.</span><span class="sxs-lookup"><span data-stu-id="0dba3-136">The format for both logs is the same: a blob containing XML descriptions of the events that occurred while copying blobs between the hard drive and the customer's account.</span></span>  
  
<span data-ttu-id="0dba3-137">Het uitgebreide logboek bevat informatie over de status van de kopieerbewerking voor elke blob (voor een import-taak) of het bestand (voor een exporttaak) terwijl het foutenlogboek bevat alleen de informatie voor blobs of bestanden die fouten tijdens het importeren aangetroffen of taak voor het exporteren.</span><span class="sxs-lookup"><span data-stu-id="0dba3-137">The verbose log contains complete information about the status of the copy operation for every blob (for an import job) or file (for an export job), whereas the error log contains only the information for blobs or files that encountered errors during the import or export job.</span></span>  
  
<span data-ttu-id="0dba3-138">De uitgebreide logboekindeling worden hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0dba3-138">The verbose log format is shown below.</span></span> <span data-ttu-id="0dba3-139">Het foutenlogboek van dezelfde structuur heeft, maar geslaagde bewerkingen, worden uitgefilterd.</span><span class="sxs-lookup"><span data-stu-id="0dba3-139">The error log has the same structure, but filters out successful operations.</span></span>  

```xml
<DriveLog Version="2014-11-01">  
  <DriveId>drive-id</DriveId>  
  [<Blob Status="blob-status">  
   <BlobPath>blob-path</BlobPath>  
   <FilePath>file-path</FilePath>  
   [<Snapshot>snapshot</Snapshot>]  
   <Length>length</Length>  
   [<LastModified>last-modified</LastModified>]  
   [<ImportDisposition Status="import-disposition-status">import-disposition</ImportDisposition>]  
   [page-range-list-or-block-list]  
   [metadata-status]  
   [properties-status]  
  </Blob>]  
  [<Blob>  
    . . .  
  </Blob>]  
  <Status>drive-status</Status>  
</DriveLog>  
  
page-range-list-or-block-list ::= 
  page-range-list | block-list  
  
page-range-list ::=   
<PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
</PageRangeList>  
  
block-list ::=  
<BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       [Hash="md5-hash"] Status="block-status"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       [Hash="md5-hash"] Status="block-status"/>]  
</BlockList>  
  
metadata-status ::=  
<Metadata Status="metadata-status">  
   [<GlobalPath Hash="md5-hash">global-metadata-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">metadata-file-path</Path>]  
</Metadata>  
  
properties-status ::=  
<Properties Status="properties-status">  
   [<GlobalPath Hash="md5-hash">global-properties-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">properties-file-path</Path>]  
</Properties>  
```

<span data-ttu-id="0dba3-140">De volgende tabel beschrijft de elementen van het logboekbestand.</span><span class="sxs-lookup"><span data-stu-id="0dba3-140">The following table describes the elements of the log file.</span></span>  
  
|<span data-ttu-id="0dba3-141">XML-Element</span><span class="sxs-lookup"><span data-stu-id="0dba3-141">XML Element</span></span>|<span data-ttu-id="0dba3-142">Type</span><span class="sxs-lookup"><span data-stu-id="0dba3-142">Type</span></span>|<span data-ttu-id="0dba3-143">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0dba3-143">Description</span></span>|  
|-----------------|----------|-----------------|  
|`DriveLog`|<span data-ttu-id="0dba3-144">XML-Element</span><span class="sxs-lookup"><span data-stu-id="0dba3-144">XML Element</span></span>|<span data-ttu-id="0dba3-145">Hiermee geeft u een station voor logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="0dba3-145">Represents a drive log.</span></span>|  
|`Version`|<span data-ttu-id="0dba3-146">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0dba3-146">Attribute, String</span></span>|<span data-ttu-id="0dba3-147">De versie van de indeling voor logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="0dba3-147">The version of the log format.</span></span>|  
|`DriveId`|<span data-ttu-id="0dba3-148">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0dba3-148">String</span></span>|<span data-ttu-id="0dba3-149">Serienummer van het station hardware.</span><span class="sxs-lookup"><span data-stu-id="0dba3-149">The drive's hardware serial number.</span></span>|  
|`Status`|<span data-ttu-id="0dba3-150">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0dba3-150">String</span></span>|<span data-ttu-id="0dba3-151">Status van de verwerking van het station.</span><span class="sxs-lookup"><span data-stu-id="0dba3-151">Status of the drive processing.</span></span> <span data-ttu-id="0dba3-152">Zie de `Drive Status Codes` tabel hieronder voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="0dba3-152">See the `Drive Status Codes` table below for more information.</span></span>|  
|`Blob`|<span data-ttu-id="0dba3-153">Geneste XML-element</span><span class="sxs-lookup"><span data-stu-id="0dba3-153">Nested XML element</span></span>|<span data-ttu-id="0dba3-154">Hiermee geeft u een blob.</span><span class="sxs-lookup"><span data-stu-id="0dba3-154">Represents a blob.</span></span>|  
|`Blob/BlobPath`|<span data-ttu-id="0dba3-155">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0dba3-155">String</span></span>|<span data-ttu-id="0dba3-156">De URI van de blob.</span><span class="sxs-lookup"><span data-stu-id="0dba3-156">The URI of the blob.</span></span>|  
|`Blob/FilePath`|<span data-ttu-id="0dba3-157">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0dba3-157">String</span></span>|<span data-ttu-id="0dba3-158">Het relatieve pad naar het bestand op het station.</span><span class="sxs-lookup"><span data-stu-id="0dba3-158">The relative path to the file on the drive.</span></span>|  
|`Blob/Snapshot`|<span data-ttu-id="0dba3-159">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="0dba3-159">DateTime</span></span>|<span data-ttu-id="0dba3-160">De versie van de momentopname van de blob, voor een exporttaak.</span><span class="sxs-lookup"><span data-stu-id="0dba3-160">The snapshot version of the blob, for an export job only.</span></span>|  
|`Blob/Length`|<span data-ttu-id="0dba3-161">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="0dba3-161">Integer</span></span>|<span data-ttu-id="0dba3-162">De totale lengte van de blob in bytes.</span><span class="sxs-lookup"><span data-stu-id="0dba3-162">The total length of the blob in bytes.</span></span>|  
|`Blob/LastModified`|<span data-ttu-id="0dba3-163">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="0dba3-163">DateTime</span></span>|<span data-ttu-id="0dba3-164">De datum/tijd die de blob het laatst is gewijzigd voor een exporttaak.</span><span class="sxs-lookup"><span data-stu-id="0dba3-164">The date/time that the blob was last modified, for an export job only.</span></span>|  
|`Blob/ImportDisposition`|<span data-ttu-id="0dba3-165">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0dba3-165">String</span></span>|<span data-ttu-id="0dba3-166">De bestemming importeren van de blob, voor een import-taak alleen.</span><span class="sxs-lookup"><span data-stu-id="0dba3-166">The import disposition of the blob, for an import job only.</span></span>|  
|`Blob/ImportDisposition/@Status`|<span data-ttu-id="0dba3-167">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0dba3-167">Attribute, String</span></span>|<span data-ttu-id="0dba3-168">De status van de toestand importeren.</span><span class="sxs-lookup"><span data-stu-id="0dba3-168">The status of the import disposition.</span></span>|  
|`PageRangeList`|<span data-ttu-id="0dba3-169">Geneste XML-element</span><span class="sxs-lookup"><span data-stu-id="0dba3-169">Nested XML element</span></span>|<span data-ttu-id="0dba3-170">Hiermee geeft u een lijst met paginabereiken voor een pagina-blob.</span><span class="sxs-lookup"><span data-stu-id="0dba3-170">Represents a list of page ranges for a page blob.</span></span>|  
|`PageRange`|<span data-ttu-id="0dba3-171">XML-element</span><span class="sxs-lookup"><span data-stu-id="0dba3-171">XML element</span></span>|<span data-ttu-id="0dba3-172">Hiermee geeft u een paginabereik.</span><span class="sxs-lookup"><span data-stu-id="0dba3-172">Represents a page range.</span></span>|  
|`PageRange/@Offset`|<span data-ttu-id="0dba3-173">Kenmerk, geheel getal</span><span class="sxs-lookup"><span data-stu-id="0dba3-173">Attribute, Integer</span></span>|<span data-ttu-id="0dba3-174">Verschuiving van het paginabereik in de blob wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="0dba3-174">Starting offset of the page range in the blob.</span></span>|  
|`PageRange/@Length`|<span data-ttu-id="0dba3-175">Kenmerk, geheel getal</span><span class="sxs-lookup"><span data-stu-id="0dba3-175">Attribute, Integer</span></span>|<span data-ttu-id="0dba3-176">De lengte in bytes van het paginabereik.</span><span class="sxs-lookup"><span data-stu-id="0dba3-176">Length in bytes of the page range.</span></span>|  
|`PageRange/@Hash`|<span data-ttu-id="0dba3-177">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0dba3-177">Attribute, String</span></span>|<span data-ttu-id="0dba3-178">Base16 gecodeerd MD5-hash van het paginabereik.</span><span class="sxs-lookup"><span data-stu-id="0dba3-178">Base16-encoded MD5 hash of the page range.</span></span>|  
|`PageRange/@Status`|<span data-ttu-id="0dba3-179">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0dba3-179">Attribute, String</span></span>|<span data-ttu-id="0dba3-180">De status van de verwerking van het paginabereik.</span><span class="sxs-lookup"><span data-stu-id="0dba3-180">Status of processing the page range.</span></span>|  
|`BlockList`|<span data-ttu-id="0dba3-181">Geneste XML-element</span><span class="sxs-lookup"><span data-stu-id="0dba3-181">Nested XML element</span></span>|<span data-ttu-id="0dba3-182">Hiermee geeft u een lijst met bouwstenen voor een blok-blob.</span><span class="sxs-lookup"><span data-stu-id="0dba3-182">Represents a list of blocks for a block blob.</span></span>|  
|`Block`|<span data-ttu-id="0dba3-183">XML-element</span><span class="sxs-lookup"><span data-stu-id="0dba3-183">XML element</span></span>|<span data-ttu-id="0dba3-184">Hiermee geeft u een blok.</span><span class="sxs-lookup"><span data-stu-id="0dba3-184">Represents a block.</span></span>|  
|`Block/@Offset`|<span data-ttu-id="0dba3-185">Kenmerk, geheel getal</span><span class="sxs-lookup"><span data-stu-id="0dba3-185">Attribute, Integer</span></span>|<span data-ttu-id="0dba3-186">Verschuiving van het blok in de blob wordt gestart.</span><span class="sxs-lookup"><span data-stu-id="0dba3-186">Starting offset of the block in the blob.</span></span>|  
|`Block/@Length`|<span data-ttu-id="0dba3-187">Kenmerk, geheel getal</span><span class="sxs-lookup"><span data-stu-id="0dba3-187">Attribute, Integer</span></span>|<span data-ttu-id="0dba3-188">De lengte in bytes van het blok.</span><span class="sxs-lookup"><span data-stu-id="0dba3-188">Length in bytes of the block.</span></span>|  
|`Block/@Id`|<span data-ttu-id="0dba3-189">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0dba3-189">Attribute, String</span></span>|<span data-ttu-id="0dba3-190">De blok-ID.</span><span class="sxs-lookup"><span data-stu-id="0dba3-190">The block ID.</span></span>|  
|`Block/@Hash`|<span data-ttu-id="0dba3-191">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0dba3-191">Attribute, String</span></span>|<span data-ttu-id="0dba3-192">Base16 gecodeerd MD5-hash van het blok.</span><span class="sxs-lookup"><span data-stu-id="0dba3-192">Base16-encoded MD5 hash of the block.</span></span>|  
|`Block/@Status`|<span data-ttu-id="0dba3-193">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0dba3-193">Attribute, String</span></span>|<span data-ttu-id="0dba3-194">De status van de verwerking van het blok.</span><span class="sxs-lookup"><span data-stu-id="0dba3-194">Status of processing the block.</span></span>|  
|`Metadata`|<span data-ttu-id="0dba3-195">Geneste XML-element</span><span class="sxs-lookup"><span data-stu-id="0dba3-195">Nested XML element</span></span>|<span data-ttu-id="0dba3-196">Hiermee geeft u de metagegevens van de blob.</span><span class="sxs-lookup"><span data-stu-id="0dba3-196">Represents the blob's metadata.</span></span>|  
|`Metadata/@Status`|<span data-ttu-id="0dba3-197">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0dba3-197">Attribute, String</span></span>|<span data-ttu-id="0dba3-198">De status van de verwerking van de blobmetagegevens.</span><span class="sxs-lookup"><span data-stu-id="0dba3-198">Status of processing of the blob metadata.</span></span>|  
|`Metadata/GlobalPath`|<span data-ttu-id="0dba3-199">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0dba3-199">String</span></span>|<span data-ttu-id="0dba3-200">Relatief pad naar het bestand algemene metagegevens.</span><span class="sxs-lookup"><span data-stu-id="0dba3-200">Relative path to the global metadata file.</span></span>|  
|`Metadata/GlobalPath/@Hash`|<span data-ttu-id="0dba3-201">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0dba3-201">Attribute, String</span></span>|<span data-ttu-id="0dba3-202">Base16 gecodeerd MD5-hash van het bestand algemene metagegevens.</span><span class="sxs-lookup"><span data-stu-id="0dba3-202">Base16-encoded MD5 hash of the global metadata file.</span></span>|  
|`Metadata/Path`|<span data-ttu-id="0dba3-203">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0dba3-203">String</span></span>|<span data-ttu-id="0dba3-204">Relatief pad naar het bestand met metagegevens.</span><span class="sxs-lookup"><span data-stu-id="0dba3-204">Relative path to the metadata file.</span></span>|  
|`Metadata/Path/@Hash`|<span data-ttu-id="0dba3-205">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0dba3-205">Attribute, String</span></span>|<span data-ttu-id="0dba3-206">Base16 gecodeerd MD5-hash van het bestand met metagegevens.</span><span class="sxs-lookup"><span data-stu-id="0dba3-206">Base16-encoded MD5 hash of the metadata file.</span></span>|  
|`Properties`|<span data-ttu-id="0dba3-207">Geneste XML-element</span><span class="sxs-lookup"><span data-stu-id="0dba3-207">Nested XML element</span></span>|<span data-ttu-id="0dba3-208">Geeft de blob-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="0dba3-208">Represents the blob properties.</span></span>|  
|`Properties/@Status`|<span data-ttu-id="0dba3-209">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0dba3-209">Attribute, String</span></span>|<span data-ttu-id="0dba3-210">Status van de verwerking van de blob-eigenschappen, bijvoorbeeld bestand niet gevonden, voltooid.</span><span class="sxs-lookup"><span data-stu-id="0dba3-210">Status of processing the blob properties, e.g. file not found, completed.</span></span>|  
|`Properties/GlobalPath`|<span data-ttu-id="0dba3-211">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0dba3-211">String</span></span>|<span data-ttu-id="0dba3-212">Relatief pad naar het bestand algemene eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="0dba3-212">Relative path to the global properties file.</span></span>|  
|`Properties/GlobalPath/@Hash`|<span data-ttu-id="0dba3-213">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0dba3-213">Attribute, String</span></span>|<span data-ttu-id="0dba3-214">Base16 gecodeerd MD5-hash van het bestand algemene eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="0dba3-214">Base16-encoded MD5 hash of the global properties file.</span></span>|  
|`Properties/Path`|<span data-ttu-id="0dba3-215">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0dba3-215">String</span></span>|<span data-ttu-id="0dba3-216">Relatief pad naar het eigenschappenbestand.</span><span class="sxs-lookup"><span data-stu-id="0dba3-216">Relative path to the properties file.</span></span>|  
|`Properties/Path/@Hash`|<span data-ttu-id="0dba3-217">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0dba3-217">Attribute, String</span></span>|<span data-ttu-id="0dba3-218">Base16 gecodeerd MD5-hash van het eigenschappenbestand.</span><span class="sxs-lookup"><span data-stu-id="0dba3-218">Base16-encoded MD5 hash of the properties file.</span></span>|  
|`Blob/Status`|<span data-ttu-id="0dba3-219">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="0dba3-219">String</span></span>|<span data-ttu-id="0dba3-220">De status van de verwerking van de blob.</span><span class="sxs-lookup"><span data-stu-id="0dba3-220">Status of processing the blob.</span></span>|  
  
# <a name="drive-status-codes"></a><span data-ttu-id="0dba3-221">Statuscodes van station</span><span class="sxs-lookup"><span data-stu-id="0dba3-221">Drive status codes</span></span>  
<span data-ttu-id="0dba3-222">De volgende tabel bevat de statuscodes voor het verwerken van een station.</span><span class="sxs-lookup"><span data-stu-id="0dba3-222">The following table lists the status codes for processing a drive.</span></span>  
  
|<span data-ttu-id="0dba3-223">Statuscode</span><span class="sxs-lookup"><span data-stu-id="0dba3-223">Status code</span></span>|<span data-ttu-id="0dba3-224">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0dba3-224">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="0dba3-225">Het station is verwerking zonder fouten voltooid.</span><span class="sxs-lookup"><span data-stu-id="0dba3-225">The drive has finished processing without any errors.</span></span>|  
|`CompletedWithWarnings`|<span data-ttu-id="0dba3-226">Het station zijn met waarschuwingen in een of meer blobs per de import dispositions opgegeven voor de blobs verwerkt.</span><span class="sxs-lookup"><span data-stu-id="0dba3-226">The drive has finished processing with warnings in one or more blobs per the import dispositions specified for the blobs.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="0dba3-227">Het station is voltooid met fouten in een of meer blobs of segmenten.</span><span class="sxs-lookup"><span data-stu-id="0dba3-227">The drive has finished with errors in one or more blobs or chunks.</span></span>|  
|`DiskNotFound`|<span data-ttu-id="0dba3-228">Er is geen schijf gevonden op de schijf.</span><span class="sxs-lookup"><span data-stu-id="0dba3-228">No disk is found on the drive.</span></span>|  
|`VolumeNotNtfs`|<span data-ttu-id="0dba3-229">De eerste gegevensvolume op de schijf is niet in een NTFS-indeling.</span><span class="sxs-lookup"><span data-stu-id="0dba3-229">The first data volume on the disk is not in NTFS format.</span></span>|  
|`DiskOperationFailed`|<span data-ttu-id="0dba3-230">Er is een onbekende fout opgetreden bij het uitvoeren van bewerkingen op het station.</span><span class="sxs-lookup"><span data-stu-id="0dba3-230">An unknown failure occurred when performing operations on the drive.</span></span>|  
|`BitLockerVolumeNotFound`|<span data-ttu-id="0dba3-231">Er is geen BitLocker encryptable volume gevonden.</span><span class="sxs-lookup"><span data-stu-id="0dba3-231">No BitLocker encryptable volume is found.</span></span>|  
|`BitLockerNotActivated`|<span data-ttu-id="0dba3-232">BitLocker is niet ingeschakeld op het volume.</span><span class="sxs-lookup"><span data-stu-id="0dba3-232">BitLocker is not enabled on the volume.</span></span>|  
|`BitLockerProtectorNotFound`|<span data-ttu-id="0dba3-233">De numerieke wachtwoordsleutelbeveiliging bestaat niet op het volume.</span><span class="sxs-lookup"><span data-stu-id="0dba3-233">The numerical password key protector does not exist on the volume.</span></span>|  
|`BitLockerKeyInvalid`|<span data-ttu-id="0dba3-234">Het opgegeven numerieke wachtwoord kan niet het volume ontgrendelen.</span><span class="sxs-lookup"><span data-stu-id="0dba3-234">The numerical password provided cannot unlock the volume.</span></span>|  
|`BitLockerUnlockVolumeFailed`|<span data-ttu-id="0dba3-235">Is een onbekende fout opgetreden bij het ontgrendelen van het volume.</span><span class="sxs-lookup"><span data-stu-id="0dba3-235">Unknown failure has happened when trying to unlock the volume.</span></span>|  
|`BitLockerFailed`|<span data-ttu-id="0dba3-236">Een onbekende fout opgetreden tijdens het uitvoeren van BitLocker-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="0dba3-236">An unknown failure occurred while performing BitLocker operations.</span></span>|  
|`ManifestNameInvalid`|<span data-ttu-id="0dba3-237">De naam van het manifestbestand is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="0dba3-237">The manifest file name is invalid.</span></span>|  
|`ManifestNameTooLong`|<span data-ttu-id="0dba3-238">De naam van het manifestbestand is te lang.</span><span class="sxs-lookup"><span data-stu-id="0dba3-238">The manifest file name is too long.</span></span>|  
|`ManifestNotFound`|<span data-ttu-id="0dba3-239">Het manifestbestand is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="0dba3-239">The manifest file is not found.</span></span>|  
|`ManifestAccessDenied`|<span data-ttu-id="0dba3-240">Toegang tot het manifestbestand is geweigerd.</span><span class="sxs-lookup"><span data-stu-id="0dba3-240">Access to the manifest file is denied.</span></span>|  
|`ManifestCorrupted`|<span data-ttu-id="0dba3-241">Het manifestbestand is beschadigd (de inhoud komt niet overeen met de hash).</span><span class="sxs-lookup"><span data-stu-id="0dba3-241">The manifest file is corrupted (the content does not match its hash).</span></span>|  
|`ManifestFormatInvalid`|<span data-ttu-id="0dba3-242">Het manifest inhoud voldoet niet aan de vereiste indeling.</span><span class="sxs-lookup"><span data-stu-id="0dba3-242">The manifest content does not conform to the required format.</span></span>|  
|`ManifestDriveIdMismatch`|<span data-ttu-id="0dba3-243">De schijf-ID in het manifestbestand komt niet overeen met het één lezen van het station.</span><span class="sxs-lookup"><span data-stu-id="0dba3-243">The drive ID in the manifest file does not match the one read from the drive.</span></span>|  
|`ReadManifestFailed`|<span data-ttu-id="0dba3-244">Er is een schijf-i/o-fout opgetreden tijdens het lezen van het manifest.</span><span class="sxs-lookup"><span data-stu-id="0dba3-244">A disk I/O failure occurred while reading from the manifest.</span></span>|  
|`BlobListFormatInvalid`|<span data-ttu-id="0dba3-245">De uitvoer-blob lijst blob voldoet niet aan de vereiste indeling.</span><span class="sxs-lookup"><span data-stu-id="0dba3-245">The export blob list blob does not conform to the required format.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="0dba3-246">Toegang tot de blobs in de storage-account is niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="0dba3-246">Access to the blobs in the storage account is forbidden.</span></span> <span data-ttu-id="0dba3-247">Dit wordt mogelijk veroorzaakt door ongeldige opslagaccountsleutel of SAS-container.</span><span class="sxs-lookup"><span data-stu-id="0dba3-247">This might be due to invalid storage account key or container SAS.</span></span>|  
|`InternalError`|<span data-ttu-id="0dba3-248">En er is een interne fout opgetreden tijdens het verwerken van het station.</span><span class="sxs-lookup"><span data-stu-id="0dba3-248">And internal error occurred while processing the drive.</span></span>|  
  
## <a name="blob-status-codes"></a><span data-ttu-id="0dba3-249">Statuscodes BLOB</span><span class="sxs-lookup"><span data-stu-id="0dba3-249">Blob status codes</span></span>  
<span data-ttu-id="0dba3-250">De volgende tabel bevat de statuscodes voor het verwerken van een blob.</span><span class="sxs-lookup"><span data-stu-id="0dba3-250">The following table lists the status codes for processing a blob.</span></span>  
  
|<span data-ttu-id="0dba3-251">Statuscode</span><span class="sxs-lookup"><span data-stu-id="0dba3-251">Status code</span></span>|<span data-ttu-id="0dba3-252">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0dba3-252">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="0dba3-253">De blob is verwerking zonder fouten voltooid.</span><span class="sxs-lookup"><span data-stu-id="0dba3-253">The blob has finished processing without errors.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="0dba3-254">De blob zijn met fouten in een of meer paginabereiken of blokken, metagegevens of eigenschappen verwerkt.</span><span class="sxs-lookup"><span data-stu-id="0dba3-254">The blob has finished processing with errors in one or more page ranges or blocks, metadata, or properties.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="0dba3-255">De bestandsnaam is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="0dba3-255">The file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="0dba3-256">De bestandsnaam is te lang.</span><span class="sxs-lookup"><span data-stu-id="0dba3-256">The file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="0dba3-257">Het bestand is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="0dba3-257">The file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="0dba3-258">Toegang tot het bestand is geweigerd.</span><span class="sxs-lookup"><span data-stu-id="0dba3-258">Access to the file is denied.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="0dba3-259">De Blob-service-aanvraag voor toegang tot de blob is mislukt.</span><span class="sxs-lookup"><span data-stu-id="0dba3-259">The Blob service request to access the blob has failed.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="0dba3-260">De Blob-service-aanvraag voor toegang tot de blob is verboden.</span><span class="sxs-lookup"><span data-stu-id="0dba3-260">The Blob service request to access the blob is forbidden.</span></span> <span data-ttu-id="0dba3-261">Dit wordt mogelijk veroorzaakt door ongeldige opslagaccountsleutel of SAS-container.</span><span class="sxs-lookup"><span data-stu-id="0dba3-261">This might be due to invalid storage account key or container SAS.</span></span>|  
|`RenameFailed`|<span data-ttu-id="0dba3-262">Wijzigen van de blob (voor een import-taak) of het bestand (voor een taak voor het exporteren) is mislukt.</span><span class="sxs-lookup"><span data-stu-id="0dba3-262">Failed to rename the blob (for an import job) or the file (for an export job).</span></span>|  
|`BlobUnexpectedChange`|<span data-ttu-id="0dba3-263">Onverwachte wijziging is opgetreden met de blob (voor een taak voor het exporteren).</span><span class="sxs-lookup"><span data-stu-id="0dba3-263">An unexpected change has occurred with the blob (for an export job).</span></span>|  
|`LeasePresent`|<span data-ttu-id="0dba3-264">Er is een lease aanwezig is op de blob.</span><span class="sxs-lookup"><span data-stu-id="0dba3-264">There is a lease present on the blob.</span></span>|  
|`IOFailed`|<span data-ttu-id="0dba3-265">Er is een schijf of het netwerk-i/o-fout opgetreden tijdens het verwerken van de blob.</span><span class="sxs-lookup"><span data-stu-id="0dba3-265">A disk or network I/O failure occurred while processing the blob.</span></span>|  
|`Failed`|<span data-ttu-id="0dba3-266">Er is een onbekende fout opgetreden tijdens het verwerken van de blob.</span><span class="sxs-lookup"><span data-stu-id="0dba3-266">An unknown failure occurred while processing the blob.</span></span>|  
  
## <a name="import-disposition-status-codes"></a><span data-ttu-id="0dba3-267">Statuscodes disposition importeren</span><span class="sxs-lookup"><span data-stu-id="0dba3-267">Import disposition status codes</span></span>  
<span data-ttu-id="0dba3-268">De volgende tabel bevat de statuscodes voor het oplossen van een toestand importeren.</span><span class="sxs-lookup"><span data-stu-id="0dba3-268">The following table lists the status codes for resolving an import disposition.</span></span>  
  
|<span data-ttu-id="0dba3-269">Statuscode</span><span class="sxs-lookup"><span data-stu-id="0dba3-269">Status code</span></span>|<span data-ttu-id="0dba3-270">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0dba3-270">Description</span></span>|  
|-----------------|-----------------|  
|`Created`|<span data-ttu-id="0dba3-271">De blob is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="0dba3-271">The blob has been created.</span></span>|  
|`Renamed`|<span data-ttu-id="0dba3-272">De blob heeft per rename importeren bestemming gekregen.</span><span class="sxs-lookup"><span data-stu-id="0dba3-272">The blob has been renamed per rename import disposition.</span></span> <span data-ttu-id="0dba3-273">De `Blob/BlobPath` element bevat de URI voor de nieuwe naam blob.</span><span class="sxs-lookup"><span data-stu-id="0dba3-273">The `Blob/BlobPath` element contains the URI for the renamed blob.</span></span>|  
|`Skipped`|<span data-ttu-id="0dba3-274">De blob is overgeslagen `no-overwrite` toestand importeren.</span><span class="sxs-lookup"><span data-stu-id="0dba3-274">The blob has been skipped per `no-overwrite` import disposition.</span></span>|  
|`Overwritten`|<span data-ttu-id="0dba3-275">De blob heeft een bestaande blob per overschreven `overwrite` toestand importeren.</span><span class="sxs-lookup"><span data-stu-id="0dba3-275">The blob has overwritten an existing blob per `overwrite` import disposition.</span></span>|  
|`Cancelled`|<span data-ttu-id="0dba3-276">Een eerdere fout is gestopt verdere verwerking van de toestand importeren.</span><span class="sxs-lookup"><span data-stu-id="0dba3-276">A prior failure has stopped further processing of the import disposition.</span></span>|  
  
## <a name="page-rangeblock-status-codes"></a><span data-ttu-id="0dba3-277">Statuscodes voor pagina-bereik/blok</span><span class="sxs-lookup"><span data-stu-id="0dba3-277">Page range/block status codes</span></span>  
<span data-ttu-id="0dba3-278">De volgende tabel bevat de statuscodes voor het verwerken van een paginabereik of een blok.</span><span class="sxs-lookup"><span data-stu-id="0dba3-278">The following table lists the status codes for processing a page range or a block.</span></span>  
  
|<span data-ttu-id="0dba3-279">Statuscode</span><span class="sxs-lookup"><span data-stu-id="0dba3-279">Status code</span></span>|<span data-ttu-id="0dba3-280">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0dba3-280">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="0dba3-281">De paginabereik of blok is verwerking zonder fouten voltooid.</span><span class="sxs-lookup"><span data-stu-id="0dba3-281">The page range or block has finished processing without any errors.</span></span>|  
|`Committed`|<span data-ttu-id="0dba3-282">Het blok is doorgevoerd, maar niet in het volledige blok lijst omdat andere blokken is mislukt, of de volledige lijst met geblokkeerde websites zelf plaatsen is mislukt.</span><span class="sxs-lookup"><span data-stu-id="0dba3-282">The block has been committed,  but not in the full block list because other blocks have failed, or put full block list itself has failed.</span></span>|  
|`Uncommitted`|<span data-ttu-id="0dba3-283">Het blok is geüpload, maar niet zijn doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="0dba3-283">The block is uploaded but not committed.</span></span>|  
|`Corrupted`|<span data-ttu-id="0dba3-284">De paginabereik of blok is beschadigd (de inhoud komt niet overeen met de hash).</span><span class="sxs-lookup"><span data-stu-id="0dba3-284">The page range or block is corrupted (the content does not match its hash).</span></span>|  
|`FileUnexpectedEnd`|<span data-ttu-id="0dba3-285">Een onverwacht bestandseinde er is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="0dba3-285">An unexpected end of file has been encountered.</span></span>|  
|`BlobUnexpectedEnd`|<span data-ttu-id="0dba3-286">Een onverwacht einde van de blob is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="0dba3-286">An unexpected end of blob has been encountered.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="0dba3-287">De Blob-service-aanvraag voor toegang tot het bereik of blok is mislukt.</span><span class="sxs-lookup"><span data-stu-id="0dba3-287">The Blob service request to access the page range or block has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="0dba3-288">Er is een schijf of het netwerk-i/o-fout opgetreden tijdens het verwerken van de paginabereik of blok.</span><span class="sxs-lookup"><span data-stu-id="0dba3-288">A disk or network I/O failure occurred while processing the page range or block.</span></span>|  
|`Failed`|<span data-ttu-id="0dba3-289">Een onbekende fout opgetreden tijdens het verwerken van de paginabereik of blok.</span><span class="sxs-lookup"><span data-stu-id="0dba3-289">An unknown failure occurred while processing the page range or block.</span></span>|  
|`Cancelled`|<span data-ttu-id="0dba3-290">Er is een eerdere fout gestopt verdere verwerking van de paginabereik of blok.</span><span class="sxs-lookup"><span data-stu-id="0dba3-290">A prior failure has stopped further processing of the page range or block.</span></span>|  
  
## <a name="metadata-status-codes"></a><span data-ttu-id="0dba3-291">Statuscodes van metagegevens</span><span class="sxs-lookup"><span data-stu-id="0dba3-291">Metadata status codes</span></span>  
<span data-ttu-id="0dba3-292">De volgende tabel bevat de statuscodes voor het verwerken van blobmetagegevens.</span><span class="sxs-lookup"><span data-stu-id="0dba3-292">The following table lists the status codes for processing blob metadata.</span></span>  
  
|<span data-ttu-id="0dba3-293">Statuscode</span><span class="sxs-lookup"><span data-stu-id="0dba3-293">Status code</span></span>|<span data-ttu-id="0dba3-294">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0dba3-294">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="0dba3-295">De metagegevens is verwerking zonder fouten voltooid.</span><span class="sxs-lookup"><span data-stu-id="0dba3-295">The metadata has finished processing without errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="0dba3-296">De bestandsnaam van metagegevens is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="0dba3-296">The metadata file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="0dba3-297">De metagegevens-bestandsnaam is te lang.</span><span class="sxs-lookup"><span data-stu-id="0dba3-297">The metadata file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="0dba3-298">Het bestand met metagegevens is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="0dba3-298">The metadata file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="0dba3-299">Toegang tot het bestand met metagegevens is geweigerd.</span><span class="sxs-lookup"><span data-stu-id="0dba3-299">Access to the metadata file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="0dba3-300">Het metagegevensbestand is beschadigd (de inhoud komt niet overeen met de hash).</span><span class="sxs-lookup"><span data-stu-id="0dba3-300">The metadata file is corrupted (the content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="0dba3-301">De metagegevens van inhoud voldoet niet aan de vereiste indeling.</span><span class="sxs-lookup"><span data-stu-id="0dba3-301">The metadata content does not conform to the required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="0dba3-302">Schrijven van de metagegevens van de is XML mislukt.</span><span class="sxs-lookup"><span data-stu-id="0dba3-302">Writing the metadata XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="0dba3-303">De Blob-service-aanvraag voor toegang tot de metagegevens is mislukt.</span><span class="sxs-lookup"><span data-stu-id="0dba3-303">The Blob service request to access the metadata has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="0dba3-304">Een schijf of het netwerk-i/o-fout opgetreden tijdens het verwerken van de metagegevens.</span><span class="sxs-lookup"><span data-stu-id="0dba3-304">A disk or network I/O failure occurred while processing the metadata.</span></span>|  
|`Failed`|<span data-ttu-id="0dba3-305">Een onbekende fout opgetreden tijdens het verwerken van de metagegevens.</span><span class="sxs-lookup"><span data-stu-id="0dba3-305">An unknown failure occurred while processing the metadata.</span></span>|  
|`Cancelled`|<span data-ttu-id="0dba3-306">Een eerdere fout is gestopt verdere verwerking van de metagegevens.</span><span class="sxs-lookup"><span data-stu-id="0dba3-306">A prior failure has stopped further processing of the metadata.</span></span>|  
  
## <a name="properties-status-codes"></a><span data-ttu-id="0dba3-307">Statuscodes van eigenschappen</span><span class="sxs-lookup"><span data-stu-id="0dba3-307">Properties status codes</span></span>  
<span data-ttu-id="0dba3-308">De volgende tabel bevat de statuscodes voor het verwerken van blob-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="0dba3-308">The following table lists the status codes for processing blob properties.</span></span>  
  
|<span data-ttu-id="0dba3-309">Statuscode</span><span class="sxs-lookup"><span data-stu-id="0dba3-309">Status code</span></span>|<span data-ttu-id="0dba3-310">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="0dba3-310">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="0dba3-311">De eigenschappen verwerken zonder fouten is voltooid.</span><span class="sxs-lookup"><span data-stu-id="0dba3-311">The properties have finished processing without any errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="0dba3-312">De bestandsnaam van de eigenschappen is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="0dba3-312">The properties file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="0dba3-313">De eigenschappen-bestandsnaam is te lang.</span><span class="sxs-lookup"><span data-stu-id="0dba3-313">The properties file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="0dba3-314">Het eigenschappenbestand is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="0dba3-314">The properties file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="0dba3-315">Toegang tot het eigenschappenbestand is geweigerd.</span><span class="sxs-lookup"><span data-stu-id="0dba3-315">Access to the properties file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="0dba3-316">De eigenschappenbestand is beschadigd (de inhoud komt niet overeen met de hash).</span><span class="sxs-lookup"><span data-stu-id="0dba3-316">The properties file is corrupted (the content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="0dba3-317">De eigenschappen van inhoud voldoet niet aan de vereiste indeling.</span><span class="sxs-lookup"><span data-stu-id="0dba3-317">The properties content does not conform to the required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="0dba3-318">Schrijven van de eigenschappen is XML mislukt.</span><span class="sxs-lookup"><span data-stu-id="0dba3-318">Writing the properties XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="0dba3-319">De aanvraag voor toegang tot de eigenschappen voor de Blob is mislukt.</span><span class="sxs-lookup"><span data-stu-id="0dba3-319">The Blob service request to access the properties has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="0dba3-320">Er is een schijf of het netwerk-i/o-fout opgetreden tijdens het verwerken van de eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="0dba3-320">A disk or network I/O failure occurred while processing the properties.</span></span>|  
|`Failed`|<span data-ttu-id="0dba3-321">Er is een onbekende fout opgetreden tijdens het verwerken van de eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="0dba3-321">An unknown failure occurred while processing the properties.</span></span>|  
|`Cancelled`|<span data-ttu-id="0dba3-322">Er is een eerdere fout gestopt verdere verwerking van de eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="0dba3-322">A prior failure has stopped further processing of the properties.</span></span>|  
  
## <a name="sample-logs"></a><span data-ttu-id="0dba3-323">Voorbeeld-Logboeken</span><span class="sxs-lookup"><span data-stu-id="0dba3-323">Sample logs</span></span>  
<span data-ttu-id="0dba3-324">Hier volgt een voorbeeld van uitgebreide logboek.</span><span class="sxs-lookup"><span data-stu-id="0dba3-324">The following is an example of verbose log.</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV123456</DriveId>  
    <Blob Status="Completed">  
       <BlobPath>pictures/bob/wild/desert.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\wild\desert.jpg</FilePath>  
       <Length>98304</Length>  
       <ImportDisposition Status="Created">overwrite</ImportDisposition>  
       <BlockList>  
          <Block Offset="0" Length="65536" Id="AAAAAA==" Hash=" 9C8AE14A55241F98533C4D80D85CDC68" Status="Completed"/>  
          <Block Offset="65536" Length="32768" Id="AQAAAA==" Hash=" DF54C531C9B3CA2570FDDDB3BCD0E27D" Status="Completed"/>  
       </BlockList>  
       <Metadata Status="Completed">  
          <GlobalPath Hash=" E34F54B7086BCF4EC1601D056F4C7E37">\Users\bob\Pictures\wild\metadata.xml</GlobalPath>  
       </Metadata>  
    </Blob>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="0" Length="65536" Hash="19701B8877418393CB3CB567F53EE225" Status="Completed"/>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
          <PageRange Offset="131072" Length="4096" Hash="9BA552E1C3EEAFFC91B42B979900A996" Status="Completed"/>  
       </PageRangeList>  
       <Properties Status="Completed">  
          <Path Hash="38D7AE80653F47F63C0222FEE90EC4E7">\Users\bob\Pictures\animals\koala.jpg.properties</Path>  
       </Properties>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
<span data-ttu-id="0dba3-325">Het foutenlogboek van het bijbehorende worden hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="0dba3-325">The corresponding error log is shown below.</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV6965824</DriveId>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
       </PageRangeList>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

 <span data-ttu-id="0dba3-326">Het foutenlogboek volgen voor een import-taak bevat een fout over een bestand niet gevonden op de schijf importeren.</span><span class="sxs-lookup"><span data-stu-id="0dba3-326">The follow error log for an import job contains an error about a file not found on the import drive.</span></span> <span data-ttu-id="0dba3-327">Denk eraan dat de status van de volgende onderdelen is `Cancelled`.</span><span class="sxs-lookup"><span data-stu-id="0dba3-327">Note that the status of subsequent components is `Cancelled`.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="FileNotFound">  
    <BlobPath>pictures/animals/koala.jpg</BlobPath>  
    <FilePath>\animals\koala.jpg</FilePath>  
    <Length>30310</Length>  
    <ImportDisposition Status="Cancelled">rename</ImportDisposition>  
    <BlockList>  
      <Block Offset="0" Length="6062" Id="MD5/cAzn4h7VVSWXf696qp5Uaw==" Hash="700CE7E21ED55525977FAF7AAA9E546B" Status="Cancelled" />  
      <Block Offset="6062" Length="6062" Id="MD5/PEnGwYOI8LPLNYdfKr7kAg==" Hash="3C49C6C18388F0B3CB35875F2ABEE402" Status="Cancelled" />  
      <Block Offset="12124" Length="6062" Id="MD5/FG4WxqfZKuUWZ2nGTU2qVA==" Hash="146E16C6A7D92AE5166769C64D4DAA54" Status="Cancelled" />  
      <Block Offset="18186" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
      <Block Offset="24248" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

<span data-ttu-id="0dba3-328">Het volgende foutenlogboek voor een taak voor het exporteren geeft aan dat de blob-inhoud is geschreven naar de schijf, maar is een fout opgetreden tijdens het exporteren van de blob-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="0dba3-328">The following error log for an export job indicates that the blob content has been successfully written to the drive, but that an error occurred while exporting the blob's properties.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C3U</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
    <FilePath>\pictures\wild\canyon.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList />  
    <Properties Status="Failed" />  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
## <a name="next-steps"></a><span data-ttu-id="0dba3-329">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0dba3-329">Next steps</span></span>
 
* [<span data-ttu-id="0dba3-330">REST-API van Storage Import/Export</span><span class="sxs-lookup"><span data-stu-id="0dba3-330">Storage Import/Export REST API</span></span>](/rest/api/storageimportexport/)
