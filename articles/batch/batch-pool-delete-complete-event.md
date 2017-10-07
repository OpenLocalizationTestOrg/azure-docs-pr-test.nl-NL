---
title: aaa "Azure Batch-pool verwijderen gebeurtenis | Microsoft Docs'
description: Naslaginformatie voor Batch-pool gebeurtenis verwijderen.
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 494c371e48ebfb1bf3d2973a7401829a939ba141
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-complete-event"></a>Gebeurtenis groep verwijderen

 Deze gebeurtenis wordt verzonden wanneer een groep delete-bewerking is voltooid.

 Hallo ziet volgende voorbeeld Hallo hoofdtekst van een groep verwijderingsgebeurtenis.

```
{
    "id": "myPool1",
    "startTime": "2016-09-09T22:13:48.579Z",
    "endTime": "2016-09-09T22:14:08.836Z"
}
```

|Element|Type|Opmerkingen|
|-------------|----------|-----------|
|id|Tekenreeks|Hallo-id van Hallo pool.|
|startTime|Datum/tijd|Hallo tijd Hallo-groep verwijderen is gestart.|
|endTime|Datum/tijd|Hallo tijd Hallo-groep verwijderen is voltooid.|

## <a name="remarks"></a>Opmerkingen
Zie voor meer informatie over statussen en foutcodes voor de bewerking formaat wijzigen van toepassingen [een adresgroep verwijderen van een account](https://docs.microsoft.com/rest/api/batchservice/delete-a-pool-from-an-account).