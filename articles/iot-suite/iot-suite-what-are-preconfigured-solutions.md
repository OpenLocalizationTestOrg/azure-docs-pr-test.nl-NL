---
title: aaaAzure IoT vooraf geconfigureerde oplossingen | Microsoft Docs
description: Een beschrijving van hello Azure IoT vooraf geconfigureerde oplossingen en hun architectuur, met koppelingen tooadditional resources.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 59009f37-9ba0-4e17-a189-7ea354a858a2
ms.service: iot-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/25/2017
ms.author: dobett
ms.openlocfilehash: bd059d08ab458fdb0b6f49b3ac469db930dab09e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-hello-azure-iot-suite-preconfigured-solutions"></a>Wat zijn hello Azure IoT Suite vooraf geconfigureerde oplossingen?

Hello Azure IoT Suite vooraf geconfigureerde oplossingen zijn implementaties van algemene IoT-oplossingspatronen dat u uw abonnement te gebruiken tooAzure kunt implementeren. U kunt Hallo vooraf geconfigureerde oplossingen gebruiken:

* Als een beginpunt voor uw eigen IoT-oplossingen.
* toolearn over algemene patronen bij IoT-oplossing ontwerpen en ontwikkelen.

Elke vooraf geconfigureerde oplossing is een volledige, end-to-end implementatie dat maakt gebruik van apparaten toogenerate telemetrie gesimuleerde.

U kunt Hallo volledige broncode code toocustomize downloaden en uw specifieke IoT-vereisten voor Hallo oplossing toomeet uitbreiden.

> [!NOTE]
> toodeploy Hallo vooraf geconfigureerde oplossingen, gaat u naar [Microsoft Azure IoT Suite][lnk-azureiotsuite]. Hallo artikel [aan de slag met vooraf geconfigureerde IoT-oplossingen Hallo] [ lnk-getstarted-preconfigured] vindt u meer informatie over hoe toodeploy en voer een van Hallo oplossingen.

Hallo volgende tabel ziet u hoe Hallo oplossingen toegewezen toospecific IoT-functies:

| Oplossing | Gegevensopname | Apparaat-id | Apparaatbeheer | Opdracht en controle | Regels en acties | Predictive analytics |
| --- | --- | --- | --- | --- | --- | --- |
| [Externe bewaking][lnk-getstarted-preconfigured] |Ja |Ja |Ja |Ja |Ja |- |
| [Voorspeld onderhoud][lnk-predictive-maintenance] |Ja |Ja |- |Ja |Ja |Ja |
| [Verbonden factory][lnk-getstarted-factory] |Ja |Ja |Ja |Ja |Ja |- |

* *Gegevensopname*: instroom van gegevens op schaal toohello cloud.
* *Apparaat-id*: unieke apparaat-id's beheren en controleren van apparaat toegang toohello oplossing.
* *Apparaatbeheer*: beheer metagegevens van apparaten en voer bewerkingen uit, zoals het opnieuw opstarten van apparaten en firmware-upgrades.
* *Opdracht en controle*: toocause Hallo apparaat tootake een actie, verzendt berichten tooa apparaat vanuit Hallo cloud.
* *Regels en acties*: tooact op specifieke apparaat-naar-cloud-gegevens, Hallo back-end oplossing gebruikt regels.
* *Predictive analytics*: Hallo back-end oplossing analyseert apparaat-naar-cloudgegevens toopredict wanneer bepaalde acties moeten plaatsvinden. Bijvoorbeeld: vliegtuig engine telemetrie toodetermine analyseren wanneer motoronderhoud vereist is.

## <a name="remote-monitoring-preconfigured-solution-overview"></a>Overzicht van vooraf geconfigureerde oplossing voor externe controle

We hebben ervoor gekozen toodiscuss Hallo vooraf geconfigureerde oplossing voor externe controle in dit artikel omdat veel voorkomende ontwerpelementen die andere oplossingen share Hallo worden geïllustreerd.

Hallo illustreert volgende diagram de belangrijkste elementen Hallo Hallo oplossing voor externe controle. Hallo bevatten volgende secties meer informatie over deze elementen.

![Architectuur van de vooraf geconfigureerde oplossing voor externe controle][img-remote-monitoring-arch]

## <a name="devices"></a>Apparaten

Wanneer u Hallo vooraf geconfigureerde oplossing voor externe controle implementeert, zijn vier gesimuleerde apparaten vooraf is ingericht in Hallo-oplossing die een koelapparaat simuleren. Deze gesimuleerde apparaten hebben een ingebouwd temperatuur- en vochtigheidsmodel dat telemetrie verzendt. Deze gesimuleerde apparaten zijn opgenomen om:

- Hallo end-to-end-stroom van gegevens door Hallo oplossing illustreren.
- Een handige bron van telemetrie te verstrekken.
- Geef een doel voor methoden of opdrachten als u een back-end-ontwikkelaar met behulp van Hallo oplossing als uitgangspunt voor een aangepaste implementatie.

Hallo gesimuleerde apparaten in Hallo oplossing kunnen reageren toohello cloud-naar-apparaat communicatie te volgen:

- *Methoden ([methoden directe][lnk-direct-methods])*: een tweerichtingscommunicatie methode waarbij een verbonden apparaat verwachte toorespond onmiddellijk is.
- *Opdrachten (cloud-naar-apparaat-berichten)*: een eenzijdige communicatiemethode waar een apparaat Hallo opdracht van een duurzame wachtrij ophaalt.

Zie [Cloud-to-device communications guidance][lnk-c2d-guidance] (Richtlijnen voor communicatie tussen cloud en apparaat) voor een vergelijking van deze verschillende methoden.

Wanneer een apparaat tooIoT Hub in Hallo vooraf geconfigureerde oplossing voor het eerst verbinding maakt, stuurt een apparaat informatie bericht toohello hub. Dit bericht inventariseren Hallo methoden Hallo apparaat kan reageren. In de vooraf geconfigureerde oplossing voor externe controle hello, ondersteunen gesimuleerde apparaten deze methoden:

* *Starten van de Firmware bijwerken*: deze methode een asynchrone taak op Hallo apparaat tooperform een firmware-update wordt gestart. Hallo asynchrone taak maakt gebruik van gerapporteerde eigenschappen toodeliver status updates toohello dashboard van de oplossing.
* *Opnieuw opstarten*: deze methode veroorzaakt Hallo gesimuleerd apparaat tooreboot.
* *FactoryReset*: deze methode een fabrieksinstellingen op Hallo gesimuleerde apparaat wordt geactiveerd.

Wanneer een apparaat tooIoT Hub in Hallo vooraf geconfigureerde oplossing voor het eerst verbinding maakt, stuurt een apparaat informatie bericht toohello hub. Dit bericht inventariseren Hallo opdrachten Hallo apparaat kan reageren. In de vooraf geconfigureerde oplossing voor externe controle hello, ondersteunen gesimuleerde apparaten deze opdrachten:

* *Ping-apparaat*: Hallo apparaat reageert toothis opdracht met een bevestiging. Deze opdracht is handig om te controleren dat het Hallo-apparaat is nog steeds actief is en luistert.
* *Starttelemetry*: Hiermee geeft u Hallo apparaat toostart verzenden van telemetrie.
* *Geen telemetrie meer*: Hiermee geeft u Hallo apparaat toostop verzenden van telemetrie.
* *Changesetpointtemperature*: besturingselementen Hallo gesimuleerde temperatuur telemetrie waarden Hallo apparaat verzendt. Deze opdracht is handig voor het testen van back-endlogica.
* *Diagnostische telemetrie*: Hiermee wordt bepaald of het apparaat Hallo Hallo externe temperatuur als telemetrie moet verzenden.
* *Changedevicestate*: Hallo apparaat status metagegevenseigenschap die Hallo apparaat rapporten ingesteld. Deze opdracht is handig voor het testen van back-endlogica.

U kunt meer gesimuleerde apparaten toohello oplossing die Hallo verzenden toevoegen dezelfde Telemetrie en reageren toohello dezelfde methoden en opdrachten.

Bovendien tooresponding toocommands en methoden Hallo oplossing maakt gebruik van [apparaat horende][lnk-device-twin]. Apparaten gebruiken apparaat horende tooreport eigenschap waarden toohello back-end oplossing. Hallo dashboard van de oplossing maakt gebruik van eigenschapswaarden voor apparaat horende tooset toonew gewenst op apparaten. Bijvoorbeeld tijdens het Hallo-firmware bijwerken proces Hallo gesimuleerd apparaat rapporten Hallo status Hallo bijwerken met behulp van gerapporteerde eigenschappen.

## <a name="iot-hub"></a>IoT Hub

In deze vooraf geconfigureerde oplossing hello IoT Hub-instantie overeen toohello *Cloudgateway* in een typische [IoT-oplossingsarchitectuur][lnk-what-is-azure-iot].

Een IoT-hub ontvangt telemetrie van Hallo apparaten op één eindpunt. Een IoT-hub onderhoudt ook apparaatspecifieke eindpunten waar elk apparaat Hallo-opdrachten die worden verzonden tooit kunt terugvinden.

Hallo iothub stelt Hallo ontvangen telemetrie beschikbaar via de telemetrie aan servicezijde Hallo eindpunt voor het lezen.

Hallo apparaat management mogelijkheden van IoT-Hub kunt u toomanage de apparaateigenschappen van uw uit Hallo oplossing portal en planning taken die bewerkingen, zoals uitvoeren:

- Apparaten opnieuw opstarten
- Apparaatstatussen wijzigen
- Firmware-updates

## <a name="azure-stream-analytics"></a>Azure Stream Analytics

Hallo vooraf geconfigureerde oplossing maakt gebruik van drie [Azure Stream Analytics] [ lnk-asa] (ASA) taken toofilter hello telemetriestroom vanaf Hallo apparaten:

* *De job DeviceInfo* -uitvoer gegevens tooan Event hub die apparaatregister van apparaat registratie-specifieke berichten toohello oplossing. Dit apparaatregister is een Azure Cosmos DB-database. Deze berichten worden verzonden wanneer een apparaat voor het eerst verbinding maakt of in het antwoord tooa **Changedevicestate** opdracht.
* *Telemetrie-taak* - verzendt alle onbewerkte telemetrie tooAzure blob storage voor koude opslag en berekent telemetrieaggregaties die worden weergegeven in het dashboard van de oplossing Hallo.
* *Job Rules* - filters Hallo telemetriestroom op waarden die groter zijn dan regeldrempelwaarden en uitvoer Hallo gegevens tooan Event hub. Wanneer een regel wordt gestart, wordt Hallo oplossing portal dashboardweergave deze gebeurtenis weergegeven als een nieuwe rij in de geschiedenistabel Hallo-waarschuwing. Deze regels kunnen ook een actie die op basis van Hallo-instellingen die zijn gedefinieerd op Hallo activeren **regels** en **acties** weergaven in de oplossingsportal Hallo.

In deze vooraf geconfigureerde oplossing Hallo ASA taken die deel uitmaken van toohello **IoT back-end oplossing** in een typische [IoT-oplossingsarchitectuur][lnk-what-is-azure-iot].

## <a name="event-processor"></a>Gebeurtenisprocessor

In deze vooraf geconfigureerde oplossing Hallo gebeurtenisprocessor deel uit van Hallo **IoT back-end oplossing** in een typische [IoT-oplossingsarchitectuur][lnk-what-is-azure-iot].

Hallo **DeviceInfo** en **regels** ASA-jobs verzenden hun uitvoer tooEvent hubs voor levering tooother back-end-services. Hallo-oplossing maakt gebruik van een [EventProcessorHost] [ lnk-event-processor] instantie, die in een [webtaak][lnk-web-job], tooread Hallo-berichten van deze Event hubs. Hallo **EventProcessorHost** gebruikt:
- Hallo **DeviceInfo** gegevens tooupdate Hallo apparaatgegevens in Hallo Cosmos-DB-database.
- Hallo **regels** gegevens tooinvoke Hallo Logic app en update Hallo waarschuwingen worden weergegeven in de oplossingsportal Hallo.

## <a name="device-identity-registry-device-twin-and-cosmos-db"></a>Register voor apparaat-id's, apparaatdubbel en Cosmos DB

Elke IoT Hub bevat een [register voor apparaat-id's][lnk-identity-registry] waarin apparaatsleutels worden opgeslagen. IoT Hub gebruikt deze informatie apparaten verifiëren op-een apparaat moet zijn geregistreerd en een geldige sleutel hebben voordat deze verbinding met toohello hub maken kan.

Een [apparaat twin] [ lnk-device-twin] is een JSON-document beheerd door Hallo IoT Hub. Een apparaatdubbel voor een apparaat bevat:

- Gerapporteerde eigenschappen is verzonden door Hallo apparaat toohello hub. U kunt deze eigenschappen in de oplossingsportal Hallo weergeven.
- Gewenste eigenschappen die u wilt dat toosend toohello apparaat. U kunt deze eigenschappen instellen in de oplossingsportal Hallo.
- Labels die zich alleen in Hallo apparaat twin en niet op Hallo-apparaat. U kunt deze labels toofilter een lijst met apparaten in de oplossingsportal Hallo gebruiken.

Deze oplossing maakt gebruik van metagegevens van apparaten horende toomanage apparaat. Hallo-oplossing gebruikt ook een Cosmos-DB database toostore extra oplossings-specifieke apparaatgegevens zoals Hallo-opdrachten die door de opdrachtgeschiedenis voor elk apparaat en Hallo ondersteund.

Hallo-oplossing moet Houd er ook informatie Hallo Hallo register met apparaat-id's gesynchroniseerd met de Hallo inhoud van Hallo Cosmos-DB-database. Hallo **EventProcessorHost** maakt gebruik van gegevens van Hallo **DeviceInfo** stream analytics-taak toomanage Hallo synchronisatie.

## <a name="solution-portal"></a>Oplossingsportal

![oplossingsportal][img-dashboard]

Hallo oplossingsportal is een webgebaseerde gebruikersinterface die toohello cloud geïmplementeerd als onderdeel van Hallo vooraf geconfigureerde oplossing. Hiermee kunt u:

* De telemetrie- en waarschuwingsgeschiedenis weergeven in een dashboard.
* Nieuwe apparaten inrichten.
* Apparaten beheren en controleren.
* Opdrachten toospecific apparaten verzenden.
* Methoden aanroepen op specifieke apparaten.
* Regels en acties beheren.
* Plannen van taken toorun op een of meer apparaten.

In deze vooraf geconfigureerde oplossing Hallo oplossingsportal deel uit van Hallo **IoT back-end oplossing** en deel van Hallo **verwerkings- en bedrijfsconnectiviteit** in Hallo typische [IoT-oplossing architectuur][lnk-what-is-azure-iot].

## <a name="next-steps"></a>Volgende stappen

Zie [Microsoft Azure IoT services: Reference Architecture][lnk-refarch] (Microsoft Azure IoT-services: referentiearchitectuur) voor meer informatie over IoT-oplossingsarchitecturen.

Nu u welke vooraf geconfigureerde oplossing weet is, u kunt aan de slag door het implementeren van Hallo *externe controle* vooraf geconfigureerde oplossing: [aan de slag met Hallo vooraf geconfigureerde oplossingen] [ lnk-getstarted-preconfigured].

[img-remote-monitoring-arch]: ./media/iot-suite-what-are-preconfigured-solutions/remote-monitoring-arch1.png
[img-dashboard]: ./media/iot-suite-what-are-preconfigured-solutions/dashboard.png
[lnk-what-is-azure-iot]: iot-suite-what-is-azure-iot.md
[lnk-asa]: https://azure.microsoft.com/documentation/services/stream-analytics/
[lnk-event-processor]: ../event-hubs/event-hubs-programming-guide.md#event-processor-host
[lnk-web-job]: ../app-service-web/web-sites-create-web-jobs.md
[lnk-identity-registry]: ../iot-hub/iot-hub-devguide-identity-registry.md
[lnk-predictive-maintenance]: iot-suite-predictive-overview.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com/
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
[lnk-getstarted-preconfigured]: iot-suite-getstarted-preconfigured-solutions.md
[lnk-c2d-guidance]: ../iot-hub/iot-hub-devguide-c2d-guidance.md
[lnk-device-twin]: ../iot-hub/iot-hub-devguide-device-twins.md
[lnk-direct-methods]: ../iot-hub/iot-hub-devguide-direct-methods.md
[lnk-getstarted-factory]: iot-suite-connected-factory-overview.md
