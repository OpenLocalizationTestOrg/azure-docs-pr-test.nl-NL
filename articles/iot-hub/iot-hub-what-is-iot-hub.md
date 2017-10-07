---
title: overzicht van IoT Hub aaaAzure | Microsoft Docs
description: 'Overzicht van Hallo service Azure IoT Hub: Wat is IoT Hub, verbindingsmogelijkheden voor apparaten, internet der dingen communicatiepatronen, gateways en Hallo service-ondersteunde communicatiepatronen'
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 24376318-5344-4a81-a1e6-0003ed587d53
ms.service: iot-hub
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d0b46868a1ec9e13c8f107b90269c5307f4ba27c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="overview-of-hello-azure-iot-hub-service"></a>Overzicht van de service Azure IoT Hub Hallo

Welkom tooAzure IoT Hub. In dit artikel biedt een overzicht van Azure IoT Hub en beschrijft waarom moet u deze service tooimplement een oplossing voor Internet der dingen (IoT). Azure IoT Hub is een volledig beheerde service die stabiele en veilige tweerichtingscommunicatie tussen miljoenen IoT-apparaten en de back-end van een oplossing mogelijk maakt. Azure IoT Hub:

* Biedt meerdere opties voor communicatie van apparaat naar cloud en cloud naar apparaat, waaronder berichten in één richting en methoden voor aanvraag/antwoord.
* Biedt ingebouwde declaratieve bericht routering tooother Azure-services.
* Biedt opslag waarop query's kunnen worden uitgevoerd voor apparaatmetagegevens en informatie over de gesynchroniseerde status.
* Maakt veilige communicatie en toegangsbeheer mogelijk met behulp van beveiligingssleutels of X.509-certificaten per apparaat.
* Biedt uitgebreide bewaking voor verbindingsmogelijkheden van apparaten en gebeurtenissen voor het beheren van apparaat-id’s.
* Apparaatbibliotheken voor Hallo meest populaire talen en platforms.

Hallo artikel [vergelijking van IoT Hub en Event Hubs] [ lnk-compare] beschrijft de belangrijkste verschillen tussen deze twee services Hallo en markeert Hallo voordelen van het gebruik van IoT-Hub in uw IoT-oplossingen.

Zie voor meer informatie over hoe Azure- en IoT-Hub te beveiligen van uw IoT-oplossing, [beveiliging van Internet der dingen van Hallo gemalen][lnk-security-ground-up].

![Azure IoT-Hub als cloudgateway in IoT-oplossing][img-architecture]

> [!NOTE]
> Zie voor een gedetailleerdere beschrijving van IoT-architectuur Hallo [Microsoft Azure IoT Reference Architecture][lnk-refarch].

## <a name="iot-device-connectivity-challenges"></a>Uitdagingen met de connectiviteit van IoT-apparaten

IoT Hub en Hallo apparaatbibliotheken kunnen u toomeet Hallo uitdagingen van hoe tooreliably en veilig verbinding apparaten toohello back-end oplossing. IoT-apparaten:

* Zijn vaak ingesloten systemen waarbij geen menselijke operator komt kijken.
* Kunnen zich op afgelegen locaties bevinden, waar fysieke toegang kostbaar is.
* Kan alleen worden bereikt via Hallo back-end oplossing.
* Hebben mogelijk een beperkt vermogen en een beperkt aantal verwerkingsbronnen.
* Hebben mogelijk een onstabiele, trage of dure netwerkverbinding.
* Mogelijk moet toouse bedrijfseigen, aangepaste of branchespecifieke toepassingsprotocollen.
* Kunnen worden gemaakt met behulp van een groot aantal populaire hardware- en softwareplatforms.

Bovendien toohello bovenstaande vereisten een IoT-oplossing moet ook leveren schaal, beveiliging en betrouwbaarheid. Hallo resulterende reeks connectiviteitsvereisten is moeilijk en tijdrovend tooimplement wanneer u conventionele technologieën, zoals webcontainers en berichtenbrokers.

## <a name="why-use-azure-iot-hub"></a>Waarom Azure IoT Hub gebruiken?

Bovendien tooa uitgebreide set [apparaat-naar-cloud] [ lnk-d2c-guidance] en [cloud-naar-apparaat] [ lnk-c2d-guidance] communicatieopties, met inbegrip van berichten, bestanden overdrachten en request-reply-methoden, adressen van Azure IoT Hub Hallo uitdagingen van de connectiviteit van apparaten in de volgende manieren Hallo:

* **Apparaatdubbels**. Met behulp van [apparaatdubbels][lnk-twins] kunt u metagegevens en statusinformatie van een apparaat opslaan en synchroniseren en er query's op uitvoeren. Apparaatdubbels zijn JSON-documenten waarin statusinformatie van een apparaat (metagegevens, configuraties en voorwaarden) zijn opgeslagen. IoT Hub persistente een apparaat twin voor elk apparaat dat u verbinding tooIoT Hub maakt.

* **Verificatie per apparaat en beveiligde verbindingen**. U kunt elk apparaat met een eigen inrichten [beveiligingssleutel] [ lnk-devguide-security] tooenable het tooconnect tooIoT Hub. Hallo [id-register IoT Hub] [ lnk-devguide-identityregistry] apparaat-id's en sleutels worden opgeslagen in een oplossing. Een back-end oplossing kan afzonderlijke apparaten tooallow toevoegen of lijsten tooenable volledige controle over apparaten toegang te weigeren.

* **Route apparaat-naar-cloud-berichten tooAzure services op basis van declaratieve regels**. IoT-Hub kunt u toodefine bericht routes op basis van routering regels toocontrol waar uw hub apparaat-naar-cloud-berichten verzendt. Routeringsregels geen nodig toowrite u code en kunnen plaatsvinden Hallo van aangepaste na opname bericht coördinatoren.

* **Bewaking van connectiviteitsbewerkingen van apparaten**. U kunt gedetailleerde bewerkingslogboeken over bewerkingen in het beheer van apparaat-id’s en connectiviteitsgebeurtenissen van apparaten ontvangen. Deze bewakingsmogelijkheid kan uw IoT-oplossing tooidentify verbindingsproblemen, zoals apparaten die proberen tooconnect met de verkeerde referenties te vaak berichten verzenden of weigeren alle cloud-naar-apparaat-berichten.

* **Een uitgebreide reeks apparaatbibliotheken**. [Apparaat-SDK's van Azure IoT][lnk-device-sdks] zijn beschikbaar en worden ondersteund in verscheidene talen en door diverse platforms: C voor veel Linux-distributies, Windows en real-time besturingssystemen. Apparaat-SDK’s van Azure IoT ondersteunen tevens beheerde talen, zoals C#, Java en JavaScript.

* **IoT-protocollen en uitbreidingsmogelijkheden**. Als uw oplossing niet kan apparaatbibliotheken hello, toont IoT Hub een openbare protocol waarmee apparaten toonatively gebruik Hallo protocollen MQTT v3.1.1, HTTP 1.1 of AMQP 1.0-protocollen. U kunt toosupport voor aangepaste protocollen door IoT Hub ook uitbreiden:

  * Maak een veldgateway met [Azure IoT rand] [ lnk-iot-edge] die uw aangepaste protocol tooone Hallo drie protocollen begrepen door de IoT Hub worden geconverteerd.
  * Aanpassen Hallo [protocolgateway van Azure IOT][protocol-gateway], een open source-component die wordt uitgevoerd in de cloud Hallo.

* **Schalen**. Azure IoT Hub schaalt toomillions van gelijktijdig verbonden apparaten en miljoenen gebeurtenissen per seconde.

## <a name="gateways"></a>Gateways

Een gateway in een IoT-oplossing is doorgaans een [protocolgateway] [ lnk-iotedge] die wordt geïmplementeerd in de cloud hello of een [veldgateway] [ lnk-field-gateway] is die lokaal is geïmplementeerd met uw apparaten. Een protocolgateway voert protocolgateway vertaalt protocollen, bijvoorbeeld MQTT tooAMQP. Een veldgateway kan analyses uitvoeren op Hallo edge, beslissingen tijdgebonden tooreduce latentie, apparaatbeheerservices bieden, beveiligings-en privacybeperkingen opleggen en protocolvertaling ook uitvoeren. Beide gatewaytypen fungeren als schakels tussen uw apparaten en uw IoT-hub.

Een veldgateway onderscheidt zich van een eenvoudig verkeersrouteringsapparaat (zoals een apparaat voor netwerkadresomzetting of firewall) doordat deze doorgaans een actieve rol speelt bij het beheren van de toegang en de informatiestroom in uw oplossing.

Een oplossing kan zowel een protocolgateway als een veldgateway bevatten.

## <a name="how-does-iot-hub-work"></a>Hoe werkt IoT Hub?

Azure IoT Hub implementeert Hallo [service-ondersteunde communicatie] [ lnk-service-assisted-pattern] patroon toomediate Hallo interacties tussen uw apparaten en uw oplossing voor back-end. Hallo-doel van de service-ondersteunde communicatie is tooestablish betrouwbaar, tweerichtingscommunicatiepaden tussen een besturingssysteem, zoals IoT Hub en apparaten voor speciale doeleinden die zijn geïmplementeerd in niet-vertrouwde fysieke ruimte. Hallo patroon gaat Hallo principes van de volgende:

* Beveiliging gaat voor alle andere functies.

* Apparaten accepteren geen ongevraagde netwerkinformatie. Een apparaat brengt alle verbindingen tot stand en routeert alleen uitgaand verkeer. Voor een tooreceive apparaat een opdracht van Hallo back-end oplossing moet Hallo-apparaat een verbinding toocheck voor alle opdrachten die in behandeling tooprocess regelmatig opnieuw.

* Apparaten moeten alleen verbinding maken met tooor tot stand brengen van de routes toowell bekende services brengen met, zoals IoT Hub.

* Hallo communicatiepad tussen het apparaat en de service of tussen apparaat en de gateway is beveiligd op de toepassingslaag protocol Hallo.

* Autorisatie en verificatie op systeemniveau geschiedt op basis van de id van een apparaat. Hierdoor kunnen toegangsreferenties en machtigingen bijna onmiddellijk worden ingetrokken.

* Tweerichtingscommunicatie tussen apparaten die verbinding maken met sporadisch vanwege toopower of verbindingen betreft proces wordt vergemakkelijkt door opdrachten en apparaatmeldingen totdat een apparaat verbinding tooreceive maakt ze. IoT Hub heeft apparaatspecifieke wachtrijen voor het Hallo-opdrachten die worden verzonden.

* De nettolading van toepassingsgegevens, afzonderlijk worden verzonden via gateways tooa bepaalde service is beveiligd.

Hallo mobiele industrie heeft gebruikt Hallo service-ondersteunde communicatiepatronen bij zeer grote schaal tooimplement push notification services zoals [Windows Push Notification Services][lnk-wns], [Google Cloud Messaging][lnk-google-messaging], en [Apple Push Notification Service][lnk-apple-push].

IoT Hub wordt via het openbare-peeringpad van ExpressRoute ondersteund.

## <a name="next-steps"></a>Volgende stappen

toolearn hoe toosend van berichten van een apparaat en ontvangen van IoT Hub, evenals hoe tooconfigure bericht routeert, Zie [berichten verzenden en ontvangen met IoT Hub][lnk-send-messages].

toolearn hoe IoT-Hub maakt op standaarden gebaseerde Apparaatbeheer mogelijk voor u tooremotely beheren, configureren en bijwerken van uw apparaten, Zie [overzicht van Apparaatbeheer met IoT Hub][lnk-device-management].

tooimplement clienttoepassingen op een groot aantal hardwareplatforms en besturingssystemen, kunt u apparaat-hello Azure IoT SDK's. Hallo apparaat-SDK's bevatten bibliotheken die vergemakkelijken verzenden telemetrie tooan IoT hub en ontvangst cloud-naar-apparaat-berichten. Wanneer u Hallo apparaat-SDK's gebruikt, kunt u kiezen uit diverse netwerk protocollen toocommunicate met IoT Hub. meer, Zie Hallo toolearn [informatie over apparaat-SKD's][lnk-device-sdks].

schrijven van code en enkele voorbeelden uitvoeren gestart tooget Zie Hallo [aan de slag met IoT Hub] [ lnk-get-started] zelfstudie.

[img-architecture]: media/iot-hub-what-is-iot-hub/hubarchitecture.png

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[protocol-gateway]: https://github.com/Azure/azure-iot-protocol-gateway/blob/master/README.md
[lnk-service-assisted-pattern]: http://blogs.msdn.com/b/clemensv/archive/2014/02/10/service-assisted-communication-for-connected-devices.aspx "Serviceondersteunde communicatie, blogpost van Clemens Vasters"
[lnk-compare]: iot-hub-compare-event-hubs.md
[lnk-iotedge]: iot-hub-protocol-gateway.md
[lnk-field-gateway]: iot-hub-devguide-endpoints.md#field-gateways
[lnk-devguide-identityregistry]: iot-hub-devguide-identity-registry.md
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-wns]: https://msdn.microsoft.com/library/windows/apps/mt187203.aspx
[lnk-google-messaging]: https://developers.google.com/cloud-messaging/
[lnk-apple-push]: https://developer.apple.com/library/ios/documentation/NetworkingInternet/Conceptual/RemoteNotificationsPG/Chapters/ApplePushService.html#//apple_ref/doc/uid/TP40008194-CH100-SW9
[lnk-device-sdks]: https://github.com/Azure/azure-iot-sdks
[lnk-refarch]: http://download.microsoft.com/download/A/4/D/A4DAD253-BC21-41D3-B9D9-87D2AE6F0719/Microsoft_Azure_IoT_Reference_Architecture.pdf
[lnk-iot-edge]: https://github.com/Azure/iot-edge
[lnk-send-messages]: iot-hub-devguide-messaging.md
[lnk-device-management]: iot-hub-device-management-overview.md

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[lnk-security-ground-up]: iot-hub-security-ground-up.md
