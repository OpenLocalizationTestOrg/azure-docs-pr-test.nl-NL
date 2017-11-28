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
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="0a0ca-104">Snelzoekgids voor veelgebruikte opdrachten voor importtaken</span><span class="sxs-lookup"><span data-stu-id="0a0ca-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="0a0ca-105">Deze sectie biedt dat een snelle verwijzingen voor een aantal veelgebruikte opdrachten.</span><span class="sxs-lookup"><span data-stu-id="0a0ca-105">This section provides a quick references for some frequently used commands.</span></span> <span data-ttu-id="0a0ca-106">Zie voor gedetailleerde informatie over het gebruik, [harde schijven voorbereiden voor een Import-taak](storage-import-export-tool-preparing-hard-drives-import-v1.md).</span><span class="sxs-lookup"><span data-stu-id="0a0ca-106">For detailed usage, see [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-hello-disks-when-data-already-copied-toohello-disks"></a><span data-ttu-id="0a0ca-107">Hallo schijven voorbereiden wanneer gegevens gekopieerd al toohello schijven</span><span class="sxs-lookup"><span data-stu-id="0a0ca-107">Prepare hello disks when data already copied toohello disks</span></span>
 <span data-ttu-id="0a0ca-108">Hier volgt een voorbeeld opdracht tooprepare een schijven wanneer gegevens gekopieerd al toohello harde schijf die nog niet is nog is versleuteld met BitLocker:</span><span class="sxs-lookup"><span data-stu-id="0a0ca-108">Here is a sample command tooprepare a disks when data already copied toohello hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a><span data-ttu-id="0a0ca-109">Een enkele directory tooa harde schijf kopiëren</span><span class="sxs-lookup"><span data-stu-id="0a0ca-109">Copy a single directory tooa hard drive</span></span>  
 <span data-ttu-id="0a0ca-110">Hier volgt een voorbeeld opdracht toocopy één bron directory tooa harde schijf die nog niet is nog is versleuteld met BitLocker:</span><span class="sxs-lookup"><span data-stu-id="0a0ca-110">Here is a sample command toocopy a single source directory tooa hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-wwo-directories-tooa-hard-drive"></a><span data-ttu-id="0a0ca-111">Wwo mappen tooa harde schijf kopiëren</span><span class="sxs-lookup"><span data-stu-id="0a0ca-111">Copy wwo directories tooa hard drive</span></span>  
 <span data-ttu-id="0a0ca-112">toocopy twee bron mappen tooa station, moet u twee opdrachten.</span><span class="sxs-lookup"><span data-stu-id="0a0ca-112">toocopy two source directories tooa drive, you will need two commands.</span></span>  
  
 <span data-ttu-id="0a0ca-113">Hello eerste opdracht geeft u de logboekmap hello, opslagaccountsleutel, doel stationsletter en `format/encrypt` vereisten in toevoeging toohello algemene parameters:</span><span class="sxs-lookup"><span data-stu-id="0a0ca-113">hello first command specifies hello log directory, storage account key, target drive letter and `format/encrypt` requirements, in addition toohello common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="0a0ca-114">de tweede opdracht Hallo geeft Hallo journal-bestand, een nieuwe sessie-ID en de bron- en doellocaties Hallo:</span><span class="sxs-lookup"><span data-stu-id="0a0ca-114">hello second command specifies hello journal file, a new session ID, and hello source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="0a0ca-115">Kopieer een groot bestand tooa harde schijf in een tweede kopieersessie</span><span class="sxs-lookup"><span data-stu-id="0a0ca-115">Copy a large file tooa hard drive in a second copy session</span></span>  
 <span data-ttu-id="0a0ca-116">Hier volgt een voorbeeld van een opdracht die door een enkele grote bestanden tooa-station dat is voorbereid in een eerdere kopieersessie. worden gekopieerd:</span><span class="sxs-lookup"><span data-stu-id="0a0ca-116">Here is a sample command that copies a single large file tooa drive that has been prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="0a0ca-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="0a0ca-117">Next steps</span></span>

* [<span data-ttu-id="0a0ca-118">Voorbeeld werkstroom tooprepare harde schijven voor een import-taak</span><span class="sxs-lookup"><span data-stu-id="0a0ca-118">Sample workflow tooprepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
