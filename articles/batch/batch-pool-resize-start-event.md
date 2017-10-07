---
title: aaa "Azure Batch pool formaat start gebeurtenis | Microsoft Docs'
description: Verwijzing voor Batch-pool formaat start-gebeurtenis.
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
ms.openlocfilehash: 2ca2a4f1195c3f785ae5b051b63340f70eecbc22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-start-event"></a>Gebeurtenissen voor het starten van toepassingen formaat wijzigen

 Deze gebeurtenis wordt verzonden wanneer het formaat van een groep van toepassingen is gestart. Aangezien Hallo groep formaat een asynchrone gebeurtenis is, kunt u verwachten een pool formaat gebeurtenis toobe verzonden zodra Hallo vergroten of verkleinen van de bewerking is voltooid.

 Hallo volgende voorbeeld toont de hoofdtekst van de groep van toepassingen startgebeurtenis resize voor een groep van toepassingen vergroten of verkleinen van 0 too2 knooppunten met een handmatige Hallo vergroten of verkleinen.

```
{
    "poolId": "myPool1",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 0,
    "targetDedicated": 2,
    "enableAutoScale": false,
    "isAutoPool": false
}
```

|Element|Type|Opmerkingen|
|-------------|----------|-----------|
|poolId|Tekenreeks|Hallo-id van Hallo pool.|
|nodeDeallocationOption|Tekenreeks|Geeft aan wanneer knooppunten kunnen worden verwijderd uit groep hello, als Hallo poolgrootte afneemt.<br /><br /> Mogelijke waarden zijn:<br /><br /> **requeue** : Beëindig actieve taken en requeue ze. Hallo taken wordt opnieuw uitgevoerd wanneer de taak Hallo is ingeschakeld. Knooppunten verwijderen zodra taken zijn beëindigd.<br /><br /> **beëindigen** – actieve taken beëindigen. Hallo-taken worden niet opnieuw uitgevoerd. Knooppunten verwijderen zodra taken zijn beëindigd.<br /><br /> **taskcompletion** : toestaan dat taken toocomplete momenteel wordt uitgevoerd. Er zijn geen nieuwe taken tijdens het wachten plannen. Verwijder de knooppunten wanneer alle taken zijn voltooid.<br /><br /> **Retaineddata** - Sta toe dat actieve taken toocomplete en wacht vervolgens tot alle gegevens bewaren perioden tooexpire taken. Er zijn geen nieuwe taken tijdens het wachten plannen. Verwijder de knooppunten wanneer alle bewaarperioden voor taken zijn verlopen.<br /><br /> de standaardwaarde Hallo is requeue.<br /><br /> Als de poolgrootte Hallo toeneemt wordt Hallo waarde te ingesteld**ongeldig**.|
|currentDedicated|Int32|het aantal rekenknooppunten Hallo momenteel toohello groep toegewezen.|
|targetDedicated|Int32|Hallo aantal rekenknooppunten die zijn aangevraagd voor Hallo van toepassingen.|
|enableAutoScale|BOOL|Hiermee geeft u op of Hallo groepsgrootte automatisch wordt aangepast gedurende een bepaalde periode.|
|isAutoPool|BOOL|Speficies of Hallo van toepassingen via een taak AutoPool mechanisme is gemaakt.|
