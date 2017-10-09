---
title: aaaPre load activa op een Azure CDN-eindpunt | Microsoft Docs
description: Meer informatie over hoe toopre laden in de cache opgeslagen inhoud op een Azure CDN-eindpunt.
services: cdn
documentationcenter: 
author: smcevoy
manager: erikre
editor: 
ms.assetid: 5ea3eba5-1335-413e-9af3-3918ce608a83
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 08ac4b834f1ac8ce59d22e65fa8adea11bafcf17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="pre-load-assets-on-an-azure-cdn-endpoint"></a>Vooraf assets op een Azure CDN-eindpunt laden
[!INCLUDE [cdn-verizon-only](../../includes/cdn-verizon-only.md)]

Standaard activa eerst in de cache opgeslagen als ze worden aangevraagd. Dit betekent dat de eerste aanvraag Hallo van elke regio kan het langer duren, omdat de randservers Hallo niet Hallo inhoud in de cache opgeslagen en moet tooforward Hallo aanvraag toohello-bronserver. Vooraf laden van inhoud, wordt dit eerste treffers latentie voorkomen.

Bovendien kan tooproviding een betere klantervaring uw assets in de cache vooraf laden ook netwerkverkeer op de bronserver Hallo verminderen.

> [!NOTE]
> Vooraf laden van de activa is handig voor grote gebeurtenissen of inhoud die wordt gelijktijdig beschikbare tooa groot aantal gebruikers, zoals een nieuwe film release of een software-update.
> 
> 

Deze zelfstudie leert u de inhoud op alle knooppunten van Azure CDN edge cache vooraf laden.

## <a name="walkthrough"></a>Walkthrough
1. In Hallo [Azure Portal](https://portal.azure.com), bladeren toohello CDN-profiel met de gewenste toopre load Hallo-eindpunt.  Hallo profiel blade wordt geopend.
2. Klik op Hallo eindpunt in Hallo-lijst.  Hallo eindpunt blade wordt geopend.
3. Klik op Hallo load knop Hallo CDN-eindpunt blade.
   
    ![Blade CDN-eindpunt](./media/cdn-preload-endpoint/cdn-endpoint-blade.png)
   
    Hallo Load blade wordt geopend.
   
    ![Load-blade CDN](./media/cdn-preload-endpoint/cdn-load-blade.png)
4. Geef het volledige pad Hallo van elk actief gewenst tooload (bijv, `/pictures/kitten.png`) in Hallo **pad** textbox.
   
   > [!TIP]
   > Meer **pad** tekstvakken wordt weergegeven nadat u hebt ingevoerd tekst tooallow toobuild een lijst met meerdere elementen.  U kunt activa verwijderen uit de lijst Hallo door te klikken op de knop met het weglatingsteken (...) Hallo.
   > 
   > Paden moeten een relatieve URL die past bij de volgende Hallo [reguliere expressie](https://msdn.microsoft.com/library/az24scfc.aspx):  
   > >Het pad naar een enkel bestand laden `@"^(?:\/[a-zA-Z0-9-_.%=\u0020]+)+$"`;  
   > >Laden van één bestand met de query-tekenreeks`@"^(?:\?[-_a-zA-Z0-9\/%:;=!,.\+'&\u0020]*)?$";`  
   > 
   > Elke asset moet een eigen pad hebben.  Er is geen functionaliteit jokerteken voor bedrijfsmiddelen die vooraf laden.
   > 
   > 
   
    ![Knop laden](./media/cdn-preload-endpoint/cdn-load-paths.png)
5. Klik op Hallo **Load** knop.
   
    ![Knop laden](./media/cdn-preload-endpoint/cdn-load-button.png)

> [!NOTE]
> Er is een beperking van 10 load aanvragen per minuut per CDN-profiel. 50 paden zijn toegestaan per aanvraag. Elk pad heeft een limiet lengte van 1024 tekens.
> 
> 

## <a name="see-also"></a>Zie ook
* [Een Azure CDN-eindpunt leegmaken](cdn-purge-endpoint.md)
* [Naslaginformatie over Azure CDN REST-API - opschonen of een eindpunt vooraf laden](https://msdn.microsoft.com/library/mt634451.aspx)

