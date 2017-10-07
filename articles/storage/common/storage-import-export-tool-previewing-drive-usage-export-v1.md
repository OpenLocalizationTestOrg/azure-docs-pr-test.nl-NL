---
title: aaaPreviewing schijfgebruik voor een taak van de export Azure Import/Export - v1 | Microsoft Docs
description: Meer informatie over hoe toopreview Hallo lijst met blobs u hebt geselecteerd voor een taak voor het exporteren in hello Azure Import/Export-service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 7707d744-7ec7-4de8-ac9b-93a18608dc9a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 7378c159f6d11702cda9ae7654e84d85f9b671b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a>Op voorhand het schijfgebruik voor een exporttaak bekijken
Voordat u een exporttaak maakt, moet u een reeks blobs toobe geëxporteerd toochoose. Hallo Microsoft Azure Import/Export-service kunt u een lijst met blob-paden toouse of blob-prefixes toorepresent Hallo blobs die u hebt geselecteerd.  
  
Vervolgens moet u toodetermine hoeveel stations moet u toosend. Hallo hulpprogramma voor importeren/exporteren biedt Hallo `PreviewExport` opdracht toopreview schijfgebruik voor Hallo blobs die u hebt geselecteerd, op basis van de grootte Hallo Hallo stations u gaat toouse.

## <a name="command-line-parameters"></a>Opdrachtregelparameters

U kunt volgende parameters bij gebruik van Hallo Hallo `PreviewExport` opdracht Hallo hulpprogramma voor importeren/exporteren.

|Opdrachtregelparameter|Beschrijving|  
|--------------------------|-----------------|  
|**schakeloptie/LOGDIR op:**< LogDirectory\>|Optioneel. Hallo logboekmap. Uitgebreide logboekbestanden geschreven toothis directory. Als er geen logboekmap is opgegeven, wordt de huidige map hello worden gebruikt als Hallo logboekmap.|  
|**/sn:**< StorageAccountName\>|Vereist. Hallo-naam van Hallo storage-account voor Hallo taak exporteren.|  
|**/SK:**< StorageAccountKey\>|Vereist als een container SAS is niet opgegeven. Hallo-toegangssleutel voor opslagaccount Hallo voor Hallo taak exporteren.|  
|**/csas:**< ContainerSas\>|Vereist als de sleutel van een opslagaccount is niet opgegeven. Hallo container SAS voor aanbieding Hallo blobs toobe geëxporteerd in Hallo exporttaak.|  
|**/ ExportBlobListFile:**< ExportBlobListFile\>|Vereist. Pad toohello XML-bestand met lijst met blob-paden of blob-pad voorvoegsels voor Hallo blobs toobe geëxporteerd. Hallo-bestandsindeling die is gebruikt in Hallo `BlobListBlobPath` -element in Hallo [taak plaatsen](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) bewerking Hallo Import/Export-service REST-API.|  
|**/ DriveSize:**< DriveSize\>|Vereist. grootte van stations toouse voor een exporttaak Hallo *bijvoorbeeld*, 500 GB, 1,5 TB.|  

## <a name="command-line-example"></a>Voorbeeld van de opdrachtregel

Hallo volgende voorbeeld toont Hallo `PreviewExport` opdracht:  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
Hallo kan blob-exportbestand bevatten blob-namen en blob-voorvoegsels, zoals hier wordt weergegeven:  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

Hello Azure-hulpprogramma voor importeren/exporteren geeft een lijst van alle blobs toobe geëxporteerd en berekent hoe ze in de stations Hallo grootte opgegeven, rekening houdend met alle benodigde overhead maakt vervolgens een schatting van het aantal stations dat Hallo toopack nodig toohold Hallo blobs en schijfgebruik informatie.  
  
Hier volgt een voorbeeld van uitvoer hello, met informatief logboeken die worden weggelaten:  
  
```  
Number of unique blob paths/prefixes:   3  
Number of duplicate blob paths/prefixes:        0  
Number of nonexistent blob paths/prefixes:      1  
  
Drive size:     500.00 GB  
Number of blobs that can be exported:   6  
Number of blobs that cannot be exported:        2  
Number of drives needed:        3  
        Drive #1:       blobs = 1, occupied space = 454.74 GB  
        Drive #2:       blobs = 3, occupied space = 441.37 GB  
        Drive #3:       blobs = 2, occupied space = 131.28 GB    
```  
  
## <a name="next-steps"></a>Volgende stappen

* [Naslaginformatie over Azure hulpprogramma voor importeren/exporteren](../storage-import-export-tool-how-to-v1.md)
