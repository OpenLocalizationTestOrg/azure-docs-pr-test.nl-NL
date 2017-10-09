---
title: aaaAdd verwijzing gegevensset tooyour Azure Time Series Insights omgeving | Microsoft Docs
description: In deze zelfstudie maakt u een verwijzing gegevensset tooyour Time Series Insights omgeving toevoegen
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
ms.openlocfilehash: 05e626ed81a22f2a8710b23a931ccd17c0f38ca5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-reference-data-set-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a>Een verwijzing gegevensset voor uw Time Series Insights-omgeving met behulp van de portal Ibiza Hallo maken

Een gegevensset verwijzing is een verzameling van items die zijn uitgebreid met Hallo gebeurtenissen van de gebeurtenisbron. De engine voor inkomende gebeurtenissen van Time Series Insights koppelt een gebeurtenis van uw gebeurtenisbron aan een item in uw referentiegegevensset. Deze uitgebreide gebeurtenis is vervolgens beschikbaar voor query’s. Deze koppeling is gebaseerd op Hallo sleutels die zijn gedefinieerd in uw gegevensset verwijzing.

## <a name="steps-tooadd-a-reference-data-set-tooyour-environment"></a>Stappen tooadd een verwijzing gegevensset tooyour omgeving

1. Meld u aan toohello [portal Ibiza](https://portal.azure.com).
2. Klik op 'Alle resources' in hello menu aan de linkerkant van de portal Ibiza Hallo Hallo.
3. Selecteer uw Time Series Insights-omgeving.

    ![Hallo Time Series Insights verwijzing gegevensset maken](media/add-reference-data-set/getstarted-create-reference-data-set-1.png)

4. Selecteer 'Referentiegegevensset', klik op '+ Toevoegen.'

    ![Hallo Time Series Insights verwijzing gegevensset maken - details](media/add-reference-data-set/getstarted-create-reference-data-set-2.png)

5. Geef de naam Hallo van gegevensset Hallo-verwijzing.
6. Hallo-sleutelnaam en het type opgeven. Deze naam en type is gebruikte toopick Hallo de juiste eigenschap van Hallo-gebeurtenis in de bron van de gebeurtenis. Hallo bijvoorbeeld tijd reeks Insights ingress-engine wordt gezocht naar een eigenschap met de naam van de Hallo 'DeviceId' van het type 'Tekenreeks' in inkomende hello-gebeurtenis op als u de sleutelnaam als 'DeviceId' en type als 'Tekenreeks' opgeeft, klikt u vervolgens. U kunt meer dan één sleutel toojoin met Hallo gebeurtenis opgeven. Hallo eigenschap naam overeenkomst is hoofdlettergevoelig.

     ![Hallo Time Series Insights verwijzing gegevensset maken - details](media/add-reference-data-set/getstarted-create-reference-data-set-3.png)

7. Klik op Maken.

## <a name="next-steps"></a>Volgende stappen

* Programmatisch [referentiegegevens beheren](time-series-insights-manage-reference-data-csharp.md).
* Zie voor volledige API-verwijzing hello, [API van Data-verwijzing](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api) document.
