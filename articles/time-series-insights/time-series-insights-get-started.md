---
title: een Azure Time Series Insights omgeving aaaCreate | Microsoft Docs
description: In deze zelfstudie leert u hoe toocreate Time Series-omgeving, verbindt u deze tooan gebeurtenisbron en klaar tooanalyze de gebeurtenisgegevens in minuten.
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: santoshb
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: omravi
ms.openlocfilehash: 7120fc9a6e4d4a4972f8cb37e4d9945cfb746fd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-new-time-series-insights-environment-in-hello-azure-portal"></a>Maak een nieuwe Time Series Insights-omgeving in hello Azure-portal

Een Time Series Insights-omgeving is een Azure-resource met inkomend verkeer en opslagcapaciteit. Klanten inrichten omgevingen via hello Azure-portal met Hallo vereist capaciteit.

## <a name="steps-toocreate-hello-environment"></a>Stappen toocreate Hallo-omgeving

Volg deze stappen toocreate uw omgeving:

1.  Meld u aan toohello [Azure-portal](https://portal.azure.com).
2.  Klik op Hallo plus -teken ('+') in de linkerbovenhoek Hallo.
3.  Zoeken naar 'Time Series Insights' in het zoekvak Hallo.

  ![Hallo Time Series Insights omgeving maken](media/get-started/getstarted-create-environment1.png)

4.  Selecteer Time Series Insights en klik op Maken.

  ![Hallo Time Series Insights resourcegroep maken](media/get-started/getstarted-create-environment2.png)

5.  Geef de naam van de omgeving op. Deze naam vertegenwoordigt Hallo-omgeving in [time series explorer](https://insights.timeseries.azure.com).
6.  Selecteer een abonnement. Kies een abonnement dat uw gebeurtenisbron bevat. Time Series inzichten kunt automatische detectie Azure IoT Hub en Event Hub-resources in bestaande Hallo hetzelfde abonnement.
7.  Selecteer of maak een resourcegroep. Een resourcegroep is een verzameling Azure-resources die samen worden gebruikt.
8.  Selecteer een hostinglocatie. tooavoid verplaatsen tussen gegevens datacenters, kies de locatie waarin de gebeurtenisbron.
9.  Selecteer een prijscategorie.
10. Selecteer de capaciteit. U kunt de capaciteit van een omgeving wijzigen nadat deze is gemaakt.
11. Maak uw omgeving. Wanneer u zich aanmeldt, kunt u uw dashboard omgeving toohello voor eenvoudige toegang vastmaken.

  ![Hallo Time Series Insights pincode toodashboard maken](media/get-started/getstarted-create-environment3.png)

## <a name="next-steps"></a>Volgende stappen

* [Definieer gegevenstoegangsbeleid](time-series-insights-data-access.md) tooaccess uw omgeving in [Time Series Insights-Portal](https://insights.timeseries.azure.com)
* [Een gebeurtenisbron maken](time-series-insights-add-event-source.md)
* [Verzenden van gebeurtenissen](time-series-insights-send-events.md) toohello gebeurtenisbron
