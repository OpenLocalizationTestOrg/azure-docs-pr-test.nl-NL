---
title: cachegedrag van Azure CDN met queryreeksen - Premium aaaControl | Microsoft Docs
description: Azure CDN-queryreeks opslaan in cache bepaalt hoe bestanden toobe worden wanneer ze queryreeksen bevatten in de cache opgeslagen.
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 99db4a85-4f5f-431f-ac3a-69e05518c997
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 5c97cf0230ae13fd378bfce49481f3135a5ef101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="control-azure-cdn-caching-behavior-with-query-strings---premium"></a>Besturingselement Azure CDN cachegedrag met queryreeksen - Premium
> [!div class="op_single_selector"]
> * [Standard](cdn-query-string.md)
> * [Azure CDN Premium van Verizon](cdn-query-string-premium.md)
> 
> 

## <a name="overview"></a>Overzicht
Queryreeks opslaan in cache bepaalt hoe bestanden toobe worden wanneer ze queryreeksen bevatten in de cache opgeslagen.

> [!IMPORTANT]
> Hallo Standard en Premium-CDN-producten bieden Hallo dezelfde tekenreeks in het cachegeheugen functionaliteit query, maar het Hallo-gebruikersinterface verschilt.  Dit document beschrijft Hallo-interface voor **Azure CDN Premium van Verizon**.  Voor deze query opslaan in cache met **Azure CDN Standard van Akamai** en **Azure CDN Standard van Verizon**, Zie [beheren cachegedrag van CDN aanvragen met querytekenreeksen](cdn-query-string.md).
> 
> 

Drie beschikbare modi zijn beschikbaar:

* **Standard-cache**: dit is de standaardmodus Hallo.  op de eerste aanvraag Hallo en cache Hallo asset geeft Hallo CDN edge-knooppunt Hallo queryreeks vanuit Hallo aanvrager toohello oorsprong.  Alle volgende aanvragen voor de activa die worden aangeboden via edge-knooppunt Hallo negeert Hallo queryreeks totdat Hallo in de cache asset verloopt.
* **Er is geen cache**: In deze modus kan aanvragen met querytekenreeksen in cache zijn niet opgeslagen op Hallo CDN edge-knooppunt.  Hallo edge-knooppunt Hallo asset haalt rechtstreeks vanuit de oorsprong Hallo en geeft deze door de aanvrager toohello bij elke aanvraag.
* **unieke cache**: in deze modus wordt elke aanvraag met een queryreeks beschouwd als een unieke activum met een eigen cache.  Bijvoorbeeld, Hallo reactie van de oorsprong Hallo voor een aanvraag voor *foo.ashx?q=bar* zou worden in de cache opgeslagen op Hallo edge-knooppunt en voor daaropvolgende caches met die dezelfde querytekenreeks geretourneerd.  Een aanvraag voor *foo.ashx?q=somethingelse* zou in de cache opgeslagen als een afzonderlijk actief met een eigen toolive tijd.

## <a name="changing-query-string-caching-settings-for-premium-cdn-profiles"></a>Het wijzigen van de queryreeks opslaan in cache-instellingen voor premium-CDN-profielen
1. Blade voor Hallo CDN-profiel, klik op Hallo **beheren** knop.
   
    ![Knop blade CDN-profiel beheren](./media/cdn-query-string-premium/cdn-manage-btn.png)
   
    Hallo CDN-beheerportal geopend.
2. Houd de muis boven Hallo **HTTP grote** tabblad en houd de muis boven Hallo **Cache-instellingen** doel.  Klik op **queryreeks Caching**.
   
    Queryreeks cache-opties worden weergegeven.
   
    ![CDN-queryreeks cacheopties](./media/cdn-query-string-premium/cdn-query-string.png)
3. Nadat u hebt geselecteerd, klikt u op Hallo **Update** knop.

> [!IMPORTANT]
> Hallo instellingen wijzigingen zijn mogelijk niet direct weergegeven als het duurt voor Hallo registratie toopropagate via Hallo CDN.  Profielen van <b>Azure CDN van Verizon</b> worden doorgaans binnen 90 minuten doorgegeven, maar in sommige gevallen kan dit langer duren.
> 
> 

