---
title: indeling van logboekbestand aaaAzure voor importeren/exporteren | Microsoft Docs
description: Meer informatie over het Hallo-indeling van logboekbestanden Hallo gemaakt wanneer de stappen worden uitgevoerd voor een taak van Import/Export-service.
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
ms.openlocfilehash: 15a652455aa947922af0aa39ccefe68811a3db19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-log-file-format"></a><span data-ttu-id="ff684-103">Azure Import/Export-service indeling van logboekbestand</span><span class="sxs-lookup"><span data-stu-id="ff684-103">Azure Import/Export service log file format</span></span>
<span data-ttu-id="ff684-104">Wanneer een actie op een station Hallo Microsoft Azure Import/Export-service als onderdeel van een import-taak of een taak voor het exporteren uitvoert, worden logboeken tooblock blobs geschreven in Hallo storage-account dat is gekoppeld met deze taak.</span><span class="sxs-lookup"><span data-stu-id="ff684-104">When hello Microsoft Azure Import/Export service performs an action on a drive as part of an import job or an export job, logs are written tooblock blobs in hello storage account associated with that job.</span></span>  
  
<span data-ttu-id="ff684-105">Er zijn twee logboekbestanden die kunnen worden geschreven door Hallo Import/Export-service:</span><span class="sxs-lookup"><span data-stu-id="ff684-105">There are two logs that may be written by hello Import/Export service:</span></span>  
  
-   <span data-ttu-id="ff684-106">Hallo-foutenlogboek is altijd Hallo geval van een fout gegenereerd.</span><span class="sxs-lookup"><span data-stu-id="ff684-106">hello error log is always generated in hello event of an error.</span></span>  
  
-   <span data-ttu-id="ff684-107">Hallo uitgebreide logboek is standaard niet ingeschakeld, maar kan worden ingeschakeld door de instelling Hallo `EnableVerboseLog` -eigenschap op een [taak plaatsen](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) of [Update taakeigenschappen](/rest/api/storageimportexport/jobs#Jobs_Update) bewerking.</span><span class="sxs-lookup"><span data-stu-id="ff684-107">hello verbose log is not enabled by default, but may be enabled by setting hello `EnableVerboseLog` property on a [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation.</span></span>  
  
## <a name="log-file-location"></a><span data-ttu-id="ff684-108">De locatie van logboekbestand</span><span class="sxs-lookup"><span data-stu-id="ff684-108">Log file location</span></span>  
<span data-ttu-id="ff684-109">Hallo Logboeken geschreven tooblock blobs in Hallo-container of virtuele map die is opgegeven door Hallo `ImportExportStatesPath` instelling, die u kunt instellen op een `Put Job` bewerking.</span><span class="sxs-lookup"><span data-stu-id="ff684-109">hello logs are written tooblock blobs in hello container or virtual directory specified by hello `ImportExportStatesPath` setting, which you can set on a `Put Job` operation.</span></span> <span data-ttu-id="ff684-110">Hallo locatie toowhich Hallo Logboeken geschreven is afhankelijk van hoe verificatie is opgegeven voor de taak hello, samen met de Hallo-waarde opgegeven voor `ImportExportStatesPath`.</span><span class="sxs-lookup"><span data-stu-id="ff684-110">hello location toowhich hello logs are written depends on how authentication is specified for hello job, together with hello value specified for `ImportExportStatesPath`.</span></span> <span data-ttu-id="ff684-111">Verificatie voor Hallo taak mag worden opgegeven via de sleutel van een opslagaccount of een container SAS (shared access signature).</span><span class="sxs-lookup"><span data-stu-id="ff684-111">Authentication for hello job may be specified via a storage account key, or a container SAS (shared access signature).</span></span>  
  
<span data-ttu-id="ff684-112">Hallo-naam van het Hallo-container of virtuele map kan ofwel worden de standaardnaam Hallo van `waimportexport`, of een andere container of de naam van de virtuele map die u opgeeft.</span><span class="sxs-lookup"><span data-stu-id="ff684-112">hello name of hello container or virtual directory may either be hello default name of `waimportexport`, or another container or virtual directory name that you specify.</span></span>  
  
<span data-ttu-id="ff684-113">Hallo in de volgende tabel ziet u Hallo mogelijke opties:</span><span class="sxs-lookup"><span data-stu-id="ff684-113">hello table below shows hello possible options:</span></span>  
  
|<span data-ttu-id="ff684-114">Verificatiemethode</span><span class="sxs-lookup"><span data-stu-id="ff684-114">Authentication Method</span></span>|<span data-ttu-id="ff684-115">Waarde van `ImportExportStatesPath`Element</span><span class="sxs-lookup"><span data-stu-id="ff684-115">Value of `ImportExportStatesPath`Element</span></span>|<span data-ttu-id="ff684-116">Locatie van het logboek Blobs</span><span class="sxs-lookup"><span data-stu-id="ff684-116">Location of Log Blobs</span></span>|  
|---------------------------|----------------------------------------------|---------------------------|  
|<span data-ttu-id="ff684-117">De sleutel van opslagaccount</span><span class="sxs-lookup"><span data-stu-id="ff684-117">Storage account key</span></span>|<span data-ttu-id="ff684-118">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="ff684-118">Default value</span></span>|<span data-ttu-id="ff684-119">Een container met de naam `waimportexport`, die de standaardcontainer Hallo is.</span><span class="sxs-lookup"><span data-stu-id="ff684-119">A container named `waimportexport`, which is hello default container.</span></span> <span data-ttu-id="ff684-120">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ff684-120">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|<span data-ttu-id="ff684-121">De sleutel van opslagaccount</span><span class="sxs-lookup"><span data-stu-id="ff684-121">Storage account key</span></span>|<span data-ttu-id="ff684-122">Gebruiker opgegeven waarde</span><span class="sxs-lookup"><span data-stu-id="ff684-122">User-specified value</span></span>|<span data-ttu-id="ff684-123">Een container met de naam door Hallo-gebruiker.</span><span class="sxs-lookup"><span data-stu-id="ff684-123">A container named by hello user.</span></span> <span data-ttu-id="ff684-124">Bijvoorbeeld:</span><span class="sxs-lookup"><span data-stu-id="ff684-124">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|<span data-ttu-id="ff684-125">Container SAS</span><span class="sxs-lookup"><span data-stu-id="ff684-125">Container SAS</span></span>|<span data-ttu-id="ff684-126">Standaardwaarde</span><span class="sxs-lookup"><span data-stu-id="ff684-126">Default value</span></span>|<span data-ttu-id="ff684-127">Een virtuele map met de naam `waimportexport`, dit is de standaardnaam Hallo onder Hallo-container die zijn opgegeven in Hallo SAS.</span><span class="sxs-lookup"><span data-stu-id="ff684-127">A virtual directory named `waimportexport`, which is hello default name, beneath hello container specified in hello SAS.</span></span><br /><br /> <span data-ttu-id="ff684-128">Bijvoorbeeld, als Hallo SAS voor het opgegeven Hallo-taak is `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, en vervolgens de locatie van het logboekbestand Hallo zou zijn`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span><span class="sxs-lookup"><span data-stu-id="ff684-128">For example, if hello SAS specified for hello job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, then hello log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span></span>|  
|<span data-ttu-id="ff684-129">Container SAS</span><span class="sxs-lookup"><span data-stu-id="ff684-129">Container SAS</span></span>|<span data-ttu-id="ff684-130">Gebruiker opgegeven waarde</span><span class="sxs-lookup"><span data-stu-id="ff684-130">User-specified value</span></span>|<span data-ttu-id="ff684-131">Een virtuele map met de naam van de gebruiker hello, onder Hallo-container die zijn opgegeven in Hallo SAS.</span><span class="sxs-lookup"><span data-stu-id="ff684-131">A virtual directory named by hello user, beneath hello container specified in hello SAS.</span></span><br /><br /> <span data-ttu-id="ff684-132">Bijvoorbeeld, als Hallo SAS voor het opgegeven Hallo-taak is `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, en Hallo opgegeven virtuele map heet `mylogblobs`, en vervolgens de locatie van het logboekbestand Hallo zou worden `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span><span class="sxs-lookup"><span data-stu-id="ff684-132">For example, if hello SAS specified for hello job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, and hello specified virtual directory is named `mylogblobs`, then hello log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span></span>|  
  
<span data-ttu-id="ff684-133">U kunt aanroepen Hallo Hallo-URL voor Hallo foutinformatie en de uitgebreide logboeken ophalen [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) bewerking.</span><span class="sxs-lookup"><span data-stu-id="ff684-133">You can retrieve hello URL for hello error and verbose logs by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="ff684-134">Hallo logboeken zijn beschikbaar nadat de verwerking van Hallo station is voltooid.</span><span class="sxs-lookup"><span data-stu-id="ff684-134">hello logs are available after processing of hello drive is complete.</span></span>  
  
## <a name="log-file-format"></a><span data-ttu-id="ff684-135">Indeling van logboekbestand</span><span class="sxs-lookup"><span data-stu-id="ff684-135">Log file format</span></span>  
<span data-ttu-id="ff684-136">Hallo-indeling voor beide logboeken is Hallo dezelfde: een blob met beschrijvingen van Hallo-gebeurtenissen die zijn opgetreden tijdens het kopiëren van BLOB's tussen Hallo harde schijf en Hallo klantaccount XML.</span><span class="sxs-lookup"><span data-stu-id="ff684-136">hello format for both logs is hello same: a blob containing XML descriptions of hello events that occurred while copying blobs between hello hard drive and hello customer's account.</span></span>  
  
<span data-ttu-id="ff684-137">Hallo uitgebreide logboek bevat volledige informatie over Hallo status van de kopieerbewerking Hallo voor elke blob (voor een import-taak) of het bestand (voor een exporttaak) terwijl Hallo foutenlogboek bevat alleen informatie Hallo voor blobs of bestanden die fouten tijdens het Hallo aangetroffen importeren of exporteren van de taak.</span><span class="sxs-lookup"><span data-stu-id="ff684-137">hello verbose log contains complete information about hello status of hello copy operation for every blob (for an import job) or file (for an export job), whereas hello error log contains only hello information for blobs or files that encountered errors during hello import or export job.</span></span>  
  
<span data-ttu-id="ff684-138">Hallo uitgebreide logboekindeling worden hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ff684-138">hello verbose log format is shown below.</span></span> <span data-ttu-id="ff684-139">Hallo-foutenlogboek heeft Hallo dezelfde structuur, maar geslaagde bewerkingen, worden uitgefilterd.</span><span class="sxs-lookup"><span data-stu-id="ff684-139">hello error log has hello same structure, but filters out successful operations.</span></span>  

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

<span data-ttu-id="ff684-140">Hallo beschrijft volgende tabel Hallo elementen van het logboekbestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="ff684-140">hello following table describes hello elements of hello log file.</span></span>  
  
|<span data-ttu-id="ff684-141">XML-Element</span><span class="sxs-lookup"><span data-stu-id="ff684-141">XML Element</span></span>|<span data-ttu-id="ff684-142">Type</span><span class="sxs-lookup"><span data-stu-id="ff684-142">Type</span></span>|<span data-ttu-id="ff684-143">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ff684-143">Description</span></span>|  
|-----------------|----------|-----------------|  
|`DriveLog`|<span data-ttu-id="ff684-144">XML-Element</span><span class="sxs-lookup"><span data-stu-id="ff684-144">XML Element</span></span>|<span data-ttu-id="ff684-145">Hiermee geeft u een station voor logboekbestanden.</span><span class="sxs-lookup"><span data-stu-id="ff684-145">Represents a drive log.</span></span>|  
|`Version`|<span data-ttu-id="ff684-146">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ff684-146">Attribute, String</span></span>|<span data-ttu-id="ff684-147">Hallo-versie van Hallo-logboekindeling.</span><span class="sxs-lookup"><span data-stu-id="ff684-147">hello version of hello log format.</span></span>|  
|`DriveId`|<span data-ttu-id="ff684-148">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ff684-148">String</span></span>|<span data-ttu-id="ff684-149">Hallo serienummer van het station-hardware.</span><span class="sxs-lookup"><span data-stu-id="ff684-149">hello drive's hardware serial number.</span></span>|  
|`Status`|<span data-ttu-id="ff684-150">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ff684-150">String</span></span>|<span data-ttu-id="ff684-151">Status van Hallo station verwerking.</span><span class="sxs-lookup"><span data-stu-id="ff684-151">Status of hello drive processing.</span></span> <span data-ttu-id="ff684-152">Zie Hallo `Drive Status Codes` tabel hieronder voor meer informatie.</span><span class="sxs-lookup"><span data-stu-id="ff684-152">See hello `Drive Status Codes` table below for more information.</span></span>|  
|`Blob`|<span data-ttu-id="ff684-153">Geneste XML-element</span><span class="sxs-lookup"><span data-stu-id="ff684-153">Nested XML element</span></span>|<span data-ttu-id="ff684-154">Hiermee geeft u een blob.</span><span class="sxs-lookup"><span data-stu-id="ff684-154">Represents a blob.</span></span>|  
|`Blob/BlobPath`|<span data-ttu-id="ff684-155">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ff684-155">String</span></span>|<span data-ttu-id="ff684-156">Hallo-URI van Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="ff684-156">hello URI of hello blob.</span></span>|  
|`Blob/FilePath`|<span data-ttu-id="ff684-157">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ff684-157">String</span></span>|<span data-ttu-id="ff684-158">Hallo relatief pad toohello bestand op Hallo-station.</span><span class="sxs-lookup"><span data-stu-id="ff684-158">hello relative path toohello file on hello drive.</span></span>|  
|`Blob/Snapshot`|<span data-ttu-id="ff684-159">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="ff684-159">DateTime</span></span>|<span data-ttu-id="ff684-160">Hallo momentopname versie van de blob hello, voor een exporttaak.</span><span class="sxs-lookup"><span data-stu-id="ff684-160">hello snapshot version of hello blob, for an export job only.</span></span>|  
|`Blob/Length`|<span data-ttu-id="ff684-161">Geheel getal</span><span class="sxs-lookup"><span data-stu-id="ff684-161">Integer</span></span>|<span data-ttu-id="ff684-162">Hallo totale lengte van de blob Hallo in bytes.</span><span class="sxs-lookup"><span data-stu-id="ff684-162">hello total length of hello blob in bytes.</span></span>|  
|`Blob/LastModified`|<span data-ttu-id="ff684-163">Datum/tijd</span><span class="sxs-lookup"><span data-stu-id="ff684-163">DateTime</span></span>|<span data-ttu-id="ff684-164">Hallo datum/tijd Hallo blob voor een exporttaak het laatst is gewijzigd.</span><span class="sxs-lookup"><span data-stu-id="ff684-164">hello date/time that hello blob was last modified, for an export job only.</span></span>|  
|`Blob/ImportDisposition`|<span data-ttu-id="ff684-165">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ff684-165">String</span></span>|<span data-ttu-id="ff684-166">Hallo disposition Hallo BLOB, voor een import-taak alleen importeren.</span><span class="sxs-lookup"><span data-stu-id="ff684-166">hello import disposition of hello blob, for an import job only.</span></span>|  
|`Blob/ImportDisposition/@Status`|<span data-ttu-id="ff684-167">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ff684-167">Attribute, String</span></span>|<span data-ttu-id="ff684-168">Hallo-status van Hallo importeren toestand.</span><span class="sxs-lookup"><span data-stu-id="ff684-168">hello status of hello import disposition.</span></span>|  
|`PageRangeList`|<span data-ttu-id="ff684-169">Geneste XML-element</span><span class="sxs-lookup"><span data-stu-id="ff684-169">Nested XML element</span></span>|<span data-ttu-id="ff684-170">Hiermee geeft u een lijst met paginabereiken voor een pagina-blob.</span><span class="sxs-lookup"><span data-stu-id="ff684-170">Represents a list of page ranges for a page blob.</span></span>|  
|`PageRange`|<span data-ttu-id="ff684-171">XML-element</span><span class="sxs-lookup"><span data-stu-id="ff684-171">XML element</span></span>|<span data-ttu-id="ff684-172">Hiermee geeft u een paginabereik.</span><span class="sxs-lookup"><span data-stu-id="ff684-172">Represents a page range.</span></span>|  
|`PageRange/@Offset`|<span data-ttu-id="ff684-173">Kenmerk, geheel getal</span><span class="sxs-lookup"><span data-stu-id="ff684-173">Attribute, Integer</span></span>|<span data-ttu-id="ff684-174">Hallo blob vanaf verschuiving van Hallo paginabereik.</span><span class="sxs-lookup"><span data-stu-id="ff684-174">Starting offset of hello page range in hello blob.</span></span>|  
|`PageRange/@Length`|<span data-ttu-id="ff684-175">Kenmerk, geheel getal</span><span class="sxs-lookup"><span data-stu-id="ff684-175">Attribute, Integer</span></span>|<span data-ttu-id="ff684-176">De lengte in bytes van Hallo paginabereik.</span><span class="sxs-lookup"><span data-stu-id="ff684-176">Length in bytes of hello page range.</span></span>|  
|`PageRange/@Hash`|<span data-ttu-id="ff684-177">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ff684-177">Attribute, String</span></span>|<span data-ttu-id="ff684-178">Base16 gecodeerd MD5-hash van Hallo paginabereik.</span><span class="sxs-lookup"><span data-stu-id="ff684-178">Base16-encoded MD5 hash of hello page range.</span></span>|  
|`PageRange/@Status`|<span data-ttu-id="ff684-179">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ff684-179">Attribute, String</span></span>|<span data-ttu-id="ff684-180">Status van de verwerking van Hallo paginabereik.</span><span class="sxs-lookup"><span data-stu-id="ff684-180">Status of processing hello page range.</span></span>|  
|`BlockList`|<span data-ttu-id="ff684-181">Geneste XML-element</span><span class="sxs-lookup"><span data-stu-id="ff684-181">Nested XML element</span></span>|<span data-ttu-id="ff684-182">Hiermee geeft u een lijst met bouwstenen voor een blok-blob.</span><span class="sxs-lookup"><span data-stu-id="ff684-182">Represents a list of blocks for a block blob.</span></span>|  
|`Block`|<span data-ttu-id="ff684-183">XML-element</span><span class="sxs-lookup"><span data-stu-id="ff684-183">XML element</span></span>|<span data-ttu-id="ff684-184">Hiermee geeft u een blok.</span><span class="sxs-lookup"><span data-stu-id="ff684-184">Represents a block.</span></span>|  
|`Block/@Offset`|<span data-ttu-id="ff684-185">Kenmerk, geheel getal</span><span class="sxs-lookup"><span data-stu-id="ff684-185">Attribute, Integer</span></span>|<span data-ttu-id="ff684-186">Vanaf verschuiving van Hallo blok Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="ff684-186">Starting offset of hello block in hello blob.</span></span>|  
|`Block/@Length`|<span data-ttu-id="ff684-187">Kenmerk, geheel getal</span><span class="sxs-lookup"><span data-stu-id="ff684-187">Attribute, Integer</span></span>|<span data-ttu-id="ff684-188">De lengte in bytes van Hallo blok.</span><span class="sxs-lookup"><span data-stu-id="ff684-188">Length in bytes of hello block.</span></span>|  
|`Block/@Id`|<span data-ttu-id="ff684-189">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ff684-189">Attribute, String</span></span>|<span data-ttu-id="ff684-190">Hallo-blok-id.</span><span class="sxs-lookup"><span data-stu-id="ff684-190">hello block ID.</span></span>|  
|`Block/@Hash`|<span data-ttu-id="ff684-191">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ff684-191">Attribute, String</span></span>|<span data-ttu-id="ff684-192">Base16 gecodeerd MD5-hash van Hallo blok.</span><span class="sxs-lookup"><span data-stu-id="ff684-192">Base16-encoded MD5 hash of hello block.</span></span>|  
|`Block/@Status`|<span data-ttu-id="ff684-193">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ff684-193">Attribute, String</span></span>|<span data-ttu-id="ff684-194">Status van de verwerking van Hallo blok.</span><span class="sxs-lookup"><span data-stu-id="ff684-194">Status of processing hello block.</span></span>|  
|`Metadata`|<span data-ttu-id="ff684-195">Geneste XML-element</span><span class="sxs-lookup"><span data-stu-id="ff684-195">Nested XML element</span></span>|<span data-ttu-id="ff684-196">Hallo blobmetagegevens vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="ff684-196">Represents hello blob's metadata.</span></span>|  
|`Metadata/@Status`|<span data-ttu-id="ff684-197">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ff684-197">Attribute, String</span></span>|<span data-ttu-id="ff684-198">Status van de verwerking van Hallo blobmetagegevens.</span><span class="sxs-lookup"><span data-stu-id="ff684-198">Status of processing of hello blob metadata.</span></span>|  
|`Metadata/GlobalPath`|<span data-ttu-id="ff684-199">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ff684-199">String</span></span>|<span data-ttu-id="ff684-200">Relatief pad toohello globale metagegevensbestand.</span><span class="sxs-lookup"><span data-stu-id="ff684-200">Relative path toohello global metadata file.</span></span>|  
|`Metadata/GlobalPath/@Hash`|<span data-ttu-id="ff684-201">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ff684-201">Attribute, String</span></span>|<span data-ttu-id="ff684-202">Base16 gecodeerd MD5-hash van de globale metagegevensbestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="ff684-202">Base16-encoded MD5 hash of hello global metadata file.</span></span>|  
|`Metadata/Path`|<span data-ttu-id="ff684-203">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ff684-203">String</span></span>|<span data-ttu-id="ff684-204">Relatief pad toohello metagegevensbestand.</span><span class="sxs-lookup"><span data-stu-id="ff684-204">Relative path toohello metadata file.</span></span>|  
|`Metadata/Path/@Hash`|<span data-ttu-id="ff684-205">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ff684-205">Attribute, String</span></span>|<span data-ttu-id="ff684-206">Base16 gecodeerd MD5-hash van het metagegevensbestand Hallo.</span><span class="sxs-lookup"><span data-stu-id="ff684-206">Base16-encoded MD5 hash of hello metadata file.</span></span>|  
|`Properties`|<span data-ttu-id="ff684-207">Geneste XML-element</span><span class="sxs-lookup"><span data-stu-id="ff684-207">Nested XML element</span></span>|<span data-ttu-id="ff684-208">Hallo blob eigenschappen vertegenwoordigt.</span><span class="sxs-lookup"><span data-stu-id="ff684-208">Represents hello blob properties.</span></span>|  
|`Properties/@Status`|<span data-ttu-id="ff684-209">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ff684-209">Attribute, String</span></span>|<span data-ttu-id="ff684-210">Status van de verwerking van Hallo blob-eigenschappen, bijvoorbeeld bestand niet gevonden, voltooid.</span><span class="sxs-lookup"><span data-stu-id="ff684-210">Status of processing hello blob properties, e.g. file not found, completed.</span></span>|  
|`Properties/GlobalPath`|<span data-ttu-id="ff684-211">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ff684-211">String</span></span>|<span data-ttu-id="ff684-212">Relatief pad toohello algemene eigenschappenbestand.</span><span class="sxs-lookup"><span data-stu-id="ff684-212">Relative path toohello global properties file.</span></span>|  
|`Properties/GlobalPath/@Hash`|<span data-ttu-id="ff684-213">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ff684-213">Attribute, String</span></span>|<span data-ttu-id="ff684-214">Base16 gecodeerd MD5-hash van Hallo algemene eigenschappenbestand.</span><span class="sxs-lookup"><span data-stu-id="ff684-214">Base16-encoded MD5 hash of hello global properties file.</span></span>|  
|`Properties/Path`|<span data-ttu-id="ff684-215">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ff684-215">String</span></span>|<span data-ttu-id="ff684-216">Relatief pad toohello eigenschappenbestand.</span><span class="sxs-lookup"><span data-stu-id="ff684-216">Relative path toohello properties file.</span></span>|  
|`Properties/Path/@Hash`|<span data-ttu-id="ff684-217">Kenmerk, tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ff684-217">Attribute, String</span></span>|<span data-ttu-id="ff684-218">Base16 gecodeerd MD5-hash van Hallo eigenschappenbestand.</span><span class="sxs-lookup"><span data-stu-id="ff684-218">Base16-encoded MD5 hash of hello properties file.</span></span>|  
|`Blob/Status`|<span data-ttu-id="ff684-219">Tekenreeks</span><span class="sxs-lookup"><span data-stu-id="ff684-219">String</span></span>|<span data-ttu-id="ff684-220">De status van de verwerking van Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="ff684-220">Status of processing hello blob.</span></span>|  
  
# <a name="drive-status-codes"></a><span data-ttu-id="ff684-221">Statuscodes van station</span><span class="sxs-lookup"><span data-stu-id="ff684-221">Drive status codes</span></span>  
<span data-ttu-id="ff684-222">Hallo bevat volgende tabel de statuscodes Hallo voor het verwerken van een station.</span><span class="sxs-lookup"><span data-stu-id="ff684-222">hello following table lists hello status codes for processing a drive.</span></span>  
  
|<span data-ttu-id="ff684-223">Statuscode</span><span class="sxs-lookup"><span data-stu-id="ff684-223">Status code</span></span>|<span data-ttu-id="ff684-224">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ff684-224">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="ff684-225">Hallo-station heeft verwerking zonder fouten voltooid.</span><span class="sxs-lookup"><span data-stu-id="ff684-225">hello drive has finished processing without any errors.</span></span>|  
|`CompletedWithWarnings`|<span data-ttu-id="ff684-226">Hallo-station zijn verwerkt met waarschuwingen in een of meer blobs per Hallo importeren dispositions opgegeven voor Hallo blobs.</span><span class="sxs-lookup"><span data-stu-id="ff684-226">hello drive has finished processing with warnings in one or more blobs per hello import dispositions specified for hello blobs.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="ff684-227">Hallo-station is voltooid met fouten in een of meer blobs of segmenten.</span><span class="sxs-lookup"><span data-stu-id="ff684-227">hello drive has finished with errors in one or more blobs or chunks.</span></span>|  
|`DiskNotFound`|<span data-ttu-id="ff684-228">Er is geen schijf is gevonden op Hallo-station.</span><span class="sxs-lookup"><span data-stu-id="ff684-228">No disk is found on hello drive.</span></span>|  
|`VolumeNotNtfs`|<span data-ttu-id="ff684-229">Hallo eerste gegevensvolume op Hallo schijf is niet in de NTFS-indeling.</span><span class="sxs-lookup"><span data-stu-id="ff684-229">hello first data volume on hello disk is not in NTFS format.</span></span>|  
|`DiskOperationFailed`|<span data-ttu-id="ff684-230">Een onbekende fout opgetreden bij het uitvoeren van bewerkingen op Hallo station.</span><span class="sxs-lookup"><span data-stu-id="ff684-230">An unknown failure occurred when performing operations on hello drive.</span></span>|  
|`BitLockerVolumeNotFound`|<span data-ttu-id="ff684-231">Er is geen BitLocker encryptable volume gevonden.</span><span class="sxs-lookup"><span data-stu-id="ff684-231">No BitLocker encryptable volume is found.</span></span>|  
|`BitLockerNotActivated`|<span data-ttu-id="ff684-232">BitLocker is niet ingeschakeld op Hallo volume.</span><span class="sxs-lookup"><span data-stu-id="ff684-232">BitLocker is not enabled on hello volume.</span></span>|  
|`BitLockerProtectorNotFound`|<span data-ttu-id="ff684-233">Hallo numerieke wachtwoordsleutelbeveiliging bestaat niet op Hallo volume.</span><span class="sxs-lookup"><span data-stu-id="ff684-233">hello numerical password key protector does not exist on hello volume.</span></span>|  
|`BitLockerKeyInvalid`|<span data-ttu-id="ff684-234">Hallo numerieke opgegeven wachtwoord ontgrendelen niet Hallo volume.</span><span class="sxs-lookup"><span data-stu-id="ff684-234">hello numerical password provided cannot unlock hello volume.</span></span>|  
|`BitLockerUnlockVolumeFailed`|<span data-ttu-id="ff684-235">Is een onbekende fout opgetreden bij het toounlock Hallo volume.</span><span class="sxs-lookup"><span data-stu-id="ff684-235">Unknown failure has happened when trying toounlock hello volume.</span></span>|  
|`BitLockerFailed`|<span data-ttu-id="ff684-236">Een onbekende fout opgetreden tijdens het uitvoeren van BitLocker-bewerkingen.</span><span class="sxs-lookup"><span data-stu-id="ff684-236">An unknown failure occurred while performing BitLocker operations.</span></span>|  
|`ManifestNameInvalid`|<span data-ttu-id="ff684-237">Hallo manifestbestand naam is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="ff684-237">hello manifest file name is invalid.</span></span>|  
|`ManifestNameTooLong`|<span data-ttu-id="ff684-238">Hallo manifestbestand naam is te lang.</span><span class="sxs-lookup"><span data-stu-id="ff684-238">hello manifest file name is too long.</span></span>|  
|`ManifestNotFound`|<span data-ttu-id="ff684-239">Hallo-manifestbestand is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="ff684-239">hello manifest file is not found.</span></span>|  
|`ManifestAccessDenied`|<span data-ttu-id="ff684-240">Manifestbestand van de toohello toegang is geweigerd.</span><span class="sxs-lookup"><span data-stu-id="ff684-240">Access toohello manifest file is denied.</span></span>|  
|`ManifestCorrupted`|<span data-ttu-id="ff684-241">Hallo manifestbestand is beschadigd (Hallo inhoud komt niet overeen met de hash).</span><span class="sxs-lookup"><span data-stu-id="ff684-241">hello manifest file is corrupted (hello content does not match its hash).</span></span>|  
|`ManifestFormatInvalid`|<span data-ttu-id="ff684-242">Hallo manifest inhoud komt niet overeen voor vereiste toohello-indeling.</span><span class="sxs-lookup"><span data-stu-id="ff684-242">hello manifest content does not conform toohello required format.</span></span>|  
|`ManifestDriveIdMismatch`|<span data-ttu-id="ff684-243">Hallo-ID in het manifestbestand Hallo komt niet overeen met een van Hallo station lezen Hallo station.</span><span class="sxs-lookup"><span data-stu-id="ff684-243">hello drive ID in hello manifest file does not match hello one read from hello drive.</span></span>|  
|`ReadManifestFailed`|<span data-ttu-id="ff684-244">Er is een schijf-i/o-fout opgetreden tijdens het lezen van Hallo manifest.</span><span class="sxs-lookup"><span data-stu-id="ff684-244">A disk I/O failure occurred while reading from hello manifest.</span></span>|  
|`BlobListFormatInvalid`|<span data-ttu-id="ff684-245">Hallo export blob lijst blob komt niet overeen voor vereiste toohello-indeling.</span><span class="sxs-lookup"><span data-stu-id="ff684-245">hello export blob list blob does not conform toohello required format.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="ff684-246">Toegang tot toohello blobs in Hallo storage-account is niet toegestaan.</span><span class="sxs-lookup"><span data-stu-id="ff684-246">Access toohello blobs in hello storage account is forbidden.</span></span> <span data-ttu-id="ff684-247">Dit kan zijn vanwege de opslagaccountsleutel tooinvalid of SAS-container.</span><span class="sxs-lookup"><span data-stu-id="ff684-247">This might be due tooinvalid storage account key or container SAS.</span></span>|  
|`InternalError`|<span data-ttu-id="ff684-248">En er is een interne fout opgetreden tijdens het verwerken van Hallo-station.</span><span class="sxs-lookup"><span data-stu-id="ff684-248">And internal error occurred while processing hello drive.</span></span>|  
  
## <a name="blob-status-codes"></a><span data-ttu-id="ff684-249">Statuscodes BLOB</span><span class="sxs-lookup"><span data-stu-id="ff684-249">Blob status codes</span></span>  
<span data-ttu-id="ff684-250">Hallo bevat volgende tabel de statuscodes Hallo voor het verwerken van een blob.</span><span class="sxs-lookup"><span data-stu-id="ff684-250">hello following table lists hello status codes for processing a blob.</span></span>  
  
|<span data-ttu-id="ff684-251">Statuscode</span><span class="sxs-lookup"><span data-stu-id="ff684-251">Status code</span></span>|<span data-ttu-id="ff684-252">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ff684-252">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="ff684-253">Hallo blob heeft verwerking zonder fouten voltooid.</span><span class="sxs-lookup"><span data-stu-id="ff684-253">hello blob has finished processing without errors.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="ff684-254">Hallo blob zijn met fouten in een of meer paginabereiken of blokken, metagegevens of eigenschappen verwerkt.</span><span class="sxs-lookup"><span data-stu-id="ff684-254">hello blob has finished processing with errors in one or more page ranges or blocks, metadata, or properties.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="ff684-255">Hallo-bestandsnaam is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="ff684-255">hello file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="ff684-256">Hallo-bestandsnaam is te lang.</span><span class="sxs-lookup"><span data-stu-id="ff684-256">hello file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="ff684-257">Hallo-bestand is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="ff684-257">hello file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="ff684-258">Toegang tot toohello bestand is geweigerd.</span><span class="sxs-lookup"><span data-stu-id="ff684-258">Access toohello file is denied.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="ff684-259">Hallo Blob-serviceaanvraag tooaccess Hallo blob is mislukt.</span><span class="sxs-lookup"><span data-stu-id="ff684-259">hello Blob service request tooaccess hello blob has failed.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="ff684-260">Hallo Blob-serviceaanvraag tooaccess Hallo blob is verboden.</span><span class="sxs-lookup"><span data-stu-id="ff684-260">hello Blob service request tooaccess hello blob is forbidden.</span></span> <span data-ttu-id="ff684-261">Dit kan zijn vanwege de opslagaccountsleutel tooinvalid of SAS-container.</span><span class="sxs-lookup"><span data-stu-id="ff684-261">This might be due tooinvalid storage account key or container SAS.</span></span>|  
|`RenameFailed`|<span data-ttu-id="ff684-262">Kan toorename Hallo-blob (voor een import-taak) of Hallo-bestand (voor een taak voor het exporteren).</span><span class="sxs-lookup"><span data-stu-id="ff684-262">Failed toorename hello blob (for an import job) or hello file (for an export job).</span></span>|  
|`BlobUnexpectedChange`|<span data-ttu-id="ff684-263">Onverwachte wijziging is opgetreden met de blob hello (voor een taak voor het exporteren).</span><span class="sxs-lookup"><span data-stu-id="ff684-263">An unexpected change has occurred with hello blob (for an export job).</span></span>|  
|`LeasePresent`|<span data-ttu-id="ff684-264">Er is een lease aanwezig is op Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="ff684-264">There is a lease present on hello blob.</span></span>|  
|`IOFailed`|<span data-ttu-id="ff684-265">Een schijf of een netwerk-i/o-fout is opgetreden tijdens het verwerken van Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="ff684-265">A disk or network I/O failure occurred while processing hello blob.</span></span>|  
|`Failed`|<span data-ttu-id="ff684-266">Een onbekende fout opgetreden tijdens het verwerken van Hallo blob.</span><span class="sxs-lookup"><span data-stu-id="ff684-266">An unknown failure occurred while processing hello blob.</span></span>|  
  
## <a name="import-disposition-status-codes"></a><span data-ttu-id="ff684-267">Statuscodes disposition importeren</span><span class="sxs-lookup"><span data-stu-id="ff684-267">Import disposition status codes</span></span>  
<span data-ttu-id="ff684-268">Hallo bevat volgende tabel Hallo statuscodes voor het oplossen van een toestand importeren.</span><span class="sxs-lookup"><span data-stu-id="ff684-268">hello following table lists hello status codes for resolving an import disposition.</span></span>  
  
|<span data-ttu-id="ff684-269">Statuscode</span><span class="sxs-lookup"><span data-stu-id="ff684-269">Status code</span></span>|<span data-ttu-id="ff684-270">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ff684-270">Description</span></span>|  
|-----------------|-----------------|  
|`Created`|<span data-ttu-id="ff684-271">Hallo-blob is gemaakt.</span><span class="sxs-lookup"><span data-stu-id="ff684-271">hello blob has been created.</span></span>|  
|`Renamed`|<span data-ttu-id="ff684-272">Hallo blob heeft per rename importeren bestemming gekregen.</span><span class="sxs-lookup"><span data-stu-id="ff684-272">hello blob has been renamed per rename import disposition.</span></span> <span data-ttu-id="ff684-273">Hallo `Blob/BlobPath` element Hallo URI voor Hallo hernoemd blob bevat.</span><span class="sxs-lookup"><span data-stu-id="ff684-273">hello `Blob/BlobPath` element contains hello URI for hello renamed blob.</span></span>|  
|`Skipped`|<span data-ttu-id="ff684-274">Hallo-blob is overgeslagen `no-overwrite` toestand importeren.</span><span class="sxs-lookup"><span data-stu-id="ff684-274">hello blob has been skipped per `no-overwrite` import disposition.</span></span>|  
|`Overwritten`|<span data-ttu-id="ff684-275">Hallo blob heeft een bestaande blob per overschreven `overwrite` toestand importeren.</span><span class="sxs-lookup"><span data-stu-id="ff684-275">hello blob has overwritten an existing blob per `overwrite` import disposition.</span></span>|  
|`Cancelled`|<span data-ttu-id="ff684-276">Een eerdere fout is gestopt verdere verwerking van Hallo importeren toestand.</span><span class="sxs-lookup"><span data-stu-id="ff684-276">A prior failure has stopped further processing of hello import disposition.</span></span>|  
  
## <a name="page-rangeblock-status-codes"></a><span data-ttu-id="ff684-277">Statuscodes voor pagina-bereik/blok</span><span class="sxs-lookup"><span data-stu-id="ff684-277">Page range/block status codes</span></span>  
<span data-ttu-id="ff684-278">Hallo bevat volgende tabel de statuscodes Hallo voor het verwerken van een paginabereik of een blok.</span><span class="sxs-lookup"><span data-stu-id="ff684-278">hello following table lists hello status codes for processing a page range or a block.</span></span>  
  
|<span data-ttu-id="ff684-279">Statuscode</span><span class="sxs-lookup"><span data-stu-id="ff684-279">Status code</span></span>|<span data-ttu-id="ff684-280">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ff684-280">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="ff684-281">Hallo paginabereik of blok is verwerking zonder fouten voltooid.</span><span class="sxs-lookup"><span data-stu-id="ff684-281">hello page range or block has finished processing without any errors.</span></span>|  
|`Committed`|<span data-ttu-id="ff684-282">Hallo blok is doorgevoerd, maar niet in Hallo volledige blokkeringslijst omdat andere blokken is mislukt, of de volledige lijst met geblokkeerde websites zelf plaatsen is mislukt.</span><span class="sxs-lookup"><span data-stu-id="ff684-282">hello block has been committed,  but not in hello full block list because other blocks have failed, or put full block list itself has failed.</span></span>|  
|`Uncommitted`|<span data-ttu-id="ff684-283">Hallo blok is geüpload, maar niet zijn doorgevoerd.</span><span class="sxs-lookup"><span data-stu-id="ff684-283">hello block is uploaded but not committed.</span></span>|  
|`Corrupted`|<span data-ttu-id="ff684-284">Hallo paginabereik of blok is beschadigd (Hallo inhoud komt niet overeen met de hash).</span><span class="sxs-lookup"><span data-stu-id="ff684-284">hello page range or block is corrupted (hello content does not match its hash).</span></span>|  
|`FileUnexpectedEnd`|<span data-ttu-id="ff684-285">Een onverwacht bestandseinde er is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="ff684-285">An unexpected end of file has been encountered.</span></span>|  
|`BlobUnexpectedEnd`|<span data-ttu-id="ff684-286">Een onverwacht einde van de blob is opgetreden.</span><span class="sxs-lookup"><span data-stu-id="ff684-286">An unexpected end of blob has been encountered.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="ff684-287">Hallo Blob serviceaanvraag tooaccess Hallo paginabereik of blok is mislukt.</span><span class="sxs-lookup"><span data-stu-id="ff684-287">hello Blob service request tooaccess hello page range or block has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="ff684-288">Een schijf of een netwerk-i/o-fout is opgetreden tijdens het verwerken van Hallo paginabereik of blok.</span><span class="sxs-lookup"><span data-stu-id="ff684-288">A disk or network I/O failure occurred while processing hello page range or block.</span></span>|  
|`Failed`|<span data-ttu-id="ff684-289">Een onbekende fout opgetreden tijdens het verwerken van Hallo paginabereik of blok.</span><span class="sxs-lookup"><span data-stu-id="ff684-289">An unknown failure occurred while processing hello page range or block.</span></span>|  
|`Cancelled`|<span data-ttu-id="ff684-290">Er is een eerdere fout gestopt verdere verwerking van het Hallo paginabereik of blok.</span><span class="sxs-lookup"><span data-stu-id="ff684-290">A prior failure has stopped further processing of hello page range or block.</span></span>|  
  
## <a name="metadata-status-codes"></a><span data-ttu-id="ff684-291">Statuscodes van metagegevens</span><span class="sxs-lookup"><span data-stu-id="ff684-291">Metadata status codes</span></span>  
<span data-ttu-id="ff684-292">Hallo bevat volgende tabel Hallo statuscodes voor verwerking van blob-metagegevens.</span><span class="sxs-lookup"><span data-stu-id="ff684-292">hello following table lists hello status codes for processing blob metadata.</span></span>  
  
|<span data-ttu-id="ff684-293">Statuscode</span><span class="sxs-lookup"><span data-stu-id="ff684-293">Status code</span></span>|<span data-ttu-id="ff684-294">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ff684-294">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="ff684-295">Hallo-metagegevens heeft verwerking zonder fouten voltooid.</span><span class="sxs-lookup"><span data-stu-id="ff684-295">hello metadata has finished processing without errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="ff684-296">Hallo metagegevens bestandsnaam is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="ff684-296">hello metadata file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="ff684-297">Hallo metagegevens bestandsnaam is te lang.</span><span class="sxs-lookup"><span data-stu-id="ff684-297">hello metadata file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="ff684-298">Hallo-metagegevensbestand is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="ff684-298">hello metadata file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="ff684-299">Bestand met metagegevens toohello toegang is geweigerd.</span><span class="sxs-lookup"><span data-stu-id="ff684-299">Access toohello metadata file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="ff684-300">Hallo metagegevensbestand is beschadigd (Hallo inhoud komt niet overeen met de hash).</span><span class="sxs-lookup"><span data-stu-id="ff684-300">hello metadata file is corrupted (hello content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="ff684-301">Hallo metagegevens inhoud komt niet overeen voor vereiste toohello-indeling.</span><span class="sxs-lookup"><span data-stu-id="ff684-301">hello metadata content does not conform toohello required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="ff684-302">Schrijven van Hallo metagegevens die is mislukt.</span><span class="sxs-lookup"><span data-stu-id="ff684-302">Writing hello metadata XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="ff684-303">Hallo Blob-serviceaanvraag tooaccess Hallo metagegevens is mislukt.</span><span class="sxs-lookup"><span data-stu-id="ff684-303">hello Blob service request tooaccess hello metadata has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="ff684-304">Een schijf of het netwerk-i/o-fout opgetreden tijdens het verwerken van Hallo metagegevens.</span><span class="sxs-lookup"><span data-stu-id="ff684-304">A disk or network I/O failure occurred while processing hello metadata.</span></span>|  
|`Failed`|<span data-ttu-id="ff684-305">Een onbekende fout opgetreden tijdens het verwerken van Hallo metagegevens.</span><span class="sxs-lookup"><span data-stu-id="ff684-305">An unknown failure occurred while processing hello metadata.</span></span>|  
|`Cancelled`|<span data-ttu-id="ff684-306">Een eerdere fout is gestopt verdere verwerking van Hallo metagegevens.</span><span class="sxs-lookup"><span data-stu-id="ff684-306">A prior failure has stopped further processing of hello metadata.</span></span>|  
  
## <a name="properties-status-codes"></a><span data-ttu-id="ff684-307">Statuscodes van eigenschappen</span><span class="sxs-lookup"><span data-stu-id="ff684-307">Properties status codes</span></span>  
<span data-ttu-id="ff684-308">Hallo bevat volgende tabel de statuscodes Hallo voor het verwerken van blob-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="ff684-308">hello following table lists hello status codes for processing blob properties.</span></span>  
  
|<span data-ttu-id="ff684-309">Statuscode</span><span class="sxs-lookup"><span data-stu-id="ff684-309">Status code</span></span>|<span data-ttu-id="ff684-310">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="ff684-310">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="ff684-311">Hallo eigenschappen verwerken zonder fouten is voltooid.</span><span class="sxs-lookup"><span data-stu-id="ff684-311">hello properties have finished processing without any errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="ff684-312">Hallo eigenschappen bestandsnaam is ongeldig.</span><span class="sxs-lookup"><span data-stu-id="ff684-312">hello properties file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="ff684-313">Hallo eigenschappen bestandsnaam is te lang.</span><span class="sxs-lookup"><span data-stu-id="ff684-313">hello properties file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="ff684-314">Hallo eigenschappenbestand is niet gevonden.</span><span class="sxs-lookup"><span data-stu-id="ff684-314">hello properties file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="ff684-315">Toegang tot toohello eigenschappenbestand is geweigerd.</span><span class="sxs-lookup"><span data-stu-id="ff684-315">Access toohello properties file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="ff684-316">Hallo eigenschappenbestand is beschadigd (Hallo inhoud komt niet overeen met de hash).</span><span class="sxs-lookup"><span data-stu-id="ff684-316">hello properties file is corrupted (hello content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="ff684-317">Hallo eigenschappen inhoud komt niet overeen voor vereiste toohello-indeling.</span><span class="sxs-lookup"><span data-stu-id="ff684-317">hello properties content does not conform toohello required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="ff684-318">Schrijven van Hallo-eigenschappen die is mislukt.</span><span class="sxs-lookup"><span data-stu-id="ff684-318">Writing hello properties XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="ff684-319">Hallo Blob-serviceaanvraag tooaccess Hallo eigenschappen is mislukt.</span><span class="sxs-lookup"><span data-stu-id="ff684-319">hello Blob service request tooaccess hello properties has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="ff684-320">Een schijf of het netwerk-i/o-fout opgetreden tijdens het verwerken van Hallo-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="ff684-320">A disk or network I/O failure occurred while processing hello properties.</span></span>|  
|`Failed`|<span data-ttu-id="ff684-321">Een onbekende fout opgetreden tijdens het verwerken van Hallo-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="ff684-321">An unknown failure occurred while processing hello properties.</span></span>|  
|`Cancelled`|<span data-ttu-id="ff684-322">Een eerdere fout is gestopt verdere verwerking van Hallo-eigenschappen.</span><span class="sxs-lookup"><span data-stu-id="ff684-322">A prior failure has stopped further processing of hello properties.</span></span>|  
  
## <a name="sample-logs"></a><span data-ttu-id="ff684-323">Voorbeeld-Logboeken</span><span class="sxs-lookup"><span data-stu-id="ff684-323">Sample logs</span></span>  
<span data-ttu-id="ff684-324">Hallo Hieronder volgt een voorbeeld van uitgebreide logboek.</span><span class="sxs-lookup"><span data-stu-id="ff684-324">hello following is an example of verbose log.</span></span>  
  
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
  
<span data-ttu-id="ff684-325">de bijbehorende foutenlogboek Hallo worden hieronder weergegeven.</span><span class="sxs-lookup"><span data-stu-id="ff684-325">hello corresponding error log is shown below.</span></span>  
  
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

 <span data-ttu-id="ff684-326">Hallo Volg-foutenlogboek voor een import-taak bevat een fout over een bestand niet gevonden op Hallo importeren station.</span><span class="sxs-lookup"><span data-stu-id="ff684-326">hello follow error log for an import job contains an error about a file not found on hello import drive.</span></span> <span data-ttu-id="ff684-327">Houd er rekening mee dat Hallo status van de volgende onderdelen is `Cancelled`.</span><span class="sxs-lookup"><span data-stu-id="ff684-327">Note that hello status of subsequent components is `Cancelled`.</span></span>  
  
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

<span data-ttu-id="ff684-328">Hallo volgende foutenlogboek voor een taak voor het exporteren geeft aan dat de blob-inhoud Hallo is geschreven toohello station, maar is een fout opgetreden tijdens het exporteren van de eigenschappen van het Hallo-blob.</span><span class="sxs-lookup"><span data-stu-id="ff684-328">hello following error log for an export job indicates that hello blob content has been successfully written toohello drive, but that an error occurred while exporting hello blob's properties.</span></span>  
  
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
  
## <a name="next-steps"></a><span data-ttu-id="ff684-329">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ff684-329">Next steps</span></span>
 
* [<span data-ttu-id="ff684-330">REST-API van Storage Import/Export</span><span class="sxs-lookup"><span data-stu-id="ff684-330">Storage Import/Export REST API</span></span>](/rest/api/storageimportexport/)
