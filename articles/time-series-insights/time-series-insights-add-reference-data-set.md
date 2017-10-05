---
title: Een referentiegegevensset toevoegen aan uw Azure Time Series Insights-omgeving | Microsoft Docs
description: In deze zelfstudie koppelt u een referentiegegevensset aan uw Time Series Insights-omgeving
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: venkatja
ms.openlocfilehash: 23444297b5231e6a026bcd9ce3ee9f943bf05867
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-the-ibiza-portal"></a>Een referentiegegevensset voor uw Time Series Insights-omgeving maken met Ibiza-portal

Een referentiegegevensset is een verzameling items die is uitgebreid met de gebeurtenissen uit uw gebeurtenisbron. De engine voor inkomende gebeurtenissen van Time Series Insights koppelt een gebeurtenis van uw gebeurtenisbron aan een item in uw referentiegegevensset. Deze uitgebreide gebeurtenis is vervolgens beschikbaar voor query’s. Deze koppeling is gebaseerd op de sleutels die zijn gedefinieerd in uw referentiegegevensset.

## <a name="steps-to-add-a-reference-data-set-to-your-environment"></a>Stappen voor het toevoegen van een referentiegegevensset aan uw omgeving

1. Meld u aan bij [Ibiza-portal](https://portal.azure.com).
2. Klik op Alle resources in het menu aan de linkerkant van de Ibiza-portal.
3. Selecteer uw Time Series Insights-omgeving.

    ![De Time Series Insights-referentiegegevensset maken](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. Selecteer 'Referentiegegevensset', klik op '+ Toevoegen.'

    ![De Time Series Insights-referentiegegevensset maken - details](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. Geef de naam van de referentiegegevensset op.
6. Geef de sleutelnaam en het bijbehorende type op. Deze naam en dit type worden gebruikt om de juiste eigenschap van de gebeurtenis in de gebeurtenisbron te kiezen. Als u bijvoorbeeld de sleutelnaam 'DeviceId' en het type 'Tekenreeks' opgeeft, zoekt de Time Series Insights-engine naar een eigenschap met de naam 'DeviceId' van het type 'Tekenreeks' in de inkomende gebeurtenis. U kunt meer meerdere sleutels opgeven om samen te voegen met de gebeurtenis. De naamsovereenkomst van de eigenschap is hoofdlettergevoelig.

     ![De Time Series Insights-referentiegegevensset maken - details](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. Klik op Maken.

## <a name="next-steps"></a>Volgende stappen

* Programmatisch [referentiegegevens beheren](time-series-insights-manage-reference-data-csharp.md).
* Zie voor de volledige API-verwijzing het document [Reference Data API](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api).