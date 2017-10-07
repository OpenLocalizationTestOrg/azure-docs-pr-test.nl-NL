---
title: aaa "Azure Batch pool verwijderen start-gebeurtenis | Microsoft Docs'
description: Verwijzing voor Batch-pool verwijderen start-gebeurtenis.
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
ms.openlocfilehash: 79bb28bffc760a49cc0a95062f5086dc96c6a795
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-start-event"></a>Gebeurtenissen voor het starten van toepassingen verwijderen

 Deze gebeurtenis wordt verzonden wanneer een groep delete-bewerking is gestart. Aangezien Hallo groep verwijderen een asynchrone gebeurtenis is, kunt u verwachten een groep verwijderen gebeurtenis toobe verzonden zodra Hallo bewerking verwijderen is voltooid.

 Hallo ziet volgende voorbeeld Hallo hoofdtekst van een groep verwijderen start-gebeurtenis.

```
{
    "id": "myPool1"
}
```

|Element|Type|Opmerkingen|
|-------------|----------|-----------|
|id|Tekenreeks|Hallo-id van Hallo pool.|
