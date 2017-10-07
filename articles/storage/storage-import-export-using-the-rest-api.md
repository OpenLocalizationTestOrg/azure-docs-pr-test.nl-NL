---
title: aaaUsing hello Azure Import/Export-service REST-API | Microsoft Docs
description: Meer informatie over waar toofind resources voor het gebruik van hello Azure Import/Export REST API, met inbegrip van beide referentiemateriaal hoe tooand service.
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 233f80e9-2e7f-48e0-9639-5c7785e7d743
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: a01c170b1bc9c2b2ce9086d39de78a39fafb2c8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-importexport-service-rest-api"></a>Met behulp van hello Azure Import/Export-service REST-API

Hallo Microsoft Azure Import/Export-service wordt een REST-API tooenable programmatisch beheer van importeren/exporteren-taken. U kunt Hallo REST-API tooperform alle Hallo voor importeren/exporteren bewerkingen die u met Hallo uitvoeren kunt [Azure-portal](https://portal.azure.com/). Bovendien kunt u Hallo REST-API tooperform bepaalde gedetailleerde bewerkingen, zoals het uitvoeren van query's Hallo percentage voltooiing van een taak die momenteel niet beschikbaar in de klassieke portal Hallo zijn.

Zie [Hallo Microsoft Azure Import/Export-service tooTransfer gegevens tooBlob opslag met](storage-import-export-service.md) voor een overzicht van Hallo Import/Export-service en een zelfstudie wordt gedemonstreerd hoe toouse Hallo klassieke portal toocreate en importeren beheren en exporteren van taken.

## <a name="service-endpoints"></a>Service-eindpunten

Hello Azure Import/Export-service is een resourceprovider voor Azure Resource Manager en biedt een set REST-API's op Hallo HTTPS-eindpunt voor het beheren van importeren/exporteren taken te volgen:

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a>Versiebeheer voor onderdelen

Aanvragen toohello Import/Export-service moet opgeven Hallo `api-version` parameter en stel de waarde te`2016-11-01`.

## <a name="importexport-service-operations"></a>Servicebewerkingen voor importeren/exporteren

[Een importtaak maken](storage-import-export-creating-an-import-job.md)

[Een exporttaak maken](storage-import-export-creating-an-export-job.md)

[Statusinformatie van een taak ophalen](storage-import-export-retrieving-state-info-for-a-job.md)

[Taken opsommen](storage-import-export-enumerating-jobs.md)

[Taken annuleren en verwijderen](storage-import-export-cancelling-and-deleting-jobs.md)

[Een back-Up station manifesten](storage-import-export-backing-up-drive-manifests.md)

[Diagnoses en het herstel van fouten voor Import/Export-taken](storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a>Volgende stappen

* [Opslag voor importeren/exporteren REST](/rest/api/storageimportexport)
