---
title: aaa "Azure Batch-pool vergroten of verkleinen van de gebeurtenis | Microsoft Docs'
description: Naslaginformatie voor Batch-pool vergroten of verkleinen van de gebeurtenis.
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
ms.openlocfilehash: dc64711a01aa4cf6192edba1a2c4cad56f953766
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-complete-event"></a>Gebeurtenis resize van toepassingen

 Deze gebeurtenis wordt verzonden wanneer het formaat van een groep van toepassingen is voltooid of mislukt.

 Hallo ziet volgende voorbeeld Hallo hoofdtekst van de groep complete gebeurtenis resize voor een groep die vergroot en is voltooid.

```
{
    "id": "p_1_0_01503750-252d-4e57-bd96-d6aa05601ad8",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 4,
    "targetDedicated": 4,
    "enableAutoScale": false,
    "isAutoPool": false,
    "startTime": "2016-09-09T22:13:06.573Z",
    "endTime": "2016-09-09T22:14:01.727Z",
    "result": "Success",
    "resizeError": "hello operation succeeded"
}
```

|Element|Type|Opmerkingen|
|-------------|----------|-----------|
|id|Tekenreeks|Hallo-id van Hallo pool.|
|nodeDeallocationOption|Tekenreeks|Geeft aan wanneer knooppunten kunnen worden verwijderd uit groep hello, als Hallo poolgrootte afneemt.<br /><br /> Mogelijke waarden zijn:<br /><br /> **requeue** : Beëindig actieve taken en requeue ze. Hallo taken wordt opnieuw uitgevoerd wanneer de taak Hallo is ingeschakeld. Knooppunten verwijderen zodra taken zijn beëindigd.<br /><br /> **beëindigen** – actieve taken beëindigen. Hallo-taken worden niet opnieuw uitgevoerd. Knooppunten verwijderen zodra taken zijn beëindigd.<br /><br /> **taskcompletion** : toestaan dat taken toocomplete momenteel wordt uitgevoerd. Er zijn geen nieuwe taken tijdens het wachten plannen. Verwijder de knooppunten wanneer alle taken zijn voltooid.<br /><br /> **Retaineddata** - Sta toe dat actieve taken toocomplete en wacht vervolgens tot alle gegevens bewaren perioden tooexpire taken. Er zijn geen nieuwe taken tijdens het wachten plannen. Verwijder de knooppunten wanneer alle bewaarperioden voor taken zijn verlopen.<br /><br /> de standaardwaarde Hallo is requeue.<br /><br /> Als de poolgrootte Hallo toeneemt wordt Hallo waarde te ingesteld**ongeldig**.|
|currentDedicated|Int32|het aantal rekenknooppunten Hallo momenteel toohello groep toegewezen.|
|targetDedicated|Int32|Hallo aantal rekenknooppunten die zijn aangevraagd voor Hallo van toepassingen.|
|enableAutoScale|BOOL|Hiermee geeft u op of Hallo groepsgrootte automatisch wordt aangepast gedurende een bepaalde periode.|
|isAutoPool|BOOL|Hiermee geeft u op of Hallo van toepassingen via een taak AutoPool mechanisme is gemaakt.|
|startTime|Datum/tijd|Hallo tijd Hallo toepassingen vergroten of verkleinen gestart.|
|endTime|Datum/tijd|Hallo tijd Hallo toepassingen vergroten of verkleinen is voltooid.|
|resultCode|Tekenreeks|Hallo resultaat Hallo vergroten of verkleinen.|
|resultMessage|Tekenreeks|Hallo formaat fout bevat Hallo details van resultaat Hallo.<br /><br /> Als Hallo vergroten of verkleinen voltooid deze statussen die Hallo van de bewerking is voltooid.|
