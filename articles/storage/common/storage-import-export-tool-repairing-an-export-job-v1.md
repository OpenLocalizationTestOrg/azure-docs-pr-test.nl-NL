---
title: een exporttaak Azure Import/Export - v1 aaaRepairing | Microsoft Docs
description: Meer informatie over hoe toorepair een exporttaak die is gemaakt en uitgevoerd met behulp van Azure Import/Export Hallo service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 728e2a42-04ce-4be8-9375-e9e2bc6827a5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: e54bc66495c8a3473b8ec51bb254bce8bdc9eab9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-export-job"></a><span data-ttu-id="7bf18-103">Een exporttaak herstellen</span><span class="sxs-lookup"><span data-stu-id="7bf18-103">Repairing an export job</span></span>
<span data-ttu-id="7bf18-104">Nadat een taak voor het exporteren is voltooid, kunt u Microsoft Azure-hulpprogramma voor importeren/exporteren on-premises naar Hallo uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="7bf18-104">After an export job has completed, you can run hello Microsoft Azure Import/Export Tool on-premises to:</span></span>  
  
1.  <span data-ttu-id="7bf18-105">Download de bestanden dat hello Azure Import/Export-service kan geen tooexport heeft.</span><span class="sxs-lookup"><span data-stu-id="7bf18-105">Download any files that hello Azure Import/Export service was unable tooexport.</span></span>  
  
2.  <span data-ttu-id="7bf18-106">Valideren of Hallo-bestanden op Hallo station correct zijn geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="7bf18-106">Validate that hello files on hello drive were correctly exported.</span></span>  
  
<span data-ttu-id="7bf18-107">Deze functionaliteit moet u connectiviteit tooAzure opslag toouse hebben.</span><span class="sxs-lookup"><span data-stu-id="7bf18-107">You must have connectivity tooAzure Storage toouse this functionality.</span></span>  
  
<span data-ttu-id="7bf18-108">Hallo-opdracht voor het herstellen van een import-taak is **RepairExport**.</span><span class="sxs-lookup"><span data-stu-id="7bf18-108">hello command for repairing an import job is **RepairExport**.</span></span>

## <a name="repairexport-parameters"></a><span data-ttu-id="7bf18-109">RepairExport parameters</span><span class="sxs-lookup"><span data-stu-id="7bf18-109">RepairExport parameters</span></span>

<span data-ttu-id="7bf18-110">Hallo volgende parameters kunnen worden opgegeven met **RepairExport**:</span><span class="sxs-lookup"><span data-stu-id="7bf18-110">hello following parameters can be specified with **RepairExport**:</span></span>  
  
|<span data-ttu-id="7bf18-111">Parameter</span><span class="sxs-lookup"><span data-stu-id="7bf18-111">Parameter</span></span>|<span data-ttu-id="7bf18-112">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="7bf18-112">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="7bf18-113">**/ r: < RepairFile\>**</span><span class="sxs-lookup"><span data-stu-id="7bf18-113">**/r:<RepairFile\>**</span></span>|<span data-ttu-id="7bf18-114">Vereist.</span><span class="sxs-lookup"><span data-stu-id="7bf18-114">Required.</span></span> <span data-ttu-id="7bf18-115">Pad toohello Herstel dit bestand houdt Hallo voortgang van Hallo herstel en kunt u tooresume reparatie van een onderbroken.</span><span class="sxs-lookup"><span data-stu-id="7bf18-115">Path toohello repair file, which tracks hello progress of hello repair, and allows you tooresume an interrupted repair.</span></span> <span data-ttu-id="7bf18-116">Elk station moet slechts één repair-bestand hebben.</span><span class="sxs-lookup"><span data-stu-id="7bf18-116">Each drive must have one and only one repair file.</span></span> <span data-ttu-id="7bf18-117">Wanneer u een reparatie voor een bepaald station start, geeft u in Hallo pad tooa herstel het bestand nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="7bf18-117">When you start a repair for a given drive, you will pass in hello path tooa repair file which does not yet exist.</span></span> <span data-ttu-id="7bf18-118">tooresume reparatie van een onderbroken, moet u doorgeven in Hallo-naam van een bestaand bestand voor herstel.</span><span class="sxs-lookup"><span data-stu-id="7bf18-118">tooresume an interrupted repair, you should pass in hello name of an existing repair file.</span></span> <span data-ttu-id="7bf18-119">Hallo reparatie bestand corresponderende toohello doelstation moet altijd worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="7bf18-119">hello repair file corresponding toohello target drive must always be specified.</span></span>|  
|<span data-ttu-id="7bf18-120">**schakeloptie/LOGDIR op: < LogDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="7bf18-120">**/logdir:<LogDirectory\>**</span></span>|<span data-ttu-id="7bf18-121">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="7bf18-121">Optional.</span></span> <span data-ttu-id="7bf18-122">Hallo logboekmap.</span><span class="sxs-lookup"><span data-stu-id="7bf18-122">hello log directory.</span></span> <span data-ttu-id="7bf18-123">Uitgebreide logboekbestanden geschreven toothis directory.</span><span class="sxs-lookup"><span data-stu-id="7bf18-123">Verbose log files will be written toothis directory.</span></span> <span data-ttu-id="7bf18-124">Als er geen logboekmap is opgegeven, wordt de huidige map hello worden gebruikt als Hallo logboekmap.</span><span class="sxs-lookup"><span data-stu-id="7bf18-124">If no log directory is specified, hello current directory will be used as hello log directory.</span></span>|  
|<span data-ttu-id="7bf18-125">**/ d: < TargetDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="7bf18-125">**/d:<TargetDirectory\>**</span></span>|<span data-ttu-id="7bf18-126">Vereist.</span><span class="sxs-lookup"><span data-stu-id="7bf18-126">Required.</span></span> <span data-ttu-id="7bf18-127">Hallo directory toovalidate en herstel.</span><span class="sxs-lookup"><span data-stu-id="7bf18-127">hello directory toovalidate and repair.</span></span> <span data-ttu-id="7bf18-128">Dit is meestal de hoofdmap Hallo van Hallo export station, maar kan ook worden een netwerkbestandsshare die een kopie van bestanden Hallo geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="7bf18-128">This is usually hello root directory of hello export drive, but could also be a network file share containing a copy of hello exported files.</span></span>|  
|<span data-ttu-id="7bf18-129">**/BK: < BitLockerKey\>**</span><span class="sxs-lookup"><span data-stu-id="7bf18-129">**/bk:<BitLockerKey\>**</span></span>|<span data-ttu-id="7bf18-130">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="7bf18-130">Optional.</span></span> <span data-ttu-id="7bf18-131">Als u wilt dat Hallo hulpprogramma toounlock versleutelde waar Hallo geëxporteerd bestanden worden opgeslagen, moet u Hallo BitLocker-sleutel opgeven.</span><span class="sxs-lookup"><span data-stu-id="7bf18-131">You should specify hello BitLocker key if you want hello tool toounlock an encrypted where hello exported files are stored.</span></span>|  
|<span data-ttu-id="7bf18-132">**/sn: < StorageAccountName\>**</span><span class="sxs-lookup"><span data-stu-id="7bf18-132">**/sn:<StorageAccountName\>**</span></span>|<span data-ttu-id="7bf18-133">Vereist.</span><span class="sxs-lookup"><span data-stu-id="7bf18-133">Required.</span></span> <span data-ttu-id="7bf18-134">Hallo-naam van Hallo storage-account voor Hallo taak exporteren.</span><span class="sxs-lookup"><span data-stu-id="7bf18-134">hello name of hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="7bf18-135">**/SK: < StorageAccountKey\>**</span><span class="sxs-lookup"><span data-stu-id="7bf18-135">**/sk:<StorageAccountKey\>**</span></span>|<span data-ttu-id="7bf18-136">**Vereist** als een container SAS is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="7bf18-136">**Required** if and only if a container SAS is not specified.</span></span> <span data-ttu-id="7bf18-137">Hallo-toegangssleutel voor opslagaccount Hallo voor Hallo taak exporteren.</span><span class="sxs-lookup"><span data-stu-id="7bf18-137">hello account key for hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="7bf18-138">**/csas: < ContainerSas\>**</span><span class="sxs-lookup"><span data-stu-id="7bf18-138">**/csas:<ContainerSas\>**</span></span>|<span data-ttu-id="7bf18-139">**Vereist** als Hallo opslagaccountsleutel is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="7bf18-139">**Required** if and only if hello storage account key is not specified.</span></span> <span data-ttu-id="7bf18-140">Hallo container SAS voor toegang tot Hallo blobs die zijn gekoppeld aan de exporttaak Hallo.</span><span class="sxs-lookup"><span data-stu-id="7bf18-140">hello container SAS for accessing hello blobs associated with hello export job.</span></span>|  
|<span data-ttu-id="7bf18-141">**/ CopyLogFile: < DriveCopyLogFile\>**</span><span class="sxs-lookup"><span data-stu-id="7bf18-141">**/CopyLogFile:<DriveCopyLogFile\>**</span></span>|<span data-ttu-id="7bf18-142">Vereist.</span><span class="sxs-lookup"><span data-stu-id="7bf18-142">Required.</span></span> <span data-ttu-id="7bf18-143">Hallo pad toohello station kopiëren logboekbestand.</span><span class="sxs-lookup"><span data-stu-id="7bf18-143">hello path toohello drive copy log file.</span></span> <span data-ttu-id="7bf18-144">Hallo-bestand wordt gegenereerd door Hallo Windows Azure Import/Export-service en kan worden gedownload vanaf Hallo blob-opslag die is gekoppeld aan het Hallo-taak.</span><span class="sxs-lookup"><span data-stu-id="7bf18-144">hello file is generated by hello Windows Azure Import/Export service and can be downloaded from hello blob storage associated with hello job.</span></span> <span data-ttu-id="7bf18-145">Hallo kopie logboekbestand bevat informatie over mislukte blobs of bestanden die toobe hersteld zijn.</span><span class="sxs-lookup"><span data-stu-id="7bf18-145">hello copy log file contains information about failed blobs or files which are toobe repaired.</span></span>|  
|<span data-ttu-id="7bf18-146">**/ ManifestFile: < DriveManifestFile\>**</span><span class="sxs-lookup"><span data-stu-id="7bf18-146">**/ManifestFile:<DriveManifestFile\>**</span></span>|<span data-ttu-id="7bf18-147">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="7bf18-147">Optional.</span></span> <span data-ttu-id="7bf18-148">het manifestbestand Hallo pad toohello exporteren van het station.</span><span class="sxs-lookup"><span data-stu-id="7bf18-148">hello path toohello export drive's manifest file.</span></span> <span data-ttu-id="7bf18-149">Dit bestand is gegenereerd door de Windows Azure Import/Export-service Hallo en opgeslagen op Hallo export station en optioneel in een blob in Hallo storage-account aan Hallo taak zijn gekoppeld.</span><span class="sxs-lookup"><span data-stu-id="7bf18-149">This file is generated by hello Windows Azure Import/Export service and stored on hello export drive, and optionally in a blob in hello storage account associated with hello job.</span></span><br /><br /> <span data-ttu-id="7bf18-150">Hallo zal inhoud van het Hallo-bestanden op Hallo export schijf worden gecontroleerd bij Hallo MD5-hashes die zijn opgenomen in dit bestand.</span><span class="sxs-lookup"><span data-stu-id="7bf18-150">hello content of hello files on hello export drive will be verified with hello MD5 hashes contained in this file.</span></span> <span data-ttu-id="7bf18-151">Bestanden die bepaald toobe beschadigd zijn zijn gedownload en herschreven toohello doel mappen.</span><span class="sxs-lookup"><span data-stu-id="7bf18-151">Any files that are determined toobe corrupted will be downloaded and rewritten toohello target directories.</span></span>|  
  
## <a name="using-repairexport-mode-toocorrect-failed-exports"></a><span data-ttu-id="7bf18-152">Met behulp van RepairExport mislukt modus toocorrect uitvoer</span><span class="sxs-lookup"><span data-stu-id="7bf18-152">Using RepairExport mode toocorrect failed exports</span></span>  
<span data-ttu-id="7bf18-153">U kunt tooexport mislukte hello Azure-hulpprogramma voor importeren/exporteren toodownload bestanden gebruiken.</span><span class="sxs-lookup"><span data-stu-id="7bf18-153">You can use hello Azure Import/Export Tool toodownload files that failed tooexport.</span></span> <span data-ttu-id="7bf18-154">Hallo kopie logboekbestand bevat een lijst met bestanden die niet zijn geslaagd tooexport.</span><span class="sxs-lookup"><span data-stu-id="7bf18-154">hello copy log file will contain a list of files that failed tooexport.</span></span>  
  
<span data-ttu-id="7bf18-155">Hallo oorzaken van fouten van de uitvoer zijn Hallo mogelijkheden te volgen:</span><span class="sxs-lookup"><span data-stu-id="7bf18-155">hello causes of export failures include hello following possibilities:</span></span>  
  
-   <span data-ttu-id="7bf18-156">Beschadigde schijven</span><span class="sxs-lookup"><span data-stu-id="7bf18-156">Damaged drives</span></span>  
  
-   <span data-ttu-id="7bf18-157">Hallo opslagaccountsleutel gewijzigd tijdens het proces van bestandsoverdracht Hallo</span><span class="sxs-lookup"><span data-stu-id="7bf18-157">hello storage account key changed during hello transfer process</span></span>  
  
<span data-ttu-id="7bf18-158">Hallo-hulpprogramma toorun in **RepairExport** modus, moet u eerst tooconnect Hallo station met de Hallo geëxporteerde bestanden tooyour computer.</span><span class="sxs-lookup"><span data-stu-id="7bf18-158">toorun hello tool in **RepairExport** mode, you first need tooconnect hello drive containing hello exported files tooyour computer.</span></span> <span data-ttu-id="7bf18-159">Voer vervolgens hello Azure Import/Export Tool Hallo pad toothat station opgeven met Hallo `/d` parameter.</span><span class="sxs-lookup"><span data-stu-id="7bf18-159">Next, run hello Azure Import/Export Tool, specifying hello path toothat drive with hello `/d` parameter.</span></span> <span data-ttu-id="7bf18-160">U moet ook toospecify Hallo pad toohello van het station kopiëren logboekbestand dat u hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="7bf18-160">You also need toospecify hello path toohello drive's copy log file that you downloaded.</span></span> <span data-ttu-id="7bf18-161">Hallo opdrachtregel voorbeeld hieronder wordt uitgevoerd Hallo hulpprogramma toorepair bestanden die tooexport is mislukt:</span><span class="sxs-lookup"><span data-stu-id="7bf18-161">hello following command line example below runs hello tool toorepair any files that failed tooexport:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
<span data-ttu-id="7bf18-162">Hallo Hieronder volgt een voorbeeld van een logbestand kopiëren waarin wordt gemeld dat een blok in tooexport van Hallo blob is mislukt:</span><span class="sxs-lookup"><span data-stu-id="7bf18-162">hello following is an example of a copy log file that shows that one block in hello blob failed tooexport:</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/desert.jpg</BlobPath>  
    <FilePath>\pictures\wild\desert.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList>  
      <Block Offset="65536" Length="65536" Id="AQAAAA==" Status="Failed" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
<span data-ttu-id="7bf18-163">Hallo kopie logboekbestand geeft aan dat is een fout opgetreden tijdens het Hallo Windows Azure Import/Export-service is Hallo-blob blokken toohello bestandsshare op Hallo export station downloaden.</span><span class="sxs-lookup"><span data-stu-id="7bf18-163">hello copy log file indicates that a failure occurred while hello Windows Azure Import/Export service was downloading one of hello blob's blocks toohello file on hello export drive.</span></span> <span data-ttu-id="7bf18-164">Hallo van andere onderdelen van Hallo-bestand met succes is gedownload en Hallo bestandslengte is correct ingesteld.</span><span class="sxs-lookup"><span data-stu-id="7bf18-164">hello other components of hello file downloaded successfully, and hello file length was correctly set.</span></span> <span data-ttu-id="7bf18-165">Hallo-hulpprogramma wordt in dit geval Hallo-bestand op Hallo schijf openen, Hallo blok downloaden van Hallo storage-account en schrijf deze toohello bestand bereik vanaf verschuiving 65536 met lengte 65536.</span><span class="sxs-lookup"><span data-stu-id="7bf18-165">In this case, hello tool will open hello file on hello drive, download hello block from hello storage account, and write it toohello file range starting from offset 65536 with length 65536.</span></span>  
  
## <a name="using-repairexport-toovalidate-drive-contents"></a><span data-ttu-id="7bf18-166">Met behulp van RepairExport toovalidate station inhoud</span><span class="sxs-lookup"><span data-stu-id="7bf18-166">Using RepairExport toovalidate drive contents</span></span>  
<span data-ttu-id="7bf18-167">U kunt ook Azure Import/Export Hello **RepairExport** optie toovalidate Hallo inhoud op Hallo station juist zijn.</span><span class="sxs-lookup"><span data-stu-id="7bf18-167">You can also use Azure Import/Export with hello **RepairExport** option toovalidate hello contents on hello drive are correct.</span></span> <span data-ttu-id="7bf18-168">Hallo-manifestbestand op elk station export bevat MD5s voor Hallo inhoud van Hallo-station.</span><span class="sxs-lookup"><span data-stu-id="7bf18-168">hello manifest file on each export drive contains MD5s for hello contents of hello drive.</span></span>  
  
<span data-ttu-id="7bf18-169">Hello Azure Import/Export-service kunt ook bestanden opslaan Hallo manifest tooa storage-account tijdens Hallo exporteren.</span><span class="sxs-lookup"><span data-stu-id="7bf18-169">hello Azure Import/Export service can also save hello manifest files tooa storage account during hello export process.</span></span> <span data-ttu-id="7bf18-170">Hallo locatie van de manifestbestanden Hallo beschikbaar is via Hallo [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) bewerking als het Hallo-taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="7bf18-170">hello location of hello manifest files is available via hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation when hello job has completed.</span></span> <span data-ttu-id="7bf18-171">Zie [Import/Export-service Manifest bestandsindeling](storage-import-export-file-format-metadata-and-properties.md) voor meer informatie over het Hallo-indeling van het manifestbestand van een station.</span><span class="sxs-lookup"><span data-stu-id="7bf18-171">See [Import/Export service Manifest File Format](storage-import-export-file-format-metadata-and-properties.md) for more information about hello format of a drive manifest file.</span></span>  
  
<span data-ttu-id="7bf18-172">Hallo volgende voorbeeld laat zien hoe toorun Azure-hulpprogramma voor importeren/exporteren Hallo Hello **/ManifestFile** en **/CopyLogFile** parameters:</span><span class="sxs-lookup"><span data-stu-id="7bf18-172">hello following example shows how toorun hello Azure Import/Export Tool with hello **/ManifestFile** and **/CopyLogFile** parameters:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
<span data-ttu-id="7bf18-173">Hallo Hieronder volgt een voorbeeld van een manifestbestand:</span><span class="sxs-lookup"><span data-stu-id="7bf18-173">hello following is an example of a manifest file:</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveManifest Version="2011-10-01">  
  <Drive>  
    <DriveId>9WM35C3U</DriveId>  
    <ClientCreator>Windows Azure Import/Export service</ClientCreator>  
    <BlobList>
      <Blob>  
        <BlobPath>pictures/city/redmond.jpg</BlobPath>  
        <FilePath>\pictures\city\redmond.jpg</FilePath>  
        <Length>15360</Length>  
        <PageRangeList>  
          <PageRange Offset="0" Length="3584" Hash="72FC55ED9AFDD40A0C8D5C4193208416" />  
          <PageRange Offset="3584" Length="3584" Hash="68B28A561B73D1DA769D4C24AA427DB8" />  
          <PageRange Offset="7168" Length="512" Hash="F521DF2F50C46BC5F9EA9FB787A23EED" />  
        </PageRangeList>  
        <PropertiesPath Hash="E72A22EA959566066AD89E3B49020C0A">\pictures\city\redmond.jpg.properties</PropertiesPath>  
      </Blob>  
      <Blob>  
        <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
        <FilePath>\pictures\wild\canyon.jpg</FilePath>  
        <Length>10884</Length>  
        <BlockList>  
          <Block Offset="0" Length="2721" Id="AAAAAA==" Hash="263DC9C4B99C2177769C5EBE04787037" />  
          <Block Offset="2721" Length="2721" Id="AQAAAA==" Hash="0C52BAE2CC20EFEC15CC1E3045517AA6" />  
          <Block Offset="5442" Length="2721" Id="AgAAAA==" Hash="73D1CB62CB426230C34C9F57B7148F10" />  
          <Block Offset="8163" Length="2721" Id="AwAAAA==" Hash="11210E665C5F8E7E4F136D053B243E6A" />  
        </BlockList>  
        <PropertiesPath Hash="81D7F81B2C29F10D6E123D386C3A4D5A">\pictures\wild\canyon.jpg.properties</PropertiesPath>  
      </Blob> 
    </BlobList>  
 </Drive>  
</DriveManifest>  
``` 
  
<span data-ttu-id="7bf18-174">Na het herstelproces bijna afgelopen hello, Hallo Lees elk bestand waarnaar wordt verwezen in het manifestbestand Hallo en hulpprogramma controleren de integriteit van Hallo-bestand met de Hallo MD5-hashes.</span><span class="sxs-lookup"><span data-stu-id="7bf18-174">After finishing hello repair process, hello tool will read through each file referenced in hello manifest file and verify hello file's integrity with hello MD5 hashes.</span></span> <span data-ttu-id="7bf18-175">Voor Hallo manifest hierboven gaat dit via de volgende onderdelen Hallo.</span><span class="sxs-lookup"><span data-stu-id="7bf18-175">For hello manifest above, it will go through hello following components.</span></span>  

```  
G:\pictures\city\redmond.jpg, offset 0, length 3584  
  
G:\pictures\city\redmond.jpg, offset 3584, length 3584  
  
G:\pictures\city\redmond.jpg, offset 7168, length 3584  
  
G:\pictures\city\redmond.jpg.properties  
  
G:\pictures\wild\canyon.jpg, offset 0, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 2721, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 5442, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 8163, length 2721  
  
G:\pictures\wild\canyon.jpg.properties  
```

<span data-ttu-id="7bf18-176">Een onderdeel Hallo verificatie mislukt door Hallo hulpprogramma wordt gedownload en herschreven toohello hetzelfde bestand op Hallo-station.</span><span class="sxs-lookup"><span data-stu-id="7bf18-176">Any component failing hello verification will be downloaded by hello tool and rewritten toohello same file on hello drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="7bf18-177">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="7bf18-177">Next steps</span></span>
 
* [<span data-ttu-id="7bf18-178">Hallo-instelling van Azure-hulpprogramma voor importeren/exporteren</span><span class="sxs-lookup"><span data-stu-id="7bf18-178">Setting Up hello Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="7bf18-179">Harde schijven voorbereiden voor een importtaak</span><span class="sxs-lookup"><span data-stu-id="7bf18-179">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="7bf18-180">De taakstatus controleren met kopielogboekbestanden</span><span class="sxs-lookup"><span data-stu-id="7bf18-180">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="7bf18-181">Een importtaak herstellen</span><span class="sxs-lookup"><span data-stu-id="7bf18-181">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="7bf18-182">Het oplossen van problemen hello Azure-hulpprogramma voor importeren/exporteren</span><span class="sxs-lookup"><span data-stu-id="7bf18-182">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
