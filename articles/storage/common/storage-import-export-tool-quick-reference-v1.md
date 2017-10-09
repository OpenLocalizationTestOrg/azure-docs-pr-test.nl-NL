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
ms.openlocfilehash: 945eb4f9eff28c92ec963585d27cba73a7eb59bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="2872e-104">Snelzoekgids voor veelgebruikte opdrachten voor importtaken</span><span class="sxs-lookup"><span data-stu-id="2872e-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="2872e-105">Deze sectie bevat dat naslaginformatie over een aantal veelgebruikte opdrachten.</span><span class="sxs-lookup"><span data-stu-id="2872e-105">This section provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="2872e-106">Zie voor gedetailleerde informatie over het gebruik, [harde schijven voorbereiden voor een Import-taak](../storage-import-export-tool-preparing-hard-drives-import-v1.md).</span><span class="sxs-lookup"><span data-stu-id="2872e-106">For detailed usage, see [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-a-hard-drive-when-data-has-already-been-copied-toohello-hard-drive"></a><span data-ttu-id="2872e-107">Bereid een harde schijf wanneer gegevens al is gekopieerd toohello harde schijf</span><span class="sxs-lookup"><span data-stu-id="2872e-107">Prepare a hard drive when data has already been copied toohello hard drive</span></span>
 <span data-ttu-id="2872e-108">Hallo volgende opdracht wordt een harde schijf voorbereid wanneer gegevens is al gekopieerde tooit, maar nog niet is versleuteld met BitLocker:</span><span class="sxs-lookup"><span data-stu-id="2872e-108">hello following command prepares a hard drive when data has already been copied tooit, but has not yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a><span data-ttu-id="2872e-109">Een enkele directory tooa harde schijf kopiëren</span><span class="sxs-lookup"><span data-stu-id="2872e-109">Copy a single directory tooa hard drive</span></span>  
 <span data-ttu-id="2872e-110">Hallo volgende opdracht wordt een enkele bron directory tooa harde schijf die nog niet is versleuteld met BitLocker gekopieerd:</span><span class="sxs-lookup"><span data-stu-id="2872e-110">hello following command copies a single source directory tooa hard drive that has not yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-two-directories-tooa-hard-drive"></a><span data-ttu-id="2872e-111">Twee mappen tooa harde schijf kopiëren</span><span class="sxs-lookup"><span data-stu-id="2872e-111">Copy two directories tooa hard drive</span></span>  
 <span data-ttu-id="2872e-112">toocopy twee bron mappen tooa station, gebruik Hallo volgende opdrachten:</span><span class="sxs-lookup"><span data-stu-id="2872e-112">toocopy two source directories tooa drive, use hello following commands:</span></span>  
  
 <span data-ttu-id="2872e-113">Hallo eerste opdracht geeft u de logboekmap hello, opslagaccountsleutel, doel stationsletter, `format/encrypt` vereisten en de algemene parameters:</span><span class="sxs-lookup"><span data-stu-id="2872e-113">hello first command specifies hello log directory, storage account key, target drive letter, `format/encrypt` requirements, and common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="2872e-114">de tweede opdracht Hallo geeft Hallo journal-bestand, een nieuwe sessie-ID en de bron- en doellocaties Hallo:</span><span class="sxs-lookup"><span data-stu-id="2872e-114">hello second command specifies hello journal file, a new session ID, and hello source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="2872e-115">Kopieer een groot bestand tooa harde schijf in een tweede kopieersessie</span><span class="sxs-lookup"><span data-stu-id="2872e-115">Copy a large file tooa hard drive in a second copy session</span></span>  
 <span data-ttu-id="2872e-116">Hallo volgende opdracht wordt een enkele grote bestanden tooa harde schijf die in een eerdere sessie. exemplaar is voorbereid gekopieerd:</span><span class="sxs-lookup"><span data-stu-id="2872e-116">hello following command copies a single large file tooa hard drive that was prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="2872e-117">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="2872e-117">Next steps</span></span>

* [<span data-ttu-id="2872e-118">Voorbeeld werkstroom tooprepare harde schijven voor een import-taak</span><span class="sxs-lookup"><span data-stu-id="2872e-118">Sample workflow tooprepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
