---
ms.assetid: 
title: aaaAzure Sleutelkluis bandbreedteregeling richtlijnen | Microsoft Docs
ms.service: key-vault
author: BrucePerlerMS
ms.author: bruceper
manager: mbaldwin
ms.date: 06/21/2017
ms.openlocfilehash: a75cf96bc6503e51f14378bee598bad57e85be82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-throttling-guidance"></a>Azure Sleutelkluis richtlijnen beperking

Beperking is een proces dat u starten dat het aantal gelijktijdige aanroepen toohello Azure service tooprevent overmatig gebruik van bronnen Hallo beperkt. Azure-kluis (Azure sleutel Sleutelkluis) is ontworpen toohandle een groot aantal aanvragen. Als er een groot aantal aanvragen optreedt, kunt beperking van de client aanvragen onderhouden voor optimale prestaties en betrouwbaarheid van hello Azure Sleutelkluis-service.

Limieten voor bandbreedteregeling variëren, afhankelijk van het Hallo-scenario. Bijvoorbeeld, als u een groot aantal schrijfbewerkingen uitvoert, is Hallo mogelijkheid voor beperking hoger dan als u alleen leesbewerkingen uitvoert.

## <a name="how-does-key-vault-handle-its-limits"></a>Hoe wordt de grenzen in Sleutelkluis verwerkt?

Servicelimieten in Sleutelkluis zijn er tooprevent misbruik van resources en controleer quality of service voor alle clients van de Sleutelkluis. Wanneer een service-drempelwaarde wordt overschreden, beperkt Sleutelkluis alle verdere aanvragen van die client voor een bepaalde periode. Als dit gebeurt, Sleutelkluis retourneert HTTP-statuscode 429 (te veel aanvragen), en het Hallo-aanvragen mislukken. Ook mislukte aanvragen die 429 geteld naar Hallo versnelling limieten bijgehouden door de Sleutelkluis. 

Als u een geldige business case voor hogere versnelling limieten hebt, neem dan contact met ons.


## <a name="how-toothrottle-your-app-in-response-tooservice-limits"></a>Hoe toothrottle uw app in het antwoord tooservice beperkt

Hallo volgen **aanbevolen procedures** voor beperking van uw app:
- Verminder het aantal bewerkingen per aanvraag Hallo.
- Verlaag de frequentie Hallo van aanvragen.
- Vermijd directe nieuwe pogingen. 
    - Alle aanvragen samenvoegen op basis van uw gebruikslimieten.

Wanneer u uw app foutafhandeling implementeert, moet gebruik Hallo HTTP fout code 429 toodetect Hallo voor client-side '-beperking. Als Hallo aanvraag opnieuw met een 429 HTTP-foutcode mislukt, doe u nog steeds een limiet voor de Azure-service. Blijven toouse Hallo aanbevolen clientzijde bandbreedteregeling methode, Hallo aanvraag opnieuw proberen totdat dit is gelukt.

### <a name="recommended-client-side-throttling-method"></a>Aanbevolen bandbreedteregeling client-side '-methode

In de HTTP-foutcode 429 beginnen met beperking van de client met een benadering exponentieel uitstel:

1. Wacht 1 seconde, de aanvraag opnieuw proberen
2. Als u nog steeds beperkt 2 seconden wachten, aanvraag opnieuw proberen
3. Als u nog steeds beperkt wacht 4 seconden, aanvraag opnieuw proberen
4. Als u nog steeds beperkt 8 seconden wachten, aanvraag opnieuw proberen
5. Als u nog steeds beperkt 16 seconden wachten, aanvraag opnieuw proberen

Op dit moment moet u niet worden opgehaald HTTP 429 responscodes.

## <a name="see-also"></a>Zie ook

Zie voor een beter afdrukstand van de beperking op Hallo Microsoft Cloud [patroon beperking](https://docs.microsoft.com/azure/architecture/patterns/throttling).

