---
title: aaaSetting Up hello Azure-hulpprogramma voor importeren/exporteren v1 | Microsoft Docs
description: Meer informatie over hoe tooset up Hallo station voorbereidings- en hulpprogramma voor hello Azure Import/Export-service. Dit verwijst toov1 Hallo hulpprogramma voor importeren/exporteren.
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
ms.openlocfilehash: 838db815a7d4e6c04369711ef3eedb31fbb0b1b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-hello-azure-importexport-tool"></a>Instellen van hello Azure-hulpprogramma voor importeren/exporteren
Hallo Microsoft Azure-hulpprogramma voor importeren/exporteren is Hallo station voorbereidings- en hulpprogramma waarmee u met Hallo Microsoft Azure Import/Export-service kunt. U kunt Hallo hulpprogramma gebruiken voor Hallo volgende functies:  
  
-   Voordat u een import-taak maakt, kunt u dit hulpprogramma toocopy toohello vaste gegevensstations u gaat tooship tooa Windows Azure-Datacenter.  
  
-   Nadat een import-taak is voltooid, kunt u dit hulpprogramma toorepair alle blobs zijn beschadigd, ontbreekt of het conflict met andere blobs.  
  
-   Nadat u Hallo-stations van een voltooide exporttaak ontvangt, kunt u dit hulpprogramma toorepair gebruiken bestanden die zijn beschadigd of ontbreekt op Hallo stations.  
  
## <a name="prerequisites"></a>Vereisten  
Als u schijven voor een import-taak voorbereidt, moet u toomeet Hallo volgende vereisten:  
  
-   U moet een actief Azure-abonnement hebben.  
  
-   Uw abonnement vergezeld gaan van een storage-account met voldoende beschikbare ruimte toostore Hallo bestanden u tooimport gaat.  
  
-   Ten minste één van de sleutels voor Hallo moet u voor Hallo storage-account.  
  
-   U moet een computer ('kopie machine' hello) met Windows 7, Windows Server 2008 R2 of een nieuwere Windows-besturingssysteem geïnstalleerd.  
  
-   Hallo .NET Framework 4 moet worden geïnstalleerd op Hallo kopie machine.  
  
-   BitLocker moet zijn ingeschakeld op Hallo kopie machine.  
  
-   U moet een of meer stations waarin gegevens toobe geïmporteerd of leeg 3.5-inch SATA harde schijven verbonden toohello kopie machine.  
  
-   Hallo-bestanden die u van plan bent tooimport moet toegankelijk is vanaf Hallo kopie machine, ongeacht of deze op een netwerkshare of een lokale vaste schijf. 
  
Als u een import die is gedeeltelijk mislukt toorepair probeert, moet u:  
  
-   Hallo kopie-logboekbestanden  
  
-   Hallo opslagaccountsleutel  
  
  Als u toorepair uitvoer gedeeltelijk mislukt probeert is, moet u:  
  
-   Hallo kopie-logboekbestanden  
  
-   Hallo manifest-bestanden (optioneel)  
  
-   Hallo opslagaccountsleutel  
  
## <a name="installing-hello-azure-importexport-tool"></a>Hello Azure-hulpprogramma voor importeren/exporteren installeren  
 Hello Azure-hulpprogramma voor importeren/exporteren bestaat uit de volgende bestanden Hallo:  
  
-   WAImportExport.exe  
  
-   WAImportExport.exe.config  
  
-   WAImportExportCore.dll  
  
-   WAImportExportRepair.dll  
  
-   Microsoft.WindowsAzure.Storage.dll  
  
-   hddid.dll  
  
 Kopieer deze bestanden tooa werkmap, bijvoorbeeld, `c:\WAImportExport`. Vervolgens een opdrachtregel-venster openen in de beheerdersmodus en Hallo boven map instellen als de huidige map.  
  
 toooutput help voor Hallo-opdracht Hallo hulpprogramma zonder parameters uitvoeren:  
  
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
        - Required. Path toohello journal file. Each drive must have one and only one  
          journal file. hello journal file corresponding toohello target drive must always  
          be specified.  
    /logdir:<LogDirectory>  
        - Optional. hello log directory. Verbose log files as well as some temporary  
          files will be written toothis directory. If not specified, current directory  
          will be used as hello log directory.  
    /id:<SessionId>  
        - Required. hello session Id is used tooidentify a copy session. It is used too 
          ensure accurate recovery of an interrupted copy session. In addition, files  
          that are copied in a copy session are stored in a directory named after hello  
          session Id on hello target drive.  
    /resumesession  
        - Optional. If hello last copy session was terminated abnormally, this parameter  
          can be specified tooresume hello session.  
    /abortsession  
        - Optional. If hello last copy session was terminated abnormally, this parameter  
          can be specified tooabort hello session.  
    /sn:<StorageAccountName>  
        - Required. Only applicable for RepairImport and RepairExport. hello name of  
          hello storage account.  
    /sk:<StorageAccountKey>  
        - Optional. hello key of hello storage account. One of /sk: and /csas: must be  
          specified.  
    /csas:<ContainerSas>  
        - Optional. A container SAS, in format of <ContainerName>?<SasString>, toobe  
          used for import hello data. One of /sk: and /csas: must be specified.  
    /t:<TargetDriveLetter>  
        - Required. Drive letter of hello target drive.  
    /r:<RepairFile>  
        - Required. Only applicable for RepairImport and RepairExport.  
          Path toohello file for tracking repair progress. Each drive must have one  
          and only one repair file.  
    /d:<TargetDirectories>  
        - Required. Only applicable for RepairImport and RepairExport.  
          For RepairImport, one or more semicolon-separated directories toorepair;  
          For RepairExport, one directory toorepair, e.g. root directory of hello drive.  
    /format  
        - Optional. If specified, hello target drive will be formatted. DO NOT specify  
          this parameter if you do not want tooformat hello drive.  
    /silentmode  
        - Optional. If not specified, hello /format parameter will require a confirmation  
          from console before hello tool formats hello drive. If this parameter is specified,  
          not confirmation will be given for formatting hello drive.  
    /encrypt  
        - Optional. If specified, hello target drive will be encrypted with BitLocker.  
          If hello drive has already been encrypted with BitLocker, do not specify this  
          parameter and instead specify hello BitLocker key using hello "/k" parameter.  
    /bk:<BitLockerKey>  
        - Optional. hello current BitLocker key if hello drive has already been encrypted  
          with BitLocker.  
    /Disposition:<Disposition>  
        - Optional. Specifies hello behavior when a blob with hello same path as hello one  
          being imported already exists. Valid values are: rename, no-overwrite and  
          overwrite (case-sensitive). If not specified, "rename" will be used as hello  
          default value.  
    /BlobType:<BlobType>  
        - Optional. hello blob type for hello imported blob(s). Valid values are BlockBlob  
          and PageBlob. If not specified, BlockBlob will be used as hello default value.  
    /PropertyFile:<PropertyFile>  
        - Optional. Path toohello property file for hello file(s) toobe imported.  
    /MetadataFile:<MetadataFile>  
        - Optional. Path toohello metadata file for hello file(s) toobe imported.  
    /CopyLogFile:<DriveCopyLogFile>  
        - Required. Only applicable for RepairImport and RepairExport. Path toohello  
          drive copy log file (verbose or error).  
    /ManifestFile:<DriveManifestFile>  
        - Required. Only applicable for RepairExport. Path toohello drive manifest file.  
    /PathMapFile:<DrivePathMapFile>  
        - Optional. Only applicable for RepairImport. Path toohello file containing  
          mappings of file paths relative toohello drive root toolocations of actual files  
          (tab-delimited). When first specified, it will be populated with file paths  
          with empty targets, which means either they are not found in TargetDirectories,  
          access denied, with invalid name, or they exist in multiple directories. hello  
          path map file can be manually edited tooinclude hello correct target paths and  
          specified again for hello tool tooresolve hello file paths correctly.  
    /ExportBlobListFile:<ExportBlobListFile>  
        - Required. Path toohello XML file containing list of blob paths or blob path  
          prefixes for hello blobs toobe exported. hello file format is hello same as hello  
          blob list blob format in hello Put Job operation of hello Import/Export service  
          REST API.  
    /DriveSize:<DriveSize>  
        - Required. Size of drives toobe used for export. For example, 500GB, 1.5TB.  
          Note: 1 GB = 1,000,000,000 bytes  
                1 TB = 1,000,000,000,000 bytes  
    /srcdir:<SourceDirectory>  
        - Required. Source directory that contains files toobe copied toohello  
          target drives.  
    /dstdir:<DestinationBlobVirtualDirectory>  
        - Required. Destination blob virtual directory toowhich hello files will  
          be imported.  
    /srcfile:<SourceFilePath>  
        - Required. Path toohello source file toobe imported.  
    /dstblob:<DestinationBlobPath>  
        - Required. Destination blob path for hello file toobe imported.  
    /skipwrite
        - Optional. tooskip write process. Used for inplace data drive preparation.
          Be sure tooreserve enough space (3 GB per 7TB) for drive manifest file!
Examples:  
  
    Copy a source directory tooa drive:  
    WAImportExport.exe PrepImport  
        /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GEL  
        xmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:x /format /encrypt /srcdir:d:\movi  
        es\drama /dstdir:movies/drama/  
  
    Copy another directory toohello same drive following hello above command:  
    WAImportExport.exe PrepImport  
        /j:9WM35C2V.jrn /id:session#2 /srcdir:d:\movies\action /dstdir:movies/action/  
  
    Copy another file toohello same drive following hello above commands:  
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
  
## <a name="next-steps"></a>Volgende stappen

* [Harde schijven voorbereiden voor een importtaak](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [Een voorbeeldweergave schijfgebruik voor een taak voor het exporteren](../storage-import-export-tool-previewing-drive-usage-export-v1.md)   
* [De taakstatus controleren met kopielogboekbestanden](../storage-import-export-tool-reviewing-job-status-v1.md)   
* [Een importtaak herstellen](../storage-import-export-tool-repairing-an-import-job-v1.md)   
* [Een exporttaak herstellen](../storage-import-export-tool-repairing-an-export-job-v1.md)   
* [Het oplossen van problemen hello Azure-hulpprogramma voor importeren/exporteren](storage-import-export-tool-troubleshooting-v1.md)
