---
title: cachegedrag van Azure CDN met queryreeksen aaaControl | Microsoft Docs
description: Azure CDN-queryreeks opslaan in cache bepaalt hoe bestanden toobe worden wanneer ze queryreeksen bevatten in de cache opgeslagen.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 17410e4f-130e-489c-834e-7ca6d6f9778d
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: e7a138b2decec624a29eb703ad9a291d19c44ee8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings"></a>Besturingselement Azure CDN cachegedrag met queryreeksen
> [!div class="op_single_selector"]
> * [Standard](cdn-query-string.md)
> * [Azure CDN Premium van Verizon](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a>Overzicht
Queryreeks opslaan in cache bepaalt hoe bestanden toobe worden wanneer ze queryreeksen bevatten in de cache opgeslagen.

> [!IMPORTANT]
> Hallo Standard en Premium-CDN-producten bieden Hallo dezelfde tekenreeks in het cachegeheugen functionaliteit query, maar het Hallo-gebruikersinterface verschilt.  Dit document beschrijft Hallo-interface voor **Azure CDN Standard van Akamai** en **Azure CDN Standard van Verizon**.  Voor deze query opslaan in cache met **Azure CDN Premium van Verizon**, Zie [beheren cachegedrag van CDN aanvragen met querytekenreeksen - Premium](cdn-query-string-premium.md).
> 
> 

Drie beschikbare modi zijn beschikbaar:

* **Querytekenreeksen negeren**: dit is de standaardmodus Hallo.  op de eerste aanvraag Hallo en cache Hallo asset geeft Hallo CDN edge-knooppunt Hallo queryreeks vanuit Hallo aanvrager toohello oorsprong.  Alle volgende aanvragen voor de activa die worden aangeboden via edge-knooppunt Hallo negeert Hallo queryreeks totdat Hallo in de cache asset verloopt.
* **Overslaan voor URL's met querytekenreeksen**: In deze modus kan aanvragen met querytekenreeksen in cache zijn niet opgeslagen op Hallo CDN edge-knooppunt.  Hallo edge-knooppunt Hallo asset haalt rechtstreeks vanuit de oorsprong Hallo en geeft deze door de aanvrager toohello bij elke aanvraag.
* **Elke unieke URL in de cache**: in deze modus wordt elke aanvraag met een queryreeks beschouwd als een unieke activum met een eigen cache.  Bijvoorbeeld, Hallo reactie van de oorsprong Hallo voor een aanvraag voor *foo.ashx?q=bar* zou worden in de cache opgeslagen op Hallo edge-knooppunt en voor daaropvolgende caches met die dezelfde querytekenreeks geretourneerd.  Een aanvraag voor *foo.ashx?q=somethingelse* zou in de cache opgeslagen als een afzonderlijk actief met een eigen toolive tijd.

## <a name="changing-query-string-caching-settings-for-standard-cdn-profiles"></a>Het wijzigen van de queryreeks opslaan in cache-instellingen voor standaard CDN-profielen
1. Blade voor Hallo CDN-profiel, klik op Hallo gewenst toomanage CDN-eindpunt.
   
    ![CDN-profiel blade-eindpunten](./media/cdn-query-string/cdn-endpoints.png)
   
    Hallo CDN-eindpunt blade wordt geopend.
2. Klik op Hallo **configureren** knop.
   
    ![Knop blade CDN-profiel beheren](./media/cdn-query-string/cdn-config-btn.png)
   
    Hallo CDN configuratie blade wordt geopend.
3. Selecteer een instelling in Hallo **queryreeks cachegedrag** vervolgkeuzelijst.
   
    ![CDN-queryreeks cacheopties](./media/cdn-query-string/cdn-query-string.png)
4. Nadat u hebt geselecteerd, klikt u op Hallo **opslaan** knop.

> [!IMPORTANT]
> Hallo instellingen wijzigingen zijn mogelijk niet direct weergegeven als het duurt voor Hallo registratie toopropagate via Hallo CDN.  Profielen van <b>Azure CDN van Akamai</b> worden doorgaans binnen één minuut doorgegeven.  Profielen van <b>Azure CDN van Verizon</b> worden doorgaans binnen 90 minuten doorgegeven, maar in sommige gevallen kan dit langer duren.
> 
> 

