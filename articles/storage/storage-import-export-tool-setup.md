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
# <a name="setting-up-hello-azure-importexport-tool"></a>Instellen van hello Azure-hulpprogramma voor importeren/exporteren

Hallo Microsoft Azure-hulpprogramma voor importeren/exporteren is Hallo station voorbereidings- en hulpprogramma waarmee u met Hallo Microsoft Azure Import/Export-service kunt. U kunt Hallo hulpprogramma gebruiken voor Hallo volgende functies:

* Voordat u een import-taak maakt, kunt u dit hulpprogramma toocopy toohello vaste gegevensstations u gaat tooship tooan Azure-Datacenter.
* Nadat een import-taak is voltooid, kunt u dit hulpprogramma toorepair alle blobs zijn beschadigd, ontbreekt of het conflict met andere blobs.
* Nadat u Hallo-stations van een voltooide exporttaak ontvangt, kunt u dit hulpprogramma toorepair gebruiken bestanden die zijn beschadigd of ontbreekt op Hallo stations.

## <a name="prerequisites"></a>Vereisten

Als u **voorbereiden stations** voor een import-taak Hallo volgende vereisten moet worden voldaan:

* U moet een actief Azure-abonnement hebben.
* Uw abonnement vergezeld gaan van een storage-account met voldoende beschikbare ruimte toostore Hallo bestanden u tooimport gaat.
* U moet ten minste één Hallo toegang toegangscodes voor opslag.
* U moet een computer ('kopie machine' hello) met Windows 7, Windows Server 2008 R2 of een nieuwere Windows-besturingssysteem geïnstalleerd.
* Hallo .NET Framework 4 moet worden geïnstalleerd op Hallo kopie machine.
* BitLocker moet zijn ingeschakeld op Hallo kopie machine.
* U moet een of meer leeg 3.5-inch SATA harde schijven toohello kopie machine verbonden.
* Hallo-bestanden die u van plan bent tooimport moet toegankelijk is vanaf Hallo kopie machine, ongeacht of deze op een netwerkshare of een lokale vaste schijf.

Als u te probeert**herstellen van een import** die is gedeeltelijk mislukt, moet u:

* Hallo kopie-logboekbestanden
* Hallo opslagaccountsleutel

Als u te probeert**herstellen exporteren van een** die is gedeeltelijk mislukt, moet u:

* Hallo kopie-logboekbestanden
* Hallo manifest-bestanden (optioneel)
* Hallo opslagaccountsleutel

## <a name="installing-hello-azure-importexport-tool"></a>Hello Azure-hulpprogramma voor importeren/exporteren installeren

Eerst [hello Azure-hulpprogramma voor importeren/exporteren downloaden](https://www.microsoft.com/download/details.aspx?id=55280) en pak tooa map op uw computer, bijvoorbeeld `c:\WAImportExport`.

Hello Azure-hulpprogramma voor importeren/exporteren bestaat uit de volgende bestanden Hallo:

* DataSet.csv
* driveset.csv
* hddid.dll
* Microsoft.Data.Services.Client.dll
* Microsoft.WindowsAzure.Storage.dll
* Microsoft.WindowsAzure.Storage.pdb
* Microsoft.WindowsAzure.Storage.xml
* WAImportExport.exe
* WAImportExport.exe.config
* WAImportExport.pdb
* WAImportExportCore.dll
* WAImportExportCore.pdb
* WAImportExportRepair.dll
* WAImportExportRepair.pdb

Open een opdrachtpromptvenster in vervolgens **beheerdersmodus**, en de wijziging in Hallo directory Hallo met bestanden hebt uitgepakt.

help voor Hallo-opdracht Hallo hulpprogramma uitvoeren toooutput (`WAImportExport.exe`) zonder parameters:

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

## <a name="next-steps"></a>Volgende stappen

* [Harde schijven voorbereiden voor een importtaak](storage-import-export-tool-preparing-hard-drives-import.md)
* [Op voorhand het schijfgebruik voor een exporttaak bekijken](storage-import-export-tool-previewing-drive-usage-export-v1.md)
* [De taakstatus controleren met kopielogboekbestanden](storage-import-export-tool-reviewing-job-status-v1.md)
* [Een importtaak herstellen](storage-import-export-tool-repairing-an-import-job-v1.md)
* [Een exporttaak herstellen](storage-import-export-tool-repairing-an-export-job-v1.md)
* [Het oplossen van problemen hello Azure-hulpprogramma voor importeren/exporteren](storage-import-export-tool-troubleshooting-v1.md)
