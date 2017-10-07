---
title: aaaHow tooscale uw omgeving Azure Time Series Insights | Microsoft Docs
description: Deze zelfstudie bevat informatie over hoe tooscale uw Azure Time Series Insights-omgeving
keywords: 
services: time-series-insights
documentationcenter: 
author: sandshadow
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/19/2017
ms.author: edett
ms.openlocfilehash: 55eda388997589185bd34228762b95e182b228ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooscale-your-time-series-insights-environment"></a>Hoe tooscale uw omgeving Time Series Insights

Deze zelfstudie bevat informatie over hoe tooscale uw Time Series Insights-omgeving.

> [!NOTE]
> Opschaling van de verschillende typen sku is niet toegestaan. Een omgeving met een Sku S1 kan niet worden geconverteerd naar een S2-omgeving.

## <a name="s1-sku-ingress-rates-and-capacities"></a>S1 SKU inkomend tarieven en capaciteit

| S1 SKU-capaciteit | Snelheid van inkomende gegevens | Maximale opslagcapaciteit
| --- | --- | --- |
| 1 | 1 GB (1 miljoen gebeurtenissen) | 30 GB (30 miljoen gebeurtenissen) per maand |
| 10 | 10 GB (10 miljoen gebeurtenissen) | 300 GB (300 miljoen gebeurtenissen) per maand |

## <a name="s2-sku-ingress-rates-and-capacities"></a>S2 SKU inkomend tarieven en capaciteit

| S2 SKU-capaciteit | Snelheid van inkomende gegevens | Maximale opslagcapaciteit
| --- | --- | --- |
| 1 | 10 GB (10 miljoen gebeurtenissen) | 300 GB (300 miljoen gebeurtenissen) per maand |
| 10 | 100 GB (100 miljoen gebeurtenissen) | 3 TB (3 miljard gebeurtenissen) per maand |

Capaciteitswaarden evenredig, zodat een sku S1 capaciteit 2 2 GB (2 miljoen) gebeurtenissen per dag inkomend en 60 GB (60 miljoen gebeurtenissen) per maand ondersteunt.

## <a name="changing-hello-capacity-of-your-environment"></a>Hallo-capaciteit van uw omgeving wijzigen

1. In hello Azure-portal, selecteer Hallo omgeving waarvan capaciteit gewenste toochange.
1. Klik onder instellingen configureren.
1. Gebruik Hallo capaciteit schuifregelaar tooselect Hallo capaciteit die voldoet aan vereisten voor de tarieven van de inkomende hello- en opslagcapaciteit.

## <a name="next-steps"></a>Volgende stappen

* Controleer of de nieuwe capaciteit Hallo voldoende tooprevent beperking. Zie voor meer informatie, Hallo *uw omgeving kan worden opgehaald beperkt* sectie [hier](time-series-insights-diagnose-and-solve-problems.md).
