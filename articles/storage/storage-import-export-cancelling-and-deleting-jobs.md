---
title: aaaCancel en verwijderen van een Azure Import/Export-taak | Microsoft Docs
description: Meer informatie over hoe toocancel en delete taken voor Hallo Microsoft Azure Import/Export-service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: fd3d66f0-1dbb-4c75-9223-307d5abaeefc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 5d2aba510dafd0ca9a10f5643f721e7059a6a8f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a>Annuleren en het verwijderen van de Azure Import/Export-taken

U kunt aanvragen dat een taak geannuleerd voordat deze in Hallo `Packaging` status door de aanroepende Hallo [Update taakeigenschappen](/rest/api/storageimportexport/jobs#Jobs_Update) bewerking en instelling Hallo `CancelRequested` element te`true`. Hallo-taak worden op basis van best-effort geannuleerd. Als er stations aanwezig zijn in het Hallo-proces voor het overbrengen van gegevens, blijft gegevens toobe overgedragen zelfs nadat de annulering is aangevraagd.

 Een geannuleerde taak gaat toohello `Completed` status en worden bewaard gedurende 90 dagen op dat moment worden verwijderd.

 toodelete een taak aanroep Hallo [taak verwijderen](/rest/api/storageimportexport/jobs#Jobs_Delete) bewerking voordat het Hallo-taak is verzonden (*dat wil zeggen*, terwijl het Hallo-taak wordt Hallo `Creating` staat). U kunt ook een taak verwijderen wanneer deze Hallo `Completed` status. Nadat een taak is verwijderd, worden de gegevens en de status niet langer zijn toegankelijk via Hallo REST-API of hello Azure-portal.

## <a name="next-steps"></a>Volgende stappen

* [Met behulp van REST-API voor Hallo Import/Export-service](storage-import-export-using-the-rest-api.md)
