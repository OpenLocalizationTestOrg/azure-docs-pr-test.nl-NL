---
title: aaaPredict vehicle gezondheid en die zorg draagt gewoonten - Azure | Microsoft Docs
description: Hallo-mogelijkheden van Cortana Intelligence toogain real-time en voorspellende inzicht op vehicle health gebruiken en gewoonten besturen.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 09fad60b-2f48-488b-8a7e-47d1f969ec6f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 54cc890ff39493bc040bb809721388349665720f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook"></a>Draaiboek met oplossingen voor voertuigtelemetrieanalyse
Dit **menu** toohello hoofdstukken in deze playbook koppelingen. 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

## <a name="overview"></a>Overzicht
Super computers worden buiten Hallo testomgeving hebt verplaatst en nu in onze garage! Deze geavanceerde auto's bevatten een groot aantal sensoren, zodat ze Hallo mogelijkheid tootrack en bewaken van miljoenen gebeurtenissen per seconde. We verwachten dat door 2020, de meeste van deze auto's wordt zijn verbonden toohello Internet. Stel dat u toegang te krijgen tot deze schat aan gegevens tooprovide groter veiligheid, betrouwbaarheid en een beter aangedreven ervaring! Microsoft heeft gesteld dat dit een situatie met Cortana Intelligence aan het einde.

Microsoft Cortana Intelligence is een volledig beheerde big data en advanced analytics suite waarmee u tootransform uw gegevens in intelligent actie. We willen toointroduce toohello Cortana Intelligence Vehicle telemetrie Analytics oplossingssjabloon. Deze oplossing wordt gedemonstreerd hoe auto dealerbedrijven, auto fabrikanten en ondernemingen Hallo-mogelijkheden van Cortana Intelligence toogain realtime gebruiken kunnen en gewoonten voorspellende insights op de drager gezondheid en groot. 

Hallo-oplossing is geïmplementeerd als een [lambda architectuur patroon](https://en.wikipedia.org/wiki/Lambda_architecture) met Hallo mogelijkheden van Hallo Cortana Intelligence platform voor realtime en batchverwerking. Hallo-oplossing: 

* biedt een simulator Vehicle telematica
* maakt gebruik van Event Hubs voor het opnemen van miljoenen gesimuleerde vehicle telemetrische gebeurtenissen in Azure 
* maakt gebruik van Stream Analytics toogain realtime-inzichten op vehicle health
* persistente gegevens Hallo in langdurige opslag voor uitgebreidere batch analyses. 
* maakt gebruik van Machine Learning voor afwijkingsdetectie in realtime en batch-verwerking toogain voorspellende insights.
* maakt gebruik van HDInsight tootransform gegevens op schaal en Data Factory toohandle orchestration, planning, bronbeheer en bewaking van de pipeline voor Hallo batch verwerkt 
* een uitgebreide dashboard van deze oplossing biedt voor realtime-gegevens en predictive analytics visualisaties met Power BI

## <a name="architecture"></a>Architectuur
![Architectuurdiagram van de oplossing](./media/cortana-analytics-playbook-vehicle-telemetry/fig1-vehicle-telemetry-annalytics-solution-architecture.png)
*afbeelding 1 – architectuur Vehicle telemetrie Analytics-oplossing*

Deze oplossing omvat Hallo volgende **Cortana Intelligence-onderdelen** en gepresenteerd hun end tooend integratie:

* **Event Hubs** voor het opnemen van miljoenen vehicle telemetrische gebeurtenissen in Azure.
* **Stream Analytics** voor realtime-inzichten op vehicle gezondheid en dat de gegevens zich blijft voordoen in langdurige opslag voor uitgebreidere batch analyses.
* **Machine Learning** voor afwijkingsdetectie in realtime en batchverwerking toogain voorspellende insights.
* **HDInsight** gegevens over tootransform op grote schaal is
* **Data Factory** verwerkt orchestration, planning, bronbeheer en controle van de pipeline voor Hallo batch verwerkt.
* **Power BI** biedt deze oplossing een uitgebreide dashboard voor realtime-gegevens en visualisaties predictive analytics.

Deze oplossing gebruikt twee verschillende **gegevensbronnen**: 

* **Vehicle signalen en diagnostische gegevens in de simulatie**: een vehicle telematica simulator verzendt de diagnostische gegevens en signalen die overeenkomen met toohello status van Hallo vehicle en Hallo besturen patroon op een bepaald tijdstip. 
* **Vehicle catalogus**: een verwijzingsgegevensset met een Chassisnummer toomodel-toewijzing.

