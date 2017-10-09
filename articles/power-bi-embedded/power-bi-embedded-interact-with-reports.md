---
title: aaaInteract met rapporten die met behulp van Hallo JavaScript-API | Microsoft Docs
description: Power BI Embedded, communiceren met de rapporten met behulp van Hallo JavaScript-API
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: bdd885d3-1b00-4dcf-bdff-531eb1f97bfb
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: 657e4d5cee031bdda173ab3f451cc19b93ddb17b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="interact-with-power-bi-reports-using-hello-javascript-api"></a>Interactie met Power BI-rapporten met Hallo JavaScript-API
Hallo Power BI JavaScript API waarmee inventarisaties tooeasily u Power BI-rapporten insluiten in uw toepassingen. Uw toepassingen kunnen programmatisch met Hallo API communiceren met andere rapportelementen zoals pagina's en filters. Door deze interactiviteit zijn Power BI-rapporten een meer geïntegreerd onderdeel van uw toepassing.

U kunt een Power BI-rapport insluiten in uw toepassing met behulp van een iframe die wordt gehost als onderdeel van de toepassing hello. Hallo iframe fungeert als een grens tussen de toepassing en het Hallo-rapport, zoals u ziet in Hallo installatiekopie te volgen. 

![Ingesloten Power BI-iframe zonder Javascript-API](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-1.png)

Hallo iframe Hallo insluiten van het proces is veel eenvoudiger maakt, maar zonder Hallo JavaScript API Hallo rapport en uw toepassing kunnen niet communiceren met elkaar. Dit gebrek aan interactie kunt u vindt dat Hallo rapport niet echt onderdeel van de toepassing hello is. Hallo-rapport en de toepassing echt nodig toocommunicate heen en weer in Hallo installatiekopie te volgen.

![Ingesloten Power BI-iframe met Javascript-API](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-2.png)

Hallo Power BI JavaScript-API kunt u toowrite-code die Hallo iframe grens veilig kunt doorgeven. Deze kan uw toepassing tooprogrammatically een actie uitvoert in een rapport en toolisten voor gebeurtenissen van acties die gebruikers in Hallo-rapport maken.

## <a name="what-can-you-do-with-hello-power-bi-javascript-api"></a>Wat kunt u doen met Hallo Power BI JavaScript-API
Hello JavaScript-API kunt u rapporten beheren, gaat u toopages in een rapport, een rapport filteren en insluiten gebeurtenissen verwerken. Hallo toont volgende diagram Hallo-structuur van Hallo API.

![Diagram van JavaScript-API van Power BI](media/powerbi-embedded-interact-with-reports/powerbi-embedded-interact-report-3.png)

### <a name="manage-reports"></a>Rapporten beheren
Hallo Javascript-API kunt u toomanage gedrag op Hallo rapport en pagina niveau:

* Een specifieke Power BI-rapport veilig insluiten in uw toepassing - Hallo probeer [voorbeeldtoepassing insluiten](http://azure-samples.github.io/powerbi-angular-client/#/scenario1)
  * Toegangstoken instellen
* Hallo rapport configureren
  * Inschakelen en uitschakelen Hallo filterdeelvenster en het navigatiedeelvenster van pagina - probeer het Hallo [instellingen demo toepassing bijwerken](http://azure-samples.github.io/powerbi-angular-client/#/scenario6)
  * Standaardopties voor pagina's en filters instellen - Hallo probeer [set standaardwaarden demo](http://azure-samples.github.io/powerbi-angular-client/#/scenario5)
* De schermvullende modus openen en sluiten

[Meer informatie over het insluiten van een rapport](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Embedding-Basics)

### <a name="navigate-toopages-in-a-report"></a>Navigeer toopages in een rapport
Hallo JavaScript API enbales u toodiscover alle pagina's in een rapport en tooset Hallo huidige pagina. Probeer Hallo [navigatie-voorbeeldtoepassing](http://azure-samples.github.io/powerbi-angular-client/#/scenario3).

[Meer informatie over paginanavigatie](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Page-Navigation)

### <a name="filter-a-report"></a>Een rapport filteren
Hallo JavaScript-API biedt basiseigenschappen en geavanceerde mogelijkheden voor ingesloten rapporten en rapportpagina's filteren. Probeer Hallo [filteren voorbeeldtoepassing](http://azure-samples.github.io/powerbi-angular-client/#/scenario4), en sommige inleidende code hier bekijken.  

#### <a name="basic-filters"></a>Basisfilters
Een basic-filter op een kolom of de hiërarchie een niveau wordt geplaatst en bevat een lijst met waarden tooinclude of uitsluiten.

```
const basicFilter: pbi.models.IBasicFilter = {
  $schema: "http://powerbi.com/product/schema#basic",
  target: {
    table: "Store",
    column: "Count"
  },
  operator: "In",
  values: [1,2,3,4]
}
```


#### <a name="advanced-filters"></a>Geavanceerde filters
Geavanceerde filters gebruiken Hallo logische operator en of OR en een of twee voorwaarden, elk met hun eigen operator en een waarde te accepteren. Ondersteunde voorwaarden zijn:

* None
* LessThan
* LessThanOrEqual
* GreaterThan
* GreaterThanOrEqual
* Contains
* DoesNotContain
* StartsWith
* DoesNotStartWith
* Is
* IsNot
* IsBlank
* IsNotBlank

```
const advancedFilter: pbi.models.IAdvancedFilter = {
  $schema: "http://powerbi.com/product/schema#advanced",
  target: {
    table: "Store",
    column: "Name"
  },
  logicalOperator: "Or",
  conditions: [
    {
      operator: "Contains",
      value: "Wash"
    },
    {
      operator: "Contains",
      value: "Park"
    }
  ]
}
```
[Meer informatie over filteren](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Filters)

### <a name="handling-events"></a>Gebeurtenissen verwerken
Bovendien toosending informatie naar Hallo iframe, uw toepassing kunt ook informatie ontvangen over Hallo gebeurtenissen die afkomstig zijn van Hallo iframe te volgen:

* Embed
  * loaded
  * error
* Rapporten
  * pageChanged
  * dataSelected (binnenkort)

[Meer informatie over het verwerken van gebeurtenissen](https://github.com/Microsoft/PowerBI-JavaScript/wiki/Handling-Events)

## <a name="next-steps"></a>Volgende stappen
Bekijk voor meer informatie over Power BI JavaScript API Hallo Hallo koppelingen te volgen:

* [Wiki over JavaScript-API](https://github.com/Microsoft/PowerBI-JavaScript/wiki)
* [Naslaginformatie over objectmodel](https://microsoft.github.io/powerbi-models/modules/_models_.html)
* Voorbeelden
  * [Angular](http://azure-samples.github.io/powerbi-angular-client)
  * [Ember](https://github.com/Microsoft/powerbi-ember)
* [Livedemo](https://microsoft.github.io/PowerBI-JavaScript/demo/)

