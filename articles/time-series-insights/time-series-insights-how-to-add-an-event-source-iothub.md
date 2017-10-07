---
title: aaaHow tooadd een IoT Hub gebeurtenis tooyour Azure Time Series Insights bronomgeving | Microsoft Docs
description: Deze zelfstudie bevat informatie over hoe een gebeurtenis die bron tooadd tooan IoT Hub tooyour Time Series Insights omgeving verbonden
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
ms.openlocfilehash: c626f9653d1c012360120fa9fc3d211d7d5beb5b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-an-iot-hub-event-source"></a>Hoe tooadd een gebeurtenisbron IoT-Hub

Deze zelfstudie bevat informatie over hoe toouse hello Azure portal tooadd een gebeurtenisbron die uit een IoT Hub tooyour Time Series Insights-omgeving kan lezen.

## <a name="prerequisites"></a>Vereisten

U hebt een IoT-Hub gemaakt en gebeurtenissen tooit schrijft. Zie voor meer informatie over IoT Hubs <https://azure.microsoft.com/services/iot-hub/>

> [Consumergroepen] Elke keer reeks Insights gebeurtenisbron moet toohave zijn eigen speciale klantengroep die niet wordt gedeeld met andere consumenten. Als meerdere lezers verbruiken gebeurtenissen van dezelfde consumergroep hello, kunnen alle lezers waarschijnlijk toosee fouten. Zie voor meer informatie, Hallo [Ontwikkelaarshandleiding voor IoT Hub](../iot-hub/iot-hub-devguide.md).

## <a name="choose-an-import-option"></a>Kies een optie importeren

Hallo-instellingen voor de gebeurtenisbron Hallo kunnen handmatig worden ingevoerd of een IoT-hub kan worden geselecteerd uit Hallo IoT hubs die tooyou beschikbaar zijn.
In Hallo **optie importeren** selector een Hallo volgende opties kiezen:

* Geef de IoT Hub-instellingen handmatig
* Gebruik IoT Hub uit de beschikbare abonnementen

### <a name="select-an-available-iot-hub"></a>Selecteer een beschikbare IoT-Hub

Hallo volgende tabel bevat uitleg over elke optie Hallo nieuwe gebeurtenisbron tabblad met de beschrijving bij het selecteren van een IoT-Hub beschikbaar als een gebeurtenisbron:

| DE NAAM VAN EIGENSCHAP | BESCHRIJVING |
| --- | --- |
| De naam van de gebeurtenis-bron | Hallo-naam van de gebeurtenisbron. Deze naam moet uniek zijn binnen uw omgeving Time Series Insights.
| Bron | Kies **IoT Hub** toocreate een gebeurtenisbron IoT Hub.
| Abonnements-Id | Selecteer Hallo abonnement waarin deze iothub is gemaakt.
| De naam van de IoT-hub | Selecteer de naam Hallo Hallo IoT Hub.
| Naam voor het IoT-hub | Selecteer Hallo gedeeld-beleid, u op Hallo tabblad IoT Hub-instellingen vinden kunt. Elk gedeeld toegangsbeleid heeft een naam, machtigingen die u instelt en toegangssleutels. Hallo gedeeld toegangsbeleid voor de gebeurtenisbron *moet* hebben **service verbinding** machtigingen.
| IoT hub klantengroep | Hallo Consumergroep tooread gebeurtenissen van Hallo IoT Hub. U wordt ten zeerste aanbevolen toouse een speciale klantengroep voor de gebeurtenisbron.

### <a name="provide-iot-hub-settings-manually"></a>Geef de IoT Hub-instellingen handmatig

Hallo volgende tabel bevat uitleg over elke eigenschap in Hallo nieuwe gebeurtenisbron tabblad met de beschrijving bij het invoeren van de instellingen handmatig:

| DE NAAM VAN EIGENSCHAP | BESCHRIJVING |
| --- | --- |
| De naam van de gebeurtenis-bron | Hallo-naam van de gebeurtenisbron. Deze naam moet uniek zijn binnen uw omgeving Time Series Insights.
| Bron | Kies **IoT Hub** toocreate een gebeurtenisbron IoT Hub.
| Abonnements-Id | Hallo abonnement waarin deze iothub is gemaakt.
| Resourcegroep | Hallo abonnement waarin deze iothub is gemaakt.
| De naam van de IoT-hub | Hallo-naam van uw IoT-Hub. Wanneer u uw IoT-hub gemaakt, u dit ook een specifieke naam gegeven
| Naam voor het IoT-hub | Hallo gedeeld toegangsbeleid, die kan worden gemaakt op Hallo tabblad IoT Hub-instellingen. Elk gedeeld toegangsbeleid heeft een naam, machtigingen die u instelt en toegangssleutels. Hallo gedeeld toegangsbeleid voor de gebeurtenisbron *moet* hebben **service verbinding** machtigingen.
| IoT hub beleidssleutel | Hallo toegang tot gedeelde sleutel gebruikt tooauthenticate toegang toohello Service Bus-naamruimte. Typ Hallo primaire of secundaire sleutel hier in.
| IoT hub klantengroep | Hallo Consumergroep tooread gebeurtenissen van Hallo IoT Hub. U wordt ten zeerste aanbevolen toouse een speciale klantengroep voor de gebeurtenisbron.

## <a name="next-steps"></a>Volgende stappen

1. Toevoegen van een data access-beleid tooyour omgeving [definiëren data access-beleid](time-series-insights-data-access.md)
1. Toegang tot uw omgeving in Hallo [Time Series Insights-Portal](https://insights.timeseries.azure.com)
