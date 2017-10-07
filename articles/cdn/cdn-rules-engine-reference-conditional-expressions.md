---
title: aaaAzure CDN regels engine voorwaardelijke expressies | Microsoft Docs
description: Documentatie bij Azure CDN regels overeen motor en onderdelen.
services: cdn
documentationcenter: 
author: Lichard
manager: akucer
editor: 
ms.assetid: 669ef140-a6dd-4b62-9b9d-3f375a14215e
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 39d0754c34a577f77ca87b6fd92e2b6a9e4ff8fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine-conditional-expressions"></a>Voorwaardelijke expressies in de engine Azure CDN-regels
Dit onderwerp vindt u gedetailleerde beschrijvingen van Hallo voorwaardelijke expressies voor Azure Content Delivery Network (CDN) [regelengine](cdn-rules-engine.md).

Hallo eerste deel van een regel is Hallo voorwaardelijke expressies.

Voorwaardelijke expressies | Beschrijving
-----------------------|-------------
ALS | Een expressie als is altijd een deel van de eerste instructie Hallo in een regel. Net als alle andere voorwaardelijke expressies, moet deze instructie worden gekoppeld aan een overeenkomst. Als er geen aanvullende voorwaardelijke expressies zijn opgegeven, bepaalt deze treffer Hallo criterium dat moet worden voldaan voordat een verzameling functies is mogelijk toegepaste tooa aanvraag.
EN ALS | Een expressie en als kan alleen worden toegevoegd na het Hallo typen voorwaardelijke expressies: als, en als volgt. Dit geeft aan dat er nog een voorwaarde die moet worden voldaan om Hallo initiële IF-instructie.
ANDERS ALS| Een expressie ELSE IF Hiermee geeft u een alternatieve voorwaarde die moet worden voldaan voordat een reeks functies specifieke toothis ELSE IF-instructie plaatsvindt. Hallo aanwezigheid van een ELSE IF-instructie geeft Hallo einde van de vorige instructie Hallo. Hallo alleen voorwaardelijke expressies die kan worden geplaatst nadat een ELSE IF-instructie een andere ELSE IF-instructie is. Dit betekent dat een ELSE IF-instructie gebruikte toospecify enige aanvullende voorwaarde is voldaan toobe is alleen mogelijk.

**Voorbeeld**: ![CDN overeenkomen met de voorwaarde](./media/cdn-rules-engine-reference/cdn-rules-engine-conditional-expression.png)

 > [!TIP]
   > Een volgende regel mogen Hallo handelingen die zijn opgegeven door een vorige regel overschrijven. Voorbeeld: Een regel catch all-beveiligt alle aanvragen via verificatie op basis van tokens. Een andere regel kan worden gemaakt onder het toomake een uitzondering voor bepaalde typen aanvragen.

### <a name="next-steps"></a>Volgende stappen
* [Overzicht van Azure CDN](cdn-overview.md)
* [Regels Engine verwijzing](cdn-rules-engine-reference.md)
* [De overeenkomst motor regels](cdn-rules-engine-reference-match-conditions.md)
* [Regels Engine functies](cdn-rules-engine-reference-features.md)
* [Standaardgedrag HTTP met Hallo regelengine](cdn-rules-engine.md)
