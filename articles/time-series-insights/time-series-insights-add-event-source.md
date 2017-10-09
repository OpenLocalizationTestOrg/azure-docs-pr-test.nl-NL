---
title: een gebeurtenis tooyour Azure Time Series Insights bronomgeving aaaAdd | Microsoft Docs
description: In deze zelfstudie maakt u verbinding maakt een gebeurtenis tooyour Time Series Insights bronomgeving
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
ms.openlocfilehash: 817df5e81cb4dc3d7376914a4651aabebadbcc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-source-for-your-time-series-insights-environment-using-hello-ibiza-portal"></a>Maken van een gebeurtenisbron voor uw Time Series Insights-omgeving met behulp van de portal Ibiza Hallo

Een Time Series Insights-gebeurtenisbron is afgeleid van een gebeurtenis-broker, zoals Azure Event Hubs. Time Series Insights maakt rechtstreeks verbinding tooEvent bronnen, Hallo gegevensstroom zonder gebruikers toowrite één regel code opnemen. Op dit moment biedt Time Series Insights ondersteuning voor Azure Event Hubs en Azure IoT Hubs. In toekomstige hello, worden meer bronnen van gebeurtenissen toegevoegd.

## <a name="steps-tooadd-an-event-source-tooyour-environment"></a>Stappen tooadd tooyour bronomgeving van een gebeurtenis

1.  Meld u aan toohello [portal Ibiza](https://portal.azure.com).
2.  Klik op 'Alle resources' in hello menu aan de linkerkant van de portal Ibiza Hallo Hallo.
3.  Selecteer uw Time Series Insights-omgeving.

  ![Hallo Time Series Insights gebeurtenisbron maken](media/add-event-source/getstarted-create-event-source-1.png)

4.  Selecteer Gebeurtenisbronnen en klik op + Toevoegen.

  ![Hallo Time Series Insights gebeurtenisbron - details maken](media/add-event-source/getstarted-create-event-source-2.png)

5.  Hallo-naam van de gebeurtenisbron Hallo opgeven. Deze naam is gekoppeld aan alle gebeurtenissen afkomstig uit deze gebeurtenisbron en komt tijdens het uitvoeren van query's beschikbaar.
6.  Selecteer een event hub uit Hallo lijst met resources in het huidige abonnement Hallo Event Hub. Kies anders optie importeren ' Geef Event Hub-instellingen handmatig ' toospecify een event hub in een ander abonnement. Gebeurtenissen moeten worden gepubliceerd in de JSON-indeling.
7.  Selecteer beleid dat u beschikt over leesmachtiging in Hallo event hub.
8.  Specificeer de Event Hub-consumergroep.

  > [!IMPORTANT]
  > Deze consumergroep mag niet worden gebruikt door een andere service (zoals een Stream Analytics-taak of een andere Time Series Insights-omgeving). Als consumergroep wordt gebruikt door andere services, bewerking nadelig wordt beïnvloed voor deze omgeving lees- en andere services Hallo. Als u '$Default' als consumergroep hello, kan dit ertoe leiden toopotential opnieuw kunnen worden gebruikt door andere lezers.

9.  Klik op Maken.

Nadat het maken van de gebeurtenisbron hello, wordt Time Series Insights automatisch gestart gegevensstromen in uw omgeving.

## <a name="next-steps"></a>Volgende stappen

* [Verzenden van gebeurtenissen](time-series-insights-send-events.md) toohello gebeurtenisbron
* Uw omgeving bekijken in de [Time Series Insights-portal](https://insights.timeseries.azure.com)
