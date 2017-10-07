---
title: aaaOverview van Azure Time Series Insights | Microsoft Docs
description: Inleiding tooAzure Time Series inzicht, een nieuwe service voor het time series-gegevensanalyse en IoT-oplossingen
keywords: 
services: tsi
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: 
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/20/2017
ms.author: omravi
ms.openlocfilehash: 8c022bf1fae88eddab3dbebc7bb36cc15a785172
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-time-series-insights"></a>Wat is Azure Time Series Insights?

Azure Time Series Insights is een beheerde cloudservice met de opslag, analytics en visualisatie onderdelen waarmee eenvoudig tooingest, opslaan, verkennen en analyseren van gebeurtenissen miljarden tegelijkertijd. Time Series Insights biedt u een integraal overzicht van uw gegevens, helpt u snel uw IoT-oplossing te valideren en kostbare stilstand van apparaten te vermijden door verborgen trends te ontdekken en afwijkingen te detecteren, en laat u in bijna realtime oorzaak-gevolganalyses uitvoeren. Time Series Insights opgenomen timeseries gegevens van de gebeurtenis-beleggingsmakelaars (bijvoorbeeld IoT Hubs of Event Hubs), indexeert Hallo gegevens en gegevens op basis van een configureerbare bewaarbeleid te beëindigen. Gebruikers gebruiken Hallo gegevens via een intuïtieve UX of REST-API's voor Query.

![Overzicht van Time Series Insight](media/overview/time-series-insights-overview-flow.png)

## <a name="primary-scenarios"></a>Primaire scenario's

* Bewaak en valideer IoT-oplossingen binnen enkele minuten.
* Visualiseer en analyseer grote hoeveelheden IoT-gegevens tegelijkertijd.
* Versnel hoofdoorzaakanalyse en afwijkingsdetectie.
* Stel een integraal overzicht samen van meerdere apparaten, locaties en gegevens.

## <a name="capabilities-and-benefits"></a>Mogelijkheden en voordelen

* **Eenvoudig tooget gestart**: Azure Time Series Insights zonder gegevensvoorbereiding vooraf vereist en zeer snel. Toobillions van gebeurtenissen in uw Azure-IoT-Hub of Event Hub verbonden in minuten. Eenmaal zijn verbonden, visualiseren en communiceren met sensorgegevens in seconden tooquickly valideren uw IoT-oplossingen. Time Series Insights is gemakkelijk toouse; u kunt werken met uw gegevens zonder een één regel code te schrijven.  Er is geen nieuwe taal toolearn; Time Series Insights biedt een gedetailleerde, vrije tekst query oppervlak voor ervaren gebruikers en en klik op alle exploratie.

* **In de buurt van realtime-inzichten**: Time Series Insights kan honderden miljoenen gebeurtenissen per dag, sensor opnemen met een latentie van één minuut, zodat u toochanges snel kan reageren. Time Series Insights biedt u meer inzicht in uw sensorgegevens, doordat u trends en afwijkingen snel herkent en efficiënt complexe hoofdoorzaakanalyses kunt uitvoeren. Zo voorkomt u dure uitvaltijd. U cross-correlatie tussen real-time en historische gegevens, kunt Time Series Insights u ontgrendelen verborgen trends in Hallo gegevens.

* **Aangepaste oplossingen bouwen**: integreer Azure Time Series Insights-gegevens in uw bestaande toepassingen of maak nieuwe aangepaste oplossingen met de Time Series Insights REST-API’s. Aangepaste weergaven die u kunt delen voor anderen tooexplore uw detecties maken en delen.

* **Schaalbaarheid**: Time Series inzicht is ontworpen toosupport IoT op grote schaal. Dit kan inkomend van 1 miljoen too100 miljoenen gebeurtenissen per dag met een bewaartermijn standaard span met 31 dagen in Preview. U hebt de mogelijkheid om live gegevensstromen bijna in realtime te visualiseren en te analyseren, en beschikt ook over enorme hoeveelheden historische gegevens. U verder gaat, verhogen inkomende en retentie tarieven tooaccommodate een ooit zich ontwikkelende enterprise schaal.

## <a name="time-series-insights-glossary"></a>Time Series Insights-terminologie

* **Omgeving**: een omgeving is een Azure-resource met inkomend verkeer en opslagcapaciteit.  Klanten inrichten omgevingen via hello Azure-portal met de vereiste capaciteit.
* **Gebeurtenisbron**: een gebeurtenisbron is afgeleid van een gebeurtenis-broker, zoals Azure Event Hubs.  Time Series Insights maakt rechtstreeks verbinding tooEvent bronnen, Hallo gegevensstroom opnemen zonder een code te schrijven. Op dit moment biedt Time Series Insights ondersteuning voor Azure Event Hubs en Azure IoT Hubs.
* **Referentiegegevens**: Time Series Insights biedt gebruikers Hallo mogelijkheid toojoin tijd reeksgegevens voorzien van referentiegegevens.  Referentiegegevens kunnen metagegevens bevatten over de apparaten of andere statische gegevens die relatief weinig veranderen. Time Series Insights lid wordt van de referentiegegevens Hallo met gegevensstromen, zodat gebruikers toovisualize en deze gegevens in bijna realtime analyseren.
