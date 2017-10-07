---
title: aaaReviewing taakstatus Azure Import/Export - v1 | Microsoft Docs
description: Meer informatie over hoe toouse Hallo logboekbestanden wanneer Hallo importeren of exporteren van de taak toosee Hallo status van Hallo Import/Export-taak werd uitgevoerd.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: c69d1d69-6403-4eee-9949-0185faeecfa1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: muralikk
ms.openlocfilehash: 363731ede4751124a714b4ce96852e0b8c4dbca4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a>De status van de Azure Import/Export-taak controleren met logboekbestanden kopiëren
Wanneer Hallo Microsoft Azure Import/Export-service stations die zijn gekoppeld aan een taak importeren of exporteren verwerkt, schrijft deze kopie logboek bestanden toohello storage account tooor van waaruit u importeert of exporteert blobs. Hallo-logboekbestand bevat gedetailleerde status van elk bestand dat is geïmporteerd of geëxporteerd. Hallo URL tooeach kopie-logboekbestand wordt geretourneerd wanneer u een query uitvoeren op Hallo status van een voltooide taak; Zie [Get Job](/rest/api/storageservices/Get-Job3) voor meer informatie.  

## <a name="example-urls"></a>Voorbeeld-URL 's

Hallo hieronder vindt u voorbeeld-URL's voor kopiëren-logboekbestanden voor een import-taak met twee schijven:  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 Zie [Import/Export-service indeling van logboekbestand](../storage-import-export-file-format-log.md) voor Hallo-indeling van Logboeken voor kopiëren en Hallo volledige lijst met statuscodes.  
  
## <a name="next-steps"></a>Volgende stappen
 
 * [Hallo-instelling van Azure-hulpprogramma voor importeren/exporteren](storage-import-export-tool-setup-v1.md)   
 * [Harde schijven voorbereiden voor een importtaak](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [Een importtaak herstellen](../storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [Een exporttaak herstellen](../storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [Het oplossen van problemen hello Azure-hulpprogramma voor importeren/exporteren](storage-import-export-tool-troubleshooting-v1.md)
