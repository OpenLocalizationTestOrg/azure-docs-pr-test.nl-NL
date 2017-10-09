---
title: aaaSetting up hello Azure-hulpprogramma voor importeren/exporteren | Microsoft Docs
description: Meer informatie over hoe tooset up Hallo station voorbereidings- en hulpprogramma voor hello Azure Import/Export-service.
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
ms.date: 06/29/2017
ms.author: muralikk
ms.openlocfilehash: ee5bb99bd84ea5ee2f6b6e99c5a375b215e94ea8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-hello-azure-importexport-tool"></a><span data-ttu-id="d6ce0-103">Instellen van hello Azure-hulpprogramma voor importeren/exporteren</span><span class="sxs-lookup"><span data-stu-id="d6ce0-103">Setting up hello Azure Import/Export Tool</span></span>

<span data-ttu-id="d6ce0-104">Hallo Microsoft Azure-hulpprogramma voor importeren/exporteren is Hallo station voorbereidings- en hulpprogramma waarmee u met Hallo Microsoft Azure Import/Export-service kunt.</span><span class="sxs-lookup"><span data-stu-id="d6ce0-104">hello Microsoft Azure Import/Export Tool is hello drive preparation and repair tool that you can use with hello Microsoft Azure Import/Export service.</span></span> <span data-ttu-id="d6ce0-105">U kunt Hallo hulpprogramma gebruiken voor Hallo volgende functies:</span><span class="sxs-lookup"><span data-stu-id="d6ce0-105">You can use hello tool for hello following functions:</span></span>

* <span data-ttu-id="d6ce0-106">Voordat u een import-taak maakt, kunt u dit hulpprogramma toocopy toohello vaste gegevensstations u gaat tooship tooan Azure-Datacenter.</span><span class="sxs-lookup"><span data-stu-id="d6ce0-106">Before creating an import job, you can use this tool toocopy data toohello hard drives you are going tooship tooan Azure data center.</span></span>
* <span data-ttu-id="d6ce0-107">Nadat een import-taak is voltooid, kunt u dit hulpprogramma toorepair alle blobs zijn beschadigd, ontbreekt of het conflict met andere blobs.</span><span class="sxs-lookup"><span data-stu-id="d6ce0-107">After an import job has completed, you can use this tool toorepair any blobs that were corrupted, were missing, or conflicted with other blobs.</span></span>
* <span data-ttu-id="d6ce0-108">Nadat u Hallo-stations van een voltooide exporttaak ontvangt, kunt u dit hulpprogramma toorepair gebruiken bestanden die zijn beschadigd of ontbreekt op Hallo stations.</span><span class="sxs-lookup"><span data-stu-id="d6ce0-108">After you receive hello drives from a completed export job, you can use this tool toorepair any files that were corrupted or missing on hello drives.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6ce0-109">Vereisten</span><span class="sxs-lookup"><span data-stu-id="d6ce0-109">Prerequisites</span></span>

<span data-ttu-id="d6ce0-110">Als u **voorbereiden stations** voor een import-taak Hallo volgende vereisten moet worden voldaan:</span><span class="sxs-lookup"><span data-stu-id="d6ce0-110">If you are **preparing drives** for an import job, hello following prerequisites must be met:</span></span>

* <span data-ttu-id="d6ce0-111">U moet een actief Azure-abonnement hebben.</span><span class="sxs-lookup"><span data-stu-id="d6ce0-111">You must have an active Azure subscription.</span></span>
* <span data-ttu-id="d6ce0-112">Uw abonnement vergezeld gaan van een storage-account met voldoende beschikbare ruimte toostore Hallo bestanden u tooimport gaat.</span><span class="sxs-lookup"><span data-stu-id="d6ce0-112">Your subscription must include a storage account with enough available space toostore hello files you are going tooimport.</span></span>
* <span data-ttu-id="d6ce0-113">U moet ten minste één Hallo toegang toegangscodes voor opslag.</span><span class="sxs-lookup"><span data-stu-id="d6ce0-113">You need at least one of hello storage account access keys.</span></span>
* <span data-ttu-id="d6ce0-114">U moet een computer ('kopie machine' hello) met Windows 7, Windows Server 2008 R2 of een nieuwere Windows-besturingssysteem geïnstalleerd.</span><span class="sxs-lookup"><span data-stu-id="d6ce0-114">You need a computer (hello "copy machine") with Windows 7, Windows Server 2008 R2, or a newer Windows operating system installed.</span></span>
* <span data-ttu-id="d6ce0-115">Hallo .NET Framework 4 moet worden geïnstalleerd op Hallo kopie machine.</span><span class="sxs-lookup"><span data-stu-id="d6ce0-115">hello .NET Framework 4 must be installed on hello copy machine.</span></span>
* <span data-ttu-id="d6ce0-116">BitLocker moet zijn ingeschakeld op Hallo kopie machine.</span><span class="sxs-lookup"><span data-stu-id="d6ce0-116">BitLocker must be enabled on hello copy machine.</span></span>
* <span data-ttu-id="d6ce0-117">U moet een of meer leeg 3.5-inch SATA harde schijven toohello kopie machine verbonden.</span><span class="sxs-lookup"><span data-stu-id="d6ce0-117">You need one or more empty 3.5-inch SATA hard drives connected toohello copy machine.</span></span>
* <span data-ttu-id="d6ce0-118">Hallo-bestanden die u van plan bent tooimport moet toegankelijk is vanaf Hallo kopie machine, ongeacht of deze op een netwerkshare of een lokale vaste schijf.</span><span class="sxs-lookup"><span data-stu-id="d6ce0-118">hello files you plan tooimport must be accessible from hello copy machine, whether they are on a network share or a local hard drive.</span></span>

<span data-ttu-id="d6ce0-119">Als u te probeert**herstellen van een import** die is gedeeltelijk mislukt, moet u:</span><span class="sxs-lookup"><span data-stu-id="d6ce0-119">If you are attempting too**repair an import** that has partially failed, you need:</span></span>

* <span data-ttu-id="d6ce0-120">Hallo kopie-logboekbestanden</span><span class="sxs-lookup"><span data-stu-id="d6ce0-120">hello copy log files</span></span>
* <span data-ttu-id="d6ce0-121">Hallo opslagaccountsleutel</span><span class="sxs-lookup"><span data-stu-id="d6ce0-121">hello storage account key</span></span>

<span data-ttu-id="d6ce0-122">Als u te probeert**herstellen exporteren van een** die is gedeeltelijk mislukt, moet u:</span><span class="sxs-lookup"><span data-stu-id="d6ce0-122">If you are attempting too**repair an export**  that has partially failed, you need:</span></span>

* <span data-ttu-id="d6ce0-123">Hallo kopie-logboekbestanden</span><span class="sxs-lookup"><span data-stu-id="d6ce0-123">hello copy log files</span></span>
* <span data-ttu-id="d6ce0-124">Hallo manifest-bestanden (optioneel)</span><span class="sxs-lookup"><span data-stu-id="d6ce0-124">hello manifest files (optional)</span></span>
* <span data-ttu-id="d6ce0-125">Hallo opslagaccountsleutel</span><span class="sxs-lookup"><span data-stu-id="d6ce0-125">hello storage account key</span></span>

## <a name="installing-hello-azure-importexport-tool"></a><span data-ttu-id="d6ce0-126">Hello Azure-hulpprogramma voor importeren/exporteren installeren</span><span class="sxs-lookup"><span data-stu-id="d6ce0-126">Installing hello Azure Import/Export Tool</span></span>

<span data-ttu-id="d6ce0-127">Eerst [hello Azure-hulpprogramma voor importeren/exporteren downloaden](https://www.microsoft.com/download/details.aspx?id=55280) en pak tooa map op uw computer, bijvoorbeeld `c:\WAImportExport`.</span><span class="sxs-lookup"><span data-stu-id="d6ce0-127">First, [download hello Azure Import/Export Tool](https://www.microsoft.com/download/details.aspx?id=55280) and extract it tooa directory on your computer, for example `c:\WAImportExport`.</span></span>

<span data-ttu-id="d6ce0-128">Hello Azure-hulpprogramma voor importeren/exporteren bestaat uit de volgende bestanden Hallo:</span><span class="sxs-lookup"><span data-stu-id="d6ce0-128">hello Azure Import/Export Tool consists of hello following files:</span></span>

* <span data-ttu-id="d6ce0-129">DataSet.csv</span><span class="sxs-lookup"><span data-stu-id="d6ce0-129">dataset.csv</span></span>
* <span data-ttu-id="d6ce0-130">driveset.csv</span><span class="sxs-lookup"><span data-stu-id="d6ce0-130">driveset.csv</span></span>
* <span data-ttu-id="d6ce0-131">hddid.dll</span><span class="sxs-lookup"><span data-stu-id="d6ce0-131">hddid.dll</span></span>
* <span data-ttu-id="d6ce0-132">Microsoft.Data.Services.Client.dll</span><span class="sxs-lookup"><span data-stu-id="d6ce0-132">Microsoft.Data.Services.Client.dll</span></span>
* <span data-ttu-id="d6ce0-133">Microsoft.WindowsAzure.Storage.dll</span><span class="sxs-lookup"><span data-stu-id="d6ce0-133">Microsoft.WindowsAzure.Storage.dll</span></span>
* <span data-ttu-id="d6ce0-134">Microsoft.WindowsAzure.Storage.pdb</span><span class="sxs-lookup"><span data-stu-id="d6ce0-134">Microsoft.WindowsAzure.Storage.pdb</span></span>
* <span data-ttu-id="d6ce0-135">Microsoft.WindowsAzure.Storage.xml</span><span class="sxs-lookup"><span data-stu-id="d6ce0-135">Microsoft.WindowsAzure.Storage.xml</span></span>
* <span data-ttu-id="d6ce0-136">WAImportExport.exe</span><span class="sxs-lookup"><span data-stu-id="d6ce0-136">WAImportExport.exe</span></span>
* <span data-ttu-id="d6ce0-137">WAImportExport.exe.config</span><span class="sxs-lookup"><span data-stu-id="d6ce0-137">WAImportExport.exe.config</span></span>
* <span data-ttu-id="d6ce0-138">WAImportExport.pdb</span><span class="sxs-lookup"><span data-stu-id="d6ce0-138">WAImportExport.pdb</span></span>
* <span data-ttu-id="d6ce0-139">WAImportExportCore.dll</span><span class="sxs-lookup"><span data-stu-id="d6ce0-139">WAImportExportCore.dll</span></span>
* <span data-ttu-id="d6ce0-140">WAImportExportCore.pdb</span><span class="sxs-lookup"><span data-stu-id="d6ce0-140">WAImportExportCore.pdb</span></span>
* <span data-ttu-id="d6ce0-141">WAImportExportRepair.dll</span><span class="sxs-lookup"><span data-stu-id="d6ce0-141">WAImportExportRepair.dll</span></span>
* <span data-ttu-id="d6ce0-142">WAImportExportRepair.pdb</span><span class="sxs-lookup"><span data-stu-id="d6ce0-142">WAImportExportRepair.pdb</span></span>

<span data-ttu-id="d6ce0-143">Open een opdrachtpromptvenster in vervolgens **beheerdersmodus**, en de wijziging in Hallo directory Hallo met bestanden hebt uitgepakt.</span><span class="sxs-lookup"><span data-stu-id="d6ce0-143">Next, open a Command Prompt window in **Administrator mode**, and change into hello directory containing hello extracted files.</span></span>

<span data-ttu-id="d6ce0-144">help voor Hallo-opdracht Hallo hulpprogramma uitvoeren toooutput (`WAImportExport.exe`) zonder parameters:</span><span class="sxs-lookup"><span data-stu-id="d6ce0-144">toooutput help for hello command, run hello tool (`WAImportExport.exe`) without parameters:</span></span>

```
WAImportExport, a client tool for Windows Azure Import/Export Service. Microsoft (c) 2013


Copy directories and/or files with a new copy session:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>]
        [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>]
        DataSet:<dataset.csv>

Add more drives:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AdditionalDriveSet:<driveset.csv>

Abort an interrupted copy session:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AbortSession

Resume an interrupted copy session:
    WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /ResumeSession

List drives:
    WAImportExport.exe PrepImport /j:<JournalFile> /ListDrives

List copy sessions:
    WAImportExport.exe PrepImport /j:<JournalFile> /ListCopySessions

Repair a Drive:
    WAImportExport.exe RepairImport | RepairExport
        /r:<RepairFile> [/logdir:<LogDirectory>]
        [/d:<TargetDirectories>] [/bk:<BitLockerKey>]
        /sn:<StorageAccountName> /sk:<StorageAccountKey>
        [/CopyLogFile:<DriveCopyLogFile>] [/ManifestFile:<DriveManifestFile>]
        [/PathMapFile:<DrivePathMapFile>]

Preview an Export Job:
    WAImportExport.exe PreviewExport
        [/logdir:<LogDirectory>]
        /sn:<StorageAccountName> /sk:<StorageAccountKey>
        /ExportBlobListFile:<ExportBlobListFile> /DriveSize:<DriveSize>

Parameters:

    /j:<JournalFile>
        - Required. Path toohello journal file. A journal file tracks a set of drives and
          records hello progress in preparing these drives. hello journal file must always
          be specified.
    /logdir:<LogDirectory>
        - Optional. hello log directory. Verbose log files as well as some temporary
          files will be written toothis directory. If not specified, current directory
          will be used as hello log directory. hello log directory can be specified only
          once for hello same journal file.
    /id:<SessionId>
        - Optional. hello session Id is used tooidentify a copy session. It is used to
          ensure accurate recovery of an interrupted copy session.
    /ResumeSession
        - Optional. If hello last copy session was terminated abnormally, this parameter
          can be specified tooresume hello session.
    /AbortSession
        - Optional. If hello last copy session was terminated abnormally, this parameter
          can be specified tooabort hello session.
    /sn:<StorageAccountName>
        - Required. Only applicable for RepairImport and RepairExport. hello name of
          hello storage account.
    /sk:<StorageAccountKey>
        - Required. hello key of hello storage account.
    /InitialDriveSet:<driveset.csv>
        - Required. A .csv file that contains a list of drives tooprepare.
    /AdditionalDriveSet:<driveset.csv>
        - Required. A .csv file that contains a list of additional drives toobe added.
    /r:<RepairFile>
        - Required. Only applicable for RepairImport and RepairExport.
          Path toohello file for tracking repair progress. Each drive must have one
          and only one repair file.
    /d:<TargetDirectories>
        - Required. Only applicable for RepairImport and RepairExport.
          For RepairImport, one or more semicolon-separated directories toorepair;
          For RepairExport, one directory toorepair, e.g. root directory of hello drive.
    /CopyLogFile:<DriveCopyLogFile>
        - Required. Only applicable for RepairImport and RepairExport. Path toothe
          drive copy log file (verbose or error).
    /ManifestFile:<DriveManifestFile>
        - Required. Only applicable for RepairExport. Path toohello drive manifest file.
    /PathMapFile:<DrivePathMapFile>
        - Optional. Only applicable for RepairImport. Path toohello file containing
          mappings of file paths relative toohello drive root toolocations of actual files
          (tab-delimited). When first specified, it will be populated with file paths
          with empty targets, which means either they are not found in TargetDirectories,
          access denied, with invalid name, or they exist in multiple directories. The
          path map file can be manually edited tooinclude hello correct target paths and
          specified again for hello tool tooresolve hello file paths correctly.
    /ExportBlobListFile:<ExportBlobListFile>
        - Required. Path toohello XML file containing list of blob paths or blob path
          prefixes for hello blobs toobe exported. hello file format is hello same as the
          blob list blob format in hello Put Job operation of hello Import/Export Service
          REST API.
    /DriveSize:<DriveSize>
        - Required. Size of drives toobe used for export. For example, 500GB, 1.5TB.
          Note: 1 GB = 1,000,000,000 bytes
                1 TB = 1,000,000,000,000 bytes
    /DataSet:<dataset.csv>
        - Required. A .csv file that contains a list of directories and/or a list files
          toobe copied tootarget drives.

    /silentmode
        - Optional. If not specified, it will remind you hello requirement of drives and
          need your confirmation toocontinue.

Examples:

    Copy a data set tooa drive:
    WAImportExport.exe PrepImport
        /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GEL
        xmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /InitialDriveSet:driveset1.csv
        /DataSet:data.csv

    Copy another dataset toohello same drive following hello above command:
    WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#2 /DataSet:dataset2.csv

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
```

## <a name="next-steps"></a><span data-ttu-id="d6ce0-145">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d6ce0-145">Next steps</span></span>

* [<span data-ttu-id="d6ce0-146">Harde schijven voorbereiden voor een importtaak</span><span class="sxs-lookup"><span data-stu-id="d6ce0-146">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import.md)
* [<span data-ttu-id="d6ce0-147">Op voorhand het schijfgebruik voor een exporttaak bekijken</span><span class="sxs-lookup"><span data-stu-id="d6ce0-147">Previewing drive usage for an export job</span></span>](storage-import-export-tool-previewing-drive-usage-export-v1.md)
* [<span data-ttu-id="d6ce0-148">De taakstatus controleren met kopielogboekbestanden</span><span class="sxs-lookup"><span data-stu-id="d6ce0-148">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)
* [<span data-ttu-id="d6ce0-149">Een importtaak herstellen</span><span class="sxs-lookup"><span data-stu-id="d6ce0-149">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)
* [<span data-ttu-id="d6ce0-150">Een exporttaak herstellen</span><span class="sxs-lookup"><span data-stu-id="d6ce0-150">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)
* [<span data-ttu-id="d6ce0-151">Het oplossen van problemen hello Azure-hulpprogramma voor importeren/exporteren</span><span class="sxs-lookup"><span data-stu-id="d6ce0-151">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
