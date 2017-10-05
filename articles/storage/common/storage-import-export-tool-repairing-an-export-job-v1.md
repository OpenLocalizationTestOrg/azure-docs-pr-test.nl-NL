---
title: Herstellen van een taak van de export Azure Import/Export - v1 | Microsoft Docs
description: Informatie over het herstellen van een taak voor het exporteren die zijn gemaakt en uitgevoerd met behulp van de Azure Import/Export-service.
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
ms.openlocfilehash: 57ab58fa1fd8371d0b6f019f94bb162bcc1e0e43
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/29/2017
---
# <a name="repairing-an-export-job"></a><span data-ttu-id="dacf1-103">Een exporttaak herstellen</span><span class="sxs-lookup"><span data-stu-id="dacf1-103">Repairing an export job</span></span>
<span data-ttu-id="dacf1-104">Nadat een taak voor het exporteren is voltooid, kunt u de Microsoft Azure-hulpprogramma voor importeren/exporteren on-premises naar uitvoeren:</span><span class="sxs-lookup"><span data-stu-id="dacf1-104">After an export job has completed, you can run the Microsoft Azure Import/Export Tool on-premises to:</span></span>  
  
1.  <span data-ttu-id="dacf1-105">Download de bestanden die de Azure Import/Export-service kon niet exporteren.</span><span class="sxs-lookup"><span data-stu-id="dacf1-105">Download any files that the Azure Import/Export service was unable to export.</span></span>  
  
2.  <span data-ttu-id="dacf1-106">Valideren of de bestanden op de schijf correct zijn geëxporteerd.</span><span class="sxs-lookup"><span data-stu-id="dacf1-106">Validate that the files on the drive were correctly exported.</span></span>  
  
<span data-ttu-id="dacf1-107">U moet zijn verbonden met Azure Storage om deze functionaliteit te gebruiken.</span><span class="sxs-lookup"><span data-stu-id="dacf1-107">You must have connectivity to Azure Storage to use this functionality.</span></span>  
  
<span data-ttu-id="dacf1-108">De opdracht voor het herstellen van een import-taak is **RepairExport**.</span><span class="sxs-lookup"><span data-stu-id="dacf1-108">The command for repairing an import job is **RepairExport**.</span></span>

## <a name="repairexport-parameters"></a><span data-ttu-id="dacf1-109">RepairExport parameters</span><span class="sxs-lookup"><span data-stu-id="dacf1-109">RepairExport parameters</span></span>

<span data-ttu-id="dacf1-110">U kunt de volgende parameters opgeven met **RepairExport**:</span><span class="sxs-lookup"><span data-stu-id="dacf1-110">The following parameters can be specified with **RepairExport**:</span></span>  
  
|<span data-ttu-id="dacf1-111">Parameter</span><span class="sxs-lookup"><span data-stu-id="dacf1-111">Parameter</span></span>|<span data-ttu-id="dacf1-112">Beschrijving</span><span class="sxs-lookup"><span data-stu-id="dacf1-112">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="dacf1-113">**/ r: < RepairFile\>**</span><span class="sxs-lookup"><span data-stu-id="dacf1-113">**/r:<RepairFile\>**</span></span>|<span data-ttu-id="dacf1-114">Vereist.</span><span class="sxs-lookup"><span data-stu-id="dacf1-114">Required.</span></span> <span data-ttu-id="dacf1-115">Pad naar het bestand herstellen, waarin de voortgang van het herstel en kunt u de reparatie van een onderbroken hervatten.</span><span class="sxs-lookup"><span data-stu-id="dacf1-115">Path to the repair file, which tracks the progress of the repair, and allows you to resume an interrupted repair.</span></span> <span data-ttu-id="dacf1-116">Elk station moet slechts één repair-bestand hebben.</span><span class="sxs-lookup"><span data-stu-id="dacf1-116">Each drive must have one and only one repair file.</span></span> <span data-ttu-id="dacf1-117">Wanneer u een reparatie voor een bepaald station start, wordt u in het pad doorgeven aan een reparatie-bestand dat nog niet bestaat.</span><span class="sxs-lookup"><span data-stu-id="dacf1-117">When you start a repair for a given drive, you will pass in the path to a repair file which does not yet exist.</span></span> <span data-ttu-id="dacf1-118">Om de reparatie van een onderbroken hervatten, moet u doorgeven in een bestaand bestand voor herstel.</span><span class="sxs-lookup"><span data-stu-id="dacf1-118">To resume an interrupted repair, you should pass in the name of an existing repair file.</span></span> <span data-ttu-id="dacf1-119">Het herstel bestand overeenkomt met het doelstation moet altijd worden opgegeven.</span><span class="sxs-lookup"><span data-stu-id="dacf1-119">The repair file corresponding to the target drive must always be specified.</span></span>|  
|<span data-ttu-id="dacf1-120">**schakeloptie/LOGDIR op: < LogDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="dacf1-120">**/logdir:<LogDirectory\>**</span></span>|<span data-ttu-id="dacf1-121">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="dacf1-121">Optional.</span></span> <span data-ttu-id="dacf1-122">De logboekmap.</span><span class="sxs-lookup"><span data-stu-id="dacf1-122">The log directory.</span></span> <span data-ttu-id="dacf1-123">Uitgebreide logboekbestanden worden geschreven naar deze map.</span><span class="sxs-lookup"><span data-stu-id="dacf1-123">Verbose log files will be written to this directory.</span></span> <span data-ttu-id="dacf1-124">Als er geen logboekmap is opgegeven, wordt de huidige map gebruikt als de logboekmap.</span><span class="sxs-lookup"><span data-stu-id="dacf1-124">If no log directory is specified, the current directory will be used as the log directory.</span></span>|  
|<span data-ttu-id="dacf1-125">**/ d: < TargetDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="dacf1-125">**/d:<TargetDirectory\>**</span></span>|<span data-ttu-id="dacf1-126">Vereist.</span><span class="sxs-lookup"><span data-stu-id="dacf1-126">Required.</span></span> <span data-ttu-id="dacf1-127">De map om te valideren en te herstellen.</span><span class="sxs-lookup"><span data-stu-id="dacf1-127">The directory to validate and repair.</span></span> <span data-ttu-id="dacf1-128">Dit is meestal de hoofdmap van het station exporteren, maar kan ook worden een netwerkbestandsshare die een kopie van de geëxporteerde bestanden.</span><span class="sxs-lookup"><span data-stu-id="dacf1-128">This is usually the root directory of the export drive, but could also be a network file share containing a copy of the exported files.</span></span>|  
|<span data-ttu-id="dacf1-129">**/BK: < BitLockerKey\>**</span><span class="sxs-lookup"><span data-stu-id="dacf1-129">**/bk:<BitLockerKey\>**</span></span>|<span data-ttu-id="dacf1-130">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="dacf1-130">Optional.</span></span> <span data-ttu-id="dacf1-131">Als u wilt dat het hulpprogramma voor het ontgrendelen van een gecodeerd waarin de geëxporteerde bestanden zijn opgeslagen, moet u de BitLocker-sleutel opgeven.</span><span class="sxs-lookup"><span data-stu-id="dacf1-131">You should specify the BitLocker key if you want the tool to unlock an encrypted where the exported files are stored.</span></span>|  
|<span data-ttu-id="dacf1-132">**/sn: < StorageAccountName\>**</span><span class="sxs-lookup"><span data-stu-id="dacf1-132">**/sn:<StorageAccountName\>**</span></span>|<span data-ttu-id="dacf1-133">Vereist.</span><span class="sxs-lookup"><span data-stu-id="dacf1-133">Required.</span></span> <span data-ttu-id="dacf1-134">De naam van het opslagaccount voor de taak voor het exporteren.</span><span class="sxs-lookup"><span data-stu-id="dacf1-134">The name of the storage account for the export job.</span></span>|  
|<span data-ttu-id="dacf1-135">**/SK: < StorageAccountKey\>**</span><span class="sxs-lookup"><span data-stu-id="dacf1-135">**/sk:<StorageAccountKey\>**</span></span>|<span data-ttu-id="dacf1-136">**Vereist** als een container SAS is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="dacf1-136">**Required** if and only if a container SAS is not specified.</span></span> <span data-ttu-id="dacf1-137">De accountsleutel voor het opslagaccount voor de taak voor exporteren.</span><span class="sxs-lookup"><span data-stu-id="dacf1-137">The account key for the storage account for the export job.</span></span>|  
|<span data-ttu-id="dacf1-138">**/csas: < ContainerSas\>**</span><span class="sxs-lookup"><span data-stu-id="dacf1-138">**/csas:<ContainerSas\>**</span></span>|<span data-ttu-id="dacf1-139">**Vereist** als de sleutel van het opslagaccount is niet opgegeven.</span><span class="sxs-lookup"><span data-stu-id="dacf1-139">**Required** if and only if the storage account key is not specified.</span></span> <span data-ttu-id="dacf1-140">De container SAS voor toegang tot de blobs die zijn gekoppeld aan de taak voor het exporteren.</span><span class="sxs-lookup"><span data-stu-id="dacf1-140">The container SAS for accessing the blobs associated with the export job.</span></span>|  
|<span data-ttu-id="dacf1-141">**/ CopyLogFile: < DriveCopyLogFile\>**</span><span class="sxs-lookup"><span data-stu-id="dacf1-141">**/CopyLogFile:<DriveCopyLogFile\>**</span></span>|<span data-ttu-id="dacf1-142">Vereist.</span><span class="sxs-lookup"><span data-stu-id="dacf1-142">Required.</span></span> <span data-ttu-id="dacf1-143">Het pad naar het logboekbestand van de schijf kopiëren.</span><span class="sxs-lookup"><span data-stu-id="dacf1-143">The path to the drive copy log file.</span></span> <span data-ttu-id="dacf1-144">Het bestand is gegenereerd door de Windows Azure Import/Export-service en kan worden gedownload van de blob-opslag die is gekoppeld aan de taak.</span><span class="sxs-lookup"><span data-stu-id="dacf1-144">The file is generated by the Windows Azure Import/Export service and can be downloaded from the blob storage associated with the job.</span></span> <span data-ttu-id="dacf1-145">Het logboekbestand kopiëren bevat informatie over mislukte blobs of bestanden die moeten worden hersteld.</span><span class="sxs-lookup"><span data-stu-id="dacf1-145">The copy log file contains information about failed blobs or files which are to be repaired.</span></span>|  
|<span data-ttu-id="dacf1-146">**/ ManifestFile: < DriveManifestFile\>**</span><span class="sxs-lookup"><span data-stu-id="dacf1-146">**/ManifestFile:<DriveManifestFile\>**</span></span>|<span data-ttu-id="dacf1-147">Optioneel.</span><span class="sxs-lookup"><span data-stu-id="dacf1-147">Optional.</span></span> <span data-ttu-id="dacf1-148">Het pad naar het manifestbestand van de export-station.</span><span class="sxs-lookup"><span data-stu-id="dacf1-148">The path to the export drive's manifest file.</span></span> <span data-ttu-id="dacf1-149">Dit bestand is gegenereerd door de Windows Azure Import/Export-service en opgeslagen op de schijf exporteren en optioneel in een blob in de storage-account die is gekoppeld aan de taak.</span><span class="sxs-lookup"><span data-stu-id="dacf1-149">This file is generated by the Windows Azure Import/Export service and stored on the export drive, and optionally in a blob in the storage account associated with the job.</span></span><br /><br /> <span data-ttu-id="dacf1-150">De inhoud van de bestanden op de schijf van de uitvoer wordt geverifieerd met de MD5-hashes die zijn opgenomen in dit bestand.</span><span class="sxs-lookup"><span data-stu-id="dacf1-150">The content of the files on the export drive will be verified with the MD5 hashes contained in this file.</span></span> <span data-ttu-id="dacf1-151">Bestanden die worden bepaald beschadigd te zijn gedownload en herschreven naar de doel-mappen.</span><span class="sxs-lookup"><span data-stu-id="dacf1-151">Any files that are determined to be corrupted will be downloaded and rewritten to the target directories.</span></span>|  
  
## <a name="using-repairexport-mode-to-correct-failed-exports"></a><span data-ttu-id="dacf1-152">RepairExport modus gebruiken om op te lossen mislukte uitvoer</span><span class="sxs-lookup"><span data-stu-id="dacf1-152">Using RepairExport mode to correct failed exports</span></span>  
<span data-ttu-id="dacf1-153">U kunt het Azure Import/Export-hulpprogramma gebruiken voor het downloaden van bestanden die exporteren is mislukt.</span><span class="sxs-lookup"><span data-stu-id="dacf1-153">You can use the Azure Import/Export Tool to download files that failed to export.</span></span> <span data-ttu-id="dacf1-154">Het logboekbestand kopie bevat een lijst met bestanden die exporteren is mislukt.</span><span class="sxs-lookup"><span data-stu-id="dacf1-154">The copy log file will contain a list of files that failed to export.</span></span>  
  
<span data-ttu-id="dacf1-155">De oorzaken van fouten van de uitvoer zijn onder andere de volgende mogelijkheden:</span><span class="sxs-lookup"><span data-stu-id="dacf1-155">The causes of export failures include the following possibilities:</span></span>  
  
-   <span data-ttu-id="dacf1-156">Beschadigde schijven</span><span class="sxs-lookup"><span data-stu-id="dacf1-156">Damaged drives</span></span>  
  
-   <span data-ttu-id="dacf1-157">De opslagaccountsleutel die is gewijzigd tijdens de overdracht</span><span class="sxs-lookup"><span data-stu-id="dacf1-157">The storage account key changed during the transfer process</span></span>  
  
<span data-ttu-id="dacf1-158">Het hulpprogramma uitvoeren **RepairExport** modus, moet u eerst verbinding maken met het station met de geëxporteerde bestanden op uw computer.</span><span class="sxs-lookup"><span data-stu-id="dacf1-158">To run the tool in **RepairExport** mode, you first need to connect the drive containing the exported files to your computer.</span></span> <span data-ttu-id="dacf1-159">Voer vervolgens het Azure Import/Export-hulpprogramma opgeven van het pad naar het station met de `/d` parameter.</span><span class="sxs-lookup"><span data-stu-id="dacf1-159">Next, run the Azure Import/Export Tool, specifying the path to that drive with the `/d` parameter.</span></span> <span data-ttu-id="dacf1-160">Ook moet u het pad opgeven naar de schijf kopiëren logboekbestand dat u hebt gedownload.</span><span class="sxs-lookup"><span data-stu-id="dacf1-160">You also need to specify the path to the drive's copy log file that you downloaded.</span></span> <span data-ttu-id="dacf1-161">De volgende opdrachtregel voorbeeld hieronder wordt uitgevoerd voor het hulpprogramma voor het herstellen van bestanden die exporteren is mislukt:</span><span class="sxs-lookup"><span data-stu-id="dacf1-161">The following command line example below runs the tool to repair any files that failed to export:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
<span data-ttu-id="dacf1-162">Hier volgt een voorbeeld van een logbestand kopiëren die laat dat een blok in de blob zien is mislukt om te exporteren:</span><span class="sxs-lookup"><span data-stu-id="dacf1-162">The following is an example of a copy log file that shows that one block in the blob failed to export:</span></span>  
  
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
  
<span data-ttu-id="dacf1-163">Het logboekbestand kopie geeft aan dat is een fout opgetreden terwijl de Windows Azure Import/Export-service is een van de blob-blokken gedownload naar het bestand op het station exporteren.</span><span class="sxs-lookup"><span data-stu-id="dacf1-163">The copy log file indicates that a failure occurred while the Windows Azure Import/Export service was downloading one of the blob's blocks to the file on the export drive.</span></span> <span data-ttu-id="dacf1-164">De andere onderdelen van het bestand is gedownload, en de bestandslengte juist is ingesteld.</span><span class="sxs-lookup"><span data-stu-id="dacf1-164">The other components of the file downloaded successfully, and the file length was correctly set.</span></span> <span data-ttu-id="dacf1-165">Het hulpprogramma wordt in dit geval open het bestand op de schijf, downloaden van het blok van het opslagaccount en schrijven naar het bestand bereik vanaf verschuiving 65536 met lengte 65536.</span><span class="sxs-lookup"><span data-stu-id="dacf1-165">In this case, the tool will open the file on the drive, download the block from the storage account, and write it to the file range starting from offset 65536 with length 65536.</span></span>  
  
## <a name="using-repairexport-to-validate-drive-contents"></a><span data-ttu-id="dacf1-166">Met behulp van RepairExport station inhoud valideren</span><span class="sxs-lookup"><span data-stu-id="dacf1-166">Using RepairExport to validate drive contents</span></span>  
<span data-ttu-id="dacf1-167">U kunt ook Azure Import/Export met de **RepairExport** optie voor het valideren van de inhoud op het station juist zijn.</span><span class="sxs-lookup"><span data-stu-id="dacf1-167">You can also use Azure Import/Export with the **RepairExport** option to validate the contents on the drive are correct.</span></span> <span data-ttu-id="dacf1-168">Het manifestbestand op elk station export bevat MD5s voor de inhoud van het station.</span><span class="sxs-lookup"><span data-stu-id="dacf1-168">The manifest file on each export drive contains MD5s for the contents of the drive.</span></span>  
  
<span data-ttu-id="dacf1-169">De Azure Import/Export-service kan ook de manifest-bestanden opslaan naar een opslagaccount tijdens het exporteren.</span><span class="sxs-lookup"><span data-stu-id="dacf1-169">The Azure Import/Export service can also save the manifest files to a storage account during the export process.</span></span> <span data-ttu-id="dacf1-170">De locatie van de manifest-bestanden is beschikbaar via de [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) bewerking als de taak is voltooid.</span><span class="sxs-lookup"><span data-stu-id="dacf1-170">The location of the manifest files is available via the [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation when the job has completed.</span></span> <span data-ttu-id="dacf1-171">Zie [Import/Export-service Manifest bestandsindeling](storage-import-export-file-format-metadata-and-properties.md) voor meer informatie over de indeling van het manifestbestand van een station.</span><span class="sxs-lookup"><span data-stu-id="dacf1-171">See [Import/Export service Manifest File Format](storage-import-export-file-format-metadata-and-properties.md) for more information about the format of a drive manifest file.</span></span>  
  
<span data-ttu-id="dacf1-172">Het volgende voorbeeld ziet u het uitvoeren van het Azure Import/Export-hulpprogramma met de **/ManifestFile** en **/CopyLogFile** parameters:</span><span class="sxs-lookup"><span data-stu-id="dacf1-172">The following example shows how to run the Azure Import/Export Tool with the **/ManifestFile** and **/CopyLogFile** parameters:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
<span data-ttu-id="dacf1-173">Hier volgt een voorbeeld van een manifestbestand:</span><span class="sxs-lookup"><span data-stu-id="dacf1-173">The following is an example of a manifest file:</span></span>  
  
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
  
<span data-ttu-id="dacf1-174">Nadat het herstelproces is voltooid, wordt het hulpprogramma Lees elk bestand waarnaar wordt verwezen in het manifestbestand en controleer of de integriteit van het bestand met de MD5-hashes.</span><span class="sxs-lookup"><span data-stu-id="dacf1-174">After finishing the repair process, the tool will read through each file referenced in the manifest file and verify the file's integrity with the MD5 hashes.</span></span> <span data-ttu-id="dacf1-175">Voor het manifest hierboven gaat dit via de volgende onderdelen.</span><span class="sxs-lookup"><span data-stu-id="dacf1-175">For the manifest above, it will go through the following components.</span></span>  

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

<span data-ttu-id="dacf1-176">De onderdelen die zijn mislukt de verificatie door het hulpprogramma wordt gedownload en herschreven naar hetzelfde bestand op de schijf.</span><span class="sxs-lookup"><span data-stu-id="dacf1-176">Any component failing the verification will be downloaded by the tool and rewritten to the same file on the drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="dacf1-177">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="dacf1-177">Next steps</span></span>
 
* [<span data-ttu-id="dacf1-178">Instellen van het hulpprogramma Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="dacf1-178">Setting Up the Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="dacf1-179">Harde schijven voorbereiden voor een importtaak</span><span class="sxs-lookup"><span data-stu-id="dacf1-179">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="dacf1-180">De taakstatus controleren met kopielogboekbestanden</span><span class="sxs-lookup"><span data-stu-id="dacf1-180">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="dacf1-181">Een importtaak herstellen</span><span class="sxs-lookup"><span data-stu-id="dacf1-181">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="dacf1-182">Problemen met het hulpprogramma Azure Import/Export oplossen</span><span class="sxs-lookup"><span data-stu-id="dacf1-182">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
