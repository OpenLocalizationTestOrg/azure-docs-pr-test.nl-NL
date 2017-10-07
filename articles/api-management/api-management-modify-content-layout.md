---
title: aaaModify pagina-inhoud in de ontwikkelaarsportal Hallo in Azure API Management | Microsoft Docs
description: Meer informatie over hoe tooedit-pagina-inhoud op Hallo ontwikkelaarsportal in Azure API Management.
services: api-management
documentationcenter: 
author: antonba
manager: vlvinogr
editor: 
ms.assetid: 186128fe-41c0-4efb-9efe-2478ad4d103f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 02/09/2017
ms.author: antonba
ms.openlocfilehash: fd5a854e900d9512518643e593b1b59a0952621f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="modify-hello-content-and-layout-of-pages-on-hello-developer-portal-in-azure-api-management"></a>Hallo-inhoud en indeling van pagina's op Hallo ontwikkelaarsportal in Azure API Management wijzigen
Er zijn drie manieren Hallo toocustomize ontwikkelaarsportal in Azure API Management:

* [Hallo-inhoud van statische pagina's en pagina-elementen voor lay-out bewerken] [ modify-content-layout] (uitgelegd in deze handleiding)
* [Update Hallo stijlen worden gebruikt voor pagina-elementen over Hallo-portal voor ontwikkelaars][customize-styles]
* [Hallo-sjablonen die worden gebruikt voor pagina's die worden gegenereerd door Hallo portal wijzigen] [ portal-templates] (bijvoorbeeld API docs, producten, gebruikersverificatie, enz.)

## <a name="page-structure"> </a>Structuur van pagina's in de ontwikkelaarsportal

Hallo developer-portal is gebaseerd op een inhoudsbeheersysteem. Hallo-indeling van elke pagina is opgebouwd op basis van de set met elementen van kleine pagina bekend als widgets:

![Paginastructuur in de ontwikkelaarsportal][api-management-customization-widget-structure]

Alle widgets kunnen worden bewerkt. 
* Hallo core inhoud specifieke tooeach afzonderlijke pagina zich bevinden in Hallo 'Inhoud' widget. Bewerken van een pagina betekent Hallo inhoud van deze widget te bewerken.
* Alle elementen voor pagina-indeling zijn met de resterende widgets Hallo opgenomen. Wijzigingen in widgets toothese tooall pagina's van toepassing. Ze zijn waarnaar wordt verwezen tooas 'widgets lay-out'.

Dagelijkse pagina wijzigt bewerken voor meerdere meestal alleen inhoud widget Hallo waarvoor verschillende inhoud voor elke afzonderlijke pagina.

## <a name="modify-layout-widget"></a>Aanpassen Hallo inhoud van een lay-widget

Inhoud in de ontwikkelaarsportal hello wordt gewijzigd via Hallo publicatieportal, die toegankelijk is vanaf hello Azure-Portal. tooreach, klikt u op **publicatieportal** van Hallo service werkbalk van uw exemplaar van API Management.

![Publicatieportal][api-management-management-console]

tooedit hello inhoud van deze widget, klikt u op **Widgets** van Hallo **Ontwikkelaarsportal** menu aan de linkerkant Hallo. Voor dit voorbeeld kunt inhoud van Hallo Header widget Hallo wijzigen. Selecteer Hallo **Header** widget uit Hallo-lijst.

![Widget Koptekst][api-management-widgets-header]

Hallo-inhoud van Hallo-header kan worden bewerkt vanuit Hallo **hoofdtekst** veld. De tekst hello naar wens wijzigen en klik vervolgens op **opslaan** Hallo Hallo pagina onderaan in.

U moet nu kunnen toosee Hallo nieuwe header op elke pagina binnen Hallo-portal voor ontwikkelaars.

> tooopen hello developer-portal in de publicatieportal hello, klikt u op **ontwikkelaarsportal** in de bovenste balk Hallo.
> 
> 

## <a name="edit-page-contents"></a>Hello inhoud van een pagina bewerken

toosee hello lijst met alle bestaande inhoudspagina's, klikt u op **inhoud** van Hallo **ontwikkelaarsportal** menu in de publicatieportal Hallo.

![Inhoud beheren][api-management-customization-manage-content]

Klik op Hallo **Welkom** tooedit pagina Wat wordt weergegeven op de startpagina Hallo van Hallo-portal voor ontwikkelaars. Breng wijzigingen Hallo, bekijk er indien nodig voorbeeld en klik vervolgens op **nu publiceren** toomake ze zichtbaar tooeveryone.

> Hallo-startpagina maakt gebruik van een speciale indeling waarmee het toodisplay een banner Hallo boven. Deze banner kan niet worden bewerkt vanuit Hallo **inhoud** sectie. tooedit dit standaardvaandel, klikt u op **Widgets** van Hallo **ontwikkelaarsportal** selecteert u **startpagina** van Hallo **huidige laag** vervolgkeuzelijst lijst en open vervolgens Hallo **Banner** item onder Hallo **sectie aanbevolen**. Hallo-inhoud van deze widget kunnen worden bewerkt net als andere pagina.
> 
> 

## <a name="next-steps"> </a>Volgende stappen
* [Update Hallo stijlen worden gebruikt voor pagina-elementen over Hallo-portal voor ontwikkelaars][customize-styles]
* [Hallo-sjablonen die worden gebruikt voor pagina's die worden gegenereerd door Hallo portal wijzigen] [ portal-templates] (bijvoorbeeld API docs, producten, gebruikersverificatie, enz.)

[Structure of developer portal pages]: #page-structure
[Modifying hello contents of a layout widget]: #modify-layout-widget
[Edit hello contents of a page]: #edit-page-contents
[Next steps]: #next-steps

[modify-content-layout]: api-management-modify-content-layout.md
[customize-styles]: api-management-customize-styles.md
[portal-templates]: api-management-developer-portal-templates.md

[api-management-customization-widget-structure]: ./media/api-management-modify-content-layout/portal-widget-structure.png
[api-management-management-console]: ./media/api-management-modify-content-layout/api-management-management-console.png
[api-management-widgets-header]: ./media/api-management-modify-content-layout/api-management-widgets-header.png
[api-management-customization-manage-content]: ./media/api-management-modify-content-layout/api-management-customization-manage-content.png
