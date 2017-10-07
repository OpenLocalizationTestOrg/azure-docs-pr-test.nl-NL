---
title: verwijzing voor opdrachten in de taak voor het importeren van Azure-hulpprogramma voor importeren/exporteren - v1 aaaQuick | Microsoft Docs
description: Hulpprogramma voor importeren/exporteren opdracht naslaginformatie over Azure voor opdrachten van veelgebruikte import-taak. Dit verwijst toov1 Hallo hulpprogramma voor importeren/exporteren.
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
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: e36f065e5d23268758cf6b6db9428fe8a8e1056d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a>Snelzoekgids voor veelgebruikte opdrachten voor importtaken
Deze sectie biedt dat een snelle verwijzingen voor een aantal veelgebruikte opdrachten. Zie voor gedetailleerde informatie over het gebruik, [harde schijven voorbereiden voor een Import-taak](storage-import-export-tool-preparing-hard-drives-import-v1.md).  

## <a name="prepare-hello-disks-when-data-already-copied-toohello-disks"></a>Hallo schijven voorbereiden wanneer gegevens gekopieerd al toohello schijven
 Hier volgt een voorbeeld opdracht tooprepare een schijven wanneer gegevens gekopieerd al toohello harde schijf die nog niet is nog is versleuteld met BitLocker:  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a>Een enkele directory tooa harde schijf kopiëren  
 Hier volgt een voorbeeld opdracht toocopy één bron directory tooa harde schijf die nog niet is nog is versleuteld met BitLocker:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-wwo-directories-tooa-hard-drive"></a>Wwo mappen tooa harde schijf kopiëren  
 toocopy twee bron mappen tooa station, moet u twee opdrachten.  
  
 Hello eerste opdracht geeft u de logboekmap hello, opslagaccountsleutel, doel stationsletter en `format/encrypt` vereisten in toevoeging toohello algemene parameters:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 de tweede opdracht Hallo geeft Hallo journal-bestand, een nieuwe sessie-ID en de bron- en doellocaties Hallo:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a>Kopieer een groot bestand tooa harde schijf in een tweede kopieersessie  
 Hier volgt een voorbeeld van een opdracht die door een enkele grote bestanden tooa-station dat is voorbereid in een eerdere kopieersessie. worden gekopieerd:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a>Volgende stappen

* [Voorbeeld werkstroom tooprepare harde schijven voor een import-taak](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
