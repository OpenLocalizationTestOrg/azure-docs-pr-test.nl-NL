---
title: aaaAzure IoT Hub verklarende woordenlijst van termen | Microsoft Docs
description: Handleiding voor ontwikkelaars - een verklarende woordenlijst van algemene termen met betrekking tooAzure IoT Hub.
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 16ef29ea-a185-48c3-ba13-329325dc6716
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: 217eb082c13e06df5c07543c65d498ad3e395939
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="glossary-of-iot-hub-terms"></a>Verklarende woordenlijst van IoT-Hub
In dit artikel vindt u enkele van Hallo algemene termen die worden gebruikt in Hallo IoT Hub artikelen.

## <a name="advanced-message-queueing-protocol"></a>Geavanceerde Message Queueing-Protocol
[Geavanceerde Message Queueing-Protocol (AMQP)](https://www.amqp.org/) is een van de messaging-Hallo protocollen die [IoT Hub](#iot-hub) ondersteunt om te communiceren met apparaten. Zie voor meer informatie over Hallo messaging-protocollen die IoT Hub worden ondersteund, [berichten verzenden en ontvangen met IoT Hub](iot-hub-devguide-messaging.md).

## <a name="azure-cli"></a>Azure CLI
Hallo [Azure CLI](../cli-install-nodejs.md) is een hulpprogramma cross-platform, open-source, op basis van shell-opdracht voor het maken en beheren van resources in Microsoft Azure. Deze versie van Hallo CLI is geïmplementeerd met behulp van Node.js.

## <a name="azure-cli-20"></a>Azure CLI 2.0
Hallo [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2) is een hulpprogramma cross-platform, open-source, op basis van shell-opdracht voor het maken en beheren van resources in Microsoft Azure. Deze preview-versie van Hallo CLI is geïmplementeerd met behulp van Python.


## <a name="azure-iot-device-sdks"></a>Apparaat met Azure IoT SDK 's
Er zijn _apparaat-SKD's_ beschikbaar zijn voor meerdere talen die u in staat toocreate stellen [apparaat-apps](#device-app) die communiceren met een IoT-hub. Hallo IoT Hub zelfstudies ziet u hoe toouse deze apparaat-SDK's. U vindt de broncode Hallo en meer informatie over Hallo apparaat-SKD's in deze GitHub [opslagplaats](https://github.com/Azure/azure-iot-sdks).

## <a name="azure-iot-edge"></a>Azure IoT Edge
IoT-rand kunt u toowrite toepassingen waarmee gateway verbonden apparaten toocommunicate met [IoT Hub](#iot-hub). Hallo IoT rand zelfstudies ziet u hoe toouse deze service. U vindt Hallo broncode en aanvullende informatie over Azure IoT Edge in deze GitHub [opslagplaats](https://github.com/Azure/iot-edge).

## <a name="azure-iot-service-sdks"></a>Azure IoT service SDK 's
Er zijn _service-SDK's_ beschikbaar zijn voor meerdere talen die u in staat toocreate stellen [back-end apps](#back-end-app) die communiceren met een IoT-hub. Hallo IoT Hub zelfstudies ziet u hoe toouse deze service-SDK's. U vindt de broncode Hallo en meer informatie over Hallo service SDK's in deze GitHub [opslagplaats](https://github.com/Azure/azure-iot-sdks).

## <a name="azure-portal"></a>Azure Portal
Hallo [Microsoft Azure-portal](https://portal.azure.com) is een centrale plaats waar u kunt inrichten en beheren van uw Azure-resources. Deze organiseert de inhoud met behulp van _blades_. In sommige Hallo Iothub zelfstudies, wordt u mogelijk gevraagd toouse hello [klassieke Azure-portal](https://manage.windowsazure.com).

## <a name="azure-powershell"></a>Azure PowerShell
[Azure PowerShell](/powershell/azure/overview) is een verzameling van cmdlets kunt u toomanage Azure met Windows PowerShell. Hallo-cmdlets toocreate gebruiken, testen, implementeren en beheren van oplossingen en services die worden aangeboden via hello Azure-platform.

## <a name="azure-resource-manager"></a>Azure Resource Manager
[Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) kunt u toowork met Hallo resources in uw oplossing als een groep. U kunt implementeren, bijwerken of verwijderen van Hallo resources voor uw oplossing in een enkele, gecoördineerde bewerking.

## <a name="azure-service-bus"></a>Azure Service Bus
[Service Bus](../service-bus/index.md) ingeschakeld voor de cloud communicatie met berichtenverzending voor bedrijven en relayed communicatie waarmee u verbinding maken met oplossingen on-premises met Hallo cloud biedt. Sommige zelfstudies IoT Hub maken gebruik van Service Bus [wachtrijen](../service-bus-messaging/service-bus-messaging-overview.md).

## <a name="azure-storage"></a>Azure Storage
[Azure Storage](../storage/common/storage-introduction.md) is een cloudoplossing voor opslag. Bevat Hallo Blob Storage-service waarmee u toostore ongestructureerde kunt objectgegevens. Sommige zelfstudies IoT Hub blob storage gebruiken.

## <a name="back-end-app"></a>Back-endserver voor apps
In de context van Hallo [IoT Hub](#iot-hub), een back-endserver voor apps is een app die verbinding tooone van Hallo gerichte service-eindpunten op een IoT-hub maakt. Bijvoorbeeld een back-endserver voor apps mogelijk opgehaald [apparaat-naar-cloud](#device-to-cloud)berichten of beheren van Hallo [identiteitsregister](#identity-registry). Doorgaans een back-end-app wordt uitgevoerd in de cloud hello, maar in veel Hallo zelfstudies Hallo back-end apps console apps die worden uitgevoerd op uw lokale ontwikkelcomputer zijn.

## <a name="built-in-endpoints"></a>Ingebouwde eindpunten
Elke iothub bevat een ingebouwde [eindpunt](iot-hub-devguide-endpoints.md) die Event Hub-compatibele. U kunt een mechanisme die geschikt is voor Event Hubs tooread apparaat-naar-cloud-berichten van dit eindpunt.

## <a name="cloud-gateway"></a>Cloudgateway
Een cloudgateway-connectiviteit voor apparaten die rechtstreeks kan geen verbinding te kunnen[IoT Hub](#iot-hub). Een cloudgateway wordt gehost in de cloud Hallo in contrast tooa [veldgateway](#field-gateway) die lokale tooyour apparaten wordt uitgevoerd. Een typische gebruiksscenario's voor een cloudgateway is tooimplement protocolvertaling voor uw apparaten.

## <a name="cloud-to-device"></a>Cloud-naar-apparaat
Verwijst toomessages verzonden vanaf een IoT hub tooa aangesloten apparaat. Deze berichten zijn vaak opdrachten die Hallo apparaat tootake een actie instrueren. Zie voor meer informatie [berichten verzenden en ontvangen met IoT Hub](iot-hub-devguide-messaging.md).

## <a name="connection-string"></a>Verbindingsreeks
U gebruikt verbindingsreeksen in uw app code tooencapsulate Hallo vereiste informatie op tooconnect tooan-eindpunt. Een verbindingsreeks bevat doorgaans Hallo-adres van het Hallo-eindpunt en beveiligingsinformatie, maar verbindingsreeks indelingen verschillen voor verschillende services. Er zijn twee typen van de verbindingsreeks die is gekoppeld aan Hallo service IoT Hub:
- *Apparaat-verbindingsreeksen* apparaten tooconnect toohello apparaat gerichte eindpunten op een IoT-hub inschakelen.
- *IoT Hub verbindingsreeksen* tooconnect toohello gerichte service-eindpunten op een IoT-hub back-end-apps inschakelen.

## <a name="custom-endpoints"></a>Aangepaste eindpunten
U kunt aangepaste maken [eindpunten](iot-hub-devguide-endpoints.md) op een IoT hub toodeliver berichten worden verzonden door een [routeringsregel](#routing-rules). Aangepaste eindpunten rechtstreeks verbinding gemaakt tooan Event hub, een Service Bus-wachtrij of een Service Bus-onderwerp.

## <a name="custom-gateway"></a>Aangepaste gateway
Een gateway-connectiviteit voor apparaten die rechtstreeks kan geen verbinding te kunnen[IoT Hub](#iot-hub). U kunt [Azure IoT rand](#azure-iot-edge) toobuild aangepaste gateways die aangepaste logica toohandle berichten, aangepaste protocol conversies en andere verwerking implementeren op Hallo rand.

## <a name="data-point-message"></a>Gegevenspunt bericht
Een gegevenspunt bericht is een [apparaat-naar-cloud](#device-to-cloud) bericht met [telemetrie](#telemetry) gegevens, zoals o snelheid of temperatuur.

## <a name="desired-configuration"></a>Gewenst Configuratiebeheer
In de context Hallo van een [apparaat twin](iot-hub-devguide-device-twins.md), desired configuration toohello volledige set eigenschappen en metagegevens in Hallo apparaat twin die moet worden gesynchroniseerd met de apparaat-Hallo verwijst.

## <a name="desired-properties"></a>Gewenste eigenschappen
In de context Hallo van een [apparaat twin](iot-hub-devguide-device-twins.md), eigenschappen is een subsectie van Hallo apparaat twin dat wordt gebruikt met de gewenste [gerapporteerd eigenschappen](#reported-properties) toosynchronize apparaatconfiguratie of voorwaarde. Gewenste eigenschappen kunnen alleen worden ingesteld door een [back-endserver voor apps](#back-end-app) en zijn waargenomen door Hallo [apparaattoepassing](#device-app).

## <a name="device-to-cloud"></a>Apparaat-naar-cloud
Verzonden vanaf een verbonden apparaat te toomessages verwijst[IoT Hub](#iot-hub). Deze berichten mogelijk [gegevenspunt](#data-point-message) of [interactieve](#interactive-message) berichten. Zie voor meer informatie [berichten verzenden en ontvangen met IoT Hub](iot-hub-devguide-messaging.md).

## <a name="device"></a>Apparaat
In de context van de Hallo van IoT, een apparaat is doorgaans een kleinschalige, zelfstandige computers die kunnen worden verzameld of andere apparaten beheren. Een apparaat zijn mogelijk een milieu bewaking apparaat of een domeincontroller voor Hallo aan en ventilatie systemen in een vergunning. Hallo [apparaat catalogus](https://catalog.azureiotsuite.com/) geeft een lijst van hardware apparaten gecertificeerde toowork met [IoT Hub](#iot-hub).

## <a name="device-app"></a>Apparaat-app
Een apparaat-app wordt uitgevoerd op uw [apparaat](#device) en ingangen Hallo communicatie met uw [IoT-hub](#iot-hub). Normaal gesproken gebruikt u een van de Hallo [apparaat Azure IoT SDK's](#azure-iot-device-sdks) bij het implementeren van een apparaat-app. In veel van Hallo IoT zelfstudies, gebruikt u een [gesimuleerd apparaat](#simulated-device) voor uw gemak.

## <a name="device-condition"></a>Voorwaarde van apparaat
Toodevice staat informatie, zoals Hallo verbindingsmethode momenteel in gebruik is, verwijst, zoals gemeld door een [apparaattoepassing](#device-app). [Apparaat-apps](#device-app) kunnen ook hun mogelijkheden rapporteren. U kunt een query voor de voorwaarde en de mogelijkheid om gegevens door middel van horende apparaten.

## <a name="device-data"></a>Apparaatgegevens
Apparaatgegevens verwijst toohello per apparaat opgeslagen gegevens in IoT Hub Hallo [identiteitsregister](#identity-registry). Het is mogelijk tooimport en deze gegevens exporteren.

## <a name="device-explorer"></a>Apparaat explorer
Hallo [apparaat explorer](https://github.com/Azure/azure-iot-sdk-csharp/tree/master/tools/DeviceExplorer) is een hulpprogramma dat wordt uitgevoerd op Windows en kunt u toomanage uw apparaten in Hallo [identiteitsregister](#identity-registry).hello hulpprogramma ook verzenden en ontvangen berichten tooyour apparaten.

## <a name="device-identities-rest-api"></a>REST-API voor apparaatidentiteiten
Hallo [apparaat identiteiten REST-API](https://docs.microsoft.com/rest/api/iothub/iothubresource) kunt u uw apparaten geregistreerd in Hallo toomanage [identiteitsregister](#identity-registry) met behulp van een REST-API. Normaal gesproken moet u een hoger niveau Hallo [service-SDK's](#azure-iot-service-sdks) zoals weergegeven in Hallo zelfstudies IoT Hub.

## <a name="device-identity"></a>Apparaat-id
Hallo apparaat-id Hallo unieke id toegewezen tooevery apparaat is geregistreerd in Hallo [identiteitsregister](#identity-registry).

## <a name="device-management"></a>Apparaatbeheer
Beheer van apparaten omvat de volledige levenscyclus Hallo die zijn gekoppeld aan het beheer van apparaten in uw IoT-oplossing met inbegrip van de planning, inrichten, configureren, bewaken en buiten gebruik stellen van Hallo.

## <a name="device-management-patterns"></a>Patronen voor apparaatbeheer
[IoT-hub](#iot-hub) kunnen algemene apparaat management patronen, zoals opnieuw op te starten, uitvoeren van de fabrieksinstellingen herstellen en firmware-updates uitvoeren op uw apparaten.

## <a name="device-messaging-rest-api"></a>REST-API voor apparaatmessaging
U kunt Hallo [apparaat Messaging REST-API](https://docs.microsoft.com/rest/api/iothub/httpruntime) van een apparaat toosend apparaat-naar-cloud tooan iothub berichten en ontvangen [cloud-naar-apparaat](#cloud-to-device) berichten van een IoT-hub. Normaal gesproken moet u een hoger niveau Hallo [apparaat-SKD's](#azure-iot-device-sdks) zoals weergegeven in Hallo zelfstudies IoT Hub.

## <a name="device-provisioning"></a>Mobiele apparaten inrichten
Apparaat inrichting is Hallo toe te voegen Hallo initiële [apparaatgegevens](#device-data) toohello worden opgeslagen in uw oplossing. een nieuwe apparaat tooconnect tooyour hub tooenable, moet u een apparaat-ID en sleutels toohello IoT Hub toevoegen [identiteitsregister](#identity-registry). Als onderdeel van Hallo inrichtingsproces, moet u mogelijk tooinitialize apparaatspecifieke gegevens in andere archieven oplossing.

## <a name="device-twin"></a>Dubbel apparaat
Een [apparaat twin](iot-hub-devguide-device-twins.md) JSON-document dat apparaat statusinformatie zoals metagegevens, configuraties en voorwaarden slaat is. [IoT Hub](#iot-hub) een apparaat twin voor elk apparaat dat u in uw IoT-hub inrichten zich blijft voordoen. Apparaat horende kunnen u toosynchronize [apparaat voorwaarden](#device-condition) en configuraties tussen Hallo-apparaat en Hallo oplossing back-end. U kunt query apparaat horende toolocate specifieke apparaten en query Hallo status van langlopende bewerkingen.

## <a name="device-twin-queries"></a>Apparaat twin query 's
[Apparaat twin query's](iot-hub-devguide-query-language.md) Hallo IoT-Hub SQL-achtige query taal tooretrieve gegevens van uw horende apparaten gebruiken. U kunt dezelfde IoT Hub taal tooretrieve informatie opvragen over Hallo [taken](#job) uitgevoerd in uw IoT-hub.

## <a name="device-twin-rest-api"></a>Apparaat Twin REST-API
Kunt u Hallo [apparaat Twin REST-API](https://docs.microsoft.com/rest/api/iothub/devicetwinapi) van Hallo oplossing back-endnetwerk toomanage uw horende apparaten. Hallo API kunt u tooretrieve en update [apparaat twin](#device-twin) eigenschappen en oproepen [methoden directe](#direct-method). Normaal gesproken moet u een hoger niveau Hallo [service-SDK's](#azure-iot-service-sdks) zoals weergegeven in Hallo zelfstudies IoT Hub.

## <a name="device-twin-synchronization"></a>Synchronisatie van apparaten twin
Synchronisatie van apparaten twin gebruikt Hallo [gewenst eigenschappen](#desired-properties) in uw apparaat horende tooconfigure uw apparaten en ophalen [eigenschappen gerapporteerd](#reported-properties) van uw apparaten toostore in Hallo apparaat twin.

## <a name="direct-method"></a>Directe methode
Een [directe methode](iot-hub-devguide-direct-methods.md) is een manier waarop u tootrigger een tooexecute methode op een apparaat door het aanroepen van een API op uw IoT-hub.

## <a name="endpoint"></a>Eindpunt
Een iothub toont meerdere [eindpunten](iot-hub-devguide-endpoints.md) die ervoor zorgen dat uw apps tooconnect toohello IoT-hub. Er zijn apparaat gerichte eindpunten waarmee apparaten tooperform bewerkingen zoals het zenden van [apparaat-naar-cloud](#device-to-cloud) berichten en ontvangst [cloud-naar-apparaat](#cloud-to-device) berichten. Er zijn service gerichte management eindpunten waarmee [back-end apps](#back-end-app) tooperform-bewerkingen zoals [apparaat-id](#device-identity) beheer- en Apparaatbeheer twin. Er zijn service gerichte [ingebouwde eindpunten](#built-in-endpoints) voor het lezen van apparaat-naar-cloud-berichten. U kunt maken [aangepaste eindpunten](#custom-endpoints) tooreceive apparaat-naar-cloud-berichten is verzonden door een [routeringsregel](#routing-rules).

## <a name="event-hubs-service"></a>Event Hubs-service
[Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md) is een uiterst schaalbare gegevens ingress-service die, miljoenen opnemen kan gebeurtenissen per seconde. Hallo-service kunt u tooprocess en analyseren van Hallo enorme hoeveelheden gegevens die worden geproduceerd door verbonden apparaten en toepassingen. Zie voor een vergelijking met Hallo service IoT Hub [vergelijking van Azure IoT Hub en Azure Event Hubs](iot-hub-compare-event-hubs.md).

## <a name="event-hub-compatible-endpoint"></a>Event Hub-compatibele eindpunt
tooread [apparaat-naar-cloud](#device-to-cloud) berichten verzonden tooyour iothub, kunt u verbinding maken met eindpunt tooan op uw hub en gebruiken van een Event Hub-compatibele methode tooread die berichten. Event Hub-compatibele methoden omvatten het gebruik van Hallo [Event Hubs SDK's](../event-hubs/event-hubs-programming-guide.md) en [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md).

## <a name="field-gateway"></a>Veldgateway
Een veldgateway connectiviteit voor apparaten die rechtstreeks kan geen verbinding te kan[IoT Hub](#iot-hub) en meestal lokaal is geïmplementeerd in uw apparaten. Zie voor meer informatie [wat is Azure IoT Hub?](iot-hub-what-is-iot-hub.md)

## <a name="free-account"></a>Gratis account
Kunt u een [gratis Azure-account](https://azure.microsoft.com/pricing/free-trial/) toocomplete Hallo IoT Hub zelfstudies en Experimenteer met Hallo service IoT Hub (en andere Azure-services).

## <a name="gateway"></a>Gateway
Een gateway-connectiviteit voor apparaten die rechtstreeks kan geen verbinding te kunnen[IoT Hub](#iot-hub). Zie ook [veld Gateway](#field-gateway), [Gateway Cloud](#cloud-gateway), en [aangepaste Gateway](#custom-gateway).

## <a name="identity-registry"></a>ID-register
Hallo [identiteitsregister](iot-hub-devguide-identity-registry.md) Hallo ingebouwde onderdeel van een IoT-hub die wordt opgeslagen informatie over afzonderlijke apparaten Hallo tooconnect tooan iothub toegestaan.

## <a name="interactive-message"></a>Interactieve bericht
Een interactieve bericht is een [cloud-naar-apparaat](#cloud-to-device) bericht dat een onmiddellijke actie in Hallo back-end oplossing activeert. Een apparaat kan bijvoorbeeld een waarschuwing over een fout die automatisch moet worden vastgelegd in tooa CRM-systeem te verzenden.

## <a name="iot-hub"></a>IoT Hub
IoT Hub is een volledig beheerde Azure-service die stabiele en veilige tweerichtingscommunicatie tussen miljoenen apparaten maakt en een back-end oplossing. Zie voor meer informatie [wat is Azure IoT Hub?](iot-hub-what-is-iot-hub.md) Met behulp van uw [Azure-abonnement](#subscription), kunt u IoT hubs toohandle uw IoT messaging-werkbelastingen.

## <a name="iot-hub-metrics"></a>IoT Hub metrische gegevens
[IoT Hub metrische gegevens](iot-hub-metrics.md) bieden u de gegevens over de status Hallo Hallo IoT hubs in uw [Azure-abonnement](#subscription). IoT Hub metrische gegevens inschakelen u tooassess algemene status van het Hallo-service en Hallo apparaten Hallo verbonden tooit. IoT Hub metrische gegevens kunt u zien wat er gebeurt met uw IoT-hub en onderzoeken van problemen met de hoofdoorzaak zonder toocontact ondersteuning van Azure.

## <a name="iot-hub-query-language"></a>IoT Hub-querytaal
Hallo [IoT Hub-querytaal](iot-hub-devguide-query-language.md) is een SQL-achtige taal waarmee u tooquery uw [taken](#job) en horende apparaten.

## <a name="iot-hub-resource-provider-rest-api"></a>Resourceprovider IoT-Hub REST-API
U kunt Hallo [IoT Hub Resource Provider REST-API](https://docs.microsoft.com/rest/api/iothub/resourceprovider/iot-hub-resource-provider-rest) toomanage Hallo IoT hubs in uw [Azure-abonnement](#subscription) uitvoeren van bewerkingen zoals het maken, bijwerken en verwijderen van hubs.

## <a name="iot-suite"></a>IoT Suite
Azure IoT Suite-pakketten meerdere Azure-services met vooraf geconfigureerde oplossingen. Deze vooraf geconfigureerde oplossingen inschakelen tooget u snel de slag met end-to-end-implementaties van algemene IoT-scenario's. Zie voor meer informatie [wat is Azure IoT Suite?](../iot-suite/iot-suite-overview.md)

## <a name="iothub-explorer"></a>iothub explorer
Hallo [iothub explorer](https://github.com/azure/iothub-explorer) is een platformoverschrijdende, opdrachtregel-hulpprogramma. Hallo-hulpprogramma kunt u toomanage uw apparaten in Hallo [identiteitsregister](#identity-registry), verzenden en ontvangen van berichten en bestanden van uw apparaten en uw IoT hub-bewerkingen te controleren.

## <a name="job"></a>Job
De back-end van uw oplossing kunt [taken](iot-hub-devguide-jobs.md) tooschedule en bijhouden activiteiten in een reeks apparaten die zijn geregistreerd bij uw IoT-hub. Activiteiten omvatten apparaat twin bijwerken [gewenst eigenschappen](#desired-properties), bijwerken apparaat twin [labels](#tags), en het aanroepen van [methoden directe](#direct-method). [IoT Hub](#iot-hub) gebruikt ook de taken te[import/export tooand](iot-hub-devguide-identity-registry.md#import-and-export-device-identities) van Hallo [identiteitsregister](#identity-registry).

## <a name="jobs-rest-api"></a>Taken REST-API
Hallo [taken REST-API](https://docs.microsoft.com/rest/api/iothub/jobapi) kunt u toomanage [taken](#job) uitgevoerd in uw IoT-hub.

## <a name="module"></a>Module
In [Azure IoT rand](iot-hub-linux-iot-edge-get-started.md), een [module](iot-hub-linux-iot-edge-get-started.md) is een onderdeel dat een specifieke taak uitvoert. Taken kunnen omvatten het opnemen van een bericht van een apparaat, een bericht transformeren of verzenden van een bericht tooan IoT-hub. Een broker is verantwoordelijk voor het doorsturen van berichten tussen modules. Azure IoT-rand bevat een set van voorbeeld-modules. U kunt ook uw eigen aangepaste modules maken.

## <a name="mqtt"></a>MQTT
[MQTT](http://mqtt.org/) is een van de messaging-Hallo protocollen die [IoT Hub](#iot-hub) ondersteunt om te communiceren met apparaten. Zie voor meer informatie over Hallo messaging-protocollen die IoT Hub worden ondersteund, [berichten verzenden en ontvangen met IoT Hub](iot-hub-devguide-messaging.md).

## <a name="operations-monitoring"></a>Controle van bewerkingen
IoT Hub [operations bewaking](iot-hub-operations-monitoring.md) kunt u de status van de toomonitor Hallo van bewerkingen voor uw IoT-hub in realtime. [IoT Hub](#iot-hub) gebeurtenissen worden bijgehouden in verscheidene categorieën van bewerkingen. U kunt kiezen voor het verzenden van gebeurtenissen uit een of meer categorieën tooan IoT Hub-eindpunt voor verwerking. U kunt bewaken Hallo gegevens op fouten of complexe verwerking op basis van gegevenspatronen instellen.

## <a name="physical-device"></a>Fysiek apparaat
Een fysiek apparaat is een echte apparaat zoals een frambozen Pi die verbinding tooan IoT-hub maakt. Veel van de Iothub-zelfstudies hello gebruiken voor het gemak [gesimuleerde apparaten](#simulated-device) tooenable u toorun op uw lokale machine voorbeelden.

## <a name="primary-and-secondary-keys"></a>Primaire en secundaire sleutels
Wanneer u verbinding maakt tooa apparaat gerichte of gerichte service-eindpunt op een IoT-hub uw [verbindingsreeks](#connection-string) bevat belangrijke toogrant u openen. Bij het toevoegen van een apparaat toohello [identiteitsregister](#identity-registry) of Voeg een [gedeeld toegangsbeleid](#shared-access-policy) tooyour hub, Hallo service genereert een primaire en secundaire sleutel. Twee sleutels, kunt u tooroll via uit één sleutel tooanother wanneer u een sleutel bijwerken zonder verlies van toegang toohello IoT-hub.

## <a name="protocol-gateway"></a>Protocolgateway
Een protocolgateway wordt meestal geïmplementeerd in Hallo cloud en protocol vertaling services biedt voor de apparaten die verbinding te maken[IoT Hub](#iot-hub). Zie voor meer informatie [wat is Azure IoT Hub?](iot-hub-what-is-iot-hub.md)

## <a name="quotas-and-throttling"></a>Quota en beperkingen
Er zijn verschillende [quota](iot-hub-devguide-quotas-throttling.md) die van toepassing zijn tooyour gebruik van [IoT Hub](#iot-hub)veel Hallo quota's variëren op basis van het Hallo-laag van Hallo iothub. [IoT Hub](#iot-hub) ook van toepassing [bandbreedte](iot-hub-devguide-quotas-throttling.md) tooyour Hallo service gebruiken tijdens de uitvoering.

## <a name="reported-configuration"></a>Gerapporteerde configuratie
In de context Hallo van een [apparaat twin](iot-hub-devguide-device-twins.md), gemelde configuratie verwijst toohello volledige set eigenschappen en metagegevens in Hallo apparaat twin die moet worden gerapporteerd toohello back-end oplossing.

## <a name="reported-properties"></a>Gerapporteerde eigenschappen
In de context Hallo van een [apparaat twin](iot-hub-devguide-device-twins.md), gerapporteerd eigenschappen is een subsectie van Hallo apparaat twin gebruikt met [gewenst eigenschappen](#desired-properties) toosynchronize apparaatconfiguratie of voorwaarde. Eigenschappen kunnen alleen worden ingesteld door Hallo gerapporteerd [apparaattoepassing](#device-app) en kan worden gelezen en een query uitgevoerd door een [back-endserver voor apps](#back-end-app).

## <a name="resource-group"></a>Resourcegroep
[Azure Resource Manager](#azure-resource-manager) maakt gebruik van resource groepen toogroup verwante resources samen. U kunt een resource groep tooperform bewerkingen op alle Hallo bronnen op Hallo groep gelijktijdig gebruiken.

## <a name="retry-policy"></a>Beleid voor opnieuw proberen
Gebruik van een beleid voor opnieuw proberen toohandle [tijdelijke fouten](https://msdn.microsoft.com/library/hh680901(v=pandp.50).aspx) wanneer u verbinding maakt tooa-cloudservice.

## <a name="routing-rules"></a>Regels voor het doorsturen
U configureert [routeringsregels](iot-hub-devguide-messages-read-custom.md) in uw IoT hub tooroute apparaat-naar-cloudberichten tooa [ingebouwd eindpunt](#built-in-endpoints) of te[aangepaste eindpunten](#custom-endpoints) voor verwerking door de back-oplossing einde.

## <a name="sasl-plain"></a>SASL ZONDER OPMAAK
SASL zonder opmaak is een protocol dat Hallo [AMQP](#advanced-message-queue-protocol) protocol gebruikt de beveiligingstokens tootransfer.

## <a name="shared-access-signature"></a>Shared access signature voor
Shared Access Signatures (SAS) zijn een verificatiemethode op basis van beveiligde SHA-256-hashes of URI's. SAS verificatie bestaat uit twee onderdelen: een _beleid voor gedeelde toegang_ en een _Shared Access Signature_ (vaak een token genoemd). Een apparaat gebruikt SAS tooauthenticate met een IoT-hub. [Back-end apps](#back-end-app) SAS tooauthenticate ook gebruiken met Hallo gerichte service-eindpunten op een IoT-hub. Normaal gesproken het opnemen van Hallo SAS-token in Hallo [verbindingsreeks](#connection-string) dat een app gebruikmaakt van een verbinding tooan IoT-hub tooestablish.

## <a name="shared-access-policy"></a>Beleid voor gedeelde toegang
Een gedeeld toegangsbeleid definieert Hallo machtigingen verleend tooanyone die een geldige heeft [primaire of secundaire sleutel](#primary-and-secondary-keys) die zijn gekoppeld aan dit beleid. U kunt Hallo gedeeld toegangsbeleid en sleutels beheren voor uw hub in Hallo [portal](#azure-portal).

## <a name="simulated-device"></a>Gesimuleerd apparaat
Voor het gemak veel van de IoT Hub zelfstudies gebruiken Hallo gesimuleerde apparaten tooenable u toorun op uw lokale machine voorbeelden. Daarentegen een [fysiek apparaat](#physical-device) is een echte apparaat zoals een frambozen Pi die verbinding tooan IoT-hub maakt.

## <a name="solution"></a>Oplossing
Een _oplossing_ tooa Visual Studio-oplossing met een of meer projecten kunnen verwijzen. Een _oplossing_ mogelijk ook tooan IoT-oplossing met elementen zoals apparaten, verwijzen [apparaat-apps](#device-app), een IoT-hub, andere Azure-services en [back-end apps](#back-end-app).

## <a name="subscription"></a>Abonnement
Een Azure-abonnement is waar facturering plaatsvindt. Elke Azure-resource die u maakt of Azure service waarmee u is gekoppeld aan één abonnement. Veel quota's zijn ook van toepassing op Hallo niveau van een abonnement.

## <a name="system-properties"></a>Systeemeigenschappen
In de context Hallo van een [apparaat twin](iot-hub-devguide-device-twins.md), Systeemeigenschappen zijn alleen-lezen en bevatten informatie over het gebruik van het apparaat Hallo zoals laatste status van activiteit tijd en de verbinding.

## <a name="tags"></a>Tags
In de context Hallo van een [apparaat twin](iot-hub-devguide-device-twins.md), labels, zijn de Apparaatmetagegevens van het opgeslagen en opgehaald door Hallo back-end oplossing in Hallo vorm van een JSON-document. Labels zijn niet zichtbaar tooapps op een apparaat.

## <a name="telemetry"></a>Telemetrie
Apparaten telemetriegegevens, zoals o snelheid of temperatuur, verzamelen en gebruiken [gegevenspunt berichten](#data-point-messages) toosend Hallo telemetrie tooan IoT-hub.

## <a name="token-service"></a>Service voor beveiligingstokens
U kunt een service voor beveiligingstokens tooimplement verificatiemechanisme voor uw apparaten. Dit maakt gebruik van een IoT-Hub [gedeeld toegangsbeleid](#shared-access-policy) met **DeviceConnect** machtigingen toocreate *binnen het bereik van apparaat* tokens. Deze tokens inschakelen voor een apparaat tooconnect tooyour IoT-hub. Een apparaat gebruikt een mechanisme voor aangepaste verificatie tooauthenticate met Hallo beveiligingstokenservice. Als het Hallo-apparaat is geverifieerd, Hallo token service geeft een SAS-token voor Hallo apparaat toouse tooaccess uw IoT-hub.

## <a name="x509-client-certificate"></a>X.509-certificaat
Een apparaat kan gebruiken een x.509-certificaat tooauthenticate met [IoT Hub](#iot-hub). Met behulp van een X.509-certificaat is een alternatieve toousing een [SAS-token](#shared-access-signature).
