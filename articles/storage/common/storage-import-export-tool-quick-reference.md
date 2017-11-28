---
title: verwijzing voor Azure-hulpprogramma voor importeren/exporteren import-taak opdrachten aaaQuick | Microsoft Docs
description: Hulpprogramma voor importeren/exporteren opdracht naslaginformatie over Azure voor opdrachten van veelgebruikte import-taak.
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
ms.openlocfilehash: 35e46f24f764a5098ca465adb51badcab2d13e9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="d6301-103">Snelzoekgids voor veelgebruikte opdrachten voor importtaken</span><span class="sxs-lookup"><span data-stu-id="d6301-103">Quick reference for frequently used commands for import jobs</span></span>

<span data-ttu-id="d6301-104">Dit artikel bevat dat naslaginformatie over een aantal veelgebruikte opdrachten.</span><span class="sxs-lookup"><span data-stu-id="d6301-104">This article provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="d6301-105">Zie voor gedetailleerde informatie over het gebruik, [harde schijven voorbereiden voor een Import-taak](../storage-import-export-tool-preparing-hard-drives-import.md).</span><span class="sxs-lookup"><span data-stu-id="d6301-105">For detailed usage, see [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import.md).</span></span>

## <a name="first-session"></a><span data-ttu-id="d6301-106">Eerste sessie</span><span class="sxs-lookup"><span data-stu-id="d6301-106">First session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1 /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

## <a name="second-session"></a><span data-ttu-id="d6301-107">Tweede sessie</span><span class="sxs-lookup"><span data-stu-id="d6301-107">Second session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /DataSet:dataset-2.csv
```

## <a name="abort-latest-session"></a><span data-ttu-id="d6301-108">Meest recente sessie afbreken</span><span class="sxs-lookup"><span data-stu-id="d6301-108">Abort latest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /AbortSession
```

## <a name="resume-latest-interrupted-session"></a><span data-ttu-id="d6301-109">Meest recente onderbroken sessie hervatten</span><span class="sxs-lookup"><span data-stu-id="d6301-109">Resume latest interrupted session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /ResumeSession
```

## <a name="add-drives-toolatest-session"></a><span data-ttu-id="d6301-110">Stations toolatest sessie toevoegen</span><span class="sxs-lookup"><span data-stu-id="d6301-110">Add drives toolatest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /AdditionalDriveSet:driveset-2.csv
```

## <a name="next-steps"></a><span data-ttu-id="d6301-111">Volgende stappen</span><span class="sxs-lookup"><span data-stu-id="d6301-111">Next steps</span></span>

* [<span data-ttu-id="d6301-112">Voorbeeld werkstroom tooprepare harde schijven voor een import-taak</span><span class="sxs-lookup"><span data-stu-id="d6301-112">Sample workflow tooprepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
