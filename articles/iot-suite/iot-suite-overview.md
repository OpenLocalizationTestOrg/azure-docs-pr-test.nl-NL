---
title: overzicht van Azure IoT Suite aaaMicrosoft | Microsoft Docs
description: Overzicht van hoe Azure IoT Suite biedt internet der dingen vooraf geconfigureerde oplossingen toocollect, analyseren en opslaan van gegevens, bieden van visualisaties en integreren met andere systemen.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 2d38d08a-4133-4e5c-8b28-f93cadb5df05
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/24/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 385025c5ec0d37c74689a928bc09e85b33439634
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-azure-iot-suite"></a>Overview of Azure IoT Suite (Engelstalig)

Hello Azure internet der dingen (IoT)-services bieden een breed scala aan mogelijkheden. Met deze hoogwaardige services kunt u het volgende doen:

* Gegevens van apparaten verzamelen
* Gegevensstromen in beweging analyseren
* Grote gegevenssets opslaan en er query’s op uitvoeren
* Gegevens in realtime en historische gegevens visualiseren
* Integraties met back-officesystemen uitvoeren
* Uw apparaten beheren

toodeliver deze mogelijkheden kunnen Azure IoT Suite-pakketten meerdere Azure-services met aangepaste extensies als *vooraf geconfigureerde oplossingen*. Deze vooraf geconfigureerde oplossingen zijn basisimplementaties van algemene patronen van IoT-oplossing waarmee tooreduce Hallo u tijd toodeliver uw IoT-oplossingen. Met behulp van Hallo [IoT-SDK's][lnk-sdks], u kunt aanpassen en uitbreiden van deze oplossingen toomeet uw eigen vereisten. U kunt deze oplossingen gebruiken als voorbeelden of sjablonen als u nieuwe IoT-oplossingen ontwikkelt.

Hallo biedt volgende video een inleiding tooAzure IoT Suite:

> [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON309/player]
> 
> 

## <a name="azure-iot-services-in-azure-iot-suite"></a>Azure IoT-services in Azure IoT Suite
Hallo vooraf geconfigureerde oplossingen gebruiken doorgaans Hallo volgende services:

* Core tooAzure IoT Suite is Hallo [Azure IoT Hub] [ lnk-iot-hub] service. Deze service bevat Hallo apparaat-naar-cloud en de mogelijkheden voor cloud-naar-apparaat messaging en besluiten als gateway toohello Hallo cloud Hallo andere belangrijke IoT Suite-services. Hallo-service kunt u berichten van uw apparaten op schaal tooreceive en opdrachten tooyour apparaten verzenden. Hallo-service kunt u ook te[beheren van uw apparaten][lnk-device-management]. U kunt bijvoorbeeld configureren, opnieuw starten of u de fabrieksinstellingen op een of meer apparaten verbonden toohello hub.
* [Azure Stream Analytics][lnk-asa] biedt de mogelijkheid om gegevens in beweging te analyseren. IoT Suite maakt gebruik van deze service tooprocess binnenkomende telemetriegegevens, uitvoeren van aggregatiebewerkingen en detecteren van gebeurtenissen. Hallo vooraf geconfigureerde oplossingen gebruiken ook stream analytics tooprocess informatieve berichten met gegevens zoals metagegevens of opdracht reacties van apparaten. Hallo oplossingen gebruik Stream Analytics tooprocess Hallo-berichten van uw apparaten en deze berichten tooother services leveren.
* [Azure Storage] [ lnk-azure-storage] en [Azure Cosmos DB] [ lnk-document-db] Hallo gegevens opslagmogelijkheden bevatten. Hallo vooraf geconfigureerde oplossingen gebruiken blob storage toostore Telemetrie en toomake deze beschikbaar voor analyse. Hallo oplossingen gebruik van metagegevens van de Cosmos-DB toostore apparaten en schakel mogelijkheden voor Apparaatbeheer Hallo van Hallo-oplossingen.
* [Azure Web Apps] [ lnk-web-apps] en [Microsoft Power BI] [ lnk-power-bi] Hallo gegevensvisualisatie mogelijkheden bieden. Hallo flexibiliteit van Power BI kunt u tooquickly bouwen uw eigen interactieve dashboards die gebruikmaken van IoT Suite-gegevens.

Zie voor een overzicht van Hallo-architectuur van een typische IoT-oplossing [Microsoft Azure en Internet der dingen (IoT) Hallo][iot-suite-what-is-azure-iot].

## <a name="preconfigured-solutions"></a>Vooraf geconfigureerde oplossingen

IoT Suite bevat vooraf geconfigureerde oplossingen die u tooquickly aan de slag met inschakelen en tooexplore Hallo algemene IoT-scenario's, zoals:

* Externe bewaking
* Voorspellend onderhoud
* Verbonden factory

U kunt deze oplossingen tooyour Azure-abonnement implementeren en voer vervolgens een volledige, end-to-end-IoT-scenario.

## <a name="next-steps"></a>Volgende stappen

Nu dat u een overzicht van wat IoT Suite kan doen en wat zijn de belangrijkste componenten hebt, kunt u meer informatie over Hallo vooraf geconfigureerde oplossingen in IoT Suite. Zie voor meer informatie [wat hello Azure IoT zijn vooraf geconfigureerde oplossingen?][lnk-what-are-preconfig]

[lnk-sdks]: https://azure.microsoft.com/documentation/articles/iot-hub-sdks-summary/
[lnk-iot-hub]: https://azure.microsoft.com/documentation/services/iot-hub/
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-azure-storage]: https://azure.microsoft.com/documentation/services/storage/
[lnk-document-db]: https://azure.microsoft.com/documentation/services/documentdb/
[lnk-power-bi]: https://powerbi.microsoft.com/
[lnk-web-apps]: https://azure.microsoft.com/documentation/services/app-service/web/
[iot-suite-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-what-are-preconfig]: iot-suite-what-are-preconfigured-solutions.md
[lnk-device-management]: ../iot-hub/iot-hub-device-management-overview.md
