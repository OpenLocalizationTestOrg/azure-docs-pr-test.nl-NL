---
title: Azure Application Insights schoorstenen
description: Meer informatie over hoe u schoorstenen kunt gebruiken om te ontdekken hoe klanten communiceert met uw toepassing.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: cfreeman
ms.openlocfilehash: 85f47daaaff8967eb83c330bab839023f128b486
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="discover-how-customers-are-using-your-application-with-the-application-insights-funnels"></a>Hoe klanten gebruikmaakt van uw toepassing met de Application Insights schoorstenen detecteren

Understanding klantervaring is van het grootste belang voor uw bedrijf. Als uw toepassing meerdere fasen omvat, moet u weten als u de voortgang van de meeste klanten door het hele proces, of als ze beëindigt het proces op een bepaald moment. De voortgang door een reeks stappen in een webtoepassing staat bekend als een 'trechter'. De Application Insights schoorstenen kunt u inzicht in uw gebruikers en de monitor stapsgewijze conversie tarieven. 

## <a name="get-started-with-the-funnels-blade"></a>Aan de slag met de blade schoorstenen
De eenvoudigste manier om meer informatie over schoorstenen is op hoe u een voorbeeld. De volgende illustraties ziet u dat de stappen eigenaren van een zakelijke e-commerce zou hebben voor meer informatie over hoe hun klanten communiceren met de webtoepassing.  

### <a name="create-your-funnel"></a>Maken van de trechter
Voordat u uw trechter maakt, moet u beslissen over de vraag die u wilt beantwoorden. U wilt weten hoe veel klanten uw startpagina klikken op een advertentie bekijken. In dit voorbeeld wilt de eigenaars van het bedrijf Fabrikam Fiber weet het percentage van de klanten die een aankoop na het toevoegen van items aan de winkelwagen tijdens de afgelopen maand.

Hier volgen de stappen waarmee ze hun trechter maken.

1. Klik op de knop Nieuw op de blade schoorstenen.
1. Selecteer het tijdsbereik van 'Afgelopen maand' in de **tijdsbereik** vervolgkeuzelijst. 
1. Selecteer de **productpagina** gebeurtenis op basis van de **stap 1** vervolgkeuzelijst. 
1. Selecteer de **toevoegen aan winkelwagen** gebeurtenis op basis van de **stap 2** vervolgkeuzelijst.
1. Selecteer de **Klik op inkoop** gebeurtenis op basis van de **stap 3** vervolgkeuzelijst.
1. Een naam in de trechter toevoegen en klik op **opslaan**.

De volgende afbeelding ziet u hoe dat de gegevens van de blade schoorstenen genereert. Eigenaars kunnen hier de Fabrikam zien dat de 22.7% aan hun klanten die een item toegevoegd aan de winkelwagen tijdens de laatste week, de aankoop voltooid. Ze kunnen ook zien dat 1% van de klanten een advertentie geklikt voordat de productpagina en 20% van hun klanten afgemeld na het voltooien van hun aankoop.


![Blade schoorstenen met gegevens](./media/app-insights-understand-usage-patterns/funnel1.png)

## <a name="next-steps"></a>Volgende stappen
- Meer informatie over [gebruiksanalyse](app-insights-usage-overview.md). 
