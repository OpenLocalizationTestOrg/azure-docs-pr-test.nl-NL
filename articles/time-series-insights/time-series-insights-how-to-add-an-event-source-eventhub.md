---
title: aaaHow tooadd een Event Hub gebeurtenis tooyour Azure Time Series Insights bronomgeving | Microsoft Docs
description: Deze zelfstudie bevat informatie over hoe tooadd een gebeurtenis de gegevensbron is verbonden tooan Event Hub tooyour Time Series Insights omgeving
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
ms.openlocfilehash: a98cd91deb51c829084a00c5f2a80b39d0fc511c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooadd-an-event-hub-event-source"></a>Hoe tooadd een gebeurtenisbron Event Hub

Deze zelfstudie bevat informatie over hoe toouse hello Azure portal tooadd een gebeurtenisbron die uit een Event Hub tooyour Time Series Insights-omgeving kan lezen.

## <a name="prerequisites"></a>Vereisten

U hebt gemaakt van een Event Hub en gebeurtenissen tooit schrijft. Zie voor meer informatie over Event Hubs <https://azure.microsoft.com/services/event-hubs/>

> [Consumergroepen] Elke keer reeks Insights gebeurtenisbron moet toohave zijn eigen speciale klantengroep die niet wordt gedeeld met andere consumenten. Als meerdere lezers verbruiken gebeurtenissen van dezelfde consumergroep hello, kunnen alle lezers waarschijnlijk toosee fouten. Houd er rekening mee dat er ook een limiet van 20 consumergroepen per Event Hub is. Zie voor meer informatie, Hallo [Event Hubs-programmeergids](../event-hubs/event-hubs-programming-guide.md).

## <a name="choose-an-import-option"></a>Kies een optie importeren

Hallo-instellingen voor de gebeurtenisbron Hallo kunnen handmatig worden ingevoerd of een event hub kan worden geselecteerd uit Hallo event hubs die tooyou beschikbaar zijn.
In Hallo **optie importeren** selector een Hallo volgende opties kiezen:

* Geef de Event Hub-instellingen handmatig
* Gebruik Event Hub uit de beschikbare abonnementen

### <a name="select-an-available-event-hub"></a>Selecteer een beschikbare Event Hub

Hallo volgende tabel bevat uitleg over elke optie Hallo nieuwe gebeurtenisbron tabblad met de beschrijving bij het selecteren van een beschikbare Event Hub als een gebeurtenisbron:

| DE NAAM VAN EIGENSCHAP | BESCHRIJVING |
| --- | --- |
| De naam van de gebeurtenis-bron | Hallo-naam van de gebeurtenisbron. Deze naam moet uniek zijn binnen uw omgeving Time Series Insights.
| Bron | Kies **Event Hub** toocreate een gebeurtenisbron Event Hub.
| Abonnements-Id | Selecteer Hallo abonnement waarin deze event hub is gemaakt.
| Service bus-naamruimte | Selecteer Hallo Service Bus-naamruimte die Hallo Event Hub bevat.
| Naam Event hub | Selecteer de naam Hallo Hallo Event Hub.
| Naam Event hub-beleid | Selecteer Hallo gedeeld toegangsbeleid, die kan worden gemaakt op Hallo Event Hub configureren tabblad. Elk gedeeld toegangsbeleid heeft een naam, machtigingen die u instelt en toegangssleutels. Hallo gedeeld toegangsbeleid voor de gebeurtenisbron *moet* hebben **lezen** machtigingen.
| Event hub klantengroep | Hallo Consumergroep tooread gebeurtenissen van Hallo Event Hub. U wordt ten zeerste aanbevolen toouse een speciale klantengroep voor de gebeurtenisbron.

### <a name="provide-event-hub-settings-manually"></a>Geef de Event Hub-instellingen handmatig

Hallo volgende tabel bevat uitleg over elke eigenschap in Hallo nieuwe gebeurtenisbron tabblad met de beschrijving bij het invoeren van de instellingen handmatig:

| DE NAAM VAN EIGENSCHAP | BESCHRIJVING |
| --- | --- |
| De naam van de gebeurtenis-bron | Hallo-naam van de gebeurtenisbron. Deze naam moet uniek zijn binnen uw omgeving Time Series Insights.
| Bron | Kies **Event Hub** toocreate een gebeurtenisbron Event Hub.
| Abonnements-Id | Hallo abonnement waarin deze event hub is gemaakt.
| Resourcegroep | Hallo abonnement waarin deze event hub is gemaakt.
| Service bus-naamruimte | Een Service Bus-naamruimte is een container voor een set berichtentiteiten. Wanneer u een nieuwe Event Hub hebt gemaakt, hebt u ook een Service Bus-naamruimte gemaakt.
| Naam Event hub | Hallo-naam van uw Event Hub. Wanneer u uw event hub hebt gemaakt, u deze ook een specifieke naam gegeven
| Naam Event hub-beleid | beleid voor gedeelde toegang, die kan worden gemaakt op Hallo Event Hub configureren tabblad Hallo. Elk gedeeld toegangsbeleid heeft een naam, machtigingen die u instelt en toegangssleutels. Hallo gedeeld toegangsbeleid voor de gebeurtenisbron *moet* hebben **lezen** machtigingen.
| Event hub beleidssleutel | Hallo toegang tot gedeelde sleutel gebruikt tooauthenticate toegang toohello Service Bus-naamruimte. Typ Hallo primaire of secundaire sleutel hier in.
| Event hub klantengroep | Hallo Consumergroep tooread gebeurtenissen van Hallo Event Hub. U wordt ten zeerste aanbevolen toouse een speciale klantengroep voor de gebeurtenisbron.

## <a name="next-steps"></a>Volgende stappen

1. Toevoegen van een data access-beleid tooyour omgeving [definiëren data access-beleid](time-series-insights-data-access.md)
1. Toegang tot uw omgeving in Hallo [Time Series Insights-Portal](https://insights.timeseries.azure.com)
