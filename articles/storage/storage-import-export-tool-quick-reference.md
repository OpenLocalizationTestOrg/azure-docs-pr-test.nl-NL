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
ms.openlocfilehash: 0a615aed938e5e1b52d55a340aa6b48fa0744367
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a>Snelzoekgids voor veelgebruikte opdrachten voor importtaken

Dit artikel bevat dat naslaginformatie over een aantal veelgebruikte opdrachten. Zie voor gedetailleerde informatie over het gebruik, [harde schijven voorbereiden voor een Import-taak](storage-import-export-tool-preparing-hard-drives-import.md).

## <a name="first-session"></a>Eerste sessie

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1 /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

## <a name="second-session"></a>Tweede sessie

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /DataSet:dataset-2.csv
```

## <a name="abort-latest-session"></a>Meest recente sessie afbreken

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /AbortSession
```

## <a name="resume-latest-interrupted-session"></a>Meest recente onderbroken sessie hervatten

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /ResumeSession
```

## <a name="add-drives-toolatest-session"></a>Stations toolatest sessie toevoegen

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /AdditionalDriveSet:driveset-2.csv
```

## <a name="next-steps"></a>Volgende stappen

* [Voorbeeld werkstroom tooprepare harde schijven voor een import-taak](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
