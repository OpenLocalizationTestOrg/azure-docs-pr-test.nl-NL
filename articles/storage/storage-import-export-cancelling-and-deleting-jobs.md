---
title: Annuleren en een Azure Import/Export-taak verwijderen | Microsoft Docs
description: Informatie over het annuleren en taken voor de Microsoft Azure Import/Export-service verwijderen.
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
ms.openlocfilehash: e0a7ff391e5a03ed563912dea54c7cfe73111bcf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a>Annuleren en het verwijderen van de Azure Import/Export-taken

U kunt aanvragen dat een taak geannuleerd voordat deze wordt de `Packaging` status door het aanroepen van de [taakeigenschappen bijwerken](/rest/api/storageimportexport/jobs#Jobs_Update) bewerking en instelling van de `CancelRequested` element op de `true`. De taak worden op basis van best-effort geannuleerd. Als er stations zijn bezig het overbrengen van gegevens, blijven gegevens worden overgebracht, zelfs nadat de annulering is aangevraagd.

 Een geannuleerde taak wordt verplaatst naar de `Completed` status en worden bewaard gedurende 90 dagen op dat moment worden verwijderd.

 Aanroepen voor het verwijderen van een taak, de [taak verwijderen](/rest/api/storageimportexport/jobs#Jobs_Delete) bewerking voordat de taak is verzonden (*dat wil zeggen*, terwijl de taak de `Creating` staat). U kunt ook een taak verwijderen wanneer deze zich in de `Completed` staat. Nadat een taak is verwijderd, de informatie en de status niet langer zijn toegankelijk via de REST-API of de Azure-portal.

## <a name="next-steps"></a>Volgende stappen

* [Met behulp van de Import/Export-service REST-API](storage-import-export-using-the-rest-api.md)
