---
title: aaaAzure CDN regels engine-verwijzing | Microsoft Docs
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
ms.openlocfilehash: 4159715d15fc792afb49dcd2a30752fabcd94a38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cdn-rules-engine"></a>Azure CDN regels-engine
Dit onderwerp vindt u gedetailleerde beschrijvingen van functies en Hallo beschikbaar overeenkomst voorwaarden voor Azure Content Delivery Network (CDN) [regelengine](cdn-rules-engine.md).

Hallo HTTP regels-Engine is ontworpen toobe Hallo laatste instantie op hoe specifieke typen aanvragen worden verwerkt door Hallo CDN.

**Veelvoorkomende toepassingen**:

- Overschrijven of een aangepaste cachebeleid definiëren.
- Secure of weigeren van aanvragen voor gevoelige inhoud.
- Aanvragen omleiden.
- Aangepaste logboekgegevens opslaan.

## <a name="terminology"></a>Terminologie
Een regel wordt gedefinieerd door het gebruik van Hallo [ **voorwaardelijke expressies**](cdn-rules-engine-reference-conditional-expressions.md), [ **overeenkomt met**](cdn-rules-engine-reference-match-conditions.md), en [  **functies**](cdn-rules-engine-reference-features.md). Deze elementen zijn gemarkeerd in de volgende illustratie Hallo.

 ![CDN overeen voorwaarde](./media/cdn-rules-engine-reference/cdn-rules-engine-terminology.png)

## <a name="syntax"></a>Syntaxis

Hallo manier waarin de speciale tekens worden behandeld varieert volgens toohow een voorwaarde overeenkomst of functie ingangen tekstwaarden. Een overeenkomst voorwaarde of onderdeel kan tekst in een van de volgende manieren Hallo interpreteren:

1. [**Letterlijke waarden**](#literal-values) 
2. [**Jokertekens waarden**](#wildcard-values)
3. [**Reguliere expressies**](#regular-expressions)

### <a name="literal-values"></a>Letterlijke waarden
Tekst die wordt geïnterpreteerd als een letterlijke waarde zal alle speciale tekens, met uitzondering van Hallo % symbool Hallo worden beschouwd als onderdeel van het Hallo-waarde die moet overeenkomen. Met andere woorden, een letterlijke waarde overeenkomen met de voorwaarde is ingesteld te`\'*'\` alleen worden verwerkt wanneer die waarde exacte (dat wil zeggen, `\'*'\`) is gevonden.
 
Een percentagesymbool is gebruikte tooindicate URL-codering (bijv, `%20`).

### <a name="wildcard-values"></a>Jokertekens waarden
Tekst die wordt geïnterpreteerd als een jokerteken wordt extra betekenis toospecial tekens toewijzen. Hallo volgende tabel wordt beschreven hoe Hallo na tekens worden geïnterpreteerd.

Teken | Beschrijving
----------|------------
\ | Een backslash is gebruikte tooescape Hallo tekens in deze tabel opgegeven. Een backslash moet direct vóór Hallo speciale teken dat moet worden voorafgegaan worden opgegeven.<br/>Hallo syntaxis verlaat u bijvoorbeeld een sterretje:`\*`
% | Een percentagesymbool is gebruikte tooindicate URL-codering (bijv, `%20`).
* | Een sterretje is een jokerteken dat een of meer tekens vertegenwoordigt.
Ruimte | Een spatie geeft aan dat een overeenkomst voorwaarde kan worden voldaan door een van de opgegeven Hallo waarden of patronen.
'value' | Een enkel aanhalingsteken heeft geen speciale betekenis. Een set met enkele aanhalingstekens wordt echter gebruikt tooindicate die een waarde moet worden behandeld als een letterlijke waarde. Worden kan gebruikt in de volgende manieren Hallo:<br><br/>-Kunt u een overeenkomst voorwaarde toobe wanneer Hallo waarde komt overeen met een gedeelte van de vergelijkingswaarde Hallo opgegeven voldaan.  Bijvoorbeeld: `'ma'` zou overeen met een Hallo tekenreeksen te volgen: <br/><br/>/Business/**ma**rathon/asset.htm<br/>**ma**p.gif<br/>zakelijke/sjabloon. **ma**p<br /><br />-Kunt u een speciaal teken toobe opgegeven als een letterlijke waarde. U kunt bijvoorbeeld een letterlijke spatie opgeven door een spatie binnen een set met enkele aanhalingstekens (dat wil zeggen, `' '` of `'sample value'`).<br/>-Kunt u een lege waarde toobe opgegeven. Geef een lege waarde door te geven van een set met enkele aanhalingstekens (dat wil zeggen, '').<br /><br/>**Belangrijk:**<br/>-Als Hallo waarde bevat geen jokerteken opgegeven, vervolgens automatisch beschouwd als een letterlijke waarde. Dit betekent dat het is niet nodig toospecify een reeks tussen enkele aanhalingstekens.<br/>-Als een backslash geen een andere in deze tabel escapeteken biedt, worden vervolgens genegeerd wanneer opgegeven binnen een set met enkele aanhalingstekens.<br/>-Een andere manier toospecify speciaal teken als een letterlijke waarde is tooescape met behulp van een backslash (dat wil zeggen, `\`).

### <a name="regular-expressions"></a>Reguliere expressies

Reguliere expressies definieert een patroon dat moet worden gezocht binnen een tekstwaarde. Notatie van reguliere expressie definieert specifieke betekenis tooa diverse symbolen. Hallo volgende tabel geeft aan hoe speciale tekens worden behandeld door overeenkomst voorwaarden en functies die ondersteuning bieden voor reguliere expressies.

Speciaal teken | Beschrijving
------------------|------------
\ | Een backslash Hiermee heft Hallo teken Hallo volgt erop. Dit zorgt ervoor dat deze teken toobe behandeld als een letterlijke waarde in plaats van nemen over de betekenis van de reguliere expressie. Hallo syntaxis verlaat u bijvoorbeeld een sterretje:`\*`
% | Hallo betekenis van een percentagesymbool, is afhankelijk van het gebruik ervan.<br/><br/> `%{HTTPVariable}`: Deze syntaxis identificeert een HTTP-variabele.<br/>`%{HTTPVariable%Pattern}`: Deze syntaxis gebruikt een percentage symbool tooidentify een HTTP-variabele en als scheidingsteken.<br />`\%`: Een percentagesymbool aanhalingstekens toestaat dat deze toobe gebruikt als een letterlijke waarde of tooindicate URL-codering (bijv, `\%20`).
* | Een sterretje kunt Hallo voorgaande teken toobe komt overeen met nul of meer keer. 
Ruimte | Een spatie wordt meestal beschouwd als een letterlijke waarde. 
'value' | Enkele aanhalingstekens worden behandeld als letterlijke tekens. Een set met enkele aanhalingstekens heeft geen speciale betekenis.


## <a name="next-steps"></a>Volgende stappen
* [De overeenkomst motor regels](cdn-rules-engine-reference-match-conditions.md)
* [Regels Engine voorwaardelijke expressies](cdn-rules-engine-reference-conditional-expressions.md)
* [Regels Engine functies](cdn-rules-engine-reference-features.md)
* [Standaardgedrag HTTP met Hallo regelengine](cdn-rules-engine.md)
* [Overzicht van Azure CDN](cdn-overview.md)
