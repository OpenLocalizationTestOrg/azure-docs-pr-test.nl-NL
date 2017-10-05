---
title: Instellen van de Azure Import/Export hulpprogramma v1 | Microsoft Docs
description: Informatie over het instellen van de voorbereiding van het station en het hulpprogramma voor de Azure Import/Export-service voor het repareren. Dit verwijst naar v1 van het hulpprogramma voor importeren/exporteren.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: c312b1ab-5b9e-4d24-becd-790a88b3ba8d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 39d7e9a71a290ace6f6f4caf48f1ec5e46fe9a48
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="setting-up-the-azure-importexport-tool"></a><span data-ttu-id="ff515-104">Instellen van de Azure-hulpprogramma voor importeren/exporteren</span><span class="sxs-lookup"><span data-stu-id="ff515-104">Setting up the Azure Import/Export Tool</span></span>
<span data-ttu-id="ff515-105">Het hulpprogramma voor importeren/exporteren van Microsoft Azure is het station voorbereiding hulpprogramma en herstel die u met de Microsoft Azure Import/Export-service gebruiken kunt.</span><span class="sxs-lookup"><span data-stu-id="ff515-105">The Microsoft Azure Import/Export Tool is the drive preparation and repair tool that you can use with the Microsoft Azure Import/Export service.</span></span> <span data-ttu-id="ff515-106">U kunt het hulpprogramma gebruiken voor de volgende functies:</span><span class="sxs-lookup"><span data-stu-id="ff515-106">You can use the tool for the following functions:</span></span>  
  
-   <span data-ttu-id="ff515-107">Voordat u een import-taak maakt, kunt u dit hulpprogramma kunt gebruiken om gegevens te kopiëren naar de harde schijven die u wilt verzenden naar een Windows Azure-Datacenter.</span><span class="sxs-lookup"><span data-stu-id="ff515-107">Before creating an import job, you can use this tool to copy data to the hard drives you are going to ship to a Windows Azure data center.</span></span>  
  
-   <span data-ttu-id="ff515-108">Nadat een import-taak is voltooid, kunt u dit hulpprogramma kunt gebruiken om te herstellen van alle bestaande blobs zijn beschadigd, ontbreekt of het conflict met andere blobs.</span><span class="sxs-lookup"><span data-stu-id="ff515-108">After an import job has completed, you can use this tool to repair any blobs that were corrupted, were missing, or conflicted with other blobs.</span></span>  
  
-   <span data-ttu-id="ff515-109">Nadat u de stations van een voltooide exporttaak ontvangt, kunt u dit hulpprogramma kunt gebruiken om te herstellen van bestanden die beschadigd of ontbreken op de stations zijn.</span><span class="sxs-lookup"><span data-stu-id="ff515-109">After you receive the drives from a completed export job, you can use this tool to repair any files that were corrupted or missing on the drives.</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="ff515-110">Vereisten</span><span class="sxs-lookup"><span data-stu-id="ff515-110">Prerequisites</span></span>  
<span data-ttu-id="ff515-111">Als u schijven voor een import-taak voorbereidt, moet u voldoen aan de volgende vereisten:</span><span class="sxs-lookup"><span data-stu-id="ff515-111">If you are preparing drives for an import job, you will need to meet the following prerequisites:</span></span>  
  
-   <span data-ttu-id="ff515-112">U moet een actief Azure-abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="ff515-112">You must have an active Azure subscription.</span></span>  
  
-   <span data-ttu-id="ff515-113">Uw abonnement vergezeld gaan van een opslagaccount met voldoende beschikbare ruimte voor het opslaan van de bestanden die u gaat importeren.</span><span class="sxs-lookup"><span data-stu-id="ff515-113">Your subscription must include a storage account with enough available space to store the files you are going to import.</span></span>  
  
-   <span data-ttu-id="ff515-114">U moet ten minste één van de sleutels voor het opslagaccount.</span><span class="sxs-lookup"><span data-stu-id="ff515-114">You need at least one of the account keys for the storage account.</span></span>  
  
-   <span data-ttu-id="ff515-115">U moet een computer (de ' kopie-machine') met Windows 7, Windows Server 2008 R2 of een nieuwere Windows-besturingssysteem geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="ff515-115">You need a computer (the "copy machine") with Windows 7, Windows Server 2008 R2, or a newer Windows operating system installed.</span></span>  
  
-   <span data-ttu-id="ff515-116">.NET Framework 4 moet worden geïnstalleerd op de computer kopiëren.</span><span class="sxs-lookup"><span data-stu-id="ff515-116">The .NET Framework 4 must be installed on the copy machine.</span></span>  
  
-   <span data-ttu-id="ff515-117">BitLocker moet zijn ingeschakeld op de computer kopiëren.</span><span class="sxs-lookup"><span data-stu-id="ff515-117">BitLocker must be enabled on the copy machine.</span></span>  
  
-   <span data-ttu-id="ff515-118">U moet een of meer stations met gegevens die moeten worden geïmporteerd of lege 3.5-inch SATA harde schijven gekoppeld aan de machine kopiëren.</span><span class="sxs-lookup"><span data-stu-id="ff515-118">You will need one or more drives that contains data to be imported or empty 3.5-inch SATA hard drives connected to the copy machine.</span></span>  
  
-   <span data-ttu-id="ff515-119">De bestanden die u van plan bent om te importeren moet toegankelijk zijn vanaf de computer kopiëren of ze zich op een netwerkshare of een lokale vaste schijf.</span><span class="sxs-lookup"><span data-stu-id="ff515-119">The files you plan to import must be accessible from the copy machine, whether they are on a network share or a local hard drive.</span></span> 
  
<span data-ttu-id="ff515-120">Als u probeert te herstellen van een import die is gedeeltelijk mislukt, moet u:</span><span class="sxs-lookup"><span data-stu-id="ff515-120">If you are attempting to repair an import that has partially failed, you will need:</span></span>  
  
-   <span data-ttu-id="ff515-121">De logboekbestanden kopiëren</span><span class="sxs-lookup"><span data-stu-id="ff515-121">The copy log files</span></span>  
  
-   <span data-ttu-id="ff515-122">De sleutel van het opslagaccount</span><span class="sxs-lookup"><span data-stu-id="ff515-122">The storage account key</span></span>  
  
  <span data-ttu-id="ff515-123">Als u probeert te herstellen van een uitvoer die is gedeeltelijk mislukt, moet u:</span><span class="sxs-lookup"><span data-stu-id="ff515-123">If you are attempting to repair an export that has partially failed, you will need:</span></span>  
  
-   <span data-ttu-id="ff515-124">De logboekbestanden kopiëren</span><span class="sxs-lookup"><span data-stu-id="ff515-124">The copy log files</span></span>  
  
-   <span data-ttu-id="ff515-125">De manifest-bestanden (optioneel)</span><span class="sxs-lookup"><span data-stu-id="ff515-125">The manifest files (optional)</span></span>  
  
-   <span data-ttu-id="ff515-126">De sleutel van het opslagaccount</span><span class="sxs-lookup"><span data-stu-id="ff515-126">The storage account key</span></span>  
  
## <a name="installing-the-azure-importexport-tool"></a><span data-ttu-id="ff515-127">Installeren van het hulpprogramma Azure Import/Export</span><span class="sxs-lookup"><span data-stu-id="ff515-127">Installing the Azure Import/Export Tool</span></span>  
 <span data-ttu-id="ff515-128">De Azure-hulpprogramma voor importeren/exporteren bestaat uit de volgende bestanden:</span><span class="sxs-lookup"><span data-stu-id="ff515-128">The Azure Import/Export Tool consists of the following files:</span></span>  
  
-   <span data-ttu-id="ff515-129">WAImportExport.exe</span><span class="sxs-lookup"><span data-stu-id="ff515-129">WAImportExport.exe</span></span>  
  
-   <span data-ttu-id="ff515-130">WAImportExport.exe.config</span><span class="sxs-lookup"><span data-stu-id="ff515-130">WAImportExport.exe.config</span></span>  
  
-   <span data-ttu-id="ff515-131">WAImportExportCore.dll</span><span class="sxs-lookup"><span data-stu-id="ff515-131">WAImportExportCore.dll</span></span>  
  
-   <span data-ttu-id="ff515-132">WAImportExportRepair.dll</span><span class="sxs-lookup"><span data-stu-id="ff515-132">WAImportExportRepair.dll</span></span>  
  
-   <span data-ttu-id="ff515-133">Microsoft.WindowsAzure.Storage.dll</span><span class="sxs-lookup"><span data-stu-id="ff515-133">Microsoft.WindowsAzure.Storage.dll</span></span>  
  
-   <span data-ttu-id="ff515-134">hddid.dll</span><span class="sxs-lookup"><span data-stu-id="ff515-134">Hddid.dll</span></span>  
  
 <span data-ttu-id="ff515-135">Deze bestanden kopiëren naar een werkmap, bijvoorbeeld `c:\WAImportExport`.</span><span class="sxs-lookup"><span data-stu-id="ff515-135">Copy these files to a working directory, for example, `c:\WAImportExport`.</span></span> <span data-ttu-id="ff515-136">Vervolgens een opdrachtregel-venster openen in de beheerdersmodus en de bovenstaande directory instellen als de huidige map.</span><span class="sxs-lookup"><span data-stu-id="ff515-136">Next, open a command line window in Administrator mode, and set the above directory as current directory.</span></span>  
  
 <span data-ttu-id="ff515-137">Voer het hulpprogramma zonder parameters om de uitvoer van de help voor de opdracht:</span><span class="sxs-lookup"><span data-stu-id="ff515-137">To output help for the command, run the tool without parameters:</span></span>  
  
```  
WAImportExport, a client tool for Microsoft Azure Import/Export service. Microsoft (c) 2013, 2014  
  
Copy a Directory:  
    WAImportExport.exe PrepImport  
        /j:<JournalFile> [/logdir:<LogDirectory>] [/id:<SessionId>] [/resumesession]  
        [/abortsession] [/sk:<StorageAccountKey>] [/csas:<ContainerSas>]  
        [/t:<TargetDriveLetter>] [/format] [/silentmode] [/encrypt]  
        [/bk:<BitLockerKey>] [/Disposition:<Disposition>] [/BlobType:<BlobType>]  
        [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]  
        /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory>  
  
Copy a File:  
    WAImportExport.exe PrepImport  
        /j:<JournalFile> [/logdir:<LogDirectory>] [/id:<SessionId>] [/resumesession]  
        [/abortsession] [/sk:<StorageAccountKey>] [/csas:<ContainerSas>]  
        [/t:<TargetDriveLetter>] [/format] [/silentmode] [/encrypt]  
        [/bk:<BitLockerKey>] [/Disposition:<Disposition>] [/BlobType:<BlobType>]  
        [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]  
        /srcfile:<SourceFilePath> /dstblob:<DestinationBlobPath>  
  
Repair a Drive:  
    WAImportExport.exe RepairImport | RepairExport  
        /r:<RepairFile> [/logdir:<LogDirectory>]  
        [/d:<TargetDirectories>] [/bk:<BitLockerKey>]  
        /sn:<StorageAccountName> [/sk:<StorageAccountKey> | /csas:<ContainerSas>]  
        [/CopyLogFile:<DriveCopyLogFile>] [/ManifestFile:<DriveManifestFile>]  
        [/PathMapFile:<DrivePathMapFile>]  
  
Preview an Export Job:  
    WAImportExport.exe PreviewExport  
        [/logdir:<LogDirectory>]  
        /sn:<StorageAccountName> [/sk:<StorageAccountKey> | /csas:<ContainerSas>]  
        /ExportBlobListFile:<ExportBlobListFile> /DriveSize:<DriveSize>  
  
Parameters:  
  
    /j:<JournalFile>  
        - Required. Path to the journal file. Each drive must have one and only one  
          journal file. The journal file corresponding to the target drive must always  
          be specified.  
    /logdir:<LogDirectory>  
        - Optional. The log directory. Verbose log files as well as some temporary  
          files will be written to this directory. If not specified, current directory  
          will be used as the log directory.  
    /id:<SessionId>  
        - Required. The session Id is used to identify a copy session. It is used to  
          ensure accurate recovery of an interrupted copy session. In addition, files  
          that are copied in a copy session are stored in a directory named after the  
          session Id on the target drive.  
    /resumesession  
        - Optional. If the last copy session was terminated abnormally, this parameter  
          can be specified to resume the session.  
    /abortsession  
        - Optional. If the last copy session was terminated abnormally, this parameter  
          can be specified to abort the session.  
    /sn:<StorageAccountName>  
        - Required. Only applicable for RepairImport and RepairExport. The name of  
          the storage account.  
    /sk:<StorageAccountKey>  
        - Optional. The key of the storage account. One of /sk: and /csas: must be  
          specified.  
    /csas:<ContainerSas>  
        - Optional. A container SAS, in format of <ContainerName>?<SasString>, to be  
          used for import the data. One of /sk: and /csas: must be specified.  
    /t:<TargetDriveLetter>  
        - Required. Drive letter of the target drive.  
    /r:<RepairFile>  
        - Required. Only applicable for RepairImport and RepairExport.  
          Path to the file for tracking repair progress. Each drive must have one  
          and only one repair file.  
    /d:<TargetDirectories>  
        - Required. Only applicable for RepairImport and RepairExport.  
          For RepairImport, one or more semicolon-separated directories to repair;  
          For RepairExport, one directory to repair, e.g. root directory of the drive.  
    /format  
        - Optional. If specified, the target drive will be formatted. DO NOT specify  
          this parameter if you do not want to format the drive.  
    /silentmode  
        - Optional. If not specified, the /format parameter will require a confirmation  
          from console before the tool formats the drive. If this parameter is specified,  
          not confirmation will be given for formatting the drive.  
    /encrypt  
        - Optional. If specified, the target drive will be encrypted with BitLocker.  
          If the drive has already been encrypted with BitLocker, do not specify this  
          parameter and instead specify the BitLocker key using the "/k" parameter.  
    /bk:<BitLockerKey>  
        - Optional. The current BitLocker key if the drive has already been encrypted  
          with BitLocker.  
    /Disposition:<Disposition>  
        - Optional. Specifies the behavior when a blob with the same path as the one  
          being imported already exists. Valid values are: rename, no-overwrite and  
          overwrite (case-sensitive). If not specified, "rename" will be used as the  
          default value.  
    /BlobType:<BlobType>  
        - Optional. The blob type for the imported blob(s). Valid values are BlockBlob  
          and PageBlob. If not specified, BlockBlob will be used as the default value.  
    /PropertyFile:<PropertyFile>  
        - Optional. Path to the property file for the file(s) to be imported.  
    /MetadataFile:<MetadataFile>  
        - Optional. Path to the metadata file for the file(s) to be imported.  
    /CopyLogFile:<DriveCopyLogFile>  
        - Required. Only applicable for RepairImport and RepairExport. Path to the  
          drive copy log file (verbose or error).  
    /ManifestFile:<DriveManifestFile>  
        - Required. Only applicable for RepairExport. Path to the drive manifest file.  
    /PathMapFile:<DrivePathMapFile>  
        - Optional. Only applicable for RepairImport. Path to the file containing  
          mappings of file paths relative to the drive root to locations of actual files  
          (tab-delimited). When first specified, it will be populated with file paths  
          with empty targets, which means either they are not found in TargetDirectories,  
          access denied, with invalid name, or they exist in multiple directories. The  
          path map file can be manually edited to include the correct target paths and  
          specified again for the tool to resolve the file paths correctly.  
    /ExportBlobListFile:<ExportBlobListFile>  
        - Required. Path to the XML file containing list of blob paths or blob path  
          prefixes for the blobs to be exported. The file format is the same as the  
          blob list blob format in the Put Job operation of the Import/Export service  
          REST API.  
    /DriveSize:<DriveSize>  
        - Required. Size of drives to be used for export. For example, 500GB, 1.5TB.  
          Note: 1 GB = 1,000,000,000 bytes  
                1 TB = 1,000,000,000,000 bytes  
    /srcdir:<SourceDirectory>  
        - Required. Source directory that contains files to be copied to the  
          target drives.  
    /dstdir:<DestinationBlobVirtualDirectory>  
        - Required. Destination blob virtual directory to which the files will  
          be imported.  
    /srcfile:<SourceFilePath>  
        - Required. Path to the source file to be imported.  
    /dstblob:<DestinationBlobPath>  
        - Required. Destination blob path for the file to be imported.  
    /skipwrite
        - Optional. To skip write process. Used for inplace data drive preparation.
          Be sure to reserve enough space (3 GB per 7TB) for drive manifest file!
Examples:  
  
    Copy a source directory to a drive:  
    WAImportExport.exe PrepImport  
        /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GEL  
        xmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:x /format /encrypt /srcdir:d:\movi  
        es\drama /dstdir:movies/drama/  
  
    Copy another directory to the same drive following the above command:  
    WAImportExport.exe PrepImport  
        /j:9WM35C2V.jrn /id:session#2 /srcdir:d:\movies\action /dstdir:movies/action/  
  
    Copy another file to the same drive following the above commands:  
    WAImportExport.exe PrepImport  
        /j:9WM35C2V.jrn /id:session#3 /srcfile:d:\movies\dvd.vhd /dstblob:movies/dvd.vhd /BlobType:PageBlob  
  
    Preview how many 1.5 TB drives are needed for an export job:  
    WAImportExport.exe PreviewExport  
        /sn:mytestaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7K  
        ysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\temp\myexportbloblist.xml  
        /DriveSize:1.5TB  
  
    Repair an finished import job:  
    WAImportExport.exe RepairImport  
        /r:9WM35C2V.rep /d:X:\ /bk:442926-020713-108086-436744-137335-435358-242242-2795  
        98 /sn:mytestaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94  
        f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\temp\9WM35C2V_error.log 

    Skip write process, inplace data drive preparation:
    WAImportExport.exe PrepImport
        /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GEL
        xmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movi
        es\drama /dstdir:movies/drama/ /skipwrite
```  
  
## <a name="next-steps"></a><span data-ttu-id="ff515-138">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="ff515-138">Next steps</span></span>

* [<span data-ttu-id="ff515-139">Harde schijven voorbereiden voor een importtaak</span><span class="sxs-lookup"><span data-stu-id="ff515-139">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="ff515-140">Een voorbeeldweergave schijfgebruik voor een taak voor het exporteren</span><span class="sxs-lookup"><span data-stu-id="ff515-140">Previewing Drive usage for an export job</span></span>](storage-import-export-tool-previewing-drive-usage-export-v1.md)   
* [<span data-ttu-id="ff515-141">De taakstatus controleren met kopielogboekbestanden</span><span class="sxs-lookup"><span data-stu-id="ff515-141">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="ff515-142">Een importtaak herstellen</span><span class="sxs-lookup"><span data-stu-id="ff515-142">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="ff515-143">Een exporttaak herstellen</span><span class="sxs-lookup"><span data-stu-id="ff515-143">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)   
* [<span data-ttu-id="ff515-144">Problemen met het hulpprogramma Azure Import/Export oplossen</span><span class="sxs-lookup"><span data-stu-id="ff515-144">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
